---
layout: post
title:  "Finding the Longest Word in a Sentence"
date:   2019-03-11
categories: beginner
---

First part of problem was to convert the string into an array of words. For this I used the split() method, giving " " as the splitting parameter. I then had to find a way to get the lengths of each string in this array. I thought that the length property only worked on arrays, so spent a lot of time trying to figure out how to convert the strings in the array to separate characters in a sub-array which was super messy and confusing. It turns out you CAN use the length property to just get the length of a string. 

The second part of the challenge is to figure out a way to compare the numbers in the newly created strLenArr to find the largest one. At first I thought this would be simple, but am struggling to come up with a solution on my own.

Turns out it was simple! I was quite proud to have come up with this solution without forum help:

```javascript
function findLongestWordLength(str) {
  const splitStr = str.split(" ");
  let strLenArr = [];
  for (let i=0; i<splitStr.length; i++){
    strLenArr.push(splitStr[i].length)
  }

  let highest = 0;

  for (let j=0; j<strLenArr.length; j++){
    if(strLenArr[j]>highest){
      highest=strLenArr[j];
      }
    }

  console.log(highest)
  return str.length;
}

findLongestWordLength("The quick brown fox jumped over the lazy dog");
```

