# Sovol-SV08-Factory-Modified-Klipper
This is a repo for the stock SV08 Image with a lot of configuration enhancements

Imrovements:
- FAN control for the Mainboard FAN as "FAN4" but on PIN: PA1!
- Improvements in the "quad_gantry_level" to enhance the accuracy
- reduce the bed mesh speed and split_delta_z to enhance accuracy of the probing
- changed microsteps from 16 to 64
- reduce the stepper run_currents
- removed the hold_currents
- some more changes for the stepper
- introduction of a "macro_own.cfg", added there an PA interpretation of the M572 which is used by Prusa Mk4(s) to set PA values individually per Filament in the "Filament->Custom G-Code" section of your slicer: eg.: M572 0.035 means a PA Value for this model of 0.035
- Some modifications in the START_PRINT macro to do a nozzle clean and Auto Z-Offset calibration before every print
- changed the AUTO Z-Offset procedure so that no print of this pattern is executed
- changed the crowsnest configuration by doing some camera parameter changes
- Changes in the macro.cfg so that the adaptive bed mesh before every print is executed with the correct bed temperature from slicer, no more with always 65 degree celsius (overtaken/reused from Gergo) For this the Slicer Startcode need to be changed. See below how:


Startcode for Orca Slicer:

M140 S[bed_temperature_initial_layer_single] 

M104 S130 

G28

G90

G1 X0 F9000

G1 Y20

G1 Z0.600 F600

G1 Y0 F9000

START_PRINT

G90

G1 X0 F9000

G1 Y20

G1 Z0.600 F600

G1 Y0 F9000

M400

G91

M83

;M140 S[bed_temperature_initial_layer_single] ;set bed temp

M104 S[nozzle_temperature_initial_layer] ;set extruder temp

M190 S[bed_temperature_initial_layer_single] ;wait for bed temp

M109 S[nozzle_temperature_initial_layer];wait for extruder temp

G1 E25 F300

G4 P1000

G1 E-0.200 Z5 F600

G1 X88.000 F9000

G1 Z-5.000 F600

G1 X87.000 E20.88 F1800

G1 X87.000 E13.92 F1800

G1 Y1 E0.16 F1800

G1 X-87.000 E13.92 F1800

G1 X-87.000 E20.88 F1800

G1 Y1 E0.24 F1800

G1 X87.000 E20.88 F1800

G1 X87.000 E13.92 F1800

G1 E-0.200 Z1 F600

M400


Prusaslicer:

M140 S[first_layer_bed_temperature] ;set bed temp

M104 S130 

G28

G90

G1 X0 F9000

G1 Y20

G1 Z0.600 F600

G1 Y0 F9000

START_PRINT

G90

G1 X0 F9000

G1 Y20

G1 Z0.600 F600

G1 Y0 F9000

M400

G91

M83

;M140 S[first_layer_bed_temperature] ;set bed temp

M104 S[first_layer_temperature[initial_tool]] ;set extruder temp

M190 S[first_layer_bed_temperature] ;wait for bed temp

M109 S[first_layer_temperature[initial_tool]];wait for extruder temp

G1 E25 F300

G4 P1000

G1 E-0.200 Z5 F600

G1 X88.000 F9000

G1 Z-5.000 F600

G1 X87.000 E20.88 F1800

G1 X87.000 E13.92 F1800

G1 Y1 E0.16 F1800

G1 X-87.000 E13.92 F1800

G1 X-87.000 E20.88 F1800

G1 Y1 E0.24 F1800

G1 X87.000 E20.88 F1800

G1 X87.000 E13.92 F1800

G1 E-0.200 Z1 F600

M400



