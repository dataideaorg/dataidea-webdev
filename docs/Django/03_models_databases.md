# Models and Databases

Learn how to define data models and work with databases in Django using the ORM (Object-Relational Mapping).

## What are Models?

Models are Python classes that represent database tables. They define:
- What data you store
- How data is structured
- Relationships between data

Django's ORM converts Python code to SQL automatically.

## Creating Your First Model

### Basic Model

```python
# myapp/models.py
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

### Model Explanation

- `models.Model` - Base class for all Django models
- `CharField` - Text field with max length
- `TextField` - Large text field (unlimited length)
- `DateTimeField` - Date and time field
- `auto_now_add=True` - Set when created
- `auto_now=True` - Update when saved

## Common Field Types

### Text Fields

```python
# Short text
title = models.CharField(max_length=200)

# Long text
description = models.TextField()

# Email
email = models.EmailField()

# URL
website = models.URLField()
```

### Number Fields

```python
# Integer
age = models.IntegerField()

# Decimal
price = models.DecimalField(max_digits=10, decimal_places=2)

# Float
rating = models.FloatField()

# Boolean
is_published = models.BooleanField(default=False)
```

### Date/Time Fields

```python
# Date only
birth_date = models.DateField()

# Time only
start_time = models.TimeField()

# Date and time
created_at = models.DateTimeField(auto_now_add=True)
updated_at = models.DateTimeField(auto_now=True)
```

### Choice Fields

```python
STATUS_CHOICES = [
    ('draft', 'Draft'),
    ('published', 'Published'),
    ('archived', 'Archived'),
]

status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='draft')
```

## Model Options

### Field Options

```python
class Post(models.Model):
    title = models.CharField(
        max_length=200,
        null=False,           # Can't be NULL in database
        blank=False,          # Required in forms
        default='',           # Default value
        unique=True,          # Must be unique
        help_text='Post title' # Help text for forms
    )
```

### Model Meta Options

```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)
    
    class Meta:
        ordering = ['-created_at']  # Order by newest first
        verbose_name = 'Blog Post'   # Human-readable name
        verbose_name_plural = 'Blog Posts'
```

## Model Methods

### __str__ Method

Define how model is displayed:

```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    
    def __str__(self):
        return self.title
```

### Custom Methods

```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    
    def get_excerpt(self, length=100):
        return self.content[:length] + '...' if len(self.content) > length else self.content
    
    def is_recent(self):
        from django.utils import timezone
        return (timezone.now() - self.created_at).days < 7
