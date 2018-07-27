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
