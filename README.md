# Digital Image Processing Lab Repository

Comprehensive, zero-error solutions for the **Digital Image Processing (DIP) Lab** assignments, designed to run natively in **Google Colab** and local Jupyter environments.

---

## 📚 Repository Overview

| Assignment | Topic / Objective | Notebook Link |
| :--- | :--- | :--- |
| **Assignment 1** | Grayscale to Binary Conversion (Mean Intensity & User Threshold) | [Assignment 1.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%201.ipynb) |
| **Assignment 2** | RGB to Grayscale Conversion (Average & User-Weighted Planes) | [Assignment 2.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%202.ipynb) |
| **Assignment 3** | Border Drawing / Image Padding & Image Complement | [Assignment 3.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%203.ipynb) |
| **Assignment 4** | Image Enhancement (Log Transform, Power-Law/Gamma, Contrast Stretching) | [Assignment 4.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%204.ipynb) |
| **Assignment 5** | Histogram Equalization & Histogram Matching (Specification) | [Assignment 5.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%205.ipynb) |
| **Assignment 6** | Spatial Smoothing (Averaging, Chebyshev Max-Weighted, Gaussian) | [Assignment 6.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%206.ipynb) |
| **Assignment 7** | Image Sharpening (Laplacian, Sobel Gradient, Canny, Unsharp Masking) | [Assignment 7.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%207.ipynb) |
| **Assignment 8** | Noise Generation from PDF Equations (Uniform, Gaussian, Erlang, Exponential, Rayleigh) | [Assignment 8.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%208.ipynb) |
| **Assignment 9** | Local Binary Pattern (LBP) & Denoising Filters (Wiener, Median, Gaussian, Bilateral) | [Assignment 9.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%209.ipynb) |
| **Assignment 10**| Adaptive Median Filter (Impulse Noise) & Otsu's Global Segmentation | [Assignment 10.ipynb](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%2010.ipynb) |
| **Assignment 11**| *Pending problem statement / prompt from user* | `Assignment 11.ipynb` |

---

## 🛠️ Assignment Breakdown & Key Implementations

### [Assignment 1: Grayscale to Binary Conversion](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%201.ipynb)
- **Case 1 (Mean Intensity):** Computes $T_{\text{mean}} = \frac{1}{MN} \sum f(x, y)$ and thresholds the image automatically.
- **Case 2 (User Threshold):** Interactive user input $T \in [0, 255]$ with validation.
- **Verification:** Step-by-step scratch binarization verified against OpenCV `cv2.threshold`.
- **Visualization:** Grayscale image, histogram with annotated threshold lines, binary output, and difference map.

### [Assignment 2: RGB to Grayscale Conversion](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%202.ipynb)
- **Case 1 (Average):** $I_{\text{gray}} = \frac{R + G + B}{3}$.
- **Case 2 (User-Weighted):** $I_{\text{gray}} = w_R R + w_G G + w_B B$ where $0 \le w_i \le 1$ and $\sum w_i = 1$.
- **Benchmark:** Comparison against standard ITU-R BT.601 / NTSC luminance ($0.299R + 0.587G + 0.114B$).
- **Visualization:** 3-channel color plane breakdown, average grayscale, and custom-weighted grayscale.

### [Assignment 3: Padding & Image Complement](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%203.ipynb)
- **Part 1 (Border Drawing / Padding):** Inputs border width and desired color; pads both binary and grayscale images using scratch array allocation and `cv2.copyMakeBorder`.
- **Part 2 (Image Complement):** Computes negative image: $I_{\text{comp}} = 255 - I(x, y)$ for grayscale and binary images.
- **Verification:** Validated against `cv2.bitwise_not`.

### [Assignment 4: Spatial Domain Enhancements](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%204.ipynb)
- **Log Transform:** $s = c \cdot \ln(1 + r)$ with $c=1$, dynamic range expansion for dark tones.
- **Power-Law (Gamma) Transform:** $s = c \cdot r^\gamma$ with user-specified $\gamma$ ($< 1$ for brightening, $> 1$ for darkening).
- **Contrast Stretching:** User-defined piecewise linear mapping $[r_1, r_2] \to [s_1, s_2]$ (e.g. $[80, 120] \to [50, 150]$).
- **Visualization:** Mathematical transfer function curves, before/after images, and histograms.

