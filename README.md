# Flask REST API

Heroku is a web service that runs our code and allows other to access/interact it.
This process is called "hosting"

Apart from being able to host our application, it also enables SSL (Secure Sockets Layer)
for us, meaning that the communication between the client and server (Heroku) will be encrypted.
This is useful when sending sensitive information such as password to ensure other people can't
snoop on that information.

## Steps to host on Heroku

https://github.com/datademofun/heroku-basic-flask

1. `runtime.txt` specifies the runtime environment, i.e. which python version.
2. include the `requirements.txt`
3. `uwsgi.ini` configuration parameters for the uwsgi process to run our app.
    1. For the http port, we will use the $POST variable that's specified by heroku.
    2. module = app:app refers to the app variable in the app module.
4. `Procfile`. Tells Heroku the process type, in our case a web process and the command to execute that starts the app. Here we will tell it to run it with uwsgi.