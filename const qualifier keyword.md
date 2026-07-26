* constants: value of this variable once declared cannot be redefined, protects variable from accidental modification(or limits modification to admin only) ex const int maxLoginAttempts = 3;
* initially stores garbage value present at that memory location, can also use #define to set constant values
* constants vs literals
constants once defined cannot be redefined, literals are fixed values that define themselves
constant is the constraint on the datatype, literal is the value stored inside them
we can find the address of a constant, but not a literal


* const vs define 
const is an immutable value, defined uses replacement of macros with values
constants are handled by a compiler, define is handled by the preprocessor