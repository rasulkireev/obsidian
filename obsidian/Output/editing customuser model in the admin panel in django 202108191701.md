---
status:
  - writing_idea
tags:
  - code
---

when you have a custom user model in [[Django]], usually you want to extend the model to include other items like profile image, like so:

```python

# users/models.py

class CustomUser(AbstractUser):
    profile_image = models.ImageField(
        upload_to="user_profile_image/", blank=True
    )
    class Meta:
        db_table = "auth_user"
```

by default you will not be able to edit that new field in the admin panel. so, in order to be able to edit this custom field in the admin panel you need to cusotmize it like so:

```python
# users/admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    model = CustomUser

    fieldsets = UserAdmin.fieldsets + (
            ('Extra Fields', {'fields': ('profile_image',)}),
    )


admin.site.register(CustomUser, CustomUserAdmin)

```