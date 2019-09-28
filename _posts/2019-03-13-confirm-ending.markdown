---
layout: post
title:  "Confirm the Ending"
date:   2019-03-13
categories: beginner
---

Well this looks like a toughie. I need to take a string variable and a target variable and see if target appears at the end of the string. I am told that this can be solved with the .endsWith() method introduced in ES2015, but that I shouldn't use it. I must instead use substring methods to solve this puzzle.

I want to try and turn both the string and target variables into arrays, but something tells me that would be quite a rabbit hole to go down. I will instead look at working with only strings and see how far I get. 

After looking [here](https://www.impressivewebs.com/javascript-string-methods-reference/) for a list of string methods, I bumped into an old friend. indexOf() can be used to find the start and end position of target in the string. Could I just ask for the index of target, and then if it is not found, return false? Could it be that easy? Let's see.

```javascript

function confirmEnding(str, target) {
  if(str.indexOf(target)==true){
    str=true;
  }else{
  return false};

   str=false;
}

confirmEnding("Bastian", "n");

```

Kind of embarrassing code. Just thought I'd see... so I guess str.indexOf(target) will not directly give true or false if there is a match. So let's try a longer way.

```javascript

function confirmEnding(str, target) {
  const slicer = str.slice(str.indexOf(target));
  if(slicer==target){
    return true;
  }else{
    return false;
  }
}

confirmEnding("Bastian", "n");

```

This was my next idea, and I'm really surprised that it worked. The idea that I sort of fumbled my way towards is that slicer would attempt to isolate the target part of str, and if it failed to do so.... wait, what?? Why does this code even work. According to the FreeCodeCamp checker I have passed all but one of the tests with this code.....

![fcc-checks](https://i811.photobucket.com/albums/zz39/EraseBegin/ffc-checks.png)

This function is ridiculous... how is it passing all of these tests? It isn't even checking if the target is appearing on the end of the string. So why would ("Open sesame","pen") return false while ("Bastian", "n") returns true.... and then ("Congratulation", "on") returns false.....
With the 3rd example I guess the difference is that the target substring appears twice. But if I don't understand how this function is working now, I can't go about improving it.

I went away and looked at that list of string methods again, just below indexOf I found lastIndexOf. I still don't quite understand how this formula works, but I thought surely if I just replace indexOf with lastIndexOf it would fix the problem I was having with finding duplicate substrings. Sure enough that did the trick. Still not quite sure why this works, but it does! On to the next challenge!

