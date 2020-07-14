# Stacks and Queues

http://projectpython.net/chapter16/

## Stacks

A stack data structure models a familiar way of organizing objects in the physical world: stacked objects. When you add an object to the stack, it’s added to the top of the stack. When you take an object off of the stack, it’s taken off the top of the stack. In order to access the bottom plate of a stack of heavy plates, you might first have to take off all of the plates above it one by one, starting from the top. We say that the stack is “last in, first out” for this reason.

So, we need operations to *push* data items onto the top of the stack, and *pop* items off the top.

Sometimes, stacks and queues are referred to as **abstract data types**. In this case, abstract means that (just like in pseudocode) we don’t really care about some details of implementation. If a data structure allows items to be pushed and popped, following a *“last in, first out”* order, we say that it is a stack. If it quacks like a duck, it is a duck!

There are many ways to implement stacks and queues, and good reasons to choose particular implementations, such as the computational costs of push and pop operations, but we will focus on how stacks and queues can be used in algorithms. Fortunately, Python lists can be used as fine stacks, using the built-in append (to push data onto the back of the list) and pop methods.


```python
#  Uses a Python list as a stack, using the built-in append() and pop() methods
#  of Python lists.

my_stack = []

my_stack.append(1)
print("After pushing 1:  " + str(my_stack))

my_stack.append(2)
print("After pushing 2:  " + str(my_stack))

my_stack.append(50)
print("After pushing 50:  " + str(my_stack))

result = my_stack.pop()
print("After popping:  " + str(my_stack) +
      " (pop result was " + str(result) + ")")

my_stack.append(5)
print("After pushing 5:  " + str(my_stack))
```

**Output:**
```
After pushing 1:  [1]
After pushing 2:  [1, 2]
After pushing 50:  [1, 2, 50]
After popping:  [1, 2] (pop result was 50)
After pushing 5:  [1, 2, 5]
```

Sometimes, it’s nice to make a class describing a data structure. You should not be able to access the interior elements of a stack (that would probably indicate an error in your code) but if you are using a ‘bare’ Python list, you could do that without Python warning you. Here’s an implementation of a Stack class:

```python
# Wraps a list to create a Stack class
class Stack:
	def __init__(self):
		self.data = []

	def push(self, x):
		self.data.append(x)

	def pop(self):
		return self.data.pop()

	def empty(self):
		return len(self.data) == 0

	def __str__(self):
		return str(self.data)


my_stack = Stack()

my_stack.push(1)
print("After pushing 1:  " + str(my_stack))

my_stack.push(2)
print("After pushing 2:  " + str(my_stack))

my_stack.push(50)
print("After pushing 50:  " + str(my_stack))

my_stack.pop()
print("After popping:  " + str(my_stack))

my_stack.push(5)
print("After pushing 5:  " + str(my_stack))
```

**Output:**
```
After pushing 1:  [1]
After pushing 2:  [1, 2]
After pushing 50:  [1, 2, 50]
After popping:  [1, 2] (pop result was 50)
After pushing 5:  [1, 2, 5]
```

## Queues

When you get in line (or **enqueue**) for an amusement park ride, you have your spot in line. Nobody can cut in front of you, and you are guaranteed to get out from the front of the line (**dequeue**) before anybody behind you. Like stacks, queues allow for the ordering of objects while following a certain set of rules. Whereas stacks are “last in, first out,” queues are the opposite - “first in, first out.”

We will need operations to **enqueue** data items at the end of the queue, and **dequeue** items from the front. 

## Efficient implementations of stacks and queues

You might notice that for the stack implementation above, the worst-case run-time of appending an item is Θ(n) (although it’s only Θ(1) amortized over many appends). If you dequeue an item a queue by deleting an item from the front of a list, the run-time is Θ(n) in all cases. When Python deletes an item from the front of a list, the interpreter loops over all remaining items, shifting them one index earlier in the list.

An alternate implementation would use a data structure called a doubly-linked list for either one, allowing Θ(1) operations to add or remove items from the beginning or end of the list. Perhaps that is how the Python deque class is implemented. I’d recommend using a deque if you need a queue or a stack.

## Exercise: writing a Queue class

Objective: write a class that implements a data structure by wrapping a simple data type.

There may be many different ways to implement a data type such as Queue. We define the Queue based on the operations available on the Queue, not based on how it is implemented: a Queue is a data type that supports enqueue and dequeue operations. It’s convenient to have a class that handles the details of the implementation.

