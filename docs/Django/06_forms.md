# Forms

Learn how to create and handle forms in Django to collect and process user input.

## What are Forms?

Forms allow users to submit data to your Django application. Django provides:
- Form classes for validation
- Automatic HTML generation
- CSRF protection
- Easy data processing

## Creating Forms

### Basic Form

```python
# myapp/forms.py
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

### Model Forms

Create forms from models:

```python
# myapp/forms.py
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content', 'status']
```

## Form Fields

### Common Field Types

```python
class MyForm(forms.Form):
    # Text
    name = forms.CharField(max_length=100)
    
    # Email
    email = forms.EmailField()
    
    # Number
    age = forms.IntegerField()
    
    # Boolean
    agree = forms.BooleanField()
    
    # Choice
    STATUS_CHOICES = [
        ('draft', 'Draft'),
        ('published', 'Published'),
    ]
    status = forms.ChoiceField(choices=STATUS_CHOICES)
    
    # Date
    birth_date = forms.DateField()
    
    # Textarea
    message = forms.CharField(widget=forms.Textarea)
    
    # Password
    password = forms.CharField(widget=forms.PasswordInput)
```

### Field Options

```python
class MyForm(forms.Form):
    name = forms.CharField(
        max_length=100,
        required=True,              # Field is required
        label='Your Name',          # Custom label
        help_text='Enter your full name',  # Help text
        initial='John',             # Default value
        widget=forms.TextInput(attrs={'class': 'form-control'})  # HTML attributes
    )
```

## Handling Forms in Views

### GET Request (Display Form)

```python
# myapp/views.py
from django.shortcuts import render, redirect
from .forms import ContactForm

def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # Process form data
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']
            
            # Save to database, send email, etc.
            
            return redirect('success')
    else:
        form = ContactForm()
    
    return render(request, 'myapp/contact.html', {'form': form})
```

### Form Validation

```python
def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # Form is valid, process data
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            # ...
            return redirect('success')
        else:
            # Form has errors, will be displayed in template
            pass
    else:
        form = ContactForm()
    
    return render(request, 'myapp/contact.html', {'form': form})
```

## Rendering Forms in Templates

### Basic Form Rendering

```html
<!-- myapp/templates/myapp/contact.html -->
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Submit</button>
</form>
```

### Manual Form Rendering

```html
<form method="post">
    {% csrf_token %}
    
    <div>
        <label for="{{ form.name.id_for_label }}">Name:</label>
        {{ form.name }}
        {% if form.name.errors %}
            <ul class="errors">
                {% for error in form.name.errors %}
                    <li>{{ error }}</li>
                {% endfor %}
            </ul>
        {% endif %}
    </div>
    
    <div>
        <label for="{{ form.email.id_for_label }}">Email:</label>
        {{ form.email }}
        {{ form.email.errors }}
    </div>
    
    <div>
        <label for="{{ form.message.id_for_label }}">Message:</label>
        {{ form.message }}
        {{ form.message.errors }}
    </div>
    
    <button type="submit">Submit</button>
</form>
```

### Display All Errors

```html
<form method="post">
    {% csrf_token %}
    
    {% if form.non_field_errors %}
        <ul class="errors">
            {% for error in form.non_field_errors %}
                <li>{{ error }}</li>
            {% endfor %}
        </ul>
    {% endif %}
    
    {{ form.as_p }}
    <button type="submit">Submit</button>
</form>
```

## CSRF Protection

Django requires CSRF token for POST requests:

```html
<form method="post">
    {% csrf_token %}
    <!-- Form fields -->
</form>
```

The `{% csrf_token %}` tag adds a hidden field for security.

## Model Forms

Forms based on models:

### Create Model Form

```python
# myapp/forms.py
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content', 'status', 'category']
        widgets = {
            'content': forms.Textarea(attrs={'rows': 10}),
        }
```

### Using Model Form

```python
# myapp/views.py
from django.shortcuts import render, redirect, get_object_or_404
from .forms import PostForm
from .models import Post

