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

evenOdd([1, 2, 3, 5, 6, 8]); // time complexity: O(n)
```
Takes an array A and index i into A, and rearranges the elements such that all elements less than A[i]("pivot") appear first, followed by elements equal to the pivot followed by elements greater than the pivot:
```javascript
function rearrange(a, i) {
    const pivot = a[i];
    let smaller = equal = 0, bigger = a.length;
    while (equal < bigger) {
        if (a[equal] < pivot) {
            const temp = a[smaller];
            a[smaller] = a[equal];
            a[equal] = temp;
            equal++;
            smaller++;
        } else if (a[equal] === pivot) {
            equal++;
        } else {
            bigger--;
            const temp = a[equal];
            a[equal] = a[bigger];
            a[bigger] = temp;
        }
    }
    return a;
}

rearrange([0, 1, 2, 0, 2, 1, 1], 3); // [ 0, 0, 2, 2, 1, 1, 1 ]
```
Increment an Arbitrary-Precision Integer:
```javascript
function addOne(nums) {
    nums[nums.length - 1]++;
    for (let i = nums.length - 1; i > 0; i--) {
        if (nums[i] === 10) {
            nums[i] = 0;
            nums[i - 1]++;
        }
    }
    if (nums[0] === 10) {
        nums[0] = 1;
        nums.push(0);
    }
    return nums;
}

addOne([9, 9, 9]); // [1, 0, 0, 0]
```
Multiply two arbitrary integers:
```javascript
function multiply(num1, num2) {
    const sign = (num1[0] < 0 && num2[0] > 0) || (num2[0] < 0 && num1[0] > 0) ? -1 : 1;
    num1[0] = Math.abs(num1[0]), num2[0] = Math.abs(num2[0]);
    const result = Array(num1.length + num2.length).fill(0);
    for (let i = num1.length - 1; i >= 0; i--) {
        for (let j = num2.length - 1; j >= 0; j--) {
            result[i + j + 1] += num1[i] * num2[j];
            result[i + j] += Math.floor(result[i + j + 1] / 10);
            result[i + j + 1] %= 10;
        }
    }
    while (result.length) {
        if (result[0]) {
            break;
        }
        result.shift();
    }
    result[0] *= sign;
    return result;
}

multiply([-1, 3, 9], [2, 8]);
```
Advancing through an array:
```javascript
function canReachEnd(a) {
    let furthest = i = 0;
    const last = a.length - 1;
    while (i <= furthest && furthest < last) {
        furthest = Math.max(furthest, a[i] + i);
        i++;
    }
    return furthest >= last;
}

canReach(3, 3, 1, 0, 2, 0, 1);
```
Compute the minimum number of steps needed to advance to the last location:
```javascript
function minimumPath(a) {
    const path = [];
    let lastIndex = 0, i = 1, furthest = a[0];
    while (i <= furthest && furthest < a.length) {
        if (a[i] + i > a[lastIndex] + lastIndex) {
            path.push(i - lastIndex);
            lastIndex = i;
            furthest = a[i] + i;
        }
        i++;
    }
    return path;
}

minimumPath([3, 3, 1, 0, 2, 0, 1]); // [1, 3, 2]
```
Delete Duplicated from a sorted Array:
```javascript
function removeDuplicate(nums) {
    if (!nums.length) {
        return 0;
    }
    let lastIndex = 1;
    for (let i = 1; i < nums.length; i++) {
        if (nums[lastIndex - 1] !== nums[i]) {
            nums[lastIndex] = nums[i];
            lastIndex++;
        }
    }
    return lastIndex;
}

removeDuplicate([2, 3, 5, 5, 7, 11, 11, 11, 13]);

function removeTarget(nums, target) {
    if (!nums.length) {
        return 0;
    }
    let lastIndex = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== target) {
            nums[lastIndex] = nums[i];
            lastIndex++;
        }
    }
    return lastIndex;
}

