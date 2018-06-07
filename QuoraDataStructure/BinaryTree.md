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
