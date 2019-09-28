---
layout: post
title:  "Title Case a Sentence"
date:   2019-03-18
categories: beginner
---

**Task: take a string of any combination of upper and lower case letters and change the first letter of each word to upper-case.**

Again, my first thought is to smash the string into a two-dimensional array and start trying to manipulate it through for loops, but there must surely be a simpler way using string methods. I there was one called toUpperCase(). So maybe I can split() the string at the spaces... that would make an array though. It's probably the case that dealing with arrays is inevitable here. Once I have an array I suppose I can use the indexOf() method to look for the first letter in each string in the array and then change it toUpperCase(). Let's see how that pans out.

Okay, so I can't use indexOf(). I forgot that it does the opposite of what I need. It returns the index of a  given string, not the string at a given index. But I've had a search and it seems there is a method called charAt() which does what I need. 

```javascript
function titleCase(str) {
  let arr = str.split(' ');
  for(let i = 0; i>arr.length; i++){
    arr[i].charAt(0).toUpperCase()
  }
  str = arr.join(' ');
}

titleCase("I'm a little tea pot");
```

Okay so some parts of this are working, but at least one thing isn't. If I feed the line arr[0].charAt(0).toUpperCase() to the console, it returns what I expected it to. Perhaps the problem is that this doesn't actually alter the strings in the array. Can I use push()? Seems unlikely, but I'll try. 

push() doesn't seem to be doing anything at all no matter what I try to push from within the for loop. Weird.

Played around with a bunch of stuff and am still scratching my head! So what do I _know_ is working?
Well split() is definitely creating a comma separated array, and join is definitely putting the string back together again correctly. So the problem is with the for loop. But syntactically it seems fine! I also don't understand why it's not possible to put a console.log() within the for loop AND whatever I put in the for loops seems to have no impact whatsoever on the array.

On the MDN pages it gives an example of a for loop and then uses console.log() to display the value of i as the loop iterates! So whaaaaat's going on? A simple syntax error? 

Okay, I have a clue. The for loop does everything it is supposed to and all logs are correct if I just change the exit condition to a fixed number. So there's a problem with using arr.length as the exit condition for the loop, but why? I've used array.length in several exercises before and have not experienced this problem. 

I swapped arr.length for str.length and that seems to have fixed the function, but still does not explain why I was having this problem. Anyway, onwards!

If I do this within the loop:

console.log(arr[i].charAt(0).toUpperCase())

It returns the first letter of each string in the array in upper case. Cool, but not what I need. I found another string method called setCharAt(), but this doesn't accept toUpperCase() as a parameter. I can imagine that there are many ways to solve this, but the one that occurs to me now is to use the above method to create a new array of capital letters and then create a new for loop that will use the setCharAt() method to change the set the first letter of each string.

Ooo0okay... according to the debug console setCharAt() is not a valid method. I think I was looking at Java, not Javascript. But there is a method called substr() which I could possibly use.

I was starting to think of all these crazy possibilities, my mind was going wild trying to figure this out. The more I thought about it, the more complex my thoughts became until I was convinced that this problem was totally beyond my grasp-- that it was overwhelmingly deep. But then I did this:

```javascript

function titleCase(str) {
  let lstr = str.toLowerCase();
  let arr = lstr.split(' ');
  let capArr = [];
  let restArr = [];
  let newArr = [];
  for(let i = 0; i < arr.length; i++) {
     		capArr.push(arr[i].substr(0,1).toUpperCase());
     		restArr.push(arr[i].substr(1,arr[i].length))
     		newArr[i] = capArr[i]+restArr[i];
	}
	return newArr.join(' ')
}

titleCase("I'm a little tea pot");
```
**Winner!**