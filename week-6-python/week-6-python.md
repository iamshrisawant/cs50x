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
- Python has no pointers in it

##### Conditionals
- Indentation in python matters a lot so as for a certain code be excuted written after definition of some condition, *same applies for loops and function definition*
- `if`: for a single condition
- `if-else` : Two contain exactly two cases/outcomes of condition
- `elif`: To handle several conditions, `else-if` counterpart from C
- Keywords like `and`, `or` and `in` work as logical connectors for conditions

##### Object-Oriented-Programming
- Datatypes have values associated with them alongside functionality built-in called methods
- Such datatypes are objects and declaring their variable is to create an instance of the datatype
- Methods are simply functions inside of object associated for data manipulation in defined instance


