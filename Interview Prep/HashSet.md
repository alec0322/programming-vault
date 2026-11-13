A HashSet, or a #set in Python, is a collection of **unique** items stored in a single variable. The key distinction between an #array and a set is that a set's items are unordered and unchangeable.

```python
# Example usage
fruits = {"apple", "banana", "cherry"}
```

At first glance, a set may seem as a downgrade of an array. Why would you want unordered and unchangeable items stored together? The answer is simple, **direct search of items in O(1)**
	Sets utilize hashing techniques to enable **linear searches** in a collection of items.

Let's say we wanted to keep track of items in our pantry within an array:

```python
def isItemInPantry(pantry: List[str], item: str) -> bool:
	for i in pantry:
		if i == item:
			return True
	return False

# Let's assume we want to know if sugar is in our pantry
pantry = ["oats", "salt", "sugar"]
print(isItemInPantry(pantry, "sugar"))
```

The algorithm above will have a #TimeComplexity of O(N), where N is the size of the array. If we place 1,000,000 items before `sugar`, it will take 1,000,001 iterations to find it in the pantry.

Sets resolve this problem:

```python
def isItemInPantry(pantry: set[str], item: str) -> bool:
	return item in pantry

pantry = {"oats", "salt", "sugar"}
print(isItemInPantry(pantry, "sugar"))
```

This algorithm will run in O(1), no matter the size of the array.