# Homework 5: MakeWiki

## Purpose (Why should I do this?)

This assignment is designed for you to practice using **forms** and **authentication**, as well as writing **unit and route tests** for your code.

**To complete this assignment, you *can* and *should* reference your code for [Assignment 4: Polls Redux](Projects/04-polls-redux.md).** This assignment is for the most part very similar, and is designed to be a check for understanding.

Scoring is as follows:

| Criteria                                       | Possible  |
| ---------------------------------------------- | :-------: |
| Login & Logout |    `10`    |
| Signup |    `10`    |
| Wiki Page Creation Form |    `10`    |
| Wiki Page Edit Form |    `10`    |
| Wiki Details Page Test |    `10`    |
| Wiki Details Page Edit Test |    `10`    |
| Wiki Creation Page Test |    `10`    |
| **TOTAL**                                  | **`70`** |

## Setup

Go to the [MakeWiki starter code](https://github.com/make-school-labs/makewiki-starter) and clone the repository to your local hard drive. Then, set up a _new_ repository for your Polls application on [GitHub.com](https://github.com) and execute the following to switch the remote:

```
$ git remote remove origin
$ git remote add origin git@github.com:USERNAME/REPOSITORY.git
```

Run the server and take a look at the site: there is a Wiki List page which lists the wiki articles, and a Wiki Detail page which lists specific details about each one.

## Part 1: Authentication

In this part, we'll add the login, logout, & signup functionality to the MakeWiki app.

### Login & Logout _(10 Points)_

1. Add the Django authentication views in `django.contrib.auth.urls` to the project's URLconf.
1. Test `/accounts/login` in your browser -- see if you can log in using username `admin` and password `djangopony`.
1. In `base.html`, hide the New Page and Log Out buttons for unauthenticated users.
1. When a user clicks `Log Out`, they should be logged out of the system, and returned to the homepage.
1. When a user clicks `Log In`, they should be navigated to the Login page.
1. Replace `Hello, USERNAME` text with the username of the logged-in user, and only show it when the user is logged in.

### Signup _(10 Points)_

1. Create a new app named `accounts`. Add it to the `INSTALLED_APPS` list in `settings.py`.
1. Create a view for signing up that extends `django.views.generic.CreateView` and renders the template contained in `registration/signup.html`.
1. In accounts/urls.py, link the `SignupView` class to a URL named `signup`.
1. Add `accounts.urls` to the project's URLconf.
1. When a user clicks `Sign Up`, they should be presented with a form to create an account, and can submit it successfully.

## Part 2: Forms

Here we'll flesh out the functionality of the "Create" button, as well as provide an Edit option to edit existing wiki pages.

### Wiki Page Creation Form _(10 Points)_

To add a Create view, complete the following steps in the `wiki` app:

1. In `views.py`, import the `PageForm` class from `forms.py`. This form enables editing and creating of `Page` objects in the database.
1. Create a new view class called `PageCreateView`. Link it to a URL named `create`.
1. On `GET`, render a template to display the `PageForm` instance.
1. On `POST`, check if the data in the form is valid.
  - If True, save the data and use the logged-in user as the `Page`'s `author`. Then, redirect to the Detail View for the newly created `Page` object.
  - If False, display all the errors in the template, above the form fields.
1. Instead of hard-coding the path to redirect to, use the `reverse` function to return the path.

### Wiki Page Edit Form _(10 Points)_

For the Page Detail view, complete the following steps in the `wiki` app:

1. In `views.py`, import the `PageForm` class from `forms.py`. Edit the `PageDetailView` class as follows:
1. On `GET`, render an edit form below the page details.
1. On `POST`, check if the data in the form is valid.
  - If True, save the data and use the logged-in user as the `Page`'s `author`. Then, redirect back to the Detail View.
  - If False, display all the errors in the template, above the form fields.
1. Instead of hard-coding the path to redirect to, use the `reverse` function to return the path.
1. _(Stretch Challenge)_ After successfully editing a Page, use [Django Messages](https://docs.djangoproject.com/en/3.0/ref/contrib/messages/) to "flash" the user a success message: "REPLACE_WITH_PAGE_TITLE has been successfully updated."
1. _(Stretch Challenge)_ Use the [Crispy Forms](https://django-crispy-forms.readthedocs.io/en/latest/install.html) library in conjunction with Bootstrap to make your forms look even more beautiful and clean (and, well, _crisp_)!

## Part 3: Testing

In this part of the assignment, we'll flex our testing muscles and write some route tests!

### Wiki Details Page Test _(10 Points)_

Write a route test that does the following:

1. Create an instance of `Page` and save it to the database. (HINT: You'll need to first create an instance of `User` to use as the page's author.)
1. Load the Wiki Details page for that `Page`'s `slug`.
1. Verify that the response has a `status_code` of `200`.
1. Verify that the response's context includes the info for the `Page` object requested. (HINT: You can use `assertContains` to check the exact text of the response.)

### Wiki Details Page Edit Test _(10 Points)_

Write a route test that does the following:

1. Create an instance of `Page` and save it to the database.
1. Create a dictionary of key-value pairs containing the post data to be sent via the form. This should include a new page title and description.
1. Make a `POST` request to the details page with `self.client.post()`.
1. Check that we get a 302 status code. (Why 302 and not 200?)
1. Check that the page object was modified in the test database.

### Wiki Creation Page Test _(10 Points)_

Write a route test that does the following:

1. Create a dictionary of key-value pairs containing the post data to be sent via the form. This should include a page title and description.
1. Make a `POST` request to the Wiki Create page with `self.client.post()`.
1. Check that we get a 302 status code.
1. Check that the page object was created in the test database.

## Submission

Submit your finished homework using our [class submission site](https://gradescope.com).