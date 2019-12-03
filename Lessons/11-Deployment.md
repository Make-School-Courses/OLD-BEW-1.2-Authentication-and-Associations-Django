# 📜 Day 11: Deployments

### ⏱ Agenda

1. [[**00m**] 🏆 Objectives](#00m-%f0%9f%8f%86-objectives)
2. [[**40m**] 📖 Guided Step By Step: Heroku Deployment](#40m-%f0%9f%93%96-guided-step-by-step-heroku-deployment)
3. [[**00m**] 💻 Activity](#00m-%f0%9f%92%bb-activity)
4. [[**10m**] 🌴 BREAK](#10m-%f0%9f%8c%b4-break)
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

## [**40m**] 📖 Guided Step By Step: Heroku Deployment

Follow along with today's step by step using your Django tutorial. You'll have another opportunity to practice deploying your MakeWiki solution soon!

### Step 1: Create Procfile

A `Procfile` tells Heroku how to run your application.

In your project root, create a file called `Procfile` and add the following line of code to it:

```txt
web: gunicorn projectname.wsgi —-log-file -
```

What does this line of code tell Heroku to do?

- `web`: Informs your Heroku dyno that you'd like to run a web process.
- `projectname.wsgi` is informs the dyno to look at a file called `wsgi` in the folder called `projectname` — substitute this with the name of your project.
—-log-file - is saying add the output to the logs

<!-- > -->

### Step 2: Run Locally Via Heroku

Heroku recommends completing this step early on to make sure your Procfile works, and Heroku has everything it needs in order to successfully deploy.

What is required to successfully deploy on Heroku? **These two files must exist in your project's root directory**:

- `Procfile`
- `requirements.txt`

### Step 3: Create New Heroku App

**3a**: In your terminal, run the following command to create a new dyno to run your deployed application:

```bash
heroku create uniqueprojectname
```

**3b**: When you run `heroku create uniqueprojectname`, Heroku also creates a git repository to host your deployed code. Run the following terminal command to add `heroku` as a remote repository --- deployment is just a `git push heroku master` away!

```bash
add heroku https://git.heroku.com/uniqueprojectname.git
```

**3c**: Open your editor, and add the following three strings to the blank `ALLOWED_HOSTS` list in `settings.py`:

```python
ALLOWED_HOSTS = [‘0.0.0.0’, ‘localhost’, 'uniqueprojectname.herokuapp.com']
```





### Step 4: `TODO`

### Step 5: `TODO`

### Step 6: `TODO`

## [**00m**] 💻 Activity

`TODO`

<!-- > -->

## [**10m**] 🌴 BREAK

<!-- > -->

## 🌃 After Class

`TODO`

<!-- > -->

## 📚 Resources & Credits

`TODO`
