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
Generate all subsets of size K:
```javascript
function generateSubset(k, n) {
    const result = [];
    (function recurse(i, combo = []) {
        if (combo.length === k) {
            return result.push([...combo]);
        }
        for (let j = i; j <= n; j++) {
            combo.push(j);
            recurse(j + 1, combo);
            combo.pop();
        }
    })(1);
    return result;
}

generateSubset(3, 5);
```
Generate Palindromic Decompositions:
```javascript
function allPalindrome(str) {
    const result = [];
    (function helper(index, current) {
        if (index === str.length) {
            return result.push(current.slice(1));
        }
        for (let i = index + 1; i < str.length + 1; i++) {
            const word = str.slice(index, i);
            if (word === word.split("").reverse().join("")) {
                helper(i, `${current},${word}`);
            }
        }
    })(0, "");
    return result;
}

allPalindrome("0204451881");
```
