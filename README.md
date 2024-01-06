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
      > [!WARNING]
      > For correct working, we need to configure bed area settings!
        - Set dimensions where the nozzle is safely on the bed, these settings can be found [here]()
        - EEPROM settings:
          ```
          #define EEPROM_SETTINGS
          ```
          ```
          #define EEPROM_AUTO_INIT
          ```
        - Safe homing:
          ```
          #define Z_SAFE_HOMING
          ```
          ```
          #define Z_HOMING_HEIGHT  20
          ```
          ```
          #define Z_AFTER_HOMING   10
          ```


## Photos:
