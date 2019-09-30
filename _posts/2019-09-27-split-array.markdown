---
layout: post
title:  "Splitting an Array"
date:   2019-09-27
categories: intermediate
---

I'm back again, some months later, and ready take on some more coding challenges! 


**The Chalenge:**

> Use the `split` method inside the `splitify` function to split `str` into an array of words. 
> The function should return the array. Note that the words are not always separated 
> by spaces, and the array should not contain punctuation.


**The Setup:**

```javascript
function splitify(str) {
  // Add your code below this line
  
  
  // Add your code above this line
}
splitify("Hello World,I-am code");
```


**My Solution:**

I had a think through several ways of doing this and they all seem pretty wacky. What if I could use something to swap the commas and hyphens for spaces, and then use `split()`. A little research shows that I could use a regular expression with `split()` but that doesn't seem like as much fun as my original idea...

After trying out everything I could think of with `filter()`, `map()` and `forEach()` (I even briefly considered if it might be somehow possible to use `reduce()`, I eventually came across the `replace()` method! This will hopefully allow me to implement the steps outlines above.

```javascript

function splitify(str) {
  
  const removeCommas = str.replace(","," ");

  const removeHyphens = removeCommas.replace("-"," ");
  
  return removeHyphens.split(" ");

}

```

So I tried it like this and, success! Well... first hurdle cleared anyway. I now face the issue that this function only works if there is only one of each of the special characters.
Actually, to look at the cases in which this function is expected to work, my method is not very suitable. Instead of having a separate stage where each kind of non-alphabet character is replaced with a space will result in a hell of a lot of stages to this process!

Instead of saying "replace this thing with a space and this thing with a space and this thing with a space......." I need to just say "replace everything that is not a letter with a space." And that brings us back to regular expressions! I saw that `replace()` can be used with regex so I'll give that a go. Just got to brush up on the syntax.

```javascript

function splitify(str) {
  
  // so here I've been able to replace all the desired 
  // characters with spaces but I'm left with excess spaces

  const replaceWithSpace = str.replace(/[\W]/g," "); 

  // so I will try and reduce the number of spaces between words 
  // to 1 with this next step

  const removeSpace = replaceWithSpace.replace(/\s+/g," ");

  // that regex says 'replace 1 or more spaces with a space'
  // seems to work!

  const splitOnSpace = removeSpace.split(" ")

  return splitOnSpace;

}

splitify("Hello, -World,I-am code")

```

Took me a while but I got there in the end! I'm sure I could have combined those two first steps into a single expression, but I think it's clearer this way. 

**Reminder: don't forget the /g flag at the end of the expression so that it doesn't just stop after the first result!**
