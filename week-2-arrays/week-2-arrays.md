# [Lecture 2](https://cs50.harvard.edu/x/weeks/2/)

- Reading levels - approximated by function of reading
- More the complexity handled higher the level
- In case of reading level increases as words, sentences, rhymes, tones, lengths,vocabulary start increasing.

### Debugging
- Bugs: problems in code or program
- Syntactical Error
    - Some found at compile time show up as errors
    - These can be fixed if read carefully through error messages
- Logical Error
    - Code is syntactically complete and compiled
    - However lack of logical implementation does not yield expected output
    - Needs careful inspection of logic for a fix
- Debuggers are the tools to inspect a the code line by line for logical operations
- Requires adding breakpoints at line to step through the code line by line

### Compiling
- clang - the compiler triggered through make command
- produces file such as a.out - assembler output
-  command line arguments play a vital role to influence compilation of file - e.g. file-name, linking header files, etc.
- these command lines can be automated by configuring different semantically simpler commands such as make
- compilation stages:
    - Preprocessing: Fetches all code about to be used through header files
    - Compiling: Takes preprocessed code and converts to assembly
    - Assembling: Assembly converts to binary
    - Linking: All code from header file prototypes precompiled linked in program file

### Types
- Different data types require different number of bits or bytes(8 bit per byte) for representation
- Memory holds data form of bits/bytes into contiguous blocks of it.
- All computation does is flip those bits by logically adressing their blocks in memory

### Arrays
- A sequence of values contiguously arranged in memory
- Of the same datatype
- `Variable[Index]` represents each unique value
- Declaring an array requires declaring it with a designated length
- When passing an array to function, another argument should be it's length

### Strings
- A sequence of `char`s where, `char`s are again numbers mapped to ASCII numbers to represent using 8 bits in contiguous memory
- Thus an array of characters, but length is +1 than number of chars for  terminal character NUL `\0` indicating end of string with `""`
- `string.h` header file contains string related libraries to use various functions to operate on strings with ease

### Command Line Arguments
- Commands like - make, clang, -o, etc and parameters expected at executions.
- Normally  `main()` takes to no input thus it has input as function- `void`
- To make a program accept such command line arguments `main(int argc, string argv[])`
    - `int argc` is count of arguments to be provided
    - `string argv[]` is a vector of acceptable arguments
- `argv[0]` contains the file name created for the program
- `argv[1]` and further may contain all accepted and acceptable command line arguments

### Exit Status
- Represents specific cases to denote success, failure and cause of failure
- Measure to point out to what in program has gone wrong
- Return 0 denotes success, any number within a range apart from standard conventions can be used to denote program specific code failures
- `echo $?` command returns the status code assigned to program for return at failure

### Cryptography
- **Encryption**: Scrambling information to achieve secure communication of it in a reversible way
- One might encrypt a message and others might access it but only the designated receiver should be able to read it
- Plain Text: Original useful data
- Cipher Text: Original Data scrambled in a reversible order
- Secret Key: Particular value used to scramble data
- Cipher: Function that takes in secret key, plain text to return Cipher Text
- The secret key and cipher function is known only to sender and receiver for secure connection
- **Decryption**: Reverse the Cipher function get plain text from cipher text.

# [Problem Set 2](https://cs50.harvard.edu/x/psets/2/)

### 1. [Scrabble](https://cs50.harvard.edu/x/psets/2/scrabble)

```
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int calculate_score(string s);

int scores[] = {1, 3, 3, 2,  1, 4, 2, 4, 1, 8, 5, 1, 3,
                1, 1, 3, 10, 1, 1, 1, 1, 4, 4, 8, 4, 10}; // Global declaration of score table

int main()
{
    int score1, score2;
    string in = get_string("Player 1: "); // Read player 1 input
    score1 = calculate_score(in);         // calculate score for player 1
    in = get_string("Player 2: ");
    score2 = calculate_score(in);
    // check for what is greater or if it is a tie
    if (score1 > score2)
    {
        printf("Player 1 wins!\n");
    }
    else if (score1 < score2)
    {
        printf("Player 2 wins!\n");
    }
    else
    {
        printf("Tie!\n");
    }
}

int calculate_score(string s)
{
    int score = 0;                // set initial score to 0
    int len = strlen(s);          // take string length
    for (int i = 0; i < len; i++) // iterate till last letter in string
    {
        if (s[i] >= 'a' && s[i] <= 'z') // check for lowercase letters
        {
            score =
                score + scores[(s[i] - 97)]; // make found letter to postionally equivalent with
                                             // index in scores table as ASCII equivalent of a is 97
        }
        if (s[i] >= 'A' && s[i] <= 'Z') // check for uppercase letters
        {
            score = score + scores[(s[i] - 65)]; // as ASCII equivalent of A is 65
        }
    }
    return score; // return calculated score for input string
}
```

### 2. [Readability](https://cs50.harvard.edu/psets/3/readability)

```

```

### 3. [Caesar](https://cs50.harvard.edu/psets/3/caesar)

```

```

### 4. [Substitution](https://cs50.harvard.edu/psets/3/substitution)

```

```