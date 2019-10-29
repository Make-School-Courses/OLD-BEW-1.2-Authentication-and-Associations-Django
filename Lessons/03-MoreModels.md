# Day 3: More Models

### Table of Contents

1. [[5m] Learning Objectives](#5m-learning-objectives)
2. [[40m] Review: Models and Filters](#40m-review-models-and-filters)
3. [[10m] BREAK](#10m-break)
4. [[45m] Activity: Creating Events](#45m-activity-creating-events)
5. [Additional Resources & Credits](#additional-resources--credits)

## [5m] Learning Objectives

1. Review models, filters, and their common usage patterns in Django.
2. Use models and filters to complete challenges and stretch challenges.

## [5m] Tips for Using the Django Documentation

In this course, we will be treating the Django documentation site ([docs.djangoproject.com](http://docs.djangoproject.com)) as our textbook. Here are some tips for using it effectively:

1. Visit the [Table of Contents](https://docs.djangoproject.com/en/2.2/contents/) page and Cmd+F for a particular topic. (**HINT:** It may be helpful to bookmark this page!)
1. Do a Google Search for a particular topic with `site:docs.djangoproject.com` included in your query.

## [40m] Review: Models and Filters

### Models Overview

- Live in `models.py`
- Describe the data that will live in your database
- Like a blueprint for your data

#### Start With A Plan

We'll start by creating a model for our clubs website, called `Event`. Let's imagine what it looks like together:

| Field Name | Field Description | Data Type |
| ---------- | ----------------- | --------- |
| `name` | Name of the event | Short Text |
| `date` | Date and time of the event | Date/Time |
| `venue` | Location of the event | Short Text |
| `manager` | Name of the person managing the event | Short Text |
| `description` | Detailed description of the event | Long Text |

#### Start your Project

We can create a new Django project with the following command:

```bash
$ django-admin startproject myclub_project
```

And create a new app with the command:

```bash
$ python manage.py startapp myclub_app
```

#### Write The Model's Code

```python
# myclub_project\events\models.py

from django.db import models

class Event(models.Model):
    name = models.CharField('Event Name', max_length=120)
    event_date = models.DateTimeField('Event Date')
    venue = models.CharField(max_length=120)
    manager = models.CharField(max_length = 60)
    description = models.TextField(blank=True)
```

1. **Question**: What command created `myclub_project`?
2. **Question**: What command created the `events` directory?

#### Models: A Line By Line Review

- ` Line 1` imports the models package from `django.db`. This line will already be in your file!
- `Line 3` is the Event class definition. Each Django model must inherit from Django’s Model class.
- `Line 4`: the `name` field is a Django `CharField`. A `CharField` is a short line of text (up to 255 characters). In this case, the `max_length` option sets the maximum length of the event name to 120 characters.
    - The `name` field also has a verbose name argument. The verbose name is used to create a human-friendly name for the model field.
    - Most model fields accept verbose name, either as the first positional argument, or as a keyword argument (`verbose_name`).
* `Line 5`. `event_date` is a Django `DateTimeField`. A `DateTimeField` records a Python `datetime` object. The `event_date` field has a single argument—the verbose name for the field. Note that I have named the field `event_date`, rather than just `date`. This is because `date` is a reserved word in Python and, while Django will let you use reserved words in field names, it’s always best not to.
* `Lines 6 & 7`: `venue` and `manager` are both Django `CharField`s. As the `max_length` argument is required on `CharField`s, they have both had their `max_length` set to limit the size of the field.
* `Line 8`: `description` is a Django `TextField`. A `TextField` is a large text container that can hold many thousands of characters (maximum depends on the database). The final option: `blank=True` —-- is set so that we can create an event without a detailed description. The default for this option is `False`; if you don’t add a description, Django will throw an error.

#### Migrate the Models

- Migrations inform the database about any changes to your models.
- You make and apply migrations when creating new models, or changing an existing model.
- Migrations can be applied by any developer on the team to ensure their local database structure is compatible with the current models.

##### Commands

1. `python manage.py makemigrations`
2. `python manage.py migrate`

#### Add Some Events Manually

Let's add a few `Event` objects manually, using the Python shell.

Calling `event1.save()` stores the object's data in the database. Later, we'll use the admin to do this!

```bash
$ python manage.py shell

>>> from events.models import Event
>>> event1 = Event(name="Test Event1", event_date="2018-12-17", venue="test venue", manager="Bob")
>>> event1.save()
```

**PROTIP**: When viewing code like this, `>>>` tells you to run the code in the Python shell. `$` means to run the command in bash --- your regular terminal.

#### Querying Events

Django allows us to retrieve all the Events we've made, or, alternatively, to filter the results to retrieve only the Events we're interested in.

**Question: What are some scenarios where Events might be filtered? Take 5 minutes to write down every situation you could think of.**

#### Filters

Perhaps we want to only see the events that are happening today --- or this weekend! Or an event that has our favorite band in it's title.

Use Django filters to enable this capability! They allow us to use a double-underscore, in conjunction with the field name, to generate results based on our unique criteria.

##### Common Filters

These common filters come in handy in nearly every project:

- `Event.objects.get(id=14)`: Return *one* `Event` with `id` `14`.
- `Event.objects.filter(name="Dungeons and Dragons")`: Return 0 to many `Event`s with the `name` `Dungeons and Dragons`.
- `Event.objects.filter(name__iexact="Kanye")`: Return Events that match `Kanye` and `kanye`.
- `Event.objects.filter(headline__contains="West")`: Return events that contain the exact string, `West`, but not `west`.

**PROTIP**: `.get()` will return 0 to one result, whereas `.filter()` can return 0 to many results.

## [10m] BREAK

## [45m] Activity: Creating Events

Create an `events` app using the walkthrough above, add data manually, then execute a few queries against it based on the suggestions below.

**Need a Hand?** Use the following resource, [Django Book: Chapter 2, Models](https://djangobook.com/mdj2-models/), to guide you in your quest!

### Challenges

1. Get an event by ID.
2. Get an event by name.
3. In the above brainstorming activity, you generated a few ideas for how you would filter events. Write the solution to those queries now!

### Stretch Challenges

1. Update one of your events by changing the `name` or `date` on which it occurs.
2. Delete one of the events.
3. Sort a list of all events by `date`, descending.

### Finish Early?

If you finish early, keep working on your Django tutorial until the end of class!

_All seven sections must be complete in order to earn credit for this class._

## Additional Resources & Credits

- [Django Tips #7: Function-Based Views vs Class-Based Views](https://wsvincent.com/class-function-based-views/)
- [Django Book: Chapter 2, Models](https://djangobook.com/mdj2-models/)
