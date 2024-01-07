# Kryal_cube_mk1.2-ABL

+ Today I am building ABL sensor to 3d printer Kryal Cube mk1.2 
+ In this solution we're using Z Endstop as calibration switch that means, we don't need Z Endstop anymore
+ Calibration will starts before every print
+ The disadvantage is that you must install the sensor next to the extruder and after calibration remove it

## Repository architecture:
 - [**Manuals**](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#manuals-to-install-abl-on-kryal-cube-mk12)
 - [**Models**](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#models)
 - [**Troubleshooting**](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#troubleshooting)
 - [**Sources**](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#sources)
 - [**Troubleshooting Sources**](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#troubleshooting-sources)

## Manuals to install ABL on Kryal Cube mk1.2:
 
**- 1.)** [English manual](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL?tab=readme-ov-file#english-manual)

**- 2.)** [Slovak Manual](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Manuals/Slovak_manual.txt)

## Models:

+ **Right side model with original extruder: (ModelR-O v1.0)***
![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/ModelR-O%20v1.0.png)

## English Manual:

***1.) Hardware preparation:***
 - 1.) **Things we need:**
    - NC Switch
    - Cables
    - Switch holder (according to the side on which the switch will be and according to the extruder type) download models [here](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models) and every model types and images are [here](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#models)
    - Some connectors
    - Screws to attach the switch to the holder

 - 2.) **Assembling the holder:**
    - 1.) Solder wires to the NC Switch and at the end of the cable make connector of your choice (as you can see in the red circle (female type))
    - 2.) With the screws attach the switch to the 3d printed model
    - _Your holder should look like this one:_
    ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/sensor%20with%20holder%20installed.png)

 - 3.) **Connect cables to the main board:**
    - Pull the cable along 3d printer case, from extruder, where you make another (male type) connector, to the main board
    - Kryal Cube mk1.2 using AtMega2560 with RAMPS14, so connect the switch to this connector:
   ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/RAMPS14.png)

 - **Final - calibration sensor installed next to the extruder:**
   ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/attached%20sensor.png)

***2.) Firmware configuration:***
 > [!IMPORTANT]
 > Marlin version - 2.0.9.2, in other versions settings can be different.
 - 1.) **Disabling settings:**
   - If you have enabled any of these settings, please disable them using // before every **#define**:
      - **Configuration.h**
        ```
        #define PROBE_MANUALLY
        ```
        ```
        #define AUTO_BED_LEVELING_3POINT
        ```
        ```
        #define AUTO_BED_LEVELING_LINEAR
        ```
        ```
        #define AUTO_BED_LEVELING_UBL
        ```
        ```
        #define MESH_BED_LEVELING
        ```
        ```
        #define RESTORE_LEVELING_AFTER_G28
        ```
        ```
        #define ENABLE_LEVELING_AFTER_G28
        ```
        ```
        #define LCD_BED_LEVELING
        ```
        
      - **Configuration_adv-h**
        ```
        #define BABYSTEP_DISPLAY_TOTAL
        ```
 > [!WARNING]
 > If you don't disable these settings and try to build the code, you can get errors!

 - 2.) **Enabling/configuring settings:**
    - Enable settings removing // before **#define**
      - **Configuration.h**
        - !! Set dimensions where the nozzle is safely on the bed and bed sizes, these settings can be found [here]() !!
        - EEPROM settings:
          ```
          #define EEPROM_SETTINGS
          ```
          ```
          #define EEPROM_AUTO_INIT
          ```
        - Z Safe homing:
          ```
          #define Z_SAFE_HOMING
          ```
          ```
          #define Z_HOMING_HEIGHT  20
          ```
          ```
          #define Z_AFTER_HOMING   10
          ```
        - ABL:
          - -left +right; -front +back; -down (our solution only has down); these settings can be found [here]()
          ```
          #define NOZZLE_TO_PROBE_OFFSET { -32, -15, -7 }
          ```
          ```
          #define AUTO_BED_LEVELING_BILINEAR
          ```
          ```
          #define FIX_MOUNTED_PROBE
          ```
          ```
          #define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
          ```
          - x*x = number of calibrating points
          ```
          #define GRID_MAX_POINTS_X x
          ```
          - x = this setting can be found [here]()
          ```
          #define PROBING_MARGIN x
          ```
          ```
          - #define MULTIPLE_PROBING 2
          ```
          - higher speed = more inaccurate calibration
          ```
          #define Z_PROBE_FEEDRATE_SLOW (Z_PROBE_FEEDRATE_FAST / 3)
          ```
          ```
          #define Z_CLEARANCE_DEPLOY_PROBE   10
          ```
          ```
          #define Z_CLEARANCE_BETWEEN_PROBES 10
          ```
          ```
          #define Z_CLEARANCE_MULTI_PROBE     3
          ```
          ```
          #define Z_AFTER_PROBING            20
          ```
          ```       
          #define Z_PROBE_LOW_POINT          -5
          ```

      - **Configuration_adv.h**
        ```
        #define BABYSTEPPING
        ```
        ```
        #define DOUBLECLICK_FOR_Z_BABYSTEPPING
        ```
        ```
        #define BABYSTEP_ZPROBE_OFFSET
        ```
        - This is XYcore 3d printer, so BABYSTEP Grafic Overlay is flipped (Symbol up = bed down; Symbol down = bed up)
        ```
        #define BABYSTEP_ZPROBE_GFX_OVERLAY
        ```
        - When trying to calibrate, on the last line the extruder head was rubbing against the back of the 3d printer frame, so I'm setting the limit from the back side
        ```
        #define PROBING_MARGIN_BACK PROBING_MARGIN +15
        ```
        ```
        #define DEFAULT_STEPPER_DEACTIVE_TIME 400
        ```
      
