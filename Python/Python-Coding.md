


> Written with [StackEdit](https://stackedit.io/).

#### [Remove multiple items from a Python list in just one statement](https://stackoverflow.com/questions/36268749/remove-multiple-items-from-a-python-list-in-just-one-statement)

The following is useful when you are working with columns names in Pandas. For example, with the following code we can get a list with all column names from a dataframe:
```python
vars = [var for var in criteria.columns]
vars
```
Output:
```
['marketer_id',
 'target1Rolling',
 'target1Eoy']
```

In Python, create a new object is often better than modify an existing one:

```python
item_list = ['item', 5, 'foo', 3.14, True]
item_list = [e for e in item_list if e not in ('item', 5)]
```

Which is equivalent to:

```python
item_list = ['item', 5, 'foo', 3.14, True]
new_list = []
for e in item_list:
    if e not in ('item', 5):
        new_list.append(e)
item_list = new_list
```
In case of a big list of filtered out values (here,  `('item', 5)`  is a small set of element), use a  `set`  can lead to performance improvement, as the  `in`  operation is in O(1) :

```python
item_list = [e for e in item_list if e not in {'item', 5}]
```

Note that, as explained in comments and suggested  [here](https://gist.github.com/Aluriak/01c3d100cb44ef048c00854c6f439642), the following could save even more time, avoiding the set to be built at each loop:

```python
unwanted = {'item', 5}
item_list = [e for e in item_list if e not in unwanted]
```


####  [How to append multiple values to a list in Python](https://stackoverflow.com/questions/20196159/how-to-append-multiple-values-to-a-list-in-python)

You can use the  [sequence method  `list.extend`](https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types)  to extend the list by multiple values from any kind of iterable, being it another list or any other thing that provides a sequence of values.

```python
>>> lst = [1, 2]
>>> lst.append(3)
>>> lst.append(4)
>>> lst
[1, 2, 3, 4]

>>> lst.extend([5, 6, 7])
>>> lst.extend((8, 9, 10))
>>> lst
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

>>> lst.extend(range(11, 14))
>>> lst
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
```
So you can use  `list.append()`  to append  _a single_  value, and  `list.extend()`  to append  _multiple_  values.

### [Writing a list to a file with Python](https://stackoverflow.com/questions/899103/writing-a-list-to-a-file-with-python)
```python
# Create a list with all column names
colsAll = [var for var in allAgents.columns]

# send the colsAll list to a txt file
with open('master_train_test/columns.txt', 'w') as f:
    for item in colsAll:
        f.write("%s\n" % item)
```

### [Python-3-quick-tip-the-easy-way-to-deal-with-file-paths-on-windows-mac-and-linux](https://medium.com/@ageitgey/python-3-quick-tip-the-easy-way-to-deal-with-file-paths-on-windows-mac-and-linux-11a072b58d5f)

from pathlib import Path

# Load the datasets
```python
data_folder = Path("/nyl/data/tenants/insurance/cdsa/Agency/Agent_Analytics/NYU_Capstone/")

file_to_open = data_folder / "contracts_with_attr.csv"

cont = pd.read_csv(file_to_open)
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjc3Nzk3MSwtMTgyMTI0NjAwMCw4OT
c2MDcwOTIsNjYwMDU5MzE3XX0=
-->