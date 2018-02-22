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
    (function recurse(node, binary) {
        if (!node) {
            return;
        }
        const curr = binary + node.val;
        if (!node.left && !node.right) {
            sum += parseInt(curr, 10);
            return;
        }
        recurse(node.left, curr);
        recurse(node.right, curr);
    })(tree, "");
    return sum;
}

sumRootToLeaf(tree);
```
Check if num is in path root to leave:
```javascript
const tree = { val: 314, left: { val: 6, left: { val: 271, left: { val: 28, left: null, right: null }, right: { val: 0, left: null, right: null } }, right: { val: 561, left: null, right: { val: 3, left: { val: 17, left: null, right: null }, right: null } } }, right: { val: 6, left: { val: 2, left: null, right: { val: 1, left: { val: 401, left: null, right: { val: 641, left: null, right: null } }, right: { val: 257, left: null, right: null } } }, right: { val: 271, left: null, right: { val: 28, left: null, right: null } } } };

function hasPathSum(node, n, sum = 0) {
    if (!node) {
        return sum === n;
    }
    const newSum = sum + node.val;
    return hasPathSum(node.left, n, newSum) || hasPathSum(node.right, n, newSum);
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
Post order search of binary tree without recursion:
```javascript
function postOrderSearch(tree) {
    const res = [], stack = [];
    let curr = tree;
    while (curr || stack.length) {
        if (curr) {
            if (curr.right) {
                stack.push(curr.right);
            }
            stack.push(curr);
            curr = curr.left;
        } else {
            curr = stack.pop();
            if (curr.right === stack[stack.length - 1]) {
                const right = stack.pop();
                stack.push(curr);
                curr = right;
            } else {
                res.push(curr.val);
                curr = null;
            }
        }
    }
    return res;
}

postOrderSearch(tree);
```
Reconstruct the binary tree with preorder and inorder traversal:
```javascript
const inOrder = ["F", "B", "A", "E", "H", "C", "D", "I", "G"];
const preOrder = ["H", "B", "F", "E", "A", "C", "D", "G", "I"];

function binaryConstruct(preOrder, inOrder) {
    const nodes = {};
    inOrder.forEach((e, i) => {
        nodes[e] = i;
    });
    return (function recurse(preStart, preEnd, inStart, inEnd) {
        if (preStart >= preEnd || inStart >= inEnd) {
            return null;
        }
        const inOrderIndx = nodes[preOrder[preStart]];
        const subTreeSize = inOrderIndx - inStart;
        return {
            val: preOrder[preStart],
            left: recurse(preStart + 1, preStart + 1 + subTreeSize, inStart, inOrderIndx),
            right: recurse(preStart + 1 + subTreeSize, preEnd, inOrderIndx + 1, inEnd)
        }
    })(0, preOrder.length, 0, inOrder.length);
}

console.log(JSON.stringify(binaryConstruct(preOrder, inOrder), null, 2));
```
Reconstruct the binary tree with postorder and inorder traversal:
```javascript
const inOrder = ["F", "B", "A", "E", "H", "C", "D", "I", "G"];
const postOrder = ["F", "A", "E", "B", "I", "G", "D", "C", "H"];

function binaryConstruct(postOrder, inOrder) {
    const nodes = {};
    inOrder.forEach((e, i) => {
        nodes[e] = i;
    });
    return (function recurse(postStart, postEnd, inStart, inEnd) {
        if (postStart >= postEnd || inStart >= inEnd) {
            return null;
        }
        const inOrderIndx = nodes[postOrder[postEnd]];
        const subTreeSize = inEnd - inOrderIndx;
        return {
            val: postOrder[postEnd],
            left: recurse(postStart, postEnd - subTreeSize, inStart, inOrderIndx),
            right: recurse(postEnd - 1 - subTreeSize, postEnd - 1, inOrderIndx + 1, inEnd)
        }
    })(-1, postOrder.length - 1, 0, inOrder.length);
}

console.log(JSON.stringify(binaryConstruct(postOrder, inOrder), null, 2));
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

console.log(JSON.stringify(generateLinkedList(tree), null, 2));
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
Print the vertical columns of the binary tree
```javascript
const tree = { val: 1, left: { val: 2, left: { val: 4, left: null, right: null }, right: { val: 5, left: null, right: null } }, right: { val: 3, left: null, right: { val: 6, left: null, right: null } } };

function findMinMax(node, map, minMax, hd) {
    if (!node) {
        return
    }
    if (hd < minMax[0]) {
        minMax[0] = hd;
    } else if (hd > minMax[1]) {
        minMax[1] = hd;
    }
    if (map[hd]) {
        map[hd].push(node.val);
    } else {
        map[hd] = [node.val];
    }
    findMinMax(node.left, map, minMax, hd - 1);
    findMinMax(node.right, map, minMax, hd + 1);
}

function verticalCol(tree) {
    const map = {};
    const minMax = [0, 0];
    let res = [];
    findMinMax(tree, map, minMax, 0);
    for (let i = minMax[0]; i <= minMax[1]; i++) {
        res = res.concat(map[i]);
    }
    return res;
}

verticalCol(tree);
```
