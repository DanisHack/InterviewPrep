Permutation of an Array:
```javascript
function permutation(arr) {
    const result = [];
    (function recurse(i) {
        if (i === arr.length - 1) {
            result.push([...arr]);
            return;
        }
        for (let j = i; j < arr.length; j++) {
            let temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            recurse(i + 1);
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    })(0);
    return result;
}

permutation([2, 3, 5, 7]);
```
Generate all subsets of size K:
```javascript
function generateSubset(k, n) {
    const result = [];
    (function recurse(i, combo = []) {
        if (combo.length === k) {
            return result.push([...combo]);
        }
        for (let j = i; j <= n; j++) {
            combo.push(j);
            recurse(j + 1, combo);
            combo.pop();
        }
    })(1);
    return result;
}

generateSubset(3, 5);
```
Generate Palindromic Decompositions:
```javascript
function allPalindrome(str) {
    const result = [];
    (function helper(index, current) {
        if (index === str.length) {
            return result.push(current.slice(1));
        }
        for (let i = index + 1; i < str.length + 1; i++) {
            const word = str.slice(index, i);
            if (word === word.split("").reverse().join("")) {
                helper(i, `${current},${word}`);
            }
        }
    })(0, "");
    return result;
}

allPalindrome("0204451881");
```
Given a number of nodes, generate all Binary trees with the number of nodes:
```javascript
function generateBST(num) {
    if (!num) {
         return [null];
    }
    let result = [];
    for (let leftNode = 0; leftNode < num; leftNode++) {
        const rightNode = num - 1 - leftNode;
        const leftTree = generateBST(leftNode);
        const rightTree = generateBST(rightNode);
        const temp = [];
        leftTree.map(left => {
            rightTree.forEach(right => {
                temp.push({ val: 0, left, right });
            });
        });
        result = result.concat(temp);
    }
    return result;
}

generateBST(3);
```
Generate N-bit Gray Code:
```javascript
function generateGrayCode(n) {
    if (n <= 0) {
        return [];
    }
    const result = ["0", "1"];
    for (let i = 2; i < 1 << n; i <<= 1) {
        for (let j = i - 1; j >= 0; j--) {
            result.push(result[j]);
        }
        for (let j = 0; j < i; j++) {
            result[j] = "0" + result[j];
        }
        for (let j = i; j < 2 * i; j++) {
            result[j] = "1" + result[j];
        }
    }
    return result;
}

generateGrayCode(3);
```
Calculate the diameter of a tree(the longest path in a tree):
```javascript
const tree = { val: 314, left: { val: 6, left: { val: 271, left: { val: 28, left: null, right: null }, right: { val: 0, left: null, right: null } }, right: { val: 561, left: null, right: { val: 3, left: { val: 17, left: null, right: null }, right: null } } }, right: { val: 6, left: { val: 2, left: null, right: { val: 1, left: { val: 401, left: null, right: { val: 641, left: null, right: null } }, right: { val: 257, left: null, right: null } } }, right: { val: 271, left: null, right: { val: 28, left: null, right: null } } } };

function height(node) {
    if (!node) {
        return 0;
    }
    return Math.max(height(node.left), height(node.right)) + 1;
}

function calcDiameter(root) {
    if (!root) {
        return 0;
    }
    const leftHeight = height(root.left);
    const rightHeight = height(root.right);
    return leftHeight + rightHeight + 1;
}

calcDiameter(tree);
```
