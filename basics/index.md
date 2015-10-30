---
layout: guide
title: The Basics
subject: basics
---

# The Basics

###### read on as we demystify web development and prepare you for your first workshop

Many technologies make up the experience we call "The Web." The following is an overview of the most common ones.

__A web browser__ is a program—such as Google Chrome, Mozilla Firefox, Apple Safari, or Internet Explorer—that retrieves the source code of a website and renders it in a way that you can interact with.

A __client__ is a program that request information from another computer. For example, your web browser acts as a client when it requests a web page from a server.

A __server__ is a computer that responds to requests from a client. Servers are often responsible for storing information permanently: when you create an account on a website, that information is stored on the server.

__Web application__ is a more all encompassing term for all the code that goes into a particular web experience. This means the HTML and CSS code that makes up what you actually see, the JavaScript makes those pages interactive, and any code that runs on a web server. Because this is a lot to talk about, we generally break it up into two parts, the __frontend__ and the __backend__.

Most web development is split up into frontend and backend development, so let’s dive a little deeper into these areas.

## The Frontend

###### everything you can touch

The frontend of a web application is everything that ends up running in the browser. It is written in three main languages, __HTML__, __CSS__, and __Javascript__.

<span class="aside">To learn how to write HTML and CSS by creating a simple portfolio website, check out <a href="{{ site.baseurl }}/html/">Introduction to HTML & CSS</a>.</span>

HTML and CSS store information about a page. HTML contains the __content__, which could include text, images, videos, and any number of other things. Complementary to this, CSS stores information about how to __display__ the content stored by the HTML. This includes layout, color, fonts, and other information about how our site looks. With just HTML and CSS we can create beautiful, informational web pages that display the same information for everyone who loads them.

On the other hand, JavaScript is a fully featured programming language.

<span class="aside">To learn about JavaScript, its many quirks, and it's infinite possibilities, attend <a href="{{ site.baseurl }}/frontend/">Frontend Engineering with JavaScript</a>.</span>

When run in a web browser, JavaScript can alter HTML and CSS on the fly, communicate with a web server, or perform computation all by itself. This opens the door to modern, interactive, experiences.

## The Backend

###### everything behind the curtain

The backend is all of the code that runs on the web server.

<span class="aside">To learn more and make a simple blog, check out <a href="{{ site.baseurl }}/backend/">Introduction to Backend Web Development</a>.</span>

A backend is necessary if you want to store information long term, sign people in, or perform complex computations.

Most backends have a set of HTML, CSS, and JavaScript that is sent to the client on request, so that the client can interact with the backend. Different parts of the frontend are called using different routes or URLs, for example the route of this page is "/basics/" whereas the route of the homepage is just "/". Finally, there is generally a database, which is where lots of information can be stored long term and accessed quickly.

Backends can be written in any programming language, but some languages are easier to use than others. In addition, to the language, web developers often use a web framework, which is a collection of code that handles common server tasks and helps organize code.

## Design

###### optimizing the user's experience
<span class="aside">To learn more about design, attend <a href="{{ site.baseurl }}/design/">Crafting Well-Designed Sites</a></span>

When creating a web application, it’s important to remember that in a good design can make or break your site’s success. Design is best described as all of the choices that go into making a website. Design is more than the way a website looks; a good design considers every aspect of a user’s experience. This includes how a user signs up, how information is laid out, and overall every action the user has to take inside your app. The goal of any good design is to be unobtrusive, intuitive, and pleasant.

We group the choices a designer makes about how a piece of software fits into a user’s life under the term __User Experience__, or UX. Another common term you will hear discussed in relation to UX is the UI, or __User Interface__. The user interface is what the user sees and actually interacts with. __Wireframes__, __mockups__ and __prototypes__ are examples of tools which facilitate the development of a good user experience.

Wireframes are like an outline to an essay. They’re non-functional, ugly, and generally use a visual style that will not end up in the app. They do help at visualizing a very rough an idea. Wireframing focuses on the broad ideas of an interface—the functionality and layout—rather than on the specific details.

Making mockups is like filling in your bulleted outline with the most important pieces of text. We say that they can be done with varying degrees of __Fidelity__. Low fidelity mockups serve roughly the same purpose as wireframes, while high fidelity mockups are pixel-perfect examples of what a developer should be implementing.

Prototypes are like rough drafts. With prototypes, users can actually interact with an interface, though it still may be rough and clunky. Prototypes are valuable because they can identify problems before developers take the time to implement a full design, which can save engineering resources.

## Deployment

###### the final flourish

<span class="aside">To learn how to deploy whatever you created during Web Dev Weekend, attend <a href="{{ site.baseurl }}/deployment/">Deployment: Making Your Site Public</a></span>

After a website has been designed, and the frontend and backend implemented, it’s time for it to be __deployed__. Deployment is the process of taking the code a developer has written, and setting it up to run on a server where the whole world can interact with it. It is a very important step, but it can be complicated because software is often not developed in the same environment it is deployed in. Deploying and running a webapp is generally called __operations__, and it’s an important step in the life cycle of creating a web application.

## Attending More Workshops

###### where to go from here

Thank you for reading this guide, and we hope that you will join us for Web Dev Weekend, being held on November 7th and 8th!

We’ve specifically designed the workshops so that they can be taken in any order, although we recommend taking the deployment workshop after you’ve completed at least one technical workshop (so you have something to deploy).

If you haven't already, __be sure to register__ (registration link coming soon)! You certainly don't have to register to attend, but we like knowing how many people to expect and what people will be interested in learning. We can't wait, and we hope to see you there!

If you have any comments or questions about this guide, please write to info at scottylabs dot org.
