* pointer to a struct called point,  struct Point* ptr = &p; //p is the name of the struct variable , ptr is the pointer to the location of p, to unpack data printf("%d %d", ptr->x, ptr->y);

typedef struct trial{
    int x;
    char y;
} xy;

int main(){
    xy varible = {.x = 5, .y = 's'};
    struct trial* ptr = &varible;
    printf("%d", ptr->x);
    return 0;
}