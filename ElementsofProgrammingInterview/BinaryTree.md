Determine if a Binary Tree is symmetric:
```javascript
const tree = { val: 314, left: { val: 6, left: null, right: { val: 2, left: null, right: { val: 3, left: null, right: null } } }, right: { val: 6, left: { val: 2, left: { val: 3, left: null, right: null }, right: null }, right: null } };

function generateStr(current, side) {
    if (!current) {
        return "";
    }
    const str = generateStr(current.left, "l") + generateStr(current.right, "r") + `${side}${current.val}`;
    return str;
}

function isSymmetric(tree) {
    const left = generateStr(tree.left, "l");
    const right = generateStr(tree.right, "r");
    if (left.length !== right.length) {
        return false;
    }
    const obj = { l: "r", r: "l" };
    for (let i = 0; i < left.length; i += 2) {
        if (obj[left[i]] !== right[i] || left[i + 1] !== right[i + 1]) {
            return false;
        }
    }
    return true;
}

isSymmetric(tree);
```