def create_post(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.save()
            return redirect('post_detail', post_id=post.id)
    else:
        form = PostForm()
    
    return render(request, 'myapp/post_form.html', {'form': form})

def edit_post(request, post_id):
    post = get_object_or_404(Post, id=post_id)
    
    if request.method == 'POST':
        form = PostForm(request.POST, instance=post)
        if form.is_valid():
            form.save()
            return redirect('post_detail', post_id=post.id)
    else:
        form = PostForm(instance=post)
    
    return render(request, 'myapp/post_form.html', {'form': form})
```

## Custom Validation

Add custom validation to forms:

```python
# myapp/forms.py
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
    
    def clean_message(self):
        message = self.cleaned_data['message']
        if len(message) < 10:
            raise forms.ValidationError("Message must be at least 10 characters.")
        return message
    
    def clean(self):
        cleaned_data = super().clean()
        name = cleaned_data.get('name')
        email = cleaned_data.get('email')
        
        # Custom validation logic
        if name and 'test' in name.lower():
            raise forms.ValidationError("Name cannot contain 'test'.")
        
        return cleaned_data
```

## Complete Example

### Form Definition

```python
# myapp/forms.py
from django import forms
from .models import Post, Category

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content', 'category', 'status']
        widgets = {
            'title': forms.TextInput(attrs={
                'class': 'form-control',
                'placeholder': 'Enter post title'
            }),
            'content': forms.Textarea(attrs={
                'class': 'form-control',
                'rows': 10,
                'placeholder': 'Enter post content'
            }),
            'category': forms.Select(attrs={'class': 'form-control'}),
            'status': forms.Select(attrs={'class': 'form-control'}),
        }
        labels = {
            'title': 'Post Title',
            'content': 'Content',
            'category': 'Category',
            'status': 'Status',
        }
```

### View

```python
# myapp/views.py
from django.shortcuts import render, redirect, get_object_or_404
from django.contrib import messages
from .forms import PostForm
from .models import Post

def create_post(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.save()
            messages.success(request, 'Post created successfully!')
            return redirect('post_detail', post_id=post.id)
    else:
        form = PostForm()
    
    return render(request, 'myapp/post_form.html', {'form': form})

def edit_post(request, post_id):
    post = get_object_or_404(Post, id=post_id)
    
    if request.method == 'POST':
        form = PostForm(request.POST, instance=post)
        if form.is_valid():
            form.save()
            messages.success(request, 'Post updated successfully!')
            return redirect('post_detail', post_id=post.id)
    else:
        form = PostForm(instance=post)
    
    return render(request, 'myapp/post_form.html', {'form': form, 'post': post})
```

### Template

```html
<!-- myapp/templates/myapp/post_form.html -->
{% extends 'myapp/base.html' %}

{% block content %}
    <h1>{% if post %}Edit Post{% else %}Create Post{% endif %}</h1>
    
    <form method="post">
        {% csrf_token %}
        
        {% if form.errors %}
            <div class="alert alert-error">
                <ul>
                    {% for field in form %}
                        {% for error in field.errors %}
                            <li>{{ error }}</li>
                        {% endfor %}
                    {% endfor %}
                </ul>
            </div>
        {% endif %}
        
        <div class="form-group">
            <label for="{{ form.title.id_for_label }}">{{ form.title.label }}</label>
            {{ form.title }}
            {% if form.title.help_text %}
                <small>{{ form.title.help_text }}</small>
            {% endif %}
        </div>
        
        <div class="form-group">
            <label for="{{ form.content.id_for_label }}">{{ form.content.label }}</label>
            {{ form.content }}
        </div>
        
        <div class="form-group">
            <label for="{{ form.category.id_for_label }}">{{ form.category.label }}</label>
            {{ form.category }}
        </div>
        
        <div class="form-group">
            <label for="{{ form.status.id_for_label }}">{{ form.status.label }}</label>
            {{ form.status }}
        </div>
        
        <button type="submit" class="btn btn-primary">Save</button>
        <a href="{% url 'post_list' %}" class="btn btn-secondary">Cancel</a>
    </form>
{% endblock %}
```

## Best Practices

1. **Use Model Forms:** When working with models
2. **Validate on Server:** Never trust client-side validation alone
3. **Use CSRF Token:** Always include `{% csrf_token %}`
4. **Display Errors:** Show validation errors to users
5. **Use Widgets:** Customize form field appearance
6. **Clean Data:** Use `cleaned_data` after validation

## Common Mistakes

### 1. Forgetting CSRF Token

```html
<!-- ❌ Wrong -->
<form method="post">
    {{ form.as_p }}
</form>

<!-- ✅ Correct -->
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
</form>
```

### 2. Not Checking Method

```python
# ❌ Wrong
def contact(request):
    form = ContactForm(request.POST)  # Always uses POST

# ✅ Correct
def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
    else:
        form = ContactForm()
```

### 3. Not Validating Form

```python
# ❌ Wrong
def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        name = form.data['name']  # Not validated!

# ✅ Correct
def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            name = form.cleaned_data['name']  # Validated
```

## Practice Exercise

Create forms for:

1. Contact form with name, email, and message
2. Post creation form using ModelForm
3. Post editing form
4. Form validation with custom rules
5. Display form errors in template
6. Success messages after submission

## What's Next?

Congratulations! You've learned Django fundamentals. Continue with:

- **User Authentication** - Login, logout, registration
- **Admin Customization** - Customize Django admin interface
- **REST APIs** - Build APIs with Django REST Framework
- **Deployment** - Deploy your Django app to production
- **Testing** - Write tests for your application

---

**Previous Tutorial:** [Templates](05_templates.md)  
**Next Steps:** Practice building a complete Django application, or explore advanced topics!

