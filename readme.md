# Python Social Auth - Django
This app is basic implementation of python-social-auth
Python Social Auth is an easy to setup social authentication/registration
mechanism with support for several frameworks and auth providers.

## Description

In this app basic implementation of social authentication with Google OAuth2 is created


Project documentation is available at http://python-social-auth.readthedocs.org/.

## Setup


1. create basic django applcation.
2. install python-social-auth package.

```shell
$ pip install python-social-auth
```
3. Add following in settings.py

To create social auth keys please refer to: 
https://developers.google.com/identity/sign-in/web/sign-in

```shell script

    # Add social_django in installed apps settings 
    INSTALLED_APPS = [
    .....
    'social_django',
    .....
    ]

    # add google auth backend and django default backend
    AUTHENTICATION_BACKENDS = (
        'social_core.backends.google.GoogleOAuth2',
        'django.contrib.auth.backends.ModelBackend',
    )
        
    # create app in google console and add api keys
    SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = ''
    SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = ''
    # Add redirect url on which user is redireced after authentication
    SOCIAL_AUTH_LOGIN_REDIRECT_URL = '/login/'

``` 

4. Create new module with any name (sauth in this repo) and do not foget to add it to INSTALLED_APPS 
5. Add path('', include('sauth.urls')) to urls.py file in new created file.
6. Create view and template file in this module.
7. Create new view in view.py
```python
from django.views.generic import TemplateView

class LoginView(TemplateView):
    template_name = "login.html"
```
8. in templates/login.html add following HTML
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Login</title>
</head>
<body>
    <a href="{% url "social:begin" "google-oauth2" %}">Google+</a>
    <p>{{ user.is_authenticated }} {{ user.username }}</p>
</body>
</html>
```

9. In sauth/urls.py add new url poining to the view created above.
```python
path('', include('social_django.urls', namespace='social')),
```

10. Include these urls to root app urls.py ie
```python
path('', include('sauth.urls'))
```



