# Flask-step-by-step  with  [@achrefabdeljalil](https://www.linkedin.com/in/achref-abdeljalil-179aa5136)



## Get Started ✅✅

1. Install (Python)[https://www.python.org/downloads/]        
2. Install [PyCharm](https://www.jetbrains.com/fr-fr/pycharm/)         
3. Create a new Flask project with Pycharm                  


## Let's Jump In ✅✅


1. Lets test our functions in **app.py** by running project 
2. To avoid running project in every single change we can activate the **debug mode**
- By adding this part of code in **app.py**
```
app.config['ENV'] = 'development'
app.config['DEBUG'] = True
app.config['TESTING'] = True
```       
- And running this two command in **terminal** 
```
$ set FLASK_ENV=development 
$ set FLASK_DEBUG=1
```
