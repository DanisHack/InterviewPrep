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
