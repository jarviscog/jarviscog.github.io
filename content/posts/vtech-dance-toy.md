---
title: 'VTech Toy Hardware Hacking'
date: 2024-02-19T09:12:17-04:00
draft: false
tags: ["Projects"]
---

A little while back a friend and I were looking for some ways to get into embedded programming and reverse engineering. 
My primary motivation was learning Ghidra, the NSA-built decompiler used for malware analysis and reverse engineering.

The original plan was to spend a weekend ripping apart and tinkering with some device from the second hand store. Something like a router or network switch. That is, until we found a VTech Kidi Star Dance toy.
Choosing this turned out to be the right decision for a few reasons:
- Low data security meant things are less likely to be locked down
- Lots of IO means debugging and following logic are going to be a lot easier
- Hacking a kids toy is pretty flashy, and communicable than something like a network switch

After returning home with the toy, as well as some Red bulls, we got to work.

## Checking out the Hardware
First things first. What are we working with here? Let's rip it apart and start looking up the hardware inside.

{{< figure src="/images/dance-memory.png" >}}
The device contained a BoyaMicro 25Q64ASSIG. After finding the datasheet, this looks to be a 64Mbit SPI Flash chip, which means we found the memory of the device! All of the songs, graphics, and fun will be locked away inside this chip.

Next up...
{{< figure src="/images/dance-chip.png" >}}
Looks like "GP31P1002". This one is a bit harder to find, but after some sweet-talking with a rep, we have a datasheet.  

Both of these chips serve as the main CPU/RAM for the toy. The more we can understand these two devices, the better.


## Ripping the Firmware
{{< figure src="/images/dance-flasher.png" title="CH341A attached to the memory chip">}}

After connecting a flashing tool to the chip, we were able to attempt to read the contents using flashrom.

{{< highlight sh >}}
~ % flashrom --programmer ch341a_spi -r firmware.bin

flashrom 1.4.0 on Darwin 23.2.0 (arm64)
flashrom is free software, get the source code at https://flashrom.org

libusb: info [darwin_detach_kernel_driver] no capture entitlements. may not be able to detach the kernel driver for this device
libusb: warning [darwin_detach_kernel_driver] USB device capture requires either an entitlement (com.apple.vm.device-access) or root privilege
Cannot detach the existing USB driver. Claiming the interface may fail. LIBUSB_ERROR_ACCESS
Found Boya/BoHong Microelectronics flash chip "B.25Q64AS" (8192 kB, SPI) on ch341a_spi.
...
Reading flash... done.
{{< / highlight >}}

This leaves us with a .bin file that we can use for further analysis, and where the real analysis starts. Theres a few different ways to go with this, and I was eager to open up Ghida and take a look, but there may be some other useful information we can pull out first.  
Running `strings` on the binary produces the following truncated output:
{{< highlight sh >}}
strings -n 10 firmware.bin

KPIiVtech5205
spi slave mode end
pG ~init~
...
device_id%d
ReadPage = 0x%x
ReadPageFail!!!
WritePage = 0x%x
WritePageFail!!!
spi flash id = %x,%x,%x
@FIFO data size A%x  B%x
...
AudDecOpenFile Err
audio_decode_start Err
AudDecBGPollingStart Err
Mount Disk[%d] ret=%d
Not Support Encode
main_entry
[Fail!] Beyong channel bound.... ch=%d
DAC fail!!!!
ADC fail!!!!
...
Confirm#Factory#Reset
Candy Wonderland
The Funky Bear
Our Favorite Song
...
Dancing Academy
Dancing Challenge
Free Dance
My Dance Trophies
...

{{< / highlight >}}


This is a lot of great data. To start, there is what looks to be debug information. Dissasembaling this will prove to be a lot easier than expected, as based on context from the strings we can tell what the variables are. This also means that there is potentially a debug mode for the device or a way to read out the debug information while the program is running.

Looking near the bottom, it appears that there are some song names and menu items. 
As a preliminary test, let's try replacing one of the strings and writing the firmware back to the toy. 
This can be done with any text editor.  
One thing to remember is that this is a compiled binary, so any pointers will be referencing fixed areas in memory. 
This means that if we change any strings, it is important that the length of those strings does not change. 
If they were to, it would shift all the data past it, and some of the pointers may become invalid.

{{< figure src="/images/dance-test.png" >}}
It worked! This means we may be able to completely bust this thing open. (Doom anyone?)

To get any further, it looks like we may need to use Ghidra.

## Ghidra
Let's start by looking at the entropy of the binary. Along the right we can see some red, gray, and green chunks, hovering over gives us "compressed", "N/A", "x86" respectively.
{{< figure src="/images/dance-entropy.jpg" >}}
The compressed section starts at `003e0000`, and looking at the ascii doesn't show anything useful:

{{< highlight text >}}
003e0000  fffa 32c0 7877 0000 05e4 2947 7461 0021  . . 2 . x w . . . . ) G t a . !
003e0010  410b aff7 1290 0249 44e1 251f 8169 9808  A . . . . . . I D . % . . i . .
003e0020  430f 26c4 c2f6 30fb b803 031c 0862 083e  C . & . . . 0 . . . . . . b . >
003e0030  381f 7e5d fcfe 1f2e 7f87 fafc 3fcb 9fae  8 . ~ ] . . . . . . . . ? . . .
003e0040  7f0f 977d 6f0f 9222 51c6 dc92 38d3 69c4  . . . } o . . " Q . . . 8 . i .
003e0050  a251 c000 20e0 2900 1f0a 0403 e6c4 d8c0  . Q . .   . ) . . . . . . . . .
003e0060  20d8 d919 6100 e04d 0022 809d 9159 3b01  . . . a . . M . " . . . Y ; . .
{{< / highlight >}}

From the output of `strings`, we know that this device can handle mp3 data, so let's look into that.  
Most files have header information describing how to process the file. 
mp3 is part of the MPEG standard, which encompasses multiple different file types that all work by splitting a larger file into chunks called 'frames'. 
Going off of [this](http://www.mp3-tech.org/programmer/frame_header.html) information, we can try and see if the start of this data makes sense as an mp3, and it turns out it does!
After extracting this block of data, we can create an mp3 file that contains all of the songs on the device.

{{<audio src="/audio/dance-song.mp3" caption="Excerpt from \"Crazy Dance\"">}}

More to come!


