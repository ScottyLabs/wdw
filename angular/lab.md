---
layout: guide
title: "Angular.js Lab"
subject: angular
---

{% raw %}

# Interactive Lab: Angular Portfolio Website


We will be working to create a portfolio website that has separate tabs for
about, contact information, and portfolio. The power of Angular lies in the way
that it can quickly change between different states. As we go through each part,
you will be introduced to different parts of the Angular structure and syntax.


## Step 1: Downloading Starter Files

First step is getting the starter files to run on your computer. You can access
the starter files at this link. The starter code consists of three files, an
angular.js file, an index.html file, and an app.js file. There will also be a
bootstrap.css file, jquery, bootstrap.js file, and app.css file, but you do not
need to worry about those two, because the bulk of our work will be modifying
and writing code in the index.html and app.js file. All the necessary javascript
source files have been referenced in the index.html file.


## Step 2: Creating a Module

So our next step will be to create the actual angular application. To do this we
will need to create a module in our javascript file, app.js. A module is similar
to the code needed to create a canvas. We will be naming our application
"portfolioApp". In order to make sure that the index.html file actually runs the
javascript code, we have to use a directive, which is similar to an "id" in
html.


app.js

```javascript
var portfolio = angular.module('portfolioApp', [])
```


index.html

```html
<html>
  <head>
    <title>Portfolio</title>
    <script src="angular.min.js"></script>
    <script src="app.js"></script>
  </head>
  <body ng-app="portfolioApp">
    <div>
    </div>
  </body>
</html>
```

## Step 3: Setting up the Main Controller:

This will be the controller that holds all of the the information that we will
be incorporating into our page. We will be creating in our app.js file first.
That will follow the format, but change the `appName` to the name of our app and
the controller to `mainController`:


```
appName.controller('nameOfController', function(){ });
```

Next, we will be setting up the content, which is stored in JSON, which is a way
data is structured. This is as easy as setting a variable to the JSON data
inside the controller. First, before we work with the controller, we need to set
the variable pageContent equal to the contents of the JSON data as shown below.
The JSON data defines all the information that you will be storing in your
website. Put this below your controller in app.js


app.js

```javascript
var pageContent = {
    name: "Scotty Terrier",
    description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam sed arcu eget quam posuere dignissim. Aliquam vulputate lorem metus, ut semper eros viverra vitae. Quisque efficitur mattis tellus a vehicula. Mauris accumsan tortor felis, non porta metus cursus sit amet. Fusce vel turpis quis risus mollis consectetur. Suspendisse varius nulla laoreet libero condimentum, ut laoreet arcu commodo. Donec lobortis nunc turpis, ut posuere diam hendrerit sed. Ut id metus dolor. Morbi luctus mollis venenatis. Quisque viverra elementum est, ac laoreet dui tincidunt a. Maecenas iaculis nulla nec massa malesuada egestas. Praesent condimentum sollicitudin sapien id cursus. Donec in velit congue, interdum enim ac, varius nisi. Nunc consequat vel mi a placerat. Donec commodo libero ligula, lobortis euismod lacus fringilla et. Sed et vestibulum sem, eget sodales magna. Phasellus dignissim dui massa, nec dapibus est mattis ut. Donec et aliquam metus. Duis fermentum, orci nec vestibulum bibendum, magna tellus consectetur libero, vel sagittis massa sem vitae nisi. Cras porta augue bibendum congue tincidunt. Maecenas cursus porta condimentum.",
    images: [
              "images/agriculture.jpg",
              "images/goat.jpg",
              "images/mushroom.jpg"

            ],
    aboutImage: "scotty.jpg",
    address: "5000 Forbes Ave, Pittsburgh PA",
    phone: "4122682000",
    email: "sterrierdog@andrew.cmu.edu",

};
```

Now we can link this data in our controller to another variable. This step will
allow us to access this information in our html page, and create two-way data
binding, or in other words the view is constantly updated as changes are made to
the model. We will also need to define the usage of this controller in the body
tag of our html file, by using the `ng-controller` directive. We will be using
the alias main when we call the controller in other areas of the code.


index.html

```html
 <body ng-controller="mainController as main">
        <title>Scotty Terrier</title>
 </body>
```


app.js

```javascript
portfolio.controller('mainController', function(){
    this.content = pageContent;
});
```


## Step 4: Creating a Controller to set up Tabs

