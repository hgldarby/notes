# Shallow vs Deep Copying

- Compound objects like lists, dicts, and sets have an important difference between shallow and deep copying.
- **Shallow copying** - means constructing a new collection object and populating it with references to the child objects found in the original. It won't create copies of the child objects themselves and is only one level deep.
- **Deep Copying** - means constructing a new collection object and recursively populating it with copies of the child objects found in the original. Walks the whole object tree to create a fully independent clone to the original object and all of its children.

### Shallow Copy

- Example:

  ```python
  >>> xs = [[1,2,3], [4,5,6], [7,8,9]]
  >>> ys = list(xs)  # make a shallow copy
  ```

- ys is a new and independent object with same contents as xs

- adding to xs will not affect ys

- Changing an object that in xs that we know is in ys also changes that in ys:

  ```python
  >>> xs[1][0] = 'X'
  >>> xs
  [[1, 2, 3], ['X', 5, 6], [7, 8, 9], ['new sublist']]
  >>> ys
  [[1, 2, 3], ['X', 5, 6], [7, 8, 9]]
  ```

- If ys was a deep copy of xs, they would be fully independent

### Deep Copy

- Example:

  ```python
  >>> import copy
  >>> xs = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
  >>> zs = copy.deepcopy(xs)
  ```

- xs and zs are fully independent of each other so changing an object in xs that we know is in zs will not change zs:

  ```python
  >>> xs[1][0] = 'X'
  >>> xs
  [[1, 2, 3], ['X', 5, 6], [7, 8, 9]]
  >>> zs
  [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
  ```



