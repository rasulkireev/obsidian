This is me writing down the process for creating a simple Django app. Couple of caveats:
- the app will be "managed" through Admin (no user interaction)
- all the data will be displayed on a page
- there will be detail view with


## 1. Create the app

```
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

```
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


```