Now we are going to make a controller to set up tabs, such as the about page,
for the website. So first we will be using basic html to setup the buttons for
the tabs. This will include using some Twitter Bootstrap to set up a navigation
as well as just plain html. Since this class will be primarily about angular,
the code to actually make the necessary navigation bar will be provided below.
The code below creates the navigation bar using the Twitter ootstrap class and
by creating an html list with each element representing a different tab. We put
all of this information inside the section tag, which will go under your title
tag.


index.html

```html
<section>
    <h1></h1>
    <ul class="nav nav-pills">
        <li>
          <a href>About</a>
        </li>
         <li>
          <a href>Portfolio</a>
        </li>
         <li>
          <a href>Contact Me</a>
        </li>


    </ul>
</section>
```


Now we are going to make a controller that defines the necessary functions for
us to change to different pages. So this controller will go after the main
controller we made earlier. We will be naming it `tabController`. That will look
something like this:

app.js

```javascript
portfolio.controller('tabController', function(){
    this.content = pageContent;
});
```

Inside the controller we will be defining a variable, this.tab. It will define
which tab is selected at a given point. We will be initializing it to the value
1, because we want our first page (the about page), to be selected when the
website initially loads.

Then it will be time to write the  two functions: one that selects a tab and
another that checks if a particular tab is the selected tab. So the first
function will not return anything, but it will change the value of our variable,
this.tab based on a parameter. The second function will return true or false
depending on if this.tab is equivalent to the the parameter that is passed in.
This is because we will need to select and switch between the different tabs,
which we will assign numbers to. We will also be defining the controller in the
html file, in the `section` tag.


app.js

```javascript
portfolio.controller('tabController', function(){
   this.tab = 1;
   this.selectTab = function(setTab) {
       this.tab= setTab;
   }
   this.isSelected = function(checkTab){
       return this.tab === checkTab;
   }

});
```

index.html

```html
<section ng-controller="tabController as navigation">
    <h1></h1>
    <ul class="nav nav-pills">
        <li>
          <a href>About</a>
        </li>
         <li>
          <a href>Portfolio</a>
        </li>
         <li>
          <a href>Contact Me</a>
        </li>


    </ul>
</section>
```

## Step 5: Adding Tab Changing Functionality to  HTML

Now that we have gotten our controller in place, the next step is to to go back
to our index.html file and use some angular syntax to extend the capabilities of
our HTML file and add the tab functionality that we have defined in our
controller. So the first step will be to make use of the active class in
Angular. This will allow you to show which tab is selected currently. The active
class will be be used in the format defined below.

```
ng-class="{ active: controllerName.someFunction(parameter) }
```

We will define this class in each of the `<li>` elements in the html. We will be
using our controller to call the function `isSelected(checkTab)`, which will
take in the values that correspond with the table below.  Remember that the
`tabController` has the alias, `navigation`


| Page         | Number        |
| ------------ | ------------- |
| About        | 1             |
| Portfolio    | 2             |
| Contact Me   | 3             |


After you add the active class to check if the tab is selected, this is what
your code will look like


index.html

```html
<section ng-controller="tabController as navigation">
  <h1>{{main.content.name}}</h1>
  <ul class="nav nav-pills">
    <li ng-class="{ active: navigation.isSelected(1)}">
      <a href>About</a>
    </li>
    <li ng-class="{ active:navigation.isSelected(2) }">
      <a href >Portfolio</a>
    </li>
    <li ng-class="{ active:navigation.isSelected(3) }">
      <a href>Contact Me</a>
    </li>
  </ul>
</section>
```

While this code does define, which tab is selected, we still need to actually
changing between tabs. In order to do this we will be using the `ng-click`
directive to define what happens when each of the buttons for the different
pages are clicked. We will be using this in the `<a href>` tag  We want
something different to happen when the about page is clicked as opposed to when
the Contact Me is clicked. In order to do this we will be calling the
`selectTab` function we defined in our controller, in the `ng-click` directive.
For the parameter will will be passing in the number corresponding to the page
in the table above.


index.html

```html
<section ng-controller="tabController as navigation">
  <h1>{{main.content.name}}</h1>
  <ul class="nav nav-pills">
    <li ng-class="{ active: navigation.isSelected(1)}">
      <a href ng-click="navigation.selectTab(1)">About</a>
    </li>
    <li ng-class="{ active:navigation.isSelected(2) }">
      <a href ng-click="navigation.selectTab(2)">Portfolio</a>
    </li>
    <li ng-class="{ active:navigation.isSelected(3) }">
      <a href ng-click="navigation.selectTab(3)">Contact Me</a>
    </li>
  </ul>
</section>
```

