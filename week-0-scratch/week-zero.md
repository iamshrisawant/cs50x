# Lecture 0

- Computer Science - Study of information, computational thinking, problem solving.
- Input $\rightarrow$ Black Box $\rightarrow$ Output - black box being the problem solving element.
- Information represented in patterns of 0s(Low/off) and 1s(High/On) and their positions - bits.
Computational hardware such as transistors can only understand High or Low values in electricity.

### Binary
- In decimal, the regular number system, digits are read left to right with positional weights being in power of 10.
- Where in decimal each position can hold 10 digits 0 to 9, in binary it is a bit - 0 or 1,  thus making weight of each position in power of 2.
- Power in such systems systems start with zero for rightmost position and increases by one as we move towards left.

$$ \text{Weighted Positional Bit Value} = 2^n \times bit(0,1)  $$

$$ \text{Decimal Representation} = \text{Sum of weighted positional bit values} $$

- Combination of eight such bits is a byte, representing 256 possibilities.
- Using 32 bits  or even 64 bits to represent a chunk of information is a standard today.

A pattern with $n$ positions can represent $2^n$ different values - numbers, colors, text, symbols, etc.

### Binary Pattern Representations

##### ASCII
A mapping corresponding set of characters to numeric equivalents. $2^7$ standard characters including - control instructions, digits, text, symbols.

| Character | Decimal |
| --------- | ------- |
| Space     | 32      |
| 0         | 48      |
| 9         | 57      |
| A         | 65      |
| Z         | 90      |
| a         | 97      |
| z         | 122     |

$$ Lowercase = Uppercase+32 $$

##### Unicode - Superset of ASCII
Used to represent all characters - symbols from all languages, expressions, idea, etc. using more number of bits to represent a particular character.

##### RGB - Additive color model
8 bits for each color- Red, Green and Blue represent its intensity from 0 to 255 for each pixel of a screen with total 24 bits that is $2^24$ possible colors.

##### Other representations
- images - Matrix of RGB pixels.
- Videos - Images per second.
- Sound - Numbers may represent all characters of a particular sound - pitch, loudness, etc.

### Algorithms
Logical steps to not only solve problems but to do it computationally efficient.

### Pseudocode
- Taking input is some representation of numbers, text, operations to compute output.
- Includes study of all possible behaviors and scenarios while computing output for any input.
- Anticipating every possibility helps in handling every possible scenario.

### Scratch
- Loops - repeating a block of code.
- Abstractions - blocks implemented already to execute a certain logic.
- Conditionals - allow to check truth of certain conditions.

# Problem Set 0 - Starting from Scratch
[Submission](https://github.com/me50/iamshrisawant/tree/386db88b0af64bf390851bb457551de7d5ded8b7)
