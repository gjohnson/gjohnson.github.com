---
layout: post
title: "Harmony"
date: 2012-01-01 14:53
comments: true
categories: JavaScript, Harmony
---


Harmony is an ECMAScript (ES) project/effort that aims to improve the current ES spec (fifth edition) with new language features and some house cleaning of quirky behavior. It will ultimately form what will become sixth edition of ES. Details can found on [ES wiki](http://wiki.ecmascript.org/doku.php?id=harmony:harmony).

Some [Harmony slated](http://wiki.ecmascript.org/doku.php?id=harmony:proposals) features are starting to make their way into various JS engines for the intriqued to tinker around with. Right around Christmas time, [Google Chrome added a flag](https://plus.google.com/113127438179392830442/posts/T615Md5JPQG) to enable a few of them. [V8](http://code.google.com/p/v8/) is the JS engine underneath Chrome, so another usefull option is to [download and build V8 locally](http://code.google.com/apis/v8/build.html); you can then pass the `--harmony` argument to the V8 shell. I like this option because these features do not need a DOM and even though node.js also uses V8 under the hood, I don't have to muck around with multiple node installs, etc.

Mozilla's JS engine, [SpiderMonkey](https://developer.mozilla.org/en/SpiderMonkey), implements these features and actually quite a few others which have been slated for the Harmony spec. Most of these require an opt in as well, so you need to pass the version flag with the latest version number to the type attribtute on the script tag: `<script type="text/javascript;version=1.8"></script>`. Just as with V8, you can [download and build SpiderMonkey locally](https://developer.mozilla.org/En/SpiderMonkey/Build_Documentation).

I will attempt to explore new additions as they are implemented, each one having a post categorized under [harmony](/blog/categories/harmony). Be sure to check back for updates, as I am sure something will change and I will try to update accordingly.



