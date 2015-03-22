---
layout: post
title:  "Fun with $parsers"
date:   2015-03-22 18:57:29
categories: angular
author: Rik
---
The NgModelController has two extremely useful properties, ``$parsers`` and ``$formatters``. ``$parsers`` is an array of functions that sanitize/convert values taken from the DOM. $formatters is an array of functions that format/convert model values before they are displayed in the UI.

##$parsers in action  

Recently created a directive that uses ``$parsers`` to validate the DOM value against the specified regex. If it doesn't match the regex is simply returns and empty string.

<script src="https://gist.github.com/rikbrowning/0e458bc85235f215e587.js"></script>