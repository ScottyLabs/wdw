---
layout: guide
title: JavaScript Lab
subject: javascript
---

# JavaScript Lab
The purpose of this lab to practice using JavaScript to create an interactive webpage and introduce new features of the language.
## Overview
In this lab, we will be creating a website for playing the game "Falling Boulders." The goal of this game is to move your player across the bottom of the screen using the left and right arrow keys to avoid constantly falling boulders. Every boulder that is successfully dodged earns the player a point. The game ends when the player collides with one of the boulders. You can play a finished demo of the game __[here][game-demo]__.
## Step 1: Initial Code

__[download starter code][starter-code]__, __[diff for this step][diff-1]__, __[code for this step][step-1]__

To start off, you are going to need to download the starter code, which you can download __[here][starter-code]__. This includes an html file (`index.html`) with the layout of the page already set up and a JavaScript file (`framework.js`) with some pre-written code that takes care of some behind-the-scenes work we don't want to have to worry about while coding the game itself.

Once you have that downloaded, go ahead and create a new file called `main.js` and add a reference to it with the `<script>` tag at the bottom of `index.html`. If you don't know how to do this, look at the tag loading `framework.js` for reference.

All of the code we write from now on will be inside `main.js`
## Step 2: Initializing Global Variables

__[diff for this step][diff-2]__, __[code for this step][step-2]__

Before we begin coding the game itself, we are going to want to initialize some variables that we will use throughout the project. At the top of `main.js`, create three variables `scoreBoard`, `startButton`, and `canvas` for storing the scoreboard, start button, and canvas respectively and use `document.getElementById()` to create references to each of their respective HTML elements in `index.html`.

Next, create a variable for storing the context of the canvas. This will look something like this:
```JavaScript
var ctx = canvas.getContext('2d');
```
What this line does is give us a way to interact with our canvas. We pass the argument `'2d'` to let JavaScript know that we want to draw 2-D images onto the canvas.

Now that we have these variables, let's use them to code our game.
## Step 3: Begin Creating the Player

__[diff for this step][diff-3]__, __[code for this step][step-3]__

The first part we want to create is our player object. On the next line, create a new object representing our player and store it in a variable called `player`. For now, we will give our player object three properties: `hitbox`, `color`, and `draw`.

First, let's assign a new `Rectangle` object to `hitbox`. The constructor for `Rectangle` is already defined in `framework.js` and is used as follows:
```JavaScript
var rect = new Rectangle(x, y, width, height);
```
This rectangle is going to represent the bounds of our player for detecting collisions and for drawing the player on the canvas.

Assign values for `x` and `y` so that the player will appear on the bottom of the canvas and give it a `width` and `height` of your choosing (in my example, I used a width of 30 and a height of 60). Keep in mind that for canvases the top left corner is the origin (0, 0). Also, you may find it useful to use `canvas.width` and `canvas.height` in your calculations.

> ### A Note about the Canvas
> Throughout the lab, it will be helpful to think about the canvas as being a grid of 10x10 cells. For example, this is why I gave my example player a width of 30 and height of 60. This corresponds nicely to a 3x6 block of cells. Keep this in mind when creating other elements later.

Next, let's give our player a color. Assign a `String` to the `color` property of your player object to represent whatever color you want. This can be a color name, such as `"red"` (if it's supported by HTML), or a hex code, such as `#FF0000`.

Finally, for `draw` we are going to write a function that will draw the player onto the canvas. For now, this will be pretty basic and just draw the hitbox in the color you chose previously. To do this, call the `draw()` method on the hitbox, which looks like:
```JavaScript
rect.draw(ctx, color);
```
where `ctx` is the context of the canvas we wish to draw on (which we created in Step 2) and `color` is a string representing the color of the rectangle. Fill in these values as well as the value of `rect` yourself. (Hint: use the `this` keyword)
## Step 4: Rendering the Player

__[diff for this step][diff-4]__, __[code for this step][step-4]__

Now that we have a player with a `draw` function, let's display the player on the canvas. To do this, we are going to assign a new function to `document.body.onload` like this:
```JavaScript
document.body.onload = function()
{
    player.draw();
};
```
So, what does this do? Well, `document.body` refers to the `<body>` of our HTML page and `onload` is property that stores a function to be called as soon as the webpage loads. `document.body.onload` is `null` by default, so by setting it to our newly created function we are telling the page that we want this new block of code to be run once the page finishes loading. This will sort of act similarly to a main method in Java or C.

