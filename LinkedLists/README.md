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

Write a method `find` of the `Node` class that is passed a data item as parameter, and returns a reference to the first node in the linked list containing that item, or `None` if the item is not found. (Use a loop to search for the item.)

```python
class Node:
    def __init__(self, data):
        self.data = data  # instance variable to store the data
        self.next = None  # instance variable with address of next node

    # Write your find method here:
    def my_find(self, data):
        current = self
        while data != current.data:
            current = current.next
        return current if current else None

    def find(self, data):
        current = self
        while(current != None):
            if current.data == data:
                return current
            current = current.next
        return None

# The head is the first node in a linked list.
head = Node("Maine")
another_node = Node("Idaho")
head.next = another_node
a_third_node = Node("Utah")
another_node.next = a_third_node

print("Found:  " + str(head.find("Utah").data))
```

## Exercise: recursive find

Objective: write a method that implements a recursive algorithm on a simple linked list.

Write a method `find` of the `Node` class that is passed a data item as parameter, and returns a reference to the first node in the linked list containing that item, or `None’ if the item is not found. This time, write the method to search for the item recursively. Specifically, one of the following three things is true: we have found the item in the current node, we are at the end of the list, or the node is in the linked list starting at the next item. Your solution should not use any for-loops or while-loops.

```python
class Node:
    def __init__(self, data):
        self.data = data  # instance variable to store the data
        self.next = None  # instance variable with address of next node

    #  Write your find method here:
    def find(self, data):
        if data == self.data:
            return self
        if self.next == None:
            return None
        return self.next.find(data)

# The head is the first node in a linked list.
head = Node("Maine")
another_node = Node("Idaho")
head.next = another_node
a_third_node = Node("Utah")
another_node.next = a_third_node

print("Found:  " + str(head.find("Utah").data))
```

## Circular, doubly linked list with a sentinel

We did some things manually in the above example. It would be nice to have a class for a linked list that stored the address of the first node, and that also provided methods for inserting into, deleting from, appending to, and finding items in the list.

Our previous model for a linked list, in which only the address of the next node is stored in any node, has some annoying special cases. We will therefore start with a slightly different implementation that has a few convenient features that at first blush might seem more complicated, but actually simplifies the implementation of certain methods, and even improves the running time of certain methods.

1. The list will be **doubly linked**: each node will contain a reference to the _previous_ node in the chain (in a `prev` instance variable) as well as a reference to the next node. This structure not only makes it easy to iterate backward through the list, but it makes other, more common, operations easy, too.

2. The list will have a sentinel node, instead of a reference to a first node. This sentinel node is a special node that acts as the 0th node in the linked list. No data is stored in this special node; it’s there just as a placeholder in the list.

3. The list will be circular. The last node containing data will hold in its `next` instance variable the address of the sentinel node, and the sentinel node’s `prev` instance variable will hold the address of the last node.

We call this structure a **circular, doubly linked list with a sentinel**. Quite a mouthful, indeed. Practice saying it fast.

A circular, doubly linked list with a sentinel has the property that every node references a next node and a previous node. Always. This uniform way of treating nodes turns out to be quite convenient, because as we write methods to insert or delete nodes into the list, we don’t have to worry about special cases that would arise if the last node didn’t have a next node, and the first node didn’t have a previous node, but all interior nodes had both.

Here is a picture of a circular, doubly linked list with a sentinel representing the same list as before:

![alt text](http://projectpython.net/chapter17/xstates-DLL.png.pagespeed.ic.STByuOn0dn.png)

We create a class, `Sentinel_DLL`, to implement a circular, doubly linked list with sentinel

```python
# sentinel_DLL.py
# CS 1 class example for a circular, doubly linked list with a sentinel.
# by db, thc

# Class for a node in a circular, doubly linked list with a sentinel.
class Node:
    def __init__(self, data):
        self.data = data  # instance variable to store the data
        self.next = None  # instance variable with address of next node
        self.prev = None  # instance variable with address of previous node

    # Return the data in the Node.
    def get_data(self):
        return self.data

