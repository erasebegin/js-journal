---
layout: post
title:  "Slice and Splice"
date:   2019-03-19
categories: beginner
---

This is quite a complicated requirement. The function takes two arrays and an index. It has to then take the second array, split it in two at the point specified by the index, and then add each of the two newly created parts to the beginning and end  of the first array.

For example:

frankenSplice([1, 2], ["a", "b"], 1) should return ["a", 1, 2, "b"]

and 

frankenSplice(["claw", "tentacle"], ["head", "shoulders", "knees", "toes"], 2) should return ["head", "shoulders", "claw", "tentacle", "knees", "toes"]

I went and looked at exactly how slice() and splice() work and it seems that I should be able to get the desired effect by using only splice(). 

```javascript
function frankenSplice(arr1, arr2, n) {
  var spliced = arr2.splice(n, 0, arr1);
  return arr2;
}

console.log(frankenSplice([1, 2], ['a', 'b'], 1));
```
This function is returning exactly what the specification is asking for as far as I can tell. It must be that I have misunderstood the specification at some point.

This is the strangest obstacle I have come up against yet. My function is doing exactly what is required. I have read the specification over and over, but can't see any difference. I have checked the type of the output to make sure its still an array, I've input all of the test inputs to see that they output correctly... everything seems fine.

I wouldn't have thought one of these challenges could be completed with such a simple function so I'm sure I'm missing something here. The title suggests that I use slice(), but that seems unecessary....

I think I understand what the problem is. The specification says that the second array needs to be added to the first array whereas my method adds the first array to the second. Well, that _could_ be it, but the tests should only be checking the output of the function, not the method that I use to get to that output. And the output is **correct**.

I had a peek at the clues and they are saying to use a for loop, so I'll go the far more complex route to see if that satisfies the checks. It'll be more fun that way anyway.

I guess what I want to be doing is using the loop to shift() to the array before n is reached and then push() to the array after n is reached. I think that will work, but I need to think of a way of using slice() and splice() to complete this... So I just need to convert the same concept into their way of thinking.

I should perhaps slice the second array at n and then perform two splices to get those two new arrays into the first array. Don't see why I would need to use a for loop for that though.....

Okay so it's taken me ages to actually understand what I am being asked to do. I have not been following clearly the direction that things need to move or the method by which they ought to do. I did this:

```javascript
function frankenSplice(arr1, arr2, n) {
  let arr2copy = arr2
  let pt1 = arr2copy.slice(0,n);
  let pt2 = arr2copy.slice(n,arr2copy.length)
  arr1.splice(0,0,pt1)
  arr1.splice(arr1.length,0,pt2)
  return arr1;
}
```
Which again returns exactly the right output, but works in the wrong order. I should be  taking array 1 and inserting it at the index point of arr2 one-by-one, so that explains why they want the for loop... I guess?

So if I slice one number out of arr1 each loop I can also splice that number into arr2 in the same iteration of the loop. Seems easy enough, but I need a way to set dynamic values for the slice parameters. I think I can use a count variable as before to achieve this. The start point of the splice will of course be n the first time the loop iterates, but it can't stay as n each iteration since I will then be splicing the numbers in reverse order.
So I'll have to make use of the counter again there I think.    

```javascript
function frankenSplice(arr1, arr2, n) {
  let count = 0;
  for(let i = 0; i<arr1.length; i++){
    let sliced = arr1.slice(count,count+1);
    arr2.splice(n+count,0,sliced)
    count++;
  }
  return arr2
}

frankenSplice([1, 2, 3], [4, 5], 1);     
```         

Well shucks. Here we are again. I've got another fully functional function and it is failing all of the tests..... When I log the output it returns exactly what the specification asks for. I give up. As far as I'm concerned I've already solved this problem 3 times over. I'm going to look at the answer.

Well the first thing I notice from the example is that they have iterated n instead of creating a new variable. Makes sense. The other thing I notice is that they used slice in a  way I didn't expect at all. When the specification said to make a copy of the first array I thought I could do that by saying arr2copy=arr2. But that just means I have the same array with 2 different names. They used slice without any parameters to copy the array so that's interesting. Then splice was used within the for loop in the same way that I used it. Let me try doing the slice copy trick to see if I can pass the tests that way.

Nope. Still doesn't like my output for some reason. I'll just try adjusting my formula to make it more similar to their given solution. I feel that the documentation for this problem is not very clear, or maybe its that their tests are too strict.

Anyway, solved now by making the function work in almost exactly the way it does in their solution. On to the next one!
