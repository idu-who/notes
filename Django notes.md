# Django Notes

# Table of Contents


## Conda Basics
- It is recommended to install in a virtual environment like conda, which allows us to have multiple installations of the same software.
- There are 2 versions of conda: miniconda and anaconda. Miniconda is sufficient for our needs.
- On Linux it is easy to install using the bash file available through the conda website.

### Conda commands
- `conda info` - to view information about the conda installation on the system.
- `conda create --name <env_name> [python=<python_version>]` - to create a new conda virtual environment with the specified name. We can also pin the environment to a particular version of python.
- `conda env list` - to list all created conda environments.
- `conda activate <env_name>` - to use a conda environment.
- `conda install <package_name>[==<package_version>]` - to install a package in the conda environment. We can pin the package to a certain package version.
- `conda list` - to list all packages installed in the current environment.
- `conda deactivate` - to deactivate a conda environment.
- `conda remove --name <env_name> --all` - to delete an entire environment.

## Introduction to Django
- [What Django Code Looks Like](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Introduction#what_does_django_code_look_like)
- Django uses the MVT (Model View Template) architecture.

## Starting a Django Project
- `django-admin startproject <project_name>` - command to create a Django project.
- This creates the following directory:
```
<project_name>
|-- <project_name>
|   |-- __init__.py
|   |-- asgi.py
|   |-- settings.py
|   |-- urls.py
|   |__ wsgi.py
|__ manage.py
```

> **NOTE:** If we don't want to create the project inside a folder and want the inner project folder and the `manage.py` file in the current directory we can run `django-admin startproject <project_name> .`.

### Overview of modules
- `manage.py` - it is called to use various Django commands.
- `settings.py` - it is used for configuring the global settings of the project.

> **NOTE:** Even though python does not support constant variables, Django uses constant variables for storing the project settings. And whenever these settings change the Django server needs to be restarted for them to take effect.

#### `settings.py`
- `BASE_DIR`: the path of the project (folder containing `manage.py`) in the system, this allows Django to work using relative paths.
- `SECRET_KEY`: every Django project has a unique `SECRET_KEY`.
- `DEBUG`: if it is `True` Django gives in-depth error messages and logs.
- `INSTALLED_APPS`: In Django, apps are the individual components of the project. `INSTALLED_APPS` is a list of all default, user-defined and third-party apps being used in the project.
- `STATIC_URL`: The url where the static files like images, JavaScript, CSS, etc. are stored.

#### `manage.py` Commands
- `python manage.py migrate` - connects Django to the database according to the settings of the project. It also syncs a few other settings.
- `python manage.py runserver` - starts the Django development server.
- `python manage.py createsuperuser` - creates a Django admin. Go to [`http://127.0.0.1:8000/admin/`](http://127.0.0.1:8000/admin/) (or `wherever-your-django-server-is-running/admin/`) to access the admin page.
- `python manage.py startapp <app_name>` - creates a new Django app.
- Given below is the directory structure of the project after creating an app:
```
<project_name>
|-- db.sqlite3
|-- <project_name>
|   |-- __init__.py
|   |-- asgi.py
|   |-- settings.py
|   |-- urls.py
|   |__ wsgi.py
|-- <app_name>
|   |-- __init__.py
|   |-- admin.py
|   |-- apps.py
|   |-- migrations
|   |   |__ __init__.py
|   |-- models.py
|   |-- tests.py
|   |__ views.py
|__ manage.py
```
- `python manage.py makemigrations` - to make migrations based on the changes made to the models.
- `python manage.py shell` - opens an interactive python shell where you can run Django commands.

##### Structure of a Django website
- In Django, the project represents the entire website or web application. For example, if we want to make a blog site we will create a Django project for it.
- But the actual web pages of the website are represented by an app in Django. An app is a discrete part of the project. So in our example of a blog site there will be an app for the blog posts, another one for the about page and maybe one more for buying a subscription. In this case we will create a `posts` app, a `pages` app and a `payments` app.
- The general convention for naming apps is that the app name should be the plural of the app's main model. So for the `posts` app the main model will be `Post`.
- When we start a Django project there are 6 pre-existing apps that are installed. These can be seen from the `INSTALLED_APPS` list in the project's `settings.py` file. Any new app we create or any third-party apps we want to use should also be added to this list.

## Configuring Templates
- Templates can be configured through the `TEMPLATES` variable in the `settings.py` module.
- `TEMPLATES` is a list of dictionaries.
- We will add `os.path.join(BASE_DIR, "templates")` to the `DIRS` list. This lets Django know that it needs to look for a `templates` directory in the project's base directory.
- Here is what it should look like:
```python
TEMPLATES = [
{
    'BACKEND': 'django.template.backends.django.DjangoTemplates',
    'DIRS': [os.path.join(BASE_DIR, "templates"),],
    'APP_DIRS': True,
    'OPTIONS': {
        'context_processors': [
            'django.template.context_processors.debug',
            'django.template.context_processors.request',
            'django.contrib.auth.context_processors.auth',
            'django.contrib.messages.context_processors.messages',
        ],
    },
},
]
```

> **NOTE:** If the `os` module is not already imported in the `settings.py` file then import it as we need it to run the `os.path.join()` method.

> **NOTE:** If `BASE_DIR` is defined as `Path(__file__).resolve().parent.parent` in your `settings.py` file then you can write `BASE_DIR / "templates"` in place of `os.path.join(BASE_DIR, "templates")`. And thus you don't need to import the `os` module as well.

## Adding a View to the App
- The purpose of a view is to take incoming requests and handle them by returning a response.
- To add a view to an app we need to either create a function-based or class-based view in the `views.py` file of the app.
- Write the following code to create a function-based view:
```python
from django.http import HttpResponse
def homepage_view(request):
    return HttpResponse("<h1>Hello World</h1>")
```
- In the above code we have created a view know as `homepage_view`. It accepts a `request` and returns a `HttpResponse`.

> **NOTE:** In is not necessary to have a `request` argument in the view. It could be called anything. If you don't want to specify the arguments then just write `*args, **kwargs` instead.

### Using a template with function-based views
- After this we will see how to create a class-based view and use a template for it, but first let's use a template with a function-based view.
- In the `view.py` file of the app, `from django.shortcuts import render` is there by default. We will use this `render` function instead of `HttpResponse`, as it returns a `HttpResponse` rendered using a template.
- `render` requires 2 arguments - `request` and `template_name`. It also has a `context` argument which will be useful in the future for passing values to the template. So this is what the code in `views.py` should be like:
```python
from django.shortcuts import render
def homepage_view(request):
    return render(request, "index.html", {})
```
- So here the `homepage_view` will display the `index.html` template. Also we passed an empty dictionary as the `context` argument but it is not required.

## Adding a `TemplateView` to the App
- We have to add the following lines of code to the `views.py` file in the app's directory:
```python
from django.views.generic import TemplateView
class HomepageView(TemplateView):
    template_name = 'index.html'
```
- Here we have created a class `HomepageView`, which inherits from the `TemplateView` class. And we set the `template_name` to `index.html`.

## URL Routing
- In the inner project directory where the `settings.py` file is located there is another file called `urls.py`. This file defines a list `urlpatterns`.
- At this stage there is only one element in `urlpatterns`, `path('admin/', admin.site.urls)` which routes any request starting with `admin/` to `admin.site.urls`. This is for the admin page.

### Adding a URL pattern for a view
- Let's add a URL pattern for the class-based view that we created before - `HomepageView`.
- First we have to import `HomepageView` from the `views.py` file. For example, if our app's name is `homepage` then the code would be `from homepage.views import HomepageView`.
- After that add this URL pattern to the `urlpatterns` list - `path('', HomepageView.as_view(), name='home')`. Now `urls.py` should look like this:
```python
from django.contrib import admin
from django.urls import path
from homepage.views import HomepageView
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', HomepageView.as_view(), name='home'),
]
```
- So we have created a URL pattern which routes all requests matching a blank value of root (`/`) to `HomepageView.as_view()`. And we also named this route `home`.

> **NOTE:** Here `HomepageView.as_view()` generates a callable object of the `HomepageView` class. Callable objects are just like functions. So, Django passes `HttpRequest` received from the user to this callable object and it returns a `HttpResponse` which Django supplies back to the user.

## Creating a Django Template
- If we run our website right now it will give us a `TemplateDoesNotExist at /` error. Since we have wired in our view but we have not created the `index.html` template.
- We will start by making a `templates` directory in the main project folder. The directory structure of the project will look like this after creating the `templates` directory:
```
<project_name>/
|-- db.sqlite3
|-- <project_name>/
|-- <app_name>/
|-- templates/
|__ manage.py
```
- Now create a file called `index.html` inside the `templates` directory. Write the following HTML code in the file.
```html
<h1>Greetings</h1>
<p>Hello, world!</p>
```
- If we execute `python manage.py runserver` now, we will see the HTML code rendered on the web page.

## Using Templated Values
- [Documentation on Template Tags and Filters](https://docs.djangoproject.com/en/3.2/ref/templates/builtins/)
- The `index.html` file that we created only contains static HTML. To make the template dynamic we can add code to it. This can be done by enclosing the code inside double curly braces (`{{ <statement> }}`).
- Any code inside double curly braces gets evaluated by the Django template engine. We can modify `index.html` like so:
```html
<h1>Greetings</h1>
<p>Hello, world!</p>
<p>{{ my_statement }}</p>
```
- `my_statement` is not defined yet but it can be either of the following:
    1. A python expression like a string, a number or an object.
    2. A callable object of a function or a method.

### `get_context_data()` method
- We need to extend the view we created `HomepageView` with `get_context_data()` to use `my_statement`. It is a method which lets you pass variables to your templates.
- Edit the `views.py` file in the app's directory as follows:
```python
from django.views.generic import TemplateView
class HomepageView(TemplateView):
    template_name = 'index.html'
    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context["my_statement"] = "Nice to see you!"
        return context
```
- `get_context_data()` is an existing method of the `TemplateView` class that we inherited from and we don't want to completely override it so we use the `super()` method to call the `get_context_data()` method of the `TemplateView` class and store the return value in the `context` variable. Then we add a new key-value pair to the `context` dictionary and return it.

> **NOTE:** We aren't using `**kwargs` but it is required for us to pass it to the `get_context_data()` method of the super class.

> **NOTE:** From what I understand, `get_context_data()` is essentially a method called by Django to get objects from the view and define them in the template's context (scope).

### Calling view methods
- The standard way to add data to a template's context is using `get_context_data()` method but there is another way. We can call view methods from the template to achieve the same thing.
- First we'll add a method to the view:
```python
from django.views.generic import TemplateView
class HomepageView(TemplateView):
    template_name = 'index.html'
    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context["my_statement"] = "Nice to see you!"
        return context
    def say_bye(self):
        return "Goodbye"
```
- Here we added the `say_bye()` method. Now let's use this method in the template:
```html
<h1>Greetings</h1>
<p>Hello, world!</p>
<p>{{ my_statement }}</p>
<p>{{ view.say_bye }}</p>
```
- So the return value of the method will be used in-place of `view.say_bye`. Notice that we aren't using parenthesis to call the method like we usually would, this is because Django checks the template variables to see if they are callable.

> **NOTE:** In the above example `view` is defined in the templates context through the `get_context_data()` method of the `TemplateView` class. If we print the return value of this method the first element in the dictionary has the key `view` and it contains an object of the view.

## Template Inheritance
- To reduce redundant code across our templates we can use template inheritance to create a kind of super-template which can be inherited by other sub-templates.
- For example if we have home, about and contact pages and each of them need a navigation bar we can create a `base.html` file which contains the navigation bar as shown below. The name `base.html` is a Django convention.
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <title>My Site</title>
    </head>
    <body>
        <h1>Navigation Bar</h1>
        <!-- This is a placeholder block that can be replaced by the sub-templates -->
        {% block content %}
            placeholder text
        {% endblock %}
        <h1>Footer</h1>
    </body>
</html>
```
- The html code for the sub-templates should be like this:
```html
<!-- This let's Django know that the template is a sub-template of base.html -->
{% extends "base.html" %}
<!-- This will replace the content block in base.html -->
{% block content %}
    <h1>Home</h1>
{% endblock %}
```

> **NOTE:** If we don't create a content block in the sub-template then the block will be displayed as it is defined in `base.html`.

> **NOTE:** In the sub-templates any html other than what is inside the block will not be displayed.

> **NOTE:** The Django template engine does not ignore html comments.

### `include` template tag
- Another template tag which can be used to reduce redundant code is the `include` tag. This tag enables us to embed a template inside another template.
- For example, if we create a `navbar.html` which contains the html code for rendering a navbar then we can add it to `base.html` or any other template like so:
```html
<body>
    {% include "navbar.html" %}
    {% block content %}
        placeholder text
    {% endblock %}
    <h1>Footer</h1>
</body>
```
- This is very useful for organizing code in a modular manner.

## Creating a Model for an App
- [Documentation on Models](https://docs.djangoproject.com/en/3.2/topics/db/models/)
- Models are used to store data for an app. They are created in the `models.py` file of the app.
- Create a class and make it a sub-class of `models.Model` class. Now we can add model fields by creating data members in the class. For now set the data members to `models.TextField()`. The `models.py` file should look like so:
```python
class <model_name>(models.Model):
    <attribute_name1> = models.TextField();
    <attribute_name2> = models.TextField();
    <attribute_name3> = models.TextField();
```
- Model fields help us map data to the database.
- After making any changes to the model we need to run 2 commands - `python manage.py makemigrations` and `python manage.py migrate`. These commands create a migration containing the actions required to make the changes and apply the migration to the database, respectively.

> **NOTE:** Make sure that you have added your app to the `INSTALLED_APPS` list in the `setting.py` file of your project before you run `python manage.py makemigrations`, else no changes will be detected.

### Registering a model to the admin page
- To utilize the model through the admin page we have to add the following code to the `admin.py` file of the app:
```python
from .models import <model_name> # here <model_name> will be the name of the class we created above
admin.site.register(<model_name>)
```

> **NOTE:** In the code we have used a relative path, i.e, instead of writing `<app_name>.models` we have only written `.models`, this is because `admin.py` and `models.py` are in the same directory.

### Using python shell to manage a model
- Run `python manage.py shell` to open a python shell.
- Then import the models you want to use. For example, if we have an app called `products` in which we created a model called `Product`. Then we will execute such a command - `from products.models import Product`.
- `<model_name>.objects.all()` - built-in Django command which returns all objects of a model.
- `<model_name>.objects.create()` - built-in Django command to create a new object of the model.
- For example, if the `Product` model has 3 fields of the type `TextField`, such as, `product_name`, `description` and `price`. Then the command to create a new object would be like so - `Product.objects.create(product_name='Grapes', description='Fruit', price='20')`.
- So when using the `create()` method the values for the fields are passed using keyword arguments.
- `<model_name>.objects.get()` - It enables us to fetch a single object by matching some lookup parameters. But it returns a `Model.DoesNotExist` exception if there are no objects matching the parameters and a `Model.MultipleObjectsReturned` when there are multiple objects matching the parameters.
- For example, if we want to get a product whose `product_name` is 'Grapes'. Then the command would be `Product.objects.get(product_name='Grapes')`.

## Deleting a Model
- To delete a model from the app and the database we need to delete all files except the `__init__.py` file and also delete the `__pycache__` folder from the `migrations` directory of the app. Along with that if you are using SQLite database delete the `db.sqlite3` file from the project.
- To recreate new models run `python manage.py makemigrations` and `python manage.py migrate`. Also run `python manage.py createsuperuser` if you deleted the database since the details of the admin account would also have been deleted.

> **NOTE:** it is not necessary to delete a model to make changes to it, changes can be made just by creating new migrations. But when we add a field to a model which did not exist in the previous migration we will be prompted to either set a temporary default value or set a default value for the field.

## Field Types
- [Documentation on Model Fields](https://docs.djangoproject.com/en/3.2/ref/models/fields/)
- Common parameters:
    - `default` - It can be used to set a default value for the field.
    - `blank` - It takes a `Boolean` value which specifies if the field is required. It is not related with the database.
    - `null` - It takes a `Boolean` value which specifies if the database can store a `null` value for the field.
- `TextField()` - It is a field to take a text input of any length.
- `CharField()` - It is a field to take a limited number of characters as an input.
    - `max_length` - It is used to set the maximum number of characters that can be accepted. It is compulsory to set `max_length` for a `CharField`.
- `DecimalField()` - It is a field to store a value using the `Decimal` class in python.
    - `max_digits` - It is a required field. It sets the total number of digits (including integer and decimal part) that is considered valid.
    - `decimal_places` - It is a required field as well. It is used for specifying the number of digits in the decimal part of the number.

## Rendering Data in a View through a Model
- In our `products` app we have created the following model in the `models.py` file:
```python
class Product(models.Model):
    product_name = models.CharField(max_length=20)
    description = models.TextField(blank=True, null=True)
    price = models.DecimalField(max_digits=5, decimal_places=2)
```
- Now let's make a view which passes the data to a template, so our `views.py` will contain this code:
```python
from .models import Product
def product_detail_view(request):
    prod = Product.objects.get(id=1)
    context = {
        'prod': prod,
    }
    return render(request, "products/product_detail.html", context)
```
- In the above code we first imported the model, then we used `Product.objects.get(id=1)` to get an object of the model. Here we have used a fixed value of one, but we'll see how to avoid that later.
- After getting the object we create a context and store the object in it, then we pass the context to the template using the render function. Note that the template is in the sub-directory `products`.
- So in the `templates` directory of our project create a sub-directory called `products` and create the template `product_detail.html` like so:
```html
{% extends "base.html" %}
{% block content %}
    <table>
        <tr>
            <th>Product Name</th>
            <th>Description</th>
            <th>Price</th>
        </tr>
        <tr>
            <td>{{ prod.product_name }}</td>
            <td>{{ prod.description }}</td>
            <td>{{ prod.price }}</td>
        </tr>
    </table>
{% endblock %}
```
- Now that we've done all that make sure that you have added the view to `urls.py` and go to the url to see the web page.

> **NOTE:** We use `id` to get the object even though we haven't created an `id` field in our model. This is because it is an auto-increment primary key field provided by default in Django.

> **NOTE:** It is recommended to store an app's templates inside the app's own directory in order to make it easily reusable. [Article on Django Best Practices for Template Structure](https://learndjango.com/tutorials/template-structure).

> **NOTE:** Django looks for templates in this order, first it will look through the directory defined by `DIRS` in `TEMPLATES` inside the `settings.py` file, after that if `APP_DIRS` is set to `True` (default) it will check the apps directory for the template. [Documentation on Template Overriding](https://docs.djangoproject.com/en/3.2/howto/overriding-templates/).

## Creating a Model Form
- Django provides us with built-in functionality to easily create forms from our models.
- To create a form for the same `Product` model of the `products` app that we used above, we will firstly have to create a `forms.py` file inside the app's directory. And then write this in it:
```python
from django import forms
from .models import Product
class ProductForm(forms.ModelForm): # possible form names: ProductForm, ProductModelForm, ProductCreateForm
    class Meta:
        model = Product
        fields = [
            'product_name',
            'description',
            'price',
        ]
```
- Once that is done we will make a view which uses this form, so add the following lines of code to the `views.py` file:
```python
from .forms import ProductForm
def product_create_view(request):
    form = ProductForm(request.POST or None)
    if form.is_valid():
        form.save()
        form = ProductForm() # To clear the fields after saving the details entered in the fields
    context = {
        'form': form,
    }
    return render(request, "products/product_create.html", context)
```
- Above we have utilized `request.POST` that belongs to the `request.QueryDict` class which is a specialized dictionary used to represent query strings in Django. Since it is an iterable object, when we use it with the logical `or` it is type coerced to a boolean value. So, when `request.POST` is empty it gets interpreted as `False` and the `or` will return `None`. Whereas when `request.POST` is not empty it gets interpreted as `True` and the `or` will return the `request.POST` object.
- We have mentioned the template `product_create.html` in the view, so we'll now make a new template in the `products` sub-directory using that name. And write this in it:
```html
{% extends "base.html" %}
{% block content %}
<!-- the method attribute is used to specify what method to use when sending the form as a request to the server and I have no clue what csrf_token is but just use it for now -->
<form method="POST"> {% csrf_token %}
    <!-- form.as_p renders the form fields using p tags -->
    {{ form.as_p }}
    <input type="submit" value="Save">
</form>
{% endblock %}
```
- Then add the view to `urls.py` and create a new product, you can view the created product from the admin page.

## Admin Customization

### Customizing `User` model
- Open the `admin.py` file in your apps directory. By default the Django admin comes with 2 models already registered, they are, `User` and `Groups`.
- We have to unregister the default `User` model using `admin.site.unregister(User)`. Then we can create our own `UserAdmin`.
- But we will import `UserAdmin` from `django.contrilb.auth.admin` and inherit it into our custom `UserAdmin` class.

### Adding a custom input field
