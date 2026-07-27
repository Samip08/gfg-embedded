* Set of generally used instructions, crammed down to 16 bits, instead of regular 32 bits to save RAM memory space
* CPU has only a single set instruction architecture, the 16 bit instruction is expanded by the hardware while executing
* THUMB architecture, includes hardcoded instructions to perform common commands
* But THUMB state does not include many important functions like:
    1. **System/Coprocessor Registers:** You cannot access system control or coprocessor registers directly.
    2. **Complex Barrel Shifting:** In standard 32-bit ARM, you can do an `ADD` and shift a register's bits left/right all in a single instruction. `ADD R1, R0, R1 LSL#2`
    3. **Interrupt Handlers:** High-level exception handlers and boot/reset vectors typically have to start in full 32-bit **ARM state** because the hardware needs raw, unconstrained access to the control registers and program status
SUB R0, #0, R1 ; R0 = 0 - R1