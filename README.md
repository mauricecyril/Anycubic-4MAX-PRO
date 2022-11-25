# Anycubic 4MAX PRO
Settings and Notes Related to the Anycubic 4Max Pro 3D Printer.

### **WARNING**: USE AT YOUR OWN RISK! All information collected on this github is for research purposes and is NOT professional advice or should not be considered a definative source for understanding, modifying or configuring the Anycubic 4Max Pro 3d printer or any 3d printer. Please do your own research and make sure you understand the potential risks, loss or damage to your health, your 3d printer, your house or those around you should you use the Anycubic 4Max Pro or follow or use any of the settings, files or information provided on this github repository. You assume all responsibility and liability for any damage or harm that may occur by following the information aggregated and posted here. USE AT YOUR OWN RISK!

## Information 
The heated bed of this printer tends to get warped and it becomes imposible to manually level the bed. The alternative is to add Mesh Leveling capabilities to this printer to make it usable.  

The printer uses a trigorilla board v1.0 but please double check by opening up the base of the printer and check the mainboard (see https://github.com/knutwurst/Marlin-2-0-x-Anycubic-i3-MEGA-S/wiki/Beginner's-Guide-(English)#3-identification-of-the-mainboard ) 

There is also a daughter board connected which has the pins for the end stops.

## Adding BL Touch to the Anycubic 4Max Pro V1.0
 **WARNING: USE AT YOUR OWN RISK! Please make sure to do your own configuration and conduct your own research before flashing your printers firmware, installing a BLTouch or configuring the BLtouch for the printer. I am not responsible for any potential risks, loss or damage to your health, your 3d printer, your house or those around you should you use the Anycubic 4Max Pro or follow or use any of the settings, files or information provided on this github repository. USE AT YOUR OWN RISK!**

### Purchase a genuine BLTouch
Try to acquire a genuine BLTouch device as there are reports of clones generally failing or having quality issues.
Make sure to also get the 1.5m extension wire with the dupont connectors.

The trigorilla mainboard on the Anycubic 4Max Pro has the servo control pins already soldered on
"+ - Power"
"- - GND"
"S - Signal"

But the BLTouch dupont connector needs to be reconfigured (see https://www.antclabs.com/wiring ) to swap the power and ground.
Original BLTouch Wiring 

| Original BLtouch Wiring | Modified BLtouch wiring | Connection to Anycubic 4MaxPro Boards |
| ------------- | ------------- |  ------------- |
| Brown (GND)  | Red (5V)  | + Servo Headers on Main Board |
| Red (5V)  | Brown (GND)  | - Servo Headers on Main Board |
| Orange (Signal)  | Orange (Signal)  | S Servo Headers on Main Board |
| Black (GND)   | Black (GND)  | Black (GND) on Daughter board |
| White (Z axis Signal)  | White (Z axis Signal)  | White (Z axis Signal) on Daughter board  |

### Print a custom mount
Find a suitable BLtouch mount or experiment with one of the following:
| STL | Approximate Offset (Make sure to do your own calibration) | 
| ------------- | ------------- |
| Ancycubic 4MaxPro Standard Fan BLtouch Mount v4.stl | X Offset = +54.87mm, Y Offset = -1.70mm, Z Offset = |
| Ancycubic 4MaxPro Vortex Fan BLtouch Mount v2.stl | X Offset =+55.43mm , Y Offset =-2.0 (other readings say -7.91mm) , Z Offset =  (Probe extends 8.78mm - Distance from probe base to nozzle is 8.43mm) |

Make sure to calibrate the location of the BLTouch Probe in relation to your nozzle.

Remember the X,Y,Z are coordinates oriented when you're facing the front of the printer (ie. the door on the front of the 4Max Pro).
Y axis is the movement towards and away from you. So +Y is moving the printer head away from you, -Y is moving the printer head towards you.
X axis is the movement left and right of you. So +X is moving the printer head to the right, -X is moving the printer to the left.
Z axis is the movement up and down. So +Z is moving the pritner head up away from the printer bed, -Z is moving the printer down towards the printer bed.

### Flash the appropriate firmware (if required)
For example: Marlin 2.0.x for Anycubic 4Max Pro
https://github.com/Poket-Jony/Marlin-A4MaxPro-2.0.x

Make sure to compile your own version using the Arduino IDE and configure the X,Y,Z offsets! Make sure to follow the post firmware installation calibration steps. 

### Remove Bottom Cover
Lay the printer flat so that the bottom cover is exposed. To remove the base plate remove the four hex machine screws (M3x12) and also remove the padded covers and remove additional 4 machine hex screws (M4x8). 

### Remove Back Cover
Stand the printer back up (you can use the cover to protect the main board).
Remove the 8 screws on the back panel and remove the back panel to get run the extension cable through the existing cable management. You may want to add your own zip ties to anchor the new wires.

### Wire up the Extension Wire to the controller and daughter board
Lay the printer flat again (ie. front door laying flat).



# Ultimaker Cura 4.4 Settings for the Anycubic 4Max Pro
If "Origin at Center" is checked when slicing the printer seems to print off the printbed and in the lower left quadrant. Recommendation is to keep this setting unchecked. 

Settings / Printer / Manage Printers

Edit Machine Settings

Printer

    Printer Settings
    
        X (Width): 270mm
        Y (Depth): 205 mm
        Z (Height): 205 mm
        Build Plate Shape: Rectangular
        Origin at Center: Unchecked
        Heated Bed: Checked
        Heated Build Volume: Unchecked
        G-Code Flavor: Marlin
        
    Printhead Settings
        X min: 0
        Y min: 0
        X max: 205
        Y max: 205
        Gantry Height: 25.0
        Number of Extruders: 1
        
    Start G-Code
        G21 ;metric values
        G90 ;absolute positioning
        M82 ;set extruder to absolute mode
        M107 ;start with the fan off
        G28 X0 Y0 ;move X/Y to min endstops
        G28 Z0 ;move Z to min endstops
        G1 X-3 Y40 ;Anycubic 4Max Pro Brush
        G1 X-3 Y5 ;Anycubic 4Max Pro Brush
        G1 X-3 Y40 ;Anycubic 4Max Pro Brush
        G1 X-3 Y5 ;Anycubic 4Max Pro Brush
        G1 Z15.0 F{speed_travel} ;move the platform down 15mm
        G92 E0 ;zero the extruded length
        G1 F200 E3 ;extrude 3mm of feed stock
        G92 E0 ;zero the extruded length again
        G1 F{speed_travel}
        M117 Printing...
        G5

    End G-Code
        M104 S0 ; turn off extruder
        M140 S0 ; turn off bed
        M84 ; disable motors
        M107
        G91 ;relative positioning
        G1 E-1 F300 ;retract the filament a bit before lifting the nozzle, to release some of the pressure
        G1 Z+0.5 E-5 ;X-20 Y-20 F{speed_travel} ;move Z up a bit and retract filament even more
        G28 X0 ;Y0 ;move X/Y to min endstops, so the head is out of the way
        G1 Y180 F2000
        M84 ;steppers off
        G90
        M300 P300 S4000        


Extruder 1

    Nozzle Settings
    
        Nozzle Size: 0.4 mm
        Compatible Material Diameter: 1.75 mm
        Nozzle Offset X: 0 mm
        Nozzle Offset Y: 0 mm
        Cooling Fan Number: 0
        
    Extruder Start G-Code: Blank
    Extruder End G-Code: Blank
    
# Ultimaker Cura 4.4 Settings for the Anycubic 4Max Pro with BLTouch
If "Origin at Center" is checked when slicing the printer seems to print off the printbed and in the lower left quadrant. Recommendation is to keep this setting unchecked. Removed 

Settings / Printer / Manage Printers

Edit Machine Settings

Printer

    Printer Settings
    
        X (Width): 270mm
        Y (Depth): 205 mm
        Z (Height): 205 mm
        Build Plate Shape: Rectangular
        Origin at Center: Unchecked
        Heated Bed: Checked
        Heated Build Volume: Unchecked
        G-Code Flavor: Marlin
        
    Printhead Settings
        X min: 0
        Y min: 0
        X max: 205
        Y max: 205
        Gantry Height: 25.0
        Number of Extruders: 1
        
    Start G-Code
        G21 ;metric values
        G90 ;absolute positioning
        M82 ;set extruder to absolute mode
        M107 ;start with the fan off
        G28 X0 Y0 ;move X/Y to min endstops
        G28 Z0 ;move Z to min endstops
        G1 X-3 Y40 ;Anycubic 4Max Pro Brush
        G1 X-3 Y5 ;Anycubic 4Max Pro Brush
        G1 X-3 Y40 ;Anycubic 4Max Pro Brush
        G1 X-3 Y5 ;Anycubic 4Max Pro Brush
        G1 Z15.0 F{speed_travel} ;move the platform down 15mm
        G92 E0 ;zero the extruded length
        G1 F200 E3 ;extrude 3mm of feed stock
        G92 E0 ;zero the extruded length again
        G1 F{speed_travel}
        M117 Printing...
        G5

    End G-Code
        M104 S0 ; turn off extruder
        M140 S0 ; turn off bed
        M84 ; disable motors
        M107
        G91 ;relative positioning
        G1 E-1 F300 ;retract the filament a bit before lifting the nozzle, to release some of the pressure
        G1 Z+0.5 E-5 ;X-20 Y-20 F{speed_travel} ;move Z up a bit and retract filament even more
        G28 X0 ;Y0 ;move X/Y to min endstops, so the head is out of the way
        G1 Y180 F2000
        M84 ;steppers off
        G90
        M300 P300 S4000        


Extruder 1

    Nozzle Settings
    
        Nozzle Size: 0.4 mm
        Compatible Material Diameter: 1.75 mm
        Nozzle Offset X: 0 mm
        Nozzle Offset Y: 0 mm
        Cooling Fan Number: 0
        
    Extruder Start G-Code: Blank
    Extruder End G-Code: Blank
        
    
# Octoprint Settings
Still researching

# Sources

## Github
Marlin 2.0.x for Anycubic 4Max Pro
https://github.com/Poket-Jony/Marlin-A4MaxPro-2.0.x

## Thingiverse
Anycubic 4Max Pro Cable Chain by wadzio October 15, 2019
https://www.thingiverse.com/thing:3918237

Anycubic 4Max Pro Cable Chain - fixed parts by BgB42O June 14, 2020
https://www.thingiverse.com/thing:4459661

Vortex Fan Duct for Anycubic 4Max Pro by ontherunstudio July 26, 2019
https://www.thingiverse.com/thing:3772311

Anycubic 4Max Pro 2.0 Print head lid by alex_trask August 16, 2021
https://www.thingiverse.com/thing:4934115

4max pro Cura 4.1 profiles by skfinley July 29, 2019
https://www.thingiverse.com/thing:3778487

4Max Pro BLTouch Cable Holder by neutr0n January 07, 2020
https://www.thingiverse.com/thing:4090425

BLTouch and 3D Touch mount for Anycubic Mega S/X/P by Knutwurst October 25, 2021
https://www.thingiverse.com/thing:5030218

## Reddit
BLtouch on an Anycubic 4Max Pro by g8tto3
https://www.reddit.com/r/3Dprinting/comments/g8tto3/bltouch_on_an_anycubic_4max_pro/
https://web.archive.org/web/20221124154853/https://www.reddit.com/r/3Dprinting/comments/g8tto3/bltouch_on_an_anycubic_4max_pro/

BLTouch Installation (english) from Marlin-2-0-x-Anycubic-i3-MEGA-S
https://github.com/knutwurst/Marlin-2-0-x-Anycubic-i3-MEGA-S/wiki/BLTouch-Installation-(english)

Beginner's Guide (English) from Marlin-2-0-x-Anycubic-i3-MEGA-S
https://github.com/knutwurst/Marlin-2-0-x-Anycubic-i3-MEGA-S/wiki/Beginner's-Guide-(English)#3-identification-of-the-mainboard

Installed BLTouch last night. Here's things I wish I'd known.
https://www.reddit.com/r/ender3/comments/c6n02e/installed_bltouch_last_night_heres_things_i_wish/

Help me recognizing Trigorilla board versions
https://www.reddit.com/r/anycubic/comments/jns8l1/help_me_recognizing_trigorilla_board_versions/

## Other references
https://3dtoday.ru/blogs/darkcats/the-installation-of-the-level-sensor-table-bltouch3dtouch-and-clones-a
