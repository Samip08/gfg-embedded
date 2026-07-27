contains the address to another pointer
** ptr means it holds the address of * ptr

* double pointers passing into a function can help change the value held by the main pointer itself, so it points to another variable
* double pointers help pass a 2d arrays or arrays of strings especally when each row has a different size

[checkout double pointers](https://www.geeksforgeeks.org/c/c-pointer-to-pointer-double-pointer/)

    int rows = 3;
    int rowsize[] = {3,5,6};
    int **arr = (int **)malloc(sizeof(int *)*rows);
    for(int i=0;i<3;i++){
        arr[i] =(int *)malloc(sizeof(int)*rowsize[i]);
    }