# [Lecture 3](https://cs50.harvard.edu/x/weeks/3)

- There are many ways to solve a problem correct - algorithms
- However the design of solution can impact cost of solving a problem in terms of limited resources - time, storage, money, etc.
- An efficient algorithm is the one bringing down the cost of limited resource that cannot be compromised

### Searching
- As problem, we are given a set of values and are required to find a particular one
- Computers can access limited set of items at a time due to design constraints of memory
- Thus the location of required value is supposed to be found with operations and compute

*1. Linear Search - Checking each item available one by one and comparing with required value till it is found or end of set is reached*

*2. Binary Search - If the given set is sorted, divide it in half and compare for required value in middle. If according to sort order the required value is behind or in front ignore where it wouldn't be and repeat steps till value is found or end is reached.*

*Pseudo-coding such operations often help designing the program*

### Running Time
- Amount of time a algorithm takes to complete the task
- Often used to compare algorithms for consumed time in terms of required steps $n$ to execute
- To represent time in order of steps $n$, asymptotic notations are used such as - $O$ : Big O notation, and - $O(n)$: Big O of n, representing an upper bound
- When representing time in order of steps $n$, the focus is on dominant term influencing growth per step $n$ ignoring those that don't 
- Some algorithms may have different growth per step but eventually, they converge in terms of growth rate per step

### Structs
- User-defined custom data structure that associates each of it's instance with defined attributes encapsulated in its structure definition
- Instance declared as a variable with datatype
- `instance.attribute` helps accessing it's particular attribute

### Sorting
Done based on required order of values

*3. Selection Sort: Pass through whole set and order the set with least value on left till whole set is ordered least to largest*

*4. Bubble Sort: Pass through whole set comparing two items and swap the least of those to left and other to right till whole set is sorted*

### Recursion
- A recursive function is defined in terms of itself
- In mathematics it is dependent on itself
- In computer science it calls itself till a terminating condition is met called a base case
- Recursive cases divide the given problem so that solving till a base case is costing less and less computationally
- Each time a function calls itself it consumes more memory till a base case is reached

*5. Merge Sort: Reach base case of comparing two values and sort them, then merge the sorted entities and again sort per merge, eventually sorting the whole set*

# [Problem Set 3](https://cs50.harvard.edu/x/psets/3/)

### 1. [Sort](https://cs50.harvard.edu/x/psets/3/sort)

```
sort1 uses: Bubble Sort

How do you know?: In best case - sorted - performs the best with for all sizes of dataset, but performs the worst in average case - random - and worst case - reversed - where it has to do more number of comparisons and a pass to ensure everything is sorted.
sort2 uses: Merge Sort

How do you know?: No matter the arrangment of input, the time for execution is consistent with increasing input size.

sort3 uses: Selection Sort

How do you know?: performs bad at all sizes of datasets no matter the order.

```

### 2. [Plurality](https://cs50.harvard.edu/x/psets/3/plurality)

```
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// Candidates have name and vote count
typedef struct
{
    string name;
    int votes;
} candidate;

// Array of candidates
candidate candidates[MAX];

// Number of candidates
int candidate_count;

// Function prototypes
bool vote(string name);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: plurality [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
    }

    int voter_count = get_int("Number of voters: ");

    // Loop over all voters
    for (int i = 0; i < voter_count; i++)
    {
        string name = get_string("Vote: ");

        // Check for invalid vote
        if (!vote(name))
        {
            printf("Invalid vote.\n");
        }
    }

    // Display winner of election
    print_winner();
}

// Update vote totals given a new vote
bool vote(string name)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (!strcmp(candidates[i].name, name)) // check for candidate name
        {
            candidates[i].votes += 1;
            return true;
        }
    }
    return false;
}

// Print the winner (or winners) of the election
void print_winner(void)
{
    int max_vote = 0; // hold encountered maximum amount of votes
    // to check and update maximum amount of votes
    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes > max_vote)
        {
            max_vote = candidates[i].votes;
        }
    }
    // to print candidates with maximum amount of votes
    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes == max_vote)
        {
            printf("%s\n", candidates[i].name);
        }
    }
    return;
}

```

### 3. [Runoff](https://cs50.harvard.edu/x/psets/3/runoff)

