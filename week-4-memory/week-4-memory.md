# [Lecture 4](https://cs50.harvard.edu/x/weeks/4)

- Digital pictures are also stored in representations of zeroes and ones
- The units of these representations are pixels which collectively for up the image to display
- More the pixels better the details in picture captured

### Hexadecimal
- An extension to decimal where 10 to 15 are reprerented with a to f, making it a total of 16 digit system
- Requires 4 bits to represent a digit in hexadecimal
- Commonly used in representation of colours in images, memory adresses, etc.

### Memory
- For ease of representation, memory addresses are represented with hexadecimal system
- It allows to represent a byte with two hexadecimal digit instead of eight independent bits
- In memory `0x` is used as prefix to indicate what follows it is a address

### Pointers
- Pointer is a variable that stores address of another variable or value in memory
- In C, program with memory access specifically:
  - `&`(Reference Operator): Accesses the address of variable in code alongside it
  - `*`(Dereference Operator): Defines a pointer variable to store address of declared datatype
  - `%p`: Specifically used to scan or print an address of a variable
- Only a pointer variable of declared datatype can hold address of variable of same datatype or access value at address it holds
- Pointer size may vary per platform - 8 bytes for 64 bit platform, 4 bytes for 32 bit platform
- Represented with arrows in memory from blocks that hold address of block holding value

### Strings
- Strings are basically an array of `char` datatype units which are addressable stored contiguously
- `string` is defined as `char *`, a pointer to first character in memory
- The declared variable holds the address of beginning of the string and `\0` holds where string ends
- If we compare `strng` variables directly the addresses of first `char`s in are compared instead of contents
- Thus `strcmp` accesses the values at the address to compare each `char` in string iteratively
- Normal equation of `string`s would only copy address in RHS to LHS
- Two functions help with memory operations well:
  - `malloc` allocates memory equivalent to passed argument and passes address of first block to it's variable
  - `free` takes that same address value to free the allocated space

### valgrind
- Aids to debug memory related errors
- Outputs a insignt into program's memory usage
- Usually verbose to read but helps with retaining most of memory alocated to the program

- *Pointers are declared with deference operators which intially do not point to anything, called null pointers(`nullptr`)*
- *Pointee is the value a pointer points at*
- *`*` helps with dereferencing the address, `&` helps with accessing the address, where as a plain variable declared with `*` is supposed to hold an address*

### Pointer Arithmetic
- Address or pointers are basically numbers, thus can be operated upon with arithmetics
- To access continuous blocks in memory same similarly to that of an array
- We simply add/subtract integers from variables holding address to point to required blocks

- Memory is assigned in a deliberate way:
  - The top of the memory usually holds machine code
  - Then come the global values, variables which are defined outside of `main()`
  - Then from top to bottom is **heap** which is growing allocation of memory using malloc
  - At the bottom is **stack** which allocation of memory per call of function for it's local variables growing upwards
- In this model, eventually, continuous allocation of memory would make **heap** and **stack** clash with each other causing a overflow
  - Stack Overflow: When program tries to access memory beyond it's call stack
  - Heap Overflow: A kind of Buffer Overflow, when program tries to write data more than the allocated buffer heap can hold
- Use of pointers can significantly make programs more efficient with thoughtful operations over memory

### scanf
- Normally used to scan or take input in program instead of using cs50's `get_int`, `get_string`, etc.
- Requires use of `&` to access variable's address while assigning input value to the address in case of variables
- Strings or arrays however which already have declaration of first value address stored in pointer do not require use of `&` as variable itself holds address

# [Problem Set 4](https://cs50.harvard.edu/x/psets/4/)=
