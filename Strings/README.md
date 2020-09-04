# Strings

> Resource: Crash Course on Python from Google IT Automation with Python Professional Certificate

https://www.coursera.org/professional-certificates/google-it-automation

## Exercise: Outdated email addresses

 Imagine that your company has recently moved to using a new domain, but a lot of the company email addresses are still using the old one. You want to write a program that replaces this old domain with the new one in any outdated email addresses.

```python
def replace_domain(email, old_domain, new_domain):
  if "@" + old_domain in email:
    index = email.index("@" + old_domain)
    new_email = email[:index] + "@" + new_domain
    return new_email
  return email
```

## Exercise: Initials

Fill in the gaps in the initials function so that it returns the initials of the words contained in the phrase received, in upper case. For example: "Universal Serial Bus" should return "USB"; "local area network" should return "LAN”.

```python
def initials(phrase):
    words = phrase.split()
    result = ""
    for word in words:
        result += word[0]
    return "".join(result).upper()

print(initials("Universal Serial Bus")) # Should be: USB
print(initials("local area network")) # Should be: LAN
print(initials("Operating system")) # Should be: OS
```

## String Formatting

We can use string formatting to make the output of our program look nice and also to generate useful logging and debugging messages. Formatting strings can help to create more informative error messages. They help understanding what's going on with a script that's failing.

You can use the **format** method on strings to concatenate and format strings in all kinds of powerful ways. To do this, create a string containing curly brackets, **{}**, as a placeholder, to be replaced. Then call the format method on the string using **.format()** and pass variables as parameters. The variables passed to the method will then be used to replace the curly bracket placeholders. This method automatically handles any conversion between data types for us. 

If the curly brackets are empty, they’ll be populated with the variables passed in the order in which they're passed. However, you can put certain expressions inside the curly brackets to do even more powerful string formatting operations. You can put the name of a variable into the curly brackets, then use the names in the parameters. This allows for more easily readable code, and for more flexibility with the order of variables.

You can also put a formatting expression inside the curly brackets, which lets you alter the way the string is formatted. For example, the formatting expression **{:.2f}** means that you’d format this as a float number, with two digits after the decimal dot. The colon acts as a separator from the field name, if you had specified one. You can also specify text alignment using the greater than operator: >. For example, the expression **{:>3.2f}** would align the text three spaces to the right, as well as specify a float number with two decimal places. String formatting can be very handy for outputting easy-to-read textual output.

## Exercise: Format Strings

Modify the student_grade function using the format method, so that it returns the phrase "X received Y% on the exam". For example, student_grade("Reed", 80) should return "Reed received 80% on the exam".

```python
def student_grade(name, grade):
	return "{name} received {grade}% on the exam".format(name=name, grade=grade)

print(student_grade("Reed", 80))
print(student_grade("Paige", 92))
print(student_grade("Jesse", 85))
```

Output:
```
Here is your output:
Reed received 80% on the exam
Paige received 92% on the exam
Jesse received 85% on the exam

You got it! Your string formatting skills are coming along
nicely!
```

One of the things we can put inside the curly brackets is the name of the variable we want in that position to make the whole string more readable. This is particularly relevant when the text can get rewritten or translated and the variables might switch places.

Because we're using placeholders with variable names, the order in which the variables are passed to the format function doesn't matter. But for this to work, we need to set the names we're going to use and assign a value to them inside the parameters to format. And that's just the tip of the iceberg of what we can do with the format method.

## Exercise: Fahrenheit to Celsius - ºF to ºC conversion

 Our conversion table can look kind of ugly because it might be full of float numbers containing too many decimal digits. Using the format function, we can make it look a lot nicer. In these two expressions we're using the greater than operator to align text to the right so that the output is neatly aligned. In the first expression we're saying we want the numbers to be aligned to the right for a total of three spaces. In the second expression we're saying we want the number to always have exactly two decimal places and we want to align it to the right at six spaces.

```python
def to_celsius(x):
  return (x-32)*5/9

for x in range(1, 101, 10):
  print("{:>3} F | {:>6.2f} C".format(x, to_celsius(x)))
```

Output:
```
  1 F | -17.22 C
 11 F | -11.67 C
 21 F |  -6.11 C
 31 F |  -0.56 C
 41 F |   5.00 C
 51 F |  10.56 C
 61 F |  16.11 C
 71 F |  21.67 C
 81 F |  27.22 C
 91 F |  32.78 C
```

## Exercise: Formatting Float Numbers

Let's say you want to output the price of an item with and without tax. Depending on what the tax rate is, the number might be a long number with a bunch of decimals. So if something costs $7.5 without tax and the tax rate is 9%, the price with tax would be $8.175. First off, ouch, and also, since there's no such thing as half a penny anymore, that number doesn't make sense. So to fix this we can make the format function print only two decimals, like this.

```python
price = 7.5
with_tax = price * 1.09
print(price, with_tax)
# 7.5 8.175

print("Base price: ${:.2f}. With tax: ${:.2f}".format(price, with_tax))
# Base price: $7.50. With tax: $8.18

```
In this case between the curly brackets we're writing a **formatting expression**. There are a bunch of different expressions we can write. These expressions are needed when we want to tell Python to format our values in a way that's different from the default. The expression starts with a `colon` to separate it from the field name that we saw before. After the colon, we write `.2f`. This means we're going to format a float number and that there should be two digits after the decimal dot. So no matter what the price is, our function always prints two decimals. 

## Oficial Python Documentation for Strings

https://docs.python.org/3/library/stdtypes.html#string-methods
https://docs.python.org/3/library/string.html#module-string
https://docs.python.org/3/reference/lexical_analysis.html#f-strings