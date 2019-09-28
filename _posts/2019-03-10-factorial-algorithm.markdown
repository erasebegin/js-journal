---
layout: post
title:  "Factorial Algorithm"
date:   2019-03-10
categories: beginner
---

While creating factorial algorithm, biggest roadblock was in not recognising that the formula was trying to multiply by 0 so the result kept coming back as NaN. The solution was to take the number that was to be factorised, create an array from 1 to that number, and then create a for loop:

```javascript
let sum = 0;
for (let i = 0; i < arr.length; i++) {
	sum = sum * arr[i];
}
```

This was problematic because of sum starting at 0 and i starting at 0. Changed both to 1 and it worked fine. If you multiply by 0 to therefore have 0 returned, the number will never reach above 0.
