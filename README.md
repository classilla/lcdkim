# KIM-1 LCD Experiments

[Another Old VCR Super Duper Thing!](https://oldvcr.blogspot.com/2023/10/what-kim-1-really-needs-is-lcd-screen.html)

Copyright (C) 2023 Cameron Kaiser.  
All rights reserved.  
Various licenses, see below.

## What these are

These are demonstration tools showing how to connect the MOS/Commodore KIM-1
single-board computer to a Matrix Orbital LK204-25, which is a
serial-addressable HD44780-style LCD display, or a compatible device.

To connect the LK to the KIM-1, you can use the built-in 20mA current loop
terminal interface with a converter, but this project provides a software
output-only driver that fits into the free RRIOT RAM at $1780. To use it,
connect the LK ground either to common ground or A-1 on the application
connector, and A-14 either directly to the LK (if you're using the TTL 5V
version) or to a connected level shifter (if you're using the RS-232 version).
The LK should be configured for 19.2kbps, which is the bit rate it ships with.
[Here's how we did it.](https://oldvcr.blogspot.com/2023/10/what-kim-1-really-needs-is-lcd-screen.html)

All source files cross-assemble with [`xa65`](http://www.floodgap.com/retrotech/xa/), or use the provided binaries.
To upload them to your KIM, you can convert them to paper tape, or upload
them directly with a tool like [KIMup](https://github.com/classilla/kimup/).

## What's included

`19200.xa` is the 19.2kbps output driver. Input is not currently supported,
nor are other bitrates. Call it with the desired character in the accumulator.
All registers are clobbered by this routine. You must upload this routine as a
prerequisite for the others, e.g., `kimup -g 0 0 test 0x1780 19200` will run the
`test` binary using this driver. The driver is called `19200` and starts at
$1780.

`test.xa` is a quick test routine that calls the output sender in a tight
loop over ASCII character codes 65 through 96. The binary is called `test`
and starts at $0000.

`kim.xa` is a demonstration that loads custom character definitions into the
LK and then displays a simple KIM-1 logo. It assumes a 20x4 LCD, the most
common screen dimensions. The binary is called `kim` and starts at $0000.

`lcdreverse.xa` is an adaptation of Jim Butterfield's version of the People's
Computer Co. game Reverse as shown in the [First Book of KIM](https://archive.org/details/The_First_Book_of_KIM/page/n101/mode/2up?view=theater),
refactored for play on the LCD. Keys and gameplay are the same, except that
your moves are shown on the LCD instead. It assumes a 20x4 LCD, the most
common screen dimensions. The binary is called `lcdr` and starts at $0200.

## Don't open issues

... except for actual bugs. Refactors, changes for your favourite assembler,
or other feature requests will not be accepted (fork the project).

## License

Re-Verse is an adaptation of a Jim Butterfield program which is (C) 1977,
1978 F. J. Butterfield. Butterfield is deceased and it is not clear which,
if any, license this program would fall under, though he has previously
granted generous free terms for the use of his other programs. No copyright
is known to be held by any other author or publisher.

The driver, `test.xa` and `kim.xa` are released under the 2-clause BSD license.

Copyright (C) 2023 Cameron Kaiser. All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.



