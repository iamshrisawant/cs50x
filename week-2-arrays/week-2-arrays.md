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

- **cryptography**: scrambling information to achieve secure communication of it
- One might encrypt a message and others might access it but only the designated receiver should be able to read it.
