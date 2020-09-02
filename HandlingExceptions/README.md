# Handling Exceptions

> Resource: Gift, Noah. Python for DevOps (p. 10). O'Reilly Media. Kindle Edition. 

```python
thinkers = ['Plato', 'PlayDo', 'Gumby']
while True:
  try:
    thinker = thinkers.pop()
    print(thinker)
  except IndexError as e:
    print("We tried to pop too many thinkers")
    print(e)
    break
```

Output:
```
Gumby
PlayDo
Plato
We tried to pop too many thinkers
pop from empty list
```
