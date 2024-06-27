# Kryal_cube_mk1.2-ABL

+ Today I am building ABL sensor to 3d printer Kryal Cube mk1.2 
+ In this solution we're using Z Endstop as calibration switch that means, we don't need Z Endstop anymore
+ Calibration will start before every print
+ The disadvantage is that you must install the sensor next to the extruder and after calibration remove it

## Repository architecture:
 - [**Manuals**](#manuals-to-install-abl-on-kryal-cube-mk12)
 - [**Models**](#models)
 - [**Nozzle_to_probe_offset**](#nozzle_to_probe_offset)
 - [**Troubleshooting**](#troubleshooting)
 - [**Sources**](#sources)
 - [**Troubleshooting Sources**](#troubleshooting-sources)

## Manuals to install ABL on Kryal Cube mk1.2:
 
**- 1.)** [English manual](#english-manual)

**- 2.)** [Slovak Manual](#slovak-manual)

## Models:

  - Formats: **.stl** and for SolidWorks **.sldprt**

+ **Right side model with original extruder: ([ModelR-O v1.0](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models/ModelR-O%20v1.0))**
![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/ModelR-O%20v1.0.png)

+ **Left side model with original extruder: ([ModelL-O v1.0](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models/ModelL-O%20v1.0))**
![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/ModelL-O%20v1.0.png)

+ **Left side model with E3D extruder: ([ModelL-E3D v1.0](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models/ModelL-E3D%20v1.0))**
![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/ModelL-E3D%20v1.0.png)

## English Manual:

***1.) Hardware preparation:***
 - 1.) **Things we need:**
    - NC Switch
    - Cables
    - Switch holder (according to the side on which the switch will be and according to the extruder type) you can download models [here](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models) and every model types and images are [here](#models)
    - Some connectors
    - Screws to attach the switch to the holder
    - Magnets 6x3mm (for magnet type ABL)

 - 2.) **Assembling the holder:**
    **Fixed type:**
    - 1.) Solder wires to the C and NC on the switch and at the end of the cable make connector of your choice (as you can see in the red circle (female type))
    - 2.) With the screws attach the switch to the 3d printed model
    - _Your holder should look like this one:_
    ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/sensor%20with%20holder%20installed.png)

    **Magnet type:**
    > [!ATTENTION]
    > Double check the magnet faces, if you don't put them in correct way, they won't snap together 
    - 1.) Insert magnets to both models
    - 2.) Attach the microswitch to the microswitch holder and put screws to hold it
    - 3.) Attach cables to the main holder

 - 3.) **Connect cables to the main board:**
    - Pull the cable along 3d printer case, from extruder, where you make another (male type) connector, to the main board
    - Kryal Cube mk1.2 using AtMega2560 with RAMPS14, so connect the switch to these pins:
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
        
      - **Configuration_adv.h**
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
          #define Z_HOMING_HEIGHT  30
          ```
          ```
          #define Z_AFTER_HOMING   20
          ```
        - ABL:
          - -left +right; -front +back; -down (our solution only has down); these settings can be found [here](#nozzle_to_probe_offset)
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
          - safe distance from each edge of the bed
          ```
          #define PROBING_MARGIN 6
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
          #define Z_AFTER_PROBING            30
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
        - This is coreXY 3d printer, so BABYSTEP Graphic Overlay is flipped (Symbol up = bed down; Symbol down = bed up)
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
 > If you have been using the Z Probe settings, reset them via "Configuration", "Restore Settings" and then "Store Settings" on the 3d printer display!
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
 > Use G28 X Y and G28 Z separately, instead of G28 (More info in [troubleshooting](#troubleshooting)).

 - Commands M140, M190, M104 and M109 can be different from slicer you're using. (I am using PrusaSlicer)

 ```
 M0 Install Sensor ; Printer will wait until you install the sensor to the printer

 G28 X Y ; Home X Y
 G28 Z ; Home Z

 M140 S[first_layer_bed_temperature] ; Set bed temperature
 M190 S[first_layer_bed_temperature] ; Wait for bed temperature

 G29 ; Calibration

 M0 Remove Senzor ; Printer will wait until you remove the sensor from printer
 ```
 > [!TIP]
 > Set nozzle temperature after calibration.

 ```
 M104 S[first_layer_temperature] T0; Set nozzle temperature
 M109 S[first_layer_temperature] T0; Wait for nozzle temperature
 ```

## Slovak Manual:

***1.) Príprava hardware:***
 - 1.) **Veci, ktoré budeme potrebovať:**
    - NC Spínač
    - Káble
    - Držiak spínača (podľa strany, kde spínač bude a podľa typu extrudera) si môžeš stiahnuť modely [tu](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models) a pozrieť si každý model s obrázkami [tu](#models)
    - Konektory
    - Šrubky na prichitenie spínača na držiak
    - Magnety 6x3mm (pre magnetický typ ABL)

 - 2.) **Skladanie držiaku snímača:**
    **Pevný typ:**
    - 1.) Prispájkovať káble na C a NC na spínači a na konci kábla urobiť konektor tvojej voľby (viď. červený kruh (female type))
    - 2.) Pomocou šrubiek pripevniť spínač na 3d vytlačený držiak
    - _Malo by to vyzerať nejako takto:_
    ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/sensor%20with%20holder%20installed.png)

    **Magnetický typ:**
    > [!ATTENTION]
    > Dvakrát skontroluj otočenie magnetov, ak sa dajú opačne, neprichytia sa o seba
    - 1.) Vlož magnety do obidvoch modelov
    - 2.) Pripevni microspínač do držiaka microspínača a upevni ho šrubami
    - 3.) Pripevni káble do hlavného modelu

  - 3.) **Pripojenie káblov k základnej doske:**
     - Natiahni káble pozdĺž rámu 3d tlačiarne, od extrudera, kde urobíš opačný konektor pre kábel (male type) k základnej doske
     - Kryal Cube mk1.2 používa AtMega2560 s RAMPS14, takže spínač zapojíme na tieto piny:
     ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/RAMPS14.png)

  - **Ukážka pripevneného senzora vedľa extrudera:**
     ![](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/blob/main/Assests/Images/attached%20sensor.png)