```
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max voters and candidates
#define MAX_VOTERS 100
#define MAX_CANDIDATES 9

// preferences[i][j] is jth preference for voter i
int preferences[MAX_VOTERS][MAX_CANDIDATES];

// Candidates have name, vote count, eliminated status
typedef struct
{
    string name;
    int votes;
    bool eliminated;
} candidate;

// Array of candidates
candidate candidates[MAX_CANDIDATES];

// Numbers of voters and candidates
int voter_count;
int candidate_count;

// Function prototypes
bool vote(int voter, int rank, string name);
void tabulate(void);
bool print_winner(void);
int find_min(void);
bool is_tie(int min);
void eliminate(int min);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: runoff [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX_CANDIDATES)
    {
        printf("Maximum number of candidates is %i\n", MAX_CANDIDATES);
        return 2;
    }
    // initializes the candidates array with the names of the candidates provided as command-line arguments, sets their initial vote counts to zero, and marks them as not eliminated
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
        candidates[i].eliminated = false;
    }

    voter_count = get_int("Number of voters: ");
    if (voter_count > MAX_VOTERS)
    {
        printf("Maximum number of voters is %i\n", MAX_VOTERS);
        return 3;
    }

    // Keep querying for votes
    for (int i = 0; i < voter_count; i++)
    {

        // Query for each rank
        for (int j = 0; j < candidate_count; j++)
        {
            string name = get_string("Rank %i: ", j + 1);

            // Record vote, unless it's invalid
            if (!vote(i, j, name))
            {
                printf("Invalid vote.\n");
                return 4;
            }
        }

        printf("\n");
    }

    // Keep holding runoffs until winner exists
    while (true)
    {
        // Calculate votes given remaining candidates
        tabulate();

        // Check if election has been won
        bool won = print_winner();
        if (won)
        {
            break;
        }

        // Eliminate last-place candidates 
        int min = find_min();
        bool tie = is_tie(min);

        // If tie, everyone wins
        if (tie)
        {
            for (int i = 0; i < candidate_count; i++)
            {
                if (!candidates[i].eliminated)
                {
                    printf("%s\n", candidates[i].name);
                }
            }
            break;
        }

        // Eliminate anyone with minimum number of votes
        eliminate(min);

        // Reset vote counts back to zero
        for (int i = 0; i < candidate_count; i++)
        {
            candidates[i].votes = 0;
        }
    }
    return 0;
}

// Record preference if vote is valid
bool vote(int voter, int rank, string name)
{
    for (int i = 0; i < candidate_count; i++)
    {
        // compare candidate exists in candidates array
        if (!strcmp(candidates[i].name, name))
        {
            preferences[voter][rank] = i; // stores preferred candidate index in voter's rank preferences 2D array
            return true;
        }
    }
    return false;
}

// Tabulate votes for non-eliminated candidates
void tabulate(void)
{
    for (int i = 0; i < voter_count; i++)
    {
        for (int j = 0; j < candidate_count; j++)
        {
            if (!candidates[preferences[i][j]].eliminated)
            {
                candidates[preferences[i][j]].votes += 1; // accesses each voter's ranked preferences and increments vote count for the highest-ranked non-eliminated candidate
                break;                                    // stops checking further preferences for this voter after counting a vote for the first non-eliminated candidate
            }
        }
    }
    return;
}

// Print the winner of the election, if there is one
bool print_winner(void)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes > voter_count / 2)
        {
            printf("%s\n", candidates[i].name); // prints the name of the candidate who has more than half of the votes
            return true;
        }
    }
    return false;
}

// Return the minimum number of votes any remaining candidate has
int find_min(void)
{
    int min = voter_count;
    for (int i = 0; i < candidate_count; i++)
    {
        if (min > candidates[i].votes && !(candidates[i].eliminated))
        {
            min = candidates[i].votes; // iterates through candidates to find the smallest vote count among non-eliminated candidates and returns that minimum value
        }
    }
    return min;
}

// Return true if the election is tied between all candidates, false otherwise
bool is_tie(int min)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (!candidates[i].eliminated && candidates[i].votes > min) // checks if there is any non-eliminated candidate with a vote count greater than the minimum; if so, it returns false, indicating that not all candidates are tied
        {
            return false;
        }
    }
    return true;
}
// Eliminate the candidate (or candidates) in last place
void eliminate(int min)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes == min && !(candidates[i].eliminated))
        {
            candidates[i].eliminated = true; // iterates through candidates and eliminates any candidate whose vote count is equal to the minimum by setting their eliminated status to true
        }
    }
    return;
}
```

### 4. [Tidemann](https://cs50.harvard.edu/x/psets/3/tidemann)

