# 📜 Day 11: Deployments

### ⏱ Agenda

1. [[**02m**] 🏆 Objectives](#02m--objectives)
2. [[**03m**] 🤔 Why You Should Know This](#03m--why-you-should-know-this)
3. [[**60m**] 📖 **Guided Tour**: Deploy Tutorial on Heroku](#60m--guided-tour-deploy-tutorial-on-heroku)
   1. [Step 0: Before We Get Started (5m)](#step-0-before-we-get-started-5m)
   2. [Step 1: Create Procfile (5m)](#step-1-create-procfile-5m)
   3. [Step 2: Run Locally Via Heroku (5m)](#step-2-run-locally-via-heroku-5m)
   4. [Step 3: Create New Heroku App (8m)](#step-3-create-new-heroku-app-8m)
   5. [Step 4: Setup Static Root (3m)](#step-4-setup-static-root-3m)
   6. [Step 5: Push to Heroku (3m)](#step-5-push-to-heroku-3m)
   7. [Step 6: Push to GitHub (2m)](#step-6-push-to-github-2m)
   8. [Step 7: Provision a Remote Database (18m)](#step-7-provision-a-remote-database-18m)
   9. [Step 8: Run Commands (5m)](#step-8-run-commands-5m)
   10. [Step 9: Release Early and Often (5m)](#step-9-release-early-and-often-5m)
4. [[**10m**] 🌴 BREAK](#10m--break)
5. [[**30m**] 💻 **In Class Activity**: Deploy MakeWiki](#30m--in-class-activity-deploy-makewiki)
6. [📚 Resources & Credits](#-resources--credits)

<!-- > -->

## [**02m**] 🏆 Objectives

1. Demonstrate a Django deployment illustrated live, step by step, with guided mini activities and skills drills.
2. Develop a generalized, standardized plan for deploying Django projects.
3. Describe each step of the standardized required to deploy a Django project to a remote server.

## [**03m**] 🤔 Why You Should Know This

- Each experience in class today is engineered to support shipping your Contractor Project!
- In two hours, you'll have two opportunities to deploy a Django site to Heroku, along with two successfully shipped mini projects that you can reference when preparing to deploy your Contractor Project for the first time.
    - The [step by step guide](#60m--guided-tour-deploy-tutorial-on-heroku) in this plan works for _any_ Django application deployed to Heroku.
    - Wise students may consider bookmarking this plan to ensure stress-free, successful Django deployments in the future. Intensives kick off at the start of the new year!

## [**60m**] 📖 **Guided Tour**: Deploy Tutorial on Heroku

### Step 0: Before We Get Started (5m)

**This guide is resource meant to walk you through deploying ANY Django project on Heroku. Please note the following guidelines to ensure your deployment experience goes smoothly**!

1. Replace references to `uniqueprojectname` with a unique and memorable name for your project.
     - **Spaces aren't allowed in a project name, so be sure any spaces in the string with dashes (`-`)**.
2. Replace references to `projectname` with the name of your Django project.
     - **Not sure what the project's name is?** Locate the folder that contains `settings.py` --- the name of that folder is your Django project name.

Now that we know how to use this guide later on, let's get started.

Open your your Django tutorial codebase in your editor, and complete each step as guided by the instructor.

### Step 1: Create Procfile (5m)

A `Procfile` tells Heroku how to run your application. In your project root, **create a file called `Procfile`** and **add the following line of code** inside:

```txt
web: gunicorn projectname.wsgi —-log-file -
```

**What does this line of code tell Heroku to do?**
- `web`: Informs the Heroku Dyno that your project is a web project.
- `projectname.wsgi` Tells the Dyno to look at a file called `wsgi` in the folder called `projectname`.
    - This file is included when you create a new Django project.
- `—-log-file -` Write all terminal output to the logs.
    - View your Heroku logs by running `heroku logs`.

### Step 2: Run Locally Via Heroku (5m)

Heroku recommends completing this step early on to make sure your `Procfile` works, and that the Dyno has everything it needs in order to successfully install your project and deploy it live.

**What files are required to successfully deploy on Heroku?** These two files must exist in your project's root directory**:

- `Procfile`
- `requirements.txt`

### Step 3: Create New Heroku App (8m)

- **3a**: In your terminal, run the following command to create a new Dyno, where your project will be installed and deployed for use by the public.

    ```bash
    heroku create uniqueprojectname
    ```

- **3b**: Open your editor, and add the following strings to the blank `ALLOWED_HOSTS` list in `settings.py`:

    ```python
    ALLOWED_HOSTS = [‘localhost’, 'uniqueprojectname.herokuapp.com']
    ```

    **What do these values mean?**:

    - `localhost`: Development environment --- the place where you write code.
    - `uniqueprojectname.herokuapp.com`: Production environment 000 the place you deploy your finished code to show others.

### Step 4: Setup Static Root (3m)

Add the following string to `settings.py`:

```python
STATIC_ROOT = os.path.join(BASE_DIR, ‘staticfiles’)
```

### Step 5: Push to Heroku (3m)

Add, commit, and push your changes to Heroku!

```bash
git add .
git commit -m "tweaked settings for deployment"
git push heroku master
```

⚠️ **GET AN ERROR?**: When deploying with Git, Heroku wants to initiate the repo from the project root, where your ` manage.py`  file lives. You might notice in the tutorial repo that `manage.py` is one level down. Even though running the app locally with Heroku worked, if you try to deploy with `git push heroku master` you’ll receive an error that says `Failed to detect app`. You can fix this by running the following command instead of `git push heroku master`:

```bash
git subtree push —-prefix projectname heroku master
```

⏰ **Why does this take so long?!**

Every time you push to Heroku, it kicks off the following deployment workflow:

1. Examine `requirements.txt` for changes since the last deployment.
      - Install new dependencies automatically.
2. Run all new migrations found since the last deployment.
      - Heroku executes the exact same `manage.py` commands we've practiced all term!
3. Launch the production server according to the command in the `Procfile`.

### Step 6: Push to GitHub (2m)

Once you know everything works, push to GitHub.

```bash
git push origin master
```

### Step 7: Provision a Remote Database (18m)

🤔 You might be asking yourself the following questions:

  - *I thought we stored our data using SQLite?!*
  - *Isn't that just a file in our repository?*
  - *Why do we need to create and use a whole new database?*

Our development environment uses SQLite. It's an excellent tool for day to day development — but **it doesn’t work with Heroku** and numerous other platforms used to deploy and manage server-side applications. PostgreSQL (or Postgres) is the most popular database deployed amongst real-world Django projects.

⁉️ ***Never heard of Postgres? Don't worry, let's walk through setting up our first database together!***

**7a**. Add a free database to your project by running the following command in your terminal:

```bash
heroku addons:create heroku-postgresql:hobby-dev
```

You'll see the following output:

```bash
Creating heroku-postgresql:hobby-dev on ⬢ uniqueprojectname... free
Database has been created and is available
 ! This database is empty.
Created postgresql-randomword-35234 as DATABASE_URL
```

**7b**: In your terminal, install `gunicorn`, `psycopg2-binary` and `dj-database-url` via `pip`:

```bash
python -m pip install gunicorn dj-database-url psycopg2-binary
```

**7c**: Add the two new dependencies to `requirements.txt` so that they are installed when you next push to Heroku:

```txt
gunicorn
dj-database-url
psycopg2-binary
```

**7d**: Add these two lines to the bottom of `settings.py`:

```python
import dj_database_url
db_from_env = dj_database_url.config()
DATABASES[‘default’].update(db_from_env)
```

This code will parse the values of the `DATABASE_URL` environment variable and convert them to something Django can understand.

**7e**: Push to Heroku to complete the database setup:

```bash
git push heroku master
```

### Step 8: Run Commands (5m)

**8a**: Right now, the database we just created is completely empty. It doesn't know about our models, or how to store the data we defined within them. We can migrate the new database by running the following command:

```bash
heroku run python manage.py migrate
```

**8b**: Finally, create an admin user to test the admin interface on your deployed website:

```bash
heroku run python manage.py createsuperuser
```

### Step 9: Release Early and Often (5m)

**So far, we've accomplished**:
- Creating a live website, located at `https://uniqueprojectname.herokuapp.com` now uses a PostgreSQL database ‒ with absolutely no changes to our application's code!
- We have our first user, an administrator, ready for the next step ‒ logging in to the admin (located at https://uniqueprojectname.herokuapp.com/admin/), entering the credentials you created in the terminal, then adding some data!
- We've done all the work required to release new features and bug fixes early and often!

<p style="color:red; font-weight: bold;">You should strive to frequently push to your production server ‒ anytime you fix a bug or add a new feature. That means you may find yourself pushing code to Heroku multiple times a day ‒ just like most major companies!</p>

## [**10m**] 🌴 BREAK

## [**30m**] 💻 **In Class Activity**: Deploy MakeWiki

1. Follow all 8 steps above to deploy the MakeWiki project.
2. Log in to `https://uniqueprojectname.herokuapp.com/admin/` with the credentials you made in Step 8.
3. Add at least two new Pages in the admin.
4. Test the application's workflow in the browser:
   1. Sign Up
   2. Log In
   3. Create Page
   4. Log Out
5. Celebrate your second deployment! Slack the link to your working deployment in our class channel.

## 📚 Resources & Credits

- [Provisioning Heroku Postgres](https://devcenter.heroku.com/articles/heroku-postgresql#provisioning-heroku-postgres)
- [Painless PostgreSQL + Django](https://medium.com/agatha-codes/painless-postgresql-django-d4f03364989)
- [9 Straightforward Steps for Deploying Your Django App With Heroku](https://medium.com/agatha-codes/9-straightforward-steps-for-deploying-your-django-app-with-heroku-82b952652fb4)
