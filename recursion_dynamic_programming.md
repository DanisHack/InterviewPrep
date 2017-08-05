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
