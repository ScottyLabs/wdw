---
layout: guide
title: The Basics
subject: basics
---

# the basics

###### Read on as we demystify web development and prepare you for your first workshop.

## What is the Web?
There are many technologies that form the experience we call the Internet. The following is an overview of the most common ones.

__Web browser__ is the most apt term to describe what you first click on to get started online. A web browser is a program—such as Google Chrome, Mozilla Firefox, Apple Safari, or Internet Explorer—that retrieves the source code of a website and displays it in an interactive form.

__Web pages__ are the content you see when you navigate somewhere online. When you go to google.com and see the big "Google" logo or the doodle of the day, that image is a part of the web page.

__Web clients__ are programs that request information from another computer (see server). In most cases this is your web browser, however some servers can act as clients too.

A __web server__ is a special type of computer whose job is to tie all the clients together by performing computations, storing persistent information, authenticating users, and more.

__Web application__ is a more all encompassing term for all the code that goes into a particular web experience. This means the HTML and CSS code that makes up what you actually see, the JavaScript code that influences how you and the app interact, and any code that runs on a web server. Because this is a lot to talk about, we generally break it up into two parts, the __frontend__ and the __backend__.

Most web development is split up into frontend and backend development, so let’s dive a little deeper into these areas.

## The Frontend

###### Everything you can touch

The frontend of a web application is everything that ends up running in the browser. It is written in three main languages, __HTML__, __CSS__, and __Javascript__.

<span class="aside">To learn how to write HTML and CSS by creating a simple portfolio website, attend <a href="{{ site.baseurl }}/html/">Introduction to HTML & CSS</a></span>

HTML and CSS store information about a page. HTML contains the __content__, which could include text, images, videos, and any number of other things. Complementary to this, CSS stores information about how to __display__ the content stored by the HTML. This includes layout, color, fonts, and other information about how our site looks. With just HTML and CSS we can create beautiful, informational web pages that display the same information for everyone who loads them.

On the other hand, JavaScript is a fully featured programming language.

<span class="aside">To learn about JavaScript and its many quirks, attend <a href="{{ site.baseurl }}/frontend/">Introduction to Frontend Engineering</a></span>

When run in a web browser, JavaScript can alter HTML and CSS on the fly, communicate with a web server, or perform computation all by itself. This opens the door to modern, interactive, experiences.

## The Backend

###### Everything behind the curtain
The backend is all of the code that runs on the web server.

<span class="aside">To learn more and make a simple blog attend <a href="{{ site.baseurl }}/backend/">Introduction to Backend Web Development</a>.</span>

A backend is necessary if you want to store information long term, sign people in, or perform complex computations.

Most backends have a set of HTML, CSS, and JavaScript that is sent to the client on request, so that the client can interact with the backend. Different parts of the frontend are called using different routes or URLs, for example the route of this page is "/basics/" whereas the route of the homepage is just "/". Finally, there is generally a database, which is where lots of information can be stored long term and accessed quickly.

<div class="aside">In the workshop, we'll teach you Flask, a popular Python framework. Other common backend languages (and the sites that use them):
    <ul>
    <li>PHP (Facebook, Wordpress)</li>
    <li>Java (Twitter)</li>
    <li>C#/.NET(Microsoft, Stack Overflow)</li>
    <li>Ruby (Airbnb, Github)</li>
    <li>Python (Pinterest,  Instagram, Reddit)</li>
    </ul>
</div>

Backends can be written in any programming language, but some languages are easier to use than others. In addition, to the language, web developers often use a web framework, which is a collection of code that handles common server tasks and helps organize code.

## Design

###### Optimizing the user's experience
<span class="aside">To learn more about design, attend <a href="{{ site.baseurl }}/design/">Introduction to Design Thinking</a></span>

When creating a web application, it’s important to remember that in a good design can make or break your site’s success. Design is best described as all of the choices that go into making a website. Design is more than the way a website looks; a good design considers every aspect of a user’s experience. This includes how a user signs up, how information is laid out, and overall every action the user has to take inside your app. The goal of any good design is to be unobtrusive, intuitive, and pleasant.

We group the choices a designer makes about how a piece of software fits into a user’s life under the term __User Experience__, or UX. Another common term you will hear discussed in relation to UX is the UI, or __User Interface__. The user interface is what the user sees and actually interacts with. __Wireframes__, __mockups__ and __prototypes__ are examples of tools which facilitate the development of a good user experience.

Wireframes are like an outline to an essay. They’re non-functional, ugly, and generally use a visual style that will not end up in the app. They do help at visualizing a very rough an idea. Wireframing focuses on the broad ideas of an interface—the functionality and layout—rather than on the specific details.

Making mockups is like filling in your bulleted outline with the most important pieces of text. We say that they can be done with varying degrees of __Fidelity__. Low fidelity mockups serve roughly the same purpose as wireframes, while high fidelity mockups are pixel-perfect examples of what a developer should be implementing.

Prototypes are like rough drafts. With prototypes, users can actually interact with an interface, though it still may be rough and clunky. Prototypes are valuable because they can identify problems before developers take the time to implement a full design, which can save engineering resources.

## Deployment

###### The final flourish
<span class="aside">To learn how to deploy whatever you've created during web dev weeks, attend <a href="{{ site.baseurl }}/deployment/">Deployment</a></span>

After a website has been designed, and the frontend and backend implemented, it’s time for it to be __deployed__. Deployment is the process of taking the code a developer has written, and setting it up to run on a server where the whole world can interact with it. It is a very important step, but it can be complicated because software is often not developed in the same environment it is deployed in. Deploying and running a webapp is generally called __operations__, and it’s an important step in the life cycle of creating a web application.

## Attending More Workshops

###### Where to go from here
Thank you for reading this guide, and we hope that you will join us for Web Dev Weeks, being held at Carnegie Mellon from September 4th to 15th!

Web Dev Weeks goes into detail in all five areas we’ve discussed above through a series of five workshops. We’ve specifically designed the workshops so that they can be taken in any order, although we recommend taking the deployment workshop after you’ve completed at least one technical workshop (so you have something to deploy).

If you have any comments or questions about this guide, please write to webdevweeks@scottylabs.org.

## Registration
[Register here](https://docs.google.com/forms/d/1uuDuLjw7tiJVhwGSLuCla-rRwrCyIZorBuQsjKvvZXQ/viewform)