# Class for a circular, doubly linked list with a sentinel.
class Sentinel_DLL:
    # Create the sentinel node, which is before the first node
    # and after the last node.
    def __init__(self):
        self.sentinel = Node(None)
        self.sentinel.next = self.sentinel
        self.sentinel.prev = self.sentinel

    # Return a reference to the first node in the list, if there is one.
    # If the list is empty, return None.
    def first_node(self):
        if self.sentinel.next == self.sentinel:
            return None
        else:
            return self.sentinel.next

    # Insert a new node with data after node x.
    def insert_after(self, x, data):
        y = Node(data)   # make a new Node object.

        # Fix up the links in the new node.
        y.prev = x
        y.next = x.next

        # The new node follows x.
        x.next = y

        # And it's the previous node of its next node.
        y.next.prev = y

    # Insert a new node at the end of the list.
    def append(self, data):
        last_node = self.sentinel.prev
        self.insert_after(last_node, data)

    # Insert a new node at the start of the list.
    def prepend(self, data):
        self.insert_after(self.sentinel, data)

    # Delete node x from the list.
    def delete(self, x):
        # Splice out node x by making its next and previous
        # reference each other.
        x.prev.next = x.next
        x.next.prev = x.prev

    # Find a node containing data, and return a reference to it.
    # If no node contains data, return None.
    def find(self, data):
        # Trick: Store a copy of the data in the sentinel,
        # so that the data is always found.
        self.sentinel.data = data

        x = self.first_node()
        while x.data != data:
            x = x.next

        # Restore the sentinel's data.
        self.sentinel.data = None

        # Why did we drop out of the while-loop?
        # If we found the data in the sentinel, then it wasn't
        # anywhere else in the list.
        if x == self.sentinel:
            return None     # data wasn't really in the list
        else:
            return x        # we found it in x, in the list

    #  Return the string representation of a circular, doubly linked
    #  list with a sentinel, just as if it were a Python list.
    def __str__(self):
        s = "["

        x = self.sentinel.next
        while x != self.sentinel:  # look at each node in the list
            if type(x.data) == str:
                s += "'"
            s += str(x.data)        # concatenate this node's data
            if type(x.data) == str:
                s += "'"
            if x.next != self.sentinel:
                s += ", "   # if not the last node, add the comma and space
            x = x.next

        s += "]"
        return s
```

## Creating an empty list: `__init__`

A `Sentinel_DLL` object has just one instance variable: `sentinel`. This instance variable is a reference to a `Node` object. I defined the `Node` class in the sentinel_DLL.py file, rather than defining it in its own file, because it’s meant only to be part of a circular, doubly linked list with a sentinel.

In order for the list to be circular, both the `next` and `prev`` instance variables of the sentinel node must contain the address of the sentinel itself. Here’s what an empty list looks like:

