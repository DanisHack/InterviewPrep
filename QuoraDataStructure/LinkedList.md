Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.
```javascript
const list = { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: { val: 4, next: { val: 4, next: { val: 5, next: null } } } } } } };

function removeTarget(head, target) {
    if (!head) {
        return null;
    }
    if (head.val === target) {
        return removeTarget(head.next, target);
    }
    (function recurse(node) {
        if (!node) {
            return;
        }
        while (node.next && node.next.val === target) {
            node.next = node.next.next;
        }
        recurse(node.next);
    })(head);
    return head;
}

function removeDup(head) {
    if (!head) {
        return null;
    }
    let curr = head;
    const res = { next: head };
    while (curr && curr.next) {
        if (curr.val === curr.next.val) {
            res.next = removeTarget(res.next, curr.val);
            curr = res.next;
        } else {
            curr = curr.next;
        }
    }
    return res.next;
}

console.log(JSON.stringify(removeDup(list), null, 2)); // 1 -> 2 -> 3 -> 3 -> 4 -> 4 -> 5, 1 -> 2 -> 5
```
