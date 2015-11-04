---
layout: guide
title: Deployment Lab
subject: deployment
---

# deployment lab
In this session, we'll take the sites you've been building this weekend and put
them on the web!  If you don't have a finished project, don't worry, we've got a
nice starter set of files.

## overview
_Deployment_ is the process of making your app or site accessible to other people. With webapps/websites, we want a URL that we can point people to.

_Static_ websites/webapps are those that don't have a backend. They can be written entirely in HTML, CSS, and JavaScript, and don't have any code running on a server. We'll show you how to deploy these with a free service called GitHub Pages.

_Dynamic_ websites/webapps are those that have a backend. These often have a database, and will have a component written in Python, Java, Ruby, etc. that runs on a server. These can also be deployed for free, and we have a lot of resources to point you in the right direction.

## getting the files
First thing's first, let's get our starter files.  You can get them as a
`.zip` [here][lab-dl].

## getting your files into git
First thing you're gonna want is a brand new git repository on GitHub.  While
there's lots of ways to go about this, the easiest if you don't know your way
around `git` is to go to GitHub and make a new repository
[here](https://github.com/new).  Make sure to check 'Initialize this repository
with a README'!

Next, clone this repository onto your machine.  With the desktop client, it
should pop up and you can just download it.  For the command-line client, select
the download URL on the new repository (it should be under `HTTPS clone URL` on
the right).  Mine looks something like

```console
https://github.com/bezi/food4cmu.git
```

Then, you'll want to clone it to your local machine with

```console
$ git clone <URL>
```

Now that you have a nice new repository on your machine, let's fill it with
code!  Unzip the handout files in the repository, and add them to your
repository.

For the terminal client, copy them into your directory repository and add them
with

```console
$ git add .
```

If you now run `git status`, it should look something like this

```console
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   favicon.ico
        new file:   index.html
        new file:   index.min.js
        new file:   main.css
```

Commit these changes with the `git commit` command. Make sure to add a useful
commit message!  Mine looks something like

```console
$ git commit -am "Added all the files knocked out during CarnegieHax 2015."
```

Get it onto GitHub with the command

```console
git push origin master
```

## setting up gh-pages
Congrats!  Your code is now on GitHub, but we need to do a bit more work to host
it.  In particular, you should put your code on `gh-pages`, so that GitHub knows
that you want to serve out your site.

First thing's first, we need to make a new branch.  Do so by running

```console
$ git checkout -b gh-pages
```
from your repository.  This makes a new `gh-pages` branch from your `master`
branch.  Then, push this new branch up to GitHub with the command

```console
$ git push origin gh-pages
```
This pushes your new `gh-pages` branch to GitHub.

Now, it's time to see your live site!  In your browser, go to
`<username>.github.io/<repo-name>`.  For example, in my case, we'll go to
[http://bezi.github.io/food4cmu/](http://bezi.github.io/food4cmu/).

## [optional] tidying up the repository
One optional step, if your repository is only going to be serving out a website,
is to go to the settings and select "Branches" from the side menu ([direct
link](https://github.com/bezi/food4cmu/settings/branches)).  In the dropdown
menu, update your `Default Branch` to `gh-pages`.

You can now delete your derelict `master` branch with

```console
$ git branch -d master
```

Delete the version on GitHub with

```console
$ git push origin --delete master
```

Now your repo just has a single branch.  How tidy!

Alright, it's time to put away `git` for now.  We're going to drop into the
exciting world of DNS!

## buying a domain name

If you want a nifty custom name for your site, you're going to have to look a
bit.  There's many, many different places to get domains from, but for this talk
we'll be using [NameCheap]().  They have fair prices and a solid user interface,
but they're not the only ones out there.

Typically a `.com` name will run somewhere ~10 dollars for a year.  There are
some free locations out there, your mileage may vary.  You can get a free one
from NameCheap by using the (GitHub Student Developer Pack)[gh-eduction].

## setting up the domain name
We'll now be setting up the domain as required by GitHub.  This is documented
[here](https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/).
In short, we want to add two `A` records to our domain that point to GitHub,
then we'll add a `CNAME` file to our repository so that `GitHub` knows where to
route requests for that particular domain.

First, we'll add the two `A` records to:

```console
192.30.252.153
192.30.252.154
```

Then, we'll add a file to our repository root called a `CNAME` file.  While we
could add it on our machine and push it up to GitHub, we can actually edit it
directly on GitHub!  In it, we put the domain that routes to our page.

If this has been set up properly, the domain should soon route to your new page!

## github tips
- You can actually make any repository you want serve out web pages!  If you
  have a cool code project that you want to have a website, just put stuff into
  its `gh-pages` branch.

- There's a special github repository for your user, which is the
  `<username>.github.io` page.  If you make a new repository with that name, the
  `master` branch will be the one serving out the content.

## non-static sites: your options

### PaaS: Platform-as-a-Service
- [Heroku](https://www.heroku.com/)
- Lots of platform-specific ones ([Nodejitsu](https://www.nodejitsu.com/), etc).

### IaaS: Infrastructure-as-a-Service
- You get a Linux machine. . . go nuts!
- [DigitalOcean](https://www.digitalocean.com/)
- [Amazon Web Services](https://aws.amazon.com/) (AWS)

### how do i choose?
- Easy answer: use Heroku.
  - Free
  - Bootstrap existing apps easily.
  - Fast!!
  - De facto solution for things like hackathon hacks.

- DigitalOcean:
  - Customizable, centralized, use the Linux box for anything.
  - Cheap, but not free. (You get credits with the [GitHub Student Developer
    Pack][gh-education])
  - Super educational in the long run!

[lab-dl]: https://scottylabs.org/wdw/deployment/lab/lab.zip "Lab Download Link"
[gh-education]: https://education.github.com/pack "Github Education Pack"
