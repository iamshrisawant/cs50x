# Lecture 1

- Source code - the program that us humans can understand
- Machine code - the program that a machine can understand
- Compiler - maps source code to machine code, helps point out errors in code

### VS Code and Hello, World
- **CLI commands** are often more productive, some to get started -
	- `code file-name.c` opens VS code to edit file - VS code specific
	- `make filename` converts Source code of C in `file-name.c` to machine code `file-name` 
	- `./file-name` lets machine access the file
- Hello, World - first program to study the ins and outs of C and all programming languages

### Scratch to C
- **Escape Sequences** are special code blocks to instruct compilers for special commands(`\n`, `\"`, etc.) in strings
- **Header Files** contain function declarations(reflecting on structure/signature of functions) somewhere else in the programming environment of compiler
- **Manual Pages** documentation of code implementations, in C for example Header Files and their functions

### Hello, You
- In C, program values cannot be directly passed into a string
- Placeholder format codes(`%s`, `%d`, etc.) are used to place in value to the string
- Value variables are written sequentially after string ends

### Terminal Commands
Used to the most fundamental computer operations like navigation, folder creation, copying, deleting files using the **Command Line Interface(CLI)** instead of **Graphical User Interface(GUI)**

### Conditionals
- Check certain condition to be true or false by returning bool values
- Comparative operators(`>`, `<`,`==`, etc.) used to compare two statements, values, variables
- `if`, `if-else`,`else if`

### Types
- In C to deal with various kinds of data efficiently there are types defines such as - for numbers: `int`, for characters:`string`, etc.
- Assigned to variables or declared values
- Format codes are different for these different types - `int`:`%d`, `string`:`%s`, etc.

### Loops
Repeat certain block of code till required condition for repetition is true - `for`,`while`,`do while`

### Functions
- Abstractions of reusable code blocks, user-defined instead of pre-defined from header files
- Often defined with return types and input arguments with their types - `void`, `int`, etc.
- Signature of the functions should come before entering the main code 
- Variables declared inside function are limited to scope of that function
- However values can be passed as arguments if parameters considered in function definition
