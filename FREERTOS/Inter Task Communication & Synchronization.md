* Since Tasks run independently but use same raw global variables , they cannot work without data corruption(race condition)
* core0 pub sub and the core1 wifi wants to write something at the same time in the same register, that is why esp32 framework doesnt allow direct register level access like bare metal Arduino coding

	1. Queues: Thread safe FIFO data pipeline, passes actual sensor struct data from producer to consumer task
	2. Semaphores: Flags for signaling, like waking up a high priority task as soon as the interrupt ends
	3. Mutexes: System to implement Priority Inheritance, protects the same task resource from being used by two different tasks simultaneously


#### Mutex
`SemaphoreHandle_t sharedResourceMutex;`    
*//memory address pointing to hidden data block in the ram storing which task has control over resource*

`int sharedCounter = 0;`               *//data the tasks are commonly using*

`void TaskAccessResource(void *pvParameters) {
	`String taskName = (char *)pvParameters;
	`for (;;) {
`// portMAX_DELAY tells the task to wait indefinitely until the lock is available
		`if (xSemaphoreTake(sharedResourceMutex, portMAX_DELAY) == pdTRUE) {`
		
*//check to see if the task is able to access resource/critical part*
		
			`int temp = sharedCounter;
			`temp = temp + 1;
			`vTaskDelay(10 / portTICK_PERIOD_MS);
			`sharedCounter = temp;
			`Serial.print(taskName);
			`Serial.print(" secured the lock. Counter is now: ");
			`Serial.println(sharedCounter);
			`xSemaphoreGive(sharedResourceMutex);}`    
*//handing resource to next requesting task

		`vTaskDelay(250 / portTICK_PERIOD_MS);
*//security period to prevent same task from hogging up continuous ticks, let other tasks check
	`}
`}