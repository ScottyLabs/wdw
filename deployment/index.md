---
layout: guide
title: "Deployment: Making Your Site Public"
subject: deployment
---

# Deployment: Making Your Site Public

###### show off what you've made


In this session, you'll learn how to put whatever you've made at Web Dev Weekend
live on the web. Didn't manage to make it to any of the other sessions, but
you're still interested in learning how to make a site public? Don't worry:
we'll give you something to deploy.


### How to Attend

This workshop will be held on Sunday, November 8th at 1:30 p.m. in the Windows
Cluster in Wean.

If you haven't already, __[be sure to register]({{ site.registration_link }})__!
You certainly don't have to register to attend, but we like knowing how many
people to expect and what people will be interested in learning. We can't wait,
and we hope to see you there!

Be sure to bring a laptop. You'll want to make sure that either [GitHub for
Mac][gh-mac], [GitHub for Windows][gh-win], or [Git][git] & a terminal are
installed on your system.

[gh-mac]: https://mac.github.com/
[gh-win]: https://windows.github.com/
[git]: http://git-scm.com/downloads

# Static Sites: GitHub Pages
## Git Resources
- [Github Bootcamp](https://help.github.com/categories/54/articles) - an intro to Git and Github for beginners
- [Pro Git](http://git-scm.com/book) - the official, free book on Git

## Getting Onto GitHub
- Make an account.
- Make a repo.
- Get `git` onto your local machine.
  - Linux: `apt-get install git`
  - Windows/OSX: https://desktop.github.com/
- Push code up to GitHub.
- Set up `gh-pages`.
- Updating your code.
# DNS: How to Get Cool Names for Your Websites
## DNS Resources
- A very thorough and very readable guide from Digital Ocean.
- A short comic made by DNSimple explaining name resolution.
- A short guide on `A` vs `CNAME` by DNSimple.
## Getting a Name
- Free
  - `.tk` domains are free (their site is kinda sketchy).
- Non-free
  - Namecheap
    - Not the only solution
    - Fair price, solid interface to set things up.
## Setting Up a Host
- What kinds of records?  `A` vs `CNAME`.
  - `A`: name to IP
  - `CNAME`: name to name
- Guide to setting up records on Namecheap.
## Getting Github to Play Nice
- `CNAME` file
- Their “Getting Started” guide.
## Other Nice DNS Things
- Mail
- Subdomains
# Non-Static Sites: Your Options
# PaaS vs IaaS
## PaaS: Platform-as-a-Service
- Heroku
- Lots of platform-specific ones (Nodejitsu, etc).
## IaaS: Infrastructure-as-a-Service
- You get a Linux machine. . . go nuts!
- DigitalOcean
- Amazon Web Services (AWS)
## How do I choose?
- Easy answer: use Heroku.
  - Free
  - Bootstrap existing apps easily.
  - Fast!!
  - De facto solution for things like hackathon hacks.
- DigitalOcean:
  - Customizable, centralized, use the Linux box for anything.
  - Cheap, but not free. (Well, kinda.)
  - Super educational in the long run!
## Heroku
- Non-technical overview to Heroku’s purpose and goals.
- The Heroku Getting Started page.
## DigitalOcean
- Awesome blog on securing your shiny new Linux box.
- So. Many. Tutorials.
