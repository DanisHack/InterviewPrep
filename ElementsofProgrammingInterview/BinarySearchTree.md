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