***2.) Configurácia Firmware:***
 > [!IMPORTANT]
 > Marlin verzia - 2.0.9.2, v iných verziách môžu byť nastavenia iné.
 - 1.) **Vypínanie nastavení:**
   - Ak máš v Marline povolené niečo z týchto nastavení, prosím vypni ich pomocou // pred každým **#define**:
      - **Configuraion.h**
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

      - **Configuration_adv.h**
        ```
        #define BABYSTEP_DISPLAY_TOTAL
        ```
> [!WARNING]
> Ak nevypneš tieto nastavenia a dáš build code, môžu nastať chyby!

 - 2.) **Povoľovanie/konfigurácia nastavení:**
    - Nastavenia povolíš vymazaním // pred každým **#define**
      - **Configuration.h**
        - !! Nastav veľkosti, kde je tryska bezpečne nad podložkou a veľkosť podložky, tieto nastavenia nájdeš [tu]() !!
        - EEPROM nastavenia:
          ```
          #define EEPROM_SETTINGS
          ```
          ```
          #define EEPROM_AUTO_INIT
          ```
        - Z Safe Homing:
          ```
          #define Z_SAFE_HOMING
          ```
          ```
          #define Z_HOMING_HEIGHT  30
          ```
          ```
          #define Z_AFTER_HOMING   20
          ```
        - ABL:
          - -vľavo +vpravo; -dopredu +dozadu; -dole (naše riešenie bude mať hodnotu len -dole, nie hore); tieto nastavenia nájdeš [tu](#nozzle_to_probe_offset)
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
          - x*x = počet kalibračných bodov
          ```
          #define GRID_MAX_POINTS_X x
          ```
          - bezpečná vzdialenosť od každého kraja podložky
          ```
          #define PROBING_MARGIN 6
          ```
          ```
          - #define MULTIPLE_PROBING 2
          ```
          - vyššia rýchlosť = menej presná kalibrácia
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
          #define Z_AFTER_PROBING            30
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
        - Keďže táto tlačiareň je coreXY, BABYSTEP Graphic Overlay je otočený (Symbol hore = bed dole; Symbol dole = bed hore)
        ```
        #define BABYSTEP_ZPROBE_GFX_OVERLAY
        ```
        - Pri pokuse o kalibráciu sa na poslednom riadku hlava extrudéra otierala o zadnú časť rámu 3d tlačiarne, takže nastavujem limit zo zadnej strany
        ```
        #define PROBING_MARGIN_BACK PROBING_MARGIN +15
        ```
        ```
        #define DEFAULT_STEPPER_DEACTIVE_TIME 400
        ```

***3.) Build a flashovanie firmware:***
 > [!WARNING]
 > Ak si používal Z Probe nastavenia, resetuj ich cez "Configuration", "Restore Settings" a potom "Store Settings" na displeji 3d tlačiarne!
 > Zabrániš tak veľa problémom!

 > [!CAUTION]
 > Flashovanie firmware je tá najbezpečnejšia časť, takže všetko 2-krát skontroluj (Kód, USB pripojenie)
 > Počas flahovania musí byť tlačiareň napájaná!
  
 - 1.) **Vo VisualCode klikni na build code, ak bol build úspešný, môžeš flashovať.**

 > [!NOTE]
 > Na tejto tlačiarni s AtMega2560 nepotrebuješ bootloader, takže flashuj s úsmevom :)
 - 2.) **Teraz klikni na flash.**
 - 3.) **Ak bol flash úspešný, reštartuj tlačiareň.**
 - 4.) **Po reštarte tlačiarne choď do "Configuration", "Restore Settings" a potom "Store Settings", takto uložíš nové dáta do pamäte EEPROM**

