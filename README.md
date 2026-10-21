# Exploring Semi-Automatic Brain Image Segmentation Using LiveWire in MeVisLab

## Overview

This educational project explores semi-automatic contour segmentation of a region of interest in a 2D brain image using **MeVisLab** and its **LiveWire** editor. The focus is on understanding how image gradients and a cost image influence the contour path, including what happens when boundaries have weak contrast.

> **Project status:** Work in progress. A complete, validated segmentation mask has not yet been produced. The bright region of interest has not been independently verified as a tumor.

## Tools

- MeVisLab
- `ImageLoad`
- `ColorModeConverter`
- `GaussGradient`
- `Arithmetic`
- `SoCSOLiveWireEditor`
- `SoView2DCSOExtensibleEditor`
- `CSOManager`
- `View2D`

## Workflow

1. Load a 2D brain image (`Tumor0.jpg`, 100 × 100 pixels).
2. Convert the RGB image to grayscale.
3. Calculate gradient magnitude using `GaussGradient` (sigma = 0.8).
4. Construct an experimental cost image with the Arithmetic expression:

   ```text
   1.0 / (1.0 + a)
   ```

   where `a` represents the gradient magnitude. Stronger gradients generally produce lower costs.
5. Feed the cost image into the LiveWire editor and display the contour over the grayscale image.
6. Inspect and manage contour objects (CSOs) using `CSOManager`.

## Key Observation

The LiveWire contour was difficult to guide through an area where the bright region of interest had very little visible contrast with neighboring tissue. Weak intensity transitions can lead to weak gradients, making the desired boundary less attractive to a gradient-based cost function. This illustrates a practical limitation of edge-guided segmentation, especially with a small, low-resolution image.

## Current Limitations

- The source is a small **2D JPEG**, not an original quantitative DICOM scan.
- The image's diagnosis, slice relationships, and availability of expert segmentation annotations have not yet been verified.
- Multiple contour objects were created during experimentation; the main contour remains open near the top.
- No ground-truth comparison or quantitative segmentation evaluation has been performed.

## Next Steps

- Improve visualization and experiment with contrast enhancement.
- Compare alternative cost functions and LiveWire seed-point placement.
- Create one closed contour and generate a binary mask.
- Evaluate against an expert annotation if one is available.

## Repository Contents

Add the following files as they become available:

```text
Brain-Image-Segmentation-with-MeVisLab/
├── README.md
├── Brain_Tumor_LiveWire_Experiment.mlab
└── screenshots/
    ├── network.png
    └── livewire_contour.png
```

The `.mlab` network may reference a local image path that must be updated when opened on another computer. Only upload source images if their dataset license permits redistribution; otherwise, provide a link to the dataset.

## Disclaimer

This is a learning project for medical image processing. It is **not** a clinically validated tumor detection or segmentation system and must not be used for diagnosis or treatment planning.
