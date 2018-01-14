Convert Col column to Integer where "A" starts at 1:
```javascript
function decodeStrCol(col) {
    return col.split("").reduce((result, c) => result * 26 + c.charCodeAt() - 64, 0)
}

decodeStrCol("ZZ"); // 702
```
Test palindrome of a sentence:
```javascript
// javascript version
function testPalindrome(str) {
    const arr = str.match(/[a-zA-Z]/gi);
    for (let i = 0; i < Math.floor(arr.length / 2); i++) {
        if (arr[i].toLowerCase() !== arr[arr.length - 1 - i].toLowerCase()) {
            return false;
        }
    }
    return true;
}

testPalindrome("Able was I, ere I saw Elba"); // true
```
Reverse a sentence:
```javascript
function reverseSentence(str) {
    return str.split(" ").reverse().join(" ");
}

reverseSentence("ram is costly");
```
Generate Look and Say sequence:
```javascript
// javascript version
function generateSequence(str) {
    let res = "", current = str[0], count = 1;
    for (let i = 1; i < str.length; i++) {
        if (str[i] === current) {
            count++;
        } else {
            res += `${count}${current}`;
            current = str[i];
            count = 1;
        }
    }
    res += `${count}${current}`;
    return res;
}

function lookAndSay(n) {
    let result = ["1"];
    if (n <= 1) {
        return result;
    }
    for (let i = 0; i < n - 1; i++) {
        result = [...result, generateSequence(result[i])];
    }
    return result;
}
lookAndSay(8);
```
First Occurence of a substring even if it is anagram:
```javascript
function isAnagram(w1, w2) {
    if (w1.length !== w2.length) {
        return false;
    }
    const obj1 = {}, obj2 = {};
    for (let i = 0; i < w1.length; i++) {
        if (obj1[w1[i]]) {
            obj1[w1[i]]++;
        } else {
            obj1[w1[i]] = 1;
        }
        if (obj2[w2[i]]) {
            obj2[w2[i]]++;
        } else {
            obj2[w2[i]] = 1;
        }
    }
    for (let key in obj1) {
        if (obj1[key] !== obj2[key]) {
            return false;
        }
    }
    return true;
}

function firstOccurence(s, t) {
    const len = t.length;
    for (let i = 0; i < s.length; i++) {
        const word = s.slice(i, i + len);
        if (isAnagram(word, t)) {
            return i;
        }
    }
    return -1;
}

firstOccurence("GACCCGA", "CGC"); // true
```
