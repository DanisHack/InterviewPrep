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
		} else if (memo[n] > -1) {
			return memo[n];
		} else {
			memo[n] = recurse(n - 1) + recurse(n - 2) + recurse(n - 3);
			return memo[n];
		}
	})(n);
}
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
        console.log(i, j)
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
    })(0, 0);
    return path.reverse();
}

findPath(grid);
```
