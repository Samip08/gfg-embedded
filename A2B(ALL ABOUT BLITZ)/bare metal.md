#include <stdint.h>

// 1. Define the physical RAM addresses from the ESP32 Datasheet
// The GPIO hardware peripheral lives at this specific hex address in the silicon.
#define GPIO_BASE_ADDR 0x3FF44000

// 2. Map the specific control registers based on offsets from the base
// We cast them to (volatile uint32_t *) so the C compiler knows these are hardware
// pointers and doesn't try to "optimize" them away.
#define GPIO_ENABLE_REG   ((volatile uint32_t *)(GPIO_BASE_ADDR + 0x0020)) // Sets INPUT or OUTPUT
#define GPIO_OUT_REG      ((volatile uint32_t *)(GPIO_BASE_ADDR + 0x0004)) // The actual state of the pins
#define GPIO_OUT_W1TS_REG ((volatile uint32_t *)(GPIO_BASE_ADDR + 0x0008)) // Write 1 To Set (ESP32 specific trick)
#define GPIO_OUT_W1TC_REG ((volatile uint32_t *)(GPIO_BASE_ADDR + 0x000C)) // Write 1 To Clear
// The pin we want to control
#define PIN_11 11

void main() {

    // ---------------------------------------------------------
    // STEP 1: MAKE THE PIN AN OUTPUT
    // ---------------------------------------------------------
    // Take a 1, shift it left 11 times: (0000100000000000 in binary)
    // OR it with the current register. This turns on the output driver for Pin 11.
    *GPIO_ENABLE_REG |= (1 << PIN_11);
    // ---------------------------------------------------------
    // STEP 2: TURN THE PIN ON (THE NAIVE WAY)
    // ---------------------------------------------------------
    // Read the register, modify the 11th bit to 1, write it back.
    *GPIO_OUT_REG |= (1 << PIN_11);
    // ---------------------------------------------------------
    // STEP 3: TURN THE PIN OFF (THE NAIVE WAY)
    // ---------------------------------------------------------
    // Shift a 1 by 11. Invert it (~). AND it with the register to force bit 11 to 0.
    *GPIO_OUT_REG &= ~(1 << PIN_11);

    // =========================================================
    // STEP 4: THE ESP32 PRO WAY (RTOS SAFE)
    // =========================================================
    // Why did I call the above method naive? RACE CONDITIONS.
    // Doing (*GPIO_OUT_REG |= 1<<11) requires the CPU to READ the memory,
    // CHANGE it, and WRITE it back (Read-Modify-Write).
    // What if the RTOS interrupts the CPU halfway through this process? Memory corruption.

    // To fix this, Espressif gave us the W1TS and W1TC registers.
    // If you write a 1 to W1TS, the hardware instantly turns the pin ON.
    // It completely ignores all the zeros. No read-modify-write required!
    // TURN PIN 11 ON safely:
    *GPIO_OUT_W1TS_REG = (1 << PIN_11);
    // TURN PIN 11 OFF safely:
    *GPIO_OUT_W1TC_REG = (1 << PIN_11);
}