In order to test the code you can add the expression `{{navigation.tab}}` to
under the `</ul>` tag to see the Angular magic. Made sure you delete this before
we get into our next step.


# Step 6: Displaying content on the website

Since we have already defined each of the tabs, we can now add the necessary
content for each page. In order to do this, we will be creating three div
elements. Since this part is more HTML, here is the basic structure we will be
using. It will go right after the `<\ul>` tag, which defines the end of our
navigation bar. Note that there are some classes already set up in the HTML code
below. These are some Twitter Bootstrap elements that just enhance the style of
the website.

```html
<div class="container">
  <p class="col-md-8"></p>
  <img class="col-md-4">
</div>
<div class="container">
  <li class="thumbnail" >
    <img/>
  </li>
</div>
<div class="container"> </div>
```

Before we do anything, we need to make sure that these divs will only show up if
the appropriate tab is selected. In order to do that, we need to add navigation
to the div class. This will allow us to use the `tabController` function,
`isSelected` so we only show tabs when they are selected. In order to show
elements only when a page is selected, we will use yet another directive.
`ng-show` will show an elements if the function `isSelected` results in true. In
code, this will look like:

index.html

```html
<div class="navigation container" ng-show="navigation.isSelected(1)">
  <p class="col-md-8"></p>
  <img class="col-md-4" >
</div>
<div class="navigation container"  ng-show="navigation.isSelected(2)">
  <li class="thumbnail">
    <img ng-src=/>
  </li>
</div>
<div class="navigation container" ng-show="navigation.isSelected(3)" >
</div>
```

That was a lot of information, so make sure you really understand the code. So
once again, we added the navigation class to each of our three divs. Then we
used `ng.show` and the function `isSelected` to determine if our specific page
is currently active.

Now let's actually add our content. We are going to start with the first div
container, which will contain the information for the about page. We will be
making use of the Angular expressions and we will call the variables that are
defined in our main controller.

These specific expressions will follow the format:

```js
{{controllerName.variable.jsonDefinedName}}
```

The JSON defined variable name refers to the elements that are before the colon
shown below:

```javascript
var pageContent = {
    name: "Scotty Terrier",
    description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam sed arcu eget quam posuere dignissim. Aliquam vulputate lorem metus, ut semper eros viverra vitae. Quisque efficitur mattis tellus a vehicula. Mauris accumsan tortor felis, non porta metus cursus sit amet. Fusce vel turpis quis risus mollis consectetur. Suspendisse varius nulla laoreet libero condimentum, ut laoreet arcu commodo. Donec lobortis nunc turpis, ut posuere diam hendrerit sed. Ut id metus dolor. Morbi luctus mollis venenatis. Quisque viverra elementum est, ac laoreet dui tincidunt a. Maecenas iaculis nulla nec massa malesuada egestas. Praesent condimentum sollicitudin sapien id cursus. Donec in velit congue, interdum enim ac, varius nisi. Nunc consequat vel mi a placerat. Donec commodo libero ligula, lobortis euismod lacus fringilla et. Sed et vestibulum sem, eget sodales magna. Phasellus dignissim dui massa, nec dapibus est mattis ut. Donec et aliquam metus. Duis fermentum, orci nec vestibulum bibendum, magna tellus consectetur libero, vel sagittis massa sem vitae nisi. Cras porta augue bibendum congue tincidunt. Maecenas cursus porta condimentum.",
    images: [
              "images/agriculture.jpg",
              "images/goat.jpg",
              "images/mushroom.jpg"
            ],
    aboutImage: "scotty.jpg",
    address: "5000 Forbes Ave, Pittsburgh PA",
    phone: "4122682000",
    email: "sterrierdog@andrew.cmu.edu",
};
```

For the about page, we will be using the description and image variables to put
data into the `<p>` and `<img>` tags respectively.We will be using `ng-src`
inside the `img` tag to define the image, but we will use the same format for
the expression defined above.

index.html

```html
<div class="navigation container" ng-show="navigation.isSelected(1)">
  <p class="col-md-8">{{main.content.description}}</p>
  <img class="col-md-4" ng-src="{{main.content.aboutImage}}">
</div>
<div class="navigation container"  ng-show="navigation.isSelected(2)">
  <li class="thumbnail" >
    <img/>
  </li>
</div>
<div class="navigation" ng-show="navigation.isSelected(3)" >
  <ul>
    <li>
      <span class="glyphicon glyphicon-map-marker"></span>
      <p></p>
    </li>
    <li>
      <span class="glyphicon glyphicon-earphone"></span>
      <p></p>
    </li>
    <li>
      <span class="glyphicon glyphicon-envelope"></span>
      <p></p>
    </li>
  </ul>
</div>
```

