# Clouds - Granular Sampler Eurorack Module
A clone of the Mutable Instruments Clouds module.

<img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/6302c4ed-5bb9-4b85-9d67-47ec249ef3a8"> <img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/3ba8f56e-13f3-4e37-b3a5-8577a873fdca"> 

<img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/bcd2b8c7-2848-4d0f-b627-2fa81ea0c80c"> <img height="500" src="https://github.com/TOILmodular/Clouds/assets/97026614/43f0c30f-708c-4732-b6cb-8b2d8db97a31">

## Module Build and PCBs
There are two different versions for the control board, an "original" and a "Thonk" version.
Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="Clouds_CtrlPCB_Orig" src="https://github.com/TOILmodular/Clouds/assets/97026614/c3f94490-ba43-41f0-9d8e-333455597aeb">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created a version with footprints for those components.
Choose the one you need.

<img width="300" alt="Clouds_CtrlPCB_Thonk" src="https://github.com/TOILmodular/Clouds/assets/97026614/dd47a851-b9ac-46b9-85bc-81456b91c30e">

The layout of the main PCB also differs for both versions, since the different size of the jacks required a slight shift of the connecting headers.

<img width="300" alt="Clouds_MainPCB" src="https://github.com/TOILmodular/Clouds/assets/97026614/013ca7f5-13fb-4ed9-afef-e591e3434d4f">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. The layout is the same for both PCB versions.

## Additional Information about specific Components
There are several SMD components, which I listed below. Besides the STM32F405 microcontroller, the other main SMD part is the WM8731 audio codec chip. 
- DAC124S085 (DAC, 10-VSSOP package, the most challenging component due to its size)
- NJM4580/TL072 (OpAmp, 8-SOIC package)
- LM1117-3.3 (voltage regulator, SOT-223 package)
- LM4040B25 and LM4040B10 (voltage regulators, SOT-23-3 package)
- MMBT3904 (SMD version of the 2N3904 transistor, SOT-23-3 Package)
- 0.1uF capacitors (1608 package)

The design contains a quad VCA IC V2164 (THT version) from Cool Audio. That chip might not be available anymore. An alternative is the AS2164, available at Electric Druid or Thonk.

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider that fact. You might still use normal size resistors and put them in a standing position on the boards. Should also work fine.

## Firmware
I shared the .hex files for the STM32F103 chip (bootloader and main) in the folder Firmware.

The upload process is the same, as for my Braids clone. You can check out my [Braids video](https://youtu.be/TBMySGm7jKk) about how to program the Blue Pill board.

An alternative Parasite firmware version available as .wav file, which can also be uploaded via the procedure described in the official Mutable Instruments manual.

Check [this YouTube video](https://youtu.be/W8zez9X0Xok) for more details about the firmware update process.

## STM32F103 Version
CAUTION! There are three different versions of the Blue Pill board available.
The difference is the version of the ST32F103 microchip on the board.
The versions differ in the flash memory size:
- STM32F103C6T6: 32kB flash memory
- STM32F103C8T6: 64kB flash memory
- STM32F103CBT6: 128kB flash memory

The code size requires the 128kB version.
However, that version might be difficult to find, if available at all.
But it turned out, that STM3F103C8T6 is also ok for this module.

## Offset CV +10V/+5V
The original design from Mutable Instruments provides the option to have a +5V offset CV for all channels, instead of +10V. This is done by a jumper setting on the module backside. I decided to skip that part and to only have the +10V offset version, since the implementation of that option would have required another dual op amp.
