# Setting Up Django

Learn how to install Django, create your first project, and understand the project structure.

## Prerequisites

Before starting, ensure you have:

- **Python 3.8+** installed
- Basic knowledge of Python
- Command line/terminal access
- A code editor (VS Code, PyCharm, etc.)

### Check Python Version

```bash
python --version
# or
python3 --version
```

Should show Python 3.8 or higher.

## Virtual Environments

Always use a virtual environment to isolate project dependencies.

### Create Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

You'll see `(venv)` in your terminal prompt when activated.

### Deactivate Virtual Environment

```bash
deactivate
```

## Installing Django

### Install Django

```bash
pip install django
```

### Install Specific Version

```bash
pip install django==4.2.7
```

### Verify Installation

```bash
python -m django --version
```

Should display the Django version (e.g., `4.2.7`).

## Creating Your First Project

### Create Project

```bash
django-admin startproject myproject
```

This creates a directory structure:

```
myproject/
    manage.py
    myproject/
        __init__.py
        settings.py
        urls.py
        wsgi.py
        asgi.py
```

### Navigate to Project

```bash
cd myproject
```

### Run Development Server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your browser. You should see the Django welcome page!

### Stop Server

Press `Ctrl+C` in the terminal.

## Project Structure Explained

### manage.py

Command-line utility for Django:

```bash
python manage.py runserver    # Start development server
python manage.py migrate      # Apply database migrations
python manage.py createsuperuser  # Create admin user
python manage.py shell        # Open Django shell
```

### settings.py

Main configuration file:

```python
# settings.py

# Secret key (keep secret in production!)
SECRET_KEY = 'your-secret-key-here'

# Debug mode (set to False in production)
DEBUG = True

# Allowed hosts
ALLOWED_HOSTS = []

# Installed apps
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

# Database configuration
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# URL configuration
ROOT_URLCONF = 'myproject.urls'

# Static files (CSS, JavaScript, images)
STATIC_URL = '/static/'
```

### urls.py

URL routing configuration:

```python
# myproject/urls.py
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

### wsgi.py / asgi.py

Server configuration files (usually don't need to modify).

## Creating Your First App

Django projects contain apps. Each app handles a specific feature.

### Create App

```bash
python manage.py startapp myapp
```

This creates:

```
myapp/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

### Register App

Add your app to `INSTALLED_APPS` in `settings.py`:

```python
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',  # Add your app here
]
```

## App Structure Explained

### models.py

Define your data models:

```python
# myapp/models.py
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

### views.py

Handle requests and return responses:

```python
# myapp/views.py
from django.shortcuts import render
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, World!")
```

### admin.py

Configure Django admin interface:

```python
# myapp/admin.py
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

### urls.py (Create this file)

URL routing for your app:

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

## Setting Up URLs

### Include App URLs in Project

```python
# myproject/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),  # Include app URLs
]
```

## Database Setup

Django uses SQLite by default (good for development).

### Create Initial Migrations

```bash
python manage.py makemigrations
```

### Apply Migrations

```bash
python manage.py migrate
```

This creates the database tables Django needs.

## Creating a Superuser

Create an admin user to access Django admin:

```bash
python manage.py createsuperuser
```

Follow prompts to create username, email, and password.

Access admin at: `http://127.0.0.1:8000/admin/`

## Your First View

### Create View

```python
# myapp/views.py
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, Django!")
```

### Create URL Pattern

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

### Include in Project URLs

```python
# myproject/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

Visit `http://127.0.0.1:8000/` - you should see "Hello, Django!"

## Development Server Options

### Run on Different Port

```bash
python manage.py runserver 8080
```

### Run on All Interfaces

```bash
python manage.py runserver 0.0.0.0:8000
```

### Auto-reload

The development server automatically reloads when you change code. No need to restart manually!

## Complete Setup Example

### Step-by-Step

```bash
# 1. Create virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# 2. Install Django
pip install django

# 3. Create project
django-admin startproject myblog
cd myblog

# 4. Create app
python manage.py startapp blog

# 5. Register app in settings.py
# Add 'blog' to INSTALLED_APPS

# 6. Run migrations
python manage.py migrate

# 7. Create superuser
python manage.py createsuperuser

# 8. Run server
python manage.py runserver
```

## Common Setup Issues

### Issue: Command Not Found

**Problem:** `django-admin` not found

**Solution:**
```bash
python -m django startproject myproject
# or
python3 -m django startproject myproject
```

### Issue: Port Already in Use

**Problem:** Port 8000 already in use

**Solution:**
```bash
python manage.py runserver 8001
```

### Issue: Migration Errors

**Problem:** Database migration errors

**Solution:**
```bash
# Delete db.sqlite3 and migrations folder
# Then:
python manage.py makemigrations
python manage.py migrate
```

## Best Practices

1. **Always use virtual environments:** Isolate dependencies
2. **Keep DEBUG=False in production:** Security risk if True
3. **Never commit SECRET_KEY:** Use environment variables
4. **Use version control:** Git for your projects
5. **Follow naming conventions:** Lowercase with underscores
6. **One app, one purpose:** Keep apps focused

## Project Checklist

After setup, verify:

- [ ] Virtual environment created and activated
- [ ] Django installed and verified
- [ ] Project created successfully
- [ ] App created and registered
- [ ] Migrations applied
- [ ] Development server runs
- [ ] Admin interface accessible
- [ ] First view working

## What's Next?

Now that Django is set up, learn to:

- **Create Models** - Define your data structure
- **Work with Databases** - Store and retrieve data
- **Create Views** - Handle user requests
- **Build Templates** - Create dynamic HTML pages
- **Handle Forms** - Process user input

---

**Previous Tutorial:** [Introduction to Django](01_introduction.md)  
**Next Tutorial:** [Models and Databases](03_models_databases.md)

