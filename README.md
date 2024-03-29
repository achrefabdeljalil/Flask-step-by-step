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
## Auth Module 
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
#### 1) Buttons for authentication ✅✅
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
#### 2) Model Creation ✅✅
As we see in the **MVC design pattern** we should prepare our model in work to ficilitate the work .        
So we can add our models in **app.py** file and this code is what we will use in our project 👇👇
```python
# Register Form Class
class RegisterForm(Form):
    name = StringField('', [validators.Length(min=1, max=50)], render_kw={"placeholder": "Name"})
    username = StringField('', [validators.Length(min=4, max=25)], render_kw={"placeholder": "Username"})
    email = StringField('', [validators.Length(min=6, max=50)], render_kw={"placeholder": "Email"})
    password = PasswordField('', [
        validators.DataRequired(),
        validators.EqualTo('confirm', message='Passwords do not match')
    ], render_kw={"placeholder": "Password"})
    confirm = PasswordField('', render_kw={"placeholder": "Confirm Password"})

```

#### 3) Route for Registration ✅✅
As we see with other **fonctionality** ,to make an action in our app we have to make a correspendant **Route** 
So let's do it : we can add this code to **app.py** file 👇👇
```python
# User Register
@app.route('/register', methods=['GET', 'POST'])
def register():
    form = RegisterForm(request.form)
    if request.method == 'POST' and form.validate():
        name = form.name.data
        email = form.email.data
        username = form.username.data
        password = sha256_crypt.hash(str(form.password.data))
        # Create cursor
        cur = mysql.connection.cursor()

        # Execute query
        cur.execute("INSERT INTO users(name, email, username, password) VALUES(%s, %s, %s, %s)",
                    (name, email, username, password))

        # Commit to DB
        mysql.connection.commit()

        # Close connection
        cur.close()

        flash('You are now registered and you can log In', 'success')

        return redirect(url_for('index'))
    return render_template('auth/register.html', form=form)

```
#### 4) Template for registration ✅✅     
So to finish our registration fonctionality w just miss the template (form)          
To work with **the best practice** , Each **Module** in our project should be in a separated folder 😉😉✅✅
So we have to create a new folder with **auth** as name in **templates/auth**
And in the **auth** folder we will create the **register.html** file : **templates/auth/register.html** file 
We just miss to put this code in our **register.html** file 👇👇
```jinja2
{% extends 'layout.html' %}
{% block title %}
    Register
{% endblock %}

{% block body %}
    <div class="card" style="width: 30rem; margin: auto">
        <div class="card-header">
            <h5 class="card-title d-inline"> Register</h5>
            <a href="/login" class="float-right"> Login</a>
        </div>
        <div class="card-body">
            {% from "includes/_formhelpers.html" import render_field %}
            <form method="POST" action="">
                <div class="form-group">
                    {{ render_field(form.name, class_="form-control") }}
                </div>
                <div class="form-group">
                    {{ render_field(form.email, class_="form-control") }}
                </div>
                <div class="form-group">
                    {{ render_field(form.username, class_="form-control") }}
                </div>
                <div class="form-group">
                    {{ render_field(form.password, class_="form-control") }}
                </div>
                <div class="form-group">
                    {{ render_field(form.confirm, class_="form-control") }}
                </div>
                <input type="submit" class="btn btn-primary float-right" value="Submit">
            </form>
        </div>
    </div>


{% endblock %}

```
#### 5) Before we finish just we miss a little somthing ✅✅
To work with the **Flash message** we can create a specefic file and include it in the base layout **layout.html**
So we can create the **templates/includes/\_messages.html** file and put this code in 
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
Let's include the **flash messages** in our base layout **layout.html**  , just before the line `{% block body %} {% endblock %}`
```jinja2
{% include 'includes/_messages.html' %}
```
To work with the a specefic **form** we can create the file and include it in the our **form**
So we can create the **templates/includes/\_formhelpers.html** file and put this code in 
```jinja2
{% macro render_field(field) %}
  {{ field(**kwargs)|safe }}
  {% if field.errors %}
    {% for error in field.errors %}
      <span class="help-inline">{{ error }}</span>
    {% endfor %}
  {% endif %}
{% endmacro %}
```
### II) Auth : Login
#### 1) Route for Login ✅✅ 
In the case bellow we have the **logic** of our **Login route** : we can add this code to **app.py** file
```python
# User login
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # Get Form Fields
        username = request.form['username']
        password_candidate = request.form['password']

        # Create cursor
        cur = mysql.connection.cursor()

        # Get user by username
        result = cur.execute("SELECT * FROM users WHERE username = %s", [username])

        if result > 0:
            # Get stored hash
            data = cur.fetchone()
            password = data['password']

            # Compare Passwords
            if sha256_crypt.verify(password_candidate, password):
                # Passed
                session['logged_in'] = True
                session['username'] = username

                flash('You are now logged in', 'success')
                return redirect(url_for('articles'))
            else:
                error = 'Invalid login'
                return render_template('auth/login.html', error=error)
            # Close connection
            cur.close()
        else:
            error = 'Username not found'
            return render_template('auth/login.html', error=error)

    return render_template('auth/login.html')
```   
#### 2) Template for Login ✅✅ 
As we see in the **register** option we can here just create a new file with **login.html** in **templates/auth/login.html**
```jinja2
{% extends 'layout.html' %}
{% block title %}
    Login
{% endblock %}
{% block body %}

    <div class="card mt-5" style="width: 30rem; margin: auto">
        <div class="card-header">
            <h5 class="card-title d-inline"> Login</h5>
            <a href="/register" class="float-right" > Register</a>
        </div>
        <div class="card-body">
            <form action="" method="POST">
                <div class="input-group mb-3">
                    <div class="input-group-prepend">
                        <div class="input-group-text">&#128102;</div>
                    </div>
                    <input type="text" name="username" placeholder="Username" class="form-control"
                           value={{ request.form.username }}>
                </div>
                <div class="input-group mb-3">
                    <div class="input-group-prepend">
                        <span class="input-group-text" id="basic-addon1">&#128273;</span>
                    </div>
                    <input type="password" name="password" placeholder="Password" class="form-control"
                           value={{ request.form.password }}>
                </div>
                <button type="submit" class="btn btn-primary float-right">Submit</button>
            </form>
        </div>
    </div>


{% endblock %}

```
### III) Auth : Logout 
#### 1) Route for Logout 
So the last thing in **Auth Module** is To create the **logout** option,The simple way to do this is to add the correspandant **route** in the **app.py**
```python
# Check if user logged in
def is_logged_in(f):
    @wraps(f)
    def wrap(*args, **kwargs):
        if 'logged_in' in session:
            return f(*args, **kwargs)
        else:
            flash('To access to your dashboard, Please login', 'danger')
            return redirect(url_for('login'))
    return wrap


# Logout
@app.route('/logout')
@is_logged_in
def logout():
    session.clear()
    flash('You are now logged out', 'success')
    return redirect(url_for('login'))
```
### IV) Auth : My Profile (Dashboard)
#### 1) Route for Dashboard 
In this level We can add our Route easily : in the file **app.py** we can add this code 
```python
# Dashboard
@app.route('/dashboard')
@is_logged_in
def dashboard():
    # Create cursor
    cur = mysql.connection.cursor()

    # Get articles
    # result = cur.execute("SELECT * FROM articles")
    # Show articles only from the user logged in
    result = cur.execute("SELECT * FROM articles WHERE author = %s", [session['username']])

    articles = cur.fetchall()

    return render_template('auth/dashboard.html', articles=articles)
    # Close connection
    cur.close()
```
#### 2) Template for Dashboard 
As long as our dashboard route belongs to **Auth Module** so the template will be in the auth folder : **templates/auth/dashboard.html**
```jinja2
{% extends 'layout.html' %}
{% block title %}
    Dashboard
{% endblock %}
{% block body %}

    <div class="card">
        <div class="card-header">
            <h3 class="d-inline"> List of articles</h3>
            <a class="float-right btn btn-light d-inline" href="/add_article">
                ➕
            </a>
        </div>
        <div class="card-body">
        {% if(articles) %}
            <table class="table table-striped">
                <tr>
                    <th>ID</th>
                    <th>Title</th>
                    <th>Author</th>
                    <th>Date</th>
                    <th></th>
                    <th></th>
                </tr>
                {% for article in articles %}
                    <tr>
                        <td>{{ article.id }}</td>
                        <td><a href="/article/{{ article.id }}">{{ article.title }}</a></td>
                        <td>{{ article.author }}</td>
                        <td>{{ article.create_date }}</td>
                        <td style="width: 5%;"><a href="edit_article/{{ article.id }}"
                                                  class="btn btn-secondary">Edit</a></td>
                        <td style="width: 5%;">
                            <form action="delete_article/{{article.id}}" method="POST">
                                <input type="hidden" name="_method" value="DELETE">
                                <input type="submit" value="Delete" class="btn btn-danger">
                            </form>
                        </td>
                    </tr>
                {% endfor %}
            </table>
        {% else %}
            <p style="margin: auto;"> There is no articles here 💔</p>
        {% endif %}
        </div>
    </div>

{% endblock %}

```
## Articles Module 
### I) New Article 
#### 1) Route for New Article (app.py)
```python

# Article Form Class
class ArticleForm(Form):
    title = StringField('', [validators.Length(min=1, max=200)], render_kw={"placeholder": "Title"})
    body = TextAreaField('', [validators.Length(min=30)], render_kw={"placeholder": "Body"})


# Add Article
@app.route('/add_article', methods=['GET', 'POST'])
@is_logged_in
def add_article():
    form = ArticleForm(request.form)
    if request.method == 'POST' and form.validate():
        title = form.title.data
        body = form.body.data

        # Create Cursor
        cur = mysql.connection.cursor()

        # Execute
        cur.execute("INSERT INTO articles(title, body, author) VALUES(%s, %s, %s)", (title, body, session['username']))

        # Commit to DB
        mysql.connection.commit()

        # Close connection
        cur.close()

        flash('Article Created', 'success')

        return redirect(url_for('dashboard'))

    return render_template('articles/add_article.html', form=form)

```
#### 2) Template for new Article (templates/articles/add_article.html)
```jinja2
{% extends 'layout.html' %}
{% block title %}
    New Article
{% endblock %}
{% block body %}
    <div class="card" style="width: 30rem; margin: auto">
        <div class="card-header">
            <h4 class="card-title"> New Article </h4>
        </div>
        <div class="card-body">
            {% from "includes/_formhelpers.html" import render_field %}
            <form method="POST" action="">
                <div class="form-group" >
                    {{ render_field(form.title, class_="form-control") }}
                </div>
                <div class="form-group">
                    {{ render_field(form.body, class_="form-control", id="editor",placeholder="Description ") }}
                </div>
                <p><input class="btn btn-primary float-right" type="submit" value="Submit">
            </form>
        </div>
    </div>

{% endblock %}

```
### II) Edit Article 
#### 1) Route for Edit Article (app.py)
```python

# Edit Article
@app.route('/edit_article/<string:id>', methods=['GET', 'POST'])
@is_logged_in
def edit_article(id):
    # Create cursor
    cur = mysql.connection.cursor()

    # Get article by id
    result = cur.execute("SELECT * FROM articles WHERE id = %s", [id])

    article = cur.fetchone()
    cur.close()
    # Get form
    form = ArticleForm(request.form)

    # Populate article form fields
    form.title.data = article['title']
    form.body.data = article['body']

    if request.method == 'POST' and form.validate():
        title = request.form['title']
        body = request.form['body']

        # Create Cursor
        cur = mysql.connection.cursor()
        app.logger.info(title)
        # Execute
        cur.execute("UPDATE articles SET title=%s, body=%s WHERE id=%s", (title, body, id))
        # Commit to DB
        mysql.connection.commit()

        # Close connection
        cur.close()

        flash('Article Updated', 'success')

        return redirect(url_for('dashboard'))

    return render_template('articles/edit_article.html', form=form)

```
#### 2) Template for Edit Article (templates/articles/edit_article.html)
```jinja2
{% extends 'layout.html' %}
{% block title %}
    Edit Article
{% endblock %}
{% block body %}
    <div class="card" style="width: 30rem; margin: auto">
        <div class="card-header">
            <h4 class="card-title"> Edit Article </h4>
        </div>
        <div class="card-body">
            {% from "includes/_formhelpers.html" import render_field %}
            <form method="POST" action="">
                <div class="form-group">
                    {{ render_field(form.title, class_="form-control") }}
                </div>
                <div class="form-group">
                    {{ render_field(form.body, class_="form-control", id="editor") }}
                </div>
                <p><input class="btn btn-primary float-right" type="submit" value="Submit">
            </form>
        </div>
    </div>

{% endblock %}

```
### III) Delete Article 
#### 1) Route for Delete Article (app.py)
```python
# Delete Article
@app.route('/delete_article/<string:id>', methods=['POST'])
@is_logged_in
def delete_article(id):
    # Create cursor
    cur = mysql.connection.cursor()

    # Execute
    cur.execute("DELETE FROM articles WHERE id = %s", [id])

    # Commit to DB
    mysql.connection.commit()

    # Close connection
    cur.close()

    flash('Article Deleted', 'success')

    return redirect(url_for('dashboard'))
```

# THE END 
