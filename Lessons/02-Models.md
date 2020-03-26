# Day 2/3: Models & ForeignKey

### Table of Contents

1. [Learning Objectives (5 Minutes)](#learning-objectives-5-minutes)
1. [Tutorial Review](#tutorial-review-20-minutes)
1. [Models Review (30 Minutes)](#models-review-30-minutes)
1. [Break](#break)
1. [Activity: Models (25 minutes)](#activity-models-25-minutes)
1. [Filters (25 minutes)](#filters-25-minutes)
1. [Lab Activity & Homework (45 minutes)](#lab-activity-homework-45-minutes)
1. [Wrap Up](#wrap-up)
1. [Additional Resources](#additional-resources)

## Learning Objectives (5 Minutes)

1. Identify and describe different types of Django model fields.
2. Define what a Django model is, and their applicable use cases.
3. Write a new Django project and app!

## Tutorial Review (20 Minutes)

Go through Part 2 of the tutorial and go over any questions.

Then, take a few minutes to submit Part 2 on [Gradescope](https://gradescope.com).

## Models Review (30 Minutes)

Bring up your `music` app from last class session. We'll be adding some new functionality to it.

Let's take a look at some Model code using a `ForeignKey` field. You can add this to `music/models.py` file.

```py
from django.db import models

class Musician(models.Model):
    name = models.CharField(max_length=50)

    def __str__(self):
        return self.name

class Song(models.Model):
    artist = models.ForeignKey(Musician, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    num_stars = models.IntegerField()

    def __str__(self):
        return self.name
```

### Tell Django about our Models

If you haven't yet, in `music_site/settings.py`, enter the following line into the `INSTALLED_APPS` list:

```py
INSTALLED_APPS = [
    ...,
    'music'
]
```

Then register the models in `music/admin.py`:

```py
from django.contrib import admin
from . import models

admin.site.register(models.Song)
admin.site.register(models.Musician)
```

### Migrate the Models

- Migrations inform the database about any changes to your models.
- You make and apply migrations when creating new models, or changing an existing model.
- Migrations can be applied by any developer on the team to ensure their local database structure is compatible with the current models.

We can do a migration using the following commands:

1. `python manage.py makemigrations`
2. `python manage.py migrate`

### Add Some Entries Manually

Run `python3 manage.py shell` to start the interactive shell.

```bash
>>> from music.models import Musician, Song

>>> Musician.objects.all()
<QuerySet []>

>>> m1 = Musician(name='Journey')
>>> m1.save()

>>> s1 = Song(name='Don\'t Stop Believing', artist=m1, num_stars=5)
>>> s1.save()
```

### Query our Database Entries

<!-- NOTE: have a section SPECIFICALLY for each of: all, get, filter -->

<!-- NOTE: do a worksheet here with above -->

Now, how can we interact with these models? Let's try it out!

```bash
>>> from music.models import Musician, Song

>>> Musician.objects.all()
<QuerySet [<Musician: Journey>]>

>>> s1 = Song.objects.get(id=1)
>>> m1 = s1.artist

>>> s1.artist
<Musician: Journey>

>>> m1.song_set
<QuerySet [<Song: Don't Stop Believing>]>
```

## BREAK

## Activity: Models (25 minutes)

Write a model for `Album` and add it to your `models.py` file.

- What are the relationships between `Musician`, `Album`, and `Song`? Are `Musician` and `Song` still related? Is it a direct relationship (Musician has-many Songs) or indirect (Musician has-many Albums each of which has-many Songs)?

- How can you migrate the database? Try doing a database migration and see what happens.

## Filters (25 minutes)

Perhaps we want to only see the songs that include a certain keyword, or are played by a certain artist. Or perhaps we want to only see albums that were published in a certain time period.

Use Django filters to enable this capability! They allow us to use a double-underscore, in conjunction with the field name, to generate results based on our unique criteria.

### Common Filters

These common filters come in handy in nearly every project:

- `Song.objects.get(id=14)`: Return *one* `Song` with `id` `14`.
- `Song.objects.filter(name="Single Ladies")`: Return 0 to many `Song`s with the `name` `Single Ladies`.
- `Song.objects.filter(name__iexact="Ocean Eyes")`: Return songs that match `Ocean Eyes` and `ocean eyes` (or any other capitalization).
- `Song.objects.filter(name__contains="Love")`: Return songs that contain the exact string, `Love`, but not `love`. (For case insensitive, use `icontains`.)
- `Album.objects.filter(pub_date__gte=datetime.date(2011, 1, 1))`: Return albums that were published after January 1, 2011.
- `Album.objects.filter(pub_date__year__range=[1980, 1990])`: Return albums that were published between 1980 and 1990, inclusive.

**PROTIP**: `.get()` will return 0 to one result, whereas `.filter()` can return 0 to many results.

## Lab Activity & Homework (45 minutes)

Your homework is to read the [Models documentation](https://docs.djangoproject.com/en/3.0/topics/db/models/) and answer the following questions:

1. What does a model's field type represent? If I use a `CharField` versus a `TextField`, for example, what does that change about how the data is stored?
1. What is the difference between the `null` and `blank` field options? What do each of them represent?
1. How do we use the `TextChoices` field type to display multiple options?
1. What is a `primary_key` field? If we don't specify a primary key, what is the default?
1. How do we specify a verbose name? What purpose does it serve?
1. In the documentation under "Many-to-one Relationships", an example is given of "Manufacturer" and "Car" models. Complete the code by adding at least 2 new fields to each model.
1. In the documentation under "Many-to-Many Relationships", an example is given of "Pizza" and "Topping" models. Complete the code by adding at least 2 new fields to each model.
1. What is an example of a one-to-one relationship? When would we use a OneToOneField?
1. Sometimes we need to relate a model to one from another app. Give an example of an `import` line to show how we'd import the other model.
1. What is the `class Meta`? When would we use it?
1. What is an example of a model method? Suppose we have a class `Album`. What methods might we want to write for it?
1. Give an example of model inheritance. How does inheritance help us to write better code?

Write your answers in a file called `models_questions.md` and submit via Gradescope. (Graded based on effort - no need to be completely correct, but "I don't know" is not a valid answer!)

## Wrap Up

Continue reading the Models documentation and submit your answers via [Gradescope](https://gradescope.com).

## Additional Resources

* [Best practices working with Django models in Python](https://steelkiwi.com/blog/best-practices-working-django-models-python/)

* [Django Models documentation](https://docs.djangoproject.com/en/2.2/topics/db/models/)
