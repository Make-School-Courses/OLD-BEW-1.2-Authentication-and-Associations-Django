# Day 4: Forms and Templates

### Table of Contents

1. [Learning Objectives (5 Minutes)](#learning-objectives-5-minutes)
2. [Initial Exercise (30 Minutes)](#initial-exercise-30-minutes)
3. [Code Along (30 Minutes)](#code-along-30-minutes)
4. [BREAK (10 Minutes)](#break-10-minutes)
5. [In Class Activity I (45 Minutes)](#in-class-activity-i-45-minutes)

## Learning Objectives (5 Minutes)

1. Practice industry-standard Python development with `pip` and `virtualenv`.
1. Incorporate prior experience with models and views in order to implement a real-world Pizza Shop project.
1. Identify and describe how to use Django Templates in conjunction with Django Forms.
2. Solve a common real-world server-side architecture interview problem.

## Initial Exercise (30 Minutes)

Today's task is inspired by a favorite backend web interview question amongst interviewers at big companies, like Twilio.

**How would you create an application, from scratch, that allows a neighborhood pizza shop to run their day-to-day business?**

### Create an Industry Standard Python Environment

**PROTIP**: All Python projects should follow this standard methodology detailed in Steps 1 through Step 6 when cloned or initialized. **All commands should be run exactly as written.** The required use of `sudo`, `pip3`, or `python3` indicates an environment issue that will need repaired as soon as possible. Notify the instructor!

#### Initialize the MakePizza Project

1. [Create a new project](https://github.com/new) on GitHub.
   - Name it `makepizza`, please!
   - In the dropdown labeled `Add .gitignore`, select `Python` in order to ignore `venv` directories by default.
   - Create the repository on GitHub and copy the URL to clone.
   - Copy it to your local machine via `git clone <REPO_URL>`
2. `cd makepizza`
3. Create a new `virtualenv`: `virtualenv -p python3 venv`
4. Activate the new `venv` environment: `source venv/bin/activate`
5. Install dependencies into your fresh `venv`: `pip install Django`
6. Keep track of requirements by running `pip freeze > requirements.txt`
7. Start a Django project in your local git repository by running `django-admin startproject pizzashop`
8. `cd pizzashop` in order to create two new Django apps:
   1. `python manage.py startapp pizza`
   2. `python manage.py startapp shop`
9. Run initial project migrations: `python manage.py migrate`
10. Open the `makepizza` directory in your IDE by running `code .`, `atom .`, etc.
11. Open `pizzashop/settings.py`, and modify the `INSTALLED_APPS` setting to include the `pizza` and `shop` apps you created in Step 8.
      - **HINT**: Use the documentation or reference the code you've written in the tutorial!
12. Run `python manage.py runserver` and open the `localhost:8000` in your browser.
      - You should see a rocket if everything went as planned!
13. Add, commit, and push to GitHub.
14. Keep your IDE window open, as well as your browser, so you can code along during class today!

## Code Along (30 Minutes)

### Models, Views, and URLConf Review

1. Show the class the MakePizza project in it's current state, highlighting the function-based view that serves the homepage.
2. Create models in `pizza/models.py`  with the class.
   - Ask for suggestions for fields in the model, and their corresponding field types, as you build the model.
3. Migrate the new models and apply them.
4. Run the development server and view the MakePizza homepage.

### Templates and Forms

1. Discuss base templates and the ability to extend them.
2. Add HTML and images into the base template and demonstrate extending a template.
3. Show how to create ModelForms from the Pizza model we created earlier.
4. Pass a form down to the template and render it.
5. Redirect to `thanks.html` when the form is successfully submitted.

### Challenges

- Is the root URLconf the best place for the `/` URL? Why or why not? Be ready to defend your answer!

## BREAK (10 Minutes)

## In Class Activity I (45 Minutes)

1. Work with a partner, but code on your own machines, in the same `makepizza` repo you created earlier.
2. Repeat the above steps in order to implement the `shop` app we created in our Initial Exercise.