***3.) Building and flashing the firmware:***
 > [!WARNING]
 > If you used Z Probe setting, please on 3d printer's display under "Configuration", "Restore Setting" and than "Store settings"!
 > You can avoid many problems!

 > [!CAUTION]
 > Flashing the firmware is the most dangerous part, so double-check everything! (Code, USB connection).
 > While flashing, printer must be powered up!

 - 1.) **In VisualCode click build code, if the build is successful, you can write.**

 > [!NOTE]
 > On this printer with AtMega2560 you don't need bootloader, so flash with smile :)
 - 2.) **Now click flash.**
 - 3.) **If the flash was successful, restart the printer.**
 - 4.) **After printer starts up, go to "Configuration", "Restore Setting" and than "Store Settings", with these you store new settings to EEPROM**

***4.) Modify start GCode:***
 > [!TIP]
 > Use G28 X Y and G28 Z separately, instead of G28 (More info in [troubleshooting](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main?tab=readme-ov-file#troubleshooting)).

 - Commands M140, M190, M104 and M109 can be different from slicer you're using. (I am using PrusaSlicer)

 ```
 M0 Install Sensor ; Printer will wait until you install the sensor to the printer

 G28 X Y ; Home X Y
 G28 Z ; Home Z

 M140 S[first_layer_bed_temperature] ; Set bed temperature
 M190 S[first_layer_bed_temperature] ; Wait for bed temperature

 G29 ; Calibration

 M0 ; Printer will wait until you remove the sensor from printer
 ```
 > [!TIP]
 > Set nozzle temperature after calibration.

 ```
 M104 S[first_layer_temperature] T0; Set nozzle temperature
 M109 S[first_layer_temperature] T0; Wait for nozzle temperature
 ```

## Troubleshooting:

***M112 Printer Halted - Probing Failed:***
 - 1.) **Make manual calibration of the bed corners and start the calibration once again.**
 > [!TIP]
 > You can enable Bed Tramming in Marlin, so the printer goes to every corner of the bed to infinity:
>#define LEVEL_BED_CORNERS
 - 2.) **Disable Multiple Probing**
   ```
   #define MULTIPLE_PROBING
   ```

***When the bed is too low, homing cannot be performed:***
 - **Use G28 X Y and G28 Z separately, instead of G28**

## Sources:
- https://www.youtube.com/watch?v=HJV82NHOY-0&
- https://www.youtube.com/watch?v=NTvjIOFMs6M

## Troubleshooting sources
- https://www.youtube.com/watch?v=t4tNSk1_Sc8
- https://www.reddit.com/r/ender3v2/comments/uq3aq3/bed_not_pressing_limit_switch_when_auto_homing/
- https://forum.drucktipps3d.de/forum/thread/14381-probe-failed-with-g29-after-initial-installation/
- https://www.3dprintgorilla.com/marlin-firmware-m112-shutdown/
- https://github.com/MarlinFirmware/Marlin/issues/21118
- https://www.reddit.com/r/3Dprinting/comments/ubwuvu/getting_mad_with_bed_size_and_margins_in_marlin/
- https://github.com/MarlinFirmware/Marlin/issues/18033
- https://www.reddit.com/r/ender3v2/comments/mtfxj3/firmware_crash_error_probing_failed/
- https://www.reddit.com/r/ender3/comments/nc2ul2/bltouch_probe_doesnt_touch_bed_on_first_point/
- https://www.reddit.com/r/3Dprinting/comments/g5a4mz/bltouch_not_probing_bed_g29_but_z_homing_works/
