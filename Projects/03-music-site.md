# Homework 3: Music Site 

## Purpose (Why should I do this?)

This assignment is designed for you to practice connecting URLs, views, templates, and models in Django in order to build out list and detail pages for `Musician`s and `Song`s. These are very important skills that you will use in nearly any full-stack project.

You will be responsible for building this project from start to finish. You may (and _are expected to_) utilize resources such as past assignments, the Django tutorial, class examples, and the Django documentation.

<!-- note: add requirement to use both FBV and CBV (part 1 and part 2) -->

<!-- note: require the use of at least 4 specific different kinds of CBV - list, detail, update, delete -->

## Requirements

Your Django site must include the following pages:

1. Artist List page
  - Must list all `Musician` objects in bullet points or list items
  - `Musician` names must link to their detail pages using the `{% url %}` template tag
1. Artist Detail page
  - Must show any relevant details about that artist
  - Must list all songs by that artist in bullet points or list items
  - Each song should link to its Song Detail page using the `{% url %}` template tag
1. Song Detail page
  - Must show any relevant details about the song, including its artist

### Stretch Goals

1. Add Bootstrap styling!
1. Include album information
1. Include a "New Artist" or "New Song" page that creates a new model instance

## Scoring

Your work will be scored out of **50** points as follows:

| Criteria                                       | Possible  |
| ---------------------------------------------- | :-------: |
| Has an `Artist List` page that lists all artists |    `10`    |
| - Each Artist in list page links to its detail page |   `10`    |
| Has an `Artist Detail` page that lists all songs by that artist |    `10`    |
| - Each Song in artist page links to its detail page |   `10`    |
| Has a `Song Detail` page that lists details about one song |    `10`    |
| **TOTAL**                                  | **`50`** |

## Starter Code

If needed, check out the starter code [here](https://github.com/meredithcat/django-music-site) which includes the `Musician` and `Song` models - however I encourage you to build your own or use your code from class!

## Resources

1. [Django Class-based Views](https://docs.djangoproject.com/en/3.0/topics/class-based-views/)
1. [Django Templates](https://docs.djangoproject.com/en/3.0/topics/templates/)
