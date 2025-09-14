# django-login-with-google


## 1. Create a new folder
```bash
cd Desktop
mkdir django_login_with_google
cd django_login_with_google
```
<hr>

## 2. Install an environment
```bash
python3 -m venv .venv
# or
virtualenv .venv
# then
source .venv/bin/activate
```
<hr>

## 3. Install django and django-allauth
```bash
pip install django
```
```bash
pip install "django-allauth[socialaccount]"
```
<hr>

## 4. Project setup
Create a new project and app:
```bash
django-admin startproject myproject .
python manage.py startapp users
```
<hr>

## 5. myproject/settings.py
```python
INSTALLED_APPS = [
    # Django apps
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.sites',


    # My app
    'users',      # new
    
]
```
<hr>

## 6. Google Cloud Console
 Start to enter Google Cloud Console website

  ## Step - 1
  
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image01.png?raw=true)

<br>

  ## Step - 2 
  Push the button "Select a project"
  
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image02.png?raw=true)

<br>

## Step - 3
Create a new project called “loginwithgoogle”

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image03.png?raw=true)

<br>

## Step - 4

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image04.png?raw=true)

<br>

## Step - 5
Then choose APIs & Services > Oauth consent screen.

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image05.png?raw=true)

<br>

## Step - 6

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image06.png?raw=true)

<br>

## Step - 7

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image07.png?raw=true)

<br>

## Step - 8

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image08.png?raw=true)

<br>

## Step - 9

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image09.png?raw=true)

<br>

## Step - 10

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image10.png?raw=true)

<br>

## Step - 11

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image11.png?raw=true)

<br>

## Step - 12

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image12.png?raw=true)

<br>

## Step - 13
Then choose Data Access > Add or remove scopes

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image13.png?raw=true)

<br>

## Step - 14
Save all things

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image14.png?raw=true)

<br>

## Step - 15
Choose “Create client”

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image15.png?raw=true)

<br>

## Step - 16
Choose “Web application”

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image16.png?raw=true)

<br>

## Step - 17

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image17.png?raw=true)

<br>

## Step - 18

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image18.png?raw=true)

<br>

## Step - 19

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image19.png?raw=true)

<br>

## Step - 20
Download JSON file

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image20.png?raw=true)

<br>

## Step - 21

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image21.png?raw=true)

<br>


## 7. myproject/settings.py
```python    

INSTALLED_APPS = [
    # Django apps
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.sites',


    # My app
    'users',

    # Allauth apps     # new              
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',

    
]

  

SOCIALACCOUNT_PROVIDERS = {      # new               
    "google": {
        "SCOPE": [
            "profile",
            "email"
        ],
        "AUTH_PARAMS": {
            "access_type": "online",
            "prompt": 'consent'
        },
        'APP': {
            'client_id': '123',
            'secret': '456',
            'key': ''
        }
    }
}

SITE_ID=1    # new


MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',  # must come before AccountMiddleware
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',

    'allauth.account.middleware.AccountMiddleware',  # ← required by newer allauth   # new
]

....

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

AUTHENTICATION_BACKENDS = [     # new

     # Needed to login by username in Django admin, regardless of `allauth`
    'django.contrib.auth.backends.ModelBackend',  # Default    

     # `allauth` specific authentication methods, such as login by email
    'allauth.account.auth_backends.AuthenticationBackend',  # Allauth
]


LOGIN_REDIRECT_URL = '/'    # new
LOGOUT_REDIRECT_URL = '/'   # new

SOCIALACCOUNT_LOGIN_ON_GET = True     # new

```
<hr>

## 8. myproject/urls.py
```python
from django.contrib import admin
from django.urls import path, include  #new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/', include('allauth.urls')),  # Allauth URLs   # new
```
<hr>

## 9. Run Migrations
Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```
<hr>

## 10. Install django-environ
```bash
pip install django-environ
```
<hr>

## 11. myproject/settings

```python
from pathlib import Path

# django-environ    # new
from environ import Env   
env = Env()
env.read_env()
...
```
<hr>

## 12. Create .env file in the myproject --- myproject/.env
```python
OAUTH_GOOGLE_CLIENT_ID=414286277036-84iv7p7p6968kerq1efbsec0kfhr36gd.apps.googleusercontent.com
OAUTH_GOOGLE_SECRET=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
```

<hr>

## 13. myproject/settings.py
```python
...

SOCIALACCOUNT_PROVIDERS = {
    "google": {
        "SCOPE": [
            "profile",
            "email"
        ],
        "AUTH_PARAMS": {
            "access_type": "online",
            "prompt": 'consent'
        },
        'APP': {
            'client_id': env('OAUTH_GOOGLE_CLIENT_ID'),  # new
            'secret': env('OAUTH_GOOGLE_SECRET'),   # new
            'key': ''
        }
    }
}
...
```



## 14. myproject/urls.py
```python
from django.contrib import admin
from django.urls import path, include
from users import views    # new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/', include('allauth.urls')),  # Allauth URLs
    path('', views.home, name='home'),   # new
]
```
<hr>

## 15. users/views.py
```python
from django.shortcuts import render, redirect
from django.contrib.auth import logout

def home(request):
    return render(request, "users/home.html")

def logout_view(request):
    logout(request)
    return redirect("/")
```

<hr>

## 16. users/urls.py
```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.home, name='home'),
    path("logout", views.logout_view, name='logout_view'),
]
```
<hr>

## 17. myproject/settings.py
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],   # new
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',   # ← allauth needs this
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
<hr>

## 18. <b>Template:</b> `templates/users/home.html`
Create a folder `templates/users/` inside our "users" app and `home.html` file.
```django
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Django Login With Google</title>
</head>
<body>
{% load socialaccount %}

{% if user.is_authenticated %}
  <h2>Welcome, {{ user.email }}</h2>
  <a href="{% url 'account_logout' %}">Logout</a>
{% else %}
  <h2>Login</h2>
  <a href="{% provider_login_url 'google' %}?next=/">Login with Google</a>
{% endif %}
</body>
</html>
```
<hr>

## 19. Run Migrations
Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```
<hr>

## 20. Create Admin

Create a superuser
```bash
python manage.py createsuperuser
```
<hr>

## Step - 1
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image22.png?raw=true)

<br>

## Step - 2
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image23.png?raw=true)

<br>

<hr>

## 21. So we can login with Google

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image25.png?raw=true)

<br>
<br>










