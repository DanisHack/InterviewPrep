1.1 Is Unique
```javascript
function isUnique(str) {
    for (let i = 0; i < str.length; i++) {
        for (let j = i + 1; j < str.length; j++) {
            if (str[i] === str[j]) {
                return false;
            }
        }
    }
    return true;
}

isUnique("Helo");
```
1.2 Check Permutation
```javascript
function checkPermutation(str1, str2) {
    const obj1 = {};
    const obj2 = {};
    str1.split("").forEach(e => {
        if (obj1[e]) {
            obj1[e]++;
        } else {
            obj1[e] = 1;
        }
    });
    str2.split("").forEach(e => {
        if (obj2[e]) {
            obj2[e]++;
        } else {
            obj2[e] = 1;
        }
    });
    for (const key in obj1) {
        if (obj1[key] !== obj2[key]) {
            return false;
        }
    }
    return true;
}

checkPermutation("aba", "aab");
```
1.3 URLify
```javascript
function URLify(str, n) {
    const inp = str.trim("");
    return inp.replace(/ /gi, "%20");
}

URLify("Mr John Smith   ", 13);
```
1.4 Palindrome Permutation
```javascript
function palinPerm(str) {
    const chars = {};
    let currChar = '';
    let track = 0;
    str.split("").forEach(e => {
        if (e !== " ") {
            currChar = e.toLowerCase();
            if (chars[currChar]) {
                chars[currChar]++;
            } else {
                chars[currChar] = 1;
            }
        }
    });
    for (const key in chars) {
        if (chars[key] % 2 !== 0) {
            track++;
        }
        if (track === 2) {
            return false;
        }
    }
    return true;
}

palinPerm('Tact coa');
```
1.5 One Away
```javascript
function oneAway(s1, s2) {
    const length = Math.abs(s1.length - s2.length);
    if (length > 1) {
        return false;
    }
    if (s1.length === s2.length) {
        let count = 0;
        for (let i = 0; i < s1.length; i++) {
            if (s1[i] !== s2[i]) {
                count++;
            }
        }
        return count <= 1;
    }
    const obj1 = {};
    const obj2 = {};
    let count = 1;
    s1.split("").forEach(e => {
        if (obj1[e]) {
            obj1[e]++;
        } else {
            obj1[e] = 1;
        }
    });
    s2.split("").forEach(e => {
        if (obj2[e]) {
            obj2[e]++;
        } else {
            obj2[e] = 1;
        }
    });
    const copyObj1 = s1.length > s2.length ? obj2 : obj1;
    const copyObj2 = copyObj1 === obj1 ? obj2 : obj1;
    for (const key in copyObj1) {
        if (copyObj1[key] !== copyObj2[key]) {
            return false;
        }
    }
    return true;
}

oneAway("pale", "bake");
```
1.6 String Compression
```javascript
function strCompress(str) {
    let current = str[0];
    let count = 1;
    let res = "";
    for (let i = 1; i < str.length; i++) {
        if (str[i] === current) {
            count++;
        } else {
            res += `${current}${count}`;
            count = 1;
            current = str[i];
        }
    }
    res += `${current}${count}`;
    return res;
}

strCompress("aabcccccaaa");
```
1.7 Rotate Matrix
```javascript
const arr = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
];

function rotateMatrix(arr) {
    const res = [];
    for (let i = 0; i < arr.length; i++) {
        for (let j = arr.length - 1; j >= 0; j--) {
            if (res[i]) {
                res[i].push(arr[j][i]);
            } else {
                res[i] = [arr[j][i]];
            }
        }
    }
    return res;
}

rotateMatrix(arr);
```
1.8 Zero Matrix
```javascript
const testMatrix = [
    [1, 1, 1, 1],
    [1, 1, 1, 1],
    [1, 0, 1, 1],
    [1, 1, 1, 1],
    [1, 1, 1, 1],
    [1, 1, 1, 1]
];

function zeroMatrix(arr) {
    let row = 0;
    let col = 0;
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr[i].length; j++) {
            if (arr[i][j] === 0) {
                row = i;
                col = j;
                break;
            }
        }
    }
    arr.forEach((e, i) => {
        arr[i][col] = 0;
    });
    arr[row].forEach((e, j) => {
        arr[row][j] = 0;
    });
    return arr;
}

zeroMatrix(testMatrix);
```
1.9 String Rotation
```javascript
function stringRotation(s1, s2) {
    if (s1.length !== s2.length) {
        return false;
    }
    return (s2 + s2).includes(s1);
}

stringRotation("waterbottle", "erbottlewat");
```
