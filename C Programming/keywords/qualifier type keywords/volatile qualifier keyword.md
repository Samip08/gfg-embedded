* volatile says that the value might change at any time without any action taken by code(ie sensors), 
1. prevents compiler from optimizing specified variables(removing unnecessary code to access variable each time)
2. always reads latest memory of that variable
3. multithreading and hardware level programming
* why to use volatile:
1. memory mapped io/hardware solutions- - A sensor updates a memory location OR An interrupt service routine (ISR) modifies a variable , the compiler might pickup old data from cache instead of new from memory if it has optimized the variable.
2. multithreading applications- if  multiple threads use the same variable, it might check registers instead of getting from memory

* If volatile is not used in such scenarios:
The compiler may cache variables in registers
Updates from other threads may not be visible
Interrupt-driven changes may be ignored
Code may behave correctly only in debug mode, not in optimized builds

* generally for optimization it would check if the status of the variable changes after each iteration and notices in normal variables it doesnt, so it disables read status and runs the value in an infinite while loop, the compiler isnt aware that your variable can change externally , so it doesnt implicitly make status = 1
* usually used w pointers of variables who's value can change