```
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// preferences[i][j] is number of voters who prefer i over j
int preferences[MAX][MAX];
// structured as - if preferences[i][j] is 5, then 5 voters prefer candidate i over candidate j similarly for each candidate pair possible out of the candidate_count candidates

// locked[i][j] means i is locked in over j
bool locked[MAX][MAX];
// structured as - if locked[i][j] is true, ; locked[j][i] must be false, and if locked[i][j] is false, locked[j][i] can be either true or false

// Each pair has a winner, loser
typedef struct
{
    int winner;
    int loser;
} pair;

// Array of candidates
string candidates[MAX];
pair pairs[MAX * (MAX - 1) / 2];

int pair_count;
int candidate_count;

// Function prototypes
bool vote(int rank, string name, int ranks[]);
void record_preferences(int ranks[]);
void add_pairs(void);
void sort_pairs(void);
void lock_pairs(void);
void print_winner(void);

// helper function
bool has_cycle(int winner, int loser);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: tideman [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i] = argv[i + 1];
    }

    // Clear graph of locked in pairs
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = 0; j < candidate_count; j++)
        {
            locked[i][j] = false;
        }
    }

    pair_count = 0;
    int voter_count = get_int("Number of voters: ");

    // Query for votes
    for (int i = 0; i < voter_count; i++)
    {
        // ranks[i] is voter's ith preference
        int ranks[candidate_count];

        // Query for each rank
        for (int j = 0; j < candidate_count; j++)
        {
            string name = get_string("Rank %i: ", j + 1);

            if (!vote(j, name, ranks))
            {
                printf("Invalid vote.\n");
                return 3;
            }
        }

        record_preferences(ranks);

        printf("\n");
    }

    add_pairs();
    sort_pairs();
    lock_pairs();
    print_winner();
    return 0;
}

// Update ranks given a new vote
bool vote(int rank, string name, int ranks[])
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (!strcmp(candidates[i], name))
        {
            ranks[rank] = i;
            return true;
        }
    }
    return false;
}

// Update preferences given one voter's ranks
void record_preferences(int ranks[])
{
    for (int i = 0; i < candidate_count; i++) // Loop through each candidate in the voter's ranks
    {
        for (int j = i + 1; j < candidate_count; j++) // Loop through candidates ranked lower than the current candidate
        {
            preferences[ranks[i]][ranks[j]]++; // Increment the count of voters who prefer candidate ranks[i] over ranks[j]
        }
    }
    return;
}

// Record pairs of candidates where one is preferred over the other
void add_pairs(void)
{
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = i + 1; j < candidate_count; j++)
        {
            // If more voters prefer candidate i over candidate j, add i as winner and j as loser
            if (preferences[i][j] > preferences[j][i])
            {
                pairs[pair_count].winner = i;
                pairs[pair_count].loser = j;
                pair_count++;
            }
            // If more voters prefer candidate j over candidate i, add j as winner and i as loser
            else if (preferences[j][i] > preferences[i][j])
            {
                pairs[pair_count].winner = j;
                pairs[pair_count].loser = i;
                pair_count++;
            }
        }
    }
    return;
}

// Sort pairs in decreasing order by strength of victory (selection sort)
void sort_pairs(void)
{
    for (int i = 0; i < pair_count - 1; i++)
    {
        int max_idx = i;
        // Find the index of the pair with the greatest strength of victory
        for (int j = i + 1; j < pair_count; j++)
        {
            if (preferences[pairs[j].winner][pairs[j].loser] >
                preferences[pairs[max_idx].winner][pairs[max_idx].loser])
            {
                max_idx = j;
            }
        }
        // Swap the pair at index i with the pair at index max_idx
        pair temp = pairs[max_idx];
        pairs[max_idx] = pairs[i];
        pairs[i] = temp;
    }
    return;
}

// Lock pairs into the candidate graph in order, without creating cycles
void lock_pairs(void)
{
    for (int i = 0; i < pair_count; i++)
    {
        if (!has_cycle(pairs[i].winner, pairs[i].loser))
        {
            locked[pairs[i].winner][pairs[i].loser] = true; // map the winner to the loser in the locked graph
        }
    }
    return;
}

// Print the winner of the election
void print_winner(void)
{
    for (int i = 0; i < candidate_count; i++) 
    {
        bool is_loser = false;
        for (int j = 0; j < candidate_count; j++)
        {
            if (locked[j][i]) // If there is a locked pair from j to i, then i is a loser
            {
                is_loser = true;
                break;
            }
        }

        if (!is_loser)
        {
            printf("%s\n", candidates[i]); // Candidate with no incoming edges is the winner
            return;
        }
    }
}

bool has_cycle(int winner, int loser)
{
    if (loser == winner)
    {
        return true; // cycle detected
    }
    for (int i = 0; i < candidate_count; i++)
    {
        if (locked[loser][i]) // If there is a locked pair from loser to i
        {
            if (has_cycle(winner, i)) // Recursively check if there is a path from i back to winner
            {
                return true; 
            }
        }
    }
    return false;
}
```