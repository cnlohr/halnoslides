# halnoslides

From [Teardown 2025 Portland](https://www.crowdsupply.com/teardown/portland-2025).

## The story of [ch32fun](https://github.com/cnlohr/ch32fun)

And how you can make your own SDK

I'm CNLohr on a few platforms. [Twitter](https://twitter.com/cnlohr), [bsky](https://bsky.app/profile/cnlohr.bsky.social), [Chaos.Social](https://chaos.social/@cnlohr), and [YouTube](https://www.youtube.com/cnlohr).

# What is it?

 * Like an SDK
 * Not a full HAL
 * Lots of examples
 * Minimal “features”
   * Startup code
   * Header
   * GPIO Config, On, Off
   * Delay
 * But these examples…
 * Teache how underlying hardware works
 * Gives a working start
 * Easy to grow/change

But I can do all this with a HAL? No?
 * Maybe?
 * “[Bootloader](https://github.com/cnlohr/rv003usb/tree/master/bootloader)” is a full USB stack in 1920 bytes of flash.
 * Allows self-program
 * Just nice to have USB on whatever pins you want

Underlying motivation:
 * Fast iteration time.
 * Stop making business decisions on fictional technical reasons.
   * If complicated apps only take a few kB, no need for expensiver chips.
   * Paradoxically avoids vendor lock-in. static_i2c.h
 * Reason about available resources
 * Stops rationale for mediocrity
 * Find new solutions to problems

[Electromage Poem](https://hackaday.io/project/159821-taptdoa/log/150490-ode-to-hal):
 > Oh HAL,
 > 
 > We're not a match.
 > 
 > I tried to be your pal
 > 
 > but you make my head scratch.
 > 
 > 
 > Your code is a puzzle
 > 
 > and the interface is jagged.
 > 
 > While CPU cycles you guzzle
 > 
 > my interrupt is run ragged!
 > 
 > 
 > But the hardware is elegant,
 > 
 > you time wasting contraption.
 > 
 > I've discovered registers most relevant
 > 
 > now I'm done with this abstraction
 > 
 >  ― Electromage

Terry A Davis Quote:
 > “An idiot admires complexity. A genius admires simplicity. [...for] an idiot, the more complicated it is, the more he will admire it.  If you make something so [confusing] he can’t understand it, he’s going to think you’re a god. Cause you made it so complicated no one can understand it.”
 > ― Terry A Davis


Oliver Wendell Holmes Quote:
 >“For the simplicity on this side of complexity, I wouldn't give you a fig. But for the simplicity on the other side of complexity, for that I would give you anything I have.”
 > ― Oliver Wendell Holmes

Simplicity on the other side of complexity IS possible.

Complexity does cancel out if you don’t keep stacking.

The goal is to take you from:

Technician -> Engineer
Application -> Crafting
Doing -> Understanding

My journey:

 * [Minecraft on a Microscope Slide](https://www.youtube.com/watch?v=EZRLOanNQ_w)
 * [Broadcasting NTSC using an ESP8266](http://www.youtube.com/watch?v=bcez5pcp55w)
 * [LoLRa (Bit banging LoRA)](https://www.youtube.com/watch?v=eIdHBDSQHyw)
 * [VR Running on the ESP32-S2](https://www.youtube.com/watch?v=VnZac6lA1_k)

... TODO Add others.

Projects that use ch32fun:
 * [Rudolph’s Sleigh On A North Pole PCB](https://hackaday.com/2024/12/20/rudolphs-sleigh-on-a-north-pole-pcb/)
 * [LED Matrix Earrings](https://mitxela.com/projects/ledstud)
 * [Smallest USB C Synth](https://mitxela.com/projects/smsc)

... TODO Add others.

Now, ch32fun uses many more features now, like USB Full Speed on the ch32v203, USB High Speed and gigabit ethernet on the ch32v307. And people are starting to add support for ch570 for ble beacons.

# Why have others been drawn?
 * RISC-V is cool?
 * Dumb luck?
 * Engineers are tired.

Originally developed [STM32F042_Fun](https://github.com/cnlohr/stm32f042_fun) based on libcm3. Did not succeed.

[STM32F042](https://github.com/cnlohr/stm32f042_fun) - 2019
 * 8 Stars, 1 Contributor
 * $0.50
 * 48MHz
 * Nice Micro
 * Has USB
 * 32kB Flash, 6kB RAM
 * 7x7 QFN Smallest Package
 * Requires 2 pins to program
 * ARM

[CH32V003](https://github.com/cnlohr/ch32fun) - 2023
 * 1.2k Stars, 86 Contributors
 * <$0.12
 * 48MHz
 * Nice micro
 * No USB*******  [https://github.com/cnlohr/rv003usb](Except for rv003usb)
 * 16kB Flash, 2kB RAM
 * 3x3 QFN Smallest Package
 * 1 pin RVSWDIO!
 * RISC-V

But ch32fun did work out.

Maybe it was my [mini-rv32ima](https://github.com/cnlohr/mini-rv32ima), which spawned off a lot of other interesting projects, like:
 * [Linux in Scratch](https://www.sohu.com/a/729343141_827544)
 * [RISC-V in Squirrle3 VScript](https://github.com/misyltoad/riscv-vscript)
 * [LinuxInExcel](https://github.com/NSG650/LinuxInExcel?tab=readme-ov-file)
 * [World's Worst Linux PC](https://www.hackster.io/news/giang-vinh-loc-creates-the-world-s-worst-linux-pc-using-an-arduino-uno-r3-and-its-atmega328p-e5ed03e3f594)
 * [Driver let's you run Linux after Windows BSODs, no reboot required](https://www.tomshardware.com/software/operating-systems/driver-hack-lets-you-run-linux-after-windows-bsods-no-reboot-required)

There has also been a lot of interesting work in the Linux in VRChat space, mostly by [_pi_ and running Linux in a Pixel Shader](https://blog.pimaker.at/texts/rvc1/).  Which a different version that didn't run linux but ran a raytracer got into [Shaderfes 2023](https://youtu.be/-KCJsZbUZ4g?t=4119).

# Philosophies

 * Zero*- or ultra-low cost abstractions only.
 * Abstractions should not hide the hardware, just make code look less verbose.
 * If you can just do something in an interrupt, do it
   * tinyusb is not so tiny
   * Much higher performance on many modes (HIDAPI feature reports)
 * No hugely complicated systems.

*https://www.youtube.com/watch?v=rHIkrotSwcc
CppCon 2019: Chandler Carruth “There Are No Zero-cost Abstractions”


## What makes a minimal SDK?
 * Programming
 * Compiler
 * “SFR” header
 * Linker Scripts
 * Startup Code
 * Interrupts
 * Build System
 * gdb
 * “Libc” / Printf, IO on/off

## Programming

 * Physical Interface
 * Register Access
 * PROGBUF
 * Reading/Writing RAM
 * Writing to Flash
 * Semihosting
 * GDB

Thankfully WCH chips use the RISC-V programming interface.

## Compiler

 * Host support
 * Windows, Linux, Mac
 * Client support
 * ARM, 32-, 64-
 * RISC-V, 32-, 64-
   * arm-none-eabi
   * riscv32-linux-gnu
 * Special features
 * xw, call0, etc.
 * GCC Versions
 * [Xpack](https://xpack-dev-tools.github.io/gcc-xpack/) Built-In, SysUtils

## ABI

 * The joke was from [Bjorkus's blog post about ABI](https://thephd.dev/binary-banshees-digital-demons-abi-c-c++-help-me-god-please
)
 * But, RISC-V has a much more stable ABI See [Wikichip's comments about RISC-V Registers](https://en.wikichip.org/wiki/risc-v/registers)

Just as an example consider the following code and assembly and you can see how parametrs are used. For instance a0 is the first prameter, a1 is the second and so on.  And return value is placed in a0.

```c
__attribute__((noinline))
int multiply( int a, int b )
{
    return a * b;
}
int MultiplyAndAdd()
{
    int a = 5;
    int b = 6;
    int c = multiply( a, b );
    return c + 7;
}
```

```asm
multiply(int, int):
        mul     a0,a0,a1
        ret
MultiplyAndAdd():
        addi    sp,sp,-16
        li      a1,6
        li      a0,5
        sw      ra,12(sp)
        call    multiply(int, int)
        lw      ra,12(sp)
        addi    a0,a0,7
        addi    sp,sp,16
        jr      ra

```

## Memory Map

RISC-V, sans MMU (memory mapped unit) sometimes will unmap memory at 0x00000000 to help make it easier to detect null pointer exceptions. The CH32 doesn't do this, they map either system flash or boot flash to 0x00000000.  This is where all code, read-only data, and, at least initially, data lives.

TODO SECTIONS














