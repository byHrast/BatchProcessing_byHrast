# BatchProcessing_byHrast

A PixInsight script that processes your masters automatically and without supervision.

One window holds a row for Ha, OIII, SII, L, R, G, B and for an already combined RGB image. Assign a master to each row, keep the processes you want, and click **Process** once. The script then runs every filter through its steps, one after another.

![BatchProcessing_byHrast dialog](https://pixinsight.hrastro.com/images/batchprocessing-dialog.png)

## Features

- One row per filter. The row decides the channel, not the file name.
- An empty row is skipped.
- Every process has a checkbox. Unchecked processes are skipped.
- Each process has its own parameters for every filter. Settings for Ha do not change OIII, and settings for R do not change G or B.
- Settings are saved and come back the next time you start the script.
- For Ha, OIII and SII, flux calibration uses the wavelength and bandwidth of the filter, plus the camera QE curve.
- If one filter fails, the others are still processed.
- Processes that are not installed are shown as not installed and skipped.
- Files on disk are never overwritten. The open images are processed in place.

## Default order

**Ha, OIII, SII, L, R, G, B**

1. BlurXTerminator, Correct Only
2. ImageSolver
3. SpectrophotometricFluxCalibration
4. MultiscaleGradientCorrection
5. BlurXTerminator
6. NoiseXTerminator
7. StarXTerminator
8. ScreenTransferFunction
9. MultiscaleAdaptiveStretch

**RGB**

1. BlurXTerminator, Correct Only
2. ImageSolver
3. SpectrophotometricFluxCalibration
4. MultiscaleGradientCorrection
5. SpectrophotometricColorCalibration
6. BlurXTerminator
7. NoiseXTerminator
8. StarXTerminator
9. ScreenTransferFunction
10. MultiscaleAdaptiveStretch

ScreenTransferFunction only changes the display. MultiscaleAdaptiveStretch stretches the pixels, and the display is reset afterwards.

## Requirements

- PixInsight 1.9.5
- BlurXTerminator, NoiseXTerminator and StarXTerminator by RC Astro are optional. Without them those steps are skipped.
- MultiscaleGradientCorrection needs the MARS database set up in PixInsight.

## Installation

Install it through the PixInsight update system:

1. In PixInsight open **Resources → Updates → Manage Repositories**.
2. Add `https://pixinsight.hrastro.com`
3. Open **Resources → Updates → Check for Updates**, select **BatchProcessing_byHrast** and click **Apply**.
4. Close PixInsight to finish the installation.
5. Run it from **Script → Batch Processing → BatchProcessing_byHrast**.

The repository is not signed, so PixInsight warns before using it. **Edit → Global Preferences → Security → Allow unsigned update repositories** must be enabled.

## Usage

1. Open your masters in PixInsight.
2. Start the script.
3. Drop each image onto its row, or pick it from the list.
4. Open **Steps** under a row, check the processes you want, and use **Settings** to adjust their parameters for that filter.
5. Click **Process**.

The console shows each filter and step as it runs. At the end the script lists the processed filters and any that stopped.

## Links

- Website: https://pixinsight.hrastro.com
- Astrophotography: https://www.hrastro.com

## Author

Matija Pozojevic (HrAstro)
