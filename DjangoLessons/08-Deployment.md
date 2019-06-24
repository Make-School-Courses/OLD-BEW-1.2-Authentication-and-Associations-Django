# 📜 Day 8: Deployment in Django

### ⏱ Agenda

1. [🏆 [5m] Learning Objectives](#%F0%9F%8F%86-5m-Learning-Objectives)
2. [🏁 [10m] Initial Exercise](#%F0%9F%8F%81-10m-Initial-Exercise)
3. [📖 [20m] Overview](#%F0%9F%93%96-20m-Overview)
4. [💻 [30m] In Class Activity I](#%F0%9F%92%BB-30m-In-Class-Activity-I)
5. [🌴 [10m] BREAK](#%F0%9F%8C%B4-10m-BREAK)
6. [💻 [30m] In Class Activity II](#%F0%9F%92%BB-30m-In-Class-Activity-II)
7. [📚 Resources & Credits](#%F0%9F%93%9A-Resources--Credits)

## 🏆 [5m] Learning Objectives

1. Identify and describe the different files required for Django deployment.
1. Implement a deployment strategy for Django on Heroku.

## 🏁 [10m] Initial Exercise

### Thinking About Deployments

With a neighbor, **write down the answers** to the following questions:

1. What is the **primary difference** between Heroku and GitHub Pages?
2. What is **Gunicorn**?
3. What **role does Gunicorn play** when deploying any Python web server?

## 📖 [20m] Overview

### Why We Use Heroku

### What You Need to Deploy

- A working Django site that runs on `localhost`
- `requirements.txt` in the root of your repository
- `Procfile` in the root of your repository

#### Interacting With a Requirements File

**PROTIP**: All commands should be run in the context of an activated `virtualenv`.

##### Generating a Requirements File

To generate a `requirements.txt` file, run the following command in the root of your repository:

```bash
pip freeze > requirements.txt
```

You should freeze your `requirements.txt` file when:

- You install a new package from `pip` (`pip install packagename`).
- You are about to deploy to any platform.

Be sure to add, commit, and push this file to GitHub!

##### Installing From a Requirements File

If a `requirements.txt` file already exists in the repository, run the following command to install all the required packages in your `virtualenv`:

```bash
pip install -r requirements.txt
```

#### Heroku Dependencies

Walk through [Django App Configuration on Heroku](https://devcenter.heroku.com/articles/django-app-configuration) to learn more about what dependencies are required to install Django on Heroku.

#### Writing a Procfile

A `Procfile` looks like this:

```Procfile
web: gunicorn hello:app
```

It consists of **two parts**:

* How/where to run the command (before the colon)
    * **Examples**: `web` or `worker`.
* The command to run in order to execute the web server (after the colon)
    * **Example**: `gunicorn hello:app` runs to the `hello` Django project via Gunicorn.

## 💻 [30m] In Class Activity I

### Deploy Sample Project

**Challenge**: **Use [this tutorial](https://devcenter.heroku.com/articles/getting-started-with-python) to deploy to Heroku.** It also serves to refresh your knowledge on everything we've learned in class so far! It will walk you through setting up a sample Django website and pushing it to Heroku.

You may ask your friends or your instructor for help, but **be sure to complete the tutorial on your own machine, and to show the instructor when you've finished**.

**Remember**: *ask the instructor if you have any questions about deploying!*

## 🌴 [10m] BREAK

## 💻 [30m] In Class Activity II

### Deploy MakePizza Project

Find a buddy and use the example you walked through earlier to develop a `Procfile` for the [makepizza](https://github.com/droxey/makepizza) project.

**Challenge**: Can you team up to push `makepizza` to Heroku?

## 📚 Resources & Credits

- **[Slant: Heroku vs. GitHub Pages](https://www.slant.co/versus/11233/13313/~heroku_vs_github-pages)**
