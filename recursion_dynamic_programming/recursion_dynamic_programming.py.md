Ways to put 8 queens on a 8x8 board:
```python
import math

def isValid(combo, row1, col1):
    for row2 in range(row1):
        col2 = combo[row2]
        if col1 == col2:
            return False
        colDistance = math.fabs(col1 - col2)
        rowDistance = row1 - row2
        if colDistance == rowDistance:
            return False
    return True

def placeQueens():
    result = []
    combo = [None] * 8
    def recurse(row):
        if row == 8:
            result.append(combo[:])
            return
        for col in range(8):
            if isValid(combo, row, col):
                combo[row] = col
                recurse(row + 1)
    recurse(0)
    return result

print(placeQueens())
```
