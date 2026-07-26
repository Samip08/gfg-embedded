control panel for the microcontroller you are working on
[env:esp32dev]
platform = espressif32
board = esp32dev
framework = arduino

lib_deps  = (github repos here)

platform ini implicitly clones the github repo in a hidden pio folder and allows you to directly use them in your code by including these

* in a microcontroller we use memory mapped i/o as a part of the physical address on the ram
* pwm signals like analog write are worked around by a hardware timer, say analogWrite(pin11, 127), in a 8 bit clk it goes high from 0 to 127 then low till 255 and overflow to 0(again high)
* esp32 has a special gpio matrix which allows rerouting perpherals, and communication networks
[[bare metal]]