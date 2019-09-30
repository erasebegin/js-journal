---
layout: post
title:  "Creating a URL Slug"
date:   2019-09-29
categories: intermediate
---

**The Challenge:**

Fill in the `urlSlug` function so it converts a string `title` and returns the hyphenated version for the URL. You can use any of the methods covered in this section, and don't use replace. Here are the requirements:
* The input is a string with spaces and title-cased words
* The output is a string with the spaces between words replaced by a hyphen (-)
* The output should be all lower-cased letters
* The output should not have any spaces

**My Solution:**

I guess the first step will be converting `title` to lower case since that's very easy to do using `toLowerCase()`.

And now, _without_ replace, I need to replace the spaces with hyphens..... hmm. It is recommended that I use map/filter/reduce etc to try and solve this so I'll need to think this through.... maybe I can use `split()` to convert the whole string to an array of characters and then... 

do something.

?

`filter()` will only return the values that I want to replace... that doesn't seem very useful. Perhaps `map()` is what I need. 

Yeeeeessss, according to [this excellent tutorial](https://codeburst.io/learn-understand-javascripts-map-function-ffc059264783) I can use conditions with `map()`. I will use the ternary operator as in the example in order to get some practice writing the syntax for this kind of conditional statement.

I spent some time scratching my head because `map()` wasn't functioning in the way I expected, but I eventually realised that it's because strings can't be worked on like arrays. I thought that because string[3] returns a character in the string, that I didn't have to use `split()` to work on it like an array. But after using split to break it into an array of individual characters, `map()` seems to be working.

Coooooool, so I did this:

`const arr = title.toLowerCase().split('').map((x) => x === " " ? x = "-" : x );`

And now I have exactly what I want, but as an array of single characters. I guess now I can just use `join()` to get them all together again!

```javascript

var globalTitle = "Winter Is Coming";

function urlSlug(title) {

  const arr = title.toLowerCase().split('').map((x) => x === " " ? x = "-" : x );

  return arr.join('')

}

var winterComing = urlSlug(globalTitle); 

console.log(winterComing)
```

Okay so this works fine for all test cases *except* this one:  "  Winter Is   Coming"

In this case the output would be "--winter-is--coming"

I think the solution here is again regex, but this seems quite complicated. In the case of changing 2 or more spaces to 1, I can use my method from the previous problem (`/\s+/g`). But getting rid of leading spaces might need to be a separate operation altogether.

Although it seems antiquated, I want to try removing the leading space(s) using a while loop that will delete characters until it reaches an alphabet character and then it will break out of the loop. I would prefer to use forEach  or something like that, but I can't think how that would work.