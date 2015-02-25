---
layout: post
title:  "Transclude Function in an Angular Directive"
date:   2015-02-25 18:57:29
categories: angular
author: Rik
---
You may not know this but there is a 5th parameter passed to the ``link`` function if ``transclude`` is set to true. This parameter is the transclude function which you can use to do some pretty interesting things.

##Take control of transcluding

The transclude function can take in two parameters, the first is the scope to be used when evaluating the nodes (this is optional) and the second is a function which is passed the contents to be transcluded. In the second parameter you can take control of which elements are inserted where. Let's say you want to put any elements with ``.bottom`` inside a ``.footer`` of your directives template, we can do that in the transclude function.

####Directive Template

{% highlight html %}
<div>
  <div class="footer"></div>
</div>
{% endhighlight %}

####Directive

{% highlight javascript %}
angular.module('app').directive(myDirective);

function myDirective(){
  return {
    transclude: true,
    restrict: 'AE',
    transclude: true,
    tempalteUrl: 'someTemplate.html',
    link: function(scope, element, attrs, ctrl, transcludeFn){      
      transcludeFn(function(content){
        var footer = element.find('.footer');
        content.forEach(function(node){
          if(node.hasClass('bottom')){
            footer.append(node);
          }else{
            element.append(node);
          }
        })
      })
    }
  }
}
{% endhighlight %}

##Word of Warning

I would recommend taking care when using the optional scope parameter, the transcludeFn will use the appropriate scope for the content so be careful what you change it to.