***4.) Modifikácia GCode:***
 > [!TIP]
 > Používaj G28 X Y a G28 Z zvlášť, namiesto G28 (Viac info [tu](#troubleshooting))

 - Príkazy M140, M190, M104 a M109 sa môžu líšiť od sliceru. (Ja používam PrusaSlicer)

 ```
 M0 Pripevnit Senzor ; Tlačiareň počká, kým nepripevníš senzor

 G28 X Y ; Home X Y
 G28 Z ; Home Z

 M140 S[first_layer_bed_temperature] ; Nastav bed teplotu
 M190 S[first_layer_bed_temperature] ; Počkaj na bed teplotu

 G29 ; Kalibrácia

 M0 Odstranit Senzor; Tlačiareň počká, kým neodstrániš senzor
 ```
 > [!TIP]
 > Nastav teplotu trysky po kalibrácii.

 ```
 M104 S[first_layer_temperature] T0; Nastav teplotu trysky
 M109 S[first_layer_temperature] T0; počkaj na teplotu trysky
 ```

## Nozzle_to_probe_offset:
**[ModelL-O v1.0](https://github.com/BlackRiverCoder/Kryal_cube_mk1.2-ABL/tree/main/Assests/Models/ModelL-O%20v1.0) with original (old) extruder:**
 - -left +right; -front +back; -down (our solution only has down);
  - Switch is 32mm left from the nozzle, so the first value will be **-32**
  - Switch is 15mm back from the nozzle, so the second value will be **-15**
  - Switch is 7mm under the nozzle, so the third value will be **-7**
  ```
  #define NOZZLE_TO_PROBE_OFFSET { -32, -15, -7 }
  ```

**[ModelL-E3D v1.0]() with E3D extruder:**
 - -left +right; -front +back; -down (our solution only has down);
  - Switch is 36mm left from the nozzle, so the first value will be **-36**
  - Switch is 10mm back from the nozzle, so the second value will be **-10**
  - Switch is 13mm under from the nozzle, so the third value will be **-13**
  ```
  #define NOZZLE_TO_PROBE_OFFSET { -36, -10, -13 }
  ```
 > [!TIP]
 > For E3D extruder you can change this setting in **Configuration_adv.h** to +10:
  ```
  #define PROBING_MARGIN_BACK PROBING_MARGIN +10
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
