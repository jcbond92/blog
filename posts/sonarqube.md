---
title: Lightweight SonarQube scanning for frontend projects in Jenkins
description: A simple way to run scans with SonarQube in Jenkins
date: 2022-01-31
tags:
  - Jenkins
layout: layouts/post.njk
---

I've been working in Jenkins a lot lately to refine the build process for a product I'm working on. Last month, a request came in for us to integrate [SonarQube](https://www.sonarqube.org/) (which does static code analysis to help increase code quality and the security of your application).

It's a great tool, but since our codebase is mostly front-end code (e.g. React, Angular, etc.), the Docker images we were using for our builds didn't have all the [Java dependencies readily installed](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/) to run `sonar-scanner`. 

## Simplifying with the official Docker image
I worked for a couple of hours trying to get the `sonarqube-scanner` [Node.js package](https://www.npmjs.com/package/sonarqube-scanner) to work in our existing build process (we use Node.js on an Alpine Linux image), but for one reason or another I had trouble getting it to work when starting from a Node.js-specific image rather than a Java-specific image (which was not an ideal solution).

After some research, I decided to use [SonarSource's official Docker image](https://hub.docker.com/r/sonarsource/sonar-scanner-cli) to simplify the process. This image has `sonar-scanner` and all of it’s dependencies pre-installed, so there isn’t much to configure, other than adding your SonarQube token as a secret text credential in Jenkins. It mitigates a lot of the challenges you might face if your pipeline is primarily focused building and testing front-end code.

## How to use the Docker image
Using the official `sonar-scanner` image, you can simply switch out of your Node.js container after building and testing your code and into a SonarQube-specific container for scanning.

### Steps
1. Create a `sonar-scanner.properties` [configuration file](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/) in the root of your project
2. [Generate a token](https://docs.sonarqube.org/latest/user-guide/user-token/) in SonarQube
3. [Add the SonarQube token as a secret text credential](https://www.jenkins.io/doc/book/using/using-credentials/) that your Jenkins pipeline can access.
4. Create a SonarQube stage in your pipeline

<pre class="lang-groovy"><code class="lang-groovy">pipeline {
  agent none
  stages {
    stage('Front-end') {
      agent {
        // start with a node image to install and test
        docker { image 'node:16.13.1-alpine' }
      }
      steps {
        sh """
        npm ci
        npm run test
        """
      }
    }
    stage('SonarQube') {
        agent {
          // switch into the sonar-scanner docker image
          docker { image 'sonarsource/sonar-scanner-cli:4' }
        }
        steps {
          // The `token` here is generated in SonarQube 
          // and can be added as a secret text credential
          withCredentials([string(credentialsId: 'token', variable: 'TOKEN')]) {
            sh """
            sonar-scanner -Dsonar.login=${TOKEN} -Dsonar.branch.name=${env.BRANCH_NAME} -Dproject.settings=./sonar-scanner.properties
            """
          }
        }
    }
  }
}</code></pre>