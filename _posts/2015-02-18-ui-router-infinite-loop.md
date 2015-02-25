---
layout: post
title:  "$urlProvider causing Infinite Loop"
date:   2015-02-18 18:57:29
categories: angular
author: Rik
---
I recently came across an interesting case in one of my Angular projects. Navigating to the site was causing an infinite loop if the app wasn't configured correctly. The offending piece of code was making use of ``$urlRouterProvide`` provided by the ``ui.router`` module.

{% highlight javascript %}
$urlRouterProvider.when('', '/home')
  .when('/', '/home')
  .otherwise('/home');
{% endhighlight %}

The issue is that whenever a state fails to resolve it will continuously go to the ``otherwise``  state which just so happened to be the one failing to resolve, infinite loop.

##Solution

###First

Handle the ``$stateChangeError`` event thrown whenever a state's resolve fails, I made it go to a 500 state.
{% highlight javascript %}
app.run(handleStateError);

handleStateError.$inject=["$state","$rootScope"];

function handleStateError($state,$rootScope){
  $rootScope.on('$stateChangeError',
    function(event, toState, toParams, fromState, fromParams, error){
      //do some sort of error handling/logging
      $state.go('500');
  })
}
{% endhighlight %}

###Second

Don't use ``$urlRouterProvider.otherwise`` for anything other than a 404 state.
{% highlight javascript %}
$urlRouterProvider.when('', '/home')
  .when('/', '/home')
  .otherwise('/404');
{% endhighlight %}

Though either step would have fixed the issue having both allows me to handle invalid navigation with 404 state and any state resolving issues with a 500 error.
