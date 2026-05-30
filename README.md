# Non-ML Face Authentication System

This repository contains a face authentication script implemented purely in **MATLAB**.

The system uses:

- A **Webcam** for capturing live reference and test images.
- **Digital Signal Processing (DSP)** techniques exclusively—no Machine Learning (ML) is used.
- **Image Preprocessing filters** (Wiener filtering, Adaptive Histogram Equalization) to normalize inputs.

There are three primary feature extraction metrics combined for the final evaluation:

1. **LBP (Local Binary Patterns)** — for texture correlation.
2. **2D DFT (Discrete Fourier Transform)** — for low-frequency structural matching.
3. **SSIM (Structural Similarity Index)** — calculated via custom Gaussian window filtering.

<img width="800" alt="Face Comparison Figure" src="https://via.placeholder.com/800x400?text=Insert+Face+Comparison+Figure+Here" />

---

## System Parameters & Weights

```matlab
%% Preprocessing Dimensions
IMAGE_WIDTH         = 256;      % Resized width
IMAGE_HEIGHT        = 256;      % Resized height
WIENER_WINDOW       = [5 5];    % Noise reduction filter size

%% Feature Extraction
DFT_LOW_FREQ_SIZE   = 32;       % Extracts 1:32 x 1:32 low-frequency components
SSIM_GAUSS_WINDOW   = [11 11];  % Gaussian filter window
SSIM_SIGMA          = 1.5;      % Gaussian filter standard deviation

%% Final Match Score Weights
WEIGHT_SSIM         = 0.4;      % 40% weight
WEIGHT_LBP          = 0.3;      % 30% weight
WEIGHT_DFT          = 0.3;      % 30% weight

%% Authentication Threshold
MATCH_THRESHOLD     = 0.70;     % > 70% required for a positive match
