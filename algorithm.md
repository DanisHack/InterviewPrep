4 Sum:
```javascript
function fourSum(nums, target) {
    const result = [];
    for (let i = 0; i < nums.length - 3; i++) {
        if (i !== 0 && nums[i] === nums[i - 1]) {
            continue;
        }
        for (let j = i + 1; j < nums.length - 2; j++) {
            if (j !== i + 1 && nums[j] === nums[j - 1]) {
                continue;
            }
            let k = j + 1, l = nums.length - 1;
            while (k < l) {
                const sum = nums[i] + nums[j] + nums[k] + nums[l];
                if (sum === target) {
                    result.push([nums[i], nums[j], nums[k], nums[l]]);
                    k++;
                    l--;
                    while (k < l && nums[k] === nums[k - 1]) {
                        k++;
                    }
                    while (k < l && nums[l] === nums[l + 1]) {
                        l--;
                    }
                } else if (sum < target) {
                    k++;
                } else {
                    l--;
                }
            }
        }
    }
    return result;
}

fourSum([-2, -2, -1, 0, 1, 2, 4], 0);
```
Convert Int to Roman Numeral:
```javascript
function convertToRoman(num) {
    const roman = {
        "M": 1000,
        "CM": 900,
        "D": 500,
        "CD": 400,
        "C": 100,
        "XC": 90,
        "L": 50,
        "XL": 40,
        "X": 10,
        "IX": 9,
        "V": 5,
        "IV": 4,
        "I": 1
    };
    let result = "";
    for (let key in roman) {
        const numberOf = Math.floor(num / roman[key]);
        num -= numberOf * roman[key];
        result += key.repeat(numberOf);
    }
    return result;
}

convertToRoman(435); // 'CDXXXV'
```
Convert Roman to Number:
```javascript
function convertToNumber(str) {
    const roman = {
        "M": 1000,
        "CM": 900,
        "D": 500,
        "CD": 400,
        "C": 100,
        "XC": 90,
        "L": 50,
        "XL": 40,
        "X": 10,
        "IX": 9,
        "V": 5,
        "IV": 4,
        "I": 1
    };
    let result = roman[str[0]];
    for (let i = 1; i < str.length; i++) {
        let num = roman[str[i]];
        const prev = roman[str[i - 1]];
        if (num > prev) {
            result += num - prev - prev;
        } else {
            result += num;
        }
    }
    return result;
}

convertToNumber('CDXXXV'); // 435
```
Phone number combination:
```javascript
function letterCombinations(digits) {
    const result = [];
    if (!digits) {
        return result;
    }
    const obj = {
        "1": ["1"],
        "0": ["0"],
        "2": ["a", "b", "c"],
        "3": ["d", "e", "f"],
        "4": ["g", "h", "i"],
        "5": ["j", "k", "l"],
        "6": ["m", "n", "o"],
        "7": ["p", "q", "r", "s"],
        "8": ["t", "u", "v"],
        "9": ["w", "x", "y", "z"]
    };
    (function recurse(str, index) {
        if (str.length === digits.length) {
            result.push(str);
            return;
        }
        for (let i = 0; i < obj[digits[index]].length; i++) {
            const current = obj[digits[index]][i];
            recurse(str + current, index + 1);
        }
    })("", 0);
    return result;
}

letterCombinations("234");
```
Island count, connected islands are count as one:
```javascript
const graph = [
 [1, 1, 0, 0, 1],
 [1, 1, 0, 0, 0],
 [0, 0, 0, 0, 0],
 [0, 1, 0, 1, 1]
]; // 4

function islandCount(graph) {
    const visited = {};
    let sum = 0;
    function isValid(row, col) {
        const key = `${row}${col}`;
        if (row >= graph.length || col >= graph[0].length || !graph[row][col] || visited[key]) {
            return false;
        }
        visited[key] = true;
        isValid(row, col + 1);
        isValid(row + 1, col + 1);
        isValid(row + 1, col);
        isValid(row + 1, col - 1);
        return true;
    }
    graph.forEach((e, row) => {
        e.forEach((ele, col) => {
            if (ele && !visited[`${row}${col}`] && isValid(row, col)) {
                sum++;
            }    
        });
    });
    return sum;
}

islandCount(graph);
```
Check if a number is prime: (for reference http://www.javascripter.net/faq/numberisprime.htm)
```javascript
function leastFactor(n){
    if (isNaN(n) || !isFinite(n)) return NaN;  
    if (n === 0 || n === 1) return n;  
    if (n%2==0) return 2;  
    if (n%3==0) return 3;  
    if (n%5==0) return 5;  
    var m = Math.sqrt(n);
    for (var i = 7; i <= m; i += 30) {
        if (n%i==0)      return i;
        if (n%(i+4)==0)  return i+4;
        if (n%(i+6)==0)  return i+6;
        if (n%(i+10)==0) return i+10;
        if (n%(i+12)==0) return i+12;
        if (n%(i+16)==0) return i+16;
        if (n%(i+22)==0) return i+22;
        if (n%(i+24)==0) return i+24;
    }
    return n;
}

function isPrime(n) {
    if (isNaN(n) || !isFinite(n) || n%1 || n<2) return false;
    if (n === leastFactor(n)) return true;
    return false;
}
```
Next permutation of a number:
```javascript
function reverse(nums, p, q) {
    while (p < q) {
        const temp = nums[p];
        nums[p] = nums[q];
        nums[q] = temp;
        p++;
        q--;
    }
}

function nextPermutation(nums) {
    let p = 0, q = 0;
    for (let i = nums.length - 2; i >= 0; i--) {
        if (nums[i] < nums[i + 1]) {
            p = i;
            break;
        }
    }
    for (let i = nums.length - 1; i > p; i--) {
        if (nums[i] > nums[p]) {
            q = i;
            break;
        }
    }
    if (p === 0 && q === 0) {
        return nums.reverse();
    }
    const temp = nums[p];
    nums[p] = nums[q];
    nums[q] = temp;
    if (p < nums.length - 1) {
        reverse(nums, p + 1, nums.length - 1);
    }
    return nums;
}

nextPermutation([1, 3, 2]); // [2, 1, 3]
```
