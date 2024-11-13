# get_next_line
This is the second project done for 42SP. It's a function that will read a document and return its content.

It's actually a pretty interesting project, focused on learning about memory allocation.
In the regular function, it will read from a file, and return it. On the bonus, it will do
the same thing, but it will use the static variable to read from different file descriptors at
the same time (and it's super easy to refactor it to do so). So, let's break down how the function operates.

So, if you check the code, you'll see that get_next_line will initialize the buffer if it doesn't exist,
then read from the source file until it sees a '\n', a linebreak. It will then extract this line using
ft_extract_line, append it to the receiver_buffer using strjoin, then calculate the remainder of the text to be
read using ft_remainder, which will then become the receiver_buffer. Lastly, it returns the line read, and the cycle
starts again until the function reaches the end of the file. TADAAAAA!
