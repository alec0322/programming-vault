Quoted from geeksforgeeks:

> [!NOTE] Introduction to Hashing
> **Hashing** refers to the process of generating a small sized output (that can be used as index in a table) from an input of typically large and variable size

Put simply, it is the way in which computers convert something big (like a string or an array) into a small number so that it can store or find it quickly.

Imagine you had a an array containing all of your credit card transactions:

```python
transactions = [1.99, 14.99, 99.99, 4.99, ...]
```

A computer would have a hard time comparing this entire array every time it wanted to check if it had seen these exact transactions before. (We would have to iterate over all elements - `O(N)`)

Instead, it could **hash** the array into a small number:

```python
hash(transactions) = 49281
```

Now, rather than remembering or comparing the entire array first, it can use `49281` as a quick way to determine where to store or look up those transactions. Both [[HashMap]]'s and [[HashSet]]'s build on this idea.