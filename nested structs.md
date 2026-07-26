* nested structs, include packed structs struct parent{int age; struct child b;} unwrapped as parent_variable.age, parent_variable.b.x etc
*   struct A{
    int x;
    struct yz{
        int y;
        int z;
    }YZ;
};

printf("%d", try.YZ.y);

* if dependent(internal) struct is defined externally the outer struct can be defined as
	 struct A{
	     int x;
	     struct yz YZ;};
used inside main as variable try then  try.x, try.YZ.y ,  struct <struct_name> <variable_defined_for struct>

* passing a nested struct as a pointer 
struct yz{
        int y;
        int z;
    };
    
struct A{
    int x;
    struct yz YZ;
} * str;

int main(){
    struct A a = {5,{6,7}};
    str = &a;
    printf("%d", str->YZ.z);
    return 0;
}

* passing to function, can happen in two ways, either you pass struct to function, unpack inside function or function is defined in terms of individual parameters which case, it can be unpacked during the calling of the function

void show(struct Organisation);
show(org);  //org is the variable for the struct storing the values

void show(char organisation_name[], char org_number[], int employee_id, char name[], int salary); 
show(org.organisation_name, org.org_number, org.emp.employee_id, org.emp.name, org.emp.salary); //unpacked in the call of the function
