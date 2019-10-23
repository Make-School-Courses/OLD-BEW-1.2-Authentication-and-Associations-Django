# Day 2: `makepizza` (Models)

### Table of Contents

1. [Learning Objectives (5 Minutes)](#learning-objectives-5-minutes)
2. [Tutorial Time (30 Minutes)](#tutorial-time-30-minutes)
3. [Overview / TT (20 Minutes)](#overview--tt-20-minutes)
4. [In Class Activity I (30 Minutes)](#in-class-activity-i-30-minutes)
5. [BREAK (10 Minutes)](#break-10-minutes)
6. [In Class Activity II (30 Minutes)](#in-class-activity-ii-30-minutes)
7. [Wrap Up Exercise (15 Minutes)](#wrap-up-exercise-15-minutes)
8. [Additional Resources](#additional-resources)

## Learning Objectives (5 Minutes)

1. Identify and describe different types of Django model fields.
2. Define what a Django model is, and their applicable use cases.
3. Write a new Django project and app!

## Tutorial Time (30 Minutes)

Begin the first portion of the Django tutorial.

Make sure to raise your hand if you get stuck installing or running Django!

## Overview / TT (20 Minutes)

Go over the [Django model](https://docs.djangoproject.com/en/2.2/topics/db/models) and [Django fields](https://docs.djangoproject.com/en/2.2/topics/db/models/#fields) documentation.

## In Class Activity I (30 Minutes)

### `makepizza`

How would you use Django models and fields to represent a Pizza with Toppings?

Work together with a friend!

**Hint**: The capitalized letters mean something special in python!

## BREAK (10 Minutes)

## In Class Activity II (30 Minutes)

Use your `makepizza` project in order to write the following queries using the command `python manage.py shell`.

### Challenges

1. Write a query that returns all Pizzas.
2. Write a query that returns one specific pizza by ID.
3. Write a query that filters the Pizza objects, and returns only Pepperoni pizzas.

### Stretch Challenges

1. Investigate the `gte` and `lte` filters.
2. Write a query that returns all Pizzas that are less than `$8.99`.
3. What is the most complex query you can write by reviewing the Django documentation?

## Wrap Up Exercise (15 Minutes)

### Check for Understanding

All answers will be in the form of a bash command.

1. What is the first step a Python developer should take before starting ANY project?
2. What two commands, run after the answer to the first, allow you to initialize the environment and safely install Django?
3. What command will allow you to create a new module (or app)?

## Additional Resources

* [Best practices working with Django models in Python](https://steelkiwi.com/blog/best-practices-working-django-models-python/)