Now we are going to use the same process in order to populate the portfolio
page, with images. The only nuance is that we will be using the directive
`ng-repeat`, which works like a for loop and iterates through every element in a
list to display it. The `ng-repeat` has the following structure.

```
ng-repeat="image in controllerName.var.images"
```

Try applying it so we can display 3 different images.  Just follow the format
for expressions given above. When completed the divs should be structured like
so:

index.html

```html
<div class="navigation container" ng-show="navigation.isSelected(1)">
  <p class="col-md-8">{{main.content.description}}</p>
    <img class="col-md-4" ng-src="{{main.content.aboutImage}}">
</div>
<div class="navigation container"  ng-show="navigation.isSelected(2)">
  <li class="thumbnail" ng-repeat="image in main.content.images">
    <img ng-src="{{image}}"/>
  </li>
</div>
<div class="navigation container" ng-show="navigation.isSelected(3)" >
  <div id="contactBox">
    <ul>
      <li>
        <span class="glyphicon glyphicon-map-marker"></span>
        <p>{{main.content.address}}</p></li>
      <li>
        <span class="glyphicon glyphicon-earphone"></span>
        <p>{{main.content.phone}}</p>
      </li>
      <li>
        <span class="glyphicon glyphicon-envelope"></span>
        <p>{{main.content.email}}</p>
      </li>
    </ul>
  </div>
</div>
```

# Step 7: Getting User Input for Comments Page:

In less than a hundred lines of code, you have a working AngularJS Application.
But we can take this a step further, by letting the user give feedback on the
Contact Me pages. Here is where we will start using the model, because the data
is generated in realtime from the user. We will be storing the information from
the user in a JSON style format. The contact page will include three different
inputs: name, email, and message.

Your form can be generated by this code. It will be placed inside the `div`
class for the the third and final tab.

index.html

```html
<form class="col-md-8">
  <div class="form-group">
    <label for="name">Name:</label>
    <input type="name" class="form-control" id="name">
  </div>
  <div class="form-group">
    <label for="email">Email address:</label>
    <input type="email" class="form-control" id="email">
  </div>
  <div class="form-group">
    <label for="msg">Message:</label>
    <textarea rows="4" cols="50" type="msg" class="form-control" id="msg"></textarea>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

This is where we get into the more complex angular topics like `$scope` and
`ng-model`. We will be creating another controller in order to store the contact
messages into a list. This controller will be named `userController`. In that
controller we will be defining a variable `userMessageList`, which is initially
an empty list. Then we will make a function that is set to the variable
`$scope.update`. The parameter for this function will be user, which stores in
the user input. Then we will be appending the list with a copy of the user using
`angular.copy`

app.js

```javascript
portfolio.controller('userController', ['$scope', function($scope) {
  $scope.userMessageList = [];


  $scope.update = function(user) {
    $scope.userMessageList.push(angular.copy(user));
    console.log($scope.userMessageList);
  };
}]);
```

Now in our HTML file, we have to call our controller using the directive
ng-controller. Next for every input, we need to add we need to add ng-model.
This will link ng-model to a particular input and bind it to the backend. We
will be using the following format for our particular ng-model.

```html
ng-model="variableName.inputType"
```

Now we will be using ng-click to call the function update(user) from the
controller.

index.html

```html
<form ng-controller="userController" class="col-md-8">
  <div class="form-group">
    <label for="name">Name:</label>
    <input type="name" class="form-control" ng-model="user.name">
  </div>
  <div class="form-group">
    <label for="email">Email address:</label>
    <input type="email" class="form-control" ng-model="user.email">
  </div>
  <div class="form-group">
    <label for="msg">Message:</label>
    <textarea rows="4" cols="50" type="msg" class="form-control" ng-model="user.msg"></textarea>
  </div>
  <button type="submit" class="btn btn-primary" ng-click="update(user)">Submit</button>
</form>
```

So all of our user data will be stored in a list. The backend challenge for you
will be to now find a way to meaningfully access the data. You could store it in
a database or a server. This is more of a backend issue and is beyond the scope
of this particular course. But we have covered most of the front-end work that
needs to happen to create your very own website.

{% endraw %}
