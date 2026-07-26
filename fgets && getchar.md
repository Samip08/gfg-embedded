### fgets
standard input method for character array in stdio.h

* stores the input into a character array and stops reading when it reaches a newline character, the specified number of characters, or end-of-file (EOF), this includes whitespaces
* it is safer than gets because it prevents buffer overflowing by limiting characters
* fgets(buff, n, stream);  //stream is input sequence, buff is the storage character arr, n is number of characters including null terminator
* returns the pointer to buff if successful or else returns NULL if error or end of file

ex: reading from txt file 
    FILE * fptr = fopen("in.txt", "r");
    fgets(buff, sizeof(buff), fptr);
    fclose(fptr);   //before return 0;

general keyboard input 
    fgets(name, sizeof(name), stdin);


* gets is the older version as it doesnt have overflow protection and can only read from stdin



### getchar
int main()
{
    int s = 13;
    int x;
    while (s--) {
        x = getchar();
        putchar(x);
    }
    return 0;
}

write multiple characters