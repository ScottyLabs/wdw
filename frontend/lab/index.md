---
layout: guide
title: Frontend Web Development
subject: frontend
---

# frontend lab
In this lab, you'll be introduced to jQuery, a popular library that helps speed
up JavaScript web development to build interactive web pages.

## Overview
The goal of this lab is to create a web app that will let us play the game
"Galumphing Banderwoozles." I didn't come up with the name: the Spring 2014
15-251 TA's did.

Nontheless, the rules of the game are as follows: 

- You are given a board composed of 15251 by 15251 tiles. 
- Any tile can be one of three colors: __red, green, or blue__.
- Initially, all tiles are blue, except for the tile in the top left corner,
  which is green.
- The object is to __turn the entire board red__.
- Green tiles can be clicked to turn them red. __Once a tile is red, it stays
  red__.
- Clicking a green tile also affects it's neighbors to top, right, bottom, and left.
    - When a green tile is clicked, __all neighbors that are currently blue
      become green__, and __all those that are green become blue__.
    - Recall that the red tiles stay red.

These rules are pretty confusing. If you want to get a feel for how the game
works, you can play a working demo of the game __[here][galumphing]__. Simply
enter a board size (say, 5 rows by 5 columns) and start clicking on the green
tiles.

15251 by 15251 is pretty big, so for our purposes, we're going to let the
player decide how big to make the board. Going one step further, this tutorial
in general requires you to recall the rules of this game very rarely. As long
as you know what goal we're trying to achieve (which will almost always be
stated), the only struggle should be figuring out the JavaScript required to
implement it.

## Diving in
The code and tutorial for this lab will be [hosted on GitHub](source-final). Each step is a
commit, allowing you to see what changed between steps. Links will be provided
to the code of the step in question. Most of the explanations will not make
sense if you do not also take a look at the corresponding code, so be sure to
do that.

## Step 1: Initial HTML and CSS
__[download starter code][starter-code]__, __[diff for this step][diff-1]__, __[code at this step][step-1]__

The first step takes care of getting the starter code. You can download it
[using this link][starter-code]. The starter code should contain two files when
unzipped: a file called index.html and one called styles.css.

For more information about how to create things like this, check out the
Web Dev Weeks talk on [HTML & CSS]({{ site.baseurl }}/html/).

Skimming over this step's code, you can see that we've included our
styles.css file containing all of our CSS, as well as an external file
called normalize.min.css which will also help make things appear
correctly.

You can also see a rough sketch of how the app will look: we've got a
couple of text inputs to get the board size, we've got a couple of
counters to keep track of some game stats, and we've got the
`tile-wrapper`, which will hold the code for all of our tiles.

If you're interested in this, you should definitely check out the [HTML & CSS
workshop]({{ site.baseurl }}/html/), which shows you how to come up with the
styles and content of a web page.

## Step 2: Load the external scripts
__[diff for this step][diff-2]__, __[code at this step][step-2]__

Now that we have all the HTML & CSS in place, we need to tell the
browswer where to look to load the JavaScript files that we'll be using.
This is done with the `<script>` tag.

For this project, we'll be using two different JavaScript sources.
First, we'll load the jQuery, a JavaScript library that helps out
tremendously with adding event listeneres, manipulating the DOM, and
doing other routine tasks. jQuery is a library written and hosted by
someone else: this means we need to go grap an external link to it. To
find it, search the Web for "Google jQuery CDN". (A CDN, or content
delivery network, is basically a super-fast network designed for hosting
commonly-requested files.) On the first result page, you should see a
large list of Google hosted libraries. Find the one titled jQuery,
copy the `<script>` tag under it, and paste it into the file `index.html`.

Now that we've loaded our helper JavaScript library, we need to load the
file which will contain our core application code. We'll be calling this
file `main.js`, so add a `<script>` tag that looks similar to the one
you just copied, but with a source of `src="main.js"` instead:

```html
<script src="main.js"></script>
```

With these lines in place in `index.html`, we should be good to go! Now
we can start writing the core JavaScript code for our game.

## Step 3: Add starter code in main.js
__[diff for this step][diff-3]__, __[code at this step][step-3]__

