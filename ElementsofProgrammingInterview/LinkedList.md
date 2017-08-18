Merge two sorted lists:
```javascript
const list1 = { val: 2, next: { val: 5, next: { val: 7, next: null } } };
const list2 = { val: 3, next: { val: 11, next: null } };

function mergeList(l1, l2) {
    let tail = {};
    const dummyHead = tail;
    while (l1 && l2) {
        if (l1.val < l2.val) {
            tail.next = l1;
            l1 = l1.next;
        } else {
            tail.next = l2;
            l2 = l2.next;
        }
        tail = tail.next;
    }
    tail.next = l1 || l2;
    return dummyHead.next;
}

mergeList(list1, list2);
```
Merge K sorted Lists:
```javascript
const list1 = { val: -2, next: { val: 1, next: { val: 4, next: { val: 5, next: null } } } };
const list2 = { val: -2, next: { val: 5, next: { val: 6, next: null } } };
const list3 = { val: -2, next: { val: 0, next: null } };

function merge(l1, l2) {
    let tail = {};
    const dummyHead = tail;
    while (l1 && l2) {
        if (l1.val < l2.val) {
            tail.next = l1;
            l1 = l1.next;
        } else {
            tail.next = l2;
            l2 = l2.next;
        }
        tail = tail.next;
    }
    tail.next = l1 || l2;
    return dummyHead.next;
}

function mergeKLists(lists) {
    if (!lists.length) {
        return null;
    }
    let result = lists[0];
    for (let i = 1; i < lists.length; i++) {
        result = merge(result, lists[i]);
    }
    return result;
}

mergeKList([list1, list2, list3]);
```
Revers sublist of a linked list:
```javascript
const list = { val: 11, next: { val: 3, next: { val: 5, next: { val: 7, next: { val: 2, next: null } } } } };

function reverseSublist(list, start, end) {
    let subHead = { next: list };
    const result = subHead;
    for (let i = 1; i < start; i++) {
        subHead = subHead.next;
    }
    let subCurrent = subHead.next;
    for (let i = 0; i < finish - start; i++) {
        const temp1 = subCurrent.next, temp2 = subHead.next;
        subCurrent.next = temp1.next, subHead.next = temp1, temp1.next = temp2;
    }
    return list;
}

reverseSublist(list, 2, 4);
```
