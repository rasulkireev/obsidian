---
status:
  - writing_idea
tags:
  - code
---

Don't forget to use the following syntax in the tempalte `{{ object.company.jobs.all }}`.

to test in `poetry run python manage.py shell`

run the follwofin:

```
buttondown = Project.objects.filter(website_title="Buttondown")[0]
```

then 

```
>>> buttondown.company.jobs
<django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager object at 0x10c53b510>
```

vs.

```
>>> buttondown.company.jobs.all()
<QuerySet [<Job: Posthog: Sfotware Engineer II>, <Job: Posthog: Senior Software Engineer - Back End focus>]>
```

https://stackoverflow.com/questions/33676289/django-db-models-fields-related-relatedmanager-object-at-0x7ff4e003d1d0-is-not