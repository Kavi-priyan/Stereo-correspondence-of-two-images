# 🛰️ Stereo Correspondence using OpenCV

This project demonstrates how to compute **stereo correspondence** (disparity map) between two stereo images using **Python** and **OpenCV**.
Stereo correspondence is a key step in **3D vision**, allowing estimation of **depth information** from a pair of 2D images captured from slightly different viewpoints.

---

## 📸 Overview

Given two rectified stereo images — typically a **left** and **right** view from a stereo camera — the algorithm:

1. Matches corresponding pixels between both images.
2. Computes the **disparity map**, where pixel intensity represents the difference in horizontal position.
3. (Optionally) Converts disparity into **depth** using camera parameters.

---

## 🚀 Features

* Stereo Block Matching (BM) and Semi-Global Block Matching (SGBM) methods.
* Normalized disparity visualization using color mapping.
* Easily adaptable for calibrated camera setups.
* Optional extension for 3D reconstruction from disparity.

---

## 🧩 Requirements

Install dependencies with:

```bash
pip install opencv-python matplotlib numpy
```

---

## 💻 Usage

1. Place your stereo image pair in the project folder:

   ```
   im2.png
   im6.png
   ```
2. Run the script:

   ```bash
   python stereo_correspondence.py
   ```
3. View the results:

   * Left image
   * Disparity map (color-coded)

---

## 🧠 Example Code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

left = cv2.imread('left.jpg', cv2.IMREAD_GRAYSCALE)
right = cv2.imread('right.jpg', cv2.IMREAD_GRAYSCALE)

stereo = cv2.StereoBM_create(numDisparities=16*6, blockSize=15)
disparity = stereo.compute(left, right)
disp_norm = cv2.normalize(disparity, None, 0, 255, cv2.NORM_MINMAX, cv2.CV_8U)

plt.imshow(disp_norm, cmap='jet')
plt.title('Disparity Map')
plt.colorbar()
plt.show()
```

---

## 🧮 (Optional) Depth and 3D Reconstruction

If you have the stereo camera calibration data (`Q` matrix), you can reproject the disparity to 3D:

```python
points_3D = cv2.reprojectImageTo3D(disparity, Q)
```

This produces real-world (X, Y, Z) coordinates for each pixel.

---

## 🧑‍💻 Author

**Kavi Priyan**
Project built for exploring stereo vision and 3D reconstruction techniques using OpenCV.

---

## 📚 References

* [OpenCV Stereo Matching Documentation](https://docs.opencv.org/master/dd/d53/tutorial_py_depthmap.html)
* [Stereo Vision Concepts – Wikipedia](https://en.wikipedia.org/wiki/Stereo_vision)

---
