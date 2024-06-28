# README #

Sample oAuth server based on DRF Django

FOLLOW: `https://django-oauth-toolkit.readthedocs.io/en/latest/rest-framework/getting_started.html`

### What is this repository for? ###

* Purpose is to provide sample oauth server for localhost development

### How do I get set up? ###

* Install requirement with `pip install -r requirements.txt`
* CD to `oauth_server` folder and run `python manage.py makemigrations`, then `python manage.py migrate`
* Create superuser with `python manage.py createsuperuser`
* Run server with `python manage.py runserver 127.0.0.1:8800`
* In browser go to `127.0.0.1:8800`, log in with super user, then create api user
* Create new application via admin with following attributes:
 - Redirect url: http://127.0.0.1:8000
 - Client type: Confidential
 - Authorization grant type: Resource owner password-based
 - Client secret: any token, must be saved and stored before saving application
 - Algorithm: No OIDC Support
* Create new Access Token with attributes:
 - User: created user
 - Token: any token
 - Application: application from previous step
 - Expires: selected date
 - Scope: read write introspection
* Alternatively:
* Go to `http://127.0.0.1:8800/o/applications/register/` and create application
* Get token via url `http://127.0.0.1:8800/o/token/`
```
curl -X POST -d "grant_type=password&username=<username>&password=<password>" -u"<client_id>:<client_secret>" http://127.0.0.1:8800/o/token/
```

### Usage ###

* To verify user request from resorce server call Introspect: `http://127.0.0.1:8800/o/introspect/`

```
curl --location --request POST 'http://127.0.0.1:8800/o/introspect/' --header 'Authorization: Bearer <access_token>' --header 'Accept: application/json' --header 'Content-Type: application/x-www-form-urlencoded' --data-urlencode 'token=<access_token>'
```
