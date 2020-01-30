# Day 3: More Models

### Table of Contents

1. Learning Objectives
1. Review: Music Site Project (15 minutes)
1. Filters (25 minutes)
1. BREAK
1. Activity: Modeling Many-to-Many Relationships
1. ManyToManyField and Through
1. Additional Resources & Credits

## Learning Objectives (5 minutes)

1. Review models, filters, and their common usage patterns in Django.
1. Use filters to query the database for a specific subset of data.
1. Write data models for real-world scenarios.
1. Use the `Many-to-Many` and `Through` relationship to model scenarios.

## Review & Submit Homework (5 minutes)

Review any questions on the homework assignment & submit via [Gradescope](https://gradescope.com).

## Review: Music Site Project (20 minutes)

Review the music site we created in the last lesson. You should have models for `Musician`, `Song`, and `Album`.

Try adding a field `publish_date`, of type `DateField`, to your `Album` class. How can we ensure that it is easy to migrate our existing data?

Go to your admin site and enter some data for your favorite songs and albums. Try to enter at least 5-10 data points.

If you're stuck, try cloning this [sample repository](https://github.com/meredithcat/django-music-site).

## Filters (20 minutes)

Perhaps we want to only see the songs that include a certain keyword, or are played by a certain artist. Or perhaps we want to only see albums that were published in a certain time period.

Use Django filters to enable this capability! They allow us to use a double-underscore, in conjunction with the field name, to generate results based on our unique criteria.

### Common Filters

These common filters come in handy in nearly every project:

- `Song.objects.get(id=14)`: Return *one* `Song` with `id` `14`.
- `Song.objects.filter(name="Single Ladies")`: Return 0 to many `Song`s with the `name` `Single Ladies`.
- `Song.objects.filter(name__iexact="Ocean Eyes")`: Return songs that match `Ocean Eyes` and `ocean eyes` (or any other capitalization).
- `Song.objects.filter(name__contains="Love")`: Return songs that contain the exact string, `Love`, but not `love`. (For case insensitive, use `icontains`.)
- `Album.objects.filter(publish_date__gte=datetime.date(2011, 1, 1))`: Return albums that were published after January 1, 2011.
- `Album.objects.filter(publish_date__year__range=[1980, 1990])`: Return albums that were published between 1980 and 1990, inclusive.

**PROTIP**: `.get()` will return 0 to one result, whereas `.filter()` can return 0 to many results.

## BREAK (10 minutes)

## Activity: Data Modeling (25 minutes)

As a class, model a Lyft/Uber competitor `MakeRide` which hires drivers to give rides to passengers. Use the whiteboard to log all relevant information for each ride.

With a partner, answer the following questions about the data you collected:

1. How do we plan to _access_ the data? (E.g. Find all rides that took place between 10am and 12pm on March 3rd.) Come up with at least 3-5 examples.
1. What are the _nouns_ we want to track? (E.g. Driver, Rider, Place.) These will be our database models.
1. What are the _relationships_ between these models? E.g. How is a driver related to a rider?

As a class, go over the answers and construct a data model for `MakeRide`.

## ManyToManyField and Through (25 minutes)

Here is an example of a many-to-many relationship using a `through` class. 

```py
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=128)

    def __str__(self):
        return self.name

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')

    def __str__(self):
        return self.name

class Membership(models.Model):
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```

This way, we can track more information about the relationship between two models. Even if you don't specify a `Through` table, Django will create one anyway, so it is usually better to be more explicit about the relationship.

We can interact with our data models as follows:

```py
>>> ringo = Person.objects.create(name="Ringo Starr")
>>> paul = Person.objects.create(name="Paul McCartney")
>>> beatles = Group.objects.create(name="The Beatles")

>>> m1 = Membership(person=ringo, group=beatles,
...     date_joined=date(1962, 8, 16),
...     invite_reason="Needed a new drummer.")
>>> m1.save()

>>> beatles.members.all()
<QuerySet [<Person: Ringo Starr>]>

>>> ringo.group_set.all()
<QuerySet [<Group: The Beatles>]>

>>> m2 = Membership.objects.create(person=paul, group=beatles,
...     date_joined=date(1960, 8, 1),
...     invite_reason="Wanted to form a band.")

>>> beatles.members.all()
<QuerySet [<Person: Ringo Starr>, <Person: Paul McCartney>]>
```

### Activity: Modeling Many-to-Many

With your partner, choose one of the following scenarios (or create your own!) and write a data model, including a `Through` class:

1. EventBrite: `Attendee` and `Event`
1. Patreon: `Creator` and `Subscriber`
1. LinkedIn: `Employee` and `Company`

Your instructor will check in on your progress before the end of class.

## Wrap-Up

Continue working on the [Tutorial Part 3](https://docs.djangoproject.com/en/2.2/intro/tutorial03/) (Views & URLs). Be sure to finish Part 3 before the next class session!

## Additional Resources & Credits

- [Many-to-Many Fields](https://docs.djangoproject.com/en/3.0/topics/db/examples/many_to_many/)
- [Django: Extra Fields on Many-to-Many](https://docs.djangoproject.com/en/3.0/topics/db/models/#extra-fields-on-many-to-many-relationships)
- [Django Book: Chapter 2, Models](https://djangobook.com/mdj2-models/)