```

## Relationships

### ForeignKey (Many-to-One)

One model references another:

```python
class Author(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()

class Post(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

### ManyToManyField

Many-to-many relationship:

```python
class Tag(models.Model):
    name = models.CharField(max_length=50)

class Post(models.Model):
    title = models.CharField(max_length=200)
    tags = models.ManyToManyField(Tag)
```

### OneToOneField

One-to-one relationship:

```python
class User(models.Model):
    username = models.CharField(max_length=100)

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio = models.TextField()
```

## Migrations

Migrations are Django's way of applying model changes to the database.

### Create Migrations

After creating or modifying models:

```bash
python manage.py makemigrations
```

This creates migration files in `migrations/` folder.

### Apply Migrations

```bash
python manage.py migrate
```

This applies migrations to the database.

### Migration Workflow

1. Modify `models.py`
2. Run `makemigrations`
3. Run `migrate`
4. Repeat as needed

## Working with Models

### Creating Objects

```python
from myapp.models import Post

# Method 1: Create and save
post = Post(title='My First Post', content='Hello, World!')
post.save()

# Method 2: Create directly
post = Post.objects.create(
    title='My First Post',
    content='Hello, World!'
)
```

### Retrieving Objects

```python
# Get all posts
all_posts = Post.objects.all()

# Get one post
post = Post.objects.get(id=1)

# Filter posts
published_posts = Post.objects.filter(status='published')

# Get first/last
first_post = Post.objects.first()
last_post = Post.objects.last()
```

### Updating Objects

```python
# Get post
post = Post.objects.get(id=1)

# Update
post.title = 'Updated Title'
post.save()

# Or update directly
Post.objects.filter(id=1).update(title='Updated Title')
```

### Deleting Objects

```python
# Delete one
post = Post.objects.get(id=1)
post.delete()

# Delete multiple
Post.objects.filter(status='draft').delete()
```

## Querying the Database

### Filtering

```python
# Exact match
Post.objects.filter(title='My Post')

# Case-insensitive
Post.objects.filter(title__iexact='my post')

# Contains
Post.objects.filter(title__contains='Django')

# Greater than / Less than
Post.objects.filter(created_at__gte=datetime.now())

# In list
Post.objects.filter(status__in=['published', 'draft'])
```

### Excluding

```python
# Exclude
Post.objects.exclude(status='draft')
```

### Ordering

```python
# Order by
Post.objects.all().order_by('-created_at')  # Newest first
Post.objects.all().order_by('title')        # Alphabetical
```

### Limiting

```python
# First 5
Post.objects.all()[:5]

# Skip first 5, get next 5
Post.objects.all()[5:10]
```

## Registering Models in Admin

Make models manageable in Django admin:

```python
# myapp/admin.py
from django.contrib import admin
from .models import Post, Author

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'created_at']
    list_filter = ['created_at', 'status']
    search_fields = ['title', 'content']

admin.site.register(Author)
```

## Complete Example

### Models

```python
# myapp/models.py
from django.db import models
from django.contrib.auth.models import User

class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)
    
    def __str__(self):
        return self.name

class Post(models.Model):
    STATUS_CHOICES = [
        ('draft', 'Draft'),
        ('published', 'Published'),
    ]
    
    title = models.CharField(max_length=200)
    slug = models.SlugField(unique=True)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    category = models.ForeignKey(Category, on_delete=models.SET_NULL, null=True)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='draft')
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    class Meta:
        ordering = ['-created_at']
    
    def __str__(self):
        return self.title
    
    def get_excerpt(self, length=150):
        return self.content[:length] + '...' if len(self.content) > length else self.content
```

### Admin Configuration

```python
# myapp/admin.py
from django.contrib import admin
from .models import Post, Category

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'category', 'status', 'created_at']
    list_filter = ['status', 'created_at', 'category']
    search_fields = ['title', 'content']
    prepopulated_fields = {'slug': ('title',)}

@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display = ['name', 'slug']
    prepopulated_fields = {'slug': ('name',)}
```

## Best Practices

1. **Use descriptive field names:** `created_at` not `date`
2. **Set appropriate max_length:** Don't use unnecessarily large values
3. **Use choices for limited options:** Better than free text
4. **Add __str__ methods:** Makes admin and shell more readable
5. **Use migrations:** Never edit database directly
6. **Index frequently queried fields:** For performance

## Common Mistakes

### 1. Forgetting to Run Migrations

```bash
# ❌ Wrong
# Changed models.py but didn't run makemigrations

# ✅ Correct
python manage.py makemigrations
python manage.py migrate
```

### 2. Not Adding __str__ Method

```python
# ❌ Wrong
class Post(models.Model):
    title = models.CharField(max_length=200)
    # No __str__ method

# ✅ Correct
class Post(models.Model):
    title = models.CharField(max_length=200)
    
    def __str__(self):
        return self.title
```

### 3. Wrong on_delete Option

```python
# ❌ Wrong - might cause errors
author = models.ForeignKey(Author, on_delete=models.DO_NOTHING)

# ✅ Correct
author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

## Practice Exercise

Create models for a blog:

1. `Category` model with name and slug
2. `Post` model with title, content, author, category, status, and timestamps
3. Add `__str__` methods to both
4. Create and run migrations
5. Register models in admin
6. Create some sample data in Django shell

## What's Next?

Now that you understand models, learn to:

- **Create Views** - Display data to users
- **Build Templates** - Create HTML pages
- **Handle URLs** - Route requests to views
- **Work with Forms** - Process user input

---

**Previous Tutorial:** [Setting Up Django](02_setup.md)  
**Next Tutorial:** [Views and URLs](04_views_urls.md)

