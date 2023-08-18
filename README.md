# Clouds - Granular Sampler Eurorack Module
A clone of the Mutable Instruments Clouds module.

<img height="500" src=https://github.com/TOILmodular/Clouds/assets/97026614/a5000123-7f93-4386-8b85-afdf539ab07d#> <img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/4f8eb8a2-2d69-4db1-bb83-a8e4bb365de1">

<img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/e2c78fd7-a510-43a8-8bc7-af06aedab49c"> <img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/7ecfbc26-5a38-4c39-950b-c84bebb76484">

## Module Build and PCBs
I added three different versions for the control board here, an "original", a "Thonk", and a "WM8731SSOP28" version.
Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="Clouds_CtrlPCB_Orig" src="https://github.com/TOILmodular/Clouds/assets/97026614/c17f2d8f-408c-4a50-b918-4de8d00c695e">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created another control board PCB for the versions "Thonk" and "WM8731SSOP28" with footprints for those components. That PCB is the same those two versions.

<img width="300" alt="Clouds_CtrlPCB_Thonk" src="https://github.com/TOILmodular/Clouds/assets/97026614/855f8c3c-d8a5-49ba-8d22-edc0a2164a0b">

The main PCB differs for all three versions. One reason is the different size of the jacks, which required a slight shift of the connecting headers between control and mainboard. The main PCB for the version "WM8731SSOP28" also differs from the "Thonk" version due to the fact that a different version of the audio codec chip WM8731 is used. You will find more details about that in the section "Additional Information about specific Components" below.

NOTE: I did not test the correctness of the "WM8731SSOP28" version of the main PCB.

<img width="300" alt="Clouds_MainPCB" src="https://github.com/TOILmodular/Clouds/assets/97026614/349e4a9b-065d-49dc-8fe8-ce97e6e2f9a0">

<img width="300" alt="Clouds_MainPCB_V2" src="https://github.com/TOILmodular/Clouds/assets/97026614/c42a49af-d477-4824-813a-67af106b92d5">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. The layout is the same for all PCB versions.

## Additional Information about specific Components
There are several SMD components, which I listed below. Besides the STM32F405 microcontroller, the other main SMD part is the WM8731 audio codec chip from Cirrus Logic. The production of that chip is now discontinued. There are still some chips available in stock, but the only ones offered by certified dealers have the package type QFN (quad flat no lead).

<img width="600" alt="WM8731 Close-Up" src="https://github.com/TOILmodular/Clouds/assets/97026614/1727ba69-bf46-4bc6-9adb-7a7ef0d35d4d">

Soldering such a part by hand might seem to be difficult. But I made the experience, that it is actually very easy to solder. You can check out [this YouTube video](https://youtu.be/pF8kdi-zm-c) about how I soldered that chip.

As mentioned above, I created a PCB version "WM8731SSOP28", which contains the footprint of the WM8731 chip with the package 28-SSOP, which was also used in the original Mutable Instruments module, as far as I know. I did not find any official online dealer, who still has such chips in stock. However, they mught still be offered by non-certified dealers on platforms, like Ebay.

Here is a list of SMD parts in my design.
- STM32F405RGT6 (microcontroller, version 7 is also working fine)
- WM8731 (audio codec, 28-VQFN or 28-SSOP package)
- LM1117-3.3 (voltage regulator, SOT-223 package)
- LM4040B10 (voltage regulator, SOT-23-3 package)
- MMBT3904 (transistor, SOT-23-3 package)
- 0.1uF capacitors (1608 package)

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider that fact. You might still use normal size resistors and put them in a standing position on the boards. Should also work fine.

The "In Gain" potentiometer is a 2-gang 50K A-type. The part from the original BOM from Mutable Instruments is the Bourns PTV112-4420A-A503. That pot does not have any screw thread at the shaft, and the shaft length is very small. So when soldering it flush to the PCB, it will not stick out enough from the front panel to prperly place a knob. I only realized those facts after I ordered the PCBs. Unfortunately, I did not find any other A50K pot with a longer shaft and the same footprint. So I used the original one and soldered it as close to the front panel as possible. It is working ok, but you need to be aware of that, when mounting the part on the PCB.

<img height="300" alt="Pot Details 4" src="https://github.com/TOILmodular/Clouds/assets/97026614/b6e7ba48-86d0-4d08-add3-360b3a6ff78c">

<img height="300" alt="Pot Details 2" src="https://github.com/TOILmodular/Clouds/assets/97026614/ba80b4f5-511f-4c99-894f-7efc2af5e2ea">

## Schematics
Due to the fact that the pin layout of the two package versions for the WM8731 chip are different, I uploaded two versions of the module schmatic in the folder "Schematic". The file "Schematic_Clouds.pdf" contains the layout for the QFN package version, while the file "Schematic_Clouds_WM8731SSOP28.pdf" is the one with the SSOP package.

## Firmware
I shared the .hex files for the STM32F405 chip (bootloader and main) in the folder Firmware.

## Programming
The main PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

<img width="200" alt="ProgrammingConnectors" src="https://github.com/TOILmodular/Clouds/assets/97026614/4c2f9492-3404-4fdb-b856-d80cbf1bd8b4">

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img width="200" alt="BootConnectors" src="https://github.com/TOILmodular/Clouds/assets/97026614/a370d390-931e-4a68-a801-566bb75f2273">

If you want to see more about the chip programming process, you can check out [this YouTube video](https://youtu.be/pF8kdi-zm-c).

## Calibration
The calibration procedure is the same, as the one for the original module from Mutable Instruments.

1. Disconnect all CV inputs.
2. Connect the note CV output of a well-calibrated keyboard interface or MIDI-CV converter to the V/OCT input.
3. Press the Load/Save button, and while you hold it down, press the Blend Parameter/Audio Quality button. 2 LEDs will blink.
4. Play a C2 note, or send a 1V voltage from your CV source.
5. Press the Load/Save button. Four LEDs will blink.
6. Play a C4 note, or send a 3V voltage from your CV source.
7. Press the Load/Save push-button.

NOTE! If you want to load the alternative Parasite firmware to the module, you need to calibrate the module afterwards. But the method to bring the module into calibration mode is slightly different. In order to put the module into calibration mode (procedure step no.3), you need to press the Load/Save button, while powering up the module. More details can be found on the [Parasites page](https://mqtthiqs.github.io/parasites/clouds.html).
