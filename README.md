NanoVNA H4 MS5351
=================
This repository contains NanoVNA-D firmware version 1.2.52 for the NanoVNA H4. A precompiled firmware image (H4.bin) is available in the /firmware folder for users who prefer to update their device without rebuilding the project. The only source code modification made before compilation was changing #define SWEEP_POINTS_MAX 401 to #define SWEEP_POINTS_MAX 351 in nanovna.h. This change was necessary because my NanoVNA H4 (MS5351 variant), originally running firmware v29, showed trace anomalies after upgrading to firmware v46 and later v52. The issue appears to be caused by excessive RAM usage, and reducing the maximum number of sweep points eliminates the problem while preserving normal operation.

2026/07/29
==========

Fixed an issue in si5351_set_frequency() where a change in output drive strength could invalidate the Si5351 register cache and then return early when the frequency was unchanged. As a result, the updated output configuration was not always written back to the device.

The fix forces the synthesizer to be reconfigured whenever the drive strength changes, even if the output frequency remains the same.

This restores correct operation with 401 sweep points on the NanoVNA H4 MS5351 and eliminates the measurement artifacts previously observed.