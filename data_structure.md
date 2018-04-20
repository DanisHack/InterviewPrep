Remove Duplicates from Linked List:
```javascript
// javascript version
const list = {val: 'F', next: { val: 'O', next: { val: 'L', next: { val: 'L', next: { val: 'O', next: { val: 'W', next: null } } } } } };

function removeDup(head){
	if(!head) {
		return;
	}
	let current = head;
	while(current) {
		let runner = current;
		while(runner) {
			if(runner.next && runner.next.val === current.val) {
				runner.next = runner.next.next;
			}
			else {
				runner = runner.next;
			}
		}
		current = current.next;
	}
	return head;
}

console.log(JSON.stringify(removeDup(list), null, 2));
```
Find Kth to the last element in a singly linked list:
```javascript
// javascript version
function findK(head, k){
	let p1 = p2 = root, num = 0;
    while (p2 && num < k) {
        p2 = p2.next;
        num++;
    }
    while (p2) {
        p1 = p1.next;
        p2 = p2.next;
    }
    return p1;
}

console.log(JSON.stringify(findK(list, 2), null, 2));
```
Removing the kth to the last element from a linked list:
```javascript
// javascript version
var list = {val: 1, next: {val: 2, next: null}};

function removeNthFromEnd(root, k) {
    let p1 = p2 = root, num = 0;
    while (p2 && num < k) {
        p2 = p2.next;
        num++;
    }
    if (!p2) {
        return root.next;
    }
    while (p2.next) {
        p1 = p1.next;
        p2 = p2.next;
    }
    p1.next = p1.next.next;
    return root;
}

console.log(JSON.stringify(removeNthFromEnd(list, 1), null, 2));
```
See if the binary tree is balanced:
```javascript
const tree = { val: 5, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 7, left: { val: 6, left: null, right: null }, right: { val: 8, left: null, right: null } } };

function checkHeight(node) {
	if(!node) {
		return 0;
	}
	let left = checkHeight(node.left);
	if(left === -1) {
		return -1;
	}
	let right = checkHeight(node.right);
	if(right === -1) {
		return -1;
	}
	let diff = right - left;
	if(Math.abs(diff) > 1) {
		return -1;
	}
	return Math.max(left, right) + 1;
}

function balanceNode(root) {
	return checkHeight(root) !== -1;
}

balanceNode(tree);
```
Create a minimal BST with a sorted array:
```javascript
const arr = [1,2,3,4,5,6,7];

function createBST(arr, start = 0, end = arr.length - 1) {
	if(start > end) {
		return null;
	}
	let middle = Math.floor((start + end) / 2);
	return {
		value: arr[middle],
		left: createBST(arr, start, middle - 1),
		right: createBST(arr, middle + 1, end)
	};
}

createBST(arr);
```
Find the lowest common ancestor of Binary Tree:
```javascript
const tree = { val: 5, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 7, left: { val: 6, left: null, right: null }, right: { val: 8, left: null, right: null } } };

function lowestCommonAncestor(node, p, q) {
	if(!node || node.val === p || node.val === q) {
		return node;
	}
	let left = lowestCommonAncestor(node.left, p, q);
	let right = lowestCommonAncestor(node.right, p, q);
	return (left && right ? node : (left || right));
}

lowestCommonAncestor(tree, 3, 4);
```
Confirm if a binary tree is binary search tree:
```javascript
function checkBST(node, min = -Infinity, max = Infinity) {
	if(!node) {
		return true;
	}
	if(node.val <= min || node.val >= max) {
		return false;
	}
	if(!checkBST(node.left, min, node.val) || !checkBST(node.right, node.val, max)) {
		return false;
	}
	return true;
}

checkBST(tree); // use min and max to check if each node is within the range.
```
Find the kth smallest in a BST:
```javascript
const tree = { val: 5, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 7, left: { val: 6, left: null, right: null }, right: { val: 8, left: null, right: null } } };

function findK(tree, k) {
    let i = 1;
    return (function recurse(current) {
        if (current) {
            const left = recurse(current.left);
            if (left) {
                return left;
            }
            if (i === k) {
                return current;
            }
            i++;
            const right = recurse(current.right);
            if (right) {
                return right;
            }
        }
        return null;
    })(tree);
}

findK(tree, 4);
```
Remove from a linkedlist that has the same val:
```javascript
const list = {val: 'F', next: { val: 'O', next: { val: 'L', next: { val: 'L', next: { val: 'O', next: { val: 'W', next: null } } } } } };

function removeElements(root, val) {
    if (!root) {
        return null;
    }
    if (root.val === val) {
        return removeElements(root.next, val);
    }
    (function recurse(current) {
        if (!current) {
            return;
        }
        while (current.next && current.next.val === val) {
            current.next = current.next.next;
        }
        recurse(current.next);
    })(root);
    return root;
}

console.log(JSON.stringify(removeElements(list, "L"), null, 2));
```
Check if subtree is part of tree:
```javascript
const tree2 =  { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } };
const tree1 = { val: 5, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 7, left: { val: 6, left: null, right: null }, right: { val: 8, left: null, right: null } } };

function match(t1, t2){
    if (!t1 && !t2) {
        return true;
    }
    if (!t1 || !t2) {
        return false;
    }
    if (t1.val !== t2.val) {
        return false;
    }
    return match(t1.left, t2.left) && match(t1.right, t2.right);
}

function subTree(t1, t2){
    if (!t1) {
        return false;
    }
    if (t1.val === t2.val && match(t1, t2)) {
        return true;
    }
    return subTree(t1.left, t2) || subTree(t1.right, t2);
}

function containsTree(t1, t2){
    return t2 ? subTree(t1, t2) : true;
}

containsTree(tree1, tree2);
```
Finding the beginning of linked list circle:
```javascript
function List(letter){
    this.val = letter;
    this.next = null;
}
const A = new List("A");
const B = A.next = new List('B');
const C = B.next = new List('C');
const D = C.next = new List('D');
const E = D.next = new List('E');
E.next = C;

// second method, less space memory
function findBeginning(head){
    var slow = head;
    var fast = head;
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
    return fast;
}

findBeginning(A);
```
Validate if a linked list is a plaindrome:
```javascript
const list = { val: 'F', next: { val: 'a', next: { val: 'b', next: { val: 'a', next: { val: 'F', next: null } } } } };

var isPalindrome = function(head) {
    if(!head){
        return true;
    }
    var fast = head, slow = head, arr = [];
    while(fast && fast.next){
        arr.push(slow.val);
        slow = slow.next;
        fast = fast.next.next;
    }
    if(fast){
        slow = slow.next;
    }
    while(slow){
        var current = arr.pop();
        if(current !== slow.val){
            return false;
        }
        slow = slow.next;
    }
    return true;
};

isPalindrome(list);
```
Find the intersection between two nodes:
```javascript
class List {
    constructor(letter) {
        this.val = letter;
        this.next = null;
    }
}

const A = new List("A"), B = new List("B"), C = new List("C");
A.next = B, B.next = C;
const D = new List("D")
D.next = new List("E");
const Z = new List("Z"), Y = new List("Y");
Z.next = Y;
C.next = Y.next = D;

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

console.log(JSON.stringify(getIntersectionNode(A, Z), null, 2));
```
Finding the next node after this current (in-order):
```javascript
function Leave(val){
    this.val = val;
    this.parent = null;
    this.left = null;
    this.right = null;
}
var five = new Leave(5);
var three = five.left = new Leave(3);
three.parent = five;
var seven = five.right = new Leave(7);
seven.parent = five;
var two = three.left = new Leave(2);
two.parent = three;
var four = three.right = new Leave(4);
four.parent = three;
var six = seven.left = new Leave(6);
six.parent = seven;
var eight = seven.right = new Leave(8);
eight.parent = seven;

function inorderSucc(root){
	let current = root;
    if (!root.parent || root.right) {
        current = root.right;
        while (current && current.left) {
            current = current.left;
        }
        return current;
    }
    let parent = current.parent;
    while(parent && parent.left !== current) {
        current = parent;
        parent = parent.parent;
    }
    return parent;
}

inorderSucc(eight);
```
Reverse a Linked List:
```javascript
function helper(arr) {
    if (!arr.length) {
        return null;
    }
    return {
        val: arr.pop(),
        next: helper(arr)
    };
}

function reverse(list) {
    if (!list) {
        return null;
    }
    let p2 = list, arr = [];
    while (p2) {
        arr.push(p2.val);
        p2 = p2.next;
    }
    return helper(arr);
}
```
Breadth First Search of Binary Tree:
```javascript
const tree = { val: 5, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 7, left: { val: 6, left: null, right: null }, right: { val: 8, left: null, right: null } } };

function BFS(node) {
    const queue = [node];
    while (queue.length) {
        const current = queue.shift();
        console.log(current.val);
        if (current.left) {
            queue.push(current.left);
        }
        if (current.right) {
            queue.push(current.right);
        }
    }
}

BFS(tree);
```
Add Up the value of each binary tree level:
```javascript
const tree = {val: 5, left: {val: 3, left: {val: 2, left: null, right: null}, right: {val: 4, left: null, right: null}}, right: {val: 7, left: {val: 6, left: null, right: null}, right: {val: 8, left: null, right: null}}};

function helper(arr, level, val) {
    if (arr[level]) {
        arr[level] += val;
    } else {
        arr[level] = val;
    }
}

function addBinaryTree(tree) {
    const queue = [tree];
    const res = [tree.val];
    let level = 1;
    let numberOfNodes = 1;
    while (queue.length) {
        if (!numberOfNodes) {
            level++;
            numberOfNodes = queue.length;
        }
        const curr = queue.shift();
        if (curr.left) {
            const { left, left: { val } } = curr;
            helper(res, level, val);
            queue.push(left);
        }
        if (curr.right) {
            const { right, right: { val } } = curr;
            helper(res, level, val);
            queue.push(right);
        }
        numberOfNodes--;
    }
    return res;
}

addBinaryTree(tree);
```
Depth First Search of Graph:
```javascript
const graph = [
  [0, 1, 0, 0, 1, 0],
  [1, 0, 1, 0, 1, 0],
  [0, 1, 0, 1, 0, 0],
  [0, 0, 1, 0, 1, 1],
  [1, 1, 0, 1, 0, 0],
  [0, 0, 0, 1, 0, 0]
];

function graphDFS(graph, start, goal) {
    const visited = {};
    const path = [];
    (function recurse(current) {
        visited[current] = true;
        path.push(current);
        if (current === goal) {
            return true;
        }
        for (let i = 0; i < graph[current].length; i++) {
            if (graph[current][i] && !visited[i]) {
                if (recurse(i)) {
                    return true;
                }
                path.pop();
            }
        }
    })(start);
    return path;
}

graphDFS(graph, 2, 5);
```
Breadth First Search of Graph: Time Complexity is O(V + E), where V is vertex and E is Edges
```javascript
const graph = [
  [0, 1, 0, 0, 1, 0],
  [1, 0, 1, 0, 1, 0],
  [0, 1, 0, 1, 0, 0],
  [0, 0, 1, 0, 1, 1],
  [1, 1, 0, 1, 0, 0],
  [0, 0, 0, 1, 0, 0]
];

function buildPath(parents, goal) {
    let current = goal;
    const path = [current];
    while (parents[current] !== null) {
        current = parents[current];
        path.push(current);
    }
    return path.reverse();
}

function graphBFS(graph, start, goal) {
	const queue = [start];
    const parents = { [start]: null };
    const visited = { [start]: true };
    while (queue.length) {
        const current = queue.shift();
        if (current === goal) {
            return buildPath(parents, goal);
        }
        for (let i = 0; i < graph[current].length; i++) {
            if (i !== current && graph[current][i] && !visited[i]) {
                visited[i] = true;
                parents[i] = current;
                queue.push(i);
            }
        }
    }
    return null;
}

graphBFS(graph, 2, 5);
```
Greatest Consecutive Sum in a Binary Tree:
```javascript
const tree = { val: 4, left: { val: 3, left: { val: 4, left: null, right: null }, right: { val: 1, left: null, right: null } }, right: { val: 7, left: null, right: null } };

function greatestSum(current, sum = 1) {
    if (!current) {
        return sum;
    }
    let leftSum = sum;
    if (current.left && current.val + 1 === current.left.val) {
        leftSum++;
    }
	let left = greatestSum(current.left, leftSum);
	let rightSum = sum;
    if (current.right && current.val + 1 === current.right.val) {
        rightSum++;
    }
	let right = greatestSum(current.right, rightSum);
    return Math.max(left, right);
}

greatestSum(tree); // 2
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL:
```javascript
const tree = { val: "A", left: { val: "B", left: { val: "C", left: null, right: null }, right: null }, right: { val: "D", left: { val: "E", left: { val: "F", left: null, right: null }, right: null }, right: { val: "G", left: { val: "H", left: null, right: null }, right: { val: "I", left: null, right: null } } } };

function connect(root) {
    if (!root) {
        return;
    }
    const queue = [root];
    let count = 1;
    while (queue.length) {
        const current = queue.shift();
		if (current.left) {
            queue.push(current.left);
        }
        if (current.right) {
            queue.push(current.right);
        }
        if (count === 1) {
            current.next = null;
            count = queue.length;
        } else {
            current.next = queue[0];
            count--;
        }
    }
}
```
