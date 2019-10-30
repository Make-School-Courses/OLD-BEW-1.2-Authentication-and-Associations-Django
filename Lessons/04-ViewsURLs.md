# 📜 Day 4: Views & URLs

### ⏱ Agenda

1. [🏆 [5m] Learning Objectives](#%f0%9f%8f%86-5m-learning-objectives)
2. [📖 Overview](#%f0%9f%93%96-overview)
3. [📝 [10m] In Class Activity: Getting to Know Views](#%f0%9f%93%9d-10m-in-class-activity-getting-to-know-views)
4. [🌴 [10m] BREAK](#%f0%9f%8c%b4-10m-break)
5. [💻 [30m] In Class Activity: Let's Make A Website!](#%f0%9f%92%bb-30m-in-class-activity-lets-make-a-website)
6. [🌃 After Class](#%f0%9f%8c%83-after-class)
7. [📚 Resources & Credits](#%f0%9f%93%9a-resources--credits)

## 🏆 [5m] Learning Objectives

1. Identify and describe the difference between class-based views and function-based views in Django.

## 📖 Overview

### Views

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

##### URLs

```python
from django.conf.urls import url

# This syntax imports all of the functions and classes
# inside the views.py in the same folder.
from . import views

urlpatterns = [
    url(r'^now/$', views.show_time_time),
]
```

#### Class-Based Views

We could do the same with class-based views.

This means we'll have to modify, or *refactor*, the code to support this:

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

##### URLs

In `urls.py`, we'll need to modify our existing `urlpattern` slightly and change how we reference this new, class-based view:

```python
from django.conf.urls import url

from . import views

urlpatterns = [
    # Change how we reference the new view.
    url(r'^now/$', views.ShowTimeView.as_view()),
]
```

## 📝 [10m] In Class Activity: Getting to Know Views

Pair up, and **write down the answers** to the following challenges:

1. When is it a good idea to use a **function-based view**?
2. When would it be better to use a **class-based view**?

We will discuss the answers together as a group when we return from break!

## 🌴 [10m] BREAK

## 💻 [30m] In Class Activity: Let's Make A Website!

For these challenges, use `views.py` in the `clubs_app` app we created last class period.

### Challenges

1. Create a **function-based view** that returns a `Hello, World!` message as a string.
2. Create a **function-based view** that returns an HTML template that does the same.

### Stretch Challenges

1. Create a **class-based view** that returns a `Hello, World!` message as a string.
2. Import the `Event` model we created during our last class. Use it to show a list of `Event`s using a class-based view and an HTML template.

## 🌃 After Class

## 📚 Resources & Credits

1. [YouTube: Intro to Class-Based Views in Django](https://www.youtube.com/watch?v=-tqhhT3R6VY)
2. [YouTube: Deep Dive - Class-Based Views](https://youtu.be/Qki2m5AyfWw)
3. [Class-Based Views: Advanced Django Training](https://django-advanced-training.readthedocs.io/en/latest/features/class-based-views/)
