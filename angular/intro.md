---
layout: guide
title: "Angular.js Introduction"
subject: angular
---

# Angular.js Introduction


AngularJS is a powerful framework from Google that extends the capabilities of
Javascript and HTML in order to create more dynamic and efficient websites.
MadeWithAngular showcases a few of the most popular websites that use this
framework. Why is it called Angular? Because it uses HTML angle brackets in
order to bind different types of data.

There is a lot of learning that needs to be done upfront about the structure of
Angular. There is some thought that needs to go in before you write your code.
It follows a MVC (Model View Controller) style setup due to the way it handles
data. This will not only make your code easier to understand, but more
efficient.

## Angular Overview

Angular requires that you have working knowledge of JavaScript and HTML, because
what Angular does is build off of these two languages. It gives you more tags,
or options for your HTML code and provides slightly different syntax for your
JavaScript code. This workshop is designed to give you a high level overview of
AngularJS while showing you how it is different from a JavaScript and HTML web
application. While, you won't learn all the intricacies of Angular, you will
have the basics to make or convert your own web apps into the Angular model.


## Javascript/HTML Versus Angular.js For Hello World

**Angular index.html**:

```html
<html>
  <head>
    <title>My Angular App!</title>
    <script src="angular.min.js"></script>
    <script src="app.js"></script>
  </head>
  <body ng-app="App" ng-controller="MainCtrl">
    <div>
      \{\{test\}\}
    </div>
  </body>
</html>
```

**Angular app.js**:

```javascript
angular.module('App', [])
.controller('MainCtrl', ['$scope', function($scope){
        $scope.test = 'Hello world!';
}]);
```

**index.html**:

```html
<html>
  <head>
    <title>My Web App!</title>
  </head>
  <body>
    <div id= "hello">

    </div>
  </body>
</html>
```

**hello.js**:

```javascript
document.getElementById("hello").innerHTML = "Hello World"
```

By looking at the code above, it may seem like a normal javascript web
application is preferred to an Angular app just based on lines of code and
complexity. However, the Angular structure will prove to be useful for more
complex web applications and it will help organize your code. Don't worry about
the specifics of the Angular version, because we will be going over the entire
structure and syntax.


## Angular Structure and Syntax

The typical structure of a complex Angular application is something like this:

```
app/
----- controllers/
---------- mainController.js
----- directives/
---------- mainDirective.js
---------- colorDirective.js
----- services/
---------- userService.js
----- js/
---------- bootstrap.js
---------- jquery.js
----- app.js
views/
----- mainView.html
----- index.html
```

### Directives

Use these in your html code in order to run the Javascript code. There are many
different types of directives, but they all start with `ng-`

You can make your own directives. Below are some ones that already exist.

| Name            | Description                                    |
| ----            | -----------                                    |
| `ng-controller` | Initializes a controller that needs to be used |
| `ng-app`        | Initializes the app                            |
| `ng-show`       | Can show or hide elements based on a condition |


### Modules

Every angular app needs a module, which is where all of the code for a specific
app will be written. Think of it as a main function that defines the
characteristics of your entire app.

To inject the module into the html code, use the directive

```js
ng-app = "appName"
```

It creates the Angular app by calling the javascript code that creates the
angular module.


### Expressions

These add dynamic values to JavaScript.

* Numerical Expression : `\{\{ 2 + 3 \}\}` evaluates to 5
* String Expression: `\{\{"Hello " + "World"\}\}` evaluates to `"Hello World"`
* Variable Expression: `\{\{text\}\}` prints out the value of text as defined in the
  angular app

### Controller

Defines the functions and values for the app behavior.

```
app.controller('ControllerName') , function(){ });
```

### Filters

* Format: taking some data and pipe that into a filter which modifies the data
* `\{\{2 | currency\}\}` outputs `$2.00`

### Services Helps you organize your code and share it.

Some built in services:

* `$location`, for the path of the current web page
* `$http`: request to server for information

You can create your own service:

* Format: `app.service("myService", function() {})`;
* `app.factory('serviceName', function serviceFunc(){});`

