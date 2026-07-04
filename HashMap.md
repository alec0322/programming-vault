A HashMap or a #dict in Python is a data structure that stores items in key/value pairs. Almost like the older brother of a [[HashSet]], a hashmap is essentially a hashset with an extra value attached to every key.

While hashsets answer the question "Does this item exist in this collection?", hashmaps go one step further: "If this item were to exist in this collection, what assigned value(s) does it have?"

Let's say that you wanted to keep track of items within an e-commerce site.

```python
items = ["Keyboard", "Monitor", "Chair"]
price = [29.99, 199.99, 99.99]
```

Let's assume that you had 2 separate arrays for `itms` and `price`, where `price[i]` represents how much `items[i]` sells for. From a programmatic standpoint, it's difficult for the computer to process these relationships - We would have to iterate over both arrays `n` times to figure out how much we can sell an item for.

We can instead use a #dict.

```python
inventory = {}

for i, item in enumerate(items):
	inventory[item] = price[i]
```

The resulting `inventory` would tell us how much an item in inventory goes for in `O(1)`

```python
print(inventory["Keyboard"]) # Prints 29.99
```