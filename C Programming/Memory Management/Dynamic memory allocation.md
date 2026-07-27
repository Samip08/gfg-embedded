* allocate, resize, and free memory at runtime
- Memory persists even after the function that allocated it finishes, allowing functions to return pointers to it. This is different from stack allocated variables as it is not safe to return address of those variable.

* realloc(): allows you to reallocate memory size to a previously allocated memory block, without needing to free the data
* ptr = (int * )realloc(ptr, 10 * sizeof(int));
* if realloc() fails and returns NULL, the original memory block is not freed, so you should not overwrite the original pointer until you've successfully allocated a new block.


* problems from dma:
1. failing to free dynamically allocated memory leads to memory leaks, exhausting system resources
2. using a pointer after it has been freed , causing undefined errors or crashes
3. Repeated allocations and deallocations can fragment memory, causing inefficient use of heap space.

[[memory leaks]]

[dynamically growing arrays](https://www.geeksforgeeks.org/c/dynamically-growing-array-in-c/)