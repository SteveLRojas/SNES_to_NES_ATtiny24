# SNES_to_NES_ATtiny24
Convert a SNES gamepad into a NES gamepad with autofire and Konami code buttons.  

Bug fix: Fixed clock configuration  
Bug fix: fixed interrupt handlers  
Changed pin configuration so that the reset line can be used.  
Changed clock speed to 8MHz  
Changed LONG_DELAY to work with 8MHz clock  
Software UART subroutines were not changed, so baud rate has doubled. This does not really matter because those subroutines were just for debugging.  
Interrupt handlers are still not working correctly, I'm working on it.  

Bug fix: Enabled pullup on NES clock to get more consistent timings.  
Bug fix: Clear GIFR in interrupt handlers to prevent single pulses from triggering the interrupts twice.  
Bug fix: Modified SNES_DELAY to work with 8MHz clock.  
This version works, and has been tested with Contra, B-Wings, and Rad Racer. Unfortunately if the NES clock pulses are made any longer this will not work, so it is probable that PAL consoles will not work.  
During testing I noticed that the NES timings depend on the game being played, Contra sends the latch pulse right before the first clock pulse but B-Wings sends the latch pulse much earlier.  
It is possible for some games to read the controller in a way that extends the clock pulses, which would not work. I am currently working on this issue.  
I also discovered that the NES clock is normally high, which annoys me greatly because I always assumed it was normally low.  

Bug fix: Added extra check in interrupt handler for NES clock. This will ensure that the interrupt handler is called only once per clock pulse.  
Now there are two methods to ensure that the interrupt works correctly: For short pulses clearing GIFR ensures that the interrupt happens only once.  
For longer pulses there is a check at the start of the interrupt handler that checks the state of the NES clock to determine if the edge was rising or falling.   Falling edges are ignored, so even though the interrupt happens twice the outputs are updated only once.  
The interrupt handler for latch pulses works in the same way. This code was tested with Contra, Rad Racer, B-Wings, and Crystalis. All games worked correctly.  
