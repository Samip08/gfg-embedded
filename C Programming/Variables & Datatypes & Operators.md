* variables are used to remove necessity of remembering memory addresses
* when a variable is declared compiler knows that the variable of given name and type exists but actual memory is only allocated at definition( int x; vs x=43;)

* datatype matters as it tells the compiler how to look at the contiguous values starting at the variable's memory address
* thus functions like printf, scanf require format specifiers, saying value starts at this address, and is of this length, treat it of this datatype, this even determines operators for it
* so even if you inherently have an int, char it sees only the memory addresses of these variables, so its not a fixed datatype until you declare how you want it to act
* datatypes are 3 mainly: basic, derived(float, boolean), user defined(arr, struct, enums)

format specifier for printf, scanf
 1. A minus(-) sign tells left alignment.
2. A number after ****%**** specifies the minimum field width to be printed if the characters are less than the size of the width the remaining space is filled with space and if it is greater then it is printed as it is without truncation.
3. A period( . ) symbol separates field width with precision.
printf("%-20.5s\n", str);


* operators: arithemetic, relational( >=, == , <=) , logical(&, |)  , bitwise(&&, ||, ^,~) , assignment( = , +=, -=, *=, /=, %=, &=, |=, ^=, >>, <<) , address/dereference(&,*)
* getchar, putchar, scanf, printf all have return types of int, returns the number of characters operated on
* printf("%d", printf("%d", b)) where b =1234 gives 12344, first evaluated print from printf then return value of printf, the number of characters printed
* sizeof operator doesnt evaluate arithmetic inside it, only sees the size of the variable inside

[[conditionals]]
[[fgets && getchar]]