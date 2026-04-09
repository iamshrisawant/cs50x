# [Lecture 5](https://cs50.harvard.edu/x/weeks/5)

- Data structures are also termed abstract datatypes
- Differ by what characterstics, functions they of regardless of lower level implementations
- **Queue:** A First-In-First-Out(FIFO)
    - First object in is first object out
    - Enqueue: Add to the end of the queue
    - Dequeue: remove from the front of the queue
- **Stack:** A Last-In-First-Out(LIFO)
    - Last object in is first object out
    - Push: Add on top of stack
    - Pop: Delete from top of stack
- **Dictionaries:**
    - Holds a *key-value* pair
    - Associates one piece of data to another piece of data
    - Like a word and it's definition

### Resizing Array and `realloc()`

- Generally, arrays are predefined in a program thus allocating a contiguous set of memory
- This allocates a static memory chunk to array
- `malloc(size)` can be used to allocate a chunk of memory and address it's address to a pointer
- Values can also be assigned to this array with syntax `*(chunk + index) = value`
- And again with `malloc(size)` can be used to allocate a bigger chunk and copy original array to it with added memory
- `realloc(chunk, size)` abstracts away the copying part and reallocate the memory for array with original data in chunk
- Even so it requires a temporary pointer to store addresses of original chunk and reallocated chunk

### Linked Lists

- No matter where the values are in memory, connecting them would make it contiguous
- Values can be allocated memory using `malloc()` but allocation per value is not necessarily contiguous
- To connect these values, memory can be allocated for a pointer to next chunk of allocation along side current value with `malloc()`
- A `struct` definition of such structure can be:
    ```
    typedef struct node
    {
        int value;
        struct node *next;
    }node;
    ```
    where node is a unit of it
- When setting values in members of this structure for a instance at n,
    - General method is: `(*n).value` / `(*n).next` - go to address of that node and update the fields
    - In C syntax simplifies it as `n->value` / `n->next`

*Linked lists with two pointers for forward and backward traversal are called doubly linked list*

### Trees
-  A node is a unit of it with pointers leading to two of it's child nodes
- Parent node is the one having a pointer leading to next node, the next node is child node
- First node in the tree is the root node 
- With each node having two childs, those with none at the end are the leaf nodes
- *Binary Search Tree* has the property: Left node < Root node < Right node

### Hashing
- Mapping a finite or infinite domain of values to a fintite range of values
- Bucketizes values into finite number of buckets where those should belong
- A hash function determines the value of data based on which it get bucketized

### Hash Tables
- Associates a piece of data with another using hash function which outputs index for input value
- Like the *key-value* pair logic of dictionaries, hash table have such pairs stored for data retrieval
- Helpful for data retrieval operations with constant time complexity for insertion, deletion and search

### Tries
- Store strings through character arrays connected as linked lists
- Common prefixes are shared among strings with breakpoints determined by null pointers
- Takes up space - bad for small datasets, effective for big ones reaching constant time complexity

