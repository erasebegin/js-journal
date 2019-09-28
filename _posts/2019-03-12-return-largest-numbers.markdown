---
layout: post
title:  "Return Largest Numbers From Nested Arrays"
date:   2019-03-12
categories: beginner
---

Bearing some resemblance to the previous problem where the longest string had to be found, this problem is somewhat more complex since the array is 2-dimensional, which means that I will probably have to use a nested for loop to access the sub-arrays.

```javascript

function largestOfFour(arr) {
  let newArr=[];
  for(let i=0; i<arr.length; i++){
    for(let j=0; j<arr[i].length; j++){
      console.log(arr[i][j])
    }
  } 
  return arr;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);

```

I created newArr to store the highest number in each sub-array. I created the nested for loop, but am not sure what to do with it. currently it just returns every number in every sub-array in a row. I need there to be a break between looping through sub-arrays so that my if statement is not looking for the highest number across all sub-arrays. I will go and look at some examples of nested for loops to see if anything looks useful. 

I guess I'm looking for a way to break out of the inner loop when the highest number in that sub-array is found. So perhaps putting an if statement there will accomplish this.

I feel like I'm getting closer. I realised that to exit the inner loop there just needs to be something returned from an if statement. I've added an else if condition to try and stop the loop from continuing to push to num if it passes.... okay .... that's dumb. I don't think that makes sense actually.

```javascript

  for(let i=0; i<arr.length; i++){
    let num = 0;
    for(let j=0; j<arr[i].length; j++){
      if(arr[i][j]>num){
        num = arr[i][j]
      } else if(num==arr[i][j]){
        newArr.push(num);
      } console.log('arr:'+newArr)
    console.log('num:'+num)
    }
  } 

```

The inner for loop is fine, I just need to somehow push num to newArr when the inner (j) loop finishes executing.

What if I add another if statement to the inner loop... No... an OR condition in the of statement that says 'if the inner loop has reached the length of the array, push num to the new array...'
Not quite right but along the right lines...

Actually yes, two if statements in the inner loop. The first checks if the number in the sub-array is larger than num, then updates num with that number. The second if statement checks if the loop has reached the end of the sub-array. But I can't think of a way to track the progress of the loop unless I add a counter to the first if statement: count++. This will iterate a variable in the outer loop that will reset each time the inner loop finishes executing. So the second if statement will compare the number stored in count to the length of the array. If they are the same, then push num to newArr.

```javascript
function largestOfFour(arr) {
  let newArr = [];
  for(let i=0; i<arr.length; i++){
    let num = 0;
    let count=0;
    for(let j=0; j<arr[i].length; j++){
      count++
      if(arr[i][j] > num){
        num = arr[i][j];
      }
      if(count==arr[i].length){
        newArr.push(num);
      }console.log(newArr)
    }
  } 
  return newArr;
}

largestOfFour([[17, 23, 25, 12], [25, 7, 34, 48], [4, -10, 18, 21], [-72, -3, -17, -10]]);
```

So close now! This returns the correct array for most inputs, but if the inputs are negative numbers it fails because the if statement is comparing to 0. Ideally, instead of comparing the element in the sub-array at [i][j] to a standalone variable outside the loop, I would compare it to the last number that has just been passed so that the reference for size is not fixed at 0 to begin with. But this seems quite beyond me at this point in time and I think its time to move on so I will just set num to a very low negative number. That should take care of the problem, but is a cop-out for sure. I hope to return to this problem one day better-equipped to truly solve it.