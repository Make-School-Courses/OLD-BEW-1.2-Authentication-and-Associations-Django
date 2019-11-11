<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: data-background="./../Slides/images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# 📜 Day 7: Authentication & Authorization

<p align="center"><a href="https://make-school-courses.github.io/REPO_NAME/Slides/00-LESSON_NAME" title="Slides" target="_blank"><strong>Slides</strong></a></p>

<!-- > -->

### ⏱ Agenda

1. [[**00m**] 🏆 Objectives](#00m-%f0%9f%8f%86-objectives)
2. [[**20m**] 📖 Overview: Authentication & Authorization](#20m-%f0%9f%93%96-overview-authentication--authorization)
3. [[**10m**] 🌴 BREAK](#10m-%f0%9f%8c%b4-break)
4. [[**45m**] 💻 Activity: v2 Challenges - Authentication](#45m-%f0%9f%92%bb-activity-v2-challenges---authentication)
5. [🌃 After Class](#%f0%9f%8c%83-after-class)
6. [📚 Resources & Credits](#%f0%9f%93%9a-resources--credits)

<!-- > -->

## [**00m**] 🏆 Objectives

|   Level   | Verbs |
| --------- | ----- |
| 6: Create | design, formulate, build, invent, create, compose, generate, derive, modify, develop |
| 5: Evaluate | choose, support, relate, determine, defend, compare, contrast, justify, support, convince, select |
| 4: Analyze | classify, break down, categorize, analyze, diagram, illustrate, criticize, simplify, associate |
| 3: Apply | calculate, predict, apply, solve, illustrate, use, demonstrate, determine, model, perform, present |
| 2: Understand | describe, explain, paraphrase, restate, summarize, contrast, interpret, discuss |
| 1: Remember | list, recite, outline, define, name, match, quote, recall, identify, label, recognize |

<!-- > -->

## [**20m**] 📖 Overview: Authentication & Authorization

### User Creation

#### Users

Created in the Python shell, in the `/admin` interface, or through your own `signup` view!

```python
from django.contrib.auth.models import User


user = User.objects.create_user('john', 'lennon@thebeatles.com', 'johnpassword')

# At this point, user is a User object that has already been saved to the database.
# You can continue to change its attributes if you want to change other fields.
user.last_name = 'Lennon'
user.save()
```

#### Superusers

Always created on the command line:

```bash
python manage.py createsuperuser --username=joe --email=joe@example.com
```

### User Authorization

In Django, superusers have access to the `/admin` interface, whereas regular users do not. This is an example of **authorization**: `TODO` define

### User Authentication

We can authenticate a user through our own **`login` view**:

```python
from django.contrib.auth import authenticate, login

def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(request, username=username, password=password)
    if user is not None:
        login(request, user)
        # Redirect to a success page.
    else:
        # Return an 'invalid login' error message.
```

For **views that only logged in users can see**, decorate the view function with `@login_required`:

```python
from django.contrib.auth.decorators import login_required

@login_required
def my_view(request):
    ...
```

To **log the user out** via a view, call the `logout` function, then redirect to a page that lets the user know they've successfully logged out:

```python
from django.contrib.auth import logout

def logout_view(request):
    logout(request)
    # Redirect to a success page.
```

### Enabling Default Login, Signup, and Logout Views

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

#### Step 1: Sign Up

#### Step 2: Log In

#### Step 3: Log Out

## [**10m**] 🌴 BREAK

## [**45m**] 💻 Activity: v2 Challenges - Authentication

<!-- > -->

## 🌃 After Class

- Complete v2 Challenges by next class period.

<!-- > -->

## 📚 Resources & Credits

- `TODO`: Link to Jasmine's authentication blog posted recently on Slack

<!-- > -->
