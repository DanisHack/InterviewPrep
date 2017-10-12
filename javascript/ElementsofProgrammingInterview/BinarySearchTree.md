Find the first node that is greater then the current node in an in-order traversal:
```javascript
const tree = { val: 19, left: { val: 7, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 5, left: null, right: null } }, right: { val: 11, left: null, right: { val: 17, left: { val: 13, left: null, right: null }, right: null } } }, right: { val: 43, left: { val: 23, left: null, right: { val: 37, left: { val: 29, left: null, right: { val: 31, left: null, right: null } }, right: { val: 41, left: null, right: null } } }, right: { val: 47, left: null, right: { val: 53, left: null, right: null } } } };

function firstGreater(tree, k) {
    let current = tree, greater = null;
    while (current) {
        if (current.val > k) {
            greater = current.val;
            current = current.left;
        } else {
            current = current.right;
        }
    }
    return greater;
}

firstGreater(tree, 23);
```
First appearance of a node with the value k:
```javascript
const tree = { val: 108, left: { val: 108, left: { val: -10, left: { val: -14, left: null, right: null }, right: { val: 2, left: null, right: null } }, right: { val: 108, left: null, right: null } }, right: { val: 285, left: { val: 243, left: null, right: null }, right: { val: 285, left: null, right: { val: 401, left: null, right: null } } } };

function firstAppearance(tree, k) {
    return (function helper(current) {
        if (!current) {
           return null;
        }
        const left = helper(current.left);
        if (left) {
            return left;
        }
        if (current.val === k) {
            return current;
        }
        const right = helper(current.right);
        if (right) {
            return right;
        }
        return null;
    })(tree);
}

firstAppearance(tree, 143);
```
Find the kth largest value in BST:
```javascript
const tree = { val: 19, left: { val: 7, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 5, left: null, right: null } }, right: { val: 11, left: null, right: { val: 17, left: { val: 13, left: null, right: null }, right: null } } }, right: { val: 43, left: { val: 23, left: null, right: { val: 37, left: { val: 29, left: null, right: { val: 31, left: null, right: null } }, right: { val: 41, left: null, right: null } } }, right: { val: 47, left: null, right: { val: 53, left: null, right: null } } } };

function kLargest(tree, k) {
    let result = null, count = 1;
    (function helper(current) {
        if (!current) {
            return;
        }
        helper(current.right);
        if (count === k) {
            result = current;
            count++;
            return;
        }
        count++;
        helper(current.left);
    })(tree);
    return result;
}

kLargest(tree, 9);
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

rebuild(preOrder);
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

function insertNode(bst, key) {
    if (!bst) {
        return true;
    }
    let parent = current = bst;
    while (current) {
        parent = current;
        if (current.val === key) {
            return false;
        } else if (current.val > key) {
            current = current.left;
        } else {
            current = current.right;
        }
    }
    if (parent.val > key) {
        parent.left = { val: key, left: null, right: null };
    } else {
        parent.right = { val: key, left: null, right: null };
    }
    return true;
}

function deleteNode(bst, val) {
    let parent = current = bst;
    while (current && current.val !== val) {
        parent = current;
        current = val < current.val ? current.left : current.right;
    }
    if (!current) {
        return false;
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
        if (bst === key) {
            bst.val = key.left.val, bst.left = key.left.val, bst.right = key.left.right;
        } else if (parent.left === key) {
            parent.left = key.left;
        } else {
            parent.right = key.right;
        }
    }
    return true;
}

insertNode(tree, 15);
deleteNode(tree, 15);
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
    let pointer0 = node0, pointer1 = node1;
    while (pointer0 !== node1 && pointer0 !== middle && pointer1 !== node0 && pointer1 !== middle && (pointer0 || pointer1)) {
        if (pointer0) {
            pointer0 = pointer0.val > middle.val ? pointer0.left : pointer0.right;
        }
        if (pointer1) {
            pointer1 = pointer1.val > middle.val ? pointer1.left : pointer1.right;
        }
    }
    if ((pointer0 !== middle && pointer1 !== middle) || pointer0 === node1 || pointer1 === node0) {
        return false;
    }
    return searchTarget(middle, (pointer0 === middle ? node1 : node0));
}

isBSTordered(seven, ten, fourteen);
```
