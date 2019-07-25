# Lecture III: Binary Search Trees and Heaps

a. [Additional Resources](#Additional-Resources)  
b. [Text Buffer](#Text-Buffer)   
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

[CS18 Sean Chen Lecture](https://youtu.be/QYddRpvTaFk)  

[CS19 Brian Doyle Lecture](https://www.youtube.com/watch?v=B4ijhReCRHw&feature=youtu.be)   

<br>
<br>

## Additional Resources

[Binary Search Trees - 15min](https://youtu.be/SsRVdvRsNG0)  

[Heaps - 30min](https://youtu.be/LYWPsV2YQBA)  

<br>

## Text Buffer

Taking a look at our project repo's [text buffer file](bst_heaps.py), let's start working through what it might be expecting and how to build a text buffer.

The first thing we'll notice is that it imports the `DoublyLinkedList` file to use that data structure.


Our `init` function shows us that we can optionally pass the string to `self.contents` if there is a string parameter passed in -- but there doesn't need to be. How should we add to this function so it passes that string to the content?

<br>

```
def __init__(self, init=None):
    self.contents = DoublyLinkedList()
    # check if an init string is provided
    # if so, put the contents of the init string in self.contents
    if init:
        pass
```

<br>


We'll want to add this data to the tail of the linked list, but we don't know _what_ a Text Buffer is, so _how_ isn't certain.

A Text Buffer is typically an array that stores each individual character of a string -- but we're using a linked list for speed.

So, we'll loop through the string and add each character to the tail of the linked list.

<br>

```
def __init__(self, init=None):
    self.contents = DoublyLinkedList()
    # check if an init string is provided
    # if so, put the contents of the init string in self.contents
    if init:
        for character in init:
            self.contents.add_to_tail(character)
```

<br>


We can use the pre-built `add_to_tail` function from our Doubly Linked List file.

If we use a test print statement like `print(f"Adding {character}")`, our terminal will print out the following based on the tests at the bottom of the file:

<br>

```
Adding S
Adding u
Adding p
Adding e
Adding r
Super
```

<br>

So we know that it's properly iterating through the list, and that the existing `str` method concatenates them back together properly to print a string value for the Text Buffer.

We could also test the contents' length or tail to see if it matches the expected output.

<br>
<br>

## Append and Prepend


Next, let's work on append and prepend. Append starts out like so:

<br>

```
def append(self, string_to_add):
    pass
```

<br>

To append to our linked list, we'll add a string in the same way as before. Just loop through the characters and add to the tail.

<br>

```
def append(self, string_to_add):
    for character in string_to_add:
        self.contents.add_to_tail(character)
```

<br>

Since we have identical code in two places, we could make our code more DRY by using `self.append` in our `init` function instead.

<br>

```
if init:
    self.append(init)
```

<br>


Prepend means we will add the string to the front of the text buffer, or the head of the list. Which means we need to reverse the character order so that the string is being prepending to read in the correct order.

We could visualize it like so. If we wanted to add `HELLO` to the existing list that says `WORLD`:

> HELLO WORLD

If we tried to add it in order, it would go like this:

> H WORLD  
> EH WORLD  
> LEH WORLD  
> LLEH WORLD  
> OLLEH WORLD  

Since this wouldnt read correctly, we need to reverse the string so it instead is added like this:

> O WORLD  
> LO WORLD  
> LLO WORLD  
> ELLO WORLD   
> HELLO WORLD  


We can reverse a string in two ways in Python. 

The first option is to use slicing with `[::-1]`, but this is considered an arcane or difficult to read way of writing:

<br>

```
def prepend(self, string_to_add):
    # reverse the incoming string to maintain correct 
    # order when adding to the front of the text buffer 
    for character in string_to_add[::-1]:
        self.contents.add_to_head(character)
```

<br>


Another method is to use the built in `reversed` function like so:

<br>

```
def prepend(self, string_to_add):
    # reverse the incoming string to maintain correct 
    # order when adding to the front of the text buffer 
    for character in reversed(string_to_add):
        self.contents.add_to_head(character)
```

<br>

You can read more about the pros and cons of each method [here](https://dbader.org/blog/python-reverse-string).


<br>
<br>

## Delete From Head or Tail

Next we want to delete some number of characters from either the head or the tail. Both of these functions will work really similarly.

Since we know exactly how _many_ characters to remove, we can call our doubly linked list functions that many times using a loop:


<br>

```
def delete_front(self, chars_to_remove):
    for i in range(0, chars_to_remove):
        self.contents.remove_from_head()

def delete_back(self, chars_to_remove):
    for i in range(0, chars_to_remove):
        self.contents.remove_from_tail()
```

<br>
<br>

## Join

The two remaining functions left to write are both join functions.

The first one asks us to join one text buffer to another, by creating a concatenated buffer where the head of this starting buffer is at the head of the concatenated buffer, and the tail of the buffer being added is the tail of the concatenated buffer.

The starting functions gives us some hints about how to approach this problem:

<br>

```
"""
Join other_buffer to self
The input buffer gets concatenated to the end of this buffer 
The tail of the concatenated buffer will be the tail of the other buffer 
The head of the concatenated buffer will be the head of this buffer 
"""
def join(self, other_buffer):
    # we might want to check that other_buffer is indeed a text buffer 
    # set self list tail's next node to be the head of the other buffer 
    
    # set other_buffer head's prev node to be the tail of this buffer
    
    pass
```

<br>

The key of concatenating two buffers relies on setting the current tail's next as the head of the other buffer.

First, we need to make sure that the passing in `other_buffer` is actually a text buffer.

We can use Python's `isInstance` to check if both are an instance of the same class. Per the docs:

> def isinstance(obj, class_or_tuple)  
> Return whether an object is an instance of a class or of a subclass thereof.  


So we'll keep going if it is a TextBuffer or print an error if there it isn't:

<br>

```
        if isinstance(other_buffer, TextBuffer):
            # set self list tail's next node to be the head of the other buffer 
            # set other_buffer head's prev node to be the tail of this buffer
            
        else:
            print("ERROR: Argument is not a TextBuffer")
            return
```

<br>


We'll set the tail of the current TextBuffer pointing to the head of the other_buffer:

<br>

```
if isinstance(other_buffer, TextBuffer):
    # set self list tail's next node to be the head of the other buffer 
    self.contents.tail.next = other_buffer.contents.head
    # set other_buffer head's prev node to be the tail of this buffer
    other_buffer.contents.head.prev = self.contents.tail
    # now that both buffers are connected, we will set this buffer's tail to the other buffer's tail, to fully concatenate together
    self.contents.tail = other_buffer.contents.tail
    # make sure to fully extend the length to include the other buffer's length
    self.contents.length += other_buffer.contents.length
```

<br>



[Paused at 26:36](https://www.youtube.com/watch?v=B4ijhReCRHw&feature=youtu.be)


