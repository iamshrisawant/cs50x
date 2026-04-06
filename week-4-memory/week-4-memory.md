# [Lecture 4](https://cs50.harvard.edu/x/weeks/4)

- Digital pictures are also stored in representations of zeroes and ones
- The units of these representations are pixels which collectively for up the image to display
- More the pixels better the details in picture captured

### Hexadecimal
- An extension to decimal where 10 to 15 are reprerented with a to f, making it a total of 16 digit system
- Requires 4 bits to represent a digit in hexadecimal
- Commonly used in representation of colours in images, memory adresses, etc.

### Memory
- For ease of representation, memory addresses are represented with hexadecimal system
- It allows to represent a byte with two hexadecimal digit instead of eight independent bits
- In memory `0x` is used as prefix to indicate what follows it is a address

### Pointers
- Pointer is a variable that stores address of another variable or value in memory
- In C, program with memory access specifically:
  - `&`(Reference Operator): Accesses the address of variable in code alongside it
  - `*`(Dereference Operator): Defines a pointer variable to store address of declared datatype
  - `%p`: Specifically used to scan or print an address of a variable
- Only a pointer variable of declared datatype can hold address of variable of same datatype or access value at address it holds
- Pointer size may vary per platform - 8 bytes for 64 bit platform, 4 bytes for 32 bit platform
- Represented with arrows in memory from blocks that hold address of block holding value

### Strings
- Strings are basically an array of `char` datatype units which are addressable stored contiguously
- `string` is defined as `char *`, a pointer to first character in memory
- The declared variable holds the address of beginning of the string and `\0` holds where string ends
- If we compare `strng` variables directly the addresses of first `char`s in are compared instead of contents
- Thus `strcmp` accesses the values at the address to compare each `char` in string iteratively
- Normal equation of `string`s would only copy address in RHS to LHS
- Two functions help with memory operations well:
  - `malloc` allocates memory equivalent to passed argument and passes address of first block to it's variable
  - `free` takes that same address value to free the allocated space

### valgrind
- Aids to debug memory related errors
- Outputs a insignt into program's memory usage
- Usually verbose to read but helps with retaining most of memory alocated to the program

- *Pointers are declared with deference operators which intially do not point to anything, called null pointers(`nullptr`)*
- *Pointee is the value a pointer points at*
- *`*` helps with dereferencing the address, `&` helps with accessing the address, where as a plain variable declared with `*` is supposed to hold an address*

### Pointer Arithmetic
- Address or pointers are basically numbers, thus can be operated upon with arithmetics
- To access continuous blocks in memory same similarly to that of an array
- We simply add/subtract integers from variables holding address to point to required blocks

- Memory is assigned in a deliberate way:
  - The top of the memory usually holds machine code
  - Then come the global values, variables which are defined outside of `main()`
  - Then from top to bottom is **heap** which is growing allocation of memory using malloc
  - At the bottom is **stack** which allocation of memory per call of function for it's local variables growing upwards
- In this model, eventually, continuous allocation of memory would make **heap** and **stack** clash with each other causing a overflow
  - Stack Overflow: When program tries to access memory beyond it's call stack
  - Heap Overflow: A kind of Buffer Overflow, when program tries to write data more than the allocated buffer heap can hold
- Use of pointers can significantly make programs more efficient with thoughtful operations over memory

### scanf
- Normally used to scan or take input in program instead of using cs50's `get_int`, `get_string`, etc.
- Requires use of `&` to access variable's address while assigning input value to the address in case of variables
- Strings or arrays however which already have declaration of first value address stored in pointer do not require use of `&` as variable itself holds address

### File I/O
- Files are entities storing data residing in Solid State Drives or Random Access Memeory based on requirement.
- fopen(): Opens and file and returns it's  file pointer - address to first it's first byte, requires a file access mode - `r` as read, `w` as write and `a` as append
- fclose(): Closes an open file and ensures all data is saved to disk and flushed from memory
- fprint(): Prints formatted text to file
- fscanf(): Reads formatted data until it hits whitespaces
- fread(): Reads binaries in the form of chunks directly into a buffer in memory
- fwrite(): Writes to a block of binary data from memory to file
- fseek(): Allows to navigate in file by moving cursor over blocks without reading sequentially
- Pointer aids in file I/O by directly operating over files in the form of bytes

