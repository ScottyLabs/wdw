---
layout: guide
title: Frontend Web Development
subject: frontend
---

# JavaScript intro
> JavaScript is both the most popular and least popular programming language.
> 
> -- Doug Crockford

JavaScript is _the_ language of the web. It runs in every web browser, has
influenced a standard way of communicating data between computers, and has even
broken into the backend scene with technologies like [node.js][nodejs] and
[Meteor][meteor]. Since just about every computing device can connect to the
web and run JavaScript, in many ways JavaScript is the most "popular" language.

By that same token, there are a lot of intricacies and pitfalls that make
JavaScript unique. It's [these][watman] sorts of non-intuitive quirks that make
it difficult to use correctly. While JavaScript is very powerful, most people
who work in it regularly don’t like the way it was designed.

The next few sections of this guide will introduce you to the language’s
features and paradigms, and point you towards resources for further learning.

## Overview of JavaScript
JavaScript is as a programming language shares many features with other popular
programming languages that you may have encountered, such as Java, C & C++, and
Python. It's important to note at this point that __JavaScript is not Java__.
The fact that they share a name was a marketing ploy when JavaScript was first
released to increase it's popularity. Even though the two languages look
similar, the underlying languages are completely different.

As much as I'm going to try in this workshop, __it's impossible to learn to
program effectively in only a few hours__. With this in mind, it's expected that
you have had some sort of programming experience for you to get the fullest out
of this workshop. The aim of this workshop will be to introduce the syntax and
semantics of the language, with the ultimate goal of building a couple frontend
web apps. On that note, let's dive right in!

## Syntax Crash Course

### Variables & Objects
Variables in JavaScript are similar to variables in Python, and different from
those in C++ or Java. The biggest difference is that you don't declare the type
of a variable. In Java or C++ you have to decide what type of variable to use
when you create the variable. For example, you might have to declare a varible
to be an `int` or a `string`. However, Javascript works like python: you can
assign whatever value to a variable, and it's type will be resolved at runtime.
Here are some examples:

```javascript
var foo = 3.14;
var bar = "thon"
var baz = true;
```

As you can see from the examples, the `var` keyword is used to indicate that a
particular _identifier_ (like `foo`, `bar`, or `baz`) is meant to be used as a
variable. We use the `var` keyword regardless of the type of value we assign to
the variable.

### Types
As you can see from the previous example, there are a number of types which are
already baked into JavaScript. The following is a "complete" list of JavaScript
types:

#### `number`
This includes all number types: integers, floating point decimal numbers,
and two special types of "numbers" which are `NaN` for "not a number" and
`Infinity`. Their use is minimal in most programs, but it's still
interesting to know that they exist.

> ##### Important takeaway
> JavaScript makes no difference between integers and floating point numbers.
> This is different from probably all languages you have experienced previously.

#### `string`
This includes any number of characters in a row. There is no type that
represents a single character: "a" and 'a' are both strings of length 1.

> ##### Important takeaway
> JavaScript has support for strings built into the language.

#### `boolean`
The boolean type is very similar to all other languages. Note that in
JavaScript, every value is "truthy", meaning that trying to convert any
JavaScript value to a boolean is always well defined.

> ##### Important takeaway
> A boolean value can be either `true` or `false`.

#### `object`
JavaScript is object-oriented, though not in the way you might expect if you're
similar with Java or Python. Unlike the others, JavaScript uses "prototypical
inheritance" instead of class-based inheritance. JavaScript objects are very
powerful, but they’re a little harder to use and we’ll spend a lot of time
explaining how to use them.

> ##### Important takeaway
> JavaScript objects are super nifty, though using them for inheritance is
> nothing like what you'd expect from other languages.

#### `function`
In JavaScript, functions are values! This is actually really cool, and if
you've ever taken a class about functional programming (like 15-150 at
CMU) you know just how powerful functions can be. For those who haven't,
functions as values simply means you can store, return, and otherwise 
manipulate functions like any of the above types of values. JavaScript
makes heavy use of this fact, and it's one of the most expressive ways to
handle _asynchronous events_, which we'll discuss later.

> ##### Important takeaway
> Functions are values, so you can manipulate them as if they were numbers,
> strings, booleans, or objects.

#### `undefined`
There is one last type: undefined. Undefined is both a value and a type, and it
is generally used _only by the JavaScript language_ to indicate the quality of
an "absent" or "uninitialized" value. __Note__: JavaScript also has the `null`
keyword. The differences between null and undefined will be discussed below.

