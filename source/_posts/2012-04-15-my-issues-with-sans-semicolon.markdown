---
layout: post
title: "On the sans-semicolon debate"
date: 2012-04-15 11:57
comments: true
categories: javascript
---

There was little community drama over the lack of semicolons that was causing an issue for a user of [twitter's bootstrap](https://github.com/twitter/bootstrap/issues/3057). I think the most pathetic thing here is the newer users who have to be stuck in the middle with broken code because everyone is teaching them different things; not to mention their actual issue(s) being ignored and burned by "community leaders" during their pissing matches.

Here are just a couple of examples that totally cause confusion amongst newcomers:

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

The issue here being `awesome.js` did not use semicolons, so once the two files were concatenated, an undefined function invocation was formed between the two imediate executing functions. 

The last issue I will mention is the exact issue on [twitter's bootstrap](https://github.com/twitter/bootstrap/issues/3057). Once the user took the recommended steps of minifying their project, the removal of whitespace smooshed together statements that were not seperated by semicolons, causing all sorts of wonky errors for the user.

``` javascript
clearMenus()
!isActive && $parent.toggleClass('open')
```

Some of these bugs are quite tricky to figure out, most novice JavaScript developers will have a difficult time pin-pointing them, especially since they occur in library code. If or once they do figure it out, [twitter's bootstrap](https://github.com/twitter/bootstrap/issues/3057) is a good example of what will happen when they seek help from the maintainer(s) of the very projects that are indirectly causing all the best practices learned to go to complete shit. No wonder we see web pages with 15 script includes, unminified, and doing everything that is recommended not to do.

There should not even be a debate whether semicolons are a required syntax or not. I think the simple fact that using semicolons causes no issues and not using them brings out various bugs should make it pretty apparent what we should be doing.




