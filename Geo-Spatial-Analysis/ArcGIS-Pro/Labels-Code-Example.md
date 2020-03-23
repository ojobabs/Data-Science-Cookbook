


> Written with [StackEdit](https://stackedit.io/).

# Labels Code Example

To show labels for office locations:

```python
def FindLabel ([USER_GO_CD_1], [USER_go_ou_nm]):
    if [USER_GO_CD_1] == "V65":
        return [USER_go_ou_nm]
```
or 

```python
def FindLabel ([USER_GO_CD_1], [USER_go_ou_nm]):
    if [USER_GO_CD_1] == "D54":
        return [USER_go_ou_nm]
    elif [USER_GO_CD_1] == "D56":
        return [USER_go_ou_nm]
    elif [USER_GO_CD_1] == "D57":
        return [USER_go_ou_nm]
```

Tho show labels for hexagon counts:

```python

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1MDU1NTk4NV19
-->