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

STM32F042 - 2019
 * 8 Stars, 1 Contributor
 * $0.50
 * 48MHz
 * Nice Micro
 * Has USB
 * 32kB Flash, 6kB RAM
 * 7x7 QFN Smallest Package
 * Requires 2 pins to program
 * ARM

CH32V003 - 2023 
 * 1.2k Stars, 86 Contributors
 * <$0.12
 * 48MHz
 * Nice micro
 * No USB*******
 * 16kB Flash, 2kB RAM
 * 3x3 QFN Smallest Package
 * 1 pin RVSWDIO!
 * RISC-V

But ch32fun did work out.


TODO - pick up here.


