# Dictionaries

> Resource: Crash Course on Python from Google IT Automation with Python Professional Certificate

Data in a dictionary is organized into pairs of keys and values. You use the key to access the corresponding value. Where a list index is always a number, a dictionary key can be a different data type, like a string, integer, float, or even tuples.

You can also check if a key is contained in a dictionary using the **in** keyword. Just like other uses of this keyword, it will return True if the key is found in the dictionary; otherwise it will return False.

Dictionaries are mutable, meaning they can be modified by adding, removing, and replacing elements in a dictionary, similar to lists. You can add a new key value pair to a dictionary by assigning a value to the key, like this: `animals["zebras"] = 2`. This creates the new key in the animal dictionary called zebras, and stores the value 2. You can modify the value of an existing key by doing the same thing. So `animals["bears"] = 11` would change the value stored in the bears key from 10 to 11. Lastly, you can remove elements from a dictionary by using the **del** keyword. By doing `del animals["lions"]` you would remove the key value pair from the animals dictionary.

Let's say for example that you're analyzing logs in your server and you want to count how many times each type of error appears in the log file. You could easily do this with a dictionary by using the type of error as the key and then incrementing the associated value each time you come across that error type.

https://www.coursera.org/professional-certificates/google-it-automation

## Exercise: 

 The "toc" dictionary represents the table of contents for a book. 1) Add an entry for Epilogue on page 39. 2) Change the page number for Chapter 3 to 24. 3) Display the new dictionary contents. 4) Display True if there is Chapter 5, False if there isn't.

```python
toc = {"Introduction":1, "Chapter 1":4, "Chapter 2":11, "Chapter 3":25, "Chapter 4":30}
toc["Epilogue"] = 39 # Epilogue starts on page 39
toc["Chapter 3"] = 24 # Chapter 3 now starts on page 24
print(toc) # What are the current contents of the dictionary?
print("Chapter 5" in toc) # Is there a Chapter 5?
```

Output:
```
{'Introduction': 1, 'Chapter 1': 4, 'Chapter 2': 11, 'Chapter 3': 24, 'Chapter 4': 30, 'Epilogue': 39}
False
```

## Iterating Over Dictionaries

You can iterate over dictionaries using a for loop, just like with strings, lists, and tuples. This will iterate over the sequence of keys in the dictionary. If you want to access the corresponding values associated with the keys, you could use the keys as indexes. Or you can use the **items** method on the dictionary, like **dictionary.items()**. This method returns a tuple for each element in the dictionary, where the first element in the tuple is the key and the second is the value.

If you only wanted to access the keys in a dictionary, you could use the **keys()** method on the dictionary: **dictionary.keys()**. If you only wanted the values, you could use the **values()** method: **dictionary.values()**.

## Oficial Python Documentation for Dictionaries
