Determine if a Binary Tree is symmetric:
```javascript
const tree = { val: 314, left: { val: 6, left: null, right: { val: 2, left: null, right: { val: 3, left: null, right: null } } }, right: { val: 6, left: { val: 2, left: { val: 3, left: null, right: null }, right: null }, right: null } };

function checkSymmetric(t1, t2) {
    if (!t1 && !t2) {
        return true;
    } else if (t1 && t2) {
        return t1.val === t2.val && checkSymmetric(t1.left, t2.right) && checkSymmetric(t1.right, t2.left);
    }
    return false;
}

function isSymmetric(tree) {
    return !tree || checkSymmetric(tree.left, tree.right);
}

isSymmetric(tree);
```
Sum from Root to Leaf:
```javascript
const tree = { val: 1, left: { val: 0, left: { val: 0, left: { val: 0, left: null, right: null }, right: { val: 1, left: null, right: null } }, right: { val: 1, left: null, right: { val: 1, left: { val: 0, left: null, right: null }, right: null } } }, right: { val: 1, left: { val: 0, left: null, right: { val: 0, left: { val: 1, left: null, right: { val: 1, left: null, right: null } }, right: { val: 0, left: null, right: null } } }, right: { val: 0, left: null, right: { val: 0, left: null, right: null } } } };

function sumRootToLeaf(tree) {
    let sum = 0;
    (function generateSum(current, currentBinary) {
        if (!current) {
            return
        }
        currentBinary += current.val;
        if (!current.left && !current.right) {
            sum += parseInt(currentBinary, 10);
            return;
        }
        generateSum(current.left, currentBinary);
        generateSum(current.right, currentBinary);
    })(tree, "");
    return sum;
}

sumRootToLeaf(tree);
```
Check if num is in path root to leave:
```javascript
const tree = { val: 314, left: { val: 6, left: { val: 271, left: { val: 28, left: null, right: null }, right: { val: 0, left: null, right: null } }, right: { val: 561, left: null, right: { val: 3, left: { val: 17, left: null, right: null }, right: null } } }, right: { val: 6, left: { val: 2, left: null, right: { val: 1, left: { val: 401, left: null, right: { val: 641, left: null, right: null } }, right: { val: 257, left: null, right: null } } }, right: { val: 271, left: null, right: { val: 28, left: null, right: null } } } };

function hasPathSum(tree, n) {
    return (function findSum(current, sum) {
        if (!current) {
            return false;
        }
        sum += current.val;
        if (!current.left && !current.right) {
            return sum === n;
        }
        if (recurse(current.left, sum)) {
            return true;
        }
        if (recurse(current.right, sum)) {
            return true;
        }
        return false;
    })(tree, 0);
}

hasPathSum(tree, 901);
```
In order search of binary tree without recursion:
```javascript
const tree = { val: 314, left: { val: 6, left: { val: 271, left: { val: 28, left: null, right: null }, right: { val: 0, left: null, right: null } }, right: { val: 561, left: null, right: { val: 3, left: { val: 17, left: null, right: null }, right: null } } }, right: { val: 6, left: { val: 2, left: null, right: { val: 1, left: { val: 401, left: null, right: { val: 641, left: null, right: null } }, right: { val: 257, left: null, right: null } } }, right: { val: 271, left: null, right: { val: 28, left: null, right: null } } } };

function inOrderSearch(tree) {
    const result = [], stack = [];
    let current = tree;
    while (stack.length || current) {
        if (current) {
            stack.push(current);
            current = current.left;
        } else {
            current = stack.pop();
            result.push(current.val);
            current = current.right;
        }
    }
    return result;
}

inOrderSearch(tree);
```
Pre order search of binary tree without recursion:
```javascript
const tree = { val: 314, left: { val: 6, left: { val: 271, left: { val: 28, left: null, right: null }, right: { val: 0, left: null, right: null } }, right: { val: 561, left: null, right: { val: 3, left: { val: 17, left: null, right: null }, right: null } } }, right: { val: 6, left: { val: 2, left: null, right: { val: 1, left: { val: 401, left: null, right: { val: 641, left: null, right: null } }, right: { val: 257, left: null, right: null } } }, right: { val: 271, left: null, right: { val: 28, left: null, right: null } } } };

function preOrderSearch(tree) {
    const stack = [], res = [];
    let current = tree;
    while (stack.length || current) {
        if (current) {
            stack.push(current.right);
            res.push(current.val);
            current = current.left;
        } else {
            current = stack.pop();
        }
    }
    return res;
}

preOrderSearch(tree);
```
Reconstruct the binary tree with preorder and inorder traversal:
```javascript
const inOrder = ["F", "B", "A", "E", "H", "C", "D", "I", "G"];
const preOrder = ["H", "B", "F", "E", "A", "C", "D", "G", "I"];

function binaryConstruct(preOrder, inOrder) {
    const nodes = {};
    inOrder.forEach((val, i) => {
       nodes[val] = i;
    });
    return (function helper(preStart, preEnd, inStart, inEnd) {
        if (preStart >= preEnd || inStart >= inEnd) {
            return null;
        }
        const inOrderIndx = nodes[preOrder[preStart]], subTreeSize = inOrderIndx - inStart;
        return {
            val: preOrder[preStart],
            left: helper(preStart + 1, preStart + 1 + subTreeSize, inStart, inOrderIndx),
            right: helper(preStart + 1 + subTreeSize, preEnd, inOrderIndx + 1, inEnd)
        }
    })(0, preOrder.length, 0, inOrder.length);
}

binaryConstruct(preOrder, inOrder);
```
Reconstruct a binary tree from a pre-order traversal with marker:
```javascript
const preOrder = ["H", "B", "F", null, null, "E", "A", null, null, null, "C", null, "D", null, "G", "I", null, null, null];

function generateTree(seq) {
    seq.reverse();
    return (function helper() {
        const val = seq.pop();
        if (!val) {
            return null;
        }
        return { val, left: helper(), right: helper() };
    })();
}

generateTree(preOrder);
```
Generate a linked list from the leaves of a binary tree:
```javascript
const tree = { val: "A", left: { val: "B", left: { val: "C", left: { val: "D", left: null, right: null }, right: { val: "E", left: null, right: null } }, right: { val: "F", left: null, right: { val: "G", left: { val: "H", left: null, right: null }, right: null } } }, right: { val: "I", left: { val: "J", left: null, right: { val: "K", left: { val: "L", left: null, right: { val: "M", left: null, right: null } }, right: { val: "N", left: null, right: null } } }, right: { val: "O", left: null, right: { val: "P", left: null, right: null } } } };

function generateLinkedList(tree) {
    let result = head = { next: null };
    (function recurse(current) {
        if (!current.left && !current.right) {
            head.next = { val: current.val, next: null };
            head = head.next;
            return;
        }
        if (current.left) {
            recurse(current.left);
        }
        if (current.right) {
            recurse(current.right);
        }
    })(tree);
    return result.next;
}

generateLinkedList(tree);
```
Find all the exterior leaves of binary tree:
```javascript
const tree = { val: "A", left: { val: "B", left: { val: "C", left: { val: "D", left: null, right: null }, right: { val: "E", left: null, right: null } }, right: { val: "F", left: null, right: { val: "G", left: { val: "H", left: null, right: null }, right: null } } }, right: { val: "I", left: { val: "J", left: null, right: { val: "K", left: { val: "L", left: null, right: { val: "M", left: null, right: null } }, right: { val: "N", left: null, right: null } } }, right: { val: "O", left: null, right: { val: "P", left: null, right: null } } } };

function isLeave(current) {
    return !current.left && !current.right;
}

function leftBoundary(subTree, isBoundary) {
    if (!subTree) {
        return [];
    }
    const current = isBoundary || isLeave(subTree) ? [subTree.val] : [];
    const left = leftBoundary(subTree.left, isBoundary);
    const right = leftBoundary(subTree.right, (isBoundary && !subTree.left));
    return current.concat(left, right);
}

function rightBoundary(subTree, isBoundary) {
    if (!subTree) {
        return [];
    }
    const left = rightBoundary(subTree.left, (isBoundary && !subTree.right));
    const right = rightBoundary(subTree.right, isBoundary);
    const current = isBoundary || isLeave(subTree) ? [subTree.val] : [];
    return left.concat(right, current);
}

function exteriorBinaryTree(tree) {
    const left = leftBoundary(tree.left, true);
    const right = rightBoundary(tree.right, true);
    return [tree.val].concat(left, right);
}

exteriorBinaryTree(tree);
```
