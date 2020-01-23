# Day 2: Models & ForeignKey

### Table of Contents

1. [Learning Objectives (5 Minutes)](#learning-objectives-5-minutes)
1. [Tutorial Review (30 Minutes)](#tutorial-review-30-minutes)
1. [Tutorial Time (30 Minutes)](#tutorial-time-30-minutes)
1. [BREAK (10 Minutes)](#break-10-minutes)
1. [Models Review (30 Minutes)](#models-review-30-minutes)
1. [Wrap Up](#wrap-up)
1. [Additional Resources](#additional-resources)

## Learning Objectives (5 Minutes)

1. Identify and describe different types of Django model fields.
2. Define what a Django model is, and their applicable use cases.
3. Write a new Django project and app!

## Tutorial Review (30 Minutes)

Submit your Tutorial Part 1 using [Gradescope](https://gradescope.com).

Review the first portion of the Django tutorial together.

As we review, be sure to compare/contrast Django syntax with what you've seen before in Flask.

### Practice - I Do, We Do, You Do

Watch as the instructor starts a new project using the techniques from the tutorial.

Then, tell the instructor what to do to accomplish the same task.

On your own, complete the following:

1. Create a project called 'music_site' that contains an app called 'music'.
1. Re-route _all_ web requests (hint: use the empty string `''`) to your music app's URLs file. Then, send any web requests for the homepage `''` to a view called `home`.
1. Create a view function `home` that returns an HttpResponse with the text "Hello World! You're at the Music App home page."

## Tutorial Time (30 Minutes)

Continue to work on the Tutorial Part 2 (Models).

## BREAK (10 Minutes)

## Models Review (30 Minutes)

Let's take a look at some Model code using a `ForeignKey` field.

```py
from django.db import models

class Musician(models.Model):
    name = models.CharField(max_length=50)

class Song(models.Model):
    artist = models.ForeignKey(Musician, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    num_stars = models.IntegerField()
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

## Wrap Up

Finish the Tutorial Part 2 (Models) before the beginning of Class 3.

Come prepared with any questions you have about how models work!

## Additional Resources

* [Best practices working with Django models in Python](https://steelkiwi.com/blog/best-practices-working-django-models-python/)

* [Django Models documentation](https://docs.djangoproject.com/en/2.2/topics/db/models/)