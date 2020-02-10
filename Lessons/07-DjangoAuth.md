<!-- .slide: data-background="./../Slides/images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# 📜 Day 7: Authentication & Authorization

<!-- <p align="center"><a href="https://make-school-courses.github.io/REPO_NAME/Slides/00-LESSON_NAME" title="Slides" target="_blank"><strong>Slides</strong></a></p> -->

<!-- > -->

### ⏱ Agenda

1. [[**02m**] 🏆 Objectives](#02m-%f0%9f%8f%86-objectives)
2. [[**15m**] 📖 Overview: Login & Logout](#15m-%f0%9f%93%96-overview-login--logout)
3. [[**30m**] 💻 Activity: v2 Challenges - Login & Logout](#30m-%f0%9f%92%bb-activity-v2-challenges---login--logout)
4. [[**10m**] 🌴 BREAK](#10m-%f0%9f%8c%b4-break)
5. [[**15m**] 📖 Overview: Signup](#15m-%f0%9f%93%96-overview-signup)
6. [[**30m**] 💻 Activity: v2 Challenges - Signup](#30m-%f0%9f%92%bb-activity-v2-challenges---signup)
7. [🌃 After Class](#%f0%9f%8c%83-after-class)
8. [📚 Resources & Credits](#%f0%9f%93%9a-resources--credits)

<!-- > -->

## [**02m**] 🏆 Objectives

1. Define authentication and authorization and discuss examples of each.
1. Apply authentication to an existing codebase.

<!-- > -->

## [**15m**] 📖 Overview: Login & Logout

### Authentication vs. Authorization

In Django, superusers have access to the `/admin` interface, whereas regular users do not. This is an example of **authentication** and **authorization**:

- All users can attempt to **log in** (*authentication*)
- But only superusers **have access to** the administrative interface (*authorization*)

### Think / Pair / Share: Brainstorm Analogies

Spend 5 minutes coming up with one or two real-world analogies for authentication and authorization. Discuss and choose your favorite analogy.

We will share these analogies together shortly.

### Enabling User Authentication in Django

In your project's root URLconf, add the following to the provided `urlpatterns` list:

```python
path('accounts/', include('django.contrib.auth.urls')),
```

This will enable the following URL patterns:

```python
accounts/login/ [name='login']
accounts/logout/ [name='logout']
accounts/password_change/ [name='password_change']
accounts/password_change/done/ [name='password_change_done']
accounts/password_reset/ [name='password_reset']
accounts/password_reset/done/ [name='password_reset_done']
accounts/reset/<uidb64>/<token>/ [name='password_reset_confirm']
accounts/reset/done/ [name='password_reset_complete']
```

As well as the following settings in `settings.py`:

```python
DEFAULT_LOGOUT_URL = '/'
```

This will enable authentication outside the administrative interface, like you see on typical websites.

Read more about [Authentication Views in Django](https://docs.djangoproject.com/en/2.2/topics/auth/default/#module-django.contrib.auth.views).


### Login Templates

A typical `login.html` template has been included with your `makewiki` `v2` starter code. [View it on GitHub](https://make.sc/makewiki/blob/master/templates/registration/login.html).

## [**30m**] 💻 Activity: v2 Challenges - Login & Logout

1. Begin the [v2 Challenges](https://make.sc/makewiki/blob/master/CHALLENGES.md) by cloning the latest `makewiki-starter` to get the starter code for today by running the following command in the directory where you store your git repositories:

    ```bash
    git clone https://make.sc/makewiki makewiki_v2
    ```

2. Stop when you complete the first section titled [`Login & Logout`](https://make.sc/makewiki/blob/master/CHALLENGES.md#login--logout).

## [**10m**] 🌴 BREAK

<!-- > -->

## [**15m**] 📖 Overview: Signup

We can log users in and out, but how do they sign up? We'll have to implement that functionality with our own view.

User-related functionality --- creation during signup, viewing or editing a user profile, etc. ---  is typically kept in an `accounts` app.

### Signup Views

Here's the `views.py` that handles the following workflow:

- Allow user to choose `username` and `password`, then confirm the password.
- Saves the user based on the submitted form data.
- Redirects the user to the homepage if successful, or shows an error that tells the user what went wrong.

**IMPORTANT**: Signing up **does not authenticate** the user! Be sure to redirect the user to the login page after signing up.

```python
from django.contrib.auth.forms import UserCreationForm
from django.urls import reverse_lazy
from django.views.generic import CreateView


class SignUpView(CreateView):
    form_class = UserCreationForm
    success_url = reverse_lazy('login')
    template_name = 'signup.html'
```

These four lines of code do a lot!

- We’re subclassing the generic class-based view `CreateView` in our `SignUpView` class.
- We specify the use of the built-in `UserCreationForm` and a template called `signup.html`.
- We then use `reverse_lazy` to redirect the user to the login page upon successful registration. Why use `reverse_lazy` instead of `reverse`?
    - All Python class attributes, like `success_url`, are **evaluated when the class is imported**.
    - When this happens, Django hasn't finished building all the URLs for the project.
    - We use `reverse_lazy` to tell Python to reverse (or "build") the URL when a user requests it, instead of saving it when the class is imported.
    - You'll get an error like the one below if you don't use `reverse_lazy` with CBVs: `django.core.exceptions.ImproperlyConfigured: The included urlconf 'accounts.urls' does not appear to have any patterns in it. If you see valid patterns in the file then the issue is probably caused by a circular import.`

### Signup Templates

The simplest `signup.html` template looks like this:

```html
{% extends 'base.html' %}

{% block title %}Sign Up{% endblock %}

{% block content %}
  <h2>Sign up</h2>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Sign up</button>
  </form>
{% endblock %}
```

Another typical `signup.html` template has been included with your `makewiki` `v2` starter code.  [View it on GitHub](https://make.sc/makewiki/blob/master/templates/registration/signup.html).

## [**30m**] 💻 Activity: v2 Challenges - Signup

Move on to the [`Signup` section](https://make.sc/makewiki/blob/master/CHALLENGES.md#signup) of the [v2 Challenges](https://make.sc/makewiki/blob/master/CHALLENGES.md) to complete the assignment.

## 🌃 After Class

- **HOMEWORK**: Complete [v2 Challenges](https://make.sc/makewiki/blob/master/CHALLENGES.md) by next class period.
- **UP NEXT:** We'll add functionality to the green 'New Page' button in our `makewiki` project to learn more about creating and customizing Django forms!

<!-- > -->

## 📚 Resources & Credits

### Unblockers

Use these resources if you get stuck on your challenges today.

- [Django Authentication: **Login & Logout Tutorial**](https://wsvincent.com/django-user-authentication-tutorial-login-and-logout/)
- [Django Authentication: **Sign Up Tutorial**](https://wsvincent.com/django-user-authentication-tutorial-signup/)
- [Django Authentication: **Password Reset Tutorial**](https://wsvincent.com/django-user-authentication-tutorial-password-reset/)

### More Information

Learn more through the resources below.

- [**Docs**: Using the Django authentication system](https://docs.djangoproject.com/en/2.2/topics/auth/default/)
- [**Django `reverse` vs `reverse_lazy`**](http://cheng.logdown.com/posts/2015/05/25/django-reverse-vs-reverse-lazy): Blog post describing a common pitfall when implementing class-based views.
<!-- > -->
