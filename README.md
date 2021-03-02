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
            <details><summary>Code ME</summary>
            <p>
            ```
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta http-equiv="X-UA-Compatible" content="IE=edge">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>Document</title>
                </head>
                <body>
                    <h1>hello world</h1>
                </body>
                </html>
            ```
            </p>
            </details>
