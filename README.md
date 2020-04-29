# SNES_to_NES_ATtiny24
Convert a SNES gamepad into a NES gamepad with autofire and Konami code buttons.
Bug fix: Fixed clock configuration
Bug fix: fixed interrupt handlers
Changed pin configuration so that the reset line can be used.
Changed clock speed to 8MHz
Changed LONG_DELAY to work with 8MHz clock
Software UART subroutines were not changed, so baud rate has doubled. This does not really matter because those subroutines were just for debugging.
Interrupt handlers are still not working correctly, I'm working on it.