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
    const heights = [];
    matrix.forEach((row, i) => {
        heights.push(Array(row.length).fill(0));
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
