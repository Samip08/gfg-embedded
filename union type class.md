* unions also allow storing data of multiple type, they share the same memory, improving memory efficiency, but changing one member overwrites the others
union A{
int x;
int y;
int z;};

* size of union is always the same as the size of the largest element, the less sized elements store their data in the same space without overflow, YOU CAN ONLY USE ONE MEMBER AT A TIME
* you cannot free the data, and rewriting provides gibberish, always instantialize to 0 , plus memory in heap, not stack there is no malloc, free
union trial T= {0};
    T.trial2.z = 64;
    unsigned char* raw_memory = (unsigned char*)&T;   //find the size of the union
    for (size_t i = 0; i < sizeof(T); i++) {
        printf("%p: %02X\n", (raw_memory + i), raw_memory[i]);    //shows memory addr, byte value
    }
    
*  Anonymous union - always nested, inside a struct/union allows accessing union member, without needing to explicitly make a union 
struct{
int x;
union{
int y;}value;
};   //can be accessed using struct_variable.value.y = 5;

* Full data overlap as members shares the same memory. if i have int x, y in union; with x initialized value 5, both union.x, union.y have value 5

[checkout the questions](https://www.geeksforgeeks.org/c/c-unions/)

