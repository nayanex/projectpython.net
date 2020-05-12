# Linked lists

http://projectpython.net/chapter17/

## Nodes in the list

Conceptually, we will create a linked list by making lots of objects called nodes. Each `Node` object will contain an item: the data in the list. The `Node` objects themselves could be anywhere in memory, and will typically not be stored sequentially, or in any other particular order, in memory.

How, then, can we tell which item in the list is first, which is second, and what the order of items is? Each Node object will contain an instance variable that has the address of the next `Node` object in the linked list.

Let’s look at an example of how this might work. (I should emphasize that this is not yet a good implementation of a linked list. I just want to show you how nodes work.) Here’s a picture of a linked list holding the names of three states, in order: Maine, Idaho, and Utah:

![alt text](http://projectpython.net/chapter17/xstates-SLL.png.pagespeed.ic.-O6dD-qGcG.png)

The arrows indicate references. The slash in the `next` instance variable of the last `Node` object (the one whose data is `Utah`) is how I indicate the value `None` in a picture.

Here’s some simple code. Although we usually put a class in its own file, I didn’t put the `Node` class in its own node.py file because I wanted to keep this example short and in one place.

```python
class Node:
    def __init__(self, data):
        self.data = data  # instance variable to store the data
        self.next = None  # instance variable with address of next node

# The head is the first node in a linked list.
head = Node("Maine")

# Create a new node.
another_node = Node("Idaho")

# Store the address of the Idaho node as the
#  next address of the first node in the list.
head.next = another_node

# Create a third node.
a_third_node = Node("Utah")

# Link the second node to the third node.
another_node.next = a_third_node

# An example of printing the data of the list in order:
node = head   # copy the address of the head node into node
while node != None:
    print(node.data)
    node = node.next
```

When we printed the list, we created a new, temporary variable `node` that initially has the address of the first `Node` object in the linked list. We use that address to find the data to print (`Maine`), and then we update `node` to hold the address of the next item. We print its data (`Idaho`) and update `node` again to hold the address of the next item. We print its data (`Utah`), and update `node` once again. Now, `node` equals `None`, and we drop out of the while-loop.

## Exercise: linked list of even numbers

Objective: Write a program that adds several items to a linked list using a loop.

Write a program that adds all of the even numbers from 0 to 100 to a linked list, and then prints out all of the items in the list. To save some typing, a simple `Node` class is provided, as is the code to print the list. You will need to do several things to create the linked list.

1. Create a first node; call it `head`.
2. Create a variable `current` that will point to the node we are currently working on.
3. For each data item, create a node and store a reference to it in an instance variable of `current`. Then update `current` to point to the next node in the list we are building.

```python
class Node:
    def __init__(self, data):
        self.data = data  # instance variable to store the data
        self.next = None  # instance variable with address of next node

# write your code here:
head = Node(0)
current = head

def my_add_even_numbers_to_linked_list(current):
    for even_number in range(2, 102, 2):
        current.next = Node(even_number)
        current = current.next

def add_even_numbers_to_linked_list(current):
    for i in range(1, 51):
        current.next = Node(2 * i)
        current = current.next

my_add_even_numbers_to_linked_list(current)

# Print the data of the list in order:
current = head   # copy the address of the head node into node
while current != None:
    print(current.data)
    current = current.next
```

## Exercise: needle in a linked list

Objective: write a method that implements an algorithm on a simple linked list.

Write a method find of the Node class that is passed a data item as parameter, and returns a reference to the first node in the linked list containing that item, or `None’ if the item is not found. (Use a loop to search for the item.)
