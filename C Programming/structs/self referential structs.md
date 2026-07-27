* self referential structs contain pointer to itself, allowing multiple of them to be linked together, create link lists, trees, graphs 

* struct structure_name {
	data_type member1;
	data_type member2;
	struct structure_name* pointer_name;  //address of another object of the same structure
	};
> ****Note:**** Always initialize self-referential pointers to nullptr before using them.

* self referential classes with a single pointer to self object(singly linked list), further multiple links(to future, past self object) helps make doubly linked list, for doubly linked list just define forward and backward address exactly like in singly linked

#include <stdio.h>
#include <stdlib.h>

struct NODE{
int x;
struct NODE* next_ptr;
}

int main(){
struct  NODE* head = (struct NODE*)malloc(sizeof(struct NODE));
struct  NODE* middle = (struct NODE*)malloc(sizeof(struct NODE));
struct  NODE* tail = (struct NODE*)malloc(sizeof(struct NODE));

head->x = 5;
head->next_ptr = middle;

head->x = 6;
head->next_ptr = tail;

head->x = 7;
head->next_ptr = NULL;

struct NODE* current = head;
while(current!=NULL){
printf("%d", current->x);
current = current->next_ptr;}

free(head);
free(middle);
free(tail);

return 0;
}

[more data structures](https://www.geeksforgeeks.org/dsa/self-referential-structures/)
