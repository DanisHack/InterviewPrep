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
Given a string containing only digits, restore it by returning all possible valid IP address combinations.
```javascript
function isValid(str) {
    if (!str || str.length > 3) {
        return false;
    }
    if (str[0] === "0" && str.length !== 1) {
        return false;
    }
    if (str.length === 3 && parseInt(str) > 255) {
        return false;
    }
    return true;
}

function validIpAddress(s) {
    const res = [], ipNums = [];
    (function findIp(i) {
        if (ipNums.length === 4) {
            if (i === s.length) {
                res.push(ipNums.join("."));
            }
            return;
        }
        for (let j = i; j < i + 3 && j < s.length; j++) {
            const str = s.slice(i, j + 1);
            if (isValid(str)) {
                ipNums.push(str);
                findIp(j + 1);
                ipNums.pop();
            }
        }
    })(0);
    return res;
}

validIpAddress("25525511135");
```
Sudoku Validator
```javascript
const board = [
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
];

function isValidSudoku(board) {
    if (!board || board.length !== 9 || board[0].length !== 9) {
        return false;
    }
    for (let i = 0; i < 9; i++) {
        const track = {};;
        for (let j = 0; j < 9; j++) {
            if (board[i][j] !== ".") {
                if (track[board[i][j]]) {
                    return false;
                }
                track[board[i][j]] = true;
            }
        }
    }
    for (let j = 0; j < 9; j++) {
        const track = {};
        for (let i = 0; i < 9; i++) {
            if (board[i][j] !== ".") {
                if (track[board[i][j]]) {
                    return false;
                }
                track[board[i][j]] = true;
            }
        }
    }
    for (let block = 0; block < 9; block++) {
        const track = {};
        for (let i = Math.floor(block / 3) * 3; i < Math.floor(block / 3) * 3 + 3; i++) {
            for (let j = block % 3 * 3; j < block % 3 * 3 + 3; j++) {
                if (board[i][j] !== ".") {
                    if (track[board[i][j]]) {
                        return false;
                    }
                    track[board[i][j]] = true;
                }
            }
        }
    }
    return true;
}

isValidSudoku(board);
```
solve sudoku:
```javascript
const board = [
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
];

function isValid(board, row, col) {
    let track = {};
    for (let i = 0; i < 9; i++) {
        if (board[row][i] !== ".") {
            if (track[board[row][i]]) {
                return false;
            }
            track[board[row][i]] = true;
        }
    }
    track = {};
    for (let i = 0; i < 9; i++) {
        if (board[i][col] !== ".") {
            if (track[board[i][col]]) {
                return false;
            }
            track[board[i][col]] = true;
        }
    }
    track = {};
    for (let i = 0; i < 3; i++) {
        const x = Math.floor(row / 3) * 3 + i;
        for (let j = 0; j < 3; j++) {
            const y = Math.floor(col / 3) * 3 + j;
            if (board[x][y] !== ".") {
                if (track[board[x][y]]) {
                    return false;
                }
                track[board[x][y]] = true;
            }
        }
    }
    return true;
}

function solveSudoku(board) {
    for (let i = 0; i < 9; i++) {
        for (let j = 0; j < 9; j++) {
            if (board[i][j] === ".") {
                for (let k = 1; k <= 9; k++) {
                    board[i][j] = k.toString();
                    if (isValid(board, i, j) && solveSudoku(board)) {
                        return true;
                    }
                    board[i][j] = ".";
                }
                return false;
            }
        }
    }
    return true;
}

solveSudoku(board);
console.log(board);
```
Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.
```javascript
const matrix = [
    ["1","0","1","0","0"],
    ["1","0","1","1","1"],
    ["1","1","1","1","1"],
    ["1","0","0","1","0"]
];

function largestRectangleArea(heights) {
    let res = 0;
    if (!heights || !heights.length) {
        return res;
    }
    const stack = [];
    let i = 0;
    while (i <= heights.length) {
        if (!stack.length || heights[stack[stack.length - 1]] <= heights[i]) {
            stack.push(i);
            i++;
        } else {
            const height = heights[stack.pop()];
            const width = !stack.length ? i : i - stack[stack.length - 1] - 1;
            res = Math.max(res, height * width);
        }
    }
    return res;
};

function maximalRectangle(matrix) {
    let res = 0;
    if (!matrix || !matrix.length || !matrix[0].length) {
        return res;
    }
    const heights = arr.map(row => row.map(() => 0));
    matrix.forEach((row, i) => {
        row.forEach((e, j) => {
            if (e === "1") {
                heights[i][j] = i === 0 ? 1 : heights[i - 1][j] + 1;
            }
        });
        res = Math.max(res, largestRectangleArea(heights[i]));
    });
    return res
};

maximalRectangle(matrix);
```
Given an integer matrix, find the length of the longest increasing path.
From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).
```javascript
const arr = [
    [3, 4, 5],
    [3, 2, 6],
    [2, 2, 1]
];

function dfs(nums, row, col, mem) {
    if (mem[row][col] !== 0) {
        return mem[row][col];
    }
    const xDir = [-1, 1, 0, 0];
    const yDir = [0, 0, -1, 1];
    xDir.forEach((e, i) => {
        const x = row + e;
        const y = col + yDir[i];
        if (x >= 0 && y >= 0 && x < nums.length && y < nums[0].length && nums[x][y] > nums[row][col]) {
            mem[row][col] = Math.max(mem[row][col], dfs(nums, x, y, mem));
        }
    });
    mem[row][col]++;
    return mem[row][col];
}

function longestIncreasingPath(nums) {
    if (!nums || !nums.length || !nums[0].length) {
        return 0;
    }
    const mem = nums.map(row => row.map(() => 0));
    let longest = 0;
    nums.forEach((row, i) => {
        row.forEach((e, j) => {
            longest = Math.max(longest, dfs(nums, i, j, mem));
        });
    });
    return longest;
}

longestIncreasingPath(arr);
```
Given a m x n matrix, if an element is 0, set its entire row and column to 0
```javascript
const a = [
  [1, 1, 1],
  [1, 0, 1],
  [1, 1, 1]
];

function setZeroes(arr) {
    let row = false, col = false;
    const n = arr.length, m = arr[0].length;
    for (let i = 0; i < m; i++) {
        if (arr[0][i] === 0) {
            row = true;
            break;
        }
    }
    for (let i = 0; i < n; i++) {
        if (arr[i][0] === 0) {
            col = true;
            break;
        }
    }
    for (let i = 1; i < n; i++) {
        for (let j = 1; j < m; j++) {
            if (arr[i][j] === 0) {
                arr[i][0] = 0;
                arr[0][j] = 0;
            }
        }
    }
    for (let i = 1; i < n; i++) {
        for (let j = 1; j < m; j++) {
            if (arr[i][0] === 0 || arr[0][j] === 0) {
                arr[i][j] = 0;
            }
        }
    }
    if (row) {
        for (let i = 0; i < m; i++) {
            arr[0][i] = 0;
        }
    }
    if (col) {
        for (let i = 0; i < n; i++) {
            arr[i][0] = 0;
        }
    }
    return arr;
}

setZeroes(a);
```