removeTarget([2, 3, 5, 5, 7, 11, 11, 11, 13], 11);
```
Buy and Sell a stock once:
```javascript
function buySellStock(prices) {
    let mostProfit = 0, prevIndex = 0
    for (let i = 0; i < prices.length; i++) {
        const diff = prices[i] - prices[prevIndex];
        if (diff > mostProfit) {
            mostProfit = diff;
        } else if (diff < 0) {
            prevIndex = i;
        }
    }
    return mostProfit;
}

buySellStock([310, 315, 275, 295, 260, 270, 290, 230, 255, 250]);
```
Generate prime from 1 to n:
```javascript
function generatePrime(n) {
    const primes = [];
    const isPrime = [false, false].concat(Array(n - 1).fill(true));
    for (let p = 2; p < n; p++) {
        if (isPrime[p]) {
            primes.push(p);
            for (let i = p; i <= n; i += p) {
                isPrime[i] = false;
            }
        }
    }
    return primes;
}

generatePrime(35);
```
Give the spiral order of a NxN matrix and to generate a NxN spiral matrix:
```javascript
const arr = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

function spiralMatrix(matrix) {
    const result = [];
    let counter = 1, top = left = 0, right = bottom = arr.length - 1;
    while (counter < arr.length * arr.length) {
        for (let i = left; i <= right; i++) {
            result.push(arr[top][i]);
            counter++;
        }
        top++;
        for (let i = top; i <= bottom; i++) {
            result.push(arr[i][right]);
            counter++;
        }
        right--;
        for (let i = right; i >= left; i--) {
            result.push(arr[bottom][i]);
            counter++;
        }
        bottom--;
        for (let i = bottom; i >= top; i--) {
            result.push(arr[i][left]);
            counter++;
        }
        left++;
    }
    if (arr.length % 2 !== 0) {
        const middle = Math.floor(arr.length / 2);
        result.push(arr[middle][middle]);
    }
    return result;
}

spiralMatrix(arr); // [ 1, 2, 3, 6, 9, 8, 7, 4, 5 ]

function generateSpiralMatrix(n) {
    const result = [];
    for (let i = 0; i < n; i++) {
        result.push([]);
    }
    let currentNum = 1, top = left = 0, bottom = right = n - 1;
    while (currentNum <= n * n) {
        for (let i = left; i <= right; i++) {
            result[top][i] = currentNum;
            currentNum++;
        }
        top++;
        for (let i = top; i <= bottom; i++) {
            result[i][right] = currentNum;
            currentNum++;
        }
        right--;
        for (let i = right; i >= left; i--) {
            result[bottom][i] = currentNum;
            currentNum++;
        }
        bottom--;
        for (let i = bottom; i >= top; i--) {
            result[i][left] = currentNum;
            currentNum++;
        }
        left++;
    }
    return result;
}

generateSpiralMatrix(4);
```
Rotate a NxN matrix 90 degree:
```javascript
const arr = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
];

function rotateMatrix(matrix) {
    const result = []
    for (let i = 0; i < arr.length; i++) {
        for (j = arr.length - 1; j >= 0; j--) {
            if (result[i]) {
                result[i].push(matrix[j][i]);
            } else {
                result[i] = [matrix[j][i]];
            }
        }
    }
    return result;
}

rotateMatrix(arr);
```
Generate Pascal Triangle:
```javascript
function generatePascalTri(n) {
    const result = [[1], [1, 1]]
    if (result.length >= n) {
        return result.slice(0, n);
    }
    let currentIndex = 2;
    while (currentIndex < n) {
        const current = [1];
        for (let i = 0; i < result[currentIndex - 1].length - 1; i++) {
            current.push(result[currentIndex - 1][i] + result[currentIndex - 1][i + 1]);
        }
        current.push(1);
        currentIndex++;
        result.push(current);
    }
    return result;
}

generatePascalTri(5); // [ [ 1 ], [ 1, 1 ], [ 1, 2, 1 ], [ 1, 3, 3, 1 ], [ 1, 4, 6, 4, 1 ] ]
```
