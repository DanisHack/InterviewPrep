Reverse a Integer without converting to string:
```javascript
function reverse(n) {
	let result = 0, num = n;
	while (num > 0) {
	    result = result * 10 + num % 10;
	    num = Math.floor(num / 10);
	}
	return result;
}

reverse(5432); // 2345
```
Swapping numbers without using a third variable:

```javascript
let a = 157;
let b = 230;

function swap() {
    a = a - b;
    b = b + a;
    a = b - a;
}

swap();
console.log(a, b); // 230, 157
```
Find the maximum without using if/else or comparison operator:
```javascript
function findMax(a, b){
    const diff = a - b;
    const k = (diff >> 31) * -1;
    return a - k * diff;
}

findMax(3, 100); // 100
```
Ways a child can run up a stairs with steps 1, 2, or 3 (memoization):
```javascript
function countWays(n) {
	const memo = [];
	return (function recurse(n) {
		if (n < 0) {
			return 0;
		} else if (n === 0) {
			return 1;
		} else if (memo[n]) {
			return memo[n];
		} else {
			memo[n] = recurse(n - 1) + recurse(n - 2) + recurse(n - 3);
			return memo[n];
		}
	})(n);
}

countWays(4); // 7
```
Find path for a Robot on a grid:
```javascript
const grid = [
    [1, 1, 0, 1],
    [1, 0, 1, 0],
    [1, 1, 1, 1]
];

function findPath(grid) {
    const path = [];
    (function recurse(i, j) {
        if (i >= grid.length || j >= grid[0].length || !grid[i][j]) {
            return false;
        }
        if (i === grid.length - 1 && j === grid[0].length - 1) {
            path.push(`${i}${j}`);
            return true;
        }
        if (recurse(i, j + 1)) {
            path.push(`${i}${j}`);
            return true;
        }
        if (recurse(i + 1, j)) {
            path.push(`${i}${j}`);
            return true;
        }
		return false;
    })(0, 0);
    return path.reverse();
}

findPath(grid);
```
Find a magic index where the index equal to its value:
```javascript
const arr1 = [-40, -20, -1, 1, 2, 3, 5, 7, 9, 12, 13];

// handles data that have only distinct values
function magicIndexDistinct(arr, start = 0, end = arr.length - 1){
    if (start > end) {
        return -1;
    }
    const middle = Math.floor((start + end) / 2);
    if (arr[middle] === middle) {
        return middle;
    } else if (arr[middle] > middle) {
        return magicIndexDistinct(arr, start, middle - 1);
    }
    return magicIndexDistinct(arr, middle + 1, end);
}

magicIndexDistinct(arr1);

const arr2 = [-10, -5, 2, 2, 2, 3, 4, 7, 9, 12, 13];

// handles array that have non distinct values
function magicIndexNonDistinct(arr, start = 0, end = arr.length - 1) {
    if (start > end) {
        return -1;
    }
    const middle = Math.floor((start + end) / 2);
    const midValue = arr[middle];
    if (middle === midValue) {
        return middle;
    }
    const leftIndex = Math.min(middle - 1, midValue);
    const left = magicIndexNonDistinct(arr, start, leftIndex);
    if (left >= 0) {
        return left;
    }
    const rightIndex = Math.max(middle + 1, midValue);
    const right = magicIndexNonDistinct(arr, rightIndex, end);
    return right;
}

magicIndexNonDistinct(arr2);
```
Write a method to return all subsets of a set:
```javascript
function getSubsets(set, index = 0) {
	if (index === set.length) {
		return [[]]
	}
	const result = getSubsets(set, index + 1);
	const item = set[index];
	const newSubsets = result.map(subset => subset.concat(item));
	return result.concat(newSubsets);
}

// time complexity: O(n2^n)
getSubsets([1, 2, 3]); // [ [], [ 3 ], [ 2 ], [ 3, 2 ], [ 1 ], [ 3, 1 ], [ 2, 1 ], [ 3, 2, 1 ] ]
```
A recursive function that multiplies two integers without the * operator:
```javascript
function multiply(x, y) {
	if (y === 0) {
		return 0;
	} else if (y > 0) {
		return x + multiply(x, y - 1);
	}
	return -multiply(x, -y);
}

multiply(5, -11); // -55
```
Moving Discs in Tower of Hanoi:
```javascript
const jar1 = {
    name: "jar1",
    jar: [1, 2, 3]
};
const jar2 = {
    name: "jar2",
    jar: []
};
const jar3 = {
    name: "jar3",
    jar: []
};

function hanoi(disc, src, buffer, dest) {
	if (disc <= 0) {
		return;
	}
	hanoi(disc - 1, src, dest, buffer);
	src.jar.shift();
	dest.jar.unshift(disc);
	console.log(src, buffer, dest);
	hanoi(disc - 1, buffer, src, dest);
}

hanoi(3, jar1, jar2, jar3);
```
Anagram of a word:
```javascript
function anagram(str) {
    const map = {};
    (function recurse(current, remain) {
        current.split("").forEach((e, i) => {
            const tail = current.slice(0, i) + current.slice(i + 1);
            const word = remain + e + tail;
            if (!map[word]) {
                map[word] = true;
            }
            if (current.length > 1) {
                recurse(tail, remain + e);
            }
        });
    })(str, "");
    return Object.keys(map);
}

anagram("ABCA");
```
Generate n numbers of proper Parentheses set:
```javascript
function generate(n) {
    const result = [];
    (function recurse(str, i, j) {
        if (i > j) {
            return;
        }
        if (i === 0 && j === 0) {
            result.push(str);
            return;
        }
        if (i > 0) {
            recurse(str + "(", i - 1, j);
        }
        if (j > 0) {
            recurse(str + ")", i, j - 1);
        }
    })("", n, n);
    return result;
}

generate(3); // [ '((()))', '(()())', '(())()', '()(())', '()()()' ]
```
Implement Paint Fill method:
```javascript
const screen = [
    [1, 1, 1, 1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1, 1, 0, 0],
    [1, 0, 0, 1, 1, 0, 1, 1],
    [1, 2, 2, 2, 2, 0, 1, 0],
    [1, 1, 1, 2, 2, 0, 1, 0],
    [1, 1, 1, 2, 2, 2, 2, 0],
    [1, 1, 1, 1, 1, 2, 1, 1],
    [1, 1, 1, 1, 1, 2, 2, 1]
];

function paintFill(screen, x, y, newColor) {
    const visited = {};
    (function recurse(x, y) {
        const key = `${x}${y}`;
        if (visited[key] || x >= screen.length || y >= screen[0].length || x < 0 || y < 0) {
            return;
        }
        if (screen[x][y] === newColor - 1) {
            screen[x][y] = newColor;
            visited[key] = true;
            recurse(x - 1, y);
            recurse(x, y - 1);
            recurse(x + 1, y);
            recurse(x, y + 1);
        }
    })(x, y);
    return screen;
}

paintFill(screen, 4, 4, 3);
```
Ways to put 8 queens on a 8x8 board:
```javascript
function isValid(combo, row1, col1) {
    for (let row2 = 0; row2 < row1; row2++) {
        const col2 = combo[row2];
        if (col1 === col2) {
            return false;
        }
        const colDistance = Math.abs(col2 - col1);
        const rowDistance = row1 - row2;
        // this is to check diagonally, if it is equal, it is diagonal
        if (colDistance === rowDistance) {
            return false;
        }
    }
    return true;
}

function placeQueens(n) {
    const result = [];
    const combo = [];
    (function recurse(row) {
        if (row === n) {
            result.push([...combo]);
            return;
        }
        for (let col = 0; col < n; col++) {
            if (isValid(combo, row, col)) {
                combo[row] = col;
                recurse(row + 1);
            }
        }
    })(0);
    return result;
}

placeQueens();
```
