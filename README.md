# Flask-step-by-step  with  [@achrefabdeljalil](https://www.linkedin.com/in/achref-abdeljalil-179aa5136)



## Get Started ✅✅

1. Install (Python)[https://www.python.org/downloads/]        
2. Install [PyCharm](https://www.jetbrains.com/fr-fr/pycharm/)         
3. Create a new Flask project with Pycharm                  


## Let's Jump In ✅✅


1. Lets test our functions in **app.py** by running project 
2. To avoid running project in every single change we can activate the **debug mode**
    - By adding this part of code in **app.py**
    ```python
    app.run(debug=True)
    ```       
    - And running this two command in **terminal** 
    ```cmd
    $ set FLASK_ENV=development 
    $ set FLASK_DEBUG=1
    ```
3. And Now Let's test our template 

    - By adding This part of code in **app.py**
    ```python
    from flask import Flask, render_template
    ```
    
