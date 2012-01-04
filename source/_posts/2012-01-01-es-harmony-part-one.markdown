---
layout: post
title: "Harmony"
date: 2012-01-01 14:53
comments: true
categories: JavaScript, Harmony
---


Harmony is an ECMAScript (ES) project/effort that aims to improve the current ES spec (fifth edition) with new language features and some house cleaning of quirky behavior. It will ultimately form what will become sixth edition of ES. More details can found on [ES wiki](http://wiki.ecmascript.org/doku.php?id=harmony:harmony).

<!-- more -->

Some [Harmony slated](http://wiki.ecmascript.org/doku.php?id=harmony:proposals) features are starting to make their way into various JS engines for the intriqued to tinker around with. Right around Christmas time, [Google Chrome added a flag](https://plus.google.com/113127438179392830442/posts/T615Md5JPQG) to enable a few of them. [V8](http://code.google.com/p/v8/) is the JS engine underneath Chrome, so another usefull option is to [download and build V8 locally](http://code.google.com/apis/v8/build.html); you can then pass the `--harmony` argument to the V8 shell. I like this option because these features do not need a DOM and even though node.js also uses V8 under the hood, I don't have to muck around with multiple node installs, etc.

``` sh Executing a script via the V8 shell.
~ $ d8 my_script.js --harmony
```

Mozilla's JS engine, [SpiderMonkey](https://developer.mozilla.org/en/SpiderMonkey), implements some of these features as well and actually quite a few others which have been slated for the Harmony spec. Most of these require an opt in too, so you need to pass the version flag with the latest version to the type attribute on the script tag.

``` html Opt in via the script tag version.
<script type="text/javascript;version=1.8"></script>
```

Just as with V8, you can [download and build SpiderMonkey locally](https://developer.mozilla.org/En/SpiderMonkey/Build_Documentation). This is actually how I currently prefer to try out new features that I come across. The only real reason for this decision is that currently SpiderMonkey has a few more features to play around with than V8.

``` sh Executing a script via SpiderMonkey.
~ $ js -f my_script.js
```

I will attempt to explore new additions as they are implemented, each one having a post categorized under [harmony](/blog/categories/harmony). Be sure to check back for updates, as I am sure something will change and I will try to update accordingly.



