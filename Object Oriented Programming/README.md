# Object Oriented Programming

> Resource: Crash Course on Python from Google IT Automation with Python Professional Certificate

Let’s add a docstring to the greeting method.

```python
class Person:
  def __init__(self, name):
    self.name = name
  def greeting(self):
    """Outputs a message with the name of the person"""
    print("Hello! My name is {name}.".format(name=self.name)) 

help(Person.greeting)
```

Output:
```
Help on function greeting in module __main__:

greeting(self)
    Outputs a message with the name of the person
```
