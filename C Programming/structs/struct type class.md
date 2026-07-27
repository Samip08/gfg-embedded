* struct consists of multiple fields of data belonging to any valid datatypes
* struct A{ 
	int x;} // creating a struct
* struct A a;  //defines a variable a belonging to struct A having fields as a.x --> int
* struct initialization either struct A a = {15} (in sequence of members) or struct  A a = {.x = 15}
* struct is passed to a function like normal variables
     void increment(struct A a, struct A* b){
		 a.x++;
		 b->x++;	} //yes thats how pointers are referred to in c
* similar to normal variables , if only passed by pointer does it change value inside the struct or it clones in the function and updates back and returns to pre function value outside function
* typdef struct structname{
	 int x;}struct1; //defined as struct1 variablename essentially alias
[[struct packing]]
[[nested structs]]
[[pointer to a struct ]]
[[self referential structs]]
[[bit field]]