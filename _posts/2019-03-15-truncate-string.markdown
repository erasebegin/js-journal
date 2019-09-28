---
layout: post
title:  "Truncate a String"
date:   2019-03-15
categories: beginner
---

The task is to take a string and a number as inputs and return a string that is truncated to the index of that number. Then the final result should append an ellipse... It looked super simple at first and, as I suspected, it is.

```javascript
function truncateString(str, num) {
  let truncated = str.slice(0, num);  
  return truncated + '...';
}

truncateString("A-tisket a-tasket A green and yellow basket", 8);
```

This passes almost all the tests, but the folks at FCC have thrown in a little curve ball:

![fcc-checks2](https://i811.photobucket.com/albums/zz39/EraseBegin/fcc-2.png)

After looking at this a while, I think it's actually a massive curve-ball. How on earth....?
I guess <span class='code-bit-func'>slice()</span> can't take such a complex argument, but I don't know how to add a step that simplifies the argument. I tried simply assigning num to a new variable, but that didn't do it. The new variable would just contain the same level of complexity. So how do I 'resolve' this argument before I pass it to <span class='code-bit-func'>slice()</span>?

I guess I'll try logging the outputs to try and see what's going on. The console output is exactly what the checks are looking for...

Oh! I misread the specification. It is not all outputs that should have an ellipse appended. For outputs that have the same length as the inputted string there should be no ellipse. This should be easy to fix.
Hmmm, added an if/else statement, but the output is still incorrect.

```javascript

function truncateString(str, num) {
  let truncated = str.slice(0, num); 
  if(truncated==str.length){
    console.log(truncated) 
    return truncated;
  }else{
    console.log(truncated + '...') 
      return truncated + '...';
  }
}

truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length);

```

Okay so a minor alteration. I had to get truncated out of the if statement. I should be comparing str to num directly, not comparing the sliced entity. And, given the code tests, I should be looking for lengths equal to or greater than str.length, not just equal to.

