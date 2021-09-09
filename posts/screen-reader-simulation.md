---
title: Simulating a Screenreader Experience with the Web Speech API
description: How and when to use screen reader only text
date: 2021-09-05
tags:
  - Development
  - Accessibility
  - Javascript
layout: layouts/post.njk
---
## What is screen reader only text?
Screen reader only text is included in the markup but hidden visually. That means that it gets read by screen readers, but doesn't show up for sighted users.

## Why is it important?
A great example of where this text is helpful is a page with multiple "Learn More" buttons. For sighted users, there is a visual association between the content surrounding the button and the button itself. For, screen reader users however, a common strategy is to tab through all the focusable elements on the page. That means they could hit multiple buttons that read "Learn More" without any additional programmatic association with other content. That user might think, "learn more about what?"


<p class="codepen" data-height="600" data-default-tab="js,result" data-slug-hash="powEwqV" data-user="jcbond92" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/jcbond92/pen/powEwqV">
  Simulating screen reader text experiences</a> by Joseph Bond (<a href="https://codepen.io/jcbond92">@jcbond92</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>