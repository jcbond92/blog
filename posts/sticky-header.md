---
title: Creating a sticky header with the Intersection Observer API
description: How to use the Intersection Observer API to create a sticky header
date: 2021-09-26
tags:
  - Javascript
layout: layouts/post.njk
---

I've been doing some testing with the intersection observer API, and it seems to be generally more performant than listening to a scroll listener.

In the simple performance tests I've seen that that scroll listeners versions of this same UI block the main thread for around .4ms over a 4 second period of scrolling down the page.

The intersection observer API version runs asynchronously, so it doesn't block the main thread at all, freeing up the CPU for other interactions. Fractions of a millisecond aren't a lot on their own, but if there are multiple items on a page we need to keep track of (like animations, a sticky navigation, or lazy loading images) it can lighten a potentially expensive process for the browser.

Creating an intersection observer is also pretty straightforward. Check the vanilla JS that's powering the CodePen at the bottom of the page for more details.

<pre class="lang-js">
<code class="lang-js">
// Get all the elements you'll want to observe or update
const header = document.querySelector("#header")
const title = document.querySelector("#title")
const placeholder = document.querySelector("#placeholder")

// adds .sticky to the header
const slideInHeader = () => {
  setTimeout(function(){
    header.classList.add("sticky")
  }, 1000);
}

// removes .stkcy from the header
const slideOutHeader = () => {
  header.classList.remove("sticky")
}

// configuration for the observer
const config = {
  root: null
};

// create the observer
const observer = new IntersectionObserver(function (entries, self) {
  entries.forEach((entry) => {
    if (!entry.isIntersecting) slideInHeader();
    if (entry.isIntersecting) slideOutHeader(); 
  });
}, config);

// observe the title to see when it's in view
observer.observe(title)
</code>
</pre>

<br/>

<p class="codepen" data-height="600" data-default-tab="js,result" data-slug-hash="YzQGBRR" data-user="jcbond92" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/jcbond92/pen/YzQGBRR">
  Sticky Header with Intersection Observer</a> by Joseph Bond (<a href="https://codepen.io/jcbond92">@jcbond92</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>