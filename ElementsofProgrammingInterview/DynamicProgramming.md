Count the number of score combinations from [2, 3, 7]:
```javascript
/* recursion solution
    function combination(n) {
        const points = [2, 3, 7];
        let sum = 0;
        (function recurse(index, num) {
            if (num === n) {
                sum++;
                return;
            } else if (num < n) {
                for (let i = index; i < points.length; i++) {
                    recurse(i, num + points[i]);
                }
            }
        })(0, 0);
        return sum;
    }

    combination(12);
*/
function combination(n) {
    const points = [2, 3, 7];
    const comb = points.map(() => [1].concat(Array(n).fill(0)));
    points.forEach((val, i) => {
        for (let j = 1; j <= n; j++) {
            const withoutScore = i >= 1 ? comb[i - 1][j] : 0;
            const withScore = j >= points[i] ? comb[i][j - points[i]] : 0;
            comb[i][j] = withoutScore + withScore;
        }
    });
    return comb[points.length - 1][n];
}

combination(12);
```
Use the Levenshtein Algorithm to calculate the minimum changes require for two words:
```javascript
function levenshtein(a, b) {
    const dist = a.split("").map(() => Array(b.length).fill(-1));
    return (function compute(aIndex, bIndex) {
        if (aIndex < 0 || bIndex < 0) {
            return (aIndex < 0 ? bIndex : aIndex) + 1;
        }
        if (dist[aIndex][bIndex] === -1) {
            if (a[aIndex] === b[bIndex]) {
                dist[aIndex][bIndex] = compute(aIndex - 1, bIndex - 1);
            } else {
                const sub = compute(aIndex - 1, bIndex - 1);
                const add = compute(aIndex - 1, bIndex);
                const del = compute(aIndex, bIndex - 1);
                dist[aIndex][bIndex] = Math.min(sub, add, del) + 1;
            }
        }
        return dist[aIndex][bIndex];
    })(a.length - 1, b.length - 1);
}

levenshtein("Saturday", "Sundays"); // 4
```
Count the Number of Ways to traverse a 2D Array:
```javascript
function nWays(n, m) {
    const ways = Array(n).fill().map(() => Array(m).fill(0));
    return (function computed(x, y) {
        if (x === 0 && y === 0) {
            return 1;
        }
        if (ways[x][y] === 0) {
            const waysTop = x === 0 ? 0 : computed(x - 1, y);
            const waysLeft = y === 0 ? 0 : computed(x, y - 1);
            ways[x][y] = waysTop + waysLeft;
        }
        return ways[x][y];
    })(n - 1, m - 1);
}

nWays(5, 5);
```
Calculate Binomial Coefficient:
```javascript
// http://mathworld.wolfram.com/images/equations/BinomialCoefficient/NumberedEquation1.gif
function binomialCoefficient(n, k) {
    const memo = Array(n + 1).fill().map(() => Array(k + 1).fill(0));
    return (function compute(x, y) {
        if (y === x || y === 0) {
            return 1;
        }
        if (memo[x][y] === 0) {
            const withoutY = compute(x - 1, y);
            const withY = compute(x - 1, y - 1);
            memo[x][y] = withoutY + withY;
        }
        return memo[x][y];
    })(n, k);
}

binomialCoefficient(5, 2);
```
Search for for the sequence in a 2D array:
```javascript
const arr = [
    [1, 2, 3],
    [3, 4, 5],
    [5, 6, 7]
];

function patternSearch(grid, pattern) {
    const result = [];
    return (function search(row, col) {
        if (!result.length && pattern[result.length] !== grid[row][col]) {
            return false;
        }
        result.push(grid[row][col]);
        if (result.length === pattern.length) {
            return true;
        }
        if (col < grid[0].length - 1 && pattern[result.length] === grid[row][col + 1]) {
            return search(row, col + 1);
        } else if (row < grid.length - 1 && pattern[result.length] === grid[row + 1][col]) {
            return search(row + 1, col);
        }
        return false;
    })(0, 0);
}

patternSearch(arr, [1, 3, 4, 6]);
```
Knapsack Problem:
```javascript
const items = [
    { value: 65, weight: 20 },
    { value: 35, weight: 8 },
    { value: 245, weight: 60 },
    { value: 195, weight: 55 },
    { value: 65, weight: 40 },
    { value: 150, weight: 70 },
    { value: 275, weight: 85 },
    { value: 155, weight: 25 },
    { value: 120, weight: 30 },
    { value: 320, weight: 65 },
    { value: 75, weight: 75 },
    { value: 40, weight: 10 },
    { value: 200, weight: 95 },
    { value: 100, weight: 50 },
    { value: 220, weight: 40 },
    { value: 99, weight: 10 }
];

function optimalCapacity(items, cap) {
    const v = items.map(() => Array(cap + 1).fill(-1));
    return (function compute(k, weight) {
        if (k < 0) {
            return 0;
        }
        if (v[k][weight] === -1) {
            const withoutCurr = compute(k - 1, weight);
            const withCurr = items[k].weight > weight ? 0 : items[k].value + compute(k - 1, weight - items[k].weight);
            v[k][weight] = Math.max(withoutCurr, withCurr);
        }
        return v[k][weight];
    })(items.length - 1, cap);
}

optimalCapacity(items, 130);
```
Find the minimum weight path in triangle:
```javascript
const tri = [[2], [4, 4], [8, 5, 6], [4, 2, 6, 2], [1, 5, 2, 3, 4]];

function minimumPathWeight(tri) {
    let minPath = [0];
    tri.forEach(row => {
        minPath = row.map((_, i) => row[i] + Math.min(minPath[Math.max(i - 1, 0)], minPath[Math.min(i, minPath.length - 1)]));
    });
    return Math.min(...minPath);
}

minimumPathWeight(tri);
```
Pick up coins for Maximum gain:
```javascript
function maxRevenue(coins) {
    const max = coins.map(() => Array(coins.length).fill(0));
    return (function compute(a, b) {
        if (a > b) {
            return 0;
        }
        if (max[a][b] === 0) {
            const bothAandB = compute(a + 1, b - 1);
            const maxA = coins[a] + Math.min(compute(a + 2, b), bothAandB);
            const maxB = coins[b] + Math.min(bothAandB, compute(a, b - 2));
            max[a][b] = Math.max(maxA, maxB);
        }
        return max[a][b];
    })(0, coins.length - 1);
}

maxRevenue([5, 25, 10, 1]);
```
Count the Number of Moves to Climb Stairs:
```javascript
function countStairs(n, k) {
    const ways = Array(n + 1).fill(0);
    return (function compute(h) {
        if (h <= 1) {
            return 1;
        }
        if (ways[h] === 0) {
            const toSum = [];
            for (let i = 1; i < Math.min(k, h) + 1; i++) {
                toSum.push(compute(h - i));
            }
            ways[h] = toSum.reduce((sum, val) => sum + val, 0);
        }
        return ways[h];
    })(n);
}

countStairs(4, 2);
```
Find the longest nondecreasing subsequence:
```javascript
function longestIncreasing(arr) {
    const maxLength = Array(arr.length).fill(1);
    for (let i = 1; i < arr.length; i++) {
        let maxNum = -Infinity;
        for (let j = 0; j < i; j++) {
            if (arr[i] >= arr[j] && maxLength[j] > maxNum) {
                maxNum = maxLength[j];
            }
        }
        maxLength[i] = Math.max(1 + maxNum, maxLength[i]);
    }
    return Math.max(...maxLength);
}

longestIncreasing([0, 8, 4, 12, 2, 10, 6, 14, 1, 9]);
```
