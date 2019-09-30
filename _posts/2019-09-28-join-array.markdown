---
layout: post
title:  "Joining an Array"
date:   2019-09-28
categories: intermediate
---

**The Challenge:**

Use the `join` method (among others) inside the `sentensify` function to make a sentence from the words in the string `str`. The function should return a string. For example, "I-like-Star-Wars" would be converted to "I like Star Wars". For this challenge, do not use the `replace` method.

**My Solution:**

This is seemingly the inverse of [the previous problem](split-array)... but this time I'm not allowed to use that beautiful `replace()`! I should be able to use some regex techniques that I looked at in the last exercise. Let's get cracking then...

I guess I'll first try to use `split()` to separate the array at each point that is _not_ a letter of the alphabet. I will specify this using a regex expression as before.

Yeup, I did `str.split(/[\W]/g)` and it seems to be functioning correctly! Next a join and then that should be it!

```javascript

function sentensify(str) {

  const splitter = str.split(/[\W]/g);
  const joiner = splitter.join(" ");
  
  return joiner
}

console.log(sentensify("The.force.is.strong.with.this.one"));

```
Easy peasy 😁
