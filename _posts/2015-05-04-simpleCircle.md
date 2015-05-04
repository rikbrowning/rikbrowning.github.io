---
layout: post
title:  "Simple Circle"
date:   2015-05-04 18:57:29
categories: CSS
author: Rik
---

Create a simple circle around one character (or icon) based off the text height.
<style>
.simple-circle{
  display: inline-block;
  height: 2em;
  width: 2em;
  line-height: 2em;
  border-radius: 50%;
  text-align: center;
}
.larger{
  font-size: 1.5em;
}
.largest{
  font-size: 2em;
}
span.simple-circle{
  background-color: #79D0AC;
  color:white;
}
</style>
<p>As simple as 
<span class="simple-circle">A</span>&nbsp;
<span class="simple-circle larger">B</span>&nbsp;
<span class="simple-circle largest">C</span>&nbsp;
</p>
{% highlight css %}
.simple-circle{
  display: inline-block;
  height: 2em;
  width: 2em;
  line-height: 2em;
  border-radius: 50%;
  text-align: center;
}
.larger{
  font-size: 1.5em;
}
.largest{
  font-size: 2em;
}
{% endhighlight %}

{% highlight html %}
<p>As simple as 
<span class="simple-circle">A</span>&nbsp;
<span class="simple-circle larger">B</span>&nbsp;
<span class="simple-circle largest">C</span>&nbsp;
</p>
{% endhighlight %}