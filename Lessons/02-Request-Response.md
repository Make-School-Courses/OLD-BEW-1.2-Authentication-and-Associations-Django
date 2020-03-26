# Day 2: Request-Response

## Agenda

1. Tutorial Review
1. Request/Response Practice
1. BREAK
1. Tutorial Time
1. Wrap-Up
1. Resources & Credits

## Learning Objectives

By the end of this class, you will be able to...

1. Create a Django project, from scratch, containing 

## Tutorial Review (50 Minutes)

Submit your Tutorial Part 1 using [Gradescope](https://gradescope.com).

Review the first portion of the Django tutorial together.

As we review, be sure to compare/contrast Django syntax with what you've seen before in Flask.

### Practice - I Do, We Do, You Do

Close your laptops and watch as the instructor starts a new project using the techniques from the tutorial.

Then, tell the instructor what to do to accomplish the same task.

### Activity: Request/Response Practice

On your own, complete the following:

1. Create a project called 'music_site' that contains an app called 'music'.
1. Re-route _all_ web requests (hint: use the empty string `''`) to your music app's URLs file. Then, send any web requests for the homepage `''` to a view called `home`.
1. Create a view function `home` that returns an HttpResponse with the text "Hello World! You're at the Music App home page."

## Break

## Django Request/Response

Django heavily utilizes what we would call **separation of concerns**. That means that pieces of code that have different responsibilities are put in different places.

In Flask, we wrote routes that look like this:

```py
@app.route('/about-me')
def about():
  return "<p>Hello! This is an about page!</p>"
```

- The first line of code above is the **URL configuration**. It tells the server that when the user visits the url `/about-me`, it should run the `about` function and return its result as a response.
- The second and third lines of code are the **view**. It describes the function that is referenced by the URL configuration.

In Django, these two separate concerns would be placed in two separate files, `urls.py` and `views.py`:

```py
# urls.py
from django.urls import path
from . import views

urlpatterns = [
  path('about-me/', views.about)
]
```

There are a few things you'll notice about this code:

1. We are importing and using a function called `path` that constructs the URL. `path` takes two arguments: The first is the **URL**, which always should end in a `/`. This is what the user would type into their browser. The second is the **view function** that should be run for this URL.
1. Because our views are located in a separate file, we need to import them. `from . import views` means "Look in the same folder as urls.py, find a file called views, and import its contents."
1. We are creating an **array of URL configurations** called `urlpatterns`. This name must match exactly, or Django won't be able to find it.

```py
from django.http import HttpResponse

def about():
  return HttpResponse('<p>Hello! This is an about page!</p>)
```

Here, you'll notice that we can't just return a regular string. We need to first wrap it in an `HttpResponse` so that it can be parsed as HTML.

### What about templates?

What's that? You want to display your HTML in a template, you say? Say no more!

<!-- NOTE: add section on render -->

## Tutorial Time (50 Minutes)

Continue to work on the Tutorial Part 2 (Models).

## Wrap-Up

Finish Tutorial Part 2 (Models) before the next class session.

## Resources & Credits

1. [Django: Writing Views](https://docs.djangoproject.com/en/3.0/topics/http/views/)
1. [Django: URL Dispatcher](https://docs.djangoproject.com/en/3.0/topics/http/urls/)