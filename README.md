NanoVNA H4 MS5351
=================

This repository contains a modified build of NanoVNA-D firmware based on version 1.2.52 for the NanoVNA H4 MS5351 variant.

A precompiled firmware image (`H4.bin`) is available in the `/firmware` folder for users who prefer to update their device without rebuilding the project.

Version 1.2.54 includes two changes that restore correct operation with 401 sweep points on my NanoVNA H4 MS5351.

Bug fixes and changes (v1.2.54)
==============================

Fixed an issue in `si5351_set_frequency()` where a change in output drive strength could invalidate the Si5351 register cache and then return early when the frequency remained unchanged. As a result, the updated output configuration was not always written back to the synthesizer.

The fix forces the Si5351 to be reconfigured whenever the output drive strength changes, even if the output frequency does not.

Changed the default MS5351 band threshold from 300 MHz to 250 MHz. This prevents the measurement anomalies observed on the tested H4 MS5351 unit.

On my NanoVNA H4 MS5351, these changes restore correct operation with 401 sweep points and eliminate the measurement artifacts observed in firmware versions v1.2.46 through v1.2.52.

Notes
=====

1. This is an unofficial build based on NanoVNA-D firmware v1.2.52.
2. It has only been tested on the NanoVNA H4 MS5351 variant.
3. After programming the device:
   a. Select **MS5351** in **Config > Expert Settings > More > Mode MS5351**.
   b. Perform a full calibration.