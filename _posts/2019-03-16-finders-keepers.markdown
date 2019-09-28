---
layout: post
title:  "Finders Keepers"
date:   2019-03-16
categories: beginner
---

Here is the premise this time: the function takes 2 arguments. The first is an array, and the second it a function. My function must use the function in the second argument as a truth test for each element in the array. The function will return the first element in the array that passes the test. If none return true, then the function returns undefined. This is the template provided:

```javascript

function findElement(arr, func) {
  let num = 0;
  return num;
}

findElement([1, 2, 3, 4], num => num % 2 === 0);

```

I plan to make a for loop of course to move through the array. Within the for loop I could create an if statement that applies the test to each element in the array. Let's give it a go.

Stumped pretty early on here. 

```javascript

function findElement(arr, func) {
  for(i=0; i<arr.length; i++){
    console.log(func(arr[i]))
  }
  let num = 0;
  return num;
}

findElement([1, 2, 3, 4], num => num % 2 === 0);

```
Tried logging the output of the function as it is passed each number in the array, but didn't get any output. One of the biggest challenges here is dealing with a function as an argument. I'm not sure how to handle it. This one has me truly stumped. Not sure what to search, not sure what to change, not sure what to log. I will leave some time to digest this and come back to it later. 

I give up, I'm looking at the clues. First clue: use a for loop to cycle through the array. Okay, done. Second clue: "num is passed to the function. We will need to set it to the elements we want to check with the function."

Okay I missed that. The importance of num. It was standing out there, but I didn't see it as relevant. So num needs to go inside the for loop I guess. What else? Wait, wait no....... I just tried something else! Haha, it was a syntax error. I didn't define the variable i. If I just add let to the if conditions, the output works! 

```javascript
function findElement(arr, func) {
  for(let i=0; i<arr.length; i++){
    let test = func(arr[i]);  
    if(test==true){
      return arr[i];
    } else {
      return null;
    }
  } 
  let num = 0;
  return num;
}

findElement([1, 2, 3, 4], num => num % 2 === 0);
```

So now that I am getting a true or false output for each element in the array, all that's left to do is check if the first true condition is met. If so, return that element, else if the for loop reaches the length of the array, return null.

But I've come to the same problem as with a previous exercise: I don't know how to check if the for loop is at the end of the array. I faced this problem when I had to find the largest number in an array, but it seems that I can actually use arr[i].length to check if the loop has finished. I just thought that this would perhaps be testing the length of a single element in an array. Anyway, let's give it a go.

```javascript
function findElement(arr, func) {
  for(let i=0; i<arr.length; i++){
    let test = func(arr[i]);  
    if(test==true){
      return arr[i];
    } else if (arr[i]==arr.length){
      return null;
    }
  } 
  let num = 0;
}

findElement([1, 3, 5, 9], num => num % 2 === 0);
```
Yup, that did the trick! Onward, ho!

