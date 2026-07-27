ESP32-WROOM has multiple cores, usually core 0 is assigned to arithmetic and code processing works, while core 1 might be handling wifi/bluetooth
[[Preemptive priority scheduling]] 
[[FreeRTOS code]]
[[Inter Task Communication & Synchronization]]

[suspended]<------>[blocked]  //waiting for delay or event
				   |
			    [Ready]  //waiting for allocation of task
				   |
				[running] //ongoing current task