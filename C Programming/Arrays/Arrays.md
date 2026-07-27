linear data structure that stores fixed size sequence of similar type of data, in contiguous memory locations
* when an array is only declared and not initialized it contains some garbage values, it can be initialized while being declared
* if you initialize even a single value all the garbage gets wiped out and replaced by 0s
* arrays provide random access , meaning you do not need to traverse remaining indexes to check a particular index
* array decay: array loses its dimensions in certain conditions and becomes pointers, so we cannot determine the size of array using size of, because its lowkey measuring size of pointer atp, to prevent this we pass pointer to start and the size
* arr(i)(j) is equivalent to * (* (arr + i) + j), i controls no of rows j controls no of elements in a row
* * (* (* (arr + i) + j) + k));
* for passing a 2d array, pass arr pointer, total elements and number of columns
* void increment_5 (int *ptr, int size, int rows){
    for(int i=0;i<size;i++){
        *(ptr+i) += 5;
        printf("%d ", *(ptr+i));
    }
}

[passing a 3d array to a function](https://www.geeksforgeeks.org/c/pass-a-3d-array-to-a-function-in-c/)

[[strings]]