---
layout: post
title:  "Useful Javascript Array Functions"
date:   2015-03-06 18:57:29
categories: javascript
author: Rik
---

Many libraries cover basic array functionality eg. for each, filter, sort, which can be extremely useful when supporting older browsers and acting as a polyfill. However in any project that gets to support IE9 and up there is a lot of great built in array functionality that doesn't require any frameworks. I am going to discuss a few.

##forEach
Iterate over an array easily, takes in a function with signature (currentValue, index, array). Now forEach unfortunately doesn't offer a way to stop the iteration early but we can use some or every to achieve the same functionality.

{% highlight js %}
var nums = [1,2,3,4,5];
nums.forEach(function(item){
  console.log(item);
});
{% endhighlight %}

##some, every
For those C# developers among us these are the equivilant to Any and All methods. Some returns true if any item returns true from the callback. Every returns true if all items return true from the callback. The callback has a signature (currentValue, index, array) => boolean.

{% highlight js %}
var nums = [1,2,3,4,5];
var containsOdd = nums.some(function(item){
  return item % 2 === 1;
});//true

var allOdd = nums.every(function(item){
  return item % 2 === 1;
});//false
{% endhighlight %}

##sort
Sort an array of items inplace. Sort takes in a call back with signature (valueA, valueB) => number. If valueA is less than valueB return a number less than 0, if valueA and valueB are equal return 0 and if valueA is greather than valueB return any number greater than 0.

{% highlight js %}
var nums = [1,3,9,2,4];
var sorted = nums.sort(function(a,b){
  return a > b ? 1 : a < b ? -1 : 0;
});
{% endhighlight %}

##filter
Returns a new array of elements that have returned true from the callback. The callback has a signature (currentValue, index, array) => boolean.

{% highlight js %}
var nums = [1,2,3,4,5];
var odds = nums.filter(function(item){
  return item % 2 === 1;
});
{% endhighlight %}

All of the above functions are available in IE9 and up so next time you are thinking of using a framework function to manipulate array, stop and think can you do it with a built in one.