![[Pasted image 20260710192611.png]]

* Text Segment: its the code segment , its read only to prevent overwriting code, stores executable code of the program, size of this part depends on the size of the code, contains the .text part of the assembly level code
* Data Segment: stores the static and global variables, variables in this segment retain their values throughout program exec, split into initialized and uninitialized(bss) segment
* Heap Segment: is used for dynamic allocation of memory , worked around with malloc(), realloc(),free()
* Stack Segment: contains local variables, function parameters, return addresses. Each function call creates a stack frame in this segment. when stack and heap meet free memory is over


[[Dynamic memory allocation]]