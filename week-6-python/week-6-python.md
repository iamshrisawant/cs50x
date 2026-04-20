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

# [Problem Set 6](https://cs50.harvard.edu/x/psets/6/)

### [hello](https://cs50.harvard.edu/x/psets/6/hello/)

```
name = input("What is your name? ")  # Take input name from the user
# Greet user with hello alongside their name formatted into the string
print(f"hello, {name}")
```

### [mario-less](https://cs50.harvard.edu/x/psets/6/mario/less/)
```
from cs50 import get_int

while True:
    try:
        height = get_int("Height: ")
        # Check if height is within the allowed range (1-8)
        if 1 <= height <= 8:
            break
    except ValueError:
        # This catches non-numeric inputs like "foo" or ""
        pass


# Your optimized logic from before
for i in range(1, height + 1):
    print(" " * (height - i) + "#" * i)
```

### [mario-more](https://cs50.harvard.edu/x/psets/6/mario/more/)
```
from cs50 import get_int

while True:
    try:
        height = get_int("Height: ")
        # Check if height is within the allowed range (1-8)
        if 1 <= height <= 8:
            break
    except ValueError:
        # This catches non-numeric inputs like "foo" or ""
        pass

# Your optimized logic from before
for i in range(1, height + 1):
    print(" " * (height - i) + "#" * i + "  " + "#" * i)
```

### [cash](https://cs50.harvard.edu/x/psets/6/cash/)
```
from cs50 import get_float

# Loop until the user gives a non-negative float
while True:
    change = get_float("Change owed: ")
    if change >= 0:
        break

# Convert to cents
cents = round(change * 100)
coins = 0

# Calculate Quarters
coins += cents // 25
cents %= 25

# Calculate Dimes
coins += cents // 10
cents %= 10

# Calculate Nickels
coins += cents // 5
cents %= 5

# Calculate Pennies (whatever is left)
coins += cents

print(int(coins))
```

### [credit](https://cs50.harvard.edu/x/psets/6/credit/)
```
from cs50 import get_string
import re

# Prompt for input
s = get_string("Number: ")

# Checksum (Luhn's Algorithm)
total = 0
# Reverse the string to work from right to left
digits = s[::-1]

for i in range(len(digits)):
    d = int(digits[i])
    if i % 2 == 1:  # Every other digit, starting from the second-to-last
        product = d * 2
        total += (product // 10) + (product % 10)  # Add digits of product
    else:
        total += d

if total % 10 != 0:
    print("INVALID")
else:
    # Check AMEX - 15 digits, starts with 34 or 37
    if re.match(r"^3[47]\d{13}$", s):
        print("AMEX")
    # MASTERCARD - 16 digits, starts with 51, 52, 53, 54, or 55
    elif re.match(r"^5[1-5]\d{14}$", s):
        print("MASTERCARD")
    # VISA - 13 or 16 digits, starts with 4
    elif re.match(r"^4(\d{12}|\d{15})$", s):
        print("VISA")
    else:
        print("INVALID")
```

### [readability](https://cs50.harvard.edu/x/psets/6/readability/)
```
from cs50 import get_string

# Get input text from user
text = get_string("Text: ")

letters = 0
words = 1  # Assume at least one word as per your C logic
sentences = 0

# Iterate through each character in the text
for char in text:
    # Count letters (alphabetic only)
    if char.isalpha():
        letters += 1
    # Count words (based on spaces)
    elif char == " ":
        words += 1
    # Count sentences (based on ending punctuation)
    elif char in [".", "!", "?"]:
        sentences += 1

# L is average letters per 100 words
l = (letters / words) * 100
# S is average sentences per 100 words
s = (sentences / words) * 100

# Coleman-Liau index formula
index = (0.0588 * l) - (0.296 * s) - 15.8
grade = round(index)

# Output formatting
if grade < 1:
    print("Before Grade 1")
elif grade >= 16:
    print("Grade 16+")
else:
    print(f"Grade {grade}")
```

### [dna](https://cs50.harvard.edu/x/psets/6/dna/)
```
import csv
import sys


def main():

    # Check for command-line usage
    if len(sys.argv) != 3:
        print("Usage: python dna.py data.csv sequence.txt")
        sys.exit(1)

    # Read database file into a variable
    database = []
    with open(sys.argv[1], "r") as file:
        reader = csv.DictReader(file)
        # Store the STR names (column headers) for later use
        strs = reader.fieldnames[1:]
        for row in reader:
            database.append(row)

    # Read DNA sequence file into a variable
    with open(sys.argv[2], "r") as file:
        sequence = file.read()

    # Find longest match of each STR in DNA sequence
    results = {}
    for str_name in strs:
        results[str_name] = longest_match(sequence, str_name)

    # Check database for matching profiles
    for person in database:
        match = True
        for str_name in strs:
            # Compare the database value (as int) to our result
            if int(person[str_name]) != results[str_name]:
                match = False
                break

        if match:
            print(person["name"])
            return

    print("No match")
    return


def longest_match(sequence, subsequence):

    # Initialize variables
    longest_run = 0
    subsequence_length = len(subsequence)
    sequence_length = len(sequence)

    # Check each character in sequence for most consecutive runs of subsequence
    for i in range(sequence_length):

        # Initialize count of consecutive runs
        count = 0

        # Check for a subsequence match in a "substring" (a subset of characters) within sequence
        while True:

            # Adjust substring start and end
            start = i + count * subsequence_length
            end = start + subsequence_length

            # If there is a match in the substring
            if sequence[start:end] == subsequence:
                count += 1

            # If there is no match in the substring
            else:
                break

        # Update most consecutive matches found
        longest_run = max(longest_run, count)

    # After checking for runs at each character in sequence, return longest run found
    return longest_run


if __name__ == "__main__":
    main()
```