# [Problem Set 4](https://cs50.harvard.edu/x/psets/4/)

### [volume](https://cs50.harvard.edu/x/psets/4/volume/)
```
// Modifies the volume of an audio file

#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

// Number of bytes in .wav header
const int HEADER_SIZE = 44;

int main(int argc, char *argv[])
{
    // Check command-line arguments
    if (argc != 4)
    {
        printf("Usage: ./volume input.wav output.wav factor\n"); // Take three arguments - input file, output file, factor to change volume by
        return 1;
    }

    // Open files and determine scaling factor
    FILE *input = fopen(argv[1], "r"); // reading input file
    if (input == NULL)
    {
        printf("Could not open file.\n");
        return 1;
    }

    FILE *output = fopen(argv[2], "w"); // writing to output file
    if (output == NULL)
    {
        printf("Could not open file.\n");
        return 1;
    }

    float factor = atof(argv[3]); // storing factor for operations

    // PSET: Copy header from input file to output file
    // unit8_t is a unsigned integer datatype that can hold a 8 bit number, that is a byte
    uint8_t buffer[HEADER_SIZE]; // Create a byte buffer to hold the header of file

    fread(buffer, sizeof(uint8_t), HEADER_SIZE, input);   // Read a byte at a time from input file header
    fwrite(buffer, sizeof(uint8_t), HEADER_SIZE, output); // Write a byte at a time to ouput file header

    // PSET: Read samples from input file and write updated data to output file
    // int16_t is a signed datatype that can hold a 16 bit number both negatives and positives
    int16_t sample; // Every sample in audio file has a size of 16 bits

    while (fread(&sample, sizeof(int16_t), 1, input) ==
           1) // while program can read a sample from file
    {
        sample = sample * factor;                    // factor the sample to scale it's volume
        fwrite(&sample, sizeof(int16_t), 1, output); // write the modified sample to ouput file
    }

    // Close files
    fclose(input);
    fclose(output);
}
```

### [filter-less](https://cs50.harvard.edu/x/psets/4/filter/less)

```
// Helper for main filter.c file to outsource filters logic

#include "helpers.h" //Define function signatures of helper.c
#include <math.h>

// Convert image to grayscale
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++) // Iterate per row of pixels of image
    {
        for (int j = 0; j < width; j++) // Iterate per column
        {
            float average =
                (image[i][j].rgbtRed + image[i][j].rgbtGreen + image[i][j].rgbtBlue) / 3.0; // Average of all values in RGB
            int result = round(average);

            // Define the shade of grey - R = G = B = Average, to keep brightness consistency
            image[i][j].rgbtRed = result;
            image[i][j].rgbtGreen = result;
            image[i][j].rgbtBlue = result;
        }
    }
    return;
}

// Convert image to sepia
void sepia(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Calculate sepia values as floats
            float sepiaRed = .393 * image[i][j].rgbtRed + .769 * image[i][j].rgbtGreen +
                             .189 * image[i][j].rgbtBlue;
            float sepiaGreen = .349 * image[i][j].rgbtRed + .686 * image[i][j].rgbtGreen +
                               .168 * image[i][j].rgbtBlue;
            float sepiaBlue = .272 * image[i][j].rgbtRed + .534 * image[i][j].rgbtGreen +
                              .131 * image[i][j].rgbtBlue;

            // Round the results of calculated values to be integers
            int totalRed = round(sepiaRed);
            int totalGreen = round(sepiaGreen);
            int totalBlue = round(sepiaBlue);

            // Cap the values at 255 as a pixel can show 0 to 255 shades per colour
            image[i][j].rgbtRed = (totalRed > 255) ? 255 : totalRed;
            image[i][j].rgbtGreen = (totalGreen > 255) ? 255 : totalGreen;
            image[i][j].rgbtBlue = (totalBlue > 255) ? 255 : totalBlue;
        }
    }
    return;
}

// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        // Loop only to the halfway point
        for (int j = 0; j < width / 2; j++)
        {
            // Store the left pixel in a temporary variable
            RGBTRIPLE temp = image[i][j];

            // Move the right pixel into the left position
            image[i][j] = image[i][width - 1 - j]; // Since opposite index for j = 0 is one less than total width in array
                                                      and so on for all j values as j increments

            // Move the temporary (original left) pixel into the right position
            image[i][width - 1 - j] = temp;
        }
    }
    return;
}

// Blur image
void blur(int height, int width, RGBTRIPLE image[height][width])
{
    // Creating a reference image
    RGBTRIPLE copy[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            copy[i][j] = image[i][j];
        }
    }

    // Start iterating over image
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            float sumRed = 0, sumGreen = 0, sumBlue = 0; // Accumulators of colours
            int counter = 0;

            // Look at the 3x3 neighbourhood with r by c kernel moving from -1 to 0 to 1
            for (int r = -1; r <= 1; r++)
            {
                for (int c = -1; c <= 1; c++)
                {
                    // Current pixel's neighbouring pixel in 3x3
                    int neighborRow = i + r; 
                    int neighborCol = j + c;

                    // Check if neighbour is valid (within image bounds)
                    if (neighborRow >= 0 && neighborRow < height && neighborCol >= 0 &&
                        neighborCol < width)
                    {
                        // Sum of intensities of each colour in 3x3 neighbourhood from reference image
                        sumRed += copy[neighborRow][neighborCol].rgbtRed;
                        sumGreen += copy[neighborRow][neighborCol].rgbtGreen;
                        sumBlue += copy[neighborRow][neighborCol].rgbtBlue;

                        // Keep a count of pixels
                        counter++;
                    }
                }
            }

            // Calculate average and update actual image
            image[i][j].rgbtRed = round(sumRed / counter);
            image[i][j].rgbtGreen = round(sumGreen / counter);
            image[i][j].rgbtBlue = round(sumBlue / counter);
        }
    }
    return;
}
```

