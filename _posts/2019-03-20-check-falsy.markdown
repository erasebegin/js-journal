---
layout: post
title:  "Checking for Falsy Values"
date:   2019-03-20
categories: beginner
---

I have to check each element in an array for a falsy value. According to a [stackoverflow](https://stackoverflow.com/questions/35642809/understanding-javascript-truthy-and-falsy) post "all values are truthy unless they are defined as falsy." 

Values defined as falsy are Nan, undefined, 0, null, an empty string (' '), and of course, false. I think I can just use a for loop and a non-strict equivalence operator (==) to check if the value returns false. I'm sure there will be more to it, but on this occassion, and in future, I will try to avoid to avoid using for loops. A friend of mine says that they are problematic and outdated so I should be using array methods like map(), filter() and reduce().

In this case I think filter will be the best choice since I am wanting to 'filter' out values of a certain kind.

So, when I log this:

arr.filter(val => val == false) 

it seems to work, so now I need to think of a way of removing these values from the array. Maybe I'm thinking backwards actually. It's probably much easier to use the filter to return all truthy values.

It's kind of working, but there are several kinks. I wonder if it's a quirk of javascript that my function is registering undefined and false as false, but none of the other falsy values. I think it's a problem with my function in the filter. I will try and write an if statement that just asks if(val) do something, else do nothing. Can I use a conditional with filter....? Let's find out.

I don't think so. I don't think that's a thing that can be done. From where I stand at the base of the mountain I can't see a way to do it. So let's keep climbing and see what else we find.

Um, actually yes. Yes it's a thing. It's totally a thing and it's totally working. My whole function looks super slim and it's working! This is it:

```javascript
function bouncer(arr) {
 return arr.filter(val => val ? true:false);
}
```
That's the whole thing! Definitely the sexiest function I have written so far. 
