mcu_pio
	* include
		* constants
		* functions
			* [[store_data.cpp]]
			* [[timer_cb.cpp]]
		* pinmaps
		* include_all.cpp
	* lib
		* Blitz
			* [[blitz.hpp]]
			* [[blitz_interfaces.hpp]]
		* Timer
			* [[blitz_timer.cpp]]
	* src
		* main.cpp
	* [[platform.ini]]


* mcu doesnt actively stare at the void tryna intercept data rather it uses a hardware fifo buffer and an interrupt system
* the hardware usb port on the mcu catches the stray bits and puts then in a ring buffer, the interrupt checks this for any new data