# [Lecture 5](https://cs50.harvard.edu/x/weeks/5)

- Data structures are also termed abstract datatypes
- Differ by what characterstics, functions they of regardless of lower level implementations
- **Queue:** A First-In-First-Out(FIFO)
    - First object in is first object out
    - Enqueue: Add to the end of the queue
    - Dequeue: remove from the front of the queue
- **Stack:** A Last-In-First-Out(LIFO)
    - Last object in is first object out
    - Push: Add on top of stack
    - Pop: Delete from top of stack
- **Dictionaries:**
    - Holds a *key-value* pair
    - Associates one piece of data to another piece of data
    - Like a word and it's definition

### Resizing Array and `realloc()`

- Generally, arrays are predefined in a program thus allocating a contiguous set of memory
- This allocates a static memory chunk to array
- `malloc(size)` can be used to allocate a chunk of memory and address it's address to a pointer
- Values can also be assigned to this array with syntax `*(chunk + index) = value`
- And again with `malloc(size)` can be used to allocate a bigger chunk and copy original array to it with added memory
- `realloc(chunk, size)` abstracts away the copying part and reallocate the memory for array with original data in chunk
- Even so it requires a temporary pointer to store addresses of original chunk and reallocated chunk

### Linked Lists

- No matter where the values are in memory, connecting them would make it contiguous
- Values can be allocated memory using `malloc()` but allocation per value is not necessarily contiguous
- To connect these values, memory can be allocated for a pointer to next chunk of allocation along side current value with `malloc()`
- A `struct` definition of such structure can be:
    ```
    typedef struct node
    {
        int value;
        struct node *next;
    }node;
    ```
    where node is a unit of it
- When setting values in members of this structure for a instance at n,
    - General method is: `(*n).value` / `(*n).next` - go to address of that node and update the fields
    - In C syntax simplifies it as `n->value` / `n->next`

*Linked lists with two pointers for forward and backward traversal are called doubly linked list*

### Trees
-  A node is a unit of it with pointers leading to two of it's child nodes
- Parent node is the one having a pointer leading to next node, the next node is child node
- First node in the tree is the root node 
- With each node having two childs, those with none at the end are the leaf nodes
- *Binary Search Tree* has the property: Left node < Root node < Right node

### Hashing
- Mapping a finite or infinite domain of values to a fintite range of values
- Bucketizes values into finite number of buckets where those should belong
- A hash function determines the value of data based on which it get bucketized

### Hash Tables
- Associates a piece of data with another using hash function which outputs index for input value
- Like the *key-value* pair logic of dictionaries, hash table have such pairs stored for data retrieval
- Helpful for data retrieval operations with constant time complexity for insertion, deletion and search

### Tries
- Store strings through character arrays connected as linked lists
- Common prefixes are shared among strings with breakpoints determined by null pointers
- Takes up space - bad for small datasets, effective for big ones reaching constant time complexity

# [Problem Set 5](https://cs50.harvard.edu/x/psets/5)

### [inheritance](https://cs50.harvard.edu/x/psets/5/inheritance)

```
// Simulate genetic inheritance of blood type
#define _DEFAULT_SOURCE
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Each person has two parents and two alleles
typedef struct person
{
    struct person *parents[2];
    char alleles[2];
} person;

const int GENERATIONS = 3;
const int INDENT_LENGTH = 4;

person *create_family(int generations);
void print_family(person *p, int generation);
void free_family(person *p);
char random_allele();

int main(void)
{
    // Seed random number generator
    srandom(time(0));

    // Create a new family with three generations
    person *p = create_family(GENERATIONS);

    // Print family tree of blood types
    print_family(p, 0);

    // Free memory
    free_family(p);
}

// Create a new individual with `generations`
person *create_family(int generations)
{
    // Allocate memory for new person
    person *current = malloc(sizeof(person));

    // If there are still generations left to create
    if (generations > 1)
    {
        // Create two new parents for current person by recursively calling create_family
        person *parent0 = create_family(generations - 1);
        person *parent1 = create_family(generations - 1);

        // Set parent pointers for current person
        current->parents[0] = parent0;
        current->parents[1] = parent1;

        // Randomly assign current person's alleles based on the alleles of their parents
        current->alleles[0] = parent0->alleles[random() % 2];
        current->alleles[1] = parent1->alleles[random() % 2];
    }

    // If there are no generations left to create
    else
    {
        // Set parent pointers to NULL
        current->parents[0] = NULL;
        current->parents[1] = NULL;

        // Randomly assign alleles
        current->alleles[0] = random_allele();
        current->alleles[1] = random_allele();
    }

    // Return newly created person
    return current;
}

// Free `p` and all ancestors of `p`.
void free_family(person *p)
{
    // Handle base case
    if (p == NULL)
    {
        return;
    }

    // Free parents recursively
    free_family(p->parents[0]);
    free_family(p->parents[1]);

    // Free child
    free(p);
}

// Print each family member and their alleles.
void print_family(person *p, int generation)
{
    // Handle base case
    if (p == NULL)
    {
        return;
    }

    // Print indentation
    for (int i = 0; i < generation * INDENT_LENGTH; i++)
    {
        printf(" ");
    }

    // Print person
    if (generation == 0)
    {
        printf("Child (Generation %i): blood type %c%c\n", generation, p->alleles[0],
               p->alleles[1]);
    }
    else if (generation == 1)
    {
        printf("Parent (Generation %i): blood type %c%c\n", generation, p->alleles[0],
               p->alleles[1]);
    }
    else
    {
        for (int i = 0; i < generation - 2; i++)
        {
            printf("Great-");
        }
        printf("Grandparent (Generation %i): blood type %c%c\n", generation, p->alleles[0],
               p->alleles[1]);
    }

    // Print parents of current generation
    print_family(p->parents[0], generation + 1);
    print_family(p->parents[1], generation + 1);
}

// Randomly chooses a blood type allele.
char random_allele()
{
    int r = random() % 3;
    if (r == 0)
    {
        return 'A';
    }
    else if (r == 1)
    {
        return 'B';
    }
    else
    {
        return 'O';
    }
}
```

