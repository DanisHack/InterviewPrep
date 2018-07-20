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
// time complexity: O(sn), space complexity: O(sn)
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
// time complexity: O(ab), space complexity: O(ab)
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
// time complexity: O(nm), space complexity: O(nm)
```
Given a grid with obstacles represented by 1, count the number of ways to traverse the grid
```javascript
const grid = [
  [0, 0, 0],
  [0, 1, 0],
  [0, 0, 0]
];

function nWays(board) {
    if (!board || !board.length) {
        return 0;
    }
    const n = board.length, m = board[0].length;
    if (board[0][0] || board[n - 1][m - 1]) {
        return 0;
    }
    const memo = board.map(row => row.map(() => 0));
    for (let i = 0; i < m; i++) {
        if (!board[0][i]) {
            memo[0][i] = 1;
        } else {
            break;
        }
    }
    for (let i = 1; i < n; i++) {
        for (let j = 0; j < m; j++) {
            if (!board[i][j]) {
                memo[i][j] = memo[i - 1][j] + (j >= 1 ? memo[i][j - 1] : 0);
            }
        }
    }
    return memo[n - 1][m - 1];
}

nWays(grid);
```
Calculate Binomial Coefficient:
```javascript
// http://mathworld.wolfram.com/BinomialCoefficient.html
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
// time complexity: O(nk), space complexity: O(nk)
```
Search for the sequence in a 2D array:
```javascript
const arr = [
    [1, 2, 3],
    [3, 4, 5],
    [5, 6, 7]
];

function patternSearch(grid, pattern) {
    const res = [], visited = {};
    function recurse(i, j) {
        const key = `${i}${j}`;
        if (i < 0 || j < 0 || visited[key]) {
            return;
        }
        visited[key] = true;
        if (grid[i][j] === pattern[res.length]) {
            res.push(grid[i][j]);
        }
        for (let row = i - 1; row <= i + 1 && row < grid.length; row++) {
            for (let col = j - 1; col <= j + 1 && col < grid[i].length; col++) {
                recurse(row, col);
            }
        }
    }
    grid.forEach((e, i) => {
        e.forEach((d, j) => {
            recurse(i, j);
        });
    });
    return res.length === pattern.length
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
// time complexity: O(nw), space complexity: O(nw)
```
Find the minimum weight path in triangle:
```javascript
const tri = [[2], [4, 4], [8, 5, 6], [4, 2, 6, 2], [1, 5, 2, 3, 4]];

function minimumPathWeight(tri) {
    let minPath = [0];
    tri.forEach(row => {
        minPath = row.map((e, i) => e + Math.min(minPath[Math.max(i - 1, 0)], minPath[Math.min(i, minPath.length - 1)]));
    });
    return Math.min(...minPath);
}

minimumPathWeight(tri);
// time complexity: O(n^2), space complexity: O(n)
```
Pick up coins for Maximum gain:
Consider a row of n coins of values v1 . . . vn, where n is even. We play a game against an opponent by alternating turns. In each turn, a player selects either the first or last coin from the row, removes it from the row permanently, and receives the value of the coin. Determine the maximum possible amount of money we can definitely win if we move first.
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
// time complexity: O(n^2)
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
            for (let i = 1; i <= Math.min(k, h); i++) {
                toSum.push(compute(h - i));
            }
            ways[h] = toSum.reduce((sum, val) => sum + val, 0);
        }
        return ways[h];
    })(n);
}

countStairs(4, 2); // time complexity: O(kn), space complexity: O(n)
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

longestIncreasing([0, 8, 4, 12, 2, 10, 6, 14, 1, 9]); // The longest increasing subsequence is {0, 4, 10, 14}
// time complexity: O(n^2), space complexity: O(n)
```
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.
Answer is 7 because the path 1→3→1→1→1 minimizes the sum.
```javascript
const grid = [
    [1, 3, 1],
    [1, 5, 1],
    [4, 2, 1]
];

function minPathSum(arr) {
    const res = arr.map(row => row.map(() => 0));
    const n = arr.length, m = arr[0].length;
    return (function compute(x, y) {
        if (x === n - 1 && y === m - 1) {
            return arr[x][y];
        }
        if (res[x][y] === 0) {
            if (x === n - 1) {
                res[x][y] = arr[x][y] + compute(x, y + 1);
            } else if (y === m - 1) {
                res[x][y] = arr[x][y] + compute(x + 1, y);
            } else {
                const right = arr[x][y] + compute(x, y + 1);
                const down = arr[x][y] + compute(x + 1, y);
                res[x][y] = Math.min(right, down);
            }
        }
        return res[x][y];
    })(0, 0);
}

minPathSum(grid);
```
Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.
```javascript
function isInterleave(s1, s2, s3) {
    if (s3.length !== s1.length + s2.length) {
        return false;
    }
    const dp = Array(s2.length + 1).fill(false);
    for (let i = 0; i <= s1.length; i++) {
        for (let j = 0; j <= s2.length; j++) {
            if (i === 0 && j === 0) {
                dp[j] = true;
            } else if (i === 0) {
                dp[j] = dp[j - 1] && s2[j - 1] === s3[j - 1];
            } else if (j === 0) {
                dp[j] = dp[j] && s1[i - 1] === s3[i - 1];
            } else {
                dp[j] = (dp[j] && s1[i - 1] === s3[i + j - 1]) || (dp[j - 1] && s2[j - 1] === s3[i + j - 1]);
            }
        };
    };
    return dp[s2.length];
}

isInterleave("aabcc", "dbbca", "aadbbcbcac");
```
