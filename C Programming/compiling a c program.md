#### compiling and running a code in linux
1. using cc compiler: cc code.c           ./a.out
2. using gcc compiler:     cc -o executable code.c           ./executable

#### compiling and running a code in the terminal
1. MinGW(minimalist GNU): gcc filename.c -o filename.exe
* The -o allows specifying the output filename we want otherwise provides a.out
* -Wall enables the compiler warning messages 

#### compilation process of c programs
1.  preprocessing:
	*  removal of comments 
	*  expansion of macros( replace each macro instruction with the corresponding grp of source language instructions , like #define, other statements that are not in macro call are retained as were)
	*  [Macro Preprocessor](https://www.geeksforgeeks.org/compiler-design/macro-processor/)
	*  [Functions vs Macros](https://embetronicx.com/tutorials/p_language/c/preprocessor-in-c/)
	* expansion of included files
	* conditional compilation( static pass over the code to check conditional compilation directives like #if, #elif where the branches not taken are scrapped and not sent to compiler, does not evaluate a loop which as a define directive variable as parameter)
	* gcc -E filename.c -o filename.i

 2. compiling:
	 * converting a .i file into a .s file of assembly level instructions
	 * syntax checking for compilation time issues
	 * gcc -S filename.i -o filename.s

3. assembly:
	 * converting assembly lang code into machine lang code 
	 * only existing code is converted into machine language , function calls like printf() are not resolved 
	 * gcc -O filename.s -o filename.o

4. linking:
	* linking all function calls to their definitions , extra code to setup environment variables 
	* static linker: all code is copied to a single file and then the executable is formed, the executable has the function code and memory addresses are already calculated for function calls, IT FUCKING PUTS THE FUNCTION DEFINTION WHERE ITS NEEDED EACH AND EVERY TIME PAINFULLY
	* dynamic linker: only the name of the shared libraries are added to the code in the place of the functions you just put a placeholder telling it that there needs to be a function here
	* when you execute the code it does back to the dynamic linker which finds the memory address of the libs in the RAM and provides the function pointer instead of the placeholders
	* the linker provides all the compiled functions at a particular mem location in the final executable and when the call hits it jumps to that mem address
	* how does it pass different arguments each time, main function is responsible for putting the arguments into particular cpu registers/stack where is the function doesn't have hardcoded data, it reads these registers.
		
[[keywords]]