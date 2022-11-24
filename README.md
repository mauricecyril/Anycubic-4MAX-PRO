# Anycubic-4MAX-PRO
Settings and Notes Related to the Anycubic 4Max Pro 3D Printer.

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
    
    
    
# Octoprint Settings


# Sources

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

## Reddit
BLtouch on an Anycubic 4Max Pro
https://www.reddit.com/r/3Dprinting/comments/g8tto3/bltouch_on_an_anycubic_4max_pro/

Installed BLTouch last night. Here's things I wish I'd known.
https://www.reddit.com/r/ender3/comments/c6n02e/installed_bltouch_last_night_heres_things_i_wish/
