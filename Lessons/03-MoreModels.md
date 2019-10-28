# Day 3: More Models

### Table of Contents

1. [Learning Objectives (5 Minutes)](#learning-objectives-5-minutes)
2. [[40m] Review: Models and Filters](#40m-review-models-and-filters)
3. [[10m] BREAK](#10m-break)
4. [[30m] Activity: Creating Events](#30m-activity-creating-events)
5. [[20m] Activity: Tutorial Time](#20m-activity-tutorial-time)
6. [Additional Resources & Credits](#additional-resources--credits)

## Learning Objectives (5 Minutes)

1. Review models, filters, and their common usage patterns in Django.

## [40m] Review: Models and Filters

### Models Overview

- Live in `models.py`
- Describe the data that will live in your database
- Like a blueprint for your data

#### Start With A Plan


| Field Name | Field Description | Data Type |
| ---------- | ----------------- | --------- |
| `name` | Name of the event | Short Text |
| `date` | Date and time of the event | Date/Time |
| `venue` | Location of the event | Short Text |
| `manager` | Name of the person managing the event | Short Text |
| `description` | Detailed description of the event | Long Text |

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

#### Models: A Line By Line Review

- ` Line 1` imports the models package from `django.db`. This line will already be in your file!
- `Line 3` is the Event class definition. Each Django model must inherit from Django’s Model class.
- `Line 4`: the `name` field is a Django `CharField`. A `CharField` is a short line of text (up to 255 characters). In this case, the max_length option sets the maximum length of the event name to 120 characters.
    - The `name` field also has a verbose name argument. The verbose name is used to create a human-friendly name for the model field.
    - Most model fields accept verbose name, either as the first positional argument, or as a keyword argument (`verbose_name`).
* `Line 5`. `event_date` is a Django `DateTimeField`. A `DateTimeField` records a Python `datetime` object. The `event_date` field has a single argument—the verbose name for the field. Note that I have named the field `event_date`, rather than just `date`. This is because `date` is a reserved word in Python and, while Django will let you use reserved words in field names, it’s always best not to.
* `Lines 6 and 7`: `venue` and `manager` are both Django `CharField`s. As the `max_length` argument is required on `CharField`s, they have both had their `max_length` set to limit the size of the field.
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

`TODO`

## [10m] BREAK

## [30m] Activity: Creating Events

**Challenge**: Create an `events` app using the walkthrough above, add data manually, then execute a few queries against it based on the suggestions below.

**Need a Hand?** Use the following resource, [Django Book: Chapter 2, Models](https://djangobook.com/mdj2-models/), to guide you in your quest!

### Queries

1. Get an event by ID.
2. Get an event by name.
3. `TODO` more

## [20m] Activity: Tutorial Time

Keep working on your Django tutorial until the end of class!

_All seven sections must be complete in order to earn credit for this class._

## Additional Resources & Credits

- [Django Tips #7: Function-Based Views vs Class-Based Views](https://wsvincent.com/class-function-based-views/)
- [Django Book: Chapter 2, Models](https://djangobook.com/mdj2-models/)
