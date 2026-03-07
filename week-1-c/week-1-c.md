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

# Problem Set 1

### 1. Hello, World

``
#include <stdio.h>

int main()
{
    printf("hello, world\n");
}
``

### 2. [Hello, Me](https://github.com/me50/iamshrisawant/tree/9116fe789df578cd5f8c1d4687bea34b8fb208fe)

``
#include <cs50.h>
#include <stdio.h>

int main()
{
    string name = get_string("name?\n");
    printf("hello, %s\n", name);
}
``

### 3. [Mario-less](https://github.com/me50/iamshrisawant/tree/390fb3f4ddc2f0396d818831a2094966f4e2bd4a)

``
#include <cs50.h>
#include <stdio.h>

int main()
{
    int n=0;
    while( n <= 0) //Accept only a positive integer
    {
        n = get_int("Enter a height:");
    }

    for (int i = n; i > 0; i--) // i rows reduce from n to 1
    {
        for (int j =  1; j < i; j++) //prints blanks till column is not same as row
        {
            printf(" ");
        }
        for (int j = i; j <= n; j++) //prints #s from column is same as row till n
        {
            printf("#");
        }
        printf("\n"); //new row
    }
}
``

### 4. [Mario-more](https://github.com/me50/iamshrisawant/tree/e1ca3787033b3af51386373c99d5d1dd5597ac9c)

``
#include <cs50.h>
#include <stdio.h>

int main()
{
    int n = 0;
    while (n <= 0) // Accept only a positive integer
    {
        n = get_int("Enter a height:");
    }

    for (int i = n; i > 0; i--) // i rows reduce from n to 1
    {
        for (int j = 1; j < i; j++) // prints blanks till column is not same as row
        {
            printf(" ");
        }
        for (int j = i; j <= n; j++) // prints #s from column is same as row till n
        {
            printf("#");
        }
        printf("  ");                // prints constant double blanks
        for (int j = n; j >= i; j--) // prints trailing #s in reverse logic
        {
            printf("#");
        }
        printf("\n"); // next row
    }
}
``

### 5. [cash](https://github.com/me50/iamshrisawant/tree/d4aa4610383d0dbbc7fb26dc2762e6159965c193)

``
#include <cs50.h>
#include <stdio.h>

int change(int x); // change function signature

int main()
{
    int owed = 0;
    while (owed <= 0) // validate input to be non-negative
    {
        owed = get_int("change owed:"); // take input
    }
    int coins = change(owed); // get coins count from change function

    printf("%d\n", coins); // print final count of coins
}

int change(int x) // change function definition
{
    // divide change with coins to cover value of availble coins(25, 10, 5, 1)
    int y = x / 25;
    // update change to give before division with next available coins
    x = x % 25;
    y += x / 10;
    x = x % 10;
    y += x / 5;
    x = x % 5;
    y += x;
    return y; // return total coins evaluated
}
``

### 6. [credit]()