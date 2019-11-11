<!-- .slide: data-background="./../Slides/images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# 📜 Day 7: Authentication & Authorization

<!-- <p align="center"><a href="https://make-school-courses.github.io/REPO_NAME/Slides/00-LESSON_NAME" title="Slides" target="_blank"><strong>Slides</strong></a></p> -->

<!-- > -->

### ⏱ Agenda

1. [[**00m**] 🏆 Objectives](#00m-%f0%9f%8f%86-objectives)
2. [[**15m**] 📖 Overview: Login & Logout](#15m-%f0%9f%93%96-overview-login--logout)
3. [[**30m**] 💻 Activity: v2 Challenges - Login & Logout](#30m-%f0%9f%92%bb-activity-v2-challenges---login--logout)
4. [[**10m**] 🌴 BREAK](#10m-%f0%9f%8c%b4-break)
5. [[**15m**] 📖 Overview: Signup](#15m-%f0%9f%93%96-overview-signup)
6. [[**30m**] 💻 Activity: v2 Challenges - Signup](#30m-%f0%9f%92%bb-activity-v2-challenges---signup)
7. [🌃 After Class](#%f0%9f%8c%83-after-class)

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

## [**15m**] 📖 Overview: Login & Logout

### Authentication vs. Authorization

In Django, superusers have access to the `/admin` interface, whereas regular users do not. This is an example of **authentication** and **authorization**:

- All users can attempt to **log in** (*authentication*)
- But only superusers **have access to** the administrative interface (*authorization*)

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

## [**30m**] 💻 Activity: v2 Challenges - Login & Logout

1. Begin the [v2 Challenges](https://github.com/make-school-labs/makewiki-starter/CHALLENGES.md) by cloning the latest `makewiki-starter` to get the starter code for today.!
2. Stop when you complete the first section titled `Login & Signup`.

## [**10m**] 🌴 BREAK

<!-- > -->

## [**15m**] 📖 Overview: Signup

## [**30m**] 💻 Activity: v2 Challenges - Signup

Begin the [v2 Challenges](https://github.com/make-school-labs/makewiki-starter/CHALLENGES.md) to complete the assignment.

## 🌃 After Class

- Complete [v2 Challenges](https://github.com/make-school-labs/makewiki-starter/CHALLENGES.md) by next class period.

<!-- > -->

<!-- ## 📚 Resources & Credits

- `TODO`: Link to Jasmine's authentication blog posted recently on Slack -->

<!-- > -->
