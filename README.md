# Flask REST API

## Endpoints

Start the app locally.

```python
python app/app.py
```

<img src=screenshots/endpoints.png width=30% height=30%>

Example:

- call `/register` with username and password to register a user.
- call `/auth` with the username and password to retrieve the JWT token.
- post `/store/<name>` to create a store.
- post `/item/<name>` with price and store_id to create a new item.
- post `/items` to retrieve all the items.

## Authentication

The app uses [JWT](https://pythonhosted.org/Flask-JWT/) on some of the endpoints for security.

JWT, Json Web Token allows us to encode our message so that other people who don't have the decryption key won't be able to read the encoded message.

Here we make a request that contains the username and password to the `/auth` resource to get the token. If done correctly, we should get a response that looks something like this:

```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjY0NDU5NDEsImlhdCI6MTU2NjQ0NTY0MSwibmJmIjoxNTY2NDQ1NjQxLCJpZGVudGl0eSI6MX0.0P9OQoNyHKfB6B9NAVeZTKdVTZULOqgz8JgGCz-5y8k"
}
```

Then for all the endpoints that are marked as `@jwt_required()`, e.g. during get `/item/<name>`, we need to send the token along with the request, i.e. we need to include an additional header `Authorization: JWT [insert the token above here]`.

# Heroku Deployment

Heroku is a web service that runs our code and allows other to access/interact with it.
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


We can then create a app with Heroku.

1. Connect the Github repo to Heroku (Deploy tab)
2. Use postgresql as our database, add it as a add-on to our app (Resources tab)
3. After the installation, we can use the database's url provided by heroku (Settings tab, Config vars)
4. Add the Python build-pack (Settings tab)
5. We can choose manual deploy or automatic deploy. (Deploy tab)
6. After deploying we can test the endpoints in Postman, remember to change the URI.

We can install the heroku command line and check our app's logs

```bash
# after installing heroku cli
heroku login
heroku logs --app=[insert out app name here]
```
