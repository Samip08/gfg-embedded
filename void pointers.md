* void * ptr  can refer to the address of any datatype, however to dereference you must specify datatype, usually used in generic functions and memory management routines where the data type is not known in advance.    
* printf("%d", * (int* )ptr);     for dereferencing it need to specify 
* pointer arithmetic is usually not allowed on void pointers because skip width not known but some compilers treat it like 1 byte/char and continue, normal gcc works like that
* Void pointers enable functions to work with multiple data types. For example, the comparison function used by qsort() accepts void pointers.
*  data structures such as linked lists, stacks, queues, and trees use void pointers to store elements of different types