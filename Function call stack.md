* This is a runtime stack data structure, manages function calls and the order in which they are executed
* stores important values such as function parameters, local values and pointers to active functions
* LIFO principal the last called function executes the first


1. Stack Frame Creation
Stores the function arguments, local variables, and the return address.
Keeps all information related to a single function call together.

2. Function Execution
The stack pointer (SP) always points to the topmost stack frame.
Local variables and parameters remain available until the function completes.

3. Returning from the Function
After execution, the function returns control to the calling function
The current stack frame is removed (popped) from the call stack.
The stored return address is used to resume execution from the point where the function was called.