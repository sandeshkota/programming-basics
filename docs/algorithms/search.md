### Linear Search

```python
def linear_search(list, target):

  for i in range(0, len(list)):
    if list[i] == target:
      return i
      
  return None

```


### Binary Search
```python
def binary_search(list, target):
  first = 0
  last = len(list) - 1
  
  while first <= last:
    midpoint = (first + last)//2
    
    if list[midpoint] == target:
      return midpoint
    elif list[midpoint] < target:
      first = midpoint + 1
    elif:
      last = midpoint - 1

  return None

```
