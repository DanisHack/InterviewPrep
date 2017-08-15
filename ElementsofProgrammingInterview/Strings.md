Convert Col column to Integer where is "A" starts at 1:
```javascript
function decodeStrCol(col) {
    return col.split("").reduce((result, c) => result * 26 + c.charCodeAt() - 64, 0)
}

decodeStrCol("ZZ"); // 702
```
```python
from functools import reduce

def decodeStrCol(col):
    return reduce(lambda result, c: result * 26 + ord(c) - 64, list(col), 0)

decodeStrCol("BB")
```