### [filter-more](https://cs50.harvard.edu/x/psets/4/filter/less)
```
// Helper for main filter.c file to outsource filters logic

#include "helpers.h" //Define function signatures of helper.c
#include <math.h>

// Convert image to grayscale
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++) // Iterate per row of pixels of image
    {
        for (int j = 0; j < width; j++) // Iterate per column
        {
            float average =
                (image[i][j].rgbtRed + image[i][j].rgbtGreen + image[i][j].rgbtBlue) / 3.0; // Average of all values in RGB
            int result = round(average);

            // Define the shade of grey - R = G = B = Average, to keep brightness consistency
            image[i][j].rgbtRed = result;
            image[i][j].rgbtGreen = result;
            image[i][j].rgbtBlue = result;
        }
    }
    return;
}

// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        // Loop only to the halfway point
        for (int j = 0; j < width / 2; j++)
        {
            // Store the left pixel in a temporary variable
            RGBTRIPLE temp = image[i][j];

            // Move the right pixel into the left position
            image[i][j] = image[i][width - 1 - j]; // Since opposite index for j = 0 is one less than total width in array
                                                      and so on for all j values as j increments

            // Move the temporary (original left) pixel into the right position
            image[i][width - 1 - j] = temp;
        }
    }
    return;
}

// Blur image
void blur(int height, int width, RGBTRIPLE image[height][width])
{
    // Creating a reference image
    RGBTRIPLE copy[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            copy[i][j] = image[i][j];
        }
    }

    // Start iterating over image
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            float sumRed = 0, sumGreen = 0, sumBlue = 0; // Accumulators of colours
            int counter = 0;

            // Look at the 3x3 neighbourhood with r by c kernel moving from -1 to 0 to 1
            for (int r = -1; r <= 1; r++)
            {
                for (int c = -1; c <= 1; c++)
                {
                    // Current pixel's neighbouring pixel in 3x3
                    int neighborRow = i + r; 
                    int neighborCol = j + c;

                    // Check if neighbour is valid (within image bounds)
                    if (neighborRow >= 0 && neighborRow < height && neighborCol >= 0 &&
                        neighborCol < width)
                    {
                        // Sum of intensities of each colour in 3x3 neighbourhood from reference image
                        sumRed += copy[neighborRow][neighborCol].rgbtRed;
                        sumGreen += copy[neighborRow][neighborCol].rgbtGreen;
                        sumBlue += copy[neighborRow][neighborCol].rgbtBlue;

                        // Keep a count of pixels
                        counter++;
                    }
                }
            }

            // Calculate average and update actual image
            image[i][j].rgbtRed = round(sumRed / counter);
            image[i][j].rgbtGreen = round(sumGreen / counter);
            image[i][j].rgbtBlue = round(sumBlue / counter);
        }
    }
    return;
}

// Detect edges
void edges(int height, int width, RGBTRIPLE image[height][width])
{
    // Create a reference image
    RGBTRIPLE copy[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            copy[i][j] = image[i][j];
        }
    }

    // Define Sobel kernels
    int Gx[3][3] = {{-1, 0, 1}, {-2, 0, 2}, {-1, 0, 1}};

    int Gy[3][3] = {{-1, -2, -1}, {0, 0, 0}, {1, 2, 1}};

    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            float GxR = 0, GxG = 0, GxB = 0;
            float GyR = 0, GyG = 0, GyB = 0;

            // Iterate through the 3x3 neighborhood
            for (int r = -1; r <= 1; r++)
            {
                for (int c = -1; c <= 1; c++)
                {
                    int row = i + r;
                    int col = j + c;

                    // If pixel is within bounds, add its weighted value
                    // If out of bounds, it's treated as 0 (black), so we do nothing
                    if (row >= 0 && row < height && col >= 0 && col < width)
                    {
                        // Weighted values of each colour in reference image over sobel kernel
                        GxR += copy[row][col].rgbtRed * Gx[r + 1][c + 1];
                        GxG += copy[row][col].rgbtGreen * Gx[r + 1][c + 1];
                        GxB += copy[row][col].rgbtBlue * Gx[r + 1][c + 1];

                        GyR += copy[row][col].rgbtRed * Gy[r + 1][c + 1];
                        GyG += copy[row][col].rgbtGreen * Gy[r + 1][c + 1];
                        GyB += copy[row][col].rgbtBlue * Gy[r + 1][c + 1];
                    }
                }
            }

            // Combine Gx and Gy results
            int red = round(sqrt(GxR * GxR + GyR * GyR));
            int green = round(sqrt(GxG * GxG + GyG * GyG));
            int blue = round(sqrt(GxB * GxB + GyB * GyB));

            // Cap at 255
            image[i][j].rgbtRed = (red > 255) ? 255 : red;
            image[i][j].rgbtGreen = (green > 255) ? 255 : green;
            image[i][j].rgbtBlue = (blue > 255) ? 255 : blue;
        }
    }
    return;
}
```

