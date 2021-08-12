This is me writing down the process for creating a simple Django app. Couple of caveats:
- the app will be "managed" through Admin (no user interaction)
- all the data will be displayed on a page
- there will be detail view with


## 1. Create the app

```bash
# run in terminal
python manage.py startapp {name}
```

## 2. Register the app in `settings.py`

```python
# {project_name}/setting.py
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
	...
    "{name}.apps.{name}Config",
]
```

## 3. Create a model(s) for the app

```python
# {app_name}/models.py
from django.db import models

class Something(models.Model):
    created_datetime = models.DateTimeField(auto_now_add=True)
    updated_datetime = models.DateTimeField(auto_now=True)

    title = models.CharField(max_length=100)
    description = models.TextField(blank=True)

    def __str__(self):
        return f"{self.title}"
```

Once you are done, run the following:

```bash
# run in terminal
python manage.py makemigrations {app_name}
python manage.py migrate
```

## 4. Register the model in the admin view

```python
# {app_name}/admin.py

from django.contrib import admin
from .models import Something

admin.site.register(Something)
```

## 5. Set up the urls

```python
# in {project_name}/urls.py modify the `urlpatterns` tuple

urlpatterns = (
    [
        path("admin/", admin.site.urls),
		...
        path("{app_name}/", include("{app_name}.urls")),
		...
    ]
    + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
    + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
)
```

Then create the `urls.py` file in your new app directory:

```python
# {app_name}/urls.py
# note that the view does not exists yet. Will create in the next step
# Change the the name of the name as you see fit. Standard practice is to say SomethingListView, where something is whatever you are displaying.

from django.urls import path
from .views import PodcastListView

urlpatterns = [
    path("", PodcastListView.as_view(), name="podcast_episodes"),
]
```

## 6. Create the View
Creating the view is necessary to pass the data to the page.

```python
# in {app_name}/views.py

from django.views.generic import ListView
from .models import Something

# note: the name of the class needs to be the same as you created in urls.py
class SomethingListView(ListView):
    model = Something
	# the template name is saying to which file/template to "send" the data
	# for me all the templates sit in the "templates" folder in at the root of the project
    template_name = "{app_name}/all_episodes.html"
    queryset = Something.objects.all()
```

Then head over to the templates directory and create a `{app_name}` folder in it. Inside that folder create a `all_episodes.html` or whatever else you named it in the `views.py` file.

```html
<!-- in templates/{app_name}/all_episodes.html -->
{% extends 'base.html' %}
{% load static %}

{% block content %}

{% for episode in object_list %}
    <p>{{ episode.title }}</p>
{% endfor %}

{% endblock content %}
```

Above is a super basic template. We are:
1. extending the base.html
2. looping over the object list. Since we have told our view to "push" the data to this template we can access it via this handy name.
3. access the model fields 

👍