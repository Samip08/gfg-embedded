`void setup(){
`xTaskCreate(TaskBlink , "Blink" , 128 , NULL , 1 , NULL);
`xTaskCreate(TaskSensor , "Sensor" , 128 , NULL , 2 , NULL);
`}

`void loop(){
`}

`void TaskBlink(void *pvParameters)
`for(;;){
`digitalWrite(13, HIGH);
`vTaskDelay(500 / portTICK_PERIOD_MS);
`digitalWrite(13, LOW);
`vTaskDelay(500 / portTICK_PERIOD_MS);
`}
`}`

tasks are given priority when they are created, like priority 1 task TaskBlink