![alt text](https://www.cs.dartmouth.edu/~scot/cs10/lectures/6/empty-DLL.gif)

It can at first be intimidating to see a line with as many dot operators in it as

`self.sentinel.next = self.sentinel`

Just work left to right for each variable. `self` is the address of a `sentinel_DLL` object. `self.sentinel` is the value of the `sentinel` instance variable in the `sentinel_DLL` object. We know that this value contains the address of some `Node` object. So `self.sentinel.next` is the `next` instance variable of the sentinel node in the `sentinel_DLL` object. That’s what we’re assigning to. The value we’re assigning is `self.sentinel`, the address of the sentinel node.

## Finding the first node

The `first_node` method just returns a reference to the first node in the list, or `None` if the list contains just the sentinel. The first node is always the one after the sentinel. If the node just after the sentinel is the sentinel itself, then the list contains just the sentinel, and the method returns `None`. Otherwise, the method returns a reference to the first node.

## Inserting a new node into a list

To insert a new node into the list, we need to know which node we’re inserting it after. The parameter `x` is a reference to that node. The parameter `data` gives the data that we’re inserting.

First, the method creates a new `Node` object, referenced by `y`, to hold the data that we want to add to the list. Now we need to “splice” the new node into the list, just as you can splice a new section into a piece of rope or magnetic tape. In order to splice in the new node, we need to do a few things:

1. Make the links in the new node refer to the previous and next nodes in the list.
2. Make the `next` link from the node that will precede the new node refer to the new node.
3. Make the `prev` link from the node that will follow the new node refer to the new node.

We have to be a little careful about the order in which we do these operations. Let’s name the nodes for convenience. We already have `x` referencing the node that the new node, referenced by `y`, goes after. Let `z` reference the next node after `x` before we insert `y`, so that `y` is supposed to go between `x` and `z`. If we clobber the value of the next instance variable of `x` too soon, we won’t have a way to get the address of `z`, which we will need.

It’s good to be comfortable with the dot notation used so heavily in the code, but it may help you to draw a picture. Here’s the same method as above, but with a temporary variable introduced for `z`:

```python
 # Insert a new node with data after node x.
def insert_after(self, x, data):
    y = Node(data)   # make a new Node object.
    z = x.next       # y goes between x and z

    # Fix up the links in the new node.
    y.prev = x
    y.next = z

    # The new node follows x.
    x.next = y

    # And it's the previous node of z.
    z.prev = y
```

## Iterating over a list

The `__str__` method shows an example of how to iterate over a list. The first node in the list is the node after the sentinel. We loop over nodes, letting `x` reference each node in the list, until returning to the sentinel again (recall that the list is circular). To get to the next node in the list, we use the line `x = x.next`.

One other interesting thing about the `__str__` method is that I wrote it to produce the same string as you’d see if the linked list were a regular Python list. When Python prints a list, it puts single quotes around all strings in the list. So I have a check to see whether `x.data` is a string, and if it is, I add in the single quotes. I use the built-in Python function `type`, which returns the type of its argument. (You can play with this function in the Python interpreter, IDLE.)

## Deleting from a list

The `delete` method takes a node `x` and deletes it from the list. It’s deceptively simple in how it splices the node out, by just making its next and previous nodes reference each other. Just we did for insertion, let’s rewrite the `delete` method, but with `y` referencing `x`’s previous node and `z` referencing `x`’s next node:

```python
# Delete node x from the list.
def delete(self, x):
    # Splice out node x by making its next and previous
    # reference each other.
    y = x.prev
    z = x.next
    y.next = z
    z.prev = y
```

## Searching a list

The `find` method searches the linked list for a node with a given data value, returning a reference to the first node that has the value, or `None` if no nodes have the value. It uses linear search, but in a linked list.

There’s a cute trick that I’ve incorporated into my implementation of `find`. If you go back to the linear search code that we saw before, you’ll notice that each loop iteration makes two tests: one to check that we haven’t reached the end of the list and one to see whether the list item matches what we’re searching for:

```python
def linear_search(the_list, key):
    index = 0
    while index < len(the_list):
        if key == the_list[index]:
            return index
        else:
            index += 1
    return None
```

Suppose that you knew you’d find the item in the list. Then you wouldn’t have to check for reaching the end of the list, right? So let’s put the value we’re looking for into the linked list, but in a special place that tells us if that’s where we find it, then the only reason we found it was because we looked everywhere else before finding it in that special place.

Gosh, if only we had an extra node in the list that didn’t contain any data and was at the end of the list. We do: the sentinel. So we put the value we’re looking for in the sentinel’s `data` instance variable, start at the first node after the sentinel, and loop until we see a match. If the match was not in the sentinel, then we found the value in the list. If the match was in the sentinel, the the value wasn’t really in the list; we found it only because we got all the way back to the sentinel. In either case, we put `None` back into the sentinel’s `data` instance variable because, well, my mother told me to.

## Appending to the list

The only other method in my `Sentinel_DLL` class is `append`. Not surprisingly, it finds the last node in the list and then calls `insert_after` for that node. How to find the last node in the list? It’s just the sentinel’s previous node.

## Running times of the linked-list operations

What are the worst-case running times of the operations for a circular, doubly linked list with a sentinel? Let’s assume that the list has n items (n + 1 nodes, including the sentinel, but of course the  + 1 won’t matter when we use asymptotic notation).

The `__init__`, `first_node`, `insert_after`, `append`, and `delete` methods each take Θ(1) time, since they each look at only a constant number of nodes.

The `__str__` method takes Θ(n) time, since it has to visit every node once.

The time taken by the `find` method depends on how far down the linked list it has to go. In the worst case, the value is not present, and `find` has to examine every node once, for a worst-case running time of Θ(n).

## Testing the linked list operations

You can test the linked list operations by writing your own driver. I have a pretty minimal driver here:

```python
# test_sentinel_DLL.py
# CS 1 class example by THC.
# Tests the Sentinel_DLL class.

from sentinel_DLL import Sentinel_DLL

def test_sentinel_DLL():
    # Make a linked list with Maine, Idaho, and Utah.
    l = Sentinel_DLL()
    l.append("Maine")
    l.append("Idaho")
    l.append("Utah")

    # Add Ohio after Idaho.
    node = l.find("Idaho")
    if node != None:
        print(node.get_data())
        l.insert_after(node, "Ohio")
    print(l)

    # Delete Idaho.
    if node != None:
        l.delete(node)
    print(l)

    # Empty out the list, one node at a time.
    while l.first_node() != None:
        l.delete(l.first_node())

    print(l)

test_sentinel_DLL()
```

Output:

```
Idaho
['Maine', 'Idaho', 'Ohio', 'Utah']
['Maine', 'Ohio', 'Utah']
[]
```

## Add Two Numbers

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
-------------------------------------
Input:
[1,8]
[0]
Expected:
[1,8]
-------------------------------------
Input:
[5]
[5]
Expected:
[1,0]
-------------------------------------
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

#     def __str__(self):
#       s = "["
#       x = self
#
#       while x != None:
#           s += "'"
#           s += str(x.val)
#           s += "'"
#
#           if x.next != None:
#               s += ", "
#           x = x.next

#       s += "]"
#       return s

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        l3 = ListNode()
        curr_l3 = l3
        carry = 0

        while l1 or l2:
            addend1 = l1.val if l1 else 0
            addend2 = l2.val if l2 else 0

            nodes_sum = addend1 + addend2 + carry
            carry, nodes_sum = divmod(nodes_sum, 10)
            curr_l3.val = nodes_sum

            if l1:
                l1 = l1.next

            if l2:
                l2 = l2.next

            if l1 or l2:
                curr_l3.next = ListNode()
                curr_l3 = curr_l3.next
            elif carry != 0:
                curr_l3.next = ListNode(carry)

        return l3

```
