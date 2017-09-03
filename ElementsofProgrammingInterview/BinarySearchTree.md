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
