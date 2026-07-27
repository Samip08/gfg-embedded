* not just a function called in the definition of another function, but another function defined in a calling function, usually not supported by c compilers
* scope of this inner function is limited to the outer function so it can only be called in the outer function, but if the address of the inner function is passed to another external function it can be called via trampolines

#### Trampoline
small piece of code generated at runtime by GCC when the address of a nested function is taken
1. address of the actual nested function.
2. address of the enclosing function's stack frame.

#### Lexical scoping
* because via the trampoline the inner function still has access to the stack frame of the external function, thus it can use variables from the outer function
* inner function works properly only while the outer functions stack frame is active