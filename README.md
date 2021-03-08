# Flask-step-by-step  with  [@achrefabdeljalil](https://www.linkedin.com/in/achref-abdeljalil-179aa5136)



## Get Started ✅✅

1. Install [Python](https://www.python.org/downloads/)        
2. Install [Xamp](https://www.apachefriends.org/fr/download.html)
3. Install [PyCharm](https://www.jetbrains.com/fr-fr/pycharm/)
4. Create a new Flask project with Pycharm                  


## Let's Jump In ✅✅ 

Befor all actions we can add this [Chrome Extention](https://chrome.google.com/webstore/detail/codecopy/fkbfebkcoelajmhanocgppanfoojcdmg) to facilitate our work

1. Lets test our functions in **app.py** by running project 
2. To avoid running project in every single change we can activate the **debug mode**
    - By adding this part of code in **app.py**
    ```python
    if __name__ == '__main__':
    app.run(host="localhost", port=8000, debug=True)
    ```
3. And Now Let's test our template
    - By Importing the package **render_template** in **app.py**
    ```python
    from flask import Flask, render_template
    ```
    - And Adding the **web service** with the **route**
    ```python
    # Home route
    @app.route('/')
    def index():
        return render_template("home.html")
    ```
    - Now Let's create the template correspondent to the **our service**
        - In the folder **template** let's create the **home.html** file
        - In **home.html** we can put this code as exemple 
        ```jinja2
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8" />
                <meta http-equiv="X-UA-Compatible" content="IE=edge" />
                <meta name="viewport" content="width=device-width, initial-scale=1.0" />
                <title>Document</title>
            </head>
            <body>
                <h1>hello world</h1>
            </body>
            </html>
        ```
4. To make our work more easy let's import all our package  and database configuration from beginning 
```python
from flask import Flask, render_template, flash, redirect, url_for, session, request, logging
from flask_mysqldb import MySQL

from wtforms import Form, StringField, TextAreaField, PasswordField, validators
from passlib.hash import sha256_crypt
from functools import wraps

app = Flask(__name__)

# Config MySQL
app.config['MYSQL_HOST'] = 'localhost'
app.config['MYSQL_USER'] = 'root'
app.config['MYSQL_PASSWORD'] = ''
app.config['MYSQL_DB'] = 'myaticlesapp'
app.config['MYSQL_CURSORCLASS'] = 'DictCursor'

# init MYSQL
mysql = MySQL(app)
```
5. The editor will underline the missed package so let's import them 
```cmd
pip install passlib
pip install flask_mysqldb 
pip install wtforms
pip install functools
```

6. We can also create our database to work with , in our project 
    <a href="https://drive.google.com/file/d/149G19WyYvmzWpJnK-wlM07xY5Hu6oVjr/view?usp=sharing" target="_blank">Database file</a>

## Block Notion

1. To make our project more professional we can work with the **Block** notion  
    so let's create a file **layout.html** : this file will be the basic of our template 
    and we can put this **code** as exemple 
```jinja2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %} My Todos {% endblock %}</title>
</head>
<body>
{% block body %} {% endblock %}
</body>
</html>
```
and update the **code** of **home.html** to 
```jinja2
{% extends 'layout.html' %}
{% block title %}
  Home
{% endblock %}
{% block body %}
    <h1>hello from <em> home page</em></h1>
{% endblock %}
```
<br>
<br>      

## Integrate bootstrap 4

The next step is to integrate [Bootstrap 4 ](https://getbootstrap.com/docs/4.6/getting-started/introduction/) with our project to make our template more **pretty** <br>
But what is **bootstrap** ?? 🙄🙄
The easiest way to integrate **Bootstrap 4** : is to add **CDN links** to our base **layout.html** <br>
In the `<head>` tag we put the link of **CSS requirement** 👇

```jinja2
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css"
          integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">
```
and in before the end tag of `<body>` we put the links of **JS requirement**
```jinja2
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"
        integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
        crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-Piv4xVNRyMGpqkS2by6br4gNJ7DXjqk09RmUpJ8jgGtD7zP9yug3goQfGII0yAns"
        crossorigin="anonymous"></script>
```
<br>


## Template Includes

Let's create a folder with **includes** as name in the **Templates** folder : `templates/includes`
Now we can create the global project files 

Let's start with the **_navbar.html** file  : `templates/includes/_navbar.html`

```jinja2
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
        <a class="navbar-brand" href="/"><Strong>My Articles</Strong></a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <a class="nav-link" href="/">Home <span class="sr-only">(current)</span></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="/">Articles</a>
                </li>

            </ul>
        </div>
    </div>
</nav>
```
So Now we can **include** our **Navbar**  in the **base layout**  

In the **layout.html** file we put this part of code 

```jinja2
 {% include 'includes/_navbar.html' %}
```

## home.html  

Let's  add some element in  **home.html**  in the `{% block body %}{% endblock %}`
```jinja2
<div class="jumbotron mt-5">
    <h1 class="display-4">Hello, This is My Todos App!</h1>
    <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to
        featured content or information.</p>
    <hr class="my-4">
    <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
    <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
</div>
```

## Getting Data from DB
### I) Get All Articles
#### 1) Web Service
To getting our articles from **DB** we can add this code to **app.py**
```python
@app.route('/articles')
def articles():
    # Create cursor
    cur = mysql.connection.cursor()

    # Get articles
    result = cur.execute("SELECT * FROM articles")

    articles = cur.fetchall()

    return render_template('articles/articles.html', articles=articles)

    cur.close()
```
#### 2) Template
let's add our template **articles.html**
```jinja2
{% extends 'layout.html' %}
{% block title %}
    Articles
{% endblock %}
{% block body %}
    <h1>Articles</h1>
    {% if(articles) %}
        <ul class="list-group">
            {% for article in articles %}
                <li class="list-group-item"><a href="article/{{ article.id }}">{{ article.title }}</a> <small class="float-right text-secondary">{{ article.author | title }}</small></li>
            {% endfor %}
        </ul>
    {% else %}
        <p style="margin: auto;"> There is no articles here 💔</p>
    {% endif %}
{% endblock %}

```
### II) Getting One Article (Show Article)
#### 1) Web service 
To get a single article in our app we can use the **id** as **key** for our selection so we can use the **dynamic route** `.../<type:name>` to do this .
to do this we can add this part of code (service) in our **app.py** file 
```python
# Single Article
@app.route('/article/<string:id>/')
def article(id):
    # Create cursor
    cur = mysql.connection.cursor()

    # Get article
    result = cur.execute("SELECT * FROM articles WHERE id = %s", [id])

    article = cur.fetchone()

    return render_template('articles/article.html', article=article)
```
#### 2) Template 
Our template is soooo easy : just we create the **article.html** file **templates/articles/article.html**
and we can put this code in our **article.html** file
```jinja2
{% extends 'layout.html' %}
{% block title %}
Article | {{ article.title |capitalize }}
{% endblock %}
{% block body %}
<div class="card ">
    <div class="card-header">
        <h5 class="card-title d-inline"> {{ article.title | title }} </h5>
        {% if(session.username == article.author) %}
        <a class="btn btn-secondary float-right" href="/edit_article/{{ article.id }}">Edit</a>
        {% endif %}
    </div>
    <div class="card-body">
        {{ article.body | safe | capitalize }}
    </div>
</div>

{% endblock %}
```
## Authentication 
### Let's play 🎳🎳
Before we creating  the **auth requirement** let's change our **Brand Logo** 🎨 :                   
Now , look at your tab(onglet) before all title of tabs we observe that it has a logo But       
How we can add this logo ?   😕😕    
In our project we had a **static** folder , this folder should contain our **assets(Css,Js,Images ...)**           
So we can put this **image** in our **static** folder 👉👉  [Image](https://drive.google.com/file/d/1QlQT-1ukeRPtWbkEjAcGIbbBubLyeXM9/view?usp=sharing)       
Now we can import it in our base template **layout.html** , To do this just we add this part of code in the `<head>` tag just after the `<title></title>` tag
```jinja2
<link rel="shortcut icon" href="{{ url_for('static', filename='favicon.png') }}" type="image/x-icon">
```
### I) Auth : Register
#### 1) Buttons for authentication
To facilitate access to our routes we have to add some buttons :  for simplicity we can just replace all the code of **\_navbar.html** by  👇
```jinja2
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
        <a class="navbar-brand" href="/"><Strong>My Articles</Strong></a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <a class="nav-link" href="/">Home <span class="sr-only">(current)</span></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="/articles">Articles</a>
                </li>

            </ul>
            {% if session.logged_in %}
            <ul class="navbar-nav">
                <a class="nav-link" href="/dashboard">Dashboard</a>
                <a class="nav-link" href="/logout">Logout</a>
            </ul>
            {% else %}
            <ul class="navbar-nav">
                <a class="btn btn-sm btn-outline-primary m-1" href="/login">Login</a>
                <a class="btn btn-sm btn-primary m-1" href="/register">Register</a>
            </ul>
            {% endif %}

        </div>
    </div>
</nav>
```
