* holds a set of int contraints, mapping them to a array type index, not unique
enum enum_name {  
n1, n2, n3, ...  
}; // implicitly n1 is assigned value 0, n2 assigned value 1...

* redefining a value inside an enum inside another enum gives error, n2 wont be defined again to have recurring value by compiler, needs to be explicitly assigned value
* an enum variable , enum enum_name variable can be used to get index of these enum constants like enum enum_name variable = n1 gives variable value 0

* enum enum_name { 
    n1 = val1, n2 = val2, n3, ... };
}; you can manually assign values too and if you forget some constants , it becomes prev constant value+1

* size of enums is defined by the number of entries , smallest size chunk that can hold the required indexes,
* enums are mainly used to represent state diagrams in state machines , used to decipher error codes or make functionalities lists(read, write, execute)

* typedef used incase you dont wanna write enums again and again
typedef enums directions{
NORTH, EAST, SOUTH, WEST
}dirctns;
dirctns variable = SOUTH;