> ##### Important takeaway
> `undefined` is used to indicate that an expression was never assigned a value,
> whereas `null` is used for variables that are intentionally valueless.

### Null vs Undefined
In JavaScript, the reserved words `null` and `undefined` both have a similar
use: to describe that the value of some expression doesn't have a meaningful
value. 

You might be wondering, wait, don't "null" and "undefined" mean practically the
same thing? Why have both? For one thing, `null` is actually of type `"object"`
while `undefined` is it's own type. But the reason for there being two
apparently identical keywords is that `undefined` is used only by core language
features, whereas `null` is reserved for use exclusively by developers like you
and me. 

This aids in debugging: when you come across the value of some variable as being
`null`, you can be sure that you personally set it to null. On the other hand,
if something has a value of `undefined`, it's generally an indication that
something with the core JavaScript language functionality is involved.

This distinction doesn't necessarily help us get writing web apps more quickly,
but it's still an important point to bring up. This is one of the many
intricacies of JavaScript, an idiom that you will likely come across or have an
issue with at some point. Unfortunately, JavaScript is full of intricacies, and
there's no master list. That being said, [__this list__][airbnb] by AirBnb
comes pretty close to being exhaustive.

### Truthiness
As mentioned earlier, every JavaScript value is either "truthy" or "falsy".
What this means is that if you want, you can convert any JavaScript value into
a boolean. This conversion is done whenever you put a value inside a
conditional.  This makes some code really hard to read and other code really
simple; it helps if you understand the following rules governing which values
are "truthy" (or convert to `true`), and which are "falsy" (meaning they are
equivalent to `false`):

|  &nbsp;   |        falsy       |       truthy      |
|-----------|:------------------:|:-----------------:|
| number    | `+0`, `-0`, `NaN ` | all other numbers |
| string    | `""`               | all other strings |
| boolean   | `false`            | `true`            |
| object    | `null`             | all other objects |
| function  | n/a                | all functions     | 
| undefined | `undefined`        | n/a               |

### Objects
We've been hinting at what objects are in the previous discussion, but as of
yet, we've not introduced any concrete example of what an object in JavaScript
is. Objects in JavaScript are incredibly powerful because they're actually just
__mappings__ (like a hash table or dict) where _key-value_ pairs are stored. 

Here is an example of an object:

```javascript
{
    foo: 3.14,
    bar: "thon"
}
```

As you can see, an object is indicated by putting keys, followed by a colon,
followed by expressions or values, between curly braces and separating them with
commas. In the above example, "foo" and "bar" are identifiers, and `3.14` and `"thon"` 
are values. Since objects are values, we can store this in a variable:

```javascript
var myFirstObject = {
    foo: 3.14,
    bar: "thon"
};
```

and then access the _properties_ (or keys) of that object using one of two ways:

```javascript
myFirstObject.foo    === 3.14    // true
myFirstObject["foo"] === 3.14    // true
myFirstObject.foo    === 0       // false

// These have the value "thon"
myFirstObject.bar    === "thon"  // true
myFirstObject["bar"] === "thon"  // true
myFirstObject["bar"] === "hacka" // false
```

In addition to noticing that you can use both the dot (`.`) and subscript (`[]`)
operator to access an object's properties, you probably also noticed that we use
`//` for comments, and `===` for equality comparisons. This is another one of
JavaScript's quirks: using `==` is also sometimes valid, but it does weird
things with conversion which we'll actually talk about next!

### Operators & Conversion
The operators you'll find in JavaScript are pretty much the same as in any other
language. Here are a bunch: if you don't think you know what one of these
symbols means, look up [JavaScript operators][operators] to learn more:

<!-- don't ask me why java works and javascript doesn't -->
```java
+ - / * ++ -- ! ~ % << >> & | == === != !=== < > <= >= && || ?: = ,
```

In addition to these symbols, JavaScript has a few of it's own reserved words
that function as operators:

#### `typeof` returns the type of a value:

```javascript
> typeof(3.14)
'number'
> typeof("thon")
'string'
```

#### `delete` removes a property from an object:

```javascript
> delete myFirstObject.foo;
> myFirstObject
{ bar: 'thon' }
```

__Caveat about `delete`__: in JavaScript, arrays are actually just objects
where the keys are zero-indexed numbers (with a few special properties). This
means that we can use `delete` on arrays to delete individual elements, but
it’s oftentimes not what you want.

#### `in` tells you whether a given property is in an object

```javascript
> bar in myFirstObject;
true
```