Write a Queue class that internally uses a list to keep the data in order. Your Queue class should have methods to enqueue an item, dequeue and return the item, empty which returns True if there are no more items on the Queue, and __str__ which returns a string representation of the queue.
(Hint: none of the bodies of these methods needs to be more than one line long.)


```python
class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, x):
        self.items.append(x)

    def dequeue(self):
        return self.items.pop(0)

    def empty(self):
        return not self.items

    def __str__(self):
        return str(self.items)

q = Queue()

q.enqueue("Dave")
print("Dave got in line:  " + str(q))

q.enqueue("Eliza")
print("Eliza got in line:  " + str(q))

q.enqueue("Alice")
print("Alice got in line:  " + str(q))

next = q.dequeue()
print(next + " is served:  " + str(q))

q.enqueue("Carol")
print("Carol got in line:  " + str(q))

q.enqueue("Betty")
print("Betty got in line:  " + str(q))

next = q.dequeue()
print(next + " is served:  " + str(q))

next = q.dequeue()
print(next + " is served:  " + str(q))

next = q.dequeue()
print(next + " is served:  " + str(q))

print("Is empty? " + str(q.empty()))

next = q.dequeue()
print(next + " is served:  " + str(q))

print("Is empty? " + str(q.empty()))
```

**Output:**
```
Dave got in line:  ['Dave']
Eliza got in line:  ['Dave', 'Eliza']
Alice got in line:  ['Dave', 'Eliza', 'Alice']
Dave is served:  ['Eliza', 'Alice']
Carol got in line:  ['Eliza', 'Alice', 'Carol']
Betty got in line:  ['Eliza', 'Alice', 'Carol', 'Betty']
Eliza is served:  ['Alice', 'Carol', 'Betty']
Alice is served:  ['Carol', 'Betty']
Carol is served:  ['Betty']
Is empty? False
Betty is served:  []
Is empty? True
```

## HackerRank Challenges

### Balanced Brackets

https://www.hackerrank.com/challenges/balanced-brackets

A bracket is considered to be any one of the following characters: `(`, `)`, `{`, `}`, `[`, or `]`.

Two brackets are considered to be a matched pair if the an opening bracket (i.e., (, [, or {) occurs to the left of a closing bracket (i.e., ), ], or }) of the exact same type. There are three types of matched pairs of brackets: [], {}, and ().

A matching pair of brackets is not balanced if the set of brackets it encloses are not matched. For example, `{[(])}` is not balanced because the contents in between { and } are not balanced. The pair of square brackets encloses a single, unbalanced opening bracket, (, and the pair of parentheses encloses a single, unbalanced closing square bracket, ].

By this logic, we say a sequence of brackets is balanced if the following conditions are met:

* It contains no unmatched brackets.
* The subset of brackets enclosed within the confines of a matched pair of brackets is also a matched pair of brackets.

Given **n** strings of brackets, determine whether each sequence of brackets is balanced. If a string is balanced, return`YES`. Otherwise, return `NO`.

**Function Description**

Complete the function `isBalanced` in the editor below. It must return a string: `YES` if the sequence is balanced or `NO` if it is not.

`isBalanced` has the following parameter(s):

`s`: a string of brackets

**Input Format**

The first line contains a single integer **n**, the number of strings.
Each of the next **n** lines contains a single string , a sequence of brackets.

**Constraints**

* 1 <= n >- 10^3
* 1 <= |s| <= 10^3, where |s| is the length of the sequence/
* All characters in the sequence ∈ { `{, }, (, ), [, ]` }.


**Output Format**

For each string, return YES or NO.

**Sample Input**

```
3
{[()]}
{[(])}
{{[[(())]]}}
```

**Sample Output**

```
YES
NO
YES
```

**Explanation**

1. The string `{[()]}` meets both criteria for being a balanced string, so we print `YES` on a new line.
2. The string `{[(])}` is not balanced because the brackets enclosed by the matched pair { and } are not balanced: [(]).
3. The string `{{[[(())]]}}` meets both criteria for being a balanced string, so we print `YES` on a new line.

```python
#!/bin/python3

import os

# Complete the isBalanced function below.
def isBalanced(s):
    stack = []
    for bracket in s:
        if bracket in ['(', '[', '{']:
            stack.append(bracket)
            continue
        if not stack: 
            return 'NO'
        top = stack.pop()
        if top == '{' and bracket != '}' or top == '[' and bracket != ']' or top == '(' and bracket != ')':
            return 'NO'
    if stack:
        return 'NO'
    return 'YES'
    

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    t = int(input())

    for t_itr in range(t):
        s = input()

        result = isBalanced(s)

        fptr.write(result + '\n')

    fptr.close()
```