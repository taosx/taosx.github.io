---
layout: post
title:  "Persist javascript between pages"
date:   2016-02-13 03:53:41 +0200
categories: javascript til
---
This is how to persist a piece of javascript code across pages in the browser. From time to time I read books in the browser (they're old or not available yet) and I really hate that I have to touch the mouse to click a button like next or get out of the current directory and to the next file (git repos), something I found during my mouse battles was [tampermonkey](https://tampermonkey.net/).

**Tampermonkey** is a free browser userscript manager.

A usecase example:

At the moment I am reading the "[Learn C The Hard Way](http://c.learncodethehardway.org/book/index.html)" by Zed A. Shaw, and I have to press the next or previous button when I want to go to the next or previous page.

![Next and Previous Buttons]({{ site.url }}/assets/learncnext_previous.jpg)

**Solution:** Make a little script which emulates the user pressing click on that button whenever I press the right key (next page) or the left key (previous page).

First I need to know what tools I have so:

~~~ html
<script src="./javascripts/jquery.js"></script>
~~~
That means that I can select elements with `$('element')` and use `.click` function on that element.
So selecting we do:

~~~ js
// Before I wrote the body like: document.body but it
// can't read arrow keys in chrome
const body = &('body');
const nextLink = document.getElementById('next_link');
const prevLink = document.getElementById('prev_link');
~~~

Then let's write all our functionality in a self-executing function:

~~~ js
(function() {
  'use strict';
  const body = $('body');
  const nextLink = document.getElementById('next_link');
  const prevLink = document.getElementById('prev_link');
  body.keydown(key => {
    if (key.keyCode === 39) {
      nextLink.click(); // 39 coresponds to the right arrow key
    } else if (key.keyCode === 37) {
      prevLink.click(); // 37 to the left arrow key
    }
  })
})();
~~~

Now go to tampermonkey extension, press add new script and just add the code below the predefined comments.

Don't forget to change the comments.

*This code above is to be taken lightly. Every browser has it's corner cases, I just made the code to work for my browser (chrome 50).*

Add script, use script, be happy, read more! Don'sleep :)