### [speller](https://cs50.harvard.edu/x/psets/5/speller)
```
// Implements a dictionary's functionality
#include <ctype.h>
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <strings.h>

#include "dictionary.h"

// Represents a node in a hash table
typedef struct node
{
    char word[LENGTH + 1];
    struct node *next;
} node;

// TODO: Choose number of buckets in hash table
// Using a power of 2 (2^16) for a balance between memory and speed
const unsigned int N = 65536;

// Hash table: an array of pointers to nodes
node *table[N];

// Global variable to keep track of words in the dictionary for size()
unsigned int word_count = 0;

// Returns true if word is in dictionary, else false
bool check(const char *word)
{
    // Hash the input word to find it's index in hash table
    unsigned int index = hash(word);

    // Create a cursor pointer to traverse linked list for the word from the index
    node *cursor = table[index];

    while (cursor != NULL)
    {
        // Compare the search word with the word in the current node using `strcasecmp()` to handle case sensitivity
        if (strcasecmp(word, cursor->word) == 0)
        {
            return true;
        }
        
        // Move the cursor to the next node in the list
        cursor = cursor->next;
    }

    // If we reach the end without finding the word
    return false;
}

// Improved hash function: Weighted sum of characters
unsigned int hash(const char *word)
{
    unsigned int value = 0;

    for (int i = 0; word[i] != '\0'; i++) // With each character in word
    {

        value = (value * 31) + tolower(word[i]); // Hash value is calculated as sum of ASCII value of character multiplied by 31
                                                 // Sequence of characters changes final value drastically
                                                 // Prime numbers like 31 minimize word collisions by treating word value as a Base-31 value system
    }

    // Restrict value to hash table size
    return value % N;
}

// Loads dictionary into memory, returning true if successful, else false
bool load(const char *dictionary)
{
    // Open the dictionary file for reading
    FILE *source = fopen(dictionary, "r");
    if (source == NULL)
    {
        return false;
    }

    // Buffer to store the current word being read
    char word[LENGTH + 1];

    // Read every string from the file one by one until EOF(End Of File)
    while (fscanf(source, "%s", word) != EOF)
    {
        // Create a new node for each word
        node *n = malloc(sizeof(node));
        
        if (n == NULL) // No memory allocated to node address
        {
            // Halt all operations
            fclose(source);
            return false;
        }

        // Copy the read word into the new node's word array
        strcpy(n->word, word);

        // Determine which bucket this word belongs to with hash function
        unsigned int index = hash(word);

        n->next = table[index]; // Set next node at bucket to current node's next in list
        table[index] = n;       // Current node set as head at hashed index in table

        // Increment the global count of words
        word_count++;
    }

    // Close the file and return success
    fclose(source);
    return true;
}

// Returns number of words in dictionary if loaded, else 0 if not yet loaded
unsigned int size(void)
{
    // Simply return the global counter updated during load()
    return word_count;
}

// Unloads dictionary from memory
bool unload(void)
{
    // Iterate through every bucket in the hash table array
    for (int i = 0; i < N; i++)
    {
        // Set a cursor to the start of the linked list in this bucket
        node *cursor = table[i];

        // Traverse the linked list and free every node
        while (cursor != NULL)
        {
            node *tmp = cursor;    // Store address of current node temporarily
            cursor = cursor->next; // Move cursor to next node first
            free(tmp);             // Now safe to free the current node
        }
    }

    return true;
}
```