Remove Duplicates from Linked List:
```javascript
// javascript version
const list = {val: 'F', next: { val: 'O', next: { val: 'L', next: { val: 'L', next: { val: 'O', next: { val: 'W', next: null } } } } } };

function remove(head){
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

remove(list);
```
```go
// go version
type Node struct {
    val string
    next *Node
}

func remove(head *Node) *Node {
    current := head
    for current != nil {
        runner := current
        for runner != nil {
            if runner.next != nil && runner.next.val == current.val {
                runner.next = runner.next.next
            } else {
                runner = runner.next;
            }
        }
        current = current.next
    }
    return head
}

func main() {
    list := Node{"F", &Node{"O", &Node {"L", &Node{"L", &Node{"O", &Node{"W", nil}}}}}}
    remove(&list)
}
```
Find Kth to the last element in a singly linked list:
```javascript
// javascript version
function findK(head, k){
    let pointer1 = head, pointer2 = head, i = 0;
    while(i < k && pointer2){
        pointer2 = pointer2.next;
        i++;
    }
    while(pointer2){
        pointer1 = pointer1.next;
        pointer2 = pointer2.next;
    }
    return pointer1;
}

findK(list, 2);
```
```go
// go version
type Node struct {
    val string
    next *Node
}

func findK(head *Node, k int) *Node {
    pointer1, pointer2 := head, head; counter := 0
    for counter < k && pointer2 != nil {
        pointer2 = pointer2.next
        counter++
    }
    for pointer2 != nil {
        pointer1 = pointer1.next
        pointer2 = pointer2.next
    }
    return pointer1
}

func main() {
    list := Node{"F", &Node{"O", &Node {"L", &Node{"L", &Node{"O", &Node{"W", nil}}}}}}
    findK(&list, 2)
}
```
Removing the kth to the last element from a linked list:
```javascript
// javascript version
var list = {val: 1, next: {val: 2, next: null}};

var removeNthFromEnd = function(head, n) {
    var pointer1 = head, pointer2 = head, i = 0;
    while(i < n){
        pointer2 = pointer2.next;
        i++;
    }
    if(!pointer2){
        return head.next;
    }
    while(pointer2.next){
        pointer1 = pointer1.next;
        pointer2 = pointer2.next;
    }
    pointer1.next = pointer1.next.next;
    return head;
};

removeNthFromEnd(list, 1);
```
```go
// go version
type Node struct {
    val string
    next *Node
}

func removeK(head *Node, k int) *Node {
    count := 0; pointer1, pointer2 := head, head
    for count < k && pointer2 != nil {
        pointer2 = pointer2.next
        count++
    }
    if pointer2 == nil {
        return pointer1.next
    }
    for pointer2.next != nil {
        pointer1 = pointer1.next
        pointer2 = pointer2.next
    }
    pointer1.next = pointer1.next.next
    return head

}

func main() {
    list := Node{"F", &Node{"O", &Node {"L", &Node{"L", &Node{"O", &Node{"W", nil}}}}}}
    removeK(&list, 3)
}
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
	if(checkHeight(root) === -1) {
		return false;
	}
	return true;
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
	let node = {
		value: arr[middle],
		left: createBST(arr, start, middle - 1),
		right: createBST(arr, middle + 1, end)
	};
	return node;
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

function findKSmallest(node, k) {
    let result = null, i = 1;
    (function recurse(current) {
        if (!current) {
            return;
        }
        if (current.left) {
            recurse(current.left);
        }
        if (i === k) {
            i++;
            result = current;
            return;
        } else {
            i++;
        }
        if (current.right) {
            recurse(current.right);
        }
    })(node)
    return result;
}

findKSmallest(tree, 4);
```
Remove from a linkedlist that has the same val:
```javascript
const list = {val: 'F', next: { val: 'O', next: { val: 'L', next: { val: 'L', next: { val: 'O', next: { val: 'W', next: null } } } } } };

var removeElements = function(head, val) {
    if(!head){
        return null;
    }
    if(head.val === val){
        return removeElements(head.next, val);
    }
    (function recurse(current){
        if(!current){
            return;
        }
        while(current.next && current.next.val === val){
            current.next = current.next.next;
        }
        recurse(current.next);
    })(head);
    return head;
};

removeElements(list, "L");
```
Check if subtree is part of tree:
```javascript
const subTree =  { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } };
const tree = { val: 5, left: { val: 3, left: { val: 2, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 7, left: { val: 6, left: null, right: null }, right: { val: 8, left: null, right: null } } };

function match(t1, t2){
    if(!t1 && !t2){
        return true;
    }
    if(!t1 || !t2){
        return false;
    }
    if(t1.val !== t2.val){
        return false;
    }
    return (match(t1.left, t2.left) && match(t1.right, t2.right));
}

function subtree(t1, t2){
    if(!t1){
        return false;
    }
    if(t1.val === t2.val){
        if(match(t1, t2)){
            return true;
        }
    }
    return (subtree(t1.left, t2) || subtree(t1.right, t2));
}

function containsTree(t1, t2){
    if(!t2){
        return true;
    }
    return subtree(t1, t2);
}

containsTree(tree, subTree);
```
Finding the beginning of linked list circle:
```javascript
function List(letter){
    this.val = letter;
    this.next = null;
}
var A = new List("A");
var B = A.next = new List('B');
var C = B.next = new List('C');
var D = C.next = new List('D');
var E = D.next = new List('E');
E.next = C;

// first method
function recurse(head){
    var current = head;
    while(!current.visit){
        current.visit = true;
        current = current.next;
    }
    return current;
}

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
var getIntersectionNode = function(headA, headB) {
    var a = headA, b = headB;
    while(true){
        if(!a){
            while(b){
                b = b.next;
                headB = headB.next;
            }
            break;
        }
        if(!b){
            while(a){
                a = a.next;
                headA = headA.next;
            }
            break;
        }
        a = a.next;
        b = b.next;
    }
    while(headA){
        if(headA === headB){
            return headA;
        }
        headA = headA.next;
        headB = headB.next
    }
    return null;
};
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
    let current = null;
    if(!root){
        return current;
    }
    if(!root.parent || root.right){
        current = current.right;
        while(current && current.left){
            current = current.left;
        }
        return current;
    }
    else{
        let prev = root.parent;
        while(prev && prev.left !== current){
            current = prev;
            prev = prev.parent;
        }
        return prev;
    }
}

inorderSucc(eight);
```
Reverse a Linked List:
```javascript
function reverseLink(node) {
    if (!node) {
        return null;
    }
    let pointer1 = node, pointer2 = node;
    const arr = [];
    while (pointer2) {
        arr.push(pointer2.value);
        pointer2 = pointer2.next;
    }
    while (pointer1) {
        pointer1.value = arr.pop();
        pointer1 = pointer1.next;
    }
    return node;
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
var tree = {val: 5, left: {val: 3, left: {val: 2, left: null, right: null}, right: {val: 4, left: null, right: null}}, right: {val: 7, left: {val: 6, left: null, right: null}, right: {val: 8, left: null, right: null}}};

function addBinaryTree(head) {
    const queue = [head];
    const sum = [head.val];
    let level = 1;
    let numberOfNodes = 1;
    while (queue.length) {
        if (!numberOfNodes) {
            level++;
            numberOfNodes = queue.length;
        }
        const current = queue.shift();
        if (current.left) {
            if (sum[level]) {
                sum[level] += current.left.val;
            } else {
                sum[level] = current.left.val;
            }
            queue.push(current.left);
        }
        if (current.right) {
            if (sum[level]) {
                sum[level] += current.right.val;
            } else {
                sum[level] = current.right.val;
            }
            queue.push(current.right);
        }
        numberOfNodes--;
    }
    return sum;
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
    const visited = { [start]: true };
    const queue = [start];
    const parents = [];
    parents[start] = null;
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
const tree = { val: 0, left: { val: 1, left: { val: 3, left: null, right: null }, right: { val: 4, left: null, right: null } }, right: { val: 2, left: { val: 5, left: null, right: null }, right: { val: 6, left: null, right: null } } };

function connect(root) {
    if (!root) {
        return;
    }
    const queue = [root];
    let count = 1;
    while (queue.length) {
        const current = queue.shift();
        if (current.right) {
            queue.push(current.left);
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
