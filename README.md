# NanoVNA H4 MS5351

This repository contains a modified build of NanoVNA-D firmware version 1.2.54
for the NanoVNA H4 MS5351 variant.

A precompiled firmware image (`H4.bin`) is available in the `/firmware` folder
for users who prefer to update their device without rebuilding the project.

# Changes

This build includes two modifications related to the MS5351 synthesizer.

## Si5351 output drive reconfiguration

Fixed an issue in `si5351_set_frequency()` where a change in output drive
strength could invalidate the Si5351 register cache and then return early when
the frequency remained unchanged.

As a result, the updated output configuration was not always written back to
the synthesizer.

The modification forces the Si5351 to be reconfigured whenever the output
drive strength changes, even if the output frequency does not.

## MS5351 band threshold

Changed the default MS5351 band threshold from 300 MHz to 250 MHz.

# Testing

The firmware has been tested on my NanoVNA H4 MS5351 with 401 sweep points.

During earlier tests I observed measurement artifacts with some firmware
versions. However, these artifacts can no longer be reproduced. I have since
reflashed and successfully tested versions 1.2.40, 1.2.46 and 1.2.54, as well
as this modified v1.2.54 build, and all of them currently operate correctly
on the same unit.

The earlier problems may therefore have been related to the device
configuration or to a persistent state rather than to a particular firmware
version.

# Notes

1. This is an unofficial build of NanoVNA-D firmware v1.2.54.
2. It has only been tested on my NanoVNA H4 MS5351.
3. A precompiled `H4.bin` is provided for convenience.
4. After programming the device, verify that **MS5351** is selected under
   **Config > Expert Settings > More > Mode MS5351**.
5. Perform a full calibration after updating the firmware.