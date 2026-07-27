### Hardware Interrupts
asynchronous triggered by external devices

###### 8085 Hardware interrupts
- **TRAP (Non-Maskable):** The highest priority. It cannot be ignored by the CPU. Used for catastrophic events like power failures. (Vectored to `0024H`).
- **RST 7.5:** Vectored, edge-triggered    
- **RST 6.5:** Vectored, level-triggered.
- **RST 5.5:** Vectored, level-triggered.
- **INTR:** The lowest priority and the only non-vectored interrupt. The CPU asks the external device to place an instruction (usually an `RST`) on the data bus to tell it where to go.

###### ARM Hardware Interrupts
1. **IRQ (Interrupt Request):** The standard interrupt line for general hardware devices.
2. **FIQ (Fast Interrupt Request):** A higher-priority interrupt designed for lower latency. When an FIQ occurs, the CPU switches to a specific mode that has banked registers so it doesnt even waste time saving to stack frame



### Software Interrupts
synchronous intentionally triggered , these are usually called by the os

###### 8085 Software Interrupts
RST 0 - RST 7. When the programmer inserts one of these 1-byte instructions into the code, it forces the CPU to save the program counter to the stack and jump to a specific, predefined memory location

###### ARM Software Interrupts
ARM uses the **SVC (Supervisor Call)** instruction (formerly known as `SWI` or Software Interrupt). When user-level code needs to open a file or access hardware, it executes an `SVC`. This triggers a synchronous exception, causing the CPU to switch from User mode to privileged Supervisor mode, allowing the OS kernel to safely execute the requested service.

### WHY PRE-SCHEDULED SOFTWARE INTERRUPTS
Modern CPUs have different security levels, usually called **User Mode** and **Kernel Mode** (or Supervisor Mode).
- **User Mode (Untrusted):** Your application runs here. It is quarantined. It can do math and manipulate its own memory, but it is physically blocked by the CPU hardware from touching the hard drive, the screen, the network card, or other programs' memory.
- **Kernel Mode (Trusted):** The Operating System runs here. It has god-mode access to the hardware.