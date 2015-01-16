---
layout: post
title:  "Grunt File Order"
date:   2015-01-16 18:57:29
categories: grunt
---
Ever wanted to force a file to be loaded last when using grunt, say when using [grunt-contrib-concat][grunt-contrib-concat]?

Well after searching about a bit I found this little gem:

{% highlight javascript %}
// All files in alpha order, but with bar.js at the end.
{src: ['foo/*.js', '!foo/bar.js', 'foo/bar.js'], dest: ...}
{% endhighlight %}

This code is taken straight from [configuring tasks][grunt-tasks] under the "Globbing patterns" section. Pretty obvious when you think about it ...

[grunt-contrib-concat]:https://github.com/gruntjs/grunt-contrib-concat
[grunt-tasks]:http://gruntjs.com/configuring-tasks