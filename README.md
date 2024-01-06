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
     

## Photos:

   


