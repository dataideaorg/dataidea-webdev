# Introduction to Django

Django is a high-level Python web framework that enables rapid development of secure and maintainable websites. It follows the "batteries included" philosophy, providing everything you need to build web applications.

## What is Django?

Django is a free, open-source web framework written in Python. It helps you build web applications quickly by providing:
- Built-in admin interface
- Database ORM (Object-Relational Mapping)
- URL routing
- Template system
- Security features
- And much more!

### Key Characteristics

- **High-Level Framework:** Handles common web development tasks
- **Batteries Included:** Comes with many built-in features
- **Secure:** Built-in protection against common vulnerabilities
- **Scalable:** Used by major sites like Instagram, Spotify, and NASA
- **Python-Based:** Uses Python, a beginner-friendly language

## Why Learn Django?

### Rapid Development

- **Fast Setup:** Get a working app in minutes
- **Less Code:** Django handles many tasks automatically
- **Best Practices:** Encourages good coding practices
- **Documentation:** Excellent, comprehensive documentation

### Industry Standard

- **Popular:** One of the most popular Python frameworks
- **Job Market:** High demand for Django developers
- **Community:** Large, active community
- **Ecosystem:** Many third-party packages available

### What You Can Build

- Web applications
- REST APIs
- Content management systems
- E-commerce sites
- Social networks
- And much more!

## How Django Works

Django follows the **MVC (Model-View-Controller)** pattern, which it calls **MTV (Model-Template-View)**:

### Model
- Represents your data structure
- Interacts with the database
- Defines business logic

### Template
- Handles presentation layer
- HTML with Django template language
- Separates design from logic

### View
- Handles user requests
- Processes data
- Returns responses

## Django Architecture

```
Request → URL Routing → View → Model → Database
                              ↓
                         Template → Response
```

1. **User makes request** (clicks link, submits form)
2. **URL routing** determines which view handles the request
3. **View** processes the request, may interact with models
4. **Model** interacts with database if needed
5. **Template** renders HTML with data
6. **Response** sent back to user

## Django vs Other Frameworks

| Framework | Language | Best For |
|-----------|----------|----------|
| **Django** | Python | Full-featured web apps, rapid development |
| **Flask** | Python | Lightweight apps, microservices |
| **Express** | JavaScript | Node.js applications |
| **Rails** | Ruby | Rapid prototyping |

## Prerequisites

Before learning Django, you should know:

- **Python Basics:** Variables, functions, classes, modules
- **HTML/CSS:** Basic web page structure
- **SQL Basics:** Understanding databases (helpful but not required)

!!! tip "Python Knowledge Required"
    Django is built on Python. Make sure you're comfortable with Python fundamentals before diving into Django.

## Installing Django

### Using pip

```bash
pip install django
```

### Using pip with virtual environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install Django
pip install django
```

### Verify Installation

```bash
python -m django --version
```

Should display Django version (e.g., `4.2.7`).

## Your First Django Project

### Create Project

```bash
django-admin startproject myproject
```

This creates:
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

### Run Development Server

```bash
cd myproject
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your browser. You should see the Django welcome page!

### Create App

Django projects contain apps. Create your first app:

```bash
python manage.py startapp myapp
```

This creates:
```
myapp/
    __init__.py
    admin.py
    apps.py
    models.py
    tests.py
    views.py
    migrations/
```

## Django Project Structure

### Project vs App

- **Project:** The entire website/application
- **App:** A feature or component of the project

A project can contain multiple apps. For example:
- `blog` app (for blog posts)
- `users` app (for user accounts)
- `shop` app (for e-commerce)

### Key Files

**manage.py:**
- Command-line utility for Django
- Used to run commands like `runserver`, `migrate`, etc.

**settings.py:**
- Configuration for your Django project
- Database settings, installed apps, middleware, etc.

**urls.py:**
- URL routing configuration
- Maps URLs to views

