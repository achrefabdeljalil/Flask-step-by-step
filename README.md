# Flask-step-by-step  with  [@achrefabdeljalil](https://www.linkedin.com/in/achref-abdeljalil-179aa5136)



## Get Started ✅✅

1. Install [Python](https://www.python.org/downloads/)        
2. Install [Xamp](https://www.apachefriends.org/fr/download.html)
3. Install [PyCharm](https://www.jetbrains.com/fr-fr/pycharm/)         
4. Create a new Flask project with Pycharm                  


## Let's Jump In ✅✅


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
7. To make our project more professional we can work with the **Block** notion  
so let's create a file **layout.html** : this file will be the basic of our template 
and we can put this code as exemple 
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
and update the code of **home.html** to 
```jinja2
{% extends 'layout.html' %}
{% block title %}
  Home
{% endblock %}
{% block body %}
    <h1>hello from <em> home page</em></h1>
{% endblock %}
```
8. The next step is to integrate [Bootstrap 4 ](https://getbootstrap.com/docs/4.6/getting-started/introduction/) with our project <br>
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
and this is the file **_navbar.html**
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
                    <a class="btn btn-outline-primary " href="/login">Login</a>
                    <a class="btn btn-primary ml-2" href="/register">Register</a>
                </ul>
            {% endif %}

        </div>
    </div>
</nav>
```
and this is the file **_messages.html** 
```jinja2
{% with messages = get_flashed_messages(with_categories=true) %}
  {% if messages %}
    {% for category, message in messages %}
      <div class="alert alert-{{ category }} " id="custom-alert">{{ message }}</div>
    {% endfor %}
  {% endif %}
{% endwith %}

{% if error %}
  <div class="alert alert-danger "  id="custom-alert">{{error}}</div>
{% endif %}

{% if msg %}
  <div class="alert alert-success " id="custom-alert">{{msg}}</div>
{% endif %}
```
