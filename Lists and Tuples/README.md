# Lists and Tuples

> Resource: Crash Course on Python from Google IT Automation with Python Professional Certificate

https://www.coursera.org/professional-certificates/google-it-automation

## Exercise 1

Given a list of filenames, we want to rename all the files with extension `hpp` to the extension `h`. To do this, we would like to generate a new list called newfilenames, consisting of the new filenames. 

```python
filenames = ["program.c", "stdio.hpp", "sample.hpp", "a.out", "math.hpp", "hpp.out"]
# Generate newfilenames as a list containing the new filenames
# using as many lines of code as your chosen method requires.
newfilenames = []
for filename in filenames:
    if ".hpp" in filename[-4:]:
        newfilenames.append(filename[:-2])
        continue
    newfilenames.append(filename)

print(newfilenames) 
# Should be ["program.c", "stdio.h", "sample.h", "a.out", "math.h", "hpp.out"]
```

## Exercise 2

Let's create a function that turns text into **pig latin**: a simple text transformation that modifies each word moving the first character to the end and appending "ay" to the end. For example, `python` ends up as `ythonpay`.

```python
def pig_latin(text):
  say = ""
  # Separate the text into words
  words = text.split()
  for word in words:
    # Create the pig latin word and add it to the list
    say += word[1:] + word[0] + "ay "
    # Turn the list back into a phrase
  return say[:-1]
		
print(pig_latin("hello how are you")) # Should be "ellohay owhay reaay ouyay"
print(pig_latin("programming in python is fun")) # Should be "rogrammingpay niay ythonpay siay unfay"
```

## Exercise 3 

The permissions of a file in a Linux system are split into three sets of three permissions: `read`, `write`, and `execute` for the `owner`, `group`, and `others`. Each of the three values can be expressed as an `octal` number summing each permission, with `4 corresponding to read, 2 to write, and 1 to execute`. Or it can be written with a string using the letters `r`, `w`, and `x` or `-` when the permission is not granted. For example: `640` is `read/write` for the `owner`, `read` for the `group`, and `no permissions` for the `others`; converted to a string, it would be: "rw-r-----" `755` is `read/write/execute` for the `owner`, and `read/execute` for `group` and `others`; converted to a string, it would be: "rwxr-xr-x". Write code to convert a permission in octal format into a string format.

```python
def octal_to_string(octal):
    result = ""
    value_letters = [(4,"r"),(2,"w"),(1,"x")]
    # Iterate over each of the digits in octal
    for permission in [int(n) for n in str(octal)]:
        # Check for each of the permissions values
        for value, letter in value_letters:
            if permission >= value:
                result += letter
                permission -= value
            else:
                result += "-"
    return result
    
print(octal_to_string(755)) # Should be rwxr-xr-x
print(octal_to_string(644)) # Should be rw-r--r--
print(octal_to_string(750)) # Should be rwxr-x---
print(octal_to_string(600)) # Should be rw-------
```

## Exercise 4

The group_list function accepts a group name and a list of members, and returns a string with the format: group_name: member1, member2, … For example, group_list("g", ["a","b","c"]) returns "g: a, b, c". Write code to do that.

```python
def group_list(group, users):
  members = ", ".join(users)
  return group + ": " + members

print(group_list("Marketing", ["Mike", "Karen", "Jake", "Tasha"])) # Should be "Marketing: Mike, Karen, Jake, Tasha"
print(group_list("Engineering", ["Kim", "Jay", "Tom"])) # Should be "Engineering: Kim, Jay, Tom"
print(group_list("Users", "")) # Should be "Users:"
```

## Exercise 5

The guest_list function reads in a list of tuples with the name, age, and profession of each party guest, and prints the sentence "Guest is X years old and works as __." for each one. For example, guest_list(('Ken', 30, "Chef"), ("Pat", 35, 'Lawyer'), ('Amanda', 25, "Engineer")) should print out: Ken is 30 years old and works as Chef. Pat is 35 years old and works as Lawyer. Amanda is 25 years old and works as Engineer. 

```python
  def guest_list(guests):
    for name, age, profession in guests:
      print("{} is {} years old and works as {}".format(name, age, profession))

  guest_list([('Ken', 30, "Chef"), ("Pat", 35, 'Lawyer'), ('Amanda', 25, "Engineer")])

"""
Output should match:
Ken is 30 years old and works as Chef
Pat is 35 years old and works as Lawyer
Amanda is 25 years old and works as Engineer
"""
```

## Oficial Python Documentation for Lists and Tuples
```
https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range
https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types
https://docs.python.org/3/library/stdtypes.html#lists
https://docs.python.org/3/tutorial/datastructures.html
```