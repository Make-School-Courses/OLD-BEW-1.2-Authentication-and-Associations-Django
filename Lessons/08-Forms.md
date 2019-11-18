<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: data-background="./../Slides/images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# 📜 Day 8: Working with Forms

<!-- > -->

### ⏱ Agenda

1. [[**05m**] 🏆 Objectives](#05m-%f0%9f%8f%86-objectives)
2. [[**05m**] ☀️ Warm Up](#05m-%e2%98%80%ef%b8%8f-warm-up)
3. [[**30m**] 📖 Overview: Working with Forms](#30m-%f0%9f%93%96-overview-working-with-forms)
4. [[**15m**] ✓ Review: v2 Solution](#15m-%e2%9c%93-review-v2-solution)
5. [[**10m**] 🌴 BREAK](#10m-%f0%9f%8c%b4-break)
6. [[**30m**] 💻 Activity: Forms Challenges](#30m-%f0%9f%92%bb-activity-forms-challenges)
7. [🌃 After Class](#%f0%9f%8c%83-after-class)
8. [📚 Resources & Credits](#%f0%9f%93%9a-resources--credits)

<!-- > -->

## [**05m**] 🏆 Objectives

<!--
|   Level   | Verbs |
| --------- | ----- |
| 6: Create | design, formulate, build, invent, create, compose, generate, derive, modify, develop |
| 5: Evaluate | choose, support, relate, determine, defend, compare, contrast, justify, support, convince, select |
| 4: Analyze | classify, break down, categorize, analyze, diagram, illustrate, criticize, simplify, associate |
| 3: Apply | calculate, predict, apply, solve, illustrate, use, demonstrate, determine, model, perform, present |
| 2: Understand | describe, explain, paraphrase, restate, summarize, contrast, interpret, discuss |
| 1: Remember | list, recite, outline, define, name, match, quote, recall, identify, label, recognize |
-->

<!-- > -->

## [**05m**] ☀️ Warm Up

Think back to what you learned in BEW 1.1.

In your own words, write down everything you know about the following questions:

**What is a form? How do they work?**

## [**30m**] 📖 Overview: Working with Forms

### Warm Up Review: HTML Forms

In HTML, **a form is a collection of elements inside `<form>...</form>` tags** that allow a visitor to do things like enter text, select options, manipulate objects or controls, and so on, and then **send that information back to the server**.

A form must specify **two things**:

- **WHERE**: The URL to which the data corresponding to the user’s input should be returned
- **HOW**: The HTTP method the form will use to send the data to the server (`GET` or `POST`)

**EXAMPLE**: Django’s login form is returned using the `POST` method, in which the browser bundles up the form data, encodes it for transmission, sends it to the server, and then receives back its response.

### GET & POST: The Rules

- `GET` and `POST` are the only methods you can use with HTML forms.
- Typically **used for different purposes**:
    - Use **`POST` when you're going to change the state of the system**
        - **EXAMPLE**: Any request that saves data to a database
    - `GET` should be used only for requests that **do not affect the state of the system**
        - **EXAMPLE**: Searching or filtering

### Django <3's Forms

Django can **simplify and automate** vast portions of this work, and **can also do it more securely** than most programmers would be able to do in code they wrote themselves.

Django handles **three distinct parts** of the work involved in forms:

- **Preparing and restructuring data** to make it ready for rendering
- **Creating HTML forms** for the data
- **Receiving and processing submitted forms** and data from the client

**NOTE**: *It is possible to write code that does all of this manually, but Django can take care of it all for you!*

#### The Form Class

Everything starts with [Django's `Form` class](https://docs.djangoproject.com/en/2.2/ref/forms/api/#django.forms.Form).

A form class's fields directly map to different HTML `<input>` elements. Think back to what you've seen in the MakeWiki admin interface --- that's a good example of what the `Form` class can do without much effort!

#### Sample Code

Forms belong in your app's `forms.py`. You will have to create it if it doesn't exist yet!

```python
from django import forms

class FriendlyForm(forms.Form):
    first_name = forms.CharField(max_length=100)
    last_name = forms.CharField(max_length=100)
```

- **Line 1**: To use the Form class, we need to import the forms module from Django.
- **Line 2**" We create our `FriendlyForm` class, which inherits from Django’s forms.Form class.

What happens when we use a Django form? Try this in `python manage.py shell`:

```python
>>> from app.form import FriendlyForm
>>> form = FriendlyForm()
>>> print(form.as_p())
```

This will be rendered in your template when you pass the form from your view! Simply surround the output with an HTML form:

```html
<form method="POST">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="submit" value="Send the names to the server!">
</form>
```


## [**15m**] ✓ Review: v2 Solution

Review the v2 solution code with students. After reviewing the solution with students, be sure to allow some time for Q&A!

<!-- > -->

## [**10m**] 🌴 BREAK

<!-- > -->

## [**30m**] 💻 Activity: Forms Challenges

*If you get stuck, be sure to check out the Resources at the bottom of this lesson plan!*

- [ ] Add a page that allows you to create a new Post in your wiki.
- [ ] Make sure that when you submit the new Post, it saves to your database.

If you finish early, continue with your tutorial!


## 🌃 After Class

Be sure to complete today's challenges in your `v2` makewiki repo!

The instructors and TAs will be checking in on your progress this week.

<!-- > -->

## 📚 Resources & Credits

- [**Django Docs**: Working with Forms](https://docs.djangoproject.com/en/2.2/topics/forms/)
- [**Django Girls**: Forms](https://tutorial.djangogirls.org/en/django_forms/)
