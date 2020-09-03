# Strings

> Resource: Crash Course on Python from Google IT Automation with Python Professional Certificate

https://www.coursera.org/professional-certificates/google-it-automation

```python
def replace_domain(email, old_domain, new_domain):
  if "@" + old_domain in email:
    index = email.index("@" + old_domain)
    new_email = email[:index] + "@" + new_domain
    return new_email
  return email
```
