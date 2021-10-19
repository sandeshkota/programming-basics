# Search Algorithm

## Unsorted List

### Linear Search

```python
def linear_search(list, target):

  for i in range(0, len(list)):
    if list[i] == target:
      return i
      
  return None

```

## Sorted List

### Binary Search
- iterative way
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
- recursive way
```python
def recursive_binary_search(list, target):
  if len(list) == 0:
    return None
  else:
    midpoint = len(list)//2
    
    if list[midpoint] == target:
      return True
    else list[midpoint] < target:
      return recursive_binary_search(list[midpoint+1:], target)
    else:
    return recursive_binary_search(list[:midpoint], target)

```

### Interpolation Search


### Ternary Search





















