![alt text](../images/isScramble.png)
```javascript
function isScramble(s1, s2) {
    if (s1.length !== s2.length) {
        return false;
    }
    if (s1.length === 0 || s1 === s2) {
        return true;
    }
    const arr1 = s1.split("").sort().join("");
    const arr2 = s2.split("").sort().join("");
    if (arr1 !== arr2) {
        return false;
    }
    for (let i = 1; i < s1.length; i++) {
        const s11 = s1.slice(0, i);
        const s12 = s1.slice(i, s1.length);
        const s21 = s2.slice(0, i);
        const s22 = s2.slice(i, s2.length);
        const s23 = s2.slice(0, s2.length - i);
        const s24 = s2.slice(s2.length - i, s2.length);
        if (isScramble(s11, s21) && isScramble(s12, s22)) {
            return true;
        }
        if (isScramble(s11, s24) && isScramble(s12, s23)) {
            return true;
        }
    }
    return false;
}

isScramble("abcde", "caebd");
```
