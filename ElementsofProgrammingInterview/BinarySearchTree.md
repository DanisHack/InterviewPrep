Find the first node that is greater then the current node in an in-order traversal:
```javascript
const tree = { val: 19, left: { val: 7, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 5, left: null, right: null } }, right: { val: 11, left: null, right: { val: 17, left: { val: 13, left: null, right: null }, right: null } } }, right: { val: 43, left: { val: 23, left: null, right: { val: 37, left: { val: 29, left: null, right: { val: 31, left: null, right: null } }, right: { val: 41, left: null, right: null } } }, right: { val: 47, left: null, right: { val: 53, left: null, right: null } } } };

function firstGreater(tree, k) {
    let current = tree, greater = null;
    while (current) {
        if (current.val > k) {
            greater = current;
            current = current.left;
        } else {
            current = current.right;
        }
    }
    return greater;
}

console.log(JSON.stringify(firstGreater(tree, 23), null, 2));
```
First appearance of a node with the value k:
```javascript
const tree = { val: 108, left: { val: 108, left: { val: -10, left: { val: -14, left: null, right: null }, right: { val: 2, left: null, right: null } }, right: { val: 108, left: null, right: null } }, right: { val: 285, left: { val: 243, left: null, right: null }, right: { val: 285, left: null, right: { val: 401, left: null, right: null } } } };

function firstAppearance(node, k) {
    if (!node || node.val === k) {
        return node;
    }
    return firstAppearance(node.left, k) || firstAppearance(node.right, k);
}

console.log(JSON.stringify(firstAppearance(tree, 285), null, 2));
```
Find the kth largest value in BST:
```javascript
const tree = { val: 19, left: { val: 7, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 5, left: null, right: null } }, right: { val: 11, left: null, right: { val: 17, left: { val: 13, left: null, right: null }, right: null } } }, right: { val: 43, left: { val: 23, left: null, right: { val: 37, left: { val: 29, left: null, right: { val: 31, left: null, right: null } }, right: { val: 41, left: null, right: null } } }, right: { val: 47, left: null, right: { val: 53, left: null, right: null } } } };

function kLargest(node, k) {
    let i = 1;
    return (function recurse(current) {
        if (!current) {
            return null;
        }
        const right = recurse(current.right);
        if (right) {
            return right;
        }
        if (i === k) {
            return current;
        }
        i++;
        return recurse(current.left);
    })(node);
}

console.log(JSON.stringify(kLargest(tree, 2), null, 2));
```
Reconstruct a Binary Search tree from preorder traversal:
```javascript
const preOrder = [19, 7, 3, 2, 5, 11, 17, 13, 43, 23, 37, 29, 31, 41, 47, 53];

function rebuild(arr) {
    let index = 0;
    return (function helper(lower, upper) {
        if (index === arr.length) {
            return null;
        }
        const val = arr[index];
        if (!(lower < val && val < upper)) {
            return null;
        }
        index++;
        const left = helper(lower, val);
        const right = helper(val, upper);
        return { val, left, right };
    })(-Infinity, Infinity);
}

console.log(JSON.stringify(reBuild(preOrder), null, 2));
```
Reconstruct a Binary Search Tree from postorder traversal:
```javascript
const postOrder = [2, 5, 3, 13, 17, 11, 7, 31, 29, 41, 37, 23, 53, 47, 43, 19];

function rebuild(arr) {
    let index = arr.length - 1;
    return (function helper(lower, upper) {
        if (index === -1) {
            return null;
        }
        const val = arr[index];
        if (!(lower < val && val < upper)) {
            return null;
        }
        index--;
        const right = helper(val, upper);
        const left = helper(lower, val);
        return { val, left, right };
    })(-Infinity, Infinity);
}

rebuild(postOrder);
```
Insert and Deletion Binary Search Tree:
```javascript
const tree = { val: 10, left: { val: 7, left: { val: 2, left: null, right: null }, right: { val: 9, left: null, right: null } }, right: { val: 14, left: { val: 12, left: null, right: null }, right: { val: 16, left: null, right: null } } };

function insertNode(node, val) {
    if (!node) {
        return null;
    }
    let parent = node, curr = node;
    while (curr) {
        parent = curr;
        if (curr.val === val) {
            return null;
        }
        curr = curr.val > val ? curr.left : curr.right;
    }
    if (parent.val > val) {
        parent.left = { val, left: null, right: null };
    } else if (parent.val < val) {
        parent.right = { val, left: null, right: null };
    }
    return node;
}

function deleteNode(node, val) {
    let parent = node, current = node;
    while (current && current.val !== val) {
        parent = current;
        current = current.val > val ? current.left : current.right;
    }
    if (!current) {
        return null;
    }
    const key = current;
    if (key.right) {
        let parentRight = key;
        let right = key.right;
        while (right.left) {
            parentRight = right;
            right = right.left;
        }
        key.val = right.val;
        if (parentRight.left === right) {
            parentRight.left = right.right;
        } else {
            parentRight.right = right.right;
        }
    } else {
        if (node === key) {
            const { val, left, right } = key.left;
            node.val = val;
            node.left = left;
            node.right = right;
        } else if (parent.left === key) {
            parent.left = key.left;
        } else {
            parent.right = key.left;
        }
    }
    return node;
}

console.log(JSON.stringify(insertNode(tree, 15), null, 2));
console.log(JSON.stringify(deleteNode(tree, 10), null, 2));
```
Given three node, check if BST is ordered:
```javascript
class Node {
    constructor(val, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

const ten = new Node(10);
const seven = ten.left = new Node(7);
const fourteen = ten.right = new Node(14);
const two = seven.left = new Node(2);
const nine = seven.right = new Node(9);
const twelve = fourteen.left = new Node(12);
const sixteen = fourteen.right = new Node(16);

function searchTarget(source, target) {
    while (source && source !== target) {
        source = source.val > target.val ? source.left : source.right;
    }
    return source === target;
}

function isBSTordered(node0, node1, middle) {
    let p1 = node1, p0 = node0;
    while (p1 !== node0 && p1 !== middle && p0 !== node1 && p0 !== middle && (p0 || p1)) {
        if (p1) {
            p1 = p1.val > middle.val ? p1.left : p1.right;
        }
        if (p0) {
            p0 = p0.val > middle.val ? p0.left : p0.right;
        }
    }
    if ((p1 !== middle && p0 !== middle) || p1 === node0 || p0 === node1) {
        return false;
    }
    return searchTarget(middle, (p0 === middle ? node1 : node0));
}

isBSTordered(two, ten, seven);
```
