# [Lecture 6](https://cs50.harvard.edu/x/weeks/6)

- Python is a higher level language
- As computers got faster with more resources, programmers started developing to make computers do more of the heavy-lifiting
- Python is designed to have resemblance with human language simplifying and abstracting away complex syntax, better function notations and modules, packages instead of libraries that of C for ease of use
- Python is also program like clang but it abstracts away the implementations that directly run any `.py` python program, unlike C/clang that has to compile the program first and then run the executable
- The tradeoff is that for same purpose of task a Python program may be slower than it's C counterpart

### Syntax Features
- Data types are not required to be declared explicitly for varaibles
- Strings can be concatenated using `+` operator
- `{variable}` can contain  value that would print a formatted string with `{}` working as placeholder for variable value
- Python accepts named arguments instead of positional arguments where passed parameters change default outcome
- Such definitions in python can be found in official python documentations

##### Data types
- Python interprets datatype based on what value is assigned to variable
- Increment and decrement operators on variables are taken away
- String in python is `str`, `char` isn't a datatype in python
- `input()` function by default takes string as input, wrapped over with conversion functions like `int()` are used for storage as other `int` data type
- Python has no pointers in it, rest data-types are - `bool(True/False)`, `float`, `int`, `str`, `range`, `list`, `tuple`, `dict`, `set`, and bunch of others

##### Conditionals
- Indentation in python matters a lot so as for a certain code be excuted written after definition of some condition, *same applies for loops and function definition*
- `if`: for a single condition
- `if-else` : Two contain exactly two cases/outcomes of condition
- `elif`: To handle several conditions, `else-if` counterpart from C
- Keywords like `and`, `or` and `in` work as logical connectors for conditions

##### Object-Oriented Programming
- Datatypes have values associated with them alongside functionality built-in called methods
- Such datatypes are objects and declaring their variable is to create an instance of the datatype
- Methods are simply functions inside of object associated for data manipulation in defined instance

##### Loops
- Python does not limits itself to increments for looping in most cases
- `for`, `while` loops till the condtion following it holds true which follow the same syntax of conditionals for `and`, `or` and `in`
- Ranges as function `range()` can be used also for looping
- `for` loops in python can have a `else` scenario defined

*Unlike C python does not require just function signatures/prototypes but whole definition of function, any function's call should be after it's definition.*

### Exceptions
- Useful to handle error-cases
- `try-except` block excutes a certain chunk of code inside `try` with the assumptions that code may throw error, `except` block executes predefined code per occurance of error
- There are numerous blocks that can go wrong and each case needs to be handled separately with separate `try-except` block

### Lists
- Contained with `[]` for values of same datatypes, like arrays

### Dictionaries
- Contained with `{}` for key-value pairs where keys serve as indices

### csv
- Dictionaries can be made into comma separated values
- These are nothing but lists of key-value pairs where keys are common for all instances but values may vary
- `csv` also serves as a library to operate upon actual comma separated values file.

### sys
- Gives access to command line arguments for python programs
- There's no need of argc as using `len()` on argv returns the same
- Another such `sys` use-case is to handle cases for command line arguments using `exit()` for correct cases and wrong ones like `return` of C

### pip
- python installs packages
- Third party packages for python exist with additional features required to be installed and setup in python environment
- Similar to that of libraries of C which requires setup with compiler, which is far too complex that `pip`

*vim is also another text editor with additional support for text file editing and navigation entirely over keyboard*

# [Problem Set 6]()

### [hello]()

```
```

### [mario-less]
```
```

### [mario-more]
```
```

### [cash]
```
```

### [credit]
```
```

### [readability]
```
```

### [dna]
```
```
