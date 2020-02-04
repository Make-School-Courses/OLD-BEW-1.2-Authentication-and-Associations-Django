# 📜 Day 4: Views & URLs

### ⏱ Agenda

1. 🏆 [5m] Learning Objectives
1. 📝 [15m] Review: Many-to-Many Relationships
1. 📖 [30m] Overview
1. 🌴 [10m] BREAK
1. 📝 [20m] From Function-based to Class-based Views
1. 💻 [30m] In Class Activity: Read the Source Code
1. 📚 Resources & Credits

## 🏆 [5m] Learning Objectives

1. Identify and describe the difference between class-based views and function-based views in Django.
2. Recognize the role of URLs in the Django framework.
3. Apply class-based views, function-based views, and urlpatterns in a series of challenges and stretch challenges.

## 📝 [15m] Review: Many-to-Many Relationships

Choose a partner you haven't worked with yet (or join a group of 3).

On the whiteboard, complete the code for the following models for a LinkedIn-like site that tracks work experience. Keep in mind that the `WorkExperience` class will represent the "through" relationship.

```js
from django.db import models

class Employee(models.Model):
  ...

class Company(models.Model):
  ...

class WorkExperience(models.Model):
  ...
```

Go over the solution together as a class.

## 📖 [30m] Overview

### Views

In Django, **views** represent the **controller** layer of the Model-View-Controller pattern. This means **views** are required to do two things:

1. They must accept an `HttpRequest` object as its first argument.
2. They must return an `HttpResponse` object (or raise an exception).

#### Function-Based Views

Let's begin by checking out this approachable, function-based view that returns the current date and time.

```python
from datetime import datetime
from django.http import HttpResponse

def show_the_time(request):
    now = datetime.now()
    html = "<html><body>It is now {}</body></html>".format(now)
    return HttpResponse(html)
```

##### Advantages of Function-Based Views

- Simple to implement
- Easy to read
- Straightforward
- Good for one-off or specialized functionality

##### Disadvantages of Function-Based Views

- Hard to extend and reuse the code
- Handling of HTTP methods (`GET`, `POST`) with if/else statements

#### Class-Based Views

At their core, CBVs are Python classes. Django ships with a variety of “template” CBVs that have pre-configured functionality that you can reuse and oftentimes extend. These classes are then given helpful names that describe what kind of functionality they provide. You’ll often see these referred to as “generic views” because they provide solutions to common requirements.

This means, to use class-based views, we'll have to modify, or *refactor*, the code to support this:

```python
from datetime import datetime
from django.http import HttpResponse
from django.views import View  # Import the View parent class

class ShowTimeView(View):  # Create a view class

    # Change the function-based view to be called get and add the self param
    def get(self, request):
        now = datetime.now()
        html = "<html><body>It is now {}</body></html>".format(now)
        return HttpResponse(html)
```

##### Advantages of Class-Based Views

- **Code Reuse**: In CBV, a view class can be inherited by another view class and modified for a different use case.
- **DRY** — Using CBVs help to reduce code duplication.
- **Code Extendability**: Can be extended to include more functionalities
- **Code Structure**: In CBVs A class based view helps you respond to different http request with different class instance methods instead of conditional statements inside a single function based view.

##### Disadvantages of Class-Based Views

- Harder to read
- Require extra imports

#### When Should I Use Each?

Class-based views provide an **alternative way to implement views as Python objects instead of functions**. They do not replace function-based views, but have certain differences and advantages when compared to function-based views.

## 🌴 [10m] BREAK

## 📝 [25m] TT: Read the Source Code

Watch as your instructor goes over the [documentation](https://docs.djangoproject.com/en/3.0/ref/class-based-views/base/#view) and [source code](https://github.com/django/django/blob/master/django/views/generic/base.py) for Django's `View` class. Then, practice using the View class to refactor existing function-based views.

## 💻 [25m] In Class Activity: Read the Source Code

With a partner, choose one of the following View classes:

  - [ListView](https://docs.djangoproject.com/en/2.2/ref/class-based-views/generic-display/#listview) - [Source Code](https://github.com/django/django/blob/master/django/views/generic/list.py)
  - [DetailView](https://docs.djangoproject.com/en/2.2/ref/class-based-views/generic-display/#detailview) - [Source Code](https://github.com/django/django/blob/master/django/views/generic/detail.py)
  - [TemplateView](https://docs.djangoproject.com/en/2.2/ref/class-based-views/base/#templateview) - [Source Code](https://github.com/django/django/blob/master/django/views/generic/base.py)

Read the documentation _and_ the source code, then use what you learned to create a page for your music site.

You will present your sample code to the class at the end of the activity.

## Lab Time

Begin working on the [MakeWiki V1 Challenges](https://github.com/Make-School-Labs/makewiki-v1) (due in 1 week). 

## 📚 Resources & Credits

1. [Medium: Django Class-Based Views vs Function-Based Views](https://medium.com/@ksarthak4ever/django-class-based-views-vs-function-based-view-e74b47b2e41b)
2. [YouTube: Intro to Class-Based Views in Django](https://www.youtube.com/watch?v=-tqhhT3R6VY)
3. [YouTube: Deep Dive - Class-Based Views](https://youtu.be/Qki2m5AyfWw)
4. [Class-Based Views: Advanced Django Training](https://django-advanced-training.readthedocs.io/en/latest/features/class-based-views/)
5. [Built-in class-based views API](https://docs.djangoproject.com/en/2.2/ref/class-based-views/)
