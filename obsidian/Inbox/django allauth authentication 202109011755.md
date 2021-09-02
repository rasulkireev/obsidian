---
status:
  - writing_idea
tags:
  - code
---

Tags:
  - [[Django]]
  - [[Authenication]]
  - [[django-allauth]]


- if in normal user authentication you use `{{ form.username }}` then in django-allauth you need to use `{{ form.login }}`

- if you are having issues with twitter login, make sure that th callback ur is the same as you provided in the urls.py. for me for example it was users vs. accounts.