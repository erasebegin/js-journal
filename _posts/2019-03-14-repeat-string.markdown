---
layout: post
title:  "Repeat a String"
date:   2019-03-14
categories: beginner
---

The challenge: take a string and a number and repeat the string that number of times. An empty string must be returned if the number is less than 0. I really can't see this being much of a problem. First I'll want to check it the number is 0 or more, so I'll open with an if statement. If that condition is met then perhaps I can use a for loop along with the concatenate method to create the new string. The else statement will create an empty string. Let's see how that pans out.

```javascript

function repeatStringNumTimes(str, num) {
  if(num>0){
    for(let i=0; i==num; i++){
      str = str.concat(str);
    } 
    console.log(str)
  }else{
    return " "
  }
}

repeatStringNumTimes("abc", 3);

```

So this is what I tried, but I am stumped. I can see that there is a problem with the logic in the for loop, but can't put my finger on it. One problem is that str is resetting every time the loop is run. But I don't think I could make the loop iterate the string variable since I'm not sure logical operators can be used on strings. I think I'm just going to try going the array route instead of concatenation. So the for loop will push the string to an array num times. I can then hopefully convert the array back to a string using the toString() method.

Swapped out the guts, but it's not working... don't think it's something as simple as a syntax error.

```javascript

function repeatStringNumTimes(str, num) {
  let arr = [];
  if(num>=0){
    for(let i=0; i==num; i++){
      arr.push(str);
    }
    return arr.toString();    
  }else{
    return " "
  }
}

repeatStringNumTimes("abc", 3);
```

Okay weird. So I can't use i==num as the condition for ending the loop. Not too sure why. Anyway, changed it to i<num and everything seems to be working. It's still not passing the tests however since the output is comma separated. Had a quick search and it seems I can use the join() method to create a string without any separators. 

Bingo! That's it! There's probably a better way to solve this, but this will do for now.