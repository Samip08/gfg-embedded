* if you redefine same variable names in multiple files it might hit a redefintion error, so extern tells c that this variables exists globally or in linked files
* so if instead of making a new variable locally w higher priority calling extern means you wanna import the variable
* helps resolver link references across multiple files, doesnt allocate memory
