# MCLZ8_debug_code
An extension of the Microcore Labs MCLZ8 Z80 emulator code to allow for debugging, based loosely on the NICE Z-80 emulator.

Changes to the original MCLZ8 code include:

1. I've taken a stab at correcting some of the timing issues with the machine. This included reducing the cycle count for extended instructions and fiddling with the cycle count for jumps. It's now better than it was but there are sure to still be a lot of issues.
2. I have commented out the bit where it waits for a clock edge on the opcode fetch. I found on my machine running at 3.375 MHz that it was invariably busy decoding the opcode on the clock edge that it was supposed to wait for, so the timing was significantly out as a result. There will be issues if you run it on a slower system. Uncomment if this is the case.
3. I removed the stuff about speeding execution, as it's not interesting in my application. I want a debugger, not something that simply executes Z80 code fast.
4. I've added a pile of functionality to the terminal console to allow the Terensy to act as a debugger. Commands are stolen from the Nicolet NICE-Z80 set, and include:
   
       Ability to start (g) and stop (q) CPU code execution.
   
       Ability to set up to three breakpoints: "bp 1 1234" sets a breakpoint at 1234h.
   
       Ability to enable and disable breakpoints: "ebp 1" enables breakpoint 1. "dbp 1" disables it.
   
       Print machine status: "st" displays the status of each of the three breakpoints, plus whether the machine is running.
   
       Display memory contents: "d" displays memory. You can add a start and end address in hex, otherwise it just dumps 128 bytes from the last dump address.
   
       Display listing: "l" displays a listing, using a disassembler. start and stop as per "d".
   
       Display single byte: "e" does what it says.
   
       Fill memory: "f 100 200 55" fills from 0100h to 0200h with 55h
   
       Input from port: "i 23" dispolays the result of in from port 23h in hex.
   
       Output to port: "o 23 45" outputs 45h to port 23h.
   
       Write: "w 100 200" Writes from 100h to 200h to the console in intel hex format.
   
       Read: Not implemented properly.
   
       Clock divisor: "cd 10" waits ten clocks between opcode fetches. Can be used to slow down execution massively.
   
       Display or edit registers: "x" dumps registers. "x de 1234" sets register to 1234. Best done while the execution is halted!

Please bear in mind that I'm an RF engineer, not a programmer, so my code is by definition garbage!
