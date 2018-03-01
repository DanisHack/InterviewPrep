bottom-up fibb:
```javascript
function fibb(x) {
    const arr = [0, 1];
    for (let i = 2; i < x + 1; i++) {
        arr[i] = arr[i - 1] + arr[i - 2];
    }
    return arr[x];
}

fibb(8);
```
3 sum:
```javascript
function sum3(arr) {
    const result = [];
    if (arr.length < 3) {
        return result;
    }
    for (let i = 0; i < arr.length - 2; i++) {
        let j = i + 1, k = arr.length - 1;
        while (j < k) {
            const sum = arr[i] + arr[j] + arr[k];
            if (sum === 0) {
                result.push(`${arr[i]},${arr[j]},${arr[k]}`);
                j++;
                k--;
                while (j < k && arr[j] === arr[j - 1]) {
                    j++;
                }
                while (j < k && arr[k] === arr[k + 1]) {
                    k--;
                }
            } else if (sum < 0) {
                j++;
            } else {
                k--;
            }
        }
    }
    return result;
}

sum3([-4, -2, 0, 0, 2, 2, 4]);
```
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
    const res = [];
    if (!digits) {
        return res;
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
            res.push(str);
            return;
        }
        obj[digits[index]].forEach(e => {
            recurse(str + e, index + 1);
        });
    })("", 0);
    return res;
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
        if (row >= graph.length || col >= graph[row].length || !graph[row][col] || visited[key]) {
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
Insert new Interval:
```javascript
const arr1 = [[1,2], [3,5], [6,7], [8,10], [12,16]];
const arr2 = [4,9];

function insertInterval(intervals, newInterval) {
    const result = [];
    intervals.forEach(e => {
        if (newInterval[0] > e[1]) {
           result.push(e);
        } else if (newInterval[1] < e[0]) {
            result.push(newInterval);
            newInterval = e;
        } else if (newInterval[1] >= e[0] || newInterval[0] <= e[1]) {
            newInterval = [Math.min(newInterval[0], e[0]), Math.max(newInterval[1], e[1])];
        }
    });
    result.push(newInterval);
    return result;
}

insertInterval(arr1, arr2); // [ [ 1, 2 ], [ 3, 10 ], [ 12, 16 ] ]
```
Find the Intersection of Two Arrays:
```javascript
function intersect(a, b) {
    let aIndex = 0, bIndex = 0;
    const result = [];
    while (aIndex < a.length && bIndex < b.length) {
        if (a[aIndex] < b[bIndex]) {
            aIndex++;
        } else if (a[aIndex] > b[bIndex]) {
            bIndex++;
        } else {
            result.push(a[aIndex]);
            aIndex++;
            bIndex++;
        }
    }
    return result;
}

intersect([1, 2, 3, 4], [2, 3, 4]);
```
Get all orders of letters of words:
```javascript
function get(s) {
	let result = [];
	function recurse(current, remain) {
		remain.split("").forEach((e, i) => {
			let tail = remain.slice(0, i) + remain.slice(i + 1);
			let word = current + e + tail;

			if(result.indexOf(word) < 0) {
				result.push(word);
			}

			if(remain.length > 1) {
				recurse(current + e, tail);
			}
		});
	}
	recurse("", s);
	return result;
}

get("dog");
```
Longest Substring Without Repeating Characters:
```javascript
function longest(str) {
    let result = 0, lastRepeat = -1, s = "";
    const visited = {};
    str.split("").forEach((e, i) => {
        if (visited.hasOwnProperty(e)) {
           lastRepeat = Math.max(lastRepeat, visited[e]);
        }
        if (i - lastRepeat > res) {
            s = str.slice(lastRepeat + 1, i + 1);
        }
        result = Math.max(result, i - lastRepeat);
        visited[e] = i;
    });
    return result;
}

longest("ewrvewvwsfa"); // 5
```
Median of two sorted array:
```javascript
function merge(a, b) {
    let aLength = a.length - 1;
    let bLength = b.length - 1;
    let mergeLength = a.length + b.length - 1;
    while (aLength >= 0 && bLength >= 0) {
        if (a[aLength] > b[bLength]) {
            a[mergeLength] = a[aLength];
            aLength--;
            mergeLength--;
        } else {
            a[mergeLength] = b[bLength];
            bLength--;
            mergeLength--;
        }
    }
    while (bLength >= 0) {
        a[mergeLength] = b[bLength];
        mergeLength--;
        bLength--;
    }
    return a;
}

function findMedian(a, b) {
    const arr = merge(a, b);
    const middle = Math.floor((arr.length - 1) / 2);
    if (arr.length % 2 !== 0) {
        return arr[middle];
    }
    return (arr[middle] + arr[middle + 1]) / 2;
}

findMedian([1, 1, 2, 3, 4], [5, 6, 7, 7]);
```
Find the longest palindrome:
```javascript
function expand(str, i, j) {
    while (i >= 0 && j < str.length && str[i] === str[j]) {
        i--;
        j++;
    }
    return j - i - 1;
}

function longestPalindrome(str) {
    let start = 0, end = 0;
    str.split("").forEach((e, i) => {
       const len1 = expand(str, i, i);
       const len2 = expand(str, i, i + 1);
       const len = Math.max(len1, len2);
       if (len > end - start) {
           start = i - (len - 1) / 2;
           end = (i + len / 2) + 1;
       }
    });
    return str.slice(Math.ceil(start), end);
}

longestPalindrome("bbcccbb");
```
Regular Expression Matching:
```javascript
function isMatch(s, p) {
    if (!p) {
        return !s;
    }
    if (p.length === 1 || p[1] !== "*") {
        if (!s || (p[0] !== "." && s[0] !== p[0])) {
            return false;
        }
        return isMatch(s.slice(1), p.slice(1));
    } else {
        let i = -1;
        while (i < s.length && (i < 0 || p[0] === "." || p[0] === s[i])) {
            if (isMatch(s.slice(i + 1), p.slice(2))) {
                return true;
            }
            i++;
        }
        return false;
    }
}
isMatch("aab", "c*a*b"); // true
isMatch("aab", "a*"); // true
```
Wildcard Matching:
```javascript
function isMatch(s, p) {
    let i = 0, j = 0, jIndex = -1, iIndex = -1;
    while (i < s.length) {
        if (j < p.length && (p[j] === "?" || p[j] === s[i])) {
            j++;
            i++;
        } else if (j < p.length && p[j] === "*") {
            jIndex = j;
            iIndex = i;
            j++;
        } else if (jIndex !== -1) {
            i = iIndex + 1;
            j = jIndex + 1;
            iIndex++;
        } else {
            return false;
        }
    }
    while (j < p.length && p[j] === "*") {
        j++;
    }
    return j === p.length;
}

isMatch("abefcdgiescdfimde", "ab*cd?i*de");
```
Longest Common Prefix:
```javascript
function longestCommonPrefix(arr) {
    if (!arr.length) {
        return "";
    }
    const firstWord = arr[0];
    for (let i = 0; i < firstWord.length; i++) {
        const currentLetter = firstWord[i];
        for (let j = 0; j < arr.length; j++) {
            if (i === arr[j].length || arr[j][i] !== currentLetter) {
                return firstWord.slice(0, i);
            }
        }
    }
    return firstWord;
}

longestCommonPrefix(["leets", "leetcode", "leet", "leeds"]); // lee
```
Check if parentheses are valid:
```javascript
function validParen(str) {
    const parentheses = { "(": 1, ")": 2 };
    const arr = [];
    let valid = 0;
    str.split("").forEach(e => {
        const current = parentheses[e];
        if (current % 2) {
            valid++;
            arr.push(e);
        } else {
            valid--;
            arr.pop();
        }
    });
    return arr.length === 0 && valid === 0;
}

validParen(")()()(");
```
Word Break:
```javascript
function wordBreak(s, dict) {
    const arr = [true].concat(Array(s.length).fill(false));
    for (let i = 0; i < s.length; i++) {
        if (arr[i]) {
            for (let j = i + 1; j <= s.length; j++) {
                const word = s.slice(i, j);
                if (dict.includes(word)) {
                    arr[j] = true;
                }
            }
        }
    }
    return arr[s.length];
}

wordBreak("leetcode", ["leet", "code"]); // Return true because "leetcode" can be segmented as "leet code".
```
Word Break II:
```javascript
function dfs(arr, result, str, index) {
    if (index === 0) {
        return result.push(str.trim());
    }
    for (let i = 0; i < arr[index].length; i++) {
        const word = arr[index][i];
        dfs(arr, result, `${word} ${str}`, index - word.length);
    }
}

function wordBreak(s, dict) {
    const arr = Array(s.length + 1).fill(null).map(() => []);
    for (let i = 0; i < s.length; i++) {
        for (let j = i + 1; j <= s.length; j++) {
            const word = s.slice(i, j);
            if (dict.includes(word)) {
                arr[j].push(word);
            }
        }
    }
    const result = [];
    dfs(arr, result, "", s.length);
    return result;
}

wordBreak("catsanddog", ["cat", "cats", "and", "sand", "dog"]); // ["cats and dog", "cat sand dog"]
```
Substring with Concatenation of All Words:
```javascript
function findSubstring(s, words) {
    const len = words.join("").length;
    const res = [];
    for (let i = 0; i <= s.length - len; i++) {
        const curr = s.slice(i, i + len);
        let count = 0;
        for (let j = 0; j < words.length; j++) {
            if (curr.includes(words[j])) {
                count++;
            }
        }
        if (count === words.length) {
            res.push(i);
        }
    }
    return res;
}

findSubstring("barfoofoobarthefoobarman", ["bar", "foo", "the"]);
```
Search for a Range:
```javascript
function searchRange(nums, target) {
    let start = 0;
    let end = nums.length - 1;
    const result = [];
    while (start <= end) {
        const middle = Math.floor((start + end) / 2);
        if (nums[middle] === target) {
            let temp = middle, temp1 = middle;
            while (temp > 0 && nums[temp] === nums[temp - 1]) {
                temp--;
            }
            while (temp1 < nums.length - 1 && nums[temp1] === nums[temp1 + 1]) {
                temp1++;
            }
            return [temp, temp1];
        } else if (nums[middle] < target) {
            start = middle + 1;
        } else {
            end = middle - 1;
        }
    }
    return [-1, -1];
};

searchRange([5, 7, 7, 8, 8, 10], 8); // [3, 4]
```
Longest Valid Parentheses:
```javascript
function longestValidParentheses(s) {
    let result = 0;
    const stack = [];
    s.split("").forEach((current, i) => {
        if (current === "(") {
            stack.push([i, 0]);
        } else {
            if (!stack.length || stack[stack.length - 1][1] === 1) {
                stack.push([i, 1]);
            } else {
                stack.pop();
                let currentLen = 0;
                if (!stack.length) {
                    currentLen = i + 1;
                } else {
                    currentLen = i - stack[stack.length - 1][0];
                }
                result = Math.max(result, currentLen);
            }
        }
    });
    return result;
}

longestValidParentheses(")()())");
```
Search in Rotated Sorted Array:
```javascript
function search(nums, target) {
    if (!nums.length) {
        return -1;
    }
    let start = 0, end = nums.length - 1;
    while (start <= end) {
        const middle = Math.floor((start + end) / 2);
        if (nums[middle] === target) {
            return middle;
        }

        if (nums[start] <= nums[middle]) { // left side is sorted
            if (nums[start] <= target && target < nums[middle]) {
                end = middle - 1;
            } else {
                start = middle + 1;
            }
        } else { // right side is sorted
            if (nums[middle] < target && target <= nums[end]) {
                start = middle + 1;
            } else {
                end = middle - 1;
            }
        }
    }
    return -1;
};

search([4, 5, 6, 7, 1, 2, 3], 5); // 1
```
Given an unsorted integer array, find the first missing positive integer:
```javascript
function firstMissingPositive(nums) {
    for (let i = 0; i < nums.length; i++) {
        while (nums[i] > 0 && nums[i] < nums.length && nums[i] !== nums[nums[i] - 1]) {
            const temp = nums[i];
            nums[i] = nums[temp - 1];
            nums[temp - 1] = temp;
        }
    }
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== i + 1) {
            return i + 1;
        }
    }
    return nums.length + 1;
}

firstMissingPositive([2, 6, 4, 1, 5]); // 3
```
Given n and k, return the kth permutation sequence:
```javascript
function getPermutation(n, k) {
    k--;
    const arr = [];
    let mod = 1, result = "";
    for (let i = 1; i <= n; i++) {
        arr.push(i);
        mod *= i;
    }
    for (let i = 0; i < n; i++) {
        mod /= n - i;
        const current = Math.floor(k / mod);
        k %= mod;
        result += arr[current];
        arr.splice(current, 1);
    }
    return result;
}

getPermutation(9, 2);
```
