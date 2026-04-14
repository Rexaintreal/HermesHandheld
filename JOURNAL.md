---
title: "HermesHandheld"
author: "Saurabh Tiwari"
description: "A custom handheld pi zero retro console"
created_at: "2026-04-14"
---

# April 14: Finding Parts and making BOM

So i found this supercool project while looking for inspiration on printables [simplyRetroZ5](https://www.printables.com/model/163507-simplyretro-z5-retropie-emulation-handheld) it was too advanced for me tho it has speakers, custom firmware etc which i am not planning to add in my hermes handheld project but this gave me a rough picture on what things i will need to build this project.

<img width="1920" height="1440" alt="image" src="https://github.com/user-attachments/assets/16f66df9-bbac-4440-9807-173eb2c6fd69" />

Core 
---------------
for Hermes i will use decided to use pi zero 2w instead of pi zero as it is more capable and finding pi zero can't handle nds emulation as it is too underpowered the zero 2w also supports 64bit architechture 

Display 
---------------
For the display any 5 inch display would work we don't need touch etc so i decided to go with the waveshare 5 inch display

![ZY18318926_4](https://github.com/user-attachments/assets/f8e26415-9360-4eee-98c4-3e730802c092)

Battery
---------------
We need atleast 2000 mah and 3.7v battery so we could get a few hours of backup but along with this we would need a powerboost so it could give a stable 5V and handles charging via usb-c The Adafruit PowerBoost 1000C fits perfectly here since it:
- Boosts battery voltage to stable 5V  
- Handles LiPo charging  
- Provides safe power regulation for portable builds

for the battery we can go with any battery which meets the voltage and capacity requriements also for the power on off we would need a slide switch
![81vWDk1H7JL _SL1200_](https://github.com/user-attachments/assets/be3b85ec-7731-435a-a908-68f17c95ea71)

Audio
---------------
Currently our goal is only wired 3.5 mm jack to make things simple we could add 1W small speakers maybe later idk so a 3.5 mm audio jack would work 

Control
---------------
for controls we will go with the tactical buttons and maybe a dpad for hard plastic 
- ABXY
- Start / Select
- D-pad (likely a 4-button layout or hard plastic cap design)

Misc
---------------
Other supporting components include:
- MicroSD card slot and storage setup  
- Resistors for pull-ups and button stability  
- Jumper wires and headers for internal wiring  
- Breadboard for initial testing  
- Possible custom PCB later if everything works well  
- Fully 3D printed case for final enclosure  

With all this in mind i created the [BOM.md](https://github.com/Rexaintreal/HermesHandheld/blob/main/bom/bom.md) 

**Total time spent: 1 hour**
