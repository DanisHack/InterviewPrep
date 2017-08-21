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
Test for overlapping lists: List may have cycles
```javascript
class List {
    constructor(letter) {
        this.val = letter;
        this.next = null;
    }
}

const A = new List("A");
const B = A.next = new List('B');
const C = B.next = new List('C');
const D = C.next = new List('D');
const E = D.next = new List('E');
E.next = A;
const Z = new List("Z");
Z.next = B;

function isCycle(head){
    let slow = fast = head;
    while(fast && fast.next){
        slow = slow.next;
        fast = fast.next.next;
        if(slow === fast){
            break;
        }
    }
    if(!fast || !fast.next){
        return null;
    }
    slow = head;
    while(slow !== fast){
        slow = slow.next;
        fast = fast.next;
    }
    return slow;
}

function getIntersectionNode(headA, headB) {
    let a = headA, b = headB;
    while (true) {
        if (!a) {
            while (b) {
                b = b.next;
                headB = headB.next;
            }
            break;
        } else if (!b) {
            while (a) {
                a = a.next;
                headA = headA.next;
            }
            break;
        }
        a = a.next;
        b = b.next;
    }
    while (headA !== headB) {
        headA = headA.next;
        headB = headB.next;
    }
    return headA;
}

function distance(a, b) {
    let dis = 0;
    while (a !== b) {
        a = a.next;
        dis++;
    }
    return dis;
}

function overlappingLists(l1, l2) {
    let root1 = isCycle(l1), root2 = isCycle(l2);
    if (!root1 && !root2) {
        return getIntersectionNode(l1, l2);
    } else if ((root1 && !root2) || (!root1 && root2)) {
        return null;   
    }
    let temp = root2;
    while (true) {
        temp = temp.next;
        if (temp === root1 || temp === root2) {
            break;
        }
    }
    if (temp !== root1) {
        return null
    }
    let l1Length = distance(l1, root1), l2Length = distance(l2, root2);
    for (let i = 0; i < Math.abs(l1Length - l2Length); i++) {
        l2 = l2.next;
    }
    while (l1 !== l2 && l1 !== root1 && l2 !== root2) {
        l1 = l1.next;
        l2 = l2.next;
    }
    return l1 === l2 ? l1 : root1;
}

overlappingLists(Z, A);
```
Write a program that stores all even nodes before the odd nodes
```javascript
const list = { val: 0, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 4, next: null } } } } };

function evenOddMerge(l) {
    const even = {}, odd = {}, arr = [even, odd];
    let turn = 0;
    while (l) {
        arr[turn].next = l;
        arr[turn] = arr[turn].next;
        l = l.next;
        turn ^= 1;
    }
    arr[1].next = null;
    arr[0].next = odd.next;
    return even.next;
}

evenOddMerge(list);
```
Write a program that tests if the linked list is a palindrome:
```javascript
const list = { val: "S", next: { val: "P", next: { val: "F", next: { val: "P", next: { val: "S", next: null } } } } };

function isPalindrome(l) {
    let slow = l, fast = l;
    const arr = [];
    while (fast && fast.next) {
        arr.push(slow.val);
        slow = slow.next;
        fast = fast.next.next;
    }
    if (fast) {
        slow = slow.next;
    }
    while (slow) {
        if (slow.val !== arr.pop()) {
            return false;
        }
        slow = slow.next;
    }
    return true;
}

isPalindrome(list);
```
Write a program that implements list pivoting:
```javascript
const list = { val: 3, next: { val: 2, next: { val: 2, next: { val: 11, next: { val: 7, next: { val: 5, next: { val: 11, next: null } } } } } } };

function listPivoting(l, k) {
    const less = {}, equal = {}, greater = {};
    let lessIter = less, equalIter = equal, greaterIter = greater;
    while (l) {
        if (l.val < k) {
            lessIter.next = l;
            lessIter = lessIter.next;
        } else if (l.val === k) {
            equalIter.next = l;
            equalIter = equalIter.next;
        } else {
            greaterIter.next = l;
            greaterIter = greaterIter.next;
        }
        l = l.next;
    }
    greaterIter.next = null;
    equalIter.next = greater.next;
    lessIter.next = equal.next;
    return less.next;
}

listPivoting(list, 5);
```