**views.py:**
- Contains view functions/classes
- Handles requests and returns responses

**models.py:**
- Defines data models
- Database schema

**admin.py:**
- Configuration for Django admin interface

## Django Philosophy

### DRY (Don't Repeat Yourself)

Write code once, reuse it everywhere. Django helps you avoid repetition.

### Explicit is Better Than Implicit

Django makes things obvious. You can see what's happening.

### Loose Coupling

Components are independent. Change one without breaking others.

### Fast Development

Get working applications quickly, then optimize.

## Django Features

### Admin Interface

Automatic admin interface for managing your data:

```python
# admin.py
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

### ORM (Object-Relational Mapping)

Work with databases using Python instead of SQL:

```python
# Instead of SQL:
# SELECT * FROM posts WHERE author = 'John'

# Django ORM:
Post.objects.filter(author='John')
```

### URL Routing

Clean, readable URLs:

```python
# urls.py
path('posts/<int:post_id>/', views.post_detail)
# Matches: /posts/123/
```

### Template System

Powerful templating with inheritance:

```django
{% extends "base.html" %}
{% block content %}
    <h1>{{ post.title }}</h1>
{% endblock %}
```

### Security Features

- Protection against SQL injection
- Cross-site scripting (XSS) protection
- Cross-site request forgery (CSRF) protection
- Clickjacking protection

## Development Workflow

1. **Create Project:** `django-admin startproject myproject`
2. **Create App:** `python manage.py startapp myapp`
3. **Define Models:** Create data models in `models.py`
4. **Create Migrations:** `python manage.py makemigrations`
5. **Apply Migrations:** `python manage.py migrate`
6. **Create Views:** Write view functions in `views.py`
7. **Configure URLs:** Map URLs to views in `urls.py`
8. **Create Templates:** Write HTML templates
9. **Test:** Run development server and test
10. **Deploy:** Deploy to production server

## Best Practices

1. **Use Virtual Environments:** Isolate project dependencies
2. **Follow Naming Conventions:** Use lowercase with underscores
3. **Keep Apps Focused:** Each app should do one thing well
4. **Use Migrations:** Never edit database directly
5. **Write Tests:** Test your code
6. **Read Documentation:** Django has excellent docs
7. **Follow Security Guidelines:** Keep Django updated

## Common Mistakes

### 1. Not Using Virtual Environment

```bash
# ❌ Wrong - installs globally
pip install django

# ✅ Correct - isolated environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install django
```

### 2. Forgetting to Run Migrations

```bash
# ❌ Wrong - models won't be in database
python manage.py makemigrations
# Forgot to run migrate!

# ✅ Correct
python manage.py makemigrations
python manage.py migrate
```

### 3. Not Registering Apps

```python
# ❌ Wrong - app not in INSTALLED_APPS
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    # 'myapp',  # Missing!
]

# ✅ Correct
INSTALLED_APPS = [
    'django.contrib.admin',
    'myapp',  # Added!
]
```

## Resources

- [Django Official Documentation](https://docs.djangoproject.com/) - Comprehensive Django docs
- [Django Tutorial](https://docs.djangoproject.com/en/stable/intro/tutorial01/) - Official tutorial
- [Django for Beginners](https://djangoforbeginners.com/) - Book and resources
- [Django Girls Tutorial](https://tutorial.djangogirls.org/) - Beginner-friendly tutorial

## What's Next?

In the following tutorials, you'll learn:

1. **Setting Up Django** - Installation, project setup, and configuration
2. **Models and Databases** - Creating data models and working with databases
3. **Views and URLs** - Handling requests and routing URLs
4. **Templates** - Creating dynamic HTML pages
5. **Forms** - Handling user input and form validation
6. **Admin Interface** - Using Django's built-in admin panel

!!! success "You're Ready!"
    You now understand what Django is and why it's powerful. Let's start building web applications!

---

**Next Tutorial:** [Setting Up Django](02_setup.md)