__Caveat about `in`__: this operator will look for properties anywhere in the
object’s prototype. This means, for instance, that `’toString’ in {}` returns
`true`, because the function `toString` is a property of all objects through
the default prototype. Prototypes are discussed in more detail below.

We can also convert types between different values. This will happen whenever we
try to use an operator between two values that have different types. As an
example:

```javascript
> "ab" + 3
'ab3'
```

Note that here, because we had a string and a number, the final conversion was
to a string. Implicit conversion is highly irregular though, so you should always explicitly convert between types when you need to.

### Functions
There are more or less three ways of declaring functions in JavaScript: two of
them assign a name to the function, and the last way leaves the function
"anonymous", or nameless.

```javascript
// First named method: `function` keyword followed by identifier, (), and {}
function myFirstFunction() {
    ...
}

// Anonymous method: omit identifier
function () {
    ...
}

// Second named method: assign anonymous method to a variable
var myFirstFunction = function() {
    ...
}

// Third named method: sane scoping & named function in stack traces
var myFirstFunction = function myFirstFunction() {
  …
}
```

In this example, the anonymous method is so lonely! That's because normally when
you have an anonymous method, you are passing it directly into another function,
or declaring it and calling it at the same time. In both of these cases, you
don't need to give the function a name for it to be useful.

Function arguments are specified like in Python, but the keyword `function` is used instead of `def`:

```javascript
function mySecondFunction(arg1, arg2, anotherArg) {
    ...
    // use arg1, arg2, and arg3 variables
    ...
}
```

### Hoisting
Hoisting is another one of those JavaScript idiosyncrasies I keep talking about,
and it deals with how and when variables are defined. Put overly simply, 
whenever JavaScript encounters a variable declaration at any point within a 
_scope_, it _hoists_ the variable declaration to the top of the scope, settings 
its value to `undefined`. This can cause problems if you run into situations 
where the scope is complex, for example when using closures.

Because hoisting has been widely discussed elsewhere already, I'm simply going
to leave [this link][hoisting] here and let people read it. For the purposes of
this workshop, it shouldn't ever become an issue. However, hoisting is something
about JavaScript that all proficient web developers should have some grasp of.

### Constructors & Prototypical Inheritance
Alright, we're in the home stretch! This is the last section before we dive into
the much more exciting world of web app development. Hang in there!

JavaScript supports the programming paradigm known as Object-Oriented
Programming. This means that we need a way of constructing objects, something
which in C++ or Java is done with the `new` keyword, and which in Python is done
using simply the name of a class with the assignment operator.

In JavaScript, there is no concept of "classes". Instead, to create a
constructor, we simply declare a function:

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
```

We use the `this` keyword to indicate that a particular property (like "name" or
"age") should be stored on the object that we are constructing.

To invoke our constructor, we call this function after the `new` operator:

```javascript
var person1 = new Person("Jake", 19);
```

We can also manipulate an object's
_prototype_. An object's prototype is a sort of reserved area on an object where
JavaScript will check for a property if one isn't defined on the object
normally. For example, we can attach an `introduce` property to `Person`'s
prototype, and it will then be available on all subsequent `Person` objects:

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.introduce = function() {
    console.log("Hello, world! My name is " + this.name + " and I am " + this.age + " years old.");
}
```

Notice that `console.log` is just the way of printing a value to the console in
JavaScript, which can be seen by pressing Command + Option + J on a Mac or 
Ctrl + Shift + J on a PC (assuming that you're using Chrome).

Now, whenever we instantiate a Person, the introduce method will be available:

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.introduce = function() {
    console.log("Hello, world! My name is " + this.name + " and I am " + this.age + " years old.");
}

var person1 = new Person("Jake", 19);

var person2 = {
    name: "Jake",
    age: 19
}

person1.introduce(); // 'Hi! My name is Jake and I am 19 years old.'
person2.introduce(); // TypeError: Object has no method 'introduce'
```

Manipulation of prototypes is also involved in inheritance and the `instanceof`
keyword, which are both powerful techniques, but something that would take too
much time to introduce here. We've got web apps to write!

__For the lab portion of this session, visit [this page][lab]__.

- - -

Written by Jake Zimmerman, July 2014

[scottylabs]: http://scottylabs.org
[nodejs]: http://nodejs.org
[meteor]: http://www.meteor.com
[watman]: https://www.destroyallsoftware.com/talks/wat
[airbnb]: https://github.com/airbnb/javascript
[operators]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators
[hoisting]: http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html
[lab]: {{ site.baseurl }}/frontend/lab/
