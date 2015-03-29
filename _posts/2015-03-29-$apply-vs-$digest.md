---
layout: post
title:  "$apply vs $digest"
date:   2015-03-29 18:57:29
categories: angular
author: Rik
---
An angular `$scope` has both a `$apply` and `$digest` function but they are subtly different. First off what do they do?

##What they do

I am going to treat both functions as doing the same thing for now, I will elaborate on differences later. When you call `$apply` or `$digest` the `$scope` is checked for any updates that have occurred. If any are found then anything that relies on that value is updated to have the new value.

##When to use them

`$apply` or `$digest` should only be used when an update to a `$scope` value has occurred outside of angular. What do I mean by outside of angular? Well if you use an `ng-click` attribute angular will automatically take care of applying your updates, same if you use `$timeout` instead of `setTimeout`. If you use a `on('click')` then you must make a call to `$apply` or `$digest` in order for angular to be aware of any changes you made. You should never have a `$apply` or `$digest` call in a controller, they should only occur in directives.

##So what's the difference

Let's say we have two `$scope`s, scopeA and scopeB. They are two sibling scopes and share a reference to a user object. scopeA has a directive that updates the user on a `on('click')` and calls `$scope.$digest()`. Anything bound to scopeA will be updated but nothing bound to scopeB changes, even though the underlying object has changed. This is because `$digest` only checks the current `$scope` and its children for updates. Now if we used `$scope.$apply()` instead of `$scope.$digest()` suddenly everything bound to scopeB is updated too. What `$scope.$apply()` does is call `$rootScope.$digest()` which means all `$scope`s get checked for updates.

##So why not always use `$apply`?
Well performance is an obvious reason, why have to check all `$scope`s for changes when you can only check what you need? Its a subtly difference but it can have serious performance implications if you aren't aware of what the difference is.