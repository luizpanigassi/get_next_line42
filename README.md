# get_next_line

This is the second project done for 42SP. It's a function that will read a document and return its content.

It's actually a pretty interesting project, focused on learning about memory allocation. In the regular function, it will read from a file and return it. On the bonus, it will do the same thing, but it will use a static variable to read from different file descriptors at the same time (and it's super easy to refactor it to do so). So, let's break down how the function operates.

If you check the code, you'll see that `get_next_line` will initialize the buffer if it doesn't exist, then read from the source file until it sees a `'\n'`, a linebreak. It will then extract this line using `ft_extract_line`, append it to the `receiver_buffer` using `strjoin`, then calculate the remainder of the text to be read using `ft_remainder`, which will then become the `receiver_buffer`. Lastly, it returns the line read, and the cycle starts again until the function reaches the end of the file. TADAAAAA!

## Features

- Read lines from a file descriptor one at a time.
- Handles files of any size.
- **Bonus:** Supports reading from multiple file descriptors simultaneously.

## Example Usage

Here’s a simple example of how to use `get_next_line`:

```c
#include "get_next_line.h"

int main(void)
{
    char *line;
    int fd;

    // Open the file for reading
    fd = open("text.txt", O_RDONLY);
    if (fd < 0)
    {
        perror("Error opening file");
        return (1);
    }

    // Read and print lines using get_next_line
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }

    // Close the file
    close(fd);
    return (0);
}
```

## File Structure

- `get_next_line.c` / `get_next_line.h`: Core implementation and header.
- `get_next_line_utils.c`: Utility functions for the core implementation.
- `get_next_line_bonus.c` / `get_next_line_bonus.h`: Bonus version supporting multiple file descriptors.
- `get_next_line_utils_bonus.c`: Utility functions for the bonus version.
- `main.c`: Example usage for reading from a single file.
- `main_bonus.c`: Example usage for reading from multiple files.

## Compilation

To compile the standard version:
```sh
gcc -Wall -Wextra -Werror get_next_line.c get_next_line_utils.c main.c -o gnl
```

To compile the bonus version:
```sh
gcc -Wall -Wextra -Werror get_next_line_bonus.c get_next_line_utils_bonus.c main_bonus.c -o gnl_bonus
```

## Running

```sh
./gnl
./gnl_bonus
```

---

Project by Luiz Panigassi
