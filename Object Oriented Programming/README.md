# Object Oriented Programming

> Resource: Crash Course on Python from Google IT Automation with Python Professional Certificate

The Python `help` function can be super helpful for easily pulling up documentation for classes and methods. We can call the **help** function on one of our classes, which will return some basic info about the methods defined in our class:
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

## Inheritance

```python
class Clothing:
  material = ""
  def __init__(self,name):
    self.name = name
  def checkmaterial(self):
	  print("This {} is made of {}".format(self.name,self.material))
			
class Shirt(Clothing):
  material="Cotton"

polo = Shirt("Polo")
polo.checkmaterial()
```

Output:
````
This Polo is made of Cotton

Nice work! You used the existing Clothing class to make a
Shirt class that inherited from it!
```