### [recover](https://cs50.harvard.edu/x/psets/4/filter/less)

```
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

// Define a byte for easier buffer management
typedef uint8_t BYTE;

int main(int argc, char *argv[])
{
    // Ensure correct usage
    if (argc != 2)
    {
        printf("Usage: ./recover IMAGE\n");
        return 1;
    }

    // Open the forensic image (memory card)
    FILE *input_file = fopen(argv[1], "r");
    if (input_file == NULL)
    {
        printf("Could not open file %s.\n", argv[1]);
        return 1;
    }

    // Buffer to store a 512-byte block
    BYTE buffer[512];

    // Variables to track the output JPEGs
    FILE *output_file = NULL;
    char filename[8]; // Enough for "###.jpg\0"
    int image_count = 0;

    // Read the memory card block by block (512 bytes each)
    while (fread(buffer, 1, 512, input_file) == 512)
    {
        // Check if the current block is the start of a new JPEG
        if (buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff &&
            (buffer[3] & 0xf0) == 0xe0)
        {
            // If we were already writing to a file, close it
            if (output_file != NULL)
            {
                fclose(output_file);
            }

            // Create a name for the new file (e.g., 000.jpg)
            sprintf(filename, "%03i.jpg", image_count);
            output_file = fopen(filename, "w");
            image_count++;
        }

        // If an output file is currently open, write the block to it
        if (output_file != NULL)
        {
            fwrite(buffer, 1, 512, output_file);
        }
    }

    // Close any remaining open files
    if (output_file != NULL)
    {
        fclose(output_file);
    }
    fclose(input_file);

    return 0;
}
```

##### Questions

- volume
  1. uint8_t
  2. int16_t
  3. factor multiplication in float and int16_t datatype
- filter-less
  1. getopt() in filter.c
  2. optind in filter.c
  3. BTMAPFILEHEADER, BITMAPINFOHEADER RGBTRIPLE, SEEK_CUR, calloc
  4. How bitmap was read to convert it to a image[height][width] array?
- filter-more: How sobel kernel works?
- recover: How come recover has one raw file and we have iterate for jpegs?