We're finally at the point where we can add some code to our `main.js`
file!

With the first few lines, we get the opportunity to see one of the many
quirks about JavaScript: something that's not really necessary but that
makes life a little bit easier.

We're going to add the following lines to our JavaScript file:

```javascript
;(function() {

})();
```

What these lines do is _terminate any previous, dangling JavaScript
statement_ (with the first semi-colon), _create an anonymous function_
(with the `function` keyword), and then _immediately call it_ (with the
`()` towards the end). This ensures that we have our own execution
context for all the code that we write. You can read more about it
[here](http://sarfraznawaz.wordpress.com/2012/01/26/javascript-self-invoking-functions/),
but you're almost always going to want to follow this convention when
writing JavaScript files.

## Step 4: Listen for ready event
__[diff for this step][diff-4]__, __[code at this step][step-4]__

If you're familiar with a language like C/C++ or Java, you'll know that
every application must have an entry point that's usually called `main`.
In Python there's a similar concept using globally defined variables
like `__name__`.

JavaScript has no such entry point. When JavaScript is run in a
browswer, each line is run as it is encountered. While this is powerful,
there are many times when being able to run a particular command when
the page is ready for it to be run is useful. For this purpose, we use
_event listeners_ to run a particular function once a corresponding
event occurs. Events are generated for many different actions and
conditions within the browser; one of these is the `ready` event, which
is fired on the `document` object whenever the page is, well, ready for
us.

We can then attach a _listener_, or a specialized function, to this
event, effectively allowing us to run a particular piece of code
whenever the event fires. This function can either have a name or be
anonymous. We'll chose the latter:

```javascript
$(document).ready(function() {

});
```

What this does is attach an empty function to the `ready` event of the
`document` element. This syntax is actually a call to a jQuery function:
the `$` is the variable name for all the things that jQuery provides,
and the `.ready()` method is a utility method for attaching listeners to
`ready` events.

This concept that we've used here of attaching a function to an event
and having it be run at a later point is _incredibly common_ in
JavaScript. In fact, it might be JavaScript's most powerful feature.
When used in this manner, the function that we attached to this event is
called a _callback_.

## Step 5: Add `play` function
__[diff for this step][diff-5]__, __[code at this step][step-5]__

Now that the "ready" event listener is in place, we can add some
boilerplate functions for where we'll write the brunt of our game code.

First, we'll need a function called `play`, which for right now will
remain empty. This function is also going to be an event listener, so
it'll take a single argument representing the event that triggered the
function to be called. You may notice that the anonymous function we
registered on the `ready` event also is an event listener, and so it
receives an event object as well. However, since we don't use it (and
almost always won't on the `ready` event), we omit it for simplicity.
This is possible because in JavaScript, _the number of arguments passed
to a function does not have to equal the number declared_.  For more
information, see [here][arguments].

Now that we've got our empty `play` function in place, we're going to
add it as an event listener on the `click` event of the submit button.
This button has an `id` of `submit`, so we can use jQuery to select that
element and bind the click event on that element to our `play` function.

[arguments]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/arguments

## Step 6: Get the user's input for rows and columns
__[diff for this step][diff-6]__, __[code at this step][step-6]__

So now we have a function that will be executed every time the user
clicks on our submit button. Let's start filling it in with something
useful.

We said one of the things we'd have to do in order to set up the game
state was to let the user choose how many rows and columns there should
be. Using the two text that are present in the HTML of the page, we can
do just this.

By the time the user clicks on our submit button and fires off the
`play` function, the text inputs with id's of `rows` and `cols` will
be holding values corresponding to the number of rows and columns that
our board should have. We can use jQuery to extract these values, using
the `.val()` function. We'll go ahead and store these values in global
variables.

Now is also a good time to deal with the circumstance when the user
accidentally hits submit twice. What should happen? Should we start a
fresh game? Add or remove rows from the game in progress? There are
many ways we could handle this situation. For sake of simplicity, we're
just going to remove the submit button and both text inputs entirely,
thereby ensuring that we don't have to deal with this weird
cirtumstance. After selecting the form with id `args` that wraps the
text inputs and submit button, we can use the `.detach()` method to
remove them from the DOM.

## Step 7: Prevent form submission event from bubbling up
__[diff for this step][diff-7]__, __[code at this step][step-7]__

Once make the changes introduced in the previous step, go ahead and see
if clicking the button removes the `#args` form. The best way to
preview your work is to start a simple Python webserver running in your
project's directory with

```javascript
$ python -m SimpleHTTPServer
```
then open [http://localhost:8000](http://localhost:8000/) in your browser. If
you need help with this, flag down a mentor! Otherwise, just open the
index.html file in your browser. __Note__: if you don't use the Python command
to preview your site, you will have to slightly change two lines. First, change
line 9 of index.html to 

```html
<link rel="stylesheet"
href="http://cdnjs.cloudflare.com/ajax/libs/normalize/3.0.1/normalize.min.css"
type="text/css">
```

(add `http:` after `href="`), and change the line that loads jQuery within
index.html (the line you copied and pasted from Google Hosted Libraries) to 

```html
<script src="http://<the link that you copied>"></script>
```

(add `http:` after `src="`). Note that `<the link you copied>` is whatever link
you copied from Google Hosted Libraries.


What you'll probably notice is that the form didn't disappear, and it
looked like the website reloaded the page. If you look carefully, you'll
probably also see that the URL changed to something with variable names,
question marks, and ampersands. This happened because of something
called `bubbling` which is another JavaScript feature which can seem
like a quirk at times.

Whenever there is a button inside a form and the button is clicked, the
browser thinks that the values of the inputs within that form need to be
submitted. If you don't specify where to submit this information on the
`<form>` tag, then it assumes that you want it to be submitted to the
current URL, effectively reloading the page.

This is pretty annoying, because we'd actually like to run our own code
instead of having the browser do something for us. To turn this feature
off, we have to understand what's actually going on. Nearly every action
a user has with a page generates some sort of event. Even though an
event might have a particular element from which it originated, the
event it self propagates up through the DOM tree from that element to
it's parent element all the way until it reaches the `<html>` tag. This
is what's known as `bubbling`, because the event bubbles up the DOM.

Our particular event handler is listening on the button itself, whereas
the form submission event is attached to the form element; we want to
shut off the bubbling before it can get there. To do this, we can use
the event argument `e` that will be passed into our `play` function. By
calling `e.preventDefault()`, we can stop the "default" action (the
event bubbling upwards) from occuring.

Try adding this line and see what happens. You should see that the
`#args` form detaches and stays detached. If not, flag down a mentor!

By now, you're probably starting to understand that there are a lot of
idiosyncrasies in JavaScript who's solutions are not obvious. In cases
like these, your best debugging tool is the ability to carefully
describe what problem you're having and searching for it on Google. At
least when you're starting out, it's likely the problems you will
experience will have relatively simple, though non-intuitive, solutions.
Being able to Google effectively is invaluable in times like these.

## Step 8: Initialize the game's starting state
__[diff for this step][diff-8]__, __[code at this step][step-8]__

Now that we can accept the user's input with our form, we can actually
begin setting up the initial board configuration. Specifically, the user
has told us how many rows and columns to use, so we can use a nested for
loop to set up the grid with the right dimensions.

HTML elements are display and drawn across and then down, we're going to
draw one row at a time (as opposed to one column at a time). To make
things easier, we're going to wrap each row in a div with the class
`tile-row` so that we can access arbitrary rows.

To create a new DOM element (basically, an element in the page), we use
the jQuery function (`$`) with a string argument representing the HTML
that we should use to construct that object. We just need to create a
`<div>` with a class of `tile-row`, so the string we want is `'<div
class="tile"></div>'`. We can then store this in a variable named
`$curTileRow` (note that `$` is a perfectly valid character to use in a
JavaScript variable name). Finally, we use the jQuery append method to
append this tile row to the tile wrapper.

We'll be using a multidimensional array to maintain what color each
board piece is. JavaScript arrays aren't fixed in length (because
they're actually just special objects), so we'll be dynamically adding a
row every time we need a new one. What that means for us is that within
the outer loop, where code will be executed once per row, we should add
a row to our multidimentional array. This is done with the code
`boardColors[curRow] = [];`, which sets the contents of the curRow'th
row to an empty array.

Now that we've done the required setup for each row, we can work on
adding the individual tiles that will ultimately constitute the columns.
We'll add a for loop inside our outer for loop that ranges over the
entire number of columns.

The first thing this inner loop should do is create the DOM element for
the tile residing in that column. This is done with the jQuery append
method that we used before to add a row to the outer, wrapper div. Next,
since all but the top left tiles should start out blue, we'll set the
color of this tile to blue (and worry about the one green one later).
I'll use a helper function called `setColor` to set the color of a tile.
It'll take a row, column, and a string representing a color. We'll write
this function after the next step. For now, just know that it takes care of
setting the color for us.

Finally, we'll have to set the click event on the div to handle what
should happen when the user "makes a move," or attempts to change the
color of a tile. This part is actually very sophisticated! We're going
to be using a technique called closures, which is a very powerful
concept that is used quite frequently in JavaScript.

The basic paradigm stems from the fact that JavaScript maintains a
context of all the variables and their values for every function that is
created. That means that we can create special contexts that bind
additional variables that a function would find useful to use.

First you'll note the helper function `getTile`. We'll write this helper
function in after next step as well, for but for now just now that it's
basically a wrapper around the `$` function that we've been using this
whole time.  What that means is that it returns to us the same jQuery
DOM object that we would normally get back, so we can set the `.click`
attribute of that result to bind a function to the click event of that
particular DOM element.

Next, we have an anonymous function wrapped in parentheses,
(function(r, c) {...}), followed by `(curRow, curCol)`. When you see
this, a function definition wrapped in parentheses immediately followed
by parentheses, this will create an anonymous function and _immediately
call it_ with the arguments specified in the second set of parentheses.
This is called a self executing function, and you can read more about it
[here](http://markdalgleish.com/2011/03/self-executing-anonymous-functions/).

Remember that the argument to the `.click` function needs to be a
function which takes one variable: the event object `e` that triggered
the click event. We're actually going to use this self-executing
function to _return a different function_. What's special about this
returned function is that it will have access to the parameters of the
outer function, namely the current row and current column. We can then
reference those inside our returned function; in our case, we're going
to pass them on to `move`, a third helper function that will take care
of the brunt of the game logic for us. We'll start writing that function
in three steps.

Since the function we pass to click must take an event object as an
argument, we'll make the function we return take just that argument, and
we'll pass it on to `move` just in case we need it.

That's it for the processing we need to do within the loop! If you
remember from before, I said that we'd take care of changing the upper
left tile to green later, so let's go ahead and do that now. Remember
that we use a helper function for this before, so we'll use the same
function again now.

## Step 9: Set the initial values on the "scoreboard"
__[diff for this step][diff-9]__, __[code at this step][step-9]__

One last thing to take care of before we start going nuts with our game
is to set up number of greens, blues, and total tiles, and then display
these values.

We'll initialize a few global variables called `reds`, `greens`, and
`blues` to 0, set `greens` to 1 (for the upper left tile), and set
`blues` to the remaining number of tiles. Obviously, the total number of
tiles is `rows * columns`, and this will be important because we will
know the user has won if the number of reds is equal to this value.

Finally, we'll use a couple more jQuery calls to display these values.
The `.html` function on a jQuery object will set the inner HTML of that
attribute to the text specified (if you pass something that's not a
string, it will try and cast it to a string). That means we can use this
method, passing it `blues` and `greens` respectively, to set these
colors to the right values. Remember that the HTML elements with id's
`blues` and `greens` house the data we want to display. Note that we
don't have to worry about setting the number of reds because it should
already be set to 0 in the HTML (you can verify this).

## Step 10: Define a couple useful helper functions
__[diff for this step][diff-10]__, __[code at this step][step-10]__

As I mentioned two steps ago, we're going to now define the helper
function we used to both set a tile's color given its indices, and to
get the DOM node of an element given its indices.

The first of these, `getTile`, is a one-liner, though it is a bit
complicated. We'll be using the jQuery/CSS `:nth()` pseudo-selector,
which basically allows us to access the nth element of a particular
class. We'll also be using the `>` selector, which selects the children
of a particular node. Remember that we wrapped every row in a div with
the class `tile-row`, so to get the nth row we can use `.tile-row:nth('
+ row + ')`. Then we want to access an individual tile (an element with
the class `tile`), which is a child of a `tile-row`. That means the next
selector needs to be a `>`. Finally, we want the nth tile, so in a
similar fashion to before, we want to use `.tile:nth(' + col + ')`. If
you hadn't already figured it out, the `:nth()` pseudo-selector takes as
an argument an integer which represents the index of which element it
should select.

Next up is `setColor`. We have two things to do: update our internal
representation of the colors of the tiles, and then actually change the
color of the element. Remember that we've been storing our internal
representation of the board's colors in a multidimensional array called
`boardColors`. We want to access the element at `[row][col]` and set
it's contents to `color`. We'll use this stored value later in
processing what to do when the user clicks on a tile.

The second thing to do is change the actual color of the tile. In the
CSS stylesheet (styles.css), there are a bunch of handy classes that
will turn our element a particular color depending on which class is
applied. First, we want to get the DOM element represented by the row
and column we are dealing with, which is simple enough because we have a
helper function to deal with that! We'll next use the `.removeClass`
jQuery method to remove any previous color class that had previously
been attached to this element, and then the `.addClass` method to add
the class corresponding to the color we want to make this tile.

There are a couple of things to note here. The first is that if
`removeClass` doesn't find the class you specified to remove, it doesn't
do anything.  The second is that you can _chain jQuery calls_. Note that
there are no semicolons after each line, only the last line. Every time
we call a jQuery method that's operating on a DOM element like this, we
can chain as many calls as we want on top of each other to keep
modifying the current jQuery DOM element.

## Step 11: Start writing move function: get adjacent tiles
__[diff for this step][diff-11]__, __[code at this step][step-11]__

We're approaching the home stretch! `move` is the last function we'll
need to implement.

Recall that `move` will be called every time someone clicks a `tile`
element, and it will have access to the current row and column because
of the closure we used when initializing the click event. We'll use this
method to handle processing all the rules of the game that we outlined
in the Overview.

In the rules, we specified that the only tiles we can actually click on
are the green ones, so let's check if the current tile is green.

Remember that we have access to the row and column of the clicked tile
from the parameters to the `move` function, and we have a
multidimensional array which will give us the color of a tile given a
row and a column. Once we have this stored in a variable, we can check
to see whether that color is `'green'`.

If it is green, we need to change it's color to red, increment the
number of reds, and decrement the number of greens.

## Step 12: Get and check whether the neighbors are valid
__[diff for this step][diff-12]__, __[code at this step][step-12]__

Once we've toggled the current tile to red, we need to process the
current tile's neighbors. If we know what the current row and column
are, we can easily get the row and column of the neighbors by adding or
subtracting one to the appropriate variable.

Note that some of these cells will actually not be valid; for example,
if we are in the 0th row, trying to access the 0 - 1 = -1th row will be
invalid. We can check whether a variable is valid by checking the
appropriate condition... beware of off by one errors!

To make things easier, we're going to utilize the fact that JavaScript
variables are dynamically typed. Since we don't have to declare a
variable's type, we could assign either a jQuery DOM element or `null`
to a variable and let the JavaScript interpreter determine this at
runtime. Combining this with the JavaScript _ternary operator_,
`<condition> ? <value if true> : <value if false>`, we can very
conveniently check the edge conditions, get the neighbor if safe, and
evaluate to `null` if not.

Once we've done this, I'm going to stick all four variables into an
array with their corresponding coordinates so that we can conveniently
iterate over the array, and do the same processing for all four.

## Step 13: Use Array.forEach to iterate over each neighbor
__[diff for this step][diff-13]__, __[code at this step][step-13]__

This time, when iterating over each potential neighbor, we're going to
use a different style of JavaScript for loop called `Array.forEach`.
This is a function present on all JavaScript arrays that allows you to
loop over all the elements of a list without using indices.

The way this works is you specify a function to the `.forEach()` method.
This function takes as parameters the current element of the list, the
index of the current element, and the a reference to the array the
function was called on (in our example this isn't necessary because we
have access to the original array variable, but there are times when
this isn't the case). Since this function is a callback, it will be
evaluated once for each element of the array, and the appropriate values
will be substituted in.

## Step 14: Process each neighbor within Array.forEach
__[diff for this step][diff-14]__, __[code at this step][step-14]__

Within the forEach callback, we want to check to make sure that the
current neighbor we're processing exists, i.e. is not null. Since the
actual element we're iterating over is an object containing the
properties `tile`, `row`, and `col`, we need to check the
`$neighbor.tile` property to see if the element itself exists. Since
JavaScript values are all truthy, an object is only ever falsy if it's
null, we can simply use `if($neighbor.tile)` to check whether the
neighbor exists or not.

Now that we know whether the neighbor exists, we can do the appropriate
processing. Particularly, what we need to do depends on the color of the
current element. Let's get the color of the current neighbor using the
same method we did for the clicked tile (making care to draw the row and
column from the properties we set on the current `$neighbor` variable).

Now we can case on the color of the current element. If it's green,
we'll need to toggle it's color to blue and adjust the number of blues
and greens, and vice versa it the neighbor is blue.

## Step 15: Update scoreboard and check for winning conditions
__[diff for this step][diff-15]__, __[code at this step][step-15]__

The only thing left to do is update the scoreboard and check whether the
player has won the game.

If you recall the code to update the scoreboard from early, we will use
the same code now, but add an additional line to update reds (because
reds will have definitely changed this time).

If the number of reds is equal to the total number of tiles, that means
that every tile has been flipped, so the user has won. If the number of
greens is 0, then the user lost, because there aren't any tiles that can
be flipped. There's a JavaScript function `alert` that lets you display
a message in a dialog box, so we can use this to report a win or a loss.

It turns out that some boards are winnable and some boards aren't (if
you're interested you should try to prove it). Regardless of this, I
thought it'd be funny when I made this game and distributed it to my
fellow 251 classmates to tell them that a non-winnable board was in fact
winnable... it had some interesting consequences. Feel free to change
the winning and losing messages to something more "agreeable."

The final thing we'll take care of is reload the page for if the user
want to play again. We can do with with `location.reload()`, which will
take the current page's URL and reload that addresss.

That's it! You should be able to try everything out and have it work in
the browser. If you're still stuck, or you've got errors, flag down a
mentor or ask someone for help and we'd love to give you some hints to
fix everything up.

Thanks!

- - -

I take great pride in writing good code, documentation, and tutorials. If you
spot something that's not quite right or you spot something confusing, let me
know! Write an email to webdevweeks@scottylabs.org and include the url of this
page in your email.

Written by Jake Zimmerman, July 2014

[galumphing]: http://scottylabs.org/webdevweeks/frontend/demo/

[source-final]: https://github.com/Z1MM32M4N/jquery-lab/
[source-final-zip]: https://github.com/Z1MM32M4N/jquery-lab/archive/gh-pages.zip

[starter-code]: https://github.com/Z1MM32M4N/jquery-lab/archive/7a570d3b69f20f89ee14f53c1f67f0e277b02dcb.zip

[diff-1]: https://github.com/Z1MM32M4N/jquery-lab/commit/7a570d3b69f20f89ee14f53c1f67f0e277b02dcb#diff-0
[step-1]: https://github.com/Z1MM32M4N/jquery-lab/blob/7a570d3b69f20f89ee14f53c1f67f0e277b02dcb/index.html

[diff-2]: https://github.com/Z1MM32M4N/jquery-lab/commit/1758ef9a9680baab2fadbeb18804b4fdac5e1e76#diff-0
[step-2]: https://github.com/Z1MM32M4N/jquery-lab/blob/1758ef9a9680baab2fadbeb18804b4fdac5e1e76/index.html

[diff-3]: https://github.com/Z1MM32M4N/jquery-lab/commit/57850d9aeffe58f11f3eda00b5c5efc56cf335b3#diff-0
[step-3]: https://github.com/Z1MM32M4N/jquery-lab/blob/57850d9aeffe58f11f3eda00b5c5efc56cf335b3/main.js

[diff-4]: https://github.com/Z1MM32M4N/jquery-lab/commit/0c558e73168bbac72ad48a448d72a1c9996f87fc#diff-0
[step-4]: https://github.com/Z1MM32M4N/jquery-lab/blob/0c558e73168bbac72ad48a448d72a1c9996f87fc/main.js

[diff-5]: https://github.com/Z1MM32M4N/jquery-lab/commit/3ac0b325290e000c62db61ec46180d80a861cd6e#diff-0
[step-5]: https://github.com/Z1MM32M4N/jquery-lab/blob/3ac0b325290e000c62db61ec46180d80a861cd6e/main.js

[diff-6]: https://github.com/Z1MM32M4N/jquery-lab/commit/4096958f937c051910e7f02343107842a0af3056#diff-0
[step-6]: https://github.com/Z1MM32M4N/jquery-lab/blob/4096958f937c051910e7f02343107842a0af3056/main.js

[diff-7]: https://github.com/Z1MM32M4N/jquery-lab/commit/7539b3c3bef06d8017875029ae6170205e24b6ed#diff-0
[step-7]: https://github.com/Z1MM32M4N/jquery-lab/blob/7539b3c3bef06d8017875029ae6170205e24b6ed/main.js

[diff-8]: https://github.com/Z1MM32M4N/jquery-lab/commit/6f03b66c13a7854af0c966bc54538e3d394f6b0c#diff-0
[step-8]: https://github.com/Z1MM32M4N/jquery-lab/blob/6f03b66c13a7854af0c966bc54538e3d394f6b0c/main.js

[diff-9]: https://github.com/Z1MM32M4N/jquery-lab/commit/d2cb6d0a00b2ace36b604a82c5ca0271b6a6c0ad#diff-0
[step-9]: https://github.com/Z1MM32M4N/jquery-lab/blob/d2cb6d0a00b2ace36b604a82c5ca0271b6a6c0ad/main.js

[diff-10]: https://github.com/Z1MM32M4N/jquery-lab/commit/e8a0125f92dc232d645cd6137c53c8e0264148ec#diff-0
[step-10]: https://github.com/Z1MM32M4N/jquery-lab/blob/e8a0125f92dc232d645cd6137c53c8e0264148ec/main.js

[diff-11]: https://github.com/Z1MM32M4N/jquery-lab/commit/d3964bd408295cb7e4cae2a15f341baa8b348f05#diff-0
[step-11]: https://github.com/Z1MM32M4N/jquery-lab/blob/d3964bd408295cb7e4cae2a15f341baa8b348f05/main.js

[diff-12]: https://github.com/Z1MM32M4N/jquery-lab/commit/7eb4aeecd41aebe184d67eaf73bf84e9c4081cb5#diff-0
[step-12]: https://github.com/Z1MM32M4N/jquery-lab/blob/7eb4aeecd41aebe184d67eaf73bf84e9c4081cb5/main.js

[diff-13]: https://github.com/Z1MM32M4N/jquery-lab/commit/c9a180d97cabc20bd89be2d019338786997d86c4#diff-0
[step-13]: https://github.com/Z1MM32M4N/jquery-lab/blob/c9a180d97cabc20bd89be2d019338786997d86c4/main.js

[diff-14]: https://github.com/Z1MM32M4N/jquery-lab/commit/638042297ef875ff438730b79d97c48150275759#diff-0
[step-14]: https://github.com/Z1MM32M4N/jquery-lab/blob/638042297ef875ff438730b79d97c48150275759/main.js

[diff-15]: https://github.com/Z1MM32M4N/jquery-lab/commit/220c4416ce04f4a0caae1c527d7bf7b75df32ef4#diff-0
[step-15]: https://github.com/Z1MM32M4N/jquery-lab/blob/220c4416ce04f4a0caae1c527d7bf7b75df32ef4/main.js
