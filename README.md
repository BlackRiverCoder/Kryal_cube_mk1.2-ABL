# Kryal_cube_mk1.2-ABL

+ Today I am building ABL sensor to 3d printer Kryal Cube mk1.2 
+ In this solution we're using Z Endstop as calibration switch that means, we don't need Z Endstop anymore
+ Calibration will starts before every print
+ The disadvantage is that you must insert the sensor next to extruder and after calibration remove it

## Manuals to install ABL on Kryal Cube mk1.2:
 
**- 1.)** [English manual](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Manuals/English_manual.txt)

**- 2.)** [Slovak Manual](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Manuals/Slovak_manual.txt)

## Models:

+ * *Right side model with original extruder: (ModelR-O v1.0)* *
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

 - 3.) **Connect cable to the main board:**
    - Pull the cable along 3d printer case, from extruder, where you make another (male type) connector, to the main board
    - Kryal Cube mk1.2 using AtMega2560 with RAMPS14, so connect the switch to this connector:
   ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/RAMPS14.png)

 - **Final calibration sensor attached next to the extruder:**
   ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/attached%20sensor.png)

***2.) Firmware configuration:***
 > [!IMPORTANT]
 > Marlin version - 2.0.9.2, in other versions settings can be different.
 - 1.) **Disabling settings:**
   - If you have enabled any these settings, please disable them using // before every **#define**:
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
  > [!CAUTION]
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
          - !! Read troubleshooting !! - how many times calibration is performed
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
      
          
          
          
          


## Photos:
