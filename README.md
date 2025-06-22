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

## Memory Map and Sections

RISC-V, sans MMU (memory mapped unit) sometimes will unmap memory at 0x00000000 to help make it easier to detect null pointer exceptions. The CH32 doesn't do this, they map either system flash or boot flash to 0x00000000.  This is where all code, read-only data, and, at least initially, data lives.

 * .init = Code that must be at beginning of flash
 * .text = Regular code
   * int MyFunction()
 * .rodata = Read-only data, can stay in flash
   * const int MyConstInt = 37;
 * .data = Data that is copied into RAM, read, write, w/ default.
   * int MyData = 45;
 * .bss = Zeroed-by-default RAM
   * static int SomeGlobal; // Initialized to 0 by default.
 * Heap = Where malloc’d values go (we don’t have malloc)
 * Stack = Local variables, call stacks, etc.

.init, .text, .rodata, .data are in Flash.
.data, .bss, Heap and Stack live in RAM.

.data starts in Flash, but is copied to RAM, so it can be later modified.

## Linker Scripts

 * Where is the memory
 * What are sections
 * Where does the memory go?

```ld
ENTRY( InterruptVector )
MEMORY
{
	FLASH (rx) : ORIGIN = 0x08000000, LENGTH = 16k
	RAM (xrw)  : ORIGIN = 0x20000000, LENGTH = 2k
}
SECTIONS
{
	.init :
	{
		. = ALIGN(4);
		KEEP(*(SORT_NONE(.init)))
		. = ALIGN(4);
	} >FLASH AT>FLASH

	.text :
	{
		. = ALIGN(4);
		*(.text)
		*(.text.*)
		*(.rodata)
		*(.rodata*)
		. = ALIGN(4);
	} >FLASH AT>FLASH

	.data :
	{
		. = ALIGN(4);
		__global_pointer$ = . + 0x3fc; 
		*(.data .data.*)
		. = ALIGN(8);
		*(.srodata .srodata.*)
		. = ALIGN(4);
		PROVIDE( _edata = .);
	} >RAM AT>FLASH

	.bss :
	{
		. = ALIGN(4);
		PROVIDE( _sbss = .);
		*(.sbss*)
		*(.bss*)
		*(COMMON*)
		. = ALIGN(4);
		PROVIDE( _ebss = .);
	} >RAM AT>FLASH

	PROVIDE( _end = _ebss);
	PROVIDE( end = . );
	PROVIDE( _eusrstack = ORIGIN(RAM) + LENGTH(RAM));
}
```

## Startup code

```as
.global InterruptVector
.section .init
InterruptVector:
	.option   push
	.option   norvc
	j         _start
	.option   pop
	.word     0
	.word     NMI_Handler
	.word     HardFault_Handler
	.word     0
…
    .word     EXTI7_0_IRQHandler
       //EXTI Line 7..0 
…

_start:
	// a0 = hart ID, a1 = DTB

.option push
.option norelax
    // Load gp for faster indexing
	la gp, __global_pointer$
.option pop

    // Machine Mode
	li a3, 0x1880
	csrw mstatus, a3

    // Setup stack
	la sp, _eusrstack

// Clear RAM to zeroes
	la  a3, _sbss
	la  a4, _ebss
	li  a5, 0
	bge a3, a4, 2f
1:	sw a5, 0(a3)
	addi a3, a3, 4
	blt a3, a4, 1b
2:

// Load .data from FLASH to RAM
	la a3, _data_lma
	la a4, _data_vma
	la a5, _edata
1:	beq a4, a5, 2f
	lw a7, 0(a3)
	sw a7, 0(a4)
	addi a3, a3, 4
	addi a4, a4, 4
	bne a4, a5, 1b
2:
	li a3, 0x3
	la a0, InterruptVector
	or a0, a0, a3
	csrw mtvec, a0

	la a4, main
	csrw mepc, a4
	mret

```

## Interrupts

 * “Pointers” in the interrupt vector.
 * Usually decorate functions in user space.


The user writes:
```c
void EXTI7_0_IRQHandler( void ) __attribute__((interrupt));
void EXTI7_0_IRQHandler( void ) 
{
    // Flash just a little blip.
    funDigitalWrite( PC1, FUN_HIGH );
    funDigitalWrite( PC1, FUN_LOW );

    // Acknowledge the interrupt
    EXTI->INTFR = EXTI_Line3;
}

```

Somewhere you need to define:
```c
typedef enum IRQn
{
    // 2 Non Maskable Interrupt
    NonMaskableInt_IRQn = 2,
    // 3 Exception Interrupt
    EXC_IRQn = 3,            
…
    // External Line[7:0] Interrupts 
    EXTI7_0_IRQn = 20,
} IRQn_Type;
```

And the ISR needs to be enabled.
```c
NVIC_EnableIRQ( EXTI7_0_IRQn );
```

So, this is the interrupt vector:
```asm
.global InterruptVector
.section .init
InterruptVector:
	.option   push
	.option   norvc
	j         _start
	.option   pop
	.word     0
	.word     NMI_Handler
	.word     HardFault_Handler
	.word     0
…
    .word     EXTI7_0_IRQHandler
       //EXTI Line 7..0 
…
```

And this is what a hexdump looks like

```as
00000000 <InterruptVector>:
   0:	0f40006f          	j	f4 <handle_reset>
   4:	00000000          	.word	0x00000000
   8:	000001b0          	.word	0x000001b0 << NMI_Handler
   c:	00000164          	.word	0x00000164 << Hard Fault Handler
	...
  30:	00000164          	.word	0x00000164
  34:	00000000          	.word	0x00000000
  38:	00000164          	.word	0x00000164
  3c:	00000000          	.word	0x00000000
  40:	00000164          	.word	0x00000164
  44:	00000164          	.word	0x00000164
  48:	00000164          	.word	0x00000164
  4c:	00000164          	.word	0x00000164
  50:	000002c0          	.word	0x000002c0 << Pin Change IRQ
  54:	00000164          	.word	0x00000164
  58:	00000164          	.word	0x00000164
```

## Build Systems

Just try make.  You should condier [https://makefiletutorial.com](https://makefiletutorial.com/)

It works this way:

```make

PARAMETER:=thing

thing_you_want : things_needed_to_make_what_you_want
	How_to_make_the_thing $(PARAMETER)
```

This is what an example user Make thing looks like:
```make
all : flash

TARGET:=bootload
LINKER_SCRIPT:=../../ch32fun/ch32v003fun-bootloader.ld
WRITE_SECTION:=bootloader
FLASH_COMMAND:=../../minichlink/minichlink -a -U -w $(TARGET).bin $(WRITE_SECTION) -B
TARGET_MCU:=CH32V003
include ../../ch32fun/ch32fun.mk

optionbytes :
    $(MINICHLINK)/minichlink -w +a55aff00 option # Enable bootloader, disable RESET

flash : cv_flash
clean : cv_clean
```

## Build assembly listings!!!

```make
$(TARGET).bin : $(TARGET).elf
	$(PREFIX)-objdump -S $^ > $(TARGET).lst  ## This one!!! 
	$(PREFIX)-objcopy $(OBJCOPY_FLAGS) -O binary $< $(TARGET).bin
	$(PREFIX)-objcopy -O ihex $< $(TARGET).hex
```

Using objdump -s will give you the assembly and your C code, in-line.

```
        funDigitalWrite( PD0, 1 );
 78a:    4785                  li    a5,1
 78c:    c81c                  sw    a5,16(s0)
        funDigitalWrite( PC0, 1 );
 78e:    40011737              lui    a4,0x40011
 792:    cb1c                  sw    a5,16(a4)
        printf( "+%lu\n", count++ );
 794:    c081a583              lw    a1,-1016(gp) # 20000004 <count>
 798:    6505                  lui    a0,0x1
 79a:    82c50513              addi    a0,a0,-2004 # 82c <main+0xe8>
 79e:    00158713              addi    a4,a1,1
 7a2:    c0e1a423              sw    a4,-1016(gp) # 20000004 <count>
 7a6:    35e5                  jal    68e <printf>
```

## Special function registers

You gotta find a way to tell C where all your IO is.

Describe the hardware:
```c
typedef struct
{
	__IO uint32_t CFGLR;	/* Port Configuration Register Low  */
	__IO uint32_t CFGHR;	/* Port Configuration Register High */
	__I  uint32_t INDR; 	/* Port Input Data Register     	*/
	__IO uint32_t OUTDR;	/* Port Output Data Register    	*/
	__IO uint32_t BSHR; 	/* Port Set/Reset Register      	*/
	__IO uint32_t BCR;  	/* Port Reset Register          	*/
	__IO uint32_t LCKR; 	/* Port Configuration Lock Register */
} GPIO_TypeDef;
```

Set up these macros:
```c
#define GPIOA_BASE  0x40010800
#define GPIOA_BASE  0x40010800
#define GPIOA_BASE  0x40010800
#define GPIOA  ((GPIO_TypeDef *)GPIOA_BASE)
#define GPIOC  ((GPIO_TypeDef *)GPIOC_BASE)
#define GPIOD  ((GPIO_TypeDef *)GPIOD_BASE)
```

## Read the technical reference manual.

No, really, they're good stuff.  They tell you so much about the chip.

## Fast I/O Abstractions

You can use funDigitalWrite() and it is as fast as the raw register code.

We spent a lot of time trying to optimize our `funDigitalWrite` function...

```c
#define FUN_HIGH 0x1

#define GpioOf( pin ) \
((GPIO_TypeDef *)(GPIOA_BASE + 0x400 * ((pin)>>4)))

#define funDigitalWrite( pin, value ) \
{ GpioOf( pin )->BSHR = 1<<((!(value))*16 + ((pin) & 0xf)); }

#define PC5 0x35
#define PC6 0x36
```


Compare the Arduino `digitalWrite`:
```asm
digitalWrite:
        lui     a5,%hi(.LANCHOR0)
        slli    a0,a0,5
        addi    a5,a5,%lo(.LANCHOR0)
        add     a5,a5,a0
        lw      a3,8(a5)
        li      a4,-1
        beq     a3,a4,.L1
        lw      a3,0(a5)
        lw      a0,4(a5)
        lui     a5,%hi(PORT)
        lw      a4,%lo(PORT)(a5)
        li      a5,84
        mul     a5,a3,a5
        li      a2,1
        sll     a2,a2,a0
        add     a5,a4,a5
        lw      a5,0(a5)
        and     a5,a2,a5
        bne     a5,zero,.L3
        li      a5,21
        mul     a5,a3,a5
        add     a5,a5,a0
        slli    a5,a5,2
        add     a5,a4,a5
        snez    a0,a1
        sw      a0,12(a5)
.L3:
        li      a5,84
        mul     a3,a3,a5
        add     a4,a4,a3
        bne     a1,zero,.L4
        sw      a2,76(a4)
        ret
.L4:
        sw      a2,80(a4)
.L1:
        ret
gpiotest:
        addi    sp,sp,-16
        li      a1,1
        li      a0,4
        sw      ra,12(sp)
        call    digitalWrite
        li      a0,5
        li      a1,1
        call    digitalWrite
        lw      ra,12(sp)
        addi    sp,sp,16
        jr      ra
        .set    .LANCHOR0,. + 0
```

To ours:
```asm
    funDigitalWrite( PC5, 1);
    funDigitalWrite( PC6, 1);

gpiotest:
        li      a5, 0x40011000
        li      a4, 32
        sw      a4, 16(a5)
        li      a4, 64
        sw      a4, 16(a5)
        ret
```

“But why does it matter”
 * Stops rationale for mediocrity
 * Bit banging is valid.
 * Reduces bloat
 * static_i2c.h

... For instance we can use static_i2c to turn every port of a microcontroller into an I2C port.

## Systick

 * Wrap-around issues
 * Scheduling issues
 * How can I delay if I want to use the systick interrupt?

You can do small delays this way and/or set the CMP to trigger the ISR at a later time.

```c
	uint32_t targend = SysTick->CNT + n;
	while( ((int32_t)( SysTick->CNT - targend )) < 0 );
```

AVOID altering/resetting SysTick->CNT

Does not work on some ARM chips.  Some ARM chips use a 24-bit SysTick.

## How does GDB work?

 * Halt Processor
 * Read/Write Register+RAM
 * Breakpoints: Write ebreak to Flash
 * Need some basic step/continue/pause
 * GDB Protocol is from 1989 as best as I can tell.
 * Works well over serial* or socket**
 * Needs gdb-multiarch
*[rvprog](https://github.com/aappleby/picorvd)
**-minichlink (in ch32fun)

You can see it all with any of the multitude of gdb stubs. For instance, from here: [mini-gdbstub](https://github.com/RinHizakura/mini-gdbstub)

```c
struct target_ops {
    gdb_action_t (*cont)(void *args);
    gdb_action_t (*stepi)(void *args);
    size_t (*get_reg_bytes)(int regno);
    int (*read_reg)(void *args, int regno, void *value);
    int (*write_reg)(void *args, int regno, void* value);
    int (*read_mem)(void *args, size_t addr, size_t len, void *val);
    int (*write_mem)(void *args, size_t addr, size_t len, void *val);
    bool (*set_bp)(void *args, size_t addr, bp_type_t type);
    bool (*del_bp)(void *args, size_t addr, bp_type_t type);
    void (*on_interrupt)(void *args);
    void (*set_cpu)(void *args, int cpuid);
    int (*get_cpu)(void *args);
};
```

## Libc functions

Add functions like this:
 * memcpy
 * memset
 * strstr
 * rand 
...and
 * printf

But don't use any printf, use something like: [mini-printf](https://github.com/mludvig/mini-printf)

## Semihosting

So you can printf over the debug cable.

 * Printf over SWD
 * On ARM, kinda slow
 * On RV32, kinda fast
 * Save I/O pins
 * Program, Debug, Printf
 * `make clean all monitor`

On ch32, printf is surprisingly fast.

```
make monitor | pv > /dev/null
Found ESP32S2 Programmer
 536KiB 0:00:15 [36.7KiB/s] [        <=>                     ]
```

It only takes about 1.6s to do [`make clean all monitor`](https://www.youtube.com/watch?v=LBCafdNdA7U) on my laptop. 

## Ending

Even if ch32fun isn’t useful to you, I hope it can stand as an approachable testament to help teach how to make your own.

Don’t make computers match someone else’s intuition

Change your brain to internalize reality

Change your intuition

I hope you have been moved...

Technician -> Engineer
Application -> Crafting
Doing -> Understanding


