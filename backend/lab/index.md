---
layout: guide
title: Backend Lab
subject: backend
---

# Backend Lab

In this lab, you'll be introduced to Flask, a popular Python framework used to
create web applications.

## Overview

The goal of this lab is to create a web app that will allow us to make simple
blog posts. This post is a derivation of [Miguel Grinberg's Flask Mega-Tutorial][mega-tutorial],
modified specifically for ScottyLabs WDW. 

## Diving in

The code and tutorial for this lab will be [hosted on GitHub][source-final].
Make sure you go over the [basic concepts][slides] of the backend: we'll be using some 
terms here that you may not be familiar with, and it's a good idea to brush up on these
first. In addition, before these steps you should download [Python][python-dl] and [pip][pip-dl].

## Step 1: Installation and Setup

__[code after this step][step-1]__

The first step takes care of setup and running a basic 'Hello, World!' application. 
You can download this step's code [using this link][step-1].

We'll begin by creating the basic structure of our application using the terminal.
Create a new folder and let's just call it `wdwflask`:

```
$ mkdir wdwflask
$ cd wdwflask
```

We will now create a virtual environment using `venv`.  Run the command
```
python3 -m venv venv
```
This creates a virtual environment at `wdwflask/venv` using the module `venv`. This
might be a bit confusing. The most general form of this command is
```
python3 -m venv /path/to/new/virtual/environment
```
which will create a virtual environment at `/path/to/new/virtual/environment`
(note: don't actually run the above command).
To activate the virtual environment, run
```
$ . venv/bin/activate
```
Your terminal prompt should now look like
```
(venv) $
```

Now run the following:

```
$ pip install flask
$ pip install flask-sqlalchemy
$ pip install flask-migrate
$ pip install flask-wtf
```

SQLAlchemy is the Python SQL toolkit that gives us the full power of SQL without having to write SQL code. Flask-Migrate is an extension created by Miguel Grinberg that simplifies making updates to an existing database and migrating old data to the modified structure.
Flask-WTF is simply a library that allows us to create forms and manage its data easily.

Now we'll create our basic application structure, so run the following. You should be inside your `wdwflask` directory.

```
$ mkdir app
$ mkdir app/templates
$ mkdir app/static
```

The app folder will be where we put our application. The static sub-folder is where we will store static files like images, JavaScript, and CSS. The templates sub-folder is where our templates/HTML will go.

Now let's get to the actual application! Let's start by creating a initialization script. We can have this under `app/__init__.py`

```python
# app/__init__.py
from flask import Flask

app = Flask(__name__)
from app import views
```

The script above creates thes application object of class Flask and then imports the views module. Views are handlers that respond to requests from web browsers and other clients. These will be written as Python functions, and each view function is mapped to one or more request URLs. Let's write our first view function in `app/views.py`!

```python
# app/views.py
from app import app

@app.route('/')
@app.route('/index')
def index():
    return "Hello, World!"
```

This view is very simple, returning just the string "Hello, World!" to be displayed on the browser. The two route decorators
`@app.route('/')` and `@app.route('/index')` create the mappings for the URLs '/' and '/index' to this function.


The final step to running this application is to create a script that starts the web server. Let's call this `microblog.py` and put it in our root directory.

```python
# wdwflask/microblog.py
from app import app
```

All this does is import the app variable from our app package. We will need to
set a few environment variables before we're ready to run our app. Run the
commands
```
$ export FLASK_APP=microblog.py
$ export FLASK_ENV=development
```

Now if we run

```
$ flask run
```

we should have our running application. Play around with the route decorators! If you enter any other URL than '/' and '/index' you will get an error, since those are the only two that have been defined so far.


## Step 2: Jinja2 Templating with HTML

__[code after this step][step-2]__

We want the homepage of our application to show our blog posts. Flask supports returning HTML in our views, so all we have to do is output some HTML as a string right?

```python
# app/views.py
from app import app

@app.route('/')
@app.route('/index')
def index():
    post = "This is my first post!"
    return '''
        <html>
          <head>
            <title> WDW Flask Demo </title>
          </head>
          <body>
            <h1> ''' + post + ''' </h1>
          </body>
        </html>
        '''
```

Wow! That was easy.

Just kidding. Imagine if we had to do this for every page we ever wanted to create. We'd just be typing up blocks and blocks of HTML.
Complex pages with more complex JavaScript would be a huge pain, and including dynamic content would be very difficult. This is very obviously not going to work in the long run. This is where templates come in!

Templates are simply HTML files that support inheritance and dynamic content. Here's what that means. Let's create our
homepage in `app/templates/index.html`.

```html
<!-- app/templates/index.html -->
<html>
  <head>
    <title> WDW Flask Demo </title>
  </head>
  <body>
    <h1> {% raw %}{{ post }}{% endraw %} </h1>
  </body>
</html>
```

As you can see, we just wrote standard HTML. The only difference is that we now have <b> {% raw %}{{ ... }}{% endraw %} </b> sections, which are placeholders for dynamic content. This feature is built into Jinja2 templating that comes with Flask, which will substitute the blocks with the corresponding values provided as template arguments. We can update our `app/views.py` file to use this template.

```python
# app/views.py
from flask import render_template
from app import app

@app.route('/')
@app.route('/index')
def index():
    post = "This is my first post!"
    return render_template("index.html", post=post)
```


### Logic in HTML: Conditionals, Control Flow, and More!

Jinja2 also supports conditional statements, control flow, and many other scripting language features. We can add an if statement to our template.

```html
<!-- app/templates/index.html -->
{% raw %}<html>
  <head>
    <title> WDW Flask Demo </title>
  </head>
  <body>
    {% if post %}
      <h1> {{ post }} </h1>
    {% else %}
      <h1> Hello, World! </h1>
    {% endif %}
  </body>
</html>{% endraw %}
```

Play around with this to see how the conditional statement works! If we don't pass in a post to `render_template` in `app/views.py`, then we should show 'Hello, World!'. 

### Inheritance

Jinja2 also supports inheritance. Let's say in our application, we will have many pages. On every page, we will want to have a navbar at the top of the page with a few links. On a fully fledged application, maybe we want a link on our navbar to go to the homepage, to logout, to view our profile, etc. We could add this navigation bar to `index.html` but as our application grows and we have more and more pages, the HTML for this navbar would have to be copied into every single one of those files. 

Instead of doing this, we can use the inheritance feature of Jinja2. This allows us to move the parts of the page that are common into one base template from which all other files inherit from. Let's define a base template that includes a navigation bar in 
`app/templates/base.html`.



```html
{% raw %}<!-- app/templates/base.html-->
<html>
  <head>
    <title> WDW Flask Demo </title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
  </head>
  <body>
    <div class="container">
      <div class="navbar">
        <nav>
          <div class="nav-wrapper">
            <a href="/index" class="brand-logo"> WDW Blog </a>
          </div>
        </nav>
      </div>
    </div>
    {% block content %}{% endblock %}
  </body>
</html>{% endraw %}
```

Here, we use the <b>{% raw %}{% block content %}{% endblock %}{% endraw %}</b> to define the place where the sub-templates can insert themselves. This content can be replaced in sub-templates. To demonstrate this, let's modify `index.html` to inherit from `base.html`. 

```html
<!-- app/templates/index.html -->
{% raw %}{% extends "base.html" %}
{% block content %}
  {% if post %}
    <h1> {{ post }} </h1>
  {% else %}
    <h1> Hello, World! </h1>
  {% endif %}
{% endblock %}{% endraw %}
```

Since `base.html` now has our page title, we can remove that from `index.html`. All we leave here is the actual content. The extends block is how Jinja2 knows to include `index.html` inside `base.html`. The templates have matching block statements, so Jinja2 knows to combine them into one. Anytime we want to write a new page with a navbar, we would create them as extensions to `base.html`.


## Step 3: Web Forms 

__[code after this step][step-3]__

To handle our web forms we're going to us the Flask-WTF library. This extension requires some coniguration, so we'll create a basic 
`config.py` file.

```python
# wdwflask/config.py
WTF_CSRF_ENABLED = True
SECRET_KEY = "so-secret-lol"
```

This is pretty simple. The WTF_CSRF_ENABLED setting allows for cross-site request forger prevention (you can read more about this on your own) and the SECRET_KEY setting is a token used to validate a form. Make it something difficult to guess.

Now that we have our config file we need to tell Flask to use it. We can do this in our `__init__.py` file.

```python
# app/__init__.py
from flask import Flask

app =  Flask(__name__)
app.config.from_object("config")

from app import views
```

In Flask-WTF, web forms are simple classes, subclassed from the super class Form. All we have to do is define the fields of our form as class variables so all we have to do to represent the creation of a Post is create a simple Python class. Let's create a file for our forms in `app/forms.py`.

```python
# app/forms.py
from flask_wtf import FlaskForm
from wtforms import TextField
from wtforms.validators import DataRequired

class PostForm(FlaskForm):
    title = TextField("title", validators=[DataRequired()])
    post = TextField("post", validators=[DataRequired()])
```

All we need now is a template that contains the HTML to create the form. Flask-WTF knows how to render form fields as HTML, so
we can focus on the actual HTML. Here's what the template should look like (`app/templates/index.html`)

```html
<!--app/templates/index.html-->
{% raw %}{% extends "base.html" %}
{% block content %}
<div class="container">
  <div class="row">
    <form class="col s12" action="" method="post" name="post">
        {{ form.hidden_tag() }}
        <div class="row">
          <div class="input-field col s3">
            <label for="Post"> Make a post: </label>
              {{ form.title(size=30, maxlength=140) }}
              {{ form.post(size=30, maxlength=140) }}
          </div>
        </div>
        <div class="row">
          <div class="col s3">
            <button class="btn red lighten-2 waves-effect" type="submit" name="action"> Post! </button>
          </div>
        </div>
    </form>
  </div>
</div>
{% endblock %}{% endraw %}
```

So on our homepage, we want to be able to make posts. We still inherit from
`base.html` so we can have a navbar on this page. The only difference between a
regular HTML form and this one is that ours expects a Form object instantiated
from the Form class we just defined, passed in as a template argument named
`form`. The fields of our form (title, post) are rendered by <b>{% raw %}{{
form.field_name }}{% endraw %}</b>.

If you recall how passing in data works, all we have to do is put it in as an argument to `render_template()` in `views.py`. Here is what our new views should look like.

```python
# app/views.py
from flask import render_template
from app import app
from app.forms import PostForm

@app.route('/', methods=['GET', 'POST'])
@app.route('/index', methods=['GET', 'POST'])
def index():
    form = PostForm()
    return render_template("index.html", form=form)
```

The only new thing here is that in our route decorators, we have added a methods argument. This tells Flask that the view function accepts GET and POST requests. We want to be able to have POST requests, since these are the ones that will bring in the form data entered by the user.

Another way Flask-WTF makes our lives easy is the processing of submitted form data. Previously, we had a `DataRequired()` validator in our `PostForm` class, which just says that in order for the form to be valid, there must be something there. There are many different types of validators that you can read about. Let's update our views again.

```python
# app/views.py
from flask import render_template
from app import app
from app.forms import PostForm

@app.route('/', methods=['GET', 'POST'])
@app.route('/index', methods=['GET', 'POST'])
def index():
    form = PostForm()
    if (form.validate()):
        print ("Successful form!")
    return render_template("index.html", form=form)
```

When `form.validate()` is called, it will gather the data and run all the validators we have specified. If everything looks ok, it will return True, letting us know we can safely use this input data. We'll just print some message for now.


## Step 4: Databases/Storing Data

__[code after this step][step-4]__

Now ideally, when our form is validated, instead of just printing some string to console we want to create a post and put this into our database, since this is data we'd like to keep. We will use the Flask-SQLAlchemy extension to manage our database. This extension provides a wrapper for the SQLAlchemy project, which is an Object Relational Mapper or 'ORM'. An ORM allows database applications to work with objects instead of tables and SQL. This allows us to use Python to access and interact with our database rather than having to write SQL queries. 

In addition, we are also going to be using SQLAlchemy-migrate to keep track of database updates for us. After we've created a database, we'll have to update the database as the application growns. When we change how our data is represented in our database, rather than having to delete our database and create a new one everytime, we can run a migration. A database migration is the process of transferring data between different formats when we want to change things that are stored in in our database. 

For this demo, we'll be using the built in `SQLite` database. This is super easy and convenient as the database is stored in a single file and there's no need to start a database server. Let's modify our `config.py` file to tell our application to use a database.

```python
# wdwflask/config.py
import os
basedir = os.path.abspath(os.path.dirname(__file__))

WTF_CSRF_ENABLED = True
SECRET_KEY = 'so-secret-lol'

SQLALCHEMY_DATABASE_URI = 'sqlite:///' + os.path.join(basedir, 'app.db')
SQLALCHEMY_MIGRATE_REPO = os.path.join(basedir, 'db_repository')
SQLALCHEMY_TRACK_MODIFICATIONS = False
```

The `SQLALCHEMY_DATABASE_URI` is just the path of our database file. The `SQLALCHEMY_MIGRATE_REPO` is the location where we will store our SQLAlchemy-migrate data files. Setting the `SQLALCHEMY_TRACK_MODIFICATIONS` flag to `False` disables a feature we don't need, and improves the performance of our application.

When we start our application, we also need to tell it to use our database. Here's the new updated `__init__.py` file.

```python
# app/__init__.py
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

app = Flask(__name__)
app.config.from_object('config')
db = SQLAlchemy(app)
migrate = Migrate(app, db)

from app import views, models
```

Here, we've made two changes to our initilization script. We create a `db` object that is our database, and a migrate object that we'll use to make changes to our database structure. We will also import `models`,
which is just that data we will store in our database. We will create these as Python classes as well.

### Models

The ORM layer will translate objects created from our classes into rows in the proper database table. Create a `models.py` file.

```python
# app/models.py
from app import db

class Post(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    body = db.Column(db.String(140))
    title = db.Column(db.String(140))
    timestamp = db.Column(db.String(140))

    def __repr__(self):
        return 'Post <%r>' %(self.body)
```

The `id` field is common in all models, and is used as the primary key. This
means that each post in the database will be assigned a unique id value, stored
in this field. We then have fields for the `body` and `title` of our posts, and
even a `timestamp` for when the post was created. The `__repr__` method tells
Python how to print objects of this class, which is going to be useful for
debugging.

Now we need to create our database. We will do this using the Flask-Migrate
extension. Flask-Migrate exposes its commands through the `flask` command. You
have already seen `flask run`, which is a sub-command that is native to Flask.
The `flask-db` sub-command is added by Flask-Migrate to manage everything
related to database migrations. So let's create the migration repository by
running
```
$ flask db init
```
The `flask` command relies on the `FLASK_APP` environment variable to know where
the Flask application lives. For this application, you want to set
`FLASK_APP=microblog.py`, as we did in step 1.

After you run the above command, you should see a new `migrations` directory
with a few files and a `versions` sub-directory.

With the migration repository in place, it is time to create the first database
migration. Run
```
$ flask db migrate
```
This does not make any changes to the database, it just generates the migration
script. To apply the changes to the database, run the command
```
$ flask db upgrade
```
You have now created the database!

Going back to our views, when we create a post we want to store it in our database.

```python
# app/views.py
from flask import render_template, redirect, session, url_for, request
from app import app, db
from app.forms import PostForm
from app.models import Post
import datetime

@app.route('/', methods=['GET', 'POST'])
@app.route('/index', methods=['GET', 'POST'])
def index():
    form = PostForm(request.form)
    if form.validate():
        time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
        post = Post(body=form.post.data, title=form.title.data, timestamp=time)
        db.session.add(post)
        db.session.commit()
        return redirect(url_for('index'))
    posts = Post.query.all()
    return render_template("index.html",
                           posts=posts, form=form)
```

Here, all we're doing now is if the form is valid, we create a new post and add it into our database. I'll also allow Miguel to explain database sessions:

`Changes to a database are done in the context of a session. Multiple changes can be accumulated in a session and once all the changes have been registered you can issue a single db.session.commit(), which writes the changes atomically. If at any time while working on a session there is an error, a call to db.session.rollback() will revert the database to its state before the session was started. If neither commit nor rollback are issued then the system by default will roll back the session. Sessions guarantee that the database will never be left in an inconsistent state.`

Now if we go back to our `index.html` file and display these posts,

```html
<!-- app/templates/index.html -->
{% raw %}{% extends "base.html" %}
{% block content %}
<div class="container">
  <div class="row">
    <form class="col s12" action="" method="post" name="post">
        {{ form.hidden_tag() }}
        <div class="row">
          <div class="input-field col s3">
            <label for="Post"> Make a post: </label>
              {{ form.title(size=30, maxlength=140) }}
              {{ form.post(size=30, maxlength=140) }}
          </div>
        </div>
        <div class="row">
          <div class="col s3">
            <button class="btn red lighten-2 waves-effect" type="submit" name="action"> Post! </button>
          </div>
        </div>
        <div class="row">
          <div class="col s6">
            {% for post in posts[::-1] %}
            <p>
              <b> {{ post.title }} </b>
            </p>
            <p> {{ post.timestamp }} </p>
            <p> {{ post.body }} </p>
            {% endfor %}
          </div>
        </div>
    </form>
  </div>
</div>
{% endblock %}{% endraw %}
```

We loop through the posts reversed because we want our most recent post to be at the top. We're done! 


## Step 5: Further Steps

Hopefully after this tutorial, you understand the basics of creating a Flask application. There are many things we didn't go over,
such as user logins, user validation, and database relationships (users have posts, users follow other users, etc.) These things are more complicated, but hopefully this lab has given you the basic building blocks to get started on those types of tasks. [Miguel Grinberg's tutorial][mega-tutorial] goes over these things, and I highly suggest you go through that tutorial for further Flask development. 

Thanks!

- - -

[slides]: https://docs.google.com/presentation/d/1HcADdPMhP35u7tUUuXhPCQw-V49eDt_fYKH2Iek863o/edit?usp=sharing
[mega-tutorial]: https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world

[source-final]: https://github.com/crcmowry/wdwdemo
[step-1]: https://github.com/crcmowry/wdwdemo/tree/57c57270750bbdd8f23250951ba888b17bdc6d26
[step-2]: https://github.com/crcmowry/wdwdemo/tree/cc4351017d4b377be10e68164d160d6779da3fed
[step-3]: https://github.com/crcmowry/wdwdemo/tree/2daf5e29d41f0af26d8e116ebe31a5afe827e54f
[step-4]: https://github.com/crcmowry/wdwdemo/tree/78184f675e639aa611534db7f359813c148300f6

[python-dl]: https://www.python.org/downloads/
[pip-dl]: https://pip.pypa.io/en/stable/installing/
