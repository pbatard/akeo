# UBRX - Universal BIOS Recovery console for x86 PCs #

## What is UBRX? ##

Imagine a world where being unable to recover your PC, because of an improperly flashed BIOS, becomes virtually impossible.

Imagine a world where you can attempt to switch an existing PC BIOS to a custom UEFI one, without having to worry about recovery in case the UEFI boot fails.

Imagine a world where you can develop/customize your own BIOS code, with a safety net that doesn't involve the ability to switch flash ROM chips or the use of an external programmer.

Imagine a world where, if your PC refuses to boot after BIOS POST, you can simply add a PCI card with an option ROM, i.e. pretty much any PCI network card, and execute a recovery program of your choosing.

Imagine a world where, even if you don't have a legacy serial port, you can plug a PCI-E USB 3.0 card to obtain a low level USB 3.0 debug console, where you are able to run any executable you can imagine, even before BIOS or EFI starts executing.

Imagine picking a BIOS ROM from one PC, putting it into another, without having to worry on whether you will be able to boot into an environment that will allow you to reflash the main BIOS payload in-situ, rather than require an external programmer.

Finally, imagine a world where the arbitrary distinctions between AMD and Intel CPUs or motherboard hardware and chipsets no longer matters, and where a universal binary allows you to run any code you want, right after CPU reset.

This is what **UBRX** is all about.

**UBRX** is simply a console, running in the very early levels of execution of a standard PC firmware (BIOS/EFI), that provides **you** with full control over the boot process of your PC and with everything you need to run the code of your choosing early, such as a BIOS/UEFI debugger, a ROM flasher or any kind of program you can imagine.

## How does UBRX work? ##

UBRX is intended to be used as a BIOS bootblock, i.e. the very first section of code that gets executed. This is because it aims at being able to provide recovery options in case the rest of the boot process from the BIOS or EFI fails.

In its very small payload (currently ~2.5 KB), it first attempts to initialize a Super I/O chipset, in a very generic fashion, then, for each potential Super I/O candidate, it tests the chip for 16550 serial capabilities, which most Super I/Os would implement.
Once a potential 16550 unit is detected, UBRX initializes it and attempts to detect a recovery entry sequence (currently a series of spaces) sent by a serial user console.

If the recovery request is detected, the UBRX console activates, where elementary commands can be used to initialize or probe part of the system, or upload a program and execute it (see the [USAGE file](http://code.google.com/p/akeo/source/browse/ubrx/USAGE) for details of the commands available). If the recovery request is not detected, and all the potential 16650 or Super I/Os have been probed, the UBRX bootblock yields the rest of the boot process to BIOS or EFI.

## News ##

  * 2011.08.04: [UBRX v0.4](http://akeo.googlecode.com/files/ubrx-0.4.tar.gz) released! - please check the [README](http://code.google.com/p/akeo/source/browse/ubrx/README).

## TODO ##

  * Procedure on how to compile bare metal executables for UBRX
  * Y-modem transfer
  * Execution from PCI Option ROM
  * Integration with coreboot/standard BIOS/UEFI and yield to it
  * USB 3.0 debug support

## Source Code ##

```
svn checkout http://akeo.googlecode.com/svn/ubrx ubrx```
