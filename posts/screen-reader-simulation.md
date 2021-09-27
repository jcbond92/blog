---
title: Simulating a screenreader experience with the Web Speech API
description: How and when to use screen reader only text
date: 2021-09-25
tags:
  - Accessibility
layout: layouts/post.njk
---
I built a bookmarklet with the Web Speech API to simulate screen reader experiences with links. <a href="#a-bookmarklet-to-help-build-empathy">Skip ahead to the last section to test it out</a>.

## What is screen reader only text?
Screen reader only text is included in the markup but hidden visually with CSS. That means that it gets read by screen readers, but doesn't show up for sighted users.

## Why is it important?
A great example of where this text is helpful is a page with multiple "Learn More" buttons. For sighted users, there is a visual association between the content surrounding the button and the button itself. For screen reader users however, a common strategy is to tab through all the focusable elements on the page. That means they could hit multiple buttons that read "Learn More" without any additional programmatic association with surrounding content. That user might think, "learn more about what?"

Screen reader only text can add critical context for quickly comprehending the purpose of the links.

<pre class="lang-markup">
<code class="lang-markup">
  &lt;!-- This link gets read as "Learn more"..."Learn more" about what?!
  The purpose of this link is not clear, especially if there 
  are multiple "learn more" links on the same page --&gt;
    &lt;a href="/"&gt;
      Learn more
    &lt;/a&gt;

  &lt;!-- This link gets read as "Learn more about product one".
  The purpose of this link is clear regardless of 
  how many "Learn more" links are on the page. --&gt;
    &lt;a href="/"&gt;
      Learn more&lt;span class="sr-only"&gt; about product one&lt;/span&gt;
    &lt;/a&gt;
</code>
</pre>

## A bookmarklet to help build empathy
I wrote some JS can be run in a bookmarklet to help simulate what it's like for users to hear a screen reader read a link. The bookmarklet will add a button beside each link on the page and then use the Web Speech API to read the text like a screen reader would as a user tabs through the links on the page. 

Check out the CodePen below for examples, and for the code to copy into your bookmarklet.

<p class="codepen" data-height="600" data-default-tab="result,js" data-slug-hash="powEwqV" data-user="jcbond92" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/jcbond92/pen/powEwqV">
  Simulating screen reader text experiences</a> by Joseph Bond (<a href="https://codepen.io/jcbond92">@jcbond92</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>