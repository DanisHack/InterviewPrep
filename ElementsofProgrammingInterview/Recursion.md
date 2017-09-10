Permutation of an Array:
```javascript
function permutation(arr) {
    const result = [];
    (function recurse(i) {
        if (i === arr.length - 1) {
            result.push([...arr]);
            return;
        }
        for (let j = i; j < arr.length; j++) {
            let temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            recurse(i + 1);
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    })(0);
    return result;
}

permutation([2, 3, 5, 7]);
```
