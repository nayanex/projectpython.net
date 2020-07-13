# Stacks and Queues

http://projectpython.net/chapter16/

## Stacks

A stack data structure models a familiar way of organizing objects in the physical world: stacked objects. When you add an object to the stack, it’s added to the top of the stack. When you take an object off of the stack, it’s taken off the top of the stack. In order to access the bottom plate of a stack of heavy plates, you might first have to take off all of the plates above it one by one, starting from the top. We say that the stack is “last in, first out” for this reason.

Here is a visualization of a stack of numbered bricks, written by Dartmouth student Daniel Shanker. Click on a brick to push it onto the stack in the correct order.

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

We will need operations to **enqueue** data items at the end of the queue, and **dequeue** items from the front. Here is a visualization of a queue (written by Dartmouth student Daniel Shanker), with enqueue and dequeue operations. Try to mimic the following sequence (each character’s name is denoted by the letter next to them, and you can enqueue them by clicking on them): Dave and Eliza get in line to buy movie tickets, followed shortly by Alice. Dave is served. Before Eliza is served, Carol and Betty get in line. At that point there are only two tickets left, so only Alice and Carol are served.

```python
class Queue:
   def __init__(self):
        self.items = []

    def enqueue(self, x):
        self.items.append(x)

    def dequeue(self):
        return self.items.pop(0)

    def empty(self):
        return self.items == []

    def __str__(self):
        return str(list(self.items))

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
```
