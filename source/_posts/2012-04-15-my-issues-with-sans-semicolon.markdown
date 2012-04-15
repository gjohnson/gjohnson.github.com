---
layout: post
title: "On the sans-semicolon debate"
date: 2012-04-15 11:57
comments: true
categories: javascript
---

There was little community drama over the lack of semicolons that was causing an issue for a user of [twitter's bootstrap](https://github.com/twitter/bootstrap/issues/3057). I think the most pathetic thing here is the newer users who have to be stuck in the middle with broken code because everyone is teaching them different things; not to mention their actual issue(s) being ignored and burned by "community leaders" during their pissing matches.

Users are taught that it is a best practice to lint check their projects. They set their directives to require semicolons, among other things because their JavaScript Book said this is important. However the lint check reports are so convoluted with errors about missing semicolons from external dependencies, they stop running link checks all together until the project structure can be re-organized in a fashion where external dependencies are not link checked.

> **"Too many errors. (12% scanned)."**

Users are also taught the benefits of splitting a project into multiple source files and to concatenate those files, along with any smaller external dependencies into a single file for deployment. This also helps get around the ignored lint check errors mentioned previously. However, with a perfect score on the link check report, loading their application in the browser stops in it's tracks with the following error:

> **"TypeError: undefined is not a function"**

It ends up that after concatening their project it ended up looking like this:

``` javascript
/*!
 * This is the awesome.js library that is portable and runs EVERYWHERE!
 */
!function(global, undefined){

}(window)

/*!
 * This is the users code, wrapped in one of those nifty imediate executing functions they learned
 * was also a best practice.
 */
(function(global){
    
})(window, undefined);
```

Most new-ish JavaScript developers are not going to figure out why that does not work, nor understand it. If or once they do, [twitter's bootstrap](https://github.com/twitter/bootstrap/issues/3057) is a good example of what will happen when they seek help from the maintainer(s) of the very projects that are indirectly causing all the best practices learned to go to complete shit.

There should not even be a debate whether semicolons are a required syntax or not. I think the simple fact that using semicolons causes no issues and not using them brings out various bugs should make it pretty apparent what we should be doing.




