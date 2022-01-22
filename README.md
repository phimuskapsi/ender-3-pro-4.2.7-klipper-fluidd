# ender-3-pro-4.2.7-klipper-fluidd
My headaches lead to writing this so you don't have to go to the levels of research I did.

## Ender 3 Pro Hardware
- 4.2.7 Creality Silent Board (STM 32-bit processor)
- [Dual Z-axis](dual_z_upgrade.md) (no UART ... yet, see UART section)
- Touchscreen upgrade (inactive, not used ... yet)
- Dawnblade Direct Drive Extruder
- Z-blocks/supports
- Yellow Springs

## Klipper Setup:
- RaspberryPi 3B running FluiddPi - https://github.com/fluidd-core/FluiddPI

## Klipper Configuration File
[printer.cfg](printer.cfg)

## Notes about Klipper Config:
### stepper-z section
1. endstop_pin: probe: z_virtual_endstop
   - Only use this if your endstop is replaced by BLTouch!

### blTouch section
1. z-offset: 3.0 
   - This number is not allowed to be negative! 
   - You want a value that will be larger than your gap so that you have room to probe
2. samples: 2
   - You may want to increase this for a better average. This is good value for after you have gotten tolerance very close to 0.0.
3. x/y offset: -43.25/-6
   - These values are different from the 'defaults' you will find around the internet
   - I measured these for *my* machine. You will have to do the same for best results.
   - To measure:
     - Home to the center of your machine
     - Set a piece of tape under the bltouch sensor
     - Take a marker and mark under the sensor on a piece of tape
     - Adjust the axis and track how much you have changed them untile the extruder is directly over the mark!
     - This made a large difference in my bed meshes!

## Calibrating your Bed
1. Go to the Fluidd Console
2. After setting these values, home your printer to the center (```G28```). 
3. Then type ```MANUAL_PROBE```
4. Adjust your z-axis with the 'paper test'.
   - If you get an 'out of range' error with the z, you will need to increase the offset, then start from 1 again.
   - Once you find a good range (adjust as close as you can to 3 significant digits) accept it.
   - Do not reset!
5. Go into the 'tuning' section, home again on this screen, then calibrate
6. View the mesh. A good variance is under 0.100, I try and get as close to 0.05 as I can.

### If your bed is significantly tilted you will need to fix it with the springs or stepper manual advance, then start at 1 again! 
### If you have low / high corners, adjust then start at #1 again!
### YOU CAN NEVER CALIBRATE TOO MUCH!

