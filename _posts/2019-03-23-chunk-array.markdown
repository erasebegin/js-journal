---
layout: post
title:  "Chunk Array"
date:   2019-03-23
categories: beginner
---

The task here is to split a single array into groups of arrays that are the length specified by the function's second parameter (size).

I guess slice and/or splice will be very useful here. I can't see this challenge being too difficult, but I want to try and make my code as succinct as possible. Unfortunately I will probably use a for loop again as I still haven't got the hang of higher order functions. It might be an idea to have the loop iteration parameter as size instead of i++.

Progress update: I've been tinkering for an hour or so now and I have a semi-functional function. I used the array copy method (using slice()) to make sure that my splicing wasn't affecting the original array. I also created a variable called n to increment by an amount of size with each loop, because I couldn't figure out how to do this using i.

I ran into a problem where the loop was iterating more times than it needed to because it was terminating after reaching arr.length which of course doesn't make sense. I need to find a way to make this parameter dynamic depending on the number of chunks so I will create a variable that stores arr.length/size. I think that makes sense... time to try it out.

So this is my final solution and it works!

```javascript

function chunkArrayInGroups(arr, size) {
  let arrCopy = arr.slice()
  let newArr = [];
  const loopLimit = arr.length/size;
  let n = 0;
  for(let i=0; i<loopLimit; i++){
    newArr[i] = arrCopy.splice(n,size)
    n+size;
  }
  return newArr;
}

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6], 3);

```

I've been working on this small segment of the course for a month now, and although I'd really like to try my hand at simplifying some of these solutions (maybe I could use forEach() to chunk the array), I think it's time to move on. I will update this journal when I reach the advanced algorithms tutorial further down the line.