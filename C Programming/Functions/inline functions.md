#### inline vs normal functions
* adding an inline constraint tells the compiler that this function is small/repetetive so instead of normal stack routine it must be copied directly in place of its call, usually when an inline function creates a local variable, it usually tries to use the cpu's general purpose registers, but incase they are not free it has to use the stack frame(less time overhead than normal functions)
 VS
 1. normal function call involves pushing the current instruction pointer to the stack, pushing the arguments onto the stack or the hardware registers, and take a screenshot of all the general registers to save main state 
 2. jumps to the address of the function definition, cannot use main mem so it has to cut down stack pointer to make a stack frame, performs the functions task
 3. places the return value into the required return register, frees the stack frame returning the pointer to the original location, pops the return address and the cpu goes back to the instruction pointer

* inline return_type function_name(parameters){  
	// function body  
  }


#### inline vs macros
* macros are like #define square x (x* x), this doesnt provide datatype safety its done by the preprocessor, while the inline is done by the complier and this gives very random errors which cannot be predicted or debugged
* macros are simply text substitution
