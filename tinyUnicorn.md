TinyURL is a URL shortening service where you enter a URL such as https://leetcode.com/problems/design-tinyurl and it returns a short URL such as http://tinyurl.com/4e9iAk.
```javascript
const library = (() => {
    const obj = {};
    return {
        store(key, val) {
            obj[key] = val;
        },
        retrieve(key) {
            return obj[key];
        }
    };
})();

function encode(s) {
    const alphabet = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
    let res = "";
    for (let i = 0; i < 6; i++) {
        res += alphabet[Math.floor(Math.random() * alphabet.length)];
    }
    library.store(res, s);
    return `http://tinyurl.com/${res}`;
}

function decode(s) {
    const key = s.slice(s.lastIndexOf("/") + 1);
    return library.retrieve(key);
}

decode(encode("https://leetcode.com/problems/design-tinyurl"));
```
Check if parentheses are valid:
```javascript
function validParen(s) {
    const obj = { "(": 1, ")": 2, "{": 3, "}": 4, "[": 5, "]": 6 };
    const res = [];
    let count = 0;
    s.split("").forEach(e => {
        if (obj[e] % 2 !== 0) {
            res.push(e);
            count++;
        } else {
            const curr = res[res.length - 1];
            if (obj[e] === obj[curr] + 1) {
                res.pop();
            }
            count--;
        }
    });
    return !res.length && !count;
}

validParen(")()()(");
```
Merge K sorted Lists:
```javascript
const list1 = { val: -2, next: { val: 1, next: { val: 4, next: { val: 5, next: null } } } };
const list2 = { val: -2, next: { val: 5, next: { val: 6, next: null } } };
const list3 = { val: -2, next: { val: 0, next: null } };

function merge(l1, l2) {
    let tail = {};
    const dummyHead = tail;
    while (l1 && l2) {
        if (l1.val < l2.val) {
            tail.next = l1;
            l1 = l1.next;
        } else {
            tail.next = l2;
            l2 = l2.next;
        }
        tail = tail.next;
    }
    tail.next = l1 || l2;
    return dummyHead.next;
}

function mergeKLists(lists) {
    if (!lists.length) {
        return null;
    }
    let result = lists[0];
    for (let i = 1; i < lists.length; i++) {
        result = merge(result, lists[i]);
    }
    return result;
}

console.log(JSON.stringify(mergeKList([list1, list2, list3])));
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
    (function recurse(i, str = "") {
        if (i === digits.length) {
            return res.push(str);
        }
        obj[digits[i]].forEach(e => {
            recurse(i + 1, str + e);
        });
    })(0);
    return res;
}

letterCombinations("234");
```
Generate n numbers of proper Parentheses set:
```javascript
function generate(n) {
	const res = [];
    (function recurse(str, i, j) {
        if (i > j) {
            return;
        }
        if (i === 0 && j === 0) {
            return res.push(str);
        }
        if (i > 0) {
            recurse(str + "(", i - 1, j);
        }
        if (j > 0) {
            recurse(str + ")", i, j - 1);
        }
    })("", n, n);
    return res;
}

generate(3); // [ '((()))', '(()())', '(())()', '()(())', '()()()' ]
```
Longest Consecutive Sequence
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.
Your algorithm should run in O(n) complexity.
```javascript
function longestConsecutive(nums) {
    if (!nums || !nums.length) {
        return 0;
    }
    nums.sort((a, b) => a - b);
    let max = 1, track = 1;
    for(let i = 1; i < nums.length; i++) {
        if (nums[i] !== nums[i - 1]) {
            if (nums[i] - 1 === nums[i - 1]) {
                track++;
            } else {
                max = Math.max(max, track);
                track = 1;
            }
        }
    }
    max = Math.max(max, track);
    return max;
}

longestConsecutive([100, 4, 200, 1, 3, 2]); // -> 4
```
Island Perimeter
```javascript
const island = [
    [0, 1, 0, 0],
    [1, 1, 1, 0],
    [0, 1, 0, 0],
    [1, 1, 0, 0]
];

function islandPerimeter(grid) {
    let sum = 0
    if (!grid || !grid.length || !grid[0].length) {
        return sum;
    }
    grid.forEach((row, i) => {
        row.forEach((e, j) => {
            if (e) {
                let count = 0;
                if (i === 0) {
                    count++;
                }
                if (i === grid.length - 1) {
                    count++;
                }
                if (j === 0) {
                    count++;
                }
                if (j === row.length - 1) {
                    count++;
                }
                const xDir = [-1, 1, 0, 0];
                const yDir = [0, 0, -1, 1];
                xDir.forEach((e, index) => {
                    const x = i + e;
                    const y = j + yDir[index];
                    if (x >= 0 && x < grid.length && y >= 0 && y < row.length && !grid[x][y]) {
                        count++;
                    }
                });
                sum += count;
            }
        });
    });
    return sum;
}

islandPerimeter(island);
```
Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place.
The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.
```javascript
function judgeCircle(moves) {
    if (!moves) {
        return true;
    }
    const pos = [0, 0]
    moves.split("").forEach(e => {
        if (e === "L") {
            pos[1]--;
        } else if (e === "R") {
            pos[1]++;
        } else if (e === "U") {
            pos[0]--;
        } else if (e === "D") {
            pos[0]++;
        }
    });
    return pos[0] === 0 && pos[1] === 0;
}

judgeCircle("LDRRLRUULR");
```
Search a 2D Matrix II
```javascript
const arr = [
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
];

function searchMatrix(matrix, target) {
	if (!matrix || !matrix.length || !matrix[0].length) {
        return false;
    }
    let row = matrix.length - 1, col = 0;
    while (row >= 0 && col < matrix[row].length) {
        if (matrix[row][col] > target) {
            row--;
        } else if (matrix[row][col] < target) {
            col++;
        } else {
            return true;
        }
    }
    return false;
}

searchMatrix(arr, 6); // time complexity -> O(n * m)
```
Reverse just the vowels of the string
```javascript
function reverseVowels(s) {
    const arr = s.split(""), regEx = (/[aeiouAEIOU]/);
    let start = 0, end = arr.length - 1;
    while (start < end) {
        if (!regEx.test(arr[start])) {
            start++;
        } else if (!regEx.test(arr[end])) {
            end--;
        } else {
            const temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
    return arr.join("");
}

reverseVowels("leetcode"); // -> "leotcede"
```
