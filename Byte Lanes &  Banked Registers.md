* To read a 32 bit word(addr/data) we need to use 4 byte lanes lanes1-4
* but if you want to write a 1 byte char you dont need 4 byte memory, that is what the wstrb helps in if its a 32 bit word then its 4'b1111 , for uint_8 its a simple 4'b0001
* arm system is rigid and doesnt allow misaligned bits, so for a data it has to have an address starting with a multiple of 4

* There are a total of 31 registers in arm but at any time of 16 at max can be accessed by the user
* in the normal USER mode there are R0 to R15 and incase of FIQ mode(frequent interrupts) registers R8-R14 get replaced by banked registers R8_fiq to R14_fiq, it doesnt waste time in storing to stack and restoring