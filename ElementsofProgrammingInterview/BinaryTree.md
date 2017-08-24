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
        if (current) {
            currentBinary += current.val;
            if (!current.left && !current.right) {
                sum += parseInt(currentBinary, 10);
                return;
            }
            generateSum(current.left, currentBinary);
            generateSum(current.right, currentBinary);
        }
    })(tree, "");
    return sum;
}

sumRootToLeaf(tree);
```
