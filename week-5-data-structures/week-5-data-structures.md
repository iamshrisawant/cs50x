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