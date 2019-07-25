# Lecture IV: 

a. [](#)  
b. [](#)   
c. [](#)   
d. [](#)   
e. [](#)   
f. [](#)   
g. [](#)   
h. [](#)   
i. [](#)   
j. [](#)   
k. [](#)   
l. [](#)   
m. [](#)   
n. [](#)      

<br>

[Add on that gives VSCode windows unique color themes](https://marketplace.visualstudio.com/items?itemName=stuart.unique-window-colors)

<br>

## Binary Search Tree

Going through our BST project, we currently have the following code and need to work on `contains`:

<br>

```
class BinarySearchTree:
  def __init__(self, value):
    self.value = value
    self.left = None
    self.right = None

  def insert(self, value):
    if value < self.value:
        if not self.left:
            self.left = BinarySearchTree(value)
        else:
            # recursively continues until we find an empty spot
            self.left.insert(value)
    else:
        if not self.right:
            self.right = BinarySearchTree(value)
        else:
            self.right.insert(value)

  def contains(self, target):
    pass
```

<br>

We need to check where we are in the tree. If the target is the current value, then we know that we're already done. Otherwise, we need to traverse the tree.

We need to decide if we want to go left or right, so how can we decide that? We'll compare our value to our target, choosing a path based on if it's less or greater than.

Depending on the direction chosen, if there are no futher nodes to search for it, and it's not a match, then we know it doesn't exist in this tree. If there are more nodes, we need to call the same function recursively, but on the node on the right or left.

<br>

```
def contains(self, target):
if self.value == target:
    return True

if target < self.value:
    # we know to go left
    if not self.left:
        # if there are no further left side nodes to search, it isn't here
        return False
    else:
        # recursively search the rest
        return self.contains(target)

else:
    # we know to go right
    if not self.right:
        return False
    else:
        return self.contains(target)
```

<br>


Next, let's work through `get_max`. 













