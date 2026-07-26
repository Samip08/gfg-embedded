* datatype * pointer , we mention datatype to account for jumps when we do * (pointer+i), and also to ensure the compiler knows what data to retrieve from the pointer

[[void pointers]]

* Dereferencing a wild pointer(pointer been declared but never initialized with the memory location of variable) can cause program crashes, memory corruption, or unexpected results. hence always initialize with valid address or NULL


* int * ptr VS (int * )malloc(sizeof(int)) in the first case its just a wild pointer generated in stack, its loaded with whatever garbage address was left in stack, so dereferencing it or trying to change the value at that address is operations on garbage/other variables in code
* malloc assigns space in the heap, it allows u to completely control it, doesnt die out when the function ends , slow but accessible till you manually free the location


* dangling pointer refers to a pointer whose space has been freed already being used
* when the pointer gets freed before use or returned by a function , but the pointer dies as you exit the function

* constant pointer int * const ptr it points to a constant address, you cannot change once assigned

[[function pointer]]

[[multilevel pointers]]
[[Memory Management]]