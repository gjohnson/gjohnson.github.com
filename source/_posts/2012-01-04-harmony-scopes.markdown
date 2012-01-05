---
layout: post
title: "Harmony - Scope"
date: 2012-01-04 00:04
comments: true
categories: 
---

Harmony finally introduces block scope into JS. While the syntax of blocks have always been in JS, they have had no associated context for variables to bind to. This is something you may be familar with if you have ever written any C.

``` c Block scoped variables in C.
#include <stdio.h>

int main() {
    char foo[] = "foo 1";

    printf("%s\n", foo); // => "foo 1"

    {
        char foo[] = "foo 2";
        char bar[] = "bar 1";
        printf("%s\n", foo); // >= "foo 2"
    }

    printf("%s\n", foo); // => "foo 1"
    printf("%s\n", bar); // => Compiler error about undeclared `bar`.

    return 0;
}
```

As shown in the example above, the declared variables within the block starting on line 8 have no side effects on the variables with the same indentifier declared in the function body block. However, as you probably know, this is not the case in JS; the only context that variables can bind to is locally to a function or globaly.

<!-- More -->

``` javascript Historically a block had no context associated with it in JS.
function main() {
    var foo = 'foo 1';
    var bar;

    print(foo); // => 'foo 1'

    {
        var foo = 'foo 2';
        var bar = 'bar 1';
        print(foo); // => 'foo 2'
        print(bar); // => 'bar 1'
    }

    print(foo); // => 'foo 2'
    print(bar); // => 'bar 1'
}
```

As previously mentioned, Harmony will fix this by adding block scope binding of variables; it will be achieved through the introduction of the `let` keyword. The syntax change is required because changing the scope semantics of `var` to bind to block scope would break the entire internet, however `let` can certainly be used to replace `var`.

``` javascript Using let as a var replacement.
function main() {
    let foo = 'foo 1';
    let bar;

    print(foo); // => 'foo 1'

    {
        let foo = 'foo 2';
        let bar = 'bar 1';

        print(foo); // => 'foo 2'
        print(bar); // => 'bar 1'
    }

    print(foo); // => 'foo 2'
    print(bar); // => undefined
}
```

``` javascript Scoping variables within the block of a condition.
if (true) {
    let foo = 'bar';
    print(foo);
} else {
    let foo = 'bum';
    print(foo);
}

print(foo); // => throws ReferenceError
```

``` javascript Scoping "counter" variables of a for-loop.
for (let i = 0, len = 10; i < len; i++) {
    print(i);
}

print(i); // => throws ReferenceError
```

``` javascript Scoping variables within the block of a loop.
let i = 10;

while (--i) {
    let foo = 'foo ' + i;
    print(foo);
}

print(foo); // => throws ReferenceError
```

You will notice in the last example that `let` can actually be used in the global context, even when no block is declared. It will behave just like a global variable would. I think the fact that this behavior was been implemented strongly encourages to work towards treating `let` as a `var` replacement.

Using `let` is not the only new keyword being introduced with blocked scoped bindings. There is also `const`, which is used to declare a constant. While this has been around for a while as a non-standard in a few JS engines, it has been re-defined to follow the block scope binding spec in Harmony.

``` javascript Constants follow block scoping rules.
const hello = 'hello';

{
    const goodbye = 'goodbye'
    print(hello);
    print(goodbye);
}

print(hello);
print(goodbye); // => throws ReferenceError
```

While it might be apparent to some, I will still mention that unlike variables declared with `let` or `var`, a constant cannot be declared without an initializer. When a constant is declared, a value must be assigned.

``` javascript Constants require an intializer, otherwise a SyntaxError will be thrown.
const foo;
foo = 'fooooo';
```

Variables should also not share the same identifier as a constant. Currently Spidermonkey implements this behavior, however V8 as of (v.3.8.4) will correctly throw an error when a variable is declared with the same identifer as a previously declared constant. However V8 will not throw an error when a constant is declared with the same identifer as a previous declared variable. IMHO Spidermonkey got this right, and perhaps this will be fixed in V8.

``` javascript Constant re-declaration errors.
// Both engines will correctly throw a TypeError here.
const bum = 'bum';
let bum = 'bum bum';

// However only V8 allows this, while Spidermonkey still throws a TypeError.
let bar = 'bum bum';
const bar = 'bum';
print(bar);
```

The additions for scope in Harmony will certainly promote cleaner code and I definitely look forward to using them.







