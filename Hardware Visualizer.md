#### tui.py
* imports serial for uart communications, argparse for cli flags, rich for ui components
* sets up baud rate 115200, and port and names for the cli agent
* cleans up comma seperated pin names to add to the table from the src code
* enters a state machine of idle and checks for 'v', 'a' as sync bits to show incoming transmission, then gets the expected payload of 2 bytes IF AVAILABLE
* f the payload length is correct, iterates through the bytes, shifts the high byte left by 8 bits, pushes onto the live ui terminal

#### hwviz.h
* initializes the max watched pins at a time at 16, a private class is defined so it cant be externally manipulated it has the stream pointer, the watched pins list and its count
* the public class defines the methods begin, watch(for single pin, multiple pins) , pump
#### hwviz.cpp
* initializes pointers and counts to 0
* `begin()`, assigning the user's provided hardware serial stream to the class's internal pointer.
* Implements the initializer list `watch()` method, looping through a provided array (e.g., `{A0, A1}`) and adding them individually.
* Starts the `pump()` method, immediately aborting if no stream is attached or no pins are watched to prevent null pointer crashes.
* Loops through the tracked array and triggers the hardware ADC to read the current pin voltage into a 16-bit variable.


[[Questions 1]]