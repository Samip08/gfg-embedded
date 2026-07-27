* arduino ide has a single loop running(blocking) which means if one action is stalling the code the other sensor data/actuations do not get changed in real time, this means your wheels might overshoot or crucial actions might be delayed
* in ros you can have seperate nodes running which do not stall the operations of other nodes, if one of them even fails the rest work normally

#### How does RTOS work
* rtos( real time operating system ) has a seperate hardware scheduler which executes functions like publishing or subscribing at hard deadlines
* cuts short any other task ongoing saves all the cpu registers to ram and then executes the current scheduled task then restores registers and returns control to the original task 
* my little nigga you cannot use arduino isr interrupts, those need to be fast as those are blocking statements too, rtos 

#### How does RTOS handle read over write schedules
incase Task A is writing into a register and systick, hardware scheduler alerts Task B which reads from this register, a value mid write from A might be picked up causing corruption
1. Mutual Exclusion: like data hazards it sees that this register is mutually exclusive and not fully operated on by Task A, call to Task B is revoked and Task A finishes its work followed by call to Task B
2. async fifo/Queue: Task B is on the recieving end of the queue, Task A never stops rather it keeps writing and Task B picks the newest values from this queue

[[blitz ros]]
[[mcu_pio]]