---
tags:
  - code
status: 
  - writing_idea  
---

Tags:
	- [[Django]]

```python
from django.db import models

class Something(models.Model):
    created_datetime = models.DateTimeField(auto_now_add=True)
	...
    title = models.CharField(max_length=100)
	...
    maker = models.ManyToManyField(
        'projects.Maker', related_name="podcast_episodes", blank=True
    )

    def __str__(self):
        return f"{self.title}"

```



```html
<div>
  {% for project in episode.project.all %}
	{{ project.website_title }}
	{%if not forloop.last%}and{%endif%}
  {% endfor %}
</div>
```