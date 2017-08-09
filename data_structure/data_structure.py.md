Greatest Consecutive Sum in a Binary Tree:
```python
class Node:
    def __init__(self, val, left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

tree = Node(4, Node(3, Node(4), Node(1)), Node(7))

def greatestSum(current, sumResult = 1):
    if not current:
        return sumResult
    leftSum = sumResult
    if current.left and current.val + 1 == current.left.val:
        leftSum += 1
    left = greatestSum(current.left, leftSum)
    rightSum = sumResult
    if current.right and current.val + 1 == current.right.val:
        rightSum += 1
    right = greatestSum(current.right, rightSum)
    return max(left, right)

greatestSum(tree)
```
