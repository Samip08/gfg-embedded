* breaks down the while() loop into smaller independent tasks which can are juggled to make it seem tasks are done in parallel
	 1.  Preemptive priority scheduling: ensures the highest priority task ready to run gets 100% cpu, preempts(interrupts) the lower priority tasks, to allow higher one to run
     2. time slicing: equal priority tasks are given a fixed time period to execute one after the other, if the first one doesnt finish executing in the given time its stopped, and the second one is run and first one proceeded after second time slice ends

* incase of delay/vTaskDelay cpu enters blocked state this allows lower priority tasks to be managed at this time/ if nothing then IDLE task(0 priority) to cleanup memory in the background


#### ANATOMY
* infinite loop that never returns a value, a task is defined inside the RAM by a Task Control Block(TCB)
* unlike regular programs the FreeRtos tasks have seperate stacks defined, each is allocated its own block of ram for local variables and function calls

#### SYSTICK
* the scheduler checks a hardware systick timer which generates periodic interrupts, when this tick comes the cpu enters the scheduler ISR, for a context/ongoing task switch
* cpu registers(PC, SP, working registers) are stored on the private stack frame of the task
* the cpu moves its internal pointers to the Task Control Block(TCB) of the highest priority ready to run task
* the cpu fetches the cpu registers from the highest priority task stack to the hardware