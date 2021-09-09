---
title: Screen Reader Only Text
description: How and when to use screen reader only text
date: 2021-09-05
tags:
  - Development
  - Accessibility
layout: layouts/post.njk
---
## What is screen reader only text?
Screen reader only text is included in the markup but hidden visually. That means that it gets read by screen readers, but doesn't show up for sighted users.

## Why is it important?
A great example of where this text is helpful is a page with multiple "Learn More" buttons. For sighted users, there is a visual association between the content surrounding the button and the button itself. For, screen reader users however, a common strategy is to tab through all the focusable elements on the page. That means they could hit multiple buttons that read "Learn More" without any additional programmatic association with other content. That user might think, "learn more about what?"

## A solution, using CSS
To solve for this problem and give additional context where needed you can a CSS rule that hides the text but still leaves it accessible to screen reader users. Bootstrap has a commonly used rule that works well:

```
.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    overflow: hidden;
    clip: rect(0,0,0,0);
    white-space: nowrap;
    -webkit-clip-path: inset(50%);
    clip-path: inset(50%);
    border: 0;
}
```

## Javascript Bookmarklet

Capitalize on low hanging fruit to identify a ballpark value added activity to beta test. Override the digital divide with additional clickthroughs from DevOps. Nanotechnology immersion along the information highway will close the loop on focusing solely on the bottom line.

``` text/2-3
// this is a command
function myCommand() {
	let counter = 0;
	counter++;
}

// Test with a line break above this line.
console.log('Test');
```
