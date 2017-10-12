Convert Col column to Integer where is "A" starts at 1:
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
    const arr = str.match(/[a-zA-Z]/ig);
    for (let i = 0; i < Math.floor((arr.length + 1) / 2); i++) {
        if (arr[i].toLowerCase() !== arr[arr.length - i - 1].toLowerCase()) {
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
    let track = 1;
    let current = str[0];
    let result = "";
    for (let i = 1; i < str.length; i++) {
        if (str[i] !== current) {
            result += `${track}${current}`
            current = str[i];
            track = 1;
        } else {
            track++;
        }
    }
    result += `${track}${current}`;
    return result;
}

function lookAndSay(n) {
    const result = ["1"];
    if (n <= 1) {
        return result;
    }
    for (let i = 0; i < n - 1; i++) {
        const nextOne = generateSequence(result[i]);
        result.push(nextOne);
    }
    return result;
}
lookAndSay(8);
```
First Occurence of a substring:
```javascript
function firstOccurence(s, t) {
    const len = t.length;
    for (let i = 0; i < s.length; i++) {
        const word = s.slice(i, i + len);
        if (word === t) {
            return i;
        }
    }
    return -1;
}

firstOccurence("GACGCCA", "CGC");
```
