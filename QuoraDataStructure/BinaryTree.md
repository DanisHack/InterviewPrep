Find the distance between given pairs of nodes in a binary tree
```javascript
const tree = { val: 1, left: { val: 2, left: null, right: { val: 4, left: null, right: null } }, right: { val: 3, left: { val: 5, left: { val: 7, left: null, right: null }, right: { val: 8, left: null, right: null } }, right: { val: 6, left: null, right: null } } };

function distance(node, target, num = 0) {
    if (!node) {
        return 0;
    }
    if (node.val === target) {
        return num;
    }
    return distance(node.left, target, num + 1) || distance(node.right, target, num + 1);
}

function lowestAncestor(node, p, q) {
    if (!node || node.val === p || node.val === q) {
        return node;
    }
    const left = lowestAncestor(node.left, p, q);
    const right = lowestAncestor(node.right, p, q);
    return left && right ? node : (left || right);
}

function findDistance(tree, p, q) {
    const LCA = lowestAncestor(tree, p, q);
    return distance(LCA, p) + distance(LCA, q);
}

findDistance(tree, 4, 7); // 5
```
Two elements of a binary search tree (BST) are swapped by mistake.
Recover the tree without changing its structure.
```javascript
const list = { val: 1, left: { val: 3, left: null, right: { val: 2, left: null, right: null } }, right: null };

function recoverTree(head) {
    if (!head) {
        return null;
    }
    let prev, first, second;
    (function inOrder(node) {
        if (!node) {
            return;
        }
        inOrder(node.left);
        if (prev && prev.val > node.val) {
            if (!first) {
                first = prev;
            }
            second = node;
        }
        prev = node;
        inOrder(node.right);
    })(head);
    if (first && second) {
        const val = first.val;
        first.val = second.val;
        second.val = val;
    }
    return head;
}

console.log(JSON.stringify(recoverTree(list), null, 2));
```
Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?
```javascript
function numTrees(n) {
    const res = [1, 1];
    for (let i = 2; i <= n; i++) {
        res[i] = 0;
        for (let j = 0; j < i; j++) {
            res[i] += res[j] * res[i - j - 1];
        }
    }
    return res[n];
}

numTrees(3); // 5
```
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.
```javascript
function generateTrees(n) {
    if (n === 0) {
        return [];
    }
    return (function generate(start, end) {
        if (start > end) {
            return [null];
        }
        const res = [];
        for (let i = start; i <= end; i++) {
            const leftTrees = generate(start, i - 1);
            const rightTrees = generate(i + 1, end);
            leftTrees.forEach(left => {
                rightTrees.forEach(right => {
                    res.push({ val: i, left, right });
                });
            });
        }
        return res;
    })(1, n);
}

console.log(JSON.stringify(generateTrees(3), null, 2));
```
