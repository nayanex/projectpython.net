# Recursion

http://projectpython.net/chapter12/

## Exercise: sum positive numbers recursively

The function sum_positive_numbers should return the sum of all positive numbers between the number n received and 1. For example, when n is 3 it should return 1+2+3=6, and when n is 5 it should return 1+2+3+4+5=15. Fill in the gaps to make this work:

```python
def sum_positive_numbers(n):
    # The base case is n being smaller than 1
    if n < 1:
        return 0

    # The recursive case is adding this number to 
    # the sum of the numbers smaller than this one.
    return n + sum_positive_numbers(n - 1)

print(sum_positive_numbers(3)) # Should be 6
print(sum_positive_numbers(5)) # Should be 15
```


## Exercise: Recursive Factorial

```python
def factorial(n):
    print("Factorial called with " + str(n))
    if n < 2:
        print("Returning 1")
        return 1
    result = n * factorial(n - 1)
    print("Returning " + str(result) + " for factorial of " + str(n))
    return result

factorial(4)
```

Output:
```
Factorial called with 4
Factorial called with 3
Factorial called with 2
Factorial called with 1
Returning 1
Returning 2 for factorial of 2
Returning 6 for factorial of 3
Returning 24 for factorial of 4
```

## Exercise: Is Power of 

Build a `is_power_of` function to return whether the number is a power of the given base. **Note:** base is assumed to be a positive number. **Tip:** for functions that return a boolean value, you can return the result of a comparison.

```python
def is_power_of(number, base):
  # Base case: when number is smaller than base.
  if number < base:
    # If number is equal to 1, it's a power (base**0).
    return base**0 == number

  # Recursive case: keep dividing number by base.
  return is_power_of(number / base, base)

print(is_power_of(8,2)) # Should be True
print(is_power_of(64,4)) # Should be True
print(is_power_of(70,10)) # Should be False
```

## Exercise: Count number of users

The `count_users` function recursively counts the amount of users that belong to a group in the company system, by going through each of the members of a group and if one of them is a group, recursively calling the function and counting the members. 

```python
def count_users(group):
  count = 0
  for member in get_members(group):
    if is_group(member):
      count += count_users(member)
    else:
      count += 1
  return count

print(count_users("sales")) # Should be 3
print(count_users("engineering")) # Should be 8
print(count_users("everyone")) # Should be 18
```

## Recursion Error

It's important to call out that in some languages there's a maximum amount of recursive calls you can use. In Python by default, you can call a recursive function 1000 times until you reach the limit. That's fine for things like subdirectories or user groups that aren't thousands of levels deep. But it might not be enough for mathematical functions.

```python
factorial(1000)
```

Output:
```
RecursionError: maximum recursion depth exceeded while calling a Python object
```

## Summary

A recursive function must include a recursive case and base case. The recursive case calls the function again, with a different value. The base case returns a value without calling the same function.

A recursive function will usually have this structure:

```python
def recursive_function(parameters):
    if base_case_condition(parameters):
        return base_case_value
    recursive_function(modified_parameters)
```

> You are not facing big obstacles, mostly you are facing opportunities for growth. =ˆ)