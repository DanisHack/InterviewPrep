Merge two sorted lists:
```javascript
const list1 = { val: 2, next: { val: 5, next: { val: 7, next: null } } };
const list2 = { val: 3, next: { val: 11, next: null } };

function mergeList(l1, l2) {
    let iter = {};
    const res = iter;
    while (l1 && l2) {
        if (l1.val < l2.val) {
            iter.next = l1;
            l1 = l1.next;
        } else {
            iter.next = l2;
            l2 = l2.next;
        }
        iter = iter.next;
    }
    iter.next = l1 || l2;
    return res.next;
}

console.log(JSON.stringify(mergeList(list2, list1), null, 2));
```
Reverse sublist of a linked list:
```javascript
const list = { val: 11, next: { val: 3, next: { val: 5, next: { val: 7, next: { val: 2, next: null } } } } };

function reverseSublist(head, start, end) {
    if (start >= end) {
        return head;
    }
    let iter = { next: head };
    const res = iter;
    for(let i = 1; i < start; i++) {
        iter = iter.next;
    }
    let prev = iter.next, curr = prev.next;
    for(i = 0; i < end - start; i++) {
        const temp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = temp;
    }
    iter.next.next = curr;
    iter.next = prev;
    return res.next;
}

console.log(JSON.stringify(reverseSublist(list, 2, 4), null, 2));
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
    const root1 = isCycle(l1), root2 = isCycle(l2);
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
    const odd = {};
    const even = {};
    const arr = [even, odd];
    while (l) {
        const index = l.val & 1;
        track[index].next = l;
        track[index] = track[index].next;
        l = l.next;
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
    const less = {};
    const equal = {};
    const greater = {};
    let lessIter = less;
    let equalIter = equal;
    let greaterIter = greater;
    while (l) {
        if (l.val < k) {
            lessIter.next = l;
            lessIter = lessIter.next;
        } else if (l.val === k) {
            equalIter.next = l
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
Add two linked list into one:
```javascript
const list1 = { val: 2, next: { val: 4, next: { val: 3, next: null } } };
const list2 = { val: 5, next: { val: 6, next: { val: 4, next: null } } };

function addTwoNumbers(l1, l2) {
    let iter = {}, carry = 0;
    const result = iter;
    while (l1 || l2 || carry) {
        const val = carry + (l1 ? l1.val : 0) + (l2 ? l2.val : 0);
        l1 = l1 ? l1.next : null;
        l2 = l2 ? l2.next : null;
        iter.next = { val: val % 10 };
        carry = Math.floor(val / 10);
        iter = iter.next;
    }
    return result.next;
}

console.log(JSON.stringify(addTwoNumbers(list1, list2), null, 2));
```
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list
Given this linked list: 1->2->3->4->5
For k = 2, you should return: 2->1->4->3->5
For k = 3, you should return: 3->2->1->4->5
```javascript
const list = { val: 1, next: { val: 2, next: { val: 3, next: { val: 4, next: { val: 5, next: null } } } } };

function reverseK(list, k) {
    let current = list, next = null, prev = null, count = 0;
    while (current && count < k) {
        current = current.next;
        count++;
    }
    if (count < k) {
        return list;
    }
    current = list, count = 0;
    while (current && count < k) {
        next = current.next;
        current.next = prev;
        prev = current;
        current = next;
        count++;
    }
    if (next) {
        list.next = reverseK(next, k);
    }
    return prev;
}

console.log(JSON.stringify(reverseK(list, 2), null, 2));
```
Given a linked list, rotate the list to the right by k places, where k is non-negative.
Input: 1->2->3->4->5->NULL, k = 2
Output: 4->5->1->2->3->NULL
```javascript
const list = {
	val: 1,
	next: {
		val: 2,
		next: { val: 3, next: { val: 4, next: { val: 5, next: null } } },
	}
};

function rotateRight(head, k) {
    if (!head || !k) {
        return head;
    }
    let slow = head, fast = head, num = k;
    while (num > 0) {
        fast = fast.next || head;
        num--;
    }
    if (!fast || fast === slow) { // if fast is slow then the rotation is back to where it started before
        return head;
    }
    while (fast.next) {
        fast = fast.next;
        slow = slow.next;
    }
    const newHead = slow.next;
    slow.next = null;
    fast.next = head;
    return newHead;
}

console.log(JSON.stringify(rotateRight(list, 2), null, 2)); // time complexity: O(n + k)
```
