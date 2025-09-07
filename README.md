# django-login-with-google


## 1. Create a new folder
```bash
cd Desktop
mkdir django_login_with_google
cd django_login_with_google
```
<hr>

## 2. Install environment
```bash
python3 -m venv .venv
# or
virtualenv .venv
# then
source .venv/bin/activate
```
<hr>

## 3. Installation django, django-allauth, requests, PyJWT, cryptography
```bash
pip install django django-allauth requests PyJWT cryptography
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
    'users',
    
]
```
<hr>

## 6. Google Cloud Console
We start to enter Google Clod Console website

  ## Step - 1
  
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image01.png?raw=true)

<br>

  ## Step - 2 
  We push the button "Select a project"
  
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image02.png?raw=true)

<br>

## Step - 3
Create new project called “loginwithgoogle”

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image03.png?raw=true)

<br>

## Step - 4

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image04.png?raw=true)

<br>

## Step - 5
Then we choose APIs & Services > Oauth consent screen.

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
Then we choose Data Access > Add or remove scopes

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image13.png?raw=true)

<br>

## Step - 14
Save all things

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image14.png?raw=true)

<br>

## Step - 15
We choose “Create client”

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image15.png?raw=true)

<br>

## Step - 16
We choose “Web application”

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
We need to download JSON file

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image20.png?raw=true)

<br>

## Step - 21

![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image21.png?raw=true)

<br>


## 7. myproject/settings.py
```python

SITE_ID=1      

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

    # Allauth apps                   
    #'django.contrib.sites',   ---> This code brings bugs, that's why don't use this

    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',

    
]

SOCIALACCOUNT_PROVIDERS = {                     
    "google": {
        "SCOPE": [
            "profile",
            "email"
        ],
        "AUTH_PARAMS": {"access_type": "online"}
    }
}


MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',  # must come before AccountMiddleware
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',

    'allauth.account.middleware.AccountMiddleware',  # ← required by newer allauth
]

....

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',  # Default
    'allauth.account.auth_backends.AuthenticationBackend',  # Allauth
]


LOGIN_REDIRECT_URL = '/'
LOGOUT_REDIRECT_URL = '/'

```
<hr>



## 8. myprofile/urls.py
```python
from django.contrib import admin
from django.urls import path, include
from accounts import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/', include('allauth.urls')),  # Allauth URLs
    path('', views.home, name='home'),
]
```
<hr>

## 9. users/views.py
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

## 10. users/urls.py
```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.home, name='home'),
    path("logout", views.logout_view, name='logout_view'),
]
```
<hr>

## 11. myprofile/settings.py
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
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

## 12. <b>Template:</b> `templates/users/home.html`
Create a folder `templates/users/` inside our "users" app and `home.html` file.
```django
{% load socialaccount %}

{% if user.is_authenticated %}
  <h2>Welcome, {{ user.email }}</h2>
  <a href="{% url 'account_logout' %}">Logout</a>
{% else %}
  <h2>Login</h2>
  <a href="{% url 'account_login' %}">Email Login</a><br>
  <a href="{% provider_login_url 'google' %}?next=/">Login with Google</a>
{% endif %}
```
<hr>

## 13. Run Migrations
Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```
<hr>

## 14. Create Admin

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

## Step - 3
![image](https://github.com/kurbonovdilmurod/django-login-with-google/blob/main/images_repository/image24.png?raw=true)

<br>

<hr>

## 10. Google OAuth Setup
1. Go to Google Cloud Console.
2. Create a project →  <b>OAuth Consent Screen</b> →  configure.
3. Create <b>OAuth 2.0 Client ID</b> (type = Web Application).
   * <b>Authorized redirect URI:
     ```ruby
     http://localhost:8000/accounts/google/login/callback/
     ```
4. Copy the <b>Client ID</b> and <b>Client Secret</b>.

<hr>

## 11. Add SocialApp in Django Admin
Run migrations and create a superuser:
```bash
python manage.py migrate
python manage.py createsuperuser
```
Run server:
```bash
python manage.py runserver
```
Go to: `http://127.0.0.1:8000/admin/`
- Open <b>Social Applications</b> → Add New:
  * Provider: <b>Google</b>
  * Name: `Google`
  * Client ID:(paste from Google)
  * Secret Key:(paste from Google)
  * Sites: check `example.com` (or `localhosts:8000`)

<hr>









