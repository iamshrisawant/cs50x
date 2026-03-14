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
#include <cs50.h>
#include <math.h>
#include <stdio.h>  //for math related functions - round
#include <string.h> //for string related functions - strlen

void count(char in);
void grade(float l, float s);

// to let all functions access three aspects of input text
float words = 1;     // words separated blank space, first input is at least 1 word
float letters = 0;   // initial letters to be zero unless found
float sentences = 0; // initial sentences to be zero unless found end

int main()
{
    float l = 0;                      // letters per 100 words
    float s = 0;                      // sentences per 100 words
    string in = get_string("Text: "); // input text
    int len = strlen(in);             // compute string length
    for (int i = 0; i < len; i++)
    {
        count(in[i]); // count total letters, words, sentences
    }
    l = ((l + letters) / words) *
        100; // calculate average letters per word and therefore for 100 words
    s = ((s + sentences) / words) *
        100; // calculate average sentences per word and therefore for 100 words
    grade(l, s);
}

void count(char in)
{

    if (in == ' ') // words separated with ' ' - blank spaces
    {
        words++; // increment words per found blank space
    }
    else if (in == '.' || in == '!' || in == '?') // sentences separated with '.' - full stops
    {
        sentences++; // increment sentences per found full stops
    }
    else if ((in >= 'a' && in <= 'z') || (in >= 'A' && in <= 'Z')) // look for character letters
    {
        letters++; // increment letters per found character letter
    }
}

void grade(float l, float s)
{
    float index = (0.0588 * l) - (0.296 * s) - 15.8; // coleman liau index
    int grade = round(index);                        // index rounded to integer
    // condiotionals to set grade per coleman liau index and required scale
    if (grade < 1)
    {
        printf("Before Grade 1\n");
    }
    else if (grade >= 16)
    {
        printf("Grade 16+\n");
    }
    else
    {
        printf("Grade %d\n", grade);
    }
}
```

### 3. [Caesar](https://cs50.harvard.edu/psets/3/caesar)

```
#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, string argv[])
{
    if (argc != 2) // check argument count is strictly 2 if not prompt usage of cauesar
    {
        printf("Usage: %s key\n", argv[0]);
        return 1;
    }
    int key_len = strlen(argv[1]);
    for (int i = 0; i < key_len; i++)
    {
        if (!(argv[1][i] >= '0' &&
              argv[1][i] <= '9')) // check key is a positive number if not prompt usage of cauesar
        {
            printf("Usage: %s key\n", argv[0]);
            return 1;
        }
    }
    string ptext;
    int key = atoi(argv[1]);           // convert key to an integer
    ptext = get_string("plaintext: "); // get plain text string
    int len = strlen(ptext);           // calculate length of plain text
    // start printing cipher text
    printf("ciphertext: ");
    for (int i = 0; i < len; i++)
    {
        // for all characters base ASCII value to start from zero equivalent then restore
        // substractions makes set start from 0 and addition restores to original ASCII value
        if (ptext[i] >= 'a' && ptext[i] <= 'z')
        {
            printf("%c", (((ptext[i] - 97) + key) % 26) + 97);
        }
        else if (ptext[i] >= 'A' && ptext[i] <= 'Z')
        {
            printf("%c", (((ptext[i] - 65) + key) % 26) + 65);
        }
        else
        {
            printf("%c", ptext[i]);
        }
    }
    printf("\n");
    return 0; // program finished successfully
}

```

### 4. [Substitution](https://cs50.harvard.edu/psets/3/substitution)

```
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(int argc, string argv[])
{
    if (argc != 2) // check if arguments are exactly 2
    {
        printf("Usage: %s key\n", argv[0]); //
        return 1;
    }
    // check key length is 26 characters
    int key_len = strlen(argv[1]);
    if (key_len != 26)
    {
        printf("Key must contain 26 characters.\n");
        return 1;
    }
    // check all key characters are alphabets
    for (int i = 0; i < key_len; i++)
    {
        // check if a character is alphabetic
        if (!((argv[1][i] >= 'A' && argv[1][i] <= 'Z') || (argv[1][i] >= 'a' && argv[1][i] <= 'z')))
        {
            printf("Key must only contain alphabetic characters.\n");
            return 1;
        }

        for (int j = i + 1; j < key_len; j++)
        {
            char char_i = (argv[1][i] >= 'a') ? argv[1][i] - 32 : argv[1][i];
            char char_j = (argv[1][j] >= 'a') ? argv[1][j] - 32 : argv[1][j];

            if (char_i == char_j)
            {
                printf("Key must not contain duplicate characters.\n");
                return 1;
            }
        }
    }

    // get plaintext from user
    string in = get_string("plaintext:  ");
    int len = strlen(in);

    // encrypt and print ciphertext
    printf("ciphertext: ");
    for (int i = 0; i < len; i++)
    {
        // handle Uppercase
        if (in[i] >= 'A' && in[i] <= 'Z')
        {
            int index = in[i] - 'A'; // get index 0-25
            char out = argv[1][index];
            // ensure output is uppercase even if key char is lowercase
            if (out >= 'a' && out <= 'z')
            {
                printf("%c", out - 32);
            }
            else
            {
                printf("%c", out);
            }
        }
        // handle Lowercase
        else if (in[i] >= 'a' && in[i] <= 'z')
        {
            int index = in[i] - 'a';
            char out = argv[1][index];
            // ensure output is lowercase even if key char is uppercase
            if (out >= 'A' && out <= 'Z')
            {
                printf("%c", out + 32);
            }
            else
            {
                printf("%c", out);
            }
        }
        else
        {
            printf("%c", in[i]); // print characters other than alphabets as are
        }
    }
    printf("\n");
    return 0;
}

```