---
layout: post
title:  "Directive Controllers and Scopes"
date:   2015-04-17 18:57:29
categories: angular
author: Rik
---

##Angular 1.2

When using a controller with a directive it is recommended to use the `controllerAs` attribute/syntax, see [John Papa style guide](https://github.com/johnpapa/angular-styleguide#style-y075). But if we use an isolated scope in our directive, how do we get the isolated scope properties into our controller?

{% highlight javascript %}
angular.module('directives').directive('rikDirective', rikDirective);

angular.module('direvtives').controller('RikDirectiveCtrl', RikDirectiveCtrl);

function rikDirective(){
  return {
    restrict: 'EA',
    scope: {
      name: '='
    }
    controller: 'RikDirectiveCtrl as rik'
  }
}
//uh oh surely using controllerAs means we dont inject the scope?
RikDirectiveCtrl.$inject = ['$scope'];
function RikDirectiveCtrl($scope){
  var vm = this;
  vm.name = $scope.name;
  
  $scope.watch('name', function(nV){
    this.name = name;
  }.bind(vm));
}
RikDirectiveCtrl.prototype.speak = function(){
  return "My name is " + this.name;
}
{% endhighlight %}

As you can see our `RikDirectiveCtrl` has to have the `$scope` injected, which is what we were trying to avoid doing using the controllerAs attribute/syntax.

##Angular 1.3 to the Rescue

In Angular 1.3 they introduced the `bindToController` property (which is `false` by default). Set this property to `true` and Angular automatically puts properties specified on the isolated scope onto the `this` of the controller and ensures they are updated as necessary.

So let's rework the above example:

{% highlight javascript %}
angular.module('directives').directive('rikDirective', rikDirective);

angular.module('direvtives').controller('RikDirectiveCtrl', RikDirectiveCtrl);

function rikDirective(){
  return {
    restrict: 'EA',
    scope: {
      name: '='
    }
    controller: 'RikDirectiveCtrl as rik',
    bindToController:true 
  }
}

//now we don't have to inject the $scope
function RikDirectiveCtrl(){
  //no need to watch anything in here.
}

RikDirectiveCtrl.prototype.speak = function(){
  return "My name is " + this.name;
}
{% endhighlight %}