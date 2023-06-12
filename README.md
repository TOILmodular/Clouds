# Clouds - Granular Sampler Eurorack Module
A clone of the Mutable Instruments Clouds module.

<img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/5dd48620-f568-4704-8d37-8d14a14df783"> <img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/ec769496-852a-4bec-b98c-c0662abd589e"> 

<img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/bcd2b8c7-2848-4d0f-b627-2fa81ea0c80c"> <img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/43f0c30f-708c-4732-b6cb-8b2d8db97a31">

## Module Build and PCBs
There are three different versions for the control board, an "original", a "Thonk", and a "WM8731SSOP28" version.
Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="Clouds_CtrlPCB_Orig" src="https://github.com/TOILmodular/Clouds/assets/97026614/c3f94490-ba43-41f0-9d8e-333455597aeb">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created another control board PCB for the versions "Thonk" and "WM8731SSOP28" with footprints for those components. That PCB is the same both versions.

<img width="300" alt="Clouds_CtrlPCB_Thonk" src="https://github.com/TOILmodular/Clouds/assets/97026614/dd47a851-b9ac-46b9-85bc-81456b91c30e">

The main PCB differs for all three versions. One reason is the different size of the jacks, which required a slight shift of the connecting headers between control and mainboard. The main PCB for the version "WM8731SSOP28" also differs from the "Thonk" version due to the fact that a different audio codec chip is used. You will find more details about that in the section "Additional Information about specific Components" below.

NOTE: I did not test the correctness of the "WM8731SSOP28" version of the main PCB.

<img width="300" alt="Clouds_MainPCB" src="https://github.com/TOILmodular/Clouds/assets/97026614/013ca7f5-13fb-4ed9-afef-e591e3434d4f">

<img width="300" alt="Clouds_MainPCB_V2" src="https://github.com/TOILmodular/Clouds/assets/97026614/fb098750-b861-4347-809c-d34ee51270a0">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. The layout is the same for all PCB versions.

## Additional Information about specific Components
There are several SMD components, which I listed below. Besides the STM32F405 microcontroller, the other main SMD part is the WM8731 audio codec chip from Cirrus Logic. The production of that chip is now discontinued. There are still some chips available on stock, but the only ones offered by certified dealers have the package type QFN (quad flat non-lead).

<img width="600" alt="WM8731 Close-Up" src="https://github.com/TOILmodular/Clouds/assets/97026614/596c0339-ab18-48d0-8c38-c2ffb3d6c844">

Soldering such a part by hand might seem to be difficult. But I made the experience, that it is actually very easy to solder. You can check out this YouTube video about how I soldered that chip.

As mentioned above, I created a PCB version "WM8731SSOP28", which contains the footprint of the WM8731 chip with the package 28-SSOP, which was also used in the original Mutable Instruments module, as far as I know. I did not find any official online dealer, who still has such chips in stock. However, I have been told that they can still be found e.g. at Ebay.

Here is a list of SMD parts in my design.
- STM32F405RGT6 (microcontroller, version 7 is also working fine)
- WM8731 (audio codec, 28-VQFN or 28-SSOP package)
- LM1117-3.3 (voltage regulator, SOT-223 package)
- LM4040B10 (voltage regulator, SOT-23-3 package)
- 0.1uF capacitors (1608 package)

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider that fact. You might still use normal size resistors and put them in a standing position on the boards. Should also work fine.

## Schematics
Due to the fact that the pin layout of the two package versions for the WM8731 chip are different, I uploaded two versions of the module schmatic in the folder "Schematic". The file "Schematic_Clouds.pdf" contains the layout for the QFN package version, while the file "Schematic_Clouds_WM8731SSOP28.pdf" is the one with the SSOP package.

## Firmware
I shared the .hex files for the STM32F405 chip (bootloader and main) in the folder Firmware.

## Programming
The main PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

<img width="200" alt="ProgrammingConnectors" src="https://github.com/TOILmodular/Clouds/assets/97026614/60779ef5-7a4f-42a2-83d0-d1fb9aacc26a">

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img width="200" alt="BootConnectors" src="https://github.com/TOILmodular/Clouds/assets/97026614/dd45d33f-ffa9-4c42-a707-e779d0dd8267">

If you want to see more about the chip programming process, you can check out [this YouTube video](https://xxx).

## Calibration
The calibration procedure is the same, as the one for the original module from Mutable Instruments.

1. Disconnect all CV inputs.
2. Connect the note CV output of a well-calibrated keyboard interface or MIDI-CV converter to the V/OCT input.
3. Press the Load/Save button, and while you hold it down, press the Blend Parameter/Audio Quality button. 2 LEDs will blink.
4. Play a C2 note, or send a 1V voltage from your CV source.
5. Press the Load/Save button. Four LEDs will blink.
6. Play a C4 note, or send a 3V voltage from your CV source.
7. Press the Load/Save push-button.
