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

We want to search the tree, holding onto a max value and updating it if a greater one is found. Our base case is an empty tree. We also know that the max value will be found down the right hand side, not the left, based on the greater than conventional architecture.

<br>

```
def get_max(self):
if not self:
    return None
if not self.right:
    return self.value
else:
    return self.right.get_max()
```

<br>

We are checking if there is a node to the right. If there isn't, then we know that's the max.

Otherwise, we keep searching down the right by calling get_max on the next right node.

Our last function to get is the `for_each` method which should visit each node in the tree and run a callback function on it.

We can continue writing this with recursion. 


<br>

```
def for_each(self, cb):
cb(self.value)

if self.left:
    self.left.for_each(cb)
if self.right:
    self.right.for_each(cb)
```

<br>

Why are we not including a return?

We're trying to _run_ a function on each value -- that may or may not already include a return statement -- not receive back a value, because if we used a return, then it will only go down the left side and exit out of the function before ever calling down the right side of the tree.

<br>
<br>

## Review Heaps

Let's talk about Heaps conceptually. A heap is stored inside of an array because we need to be able to access things at a specific spot -- but it looks like a tree because when we access items, we use specific functions that traverses the array like a binary tree in parent-child relatonships.

This is unlike the usual array method of accessing things just in a sequential method.

This is more efficient because it has an O(1) run time for some operations and the space complexity is simply O(n). There is no extra space or pointer storage. It's solely storing the data.

Visually, it makes more sense to "view" this as a tree (because of the parent-child relationships), but it _is_ stored in an array.

<br>

[Here](https://www.cs.usfca.edu/~galles/visualization/Heap.html) and [here](http://btv.melezinek.cz/binary-heap.html) are heap visualiation websites.  


<br>

Inserting in a min heap means adding a node, then bubbling up through the array to compare to each parent, and swapping them if they should be reversed based on value.

In the array, the new node is being added to the end of the array, then it's finding the parent using [these equations](http://geeksquiz.com/binary-heap/).


_Brian goes into depth about this around 40 minutes into the CS19 lecture._

Q: Why it is advantageous to replace the lowest leaf when popping off the root and then sift that child down. Why not swap the next largest child of that root after removing the root?

A: Less comparisons to make by sifting the lowest down.  If we just move the 2nd largest up, then we have to check all of the children of each child to make sure the heap property is maintained.

Heap Insert:
 - Add Item to end of tree
 -  Bubble it up to the right spot

Heap delete:
 - Swap priority element with least priorty
 - Remove the last element (previously the root)
 -  Sift down new top to the correct spot

<br>
<br>


## Practice Interview Questions









