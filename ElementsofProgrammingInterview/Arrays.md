Input is an array of integers, reorder its entries so that the even entries appear first:
```javascript
function evenOdd(nums) {
    let even = 0, odd = nums.length - 1;
    while (even < odd) {
        if (nums[even] % 2 === 0) {
            even++;
        } else {
            const temp = nums[even];
            nums[even] = nums[odd];
            nums[odd] = temp;
            odd--;
        }
    }
    return nums;
}

evenOdd([1, 2, 3, 5, 6, 8]); // time complexity: O(n) [ 8, 2, 6, 5, 3, 1 ]
```
Takes an array A and index i into A, and rearranges the elements such that all elements less than A[i]("pivot") appear first, followed by elements equal to the pivot followed by elements greater than the pivot:
```javascript
function rearrange(a, i) {
    const pivot = a[i];
    let small = 0, equal = 0, big = a.length - 1;
    while (equal <= big) {
        if (a[equal] < pivot) {
            const temp = a[equal];
            a[equal] = a[small];
            a[small] = temp;
            equal++;
            small++;
        } else if (a[equal] === pivot) {
            equal++;
        } else {
            const temp = a[equal];
            a[equal] = a[big];
            a[big] = temp;
            big--;
        }
    }
    return a;
}

rearrange([0, 1, 2, 0, 2, 1, 1], 3); // [ 0, 0, 2, 2, 1, 1, 1 ]
```
Multiply two arbitrary integers:
```javascript
function multiply(num1, num2) {
    const sign = (num1[0] < 0 && num2[0] > 0) || (num2[0] < 0 && num1[0] > 0) ? -1 : 1;
    num1[0] = Math.abs(num1[0]), num2[0] = Math.abs(num2[0]);
    const arr = Array(num1.length + num2.length).fill(0);
    for (let i = num1.length - 1; i >= 0; i--) {
        for (let j = num2.length - 1; j >= 0; j--) {
            arr[i + j + 1] += num1[i] * num2[j];
            arr[i + j] += Math.floor(arr[i + j + 1] / 10);
            arr[i + j + 1] %= 10;
        }
    }
    while (arr[0] === 0) {
        arr.shift();
    }
    arr[0] *= sign;
    return arr;
}

multiply([-1, 3, 9], [2, 8]);
```
Given an array of non-negative integers, you are initially positioned at the first index of the array.
Each element in the array represents your maximum jump length at that position.
Your goal is to reach the last index in the minimum number of jumps.
```javascript
function minimumPath(nums) {
    if (!nums || !nums.length) {
        return 0;
    }
    let lastReach = 0, reach = 0, jump = 0;
    for (let i = 0; i <= reach && i < nums.length; i++) {
        if (i > lastReach) {
            lastReach = reach;
            jump++;
        }
        reach = Math.max(reach, nums[i] + i);
    }
    if (reach < nums.length - 1) {
        return 0;
    }
    return jump;
}

minimumPath([3, 3, 1, 0, 2, 0, 1]); // 3
```
Delete Duplicated from a sorted Array:
```javascript
function removeDuplicate(nums) {
    if (!nums.length) {
        return nums;
    }
    let lastIndex = 1;
    for (let i = 1; i < nums.length; i++) {
        if (nums[lastIndex - 1] !== nums[i]) {
            nums[lastIndex] = nums[i];
            lastIndex++;
        }
    }
    return nums.slice(0, lastIndex);
}

removeDuplicate([2, 3, 5, 5, 7, 11, 11, 11, 13]);

function removeTarget(nums, target) {
    if (!nums.length) {
        return 0;
    }
    let lastIndex = 0;
    nums.forEach((e, i) => {
        if (nums[i] !== target) {
            nums[lastIndex] = nums[i];
            lastIndex++;
        }
    });
    return nums.slice(0, lastIndex);
}

removeTarget([2, 3, 5, 5, 7, 11, 11, 11, 13], 11);
```
Buy and Sell a stock once:
```javascript
function buySellStock(prices) {
    let mostProfit = 0, prevIndex = 0;
    prices.forEach((e, i) => {
        const diff = e - prices[prevIndex];
        if (diff > mostProfit) {
            mostProfit = diff;
        } else if (diff < 0) {
            prevIndex = i;
        }
    });
    return mostProfit;
}

buySellStock([310, 315, 275, 295, 260, 270, 290, 230, 255, 250]);
```
Generate prime from 1 to n:
```javascript
function generatePrime(n) {
    const isPrime = [false, false].concat(Array(n - 1).fill(true)), res = [];
    isPrime.forEach((e, i) => {
        if (e) {
            res.push(i);
            for (let p = i; p <= n; p += i) {
                isPrime[p] = false;
            }
        }
    });
    return res;
}

generatePrime(35);
```
Give the spiral order of a NxN matrix and to generate a NxN spiral matrix:
```javascript
function generateSpiralMatrix(n) {
    const res = Array(n).fill().map(() => []);
    let left = 0, top = 0, right = n - 1, bottom = n - 1, count = 1;
    while (count <= n * n) {
        for (let i = left; i <= right; i++) {
            res[top][i] = count;
            count++;
        }
        top++;
        for (let i = top; i <= bottom; i++) {
            res[i][right] = count;
            count++;
        }
        right--;
        for (let i = right; i >= left; i--) {
            res[bottom][i] = count;
            count++;
        }
        bottom--;
        for (let i = bottom; i >= top; i--) {
            res[i][left] = count;
            count++;
        }
        left++;
    }
    return res;
}

generateSpiralMatrix(4);
```
Rotate a NxN matrix 90 degree:
```javascript
const matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
];

function rotateMatrix(arr) {
    for (let i = 0; i < arr.length / 2; i++) {
        for (let j = 0; j < Math.floor(arr.length / 2); j++) {
            const temp = arr[i][j];
            arr[i][j] = arr[arr.length - 1 - j][i];
            arr[arr.length - 1 - j][i] = arr[arr.length - 1 - i][arr.length - 1 - j];
            arr[arr.length - 1 - i][arr.length - 1 - j] = arr[j][arr.length - 1 - i];
            arr[j][arr.length - 1 - i] = temp;
        }
    }
    return arr;
}

rotateMatrix(matrix);
```
Generate Pascal Triangle:
```javascript
function generatePascalTri(n) {
    const res = [[1], [1, 1]];
    if (res.length > n) {
        return res[n];
    }
    for (let i = 2; i < n; i++) {
        const current = [1];
        for (let j = 0; j < res[i - 1].length - 1; j++) {
            current.push(res[i - 1][j] + res[i - 1][j + 1]);
        }
        current.push(1);
        res.push(current);
    }
    return res;
}

generatePascalTri(5); // [ [ 1 ], [ 1, 1 ], [ 1, 2, 1 ], [ 1, 3, 3, 1 ], [ 1, 4, 6, 4, 1 ] ]
```
Container With Most Water:
```javascript
function maxArea(height) {
    let max = 0, left = 0, right = height.length - 1;
    while (left < right) {
        max = Math.max(max, Math.min(height[left], height[right]) * (right - left));
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    return max;
}

maxArea([1, 8, 6, 2, 5, 4, 8, 3, 7]); // 49
// good link: https://leetcode.com/articles/container-most-water/
```
Given a sorted array of numbers, write a function to return a range summary of the array.
```javascript
const arr = [0,3,4,5];

function createRange(arr) {
    const res = [[arr[0]]];
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] - arr[i - 1] > 1) {
            if (i - 1 !== 0) {
                res[res.length - 1].push(arr[i - 1]);
            }
            res.push([arr[i]]);
        }
    }
    res[res.length - 1].push(arr[arr.length - 1]);
    return res;
}

createRange(arr);
