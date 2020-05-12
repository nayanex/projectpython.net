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
