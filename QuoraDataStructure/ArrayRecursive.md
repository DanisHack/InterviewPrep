Combinations of words formed by replacing given numbers with corresponding alphabets
```javascript
function digitsWord(digits) {
    const res = [];
    (function recurse(index, str = "") {
        if (index === digits.length) {
            return res.push(str);
        }
        let sum = 0;
        for (let j = index; j <= Math.min(index + 1, digits.length - 1); j++) {
            sum = sum * 10 + digits[j];
            if (sum <= 26) {
                recurse(j + 1, str + String.fromCharCode(sum + 64));
            }
        }
    })(0);
    return res;
}

digitsWord([1, 2, 2, 1]);
```