Now, we can begin seeing the fruits of labor! Open up a web browser and click `File > Open File` (`ctrl/cmd + O`), navigate to wherever you saved this project, and select `index.html`. If your code is all correct, you should see a colored rectangle on a blank gameboard. (If you don't see this, check the JavaScript console for errors).

From here on out, we will be able to test our code simply by going to the browser and refreshing the page.
## Step 5: Drawing a Prettier Player (Optional)

__[diff for this step][diff-5]__, __[code for this step][step-5]__

At this point we have a pretty basic player displaying on the gameboard. But what if our player aspires to be more than just a rectangle? Well, we can fix that!

Back in the `player` object, add a new property called `body`. `body` is going to be an array of rectangle objects that represent different pieces of our player's body. This can look like however you want, just keep in mind it should fit the bounds of `hitbox`. Also, consider the top left corner of `hitbox` to be the coordinate (0,0) when assigning `x` and `y` values to your rectangles. The reason for this will be apparent in the next part of this step.

Since we've changed what our player looks like, we're going to want to rewrite the `draw` function. Instead of calling `Rectangle.draw()` on just `hitbox`, loop through the rectangles in `body` and call `Rectangle.draw()` on each one of them. However, this time we are going to add an argument as follows:
```JavaScript
rect.draw(ctx, color, offset)
```
`offset` is an optional parameter that offsets the rectangle by the `x` and `y` values of the rectangle passed in (this is why we treated the top left corner of `hitbox` as (0,0) when making `body`). Fill in `rect`, `ctx`, and `color` as you did previously, but for `offset` fill in the value `this.hitbox`.
## Step 6: Moving the Player

__[diff for this step][diff-6]__, __[code for this step][step-6]__

So now we have a player displaying, but what good is a player if it can't move? Our next step will be to add `moveLeft()` and `moveRight()` functions to move the player across the bottom of the gameboard.

Before we write these functions, we are going to first define a function `erase()` inside `player`. The reason for this is that we want to be able to update the player's location on the canvas after we move it and the only way we can do this is by erasing the player from its previous location then redrawing it in the new one. Similarly to `draw()`, we already have a function defined in `framework.js` for erasing that can called like:
```JavaScript
clearRect(ctx, rect);
```
Again, call `clearRect()` in your `erase()` function replacing `ctx` and `rect` with the correct values and you are done.

Now, let's write `moveLeft()` and `moveRight()` (still inside `player`). I'll leave the implementation to you, but each function should fulfill the following tasks:
1. Erase the player from the canvas
2. Move the player's location (hint: edit some property in `hitbox`)
3. Make sure the player cannot leave the bounds of the screen
4. Redraw the player onto the canvas

When choosing the amount to shift the player by, keep in mind the hypothetical grid of 10x10 cells discussed in Step 3.
## Step 7: Listening for Key Presses

__[diff for this step][diff-7]__, __[code for this step][step-7]__

Remember when we assigned a function to `document.body.onload` to run some code when the page loaded? Well, we can edit a similar property to have code whenever a key is pressed on the keyboard. Inside the function we assigned to `document.body.onload`, add the following snippet:
```JavaScript
document.body.onkeydown = function(e)
{
    var keyCode = e.which || e.keyCode;
    // to be implemented
};
```
Notice that for this function we have defined a parameter `e`. This refers to the event data that will be passed by the browser when it calls the function, which is how we determine which key was pressed.

This determination is performed in the line `var keyCode = e.which || e.keyCode;`. Similarly to how characters have an ASCII value, every key on the keyboard has its own key code that can be used to identify it. This value is stored in either `e.which` or `e.keyCode` depending on which browser you are using. That's why we include `e.which || e.keyCode`. What this does is check if `e.which` is defined: if it is, then its value is returned, if not, then `e.keyCode` is returned.

Now that we have the key code, we can check if the left or right arrow keys have been pressed. If the left arrow key is pressed, the player should move left; otherwise, if the right arrow key is pressed, the player should move right. Implement this yourself. (Note: left arrow has a key code of 37, right arrow is 39)
## Step 8: Constructing Boulders

__[diff for this step][diff-8]__, __[code for this step][step-8]__

At this point, you should have all the skills necessary to write a constructor for `Boulder` objects yourself. Like `player`, it should have `x`, `y`, `color`, `hitbox`, `draw`, and `erase` properties. `color` should be passed as a parameter into the constructor so that we can easily change it (or even have differently colored boulders!). The `x` coordinate should be given a random position on the canvas such that it is fully visible (hint: use `Math.random()`) and the `y` coordinate should be `0`. Since our boulders are just squares, just having `hitbox` will suffice to represent both the bounds and the shape we want displayed. `draw` and `erase` should look pretty similar to those of `player`.

Keeping with the idea of 10x10 cells, I recommend making the boulders 10x10 and making their `x` values multiples of 10.
## Step 9: Falling Boulders Part 1

__[diff for this step][diff-9]__, __[code for this step][step-9]__

Now that we have our `Boulder` constructor, let's start making boulders. First, we need some variables to store our boulders. Under the global variables we created at the top of the file, add two more variables: `boulderCount`, which is how many boulders we want in existence at one time, and `boulders`, which should be initialized as a empty array. Give `boulderCount` any value you want; I chose 15 in my example.

The rest of this step is going to be creating a new function called `start`. The purpose of `start` is to create new boulders after a time interval until we reach the size of `boulderCount`.

Inside `start`, initialize a new variable to 0 to represent a counter. Next, we are going to use JavaScript's `setInterval()` function to create new boulders every second or so. Add the following code underneath your counter:
```JavaScript
var boulderInterval = setInterval(function() {
  // to be implemented
}, 900);
```
This will run the code inside the anonymously defined function every `900` milliseconds forever or until we terminate the interval. To terminate it, call the function `clearInterval(boulderInterval)`. Inside the new function for our interval, check if the counter is equal to `boulderCount` and terminate the interval if it is. Otherwise, add a new boulder to `boulders` with a color of your choosing and increment the counter. Note that right now we are only creating boulders, not drawing them. Drawing will come in the next step.

Finally, we want `start` to run when the user presses the start button on the webpage. Back inside the function we assigned to `document.body.onload`, add the following line:
```JavaScript
startButton.onclick = start;
```
This tells the website that whenever someone clicks the start button, we want our `start` function to be called. However, we really only want `start` to be called the first time the start button gets clicked. So, at the top of `start`, add a similar line:
```JavaScript
startButton.onclick = null;
```
This will stop `start` from being called again when the start button gets clicked.
## Step 10: Falling Boulders Part 2

__[diff for this step][diff-10]__, __[code for this step][step-10]__

In Step 9 we created several boulders, but we haven't made them fall yet. Let's write a new function called `fall` to do just that. Here's what `fall` should do: for each boulder in the array `boulders`,
1. Erase the boulder from the canvas
2. Update its `y` value (again, I recommend adding 10)
3. If a boulder reaches the bottom, replace it with a new a boulder starting at the top
4. Redraw the boulder

Once you finish that, we need to call `fall`. At the top of the file, add another global variable called `fallInterval` and set it to `null`. Next, add the following line to the end of `start`:
```JavaScript
fallInterval = setInterval(fall, 40);
```
This makes it so `fall` gets called every 40 milliseconds. We store the interval in `fallInterval` so that we can clear it later.
## Step 11: Keeping Score

__[diff for this step][diff-11]__, __[code for this step][step-11]__

Our game is almost complete! All we have left is to keep track of score and determine when the game is over.

Create another global variable called `score` and initialize it to 0. Next, write a new function called `updateScore`. This function is pretty simple: all it does is increment `score` by 1 and display the new score on the screen. To display the new score, edit the `innerHTML` property of `scoreBoard` as follows:
```JavaScript
scoreBoard.innerHTML = "Score: " + score;
```

Next, write a new function called `checkHit`. This will be how we determine when to the player has lost. In the function, for each boulder in `boulders`, check if its hitbox intersects the player's hitbox with the `intersects()` function from our rectangle framework which looks like:
```JavaScript
rect.intersects(rect2)
```
and returns true if the `rect` and `rect2` are intersecting. If the player has been hit, clear `fallInterval` and let the player know that the game is over using JavaScript's built-in `alert()` function. Pass a String with a message telling the player that they lost and letting them know their final score into `alert` (e.g. `alert("Game Over")`) and the page will display a popup with your message. Finally, we want to refresh the page so that the player can play again. To do this, all we need is the line
```JavaScript
document.location.reload();
```

Now that we have `updateScore` and `checkHit`, let's put them inside `fall`. At the top of `fall` call `checkHit` and inside your check for if a boulder reached the bottom call `updateScore` if it in fact hit the bottom.

Congratulations, you've finished your first game in JavaScript!

- - -

Written by Ari Cohn, October 2017

[game-demo]: https://wafflecohn.github.io/javascript-lab/

[starter-code]: https://wafflecohn.github.io/javascript-lab/starter-code.zip

[diff-1]: https://github.com/WaffleCohn/javascript-lab/commit/427829f46feb493cd3b11839c58c8c53c3ea250c
[step-1]: https://github.com/WaffleCohn/javascript-lab/blob/427829f46feb493cd3b11839c58c8c53c3ea250c/index.html

[diff-2]: https://github.com/WaffleCohn/javascript-lab/commit/adb00d3b766bfd808b547ed29997717172242c5b
[step-2]: https://github.com/WaffleCohn/javascript-lab/blob/adb00d3b766bfd808b547ed29997717172242c5b/main.js

[diff-3]: https://github.com/WaffleCohn/javascript-lab/commit/2d8c80d902cfcbf46de8198a048201e0367cf723
[step-3]: https://github.com/WaffleCohn/javascript-lab/blob/2d8c80d902cfcbf46de8198a048201e0367cf723/main.js

[diff-4]: https://github.com/WaffleCohn/javascript-lab/commit/4c4665f47fefc38878965bc79313a5a9cf7e49fc
[step-4]: https://github.com/WaffleCohn/javascript-lab/blob/4c4665f47fefc38878965bc79313a5a9cf7e49fc/main.js

[diff-5]: https://github.com/WaffleCohn/javascript-lab/commit/44df2b7cb2806eea61beaeb7645556e2bd86016d
[step-5]: https://github.com/WaffleCohn/javascript-lab/blob/44df2b7cb2806eea61beaeb7645556e2bd86016d/main.js

[diff-6]: https://github.com/WaffleCohn/javascript-lab/commit/95cba599ff2c65a4aa0f733a6b95e95da8111906
[step-6]: https://github.com/WaffleCohn/javascript-lab/blob/95cba599ff2c65a4aa0f733a6b95e95da8111906/main.js

[diff-7]: https://github.com/WaffleCohn/javascript-lab/commit/4b6c9121c4f26b66fc7804a3f030e7a62aad8b80
[step-7]: https://github.com/WaffleCohn/javascript-lab/blob/4b6c9121c4f26b66fc7804a3f030e7a62aad8b80/main.js

[diff-8]: https://github.com/WaffleCohn/javascript-lab/commit/6c378f5af6b6e8f8149aa0ee97b4ee8ed2d38398
[step-8]: https://github.com/WaffleCohn/javascript-lab/blob/6c378f5af6b6e8f8149aa0ee97b4ee8ed2d38398/main.js

[diff-9]: https://github.com/WaffleCohn/javascript-lab/commit/ec020639551b57342964da71eec31a7e3ef88ee9
[step-9]: https://github.com/WaffleCohn/javascript-lab/blob/ec020639551b57342964da71eec31a7e3ef88ee9/main.js

[diff-10]: https://github.com/WaffleCohn/javascript-lab/commit/f5c7c8511289ce74e9e2fd8f04df7404009720f1
[step-10]: https://github.com/WaffleCohn/javascript-lab/blob/f5c7c8511289ce74e9e2fd8f04df7404009720f1/main.js

[diff-11]: https://github.com/WaffleCohn/javascript-lab/commit/df8042c3818087c0cf77eb79ef470120b9b55aa1
[step-11]: https://github.com/WaffleCohn/javascript-lab/blob/df8042c3818087c0cf77eb79ef470120b9b55aa1/main.js
