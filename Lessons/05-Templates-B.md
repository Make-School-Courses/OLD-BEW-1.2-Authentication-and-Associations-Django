# 📜 Day 5: Templates: Tying it Together

### ⏱ Agenda

1. [🏆 [**5m**] Learning Objectives](#%f0%9f%8f%86-5m-learning-objectives)
2. [📖 [**20m**] **Overview**: Template Deja-Vu](#%f0%9f%93%96-20m-overview-template-deja-vu)
3. [📝 [**20m**] **Demo**: Personal Wiki](#%f0%9f%93%9d-20m-demo-personal-wiki)
4. [🌴 [**10m**] BREAK](#%f0%9f%8c%b4-10m-break)
5. [💻 [**65m**] **Activity**: Personal Wiki (makewiki)](#%f0%9f%92%bb-65m-activity-personal-wiki-makewiki)
6. [🌃 **After Class**: Complete Project](#%f0%9f%8c%83-after-class-complete-project)
7. [📚 Resources & Credits](#%f0%9f%93%9a-resources--credits)

## 🏆 [**5m**] Learning Objectives

1. Contrast and compare Django template implementation to Jinja.
2. Demonstrate out how Django processes a single request/response cycle.
3. Distinguish the each file in a Django app and when it's executed by the framework.
4. Create a minimal application from start to finish.

## 📖 [**20m**] **Overview**: Template Deja-Vu

- Built on top of Jinja!
- Enhance the template syntax you're already familiar with
- New [Template Tags](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-tag-reference) and [Filters](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-filter-reference)

### Definitions: Template Tags & Filters

In Django templating, the following terminology is used frequently:

- [**Template Tags**](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-tag-reference): Template tags allow you to recycle functionality, iterate, and use conditionals to control how your HTML is rendered.
- [**Filters**](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-filter-reference): Filters allow you to compute or transform any value in the template itself, rather than the view.

#### Syntax

- **Template Tags** use `{% keyword %}{% endkeyword %}` syntax.
- **Filters** use `{{ variable_name|filter }}` syntax.

#### Template Tags + Filters

##### Working Together

  ```python
  <p class="info">
    You have {{ walrus_list|length }} walrus{{ walrus_list|length|pluralize:"es" }.
  </p>
  <ul id="walruses-list">
    {% for walrus in walrus_list %}
      <li class="walrus">
        <p><strong>Nickname</strong>: {{ walrus.nickname|title }}</p>
        <p><strong>Age</strong>: {{ now|timesince:walrus.birthdate }}
      <li>
    {% empty %}
        <li class="no-walruses">No walruses here. ¯\_(ツ)_/¯</li>
    {% endfor %}
  </ul>
  ```

### Activity: Exploring Filters [5 minutes]

Look through the [filters documentation](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-filter-reference) and, with a partner, identify 3 interesting or useful filters. Discuss how they could be used in a project.

### Inheritance Structure

- **`myproject/templates/base.html`**: Equivalent to Jinja, the parent page contained in  `base.html` allows you to render resources common to many pages on your website.
  - Each app's custom templates can extend from the parent template.
  - Define placeholders for content with the `block` template tag: `{% block NAME_OF_BLOCK %}{% endblock %}`.
- **`myproject/app/templates/list.html`**: Extends the project's `base.html` page using the `extends` template tag: `{% extends "base.html" %}`.
  - Starting point for most templates you write.
- **`myproject/app/templates/partials/list_item.html`**: Write less code with partial templates! Use the `include` template tag to include a partial in a parent or child template:`{% include "templates/partials/comment.html" %}`

### Rendering Templates in Views

#### Function-Based View

```python
"""
filename: app/views.py
---
A function-based view that renders an HTML template named 'now.html`.
This template is located in the app/templates/now.html.
"""
from datetime import datetime
from django.shortcuts import render

def show_the_time(request):
    """
    Gets the current datetime from the server and passes it to the template,
    and rendered via {{ current_date_time }}.
    """
    return render(request, 'now.html', {
      'current_date_time': datetime.now()
    })
```

#### Class-Based View

```python
"""
filename: app/views.py
---
A class-based view that renders an HTML template named 'now.html`.
This template is located in the app/templates/now.html.
"""
from datetime import datetime
from django.shortcuts import render
from django.views import View

class ShowTimeView(View):
    def get(self, request):
        return render(request, 'now.html', {
          'current_date_time': datetime.now()
        })
```

## 📝 [**20m**] URLs with `reverse`

When working with URLs, we often give a certain URL a 'name' attribute. The value of that 'name' field can be used to identify the URL, even if the URL path itself changes.

Let's say we have the following URLs file:

```py
from news import views

urlpatterns = [
  path('articles/<int:year>', views.year_archive, name='news-year-archive')
]
```

### reverse

We can use the `reverse` function to "reverse-engineer" a URL from its `name` field and any parameters:

```py
from django.http import HttpResponseRedirect
from django.urls import reverse

def redirect_to_year(request):
    # ...
    year = 2006
    # ...
    news_year_url = reverse('news-year-archive', args=[year])
    return HttpResponseRedirect(article_url)
```

### reverse_lazy

We can use `reverse_lazy` in exactly the same way. Its benefit is that it "lazily" constructs the URL, so it works even if that URL file hasn't been loaded yet!

### url Template Tag

In a template, we can use the `{% url %}` template tag to accomplish the same goal:

```html
<a href="{% url 'news-year-archive' 2012 %}">2012 Archive</a>
```

Or with the year in a template context variable:

```html
<ul>
{% for year in year_list %}
<li><a href="{% url 'news-year-archive' yearvar %}">{{ year }} Archive</a></li>
{% endfor %}
</ul>
```

How could we use the `{% url %}` template tag in our music app?

## 🌴 [**10m**] BREAK

## 💻 [**65m**] **Activity**: Personal Wiki (makewiki)

> ⚠️ **IMPORTANT NOTE BEFORE YOU START** ⚠️ <br>
> To ensure the best development experience, **_carefully and mindfully_** follow each instruction <font color="red">**_exactly_**</font> as written. _No exceptions_. Blocked? Raise your hand and let us know!

### Setup From Starter Code

 **⭐️ IMPORTANT**: Change **YOUR_GITHUB_USERNAME** before hitting `<ENTER>` on the last step.<br>**✅ EXAMPLE**: Change `git remote add https://github.com/YOUR_GITHUB_USERNAME/makewiki` to `git remote add https://github.com/droxey/makewiki` for [Dani](https://github.com/droxey/makewiki)'s version of the `makewiki` project.

1. **In your browser**, create a **[new public repository](https://github.com/new)** on GitHub called `makewiki`.
2. **In your terminal**, navigate to the directory where you store your projects.
3. **Paste each line below** into the terminal, *one by one*. **Hit `<Return>` after *each* line**:

    ```bash
    git clone https://github.com/make-school-labs/makewiki-starter makewiki
    cd makewiki
    rm -rf .git
    git init
    git remote add origin https://github.com/YOUR_GITHUB_USERNAME/makewiki
    ```

4. **Open the `makewiki` repository folder** in your IDE.

### Starting the Challenges

1. **REQUIRED**: Complete challenges in each of these files, in order:
    1. `makewiki/urls.py`
    1. `wiki/views.py`
    1. `wiki/urls.py`
    1. `templates/base.html`

You will also need to create template files in `wiki/templates/wiki` for the list and detail pages that extend `base.html`. The naming of those files is up to you!

**TIP**: Find all challenges by searching the project for instances of the word CHALLENGE. To search all files in your project directory, press <Command> + <Shift> + <F>, type CHALLENGE, and hit <Return>.

## Wrap-Up

Continue working on your [tutorial part 4](https://docs.djangoproject.com/en/2.2/intro/tutorial04/) (due next class) and the [music site]() mini-project (due in 1 week).

## 📚 Resources & Credits

- **Docs**: Built-in [Template Tags](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-tag-reference) list
- **Docs**: Built-in [Filters](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#built-in-filter-reference) list
- **Docs**: How to Implement [Custom Tags and Filters](https://docs.djangoproject.com/en/2.2/howto/custom-template-tags/)