### [Assignment 5: Histogram Equalization & Matching](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%205.ipynb)
- **Histogram Equalization:** From-scratch computation of PDF, CDF, and transformation mapping $s_k = \text{round}(255 \cdot \text{CDF}(r_k))$. Verified against `cv2.equalizeHist`.
- **Histogram Matching (Specification):** Inverts reference image CDF to reshape input image distribution to match a target reference image.
- **Visualization:** Input, reference, and matched images alongside corresponding histograms and CDF curves.

### [Assignment 6: Spatial Smoothing Filters](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%206.ipynb)
- **Averaging Filter:** Un-weighted box filter $h(x, y) = \frac{1}{K^2}$.
- **Weighted Filter:** Filter kernel defined by Chebyshev metric $h(x, y) = \max(|x|, |y|)$.
- **Gaussian Filter:** Isotropic 2D normal distribution $h(x, y) = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}$.
- **Custom 2D Convolution:** Supports user-selectable filter sizes, $\sigma$, and boundary padding modes (`replicate`, `zero`, `reflect`).

### [Assignment 7: Image Sharpening](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%207.ipynb)
- **Laplacian Filter:** 2nd derivative operator $g(x, y) = f(x, y) - \nabla^2 f(x, y)$.
- **Gradient Operators:** 1st derivative Sobel gradient magnitude $G = \sqrt{G_x^2 + G_y^2}$ and multi-stage Canny edge detector.
- **Unsharp Masking:** Blurring using $5 \times 5$ Gaussian filter with $\sigma=3$, subtracting to form mask $g_{\text{mask}} = f - f_{\text{blur}}$, and sharpening $g = f + k \cdot g_{\text{mask}}$.

### [Assignment 8: Noise Generation from First Principles](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%208.ipynb)
- **Equations Derived from Probability Density Functions (PDFs):**
  - **Uniform:** $z = a + (b - a) U$
  - **Gaussian:** Box-Muller transform $z = \mu + \sigma \sqrt{-2\ln U_1}\cos(2\pi U_2)$
  - **Erlang (Gamma):** Sum of $b$ exponential random variables $z = -\frac{1}{a} \sum \ln(U_i)$
  - **Exponential:** Inverse CDF $z = -\frac{1}{a} \ln(1 - U)$
  - **Rayleigh:** Inverse CDF $z = a + \sqrt{-b \ln(1 - U)}$
- **Verification:** Overlaid histogram plots confirming generated noise shapes match theoretical distributions, with image corruption and comparison to built-in generation.

### [Assignment 9: LBP Texture & Denoising Filters](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%209.ipynb)
- **Local Binary Pattern (LBP):** From-scratch 8-neighbor circular/square micro-texture descriptor with 256-bin histogram.
- **Denoising Comparison:** Tests 4 filters on Gaussian and Speckle noise across $3 \times 3$ or $5 \times 5$ windows:
  1. Wiener Filter (`scipy.signal.wiener`)
  2. Median Filter (`cv2.medianBlur`)
  3. Gaussian Filter (`cv2.GaussianBlur`)
  4. Bilateral Filter (`cv2.bilateralFilter`)
- **Quantitative Metrics:** Comprehensive PSNR (dB) and visual matrix comparison.

### [Assignment 10: Adaptive Median & Otsu's Thresholding](file:///Users/meharahuja/Downloads/ip%20lab%20github/Assignment%2010.ipynb)
- **Adaptive Median Filter:** Gonzalez & Woods algorithm dynamically expanding window up to $S_{\text{max}}$, tested on heavy ($30\%$) salt-and-pepper impulse noise. Demonstrates massive PSNR gain over standard median filter.
- **Otsu's Global Thresholding:** From-scratch derivation maximizing between-class variance $\sigma_B^2(k)$. Verified with 100% equivalence to OpenCV's Otsu implementation.

---

## 🚀 How to Run in Google Colab

1. **Direct Upload:** Upload any `Assignment X.ipynb` directly to [Google Colab](https://colab.research.google.com).
2. **Built-in Self-Contained Execution:** Every notebook includes a synthetic benchmark image generator, meaning you can click **Runtime $\to$ Run all** without needing to upload external files!
3. **Custom Image Support:** Each notebook provides helper loading functions so you can upload your own test photos if desired.

### Dependencies
All required libraries are pre-installed in Google Colab:
- `numpy`
- `matplotlib`
- `opencv-python` (`cv2`)
- `scipy`
