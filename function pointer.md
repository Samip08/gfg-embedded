points to a function
datatype of pointer is considered the one of the function return 

int (* fptr)(int , int)  tells about the arguments of the function
then fptr = &add
can be called as fptr(5,10)

function pointer can be given as an argument
void calc(int a, int b, int (* op)(int, int)) {
    printf("%d\n", op(a, b));
}


array of function pointers 
 int (* farr[ ])(int, int) = {add, sub, mul, divd};
  printf("Sum: %d\n", farr [ 0 ] (x, y)); 