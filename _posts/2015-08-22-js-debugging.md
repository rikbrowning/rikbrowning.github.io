---
layout: post
title:  "Javascript Debugging"
date:   2015-08-22 18:57:29
categories: Javascript
author: Rik
---

Every now and then I come across a bug, you know the kind, seems to happen for no logical reason. You do the obvious things first, check what you just changed cause that's normally what caused it. When that doesn't work it's time to get your hands dirty in a Javascript debugger. I normally use the Chrome JS debugger as its pretty awesome for some of the following reasons.

##Debugger

`debugger;` is a nifty bit of code that  when hit by the Chrome debugger will automatically stop execution. This can be helpful if you are in the editor and don't want the hassle of having to find a specific line in the source tab.

##Don't just log strings

`console.log()` is great for logging out messages to the console but did you know you can log `Objects` and `DOM Elements` too? Well now you do. 

{% highlight js %}
var obj = {
  num: 1,
  str: "hellow"
};

//print out what is in obj
//%O prints out a nicely formatted object (that is a captial o)
console.log('this is what is in obj %O', obj);
{% endhighlight %}
This is what the result looks like:

![alt text](/assets/images/js-debugging-object-print.png "image of console after running above code.")

{% highlight js %}
var body = document.querySelector('body');

//print out what is in body
//%o prints out a nicely formatted DOM element
console.log('this is what is in body %o', body); 
{% endhighlight %}
This is what the result looks like:

![alt text](/assets/images/js-debugging-dom-print.png "image of console after running above code.")

##Console shortcuts

Every select a DOM element in the Elements tab and want to access it directly in the console? Well `$0` will return the currently selected DOM element in the console. Similarly $1 will return the previously selected element.  What if you want to query for an element as searching through the DOM is too tedious? `$$` is a short cut to `document.querySelectorAll`. I know it is only a short cut but it is very handy and saves those all important key strokes.


##Powerful Conditions
Don't just use conditional breakpoints to check conditions. The code you put in for the condition will be executed so it can be useful to put some logging statements in there instead of having to go back to the editor.

##File navigation
`Ctrl+o` will allow you to search for that particular Javascript file you are looking for. `Ctrl+Shift+o` will allow you to search for a particular function inside the current Javascript file. Both of these commands save me so much time when trying to find that troublesome piece of code.

The above is by no means a comprehensive list of all the things Chrome Debugger can do but just a few of my favourite features that I use regularly. Hopefully you learnt something that will help you track down your next bug easier.
