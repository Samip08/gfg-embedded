its a polling timer to ensure all things happen at exact time, can be done by hardware interrupts or software polling:
* hardware interrupts cause the whole frame to freeze and restart blocking execution of current actions
* software polling has tiny ns interrupts to ask if its time for execution 

this module helps the microcontroller keep a track of time, and the timespots at which the packets arrive