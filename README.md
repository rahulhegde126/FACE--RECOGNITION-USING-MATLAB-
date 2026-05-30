# Non-ML Face Authentication System

A purely Digital Signal Processing (DSP) approach to face matching implemented in **MATLAB**. 

This project strictly avoids Machine Learning (ML) techniques, relying instead on classical image processing, spatial feature extraction, and spectral analysis to authenticate a user.

## How It Works

The authentication pipeline consists of three main stages:

1. **Image Capture & Preprocessing**
   - Captures live reference and test images via Webcam.
   - Converts to Grayscale and standardizes the size to 256×256.
   - Applies **Wiener filtering** (noise reduction) and **Adaptive Histogram Equalization** (local contrast enhancement).

2. **Feature Extraction**
   - **LBP (Local Binary Patterns):** Extracts micro-texture features of the face.
   - **2D DFT (Discrete Fourier Transform):** Extracts the low-frequency spectral components (32×32) to capture broad facial geometry in the frequency domain.

3. **Similarity Scoring**
   - Calculates **SSIM (Structural Similarity Index)** using a custom Gaussian window to evaluate luminance, contrast, and structure.
   - Calculates **NCC (Normalized Cross-Correlation)** for both the LBP and DFT features.

---

## Requirements

To run this script, you need MATLAB installed with the following add-ons:
- Image Processing Toolbox
- Computer Vision Toolbox
- MATLAB Support Package for USB Webcams

---

## Usage

1. Open and run the script in the MATLAB environment.
2. Look at the webcam and press **Enter** (or any key) in the command window when prompted to capture the **Reference Image**.
3. Look at the webcam again and press **Enter** when prompted to capture the **Test Image**.
4. The command window will output the individual metric scores and display a final `✅ Faces Match!` or `❌ Faces Do Not Match.` verdict.
5. A figure window will automatically open showing the original faces side-by-side with their 2D DFT spectra.

---

## System Parameters & Weights

```matlab
% Preprocessing
Image_Size = [256, 256];
Wiener_Window = [5 5];

% DFT Extraction
Low_Freq_Grid = 1:32;

% SSIM Calculation
Gaussian_Window = [11 11];
Gaussian_Sigma = 1.5;

% Final Match Score Weights
Weight_SSIM = 0.4;  % 40% contribution
Weight_LBP  = 0.3;  % 30% contribution
Weight_DFT  = 0.3;  % 30% contribution

% Authentication Threshold
Match_Threshold = 0.70; % > 70% required for a positive match
