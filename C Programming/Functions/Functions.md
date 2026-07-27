return_type function_name (function_parameters_definition){
	   //body statements
	   return value_type;
}

* library/inbuilt functions require corresponding header files
* stdio.h, primarily deals with input output operations- printf, scanf, puts, gets(keyboard operations), fopen, fclose, fread, fseek, fprint, fscan, fwrite(file operations), tmpfile(temporay file handling), setbuf, setvbuf(for buffer handling), perror, clearerr(for error managmen)
* stdlib is mostly for dynamic memory allocation- malloc , calloc , realloc, free(dynamic mem), rand, srand( random number gen), exit , abort, system(process control), type conversion, search sort, mathematical utilities , environment handling


* each function call creates a separate stack frame to store its local variables, parameters, and return information , once the function is exited the frame deletes itself , freeing up memory

#### calling a function by pointer vs value
* calling by values directly passes a copy of the actual values to be operated on inside the function, changes made inside the function are not represented inside the calling function 
* calling by parameter involves passing the pointer of the argument to the function, reflected in the final calling function
* instead of void function(int x, int y) pass void function(int * x, int * y)

#### returning multiple values from a function
1. returning multiple values via pointers: enter normal arguments, also enter the pointers to the variables you want to return value to , ex void compare(int a, int b, int * addr_min, int * addr_max) which can be called as compare(a, b, &min, &max)
2. returning multiple values as struct: make a struct with the return type values , make the function return a struct , struct struct_name function_name(argument definition), while packing return values inside the function itself say , struct struct_name result; result.member1= ___ , then finally return results, in the calling function you need a struct to hold the incoming return from the function
3. returning using arrays: passing the array(its pointer), to the function to append values , in the calling function need to create an array to be passed the required return values are returned at the indexes of the array appropriately

[[functioning of printf, scanf]]
[[standard library functions]]
[[main function with arguments]]
[[recursions]]
[[inline functions]]
[[nested functions]]


[[Arrays]]