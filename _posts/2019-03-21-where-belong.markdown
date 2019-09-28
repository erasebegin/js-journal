---
layout: post
title:  "Where Do I Belong?"
date:   2019-03-21
categories: beginner
---

The task, from what I can tell, is to put the numbers in an array in order from smallest to largest and then find the index that the number provided by the second parameter should go. Although I am trying to avoid using for loops, it seems that the appropriate array method here would be sort() and I feel like that would make things a bit too easy. I'm going to go ahead and use a for loop anyway for the challenge of it.

So I guess the first time the loop iterates it will look for the lowest number and push to an array. So how can it look for the lowest number? If i is lower than arr[0], iterate, else push that value to the new array... It's difficult to put this in words, I think it will be easier if I just start tinkering. 

```javascript

function getIndexToIns(arr, num) {
  let ordered = [];
  for(let i=0; i<arr.length; i++){
    let n=1;
    if(arr[i]<arr[n]){
      n++
    } else {
      ordered.push(arr[i]);
    }
  } 
  return num;
}
```
This is the first step. Something is working, but instead of having the lowest number returned, I'm having everything but the lowest number returned. Surely just a slight adjustment needed.... no... this is just...

I need a variable to always contain the lowest or largest thus far. I think I'll try largest since it makes the most sense in my current setup (I can always just unshift instead of pushing).

Okay I've arrived at a checkpoint:

```javascript
function getIndexToIns(arr, num) {
  let ordered = [];
  let highest=0
  for(let i=0; i<arr.length; i++){
    if(arr[i]>arr[highest]){
      highest=arr[i]
    } else if (highest != 0){
      ordered.push(arr.splice(highest));
    }
  } console.log(ordered)
  return num;
}
```
I just need to loop this loop somehow and I'll have my ordered array. But I guess in order to repeat this process I will  need to be altering the array each time, not just returning the highest number. So I'll do a snippy snip (splice()) instead of a push.

-------------

This problem made my head ache so I left it for a few days. The solution proposed in the previous paragraph confused me quite a lot and seemed to regress the situation. I have come back with renewed determination. I need help, but I don't want to look at the FCC hints. I remember an app I used to have that taught the general concept of different algorithms through pseudo-code. So I have found a website that [explains sorting algorithms in python](https://danishmujeeb.com/blog/2014/01/basic-sorting-algorithms-implemented-in-python/). It seems that the method I was trying to figure out was the **Insertion Sort**. Which pushes values into a new array one by one. 

It looks like I need to be using i-1 as a reference for the previous number in the array when comparing. The example uses a while loop within the for loop, but I can't remember what the difference is between the two. Hopefully [this website] (https://techdifferences.com/differenece-between-for-and-while-loop.html) will help me understand.

Nope, not getting it. The python algorithms do not make sense to me. I'll try another website and see if it can put things in clearer terms.

I like [this website](https://www.tutorialspoint.com/data_structures_algorithms/bubble_sort_algorithm.htm), the explanation seems clearer and doesn't even use code. I'm currently reading about **Bubble Sort** which moves the elements around in an array rather than pushing or copying them to a new array which I think means it is an **unstable** algorithm.

So I want to look at 2 values and compare them, which is what I have been doing. I should check if **i** is smaller than the previous value. If it is larger, it means those two elements are already in the correct order. In the event that i is smaller than the previous value, I need to swap the two values being compared. But this is where I'm having trouble. I found a post on [stackoverflow](https://techdifferences.com/differenece-between-for-and-while-loop.html) that explains how to do this, but it seems a bit tricky.

I guess I understand the logic of creating the temp variable. If I just say arr[i] = arr[i-1] or vice versa, then I lose one of the variables since the first overwrites the second. But I need to play around to figure out how to use this 'temp' logic.

Okay this seems to work up to a point:

```javascript

for(let i=0; i<arr.length; i++){
      if(arr[i]>arr[i-1]){
        let temp = arr[i-1];
        arr[i-1] = arr[i];
        arr[i] = temp;
      }

```

So what's the problem and what's the next step? Feels like progress anyway!

Okay, I get it. There needs to be another loop. I guess that's why the python example was nesting a while loop inside the for loop. This is the same conclusion I came to earlier, a nested loop. But I didn't really understand as clearly as I do now. So the condition for the inner loop will be reaching the end of the array (array.length) but what about the outer loop? How does it know when everything is sorted? I guess a caveman solution would be to set an upper-number of loops based on the maximum possible number of loops. This means that even if the sorting completes after the first loop, it will continue to loop several times. I'm going with that for now... sorry future me if this causes you embarassment.

 GREAT! This is doing just what I want:

```javascript
for(let j=0; j<10; j++){
      for(let i=0; i<arr.length; i++){
        if(arr[i]>arr[i-1]){
          let temp = arr[i-1];
          arr[i-1] = arr[i];
          arr[i] = temp;
        }
      }
    }
```

Well... it's ordering things in from largest to smallest... but it's ordering them! I'm sure I can reverse that fairly simply (woah, deja vu).

Yup, just flipped the i-1 and i values in the inner-loop to reverse the order. Super!

Now I just have to push num into the array, let the loops sort it, and then find it again with indexof. Should be simple enough. Actually, in case there are duplicate entries I should use firstIndexOf.... I'm pretty sure that's a thing. Okay no, it's not a thing. I definitely remember there being a lastIndexOf. Perhaps there is no firstIndexOf because indexOf already functions in this way.

That's it! Bingo bango whambo blambo!

```javascript

function getIndexToIns(arr, num) {
    arr.push(num);
    for(let j=0; j<10; j++){
      for(let i=0; i<arr.length; i++){
        if(arr[i-1]>arr[i]){
          let temp = arr[i];
          arr[i] = arr[i-1];
          arr[i-1] = temp;
        }
      }
    }
  return arr.indexOf(num)
}

getIndexToIns([32, 16, 10, 1, 18, 72], 50);
```
**NOTE: This method of setting the end condition of the outer loop has significant limitations.**       