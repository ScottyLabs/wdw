---
layout: guide
title: Deployment
subject: deployment
---

# deployment lab
In this session, you'll learn how to put whatever you've made in Web Dev Weeks on the web. We'll teach you how to host your project for free, and how to actually deploy them to the services.

## Overview
_Deployment_ is the process of making your app or site accessible to other people. With webapps/websites, we want a URL that we can point people to.

_Static_ websites/webapps are those that don't have a backend. They can be written entirely in HTML, CSS, and JavaScript, and don't have any code running on a server. We'll show you how to deploy these with a free service called GitHub Pages.

_Dynamic_ websites/webapps are those that have a backend. These often have a database, and will have a component written in Python, Java, Ruby, etc. that runs on a server. We'll show you how to deploy these using the free tier of a service called Heroku.

## Git
We're going to use [Git](http://git-scm.com/) to help us deploy our applications. Git is a distributed __version control__ system for code. This means that it lets you keep track of any changes to your code, merge your changes with other people's on collaborative projects, and download or upload code from a server. We're going to use Git to help us deploy our code to a server.

You can [download Git here](http://git-scm.com/download).

### Basic Commands
Git is a program that runs inside a terminal. This means that you'll have to run it in Terminal (on OS X or Linux) or Git Bash (on Windows). Make a folder somewhere on your computer and go to it in the terminal. We're going to show some very basic commands in Git, but if you're interested in using it to its full potential, check out the free book [_Pro Git_](http://git-scm.com/book).

#### Creating a Git repository
Enter

```python
$ git init
```

in your folder to _intialize_ your Git repository. This will make a folder called `.git` in your directory that will contain the history of your directory. Any code that you add or delete will be backed up in that folder.

#### Adding files to a Git repository
Copy the files you want to deploy into this directory. This should be the files you worked on either in the Frontend, Backend, or HTML & CSS. If you don't have anything from those sessions, or anything else you want to deploy, download [this code](https://github.com/jez/jquery-lab/archive/gh-pages.zip) if you want to learn to deploy a static site on GitHub Pages, or [this code](https://github.com/anbenson/webdevblog-example/archive/master.zip) if you want to learn to deploy a dynamic site on Heroku.

Now, enter

```python
$ git add -A
```

to add all the files in this directory to the repository. This means that Git will now _track_ any changes to these files.

After adding all these files, you'll want to enter

```python
$ git commit -m "Initial commit"
```

to _commit_ your files. This will store the current state of all these files to the repository (the `.git` folder). If you change the files in the future, Git will take note of that and keep the old versions of your files around.

The text in quotes after `-m` is the commit message. This lets anyone who is viewing the repository know what you did in this commit. Thus, it's important that it's informative enough that you or anyone else can tell what you changed (on a very high level) without reading your code.

If you now enter

```python
$ git log
```

you can see a log of all the changes that have been made to this repository. You should see one commit with the message "Initial commit."

#### Updating files in a Git repository
Whenever you change a file, you can run

```python
$ git add <filename>
```

where `<filename>` is the name of the file you changed. This will add the changes to the next commit you make. This way, the next time you run

```python
$ git commit -m "Some commit message"
```

this change will be saved as part of that commit in the repository.


#### Pushing and pulling code from remote servers
Git is pretty useful if you just use it locally to keep track of changes, but its real power is when you use it to download and upload (pull and push) code from servers. To configure your repository to work with a remote server, enter

```python
$ git remote add origin <remote_url>
```

where `<remote_url>` is the URL of the server. We'll talk about which URLs to actually use later in the lab.

Then, to push (upload) code to the server, enter

```python
$ git push
```

To pull (download) code from the server, enter

```python
$ git pull
```

At this point, the lab branches off. If you're deploying a static site (from the Frontend or HTML & CSS workshops), go [here](#github-pages-deployment). If you're deploying a dynamic site (from the Backend workshop), go [here](#heroku-deployment).

## GitHub Pages deployment
To deploy your static site, we're going to be using a site hosting service called [GitHub Pages](https://pages.github.com/). To begin, you're going to want to [make a GitHub account](https://pages.github.com/), if you don't already have one.

### Creating a GitHub repository
You want to start off by creating a Git repository on GitHub's servers. Go to [https://github.com/new](https://github.com/new), fill in a name and description, and click "Create repository."

### Linking your GitHub and local repositories
Run the following commands in your terminal:

```python
$ git remote add origin https://github.com/<username>/<reponame>.git
$ git checkout -b gh-pages
$ git push -u origin gh-pages
```

where `<username>` is your GitHub username, and `<reponame>` is the name of your GitHub repo. Make sure that the first command is __all one line__. On some screens, it wraps around, but it should all be one command. The first command links the remote repository with your local one. The second command creates a _branch_ of your code, which just tells GitHub that that's the code you want to deploy. Finally, the last command pushes the code up to the server.

If you wait a minute or so, your site should be up at `http://<username>.github.io/<reponame>/`.

Congratulations! You've just deployed a website.

## Heroku deployment
To deploy your dynamic site, we're going to be using a webapp hosting service called [Heroku](https://www.heroku.com/). To begin, you're going to want to [make a Heroku account](https://www.heroku.com/). Then, you'll want to download the [Heroku toolbelt](https://toolbelt.heroku.com/), which includes a set of tools for developing and deploying webapps. Finally, in the Terminal, run

```python
$ heroku login
```

to authenticate your local toolbelt with Heroku.

### Creating a Heroku app
While in the directory that contains your git repo, run

```python
$ heroku create <appname>
```

where <appname> is the optional name you want to give your webapp. If you don't specify an app name, then Heroku will generate one for you.

### Deploying a Heroku app
Now, deploy your code with

```python
$ git push heroku master
```

Then, to assign a server node to run your code, run

```python
$ heroku ps:scale web=1
```

Finally, you can open your app in the browser by running

```python
$ heroku open
```

Congratulations! You've just deployed a webapp.

### Setting up a database
However, if you've just deployed the webapp you made in the Backend workshop, you're not quite done. The webapp you wrote uses SQLite as a database. SQLite is a database that stores all of your data in a single file in your local filesystem. This is fine for local development, but when you deploy to Heroku, the servers that your code is running on doesn't have a persistent filesystem. This means your database is going to be wiped every once in a while.

For your database to perist, that is, for your data to stick around for as long as Heroku does, you'll want to switch to a database that runs as a server. Fortunately, Heroku will also host database servers for free. We're going to use a database called [PostgreSQL](http://www.postgresql.org/).

You can tell Heroku to set up a database for you by running

```python
$ heroku addons:add heroku-postgresql:dev
```

Next, you need to install a Python module for connecting to this database by running

```python
$ pip install psycopg2
```

while inside the `virtualenv`. You'll also need to include that in the list of requirements:

```python
$ pip freeze > requirements.txt
```

Finally, you'll want to change the line in your `main.py` that says

```python
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:////tmp/webdevblog.db"
```

to

```python
app.config["SQLALCHEMY_DATABASE_URI"] = os.environ["DATABASE_URL"]
```

in order to use Heroku's database. Note that `DATABASE_URL` is an environmental variable that Heroku will supply your application giving the location of the database.

Finally, you'll want to run

```python
$ git add .
$ git commit -m "Set up Postgres"
$ git push heroku master
```

to deploy your changes and switch your app over the using Heroku's PostgreSQL database.
