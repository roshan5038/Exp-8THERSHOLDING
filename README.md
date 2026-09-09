# EX 8 Thresholding Techniques Using OpenCV

## Aim

To write a Python program using OpenCV to perform image thresholding techniques and compare the results of **Global Thresholding, Adaptive Thresholding, and Otsu's Thresholding**.

---

## Experiment Details

- **Experiment No.:** 8
- **Experiment Name:** Thresholding
- **Name:** Roshan V 
- **Register No.:** 212225230232

---

## Learning Objective

The objectives of this experiment are:

- To understand image thresholding.
- To convert a color image into grayscale.
- To perform Global Thresholding.
- To perform Adaptive Thresholding.
- To perform Otsu's Thresholding.
- To compare different thresholding techniques.

---

## Software Used

- Anaconda – Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (`cv2`)
- NumPy
- Matplotlib

---

## Libraries Used

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

# Algorithm

## Step 1: Import Required Libraries

Import OpenCV, NumPy, and Matplotlib.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

## Step 2: Read the Image and Convert to Grayscale

The input image **`chip.png`** is read using OpenCV and converted from BGR to grayscale.

```python
image = cv2.imread('chip.png')
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

The grayscale image is used as the input for the thresholding operations.

---

## Step 3: Display the Original Image

The original image is displayed using Matplotlib.

```python
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')
```

### Output – Original Image

<img width="105" height="158" alt="image" src="https://github.com/user-attachments/assets/3c1b8237-07e6-4cf2-a5ba-80a07a53d7a8" />


---

# Step 4: Global Thresholding

Global thresholding is applied using a fixed threshold value of **127**.

```python
_, global_thresholded = cv2.threshold(
    gray_image,
    127,
    255,
    cv2.THRESH_BINARY
)
```

The threshold value used is:

**127**

Pixels are classified into two groups based on this fixed threshold.

### Output – Global Thresholding

<img width="146" height="186" alt="image" src="https://github.com/user-attachments/assets/7328d037-3355-4229-a90a-c0f640289b5f" />


---

# Step 5: Adaptive Thresholding

Adaptive thresholding is applied using the **Gaussian method**.

```python
adaptive_thresholded = cv2.adaptiveThreshold(
    gray_image,
    255,
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)
```

The parameters used in the notebook are:

| Parameter | Value |
|---|---:|
| Maximum value | 255 |
| Adaptive method | `ADAPTIVE_THRESH_GAUSSIAN_C` |
| Threshold type | `THRESH_BINARY` |
| Block size | 11 |
| Constant C | 2 |

Adaptive thresholding calculates the threshold based on local image regions.

### Output – Adaptive Thresholding

<img width="148" height="181" alt="image" src="https://github.com/user-attachments/assets/3a8d92fa-bdd4-48c0-8c27-25b07e3bfc42" />



---

# Step 6: Otsu's Thresholding

Otsu's method is applied to automatically determine an appropriate threshold value.

```python
_, otsu_thresholded = cv2.threshold(
    gray_image,
    0,
    255,
    cv2.THRESH_BINARY + cv2.THRESH_OTSU
)
```

The threshold value is set to `0` because Otsu's method automatically determines the optimal threshold from the image.

### Output – Otsu's Method

<img width="124" height="175" alt="image" src="https://github.com/user-attachments/assets/ac727d00-4819-497e-8ee4-6556082ec6b9" />

---

# Step 7: Display All Results

The notebook displays the original image and all three thresholding results in a **2 × 2 subplot**.

```python
# Global Thresholding
plt.subplot(2, 2, 2)
plt.imshow(global_thresholded, cmap='gray')
plt.title("Global Thresholding")
plt.axis('off')

# Adaptive Thresholding
plt.subplot(2, 2, 3)
plt.imshow(adaptive_thresholded, cmap='gray')
plt.title("Adaptive Thresholding")
plt.axis('off')

# Otsu's Method
plt.subplot(2, 2, 4)
plt.imshow(otsu_thresholded, cmap='gray')
plt.title("Otsu's Method")
plt.axis('off')

plt.tight_layout()
plt.show()
```

---

# Complete Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Read the image and convert to grayscale
image = cv2.imread('chip.png')
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Original Image
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

# Step 3: Use Global Thresholding to segment the image
_, global_thresholded = cv2.threshold(
    gray_image,
    127,
    255,
    cv2.THRESH_BINARY
)

# Step 4: Use Adaptive Thresholding to segment the image
adaptive_thresholded = cv2.adaptiveThreshold(
    gray_image,
    255,
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)

# Step 5: Use Otsu's method to segment the image
_, otsu_thresholded = cv2.threshold(
    gray_image,
    0,
    255,
    cv2.THRESH_BINARY + cv2.THRESH_OTSU
)

# Global Thresholding
plt.subplot(2, 2, 2)
plt.imshow(global_thresholded, cmap='gray')
plt.title("Global Thresholding")
plt.axis('off')

# Adaptive Thresholding
plt.subplot(2, 2, 3)
plt.imshow(adaptive_thresholded, cmap='gray')
plt.title("Adaptive Thresholding")
plt.axis('off')

# Otsu's Method
plt.subplot(2, 2, 4)
plt.imshow(otsu_thresholded, cmap='gray')
plt.title("Otsu's Method")
plt.axis('off')

plt.tight_layout()
plt.show()
```

---

# Working Principle

The complete image-processing pipeline is:

```text
Input Image (chip.png)
        ↓
Convert to Grayscale
        ↓
   ┌────┼─────────────┐
   ↓    ↓             ↓
Global Adaptive      Otsu
   ↓    ↓             ↓
   └────┼─────────────┘
        ↓
Compare Thresholded Images
        ↓
Display Results
```

---

# Thresholding Techniques

## 1. Global Thresholding

Global thresholding uses a single fixed threshold value for the complete image.

In this experiment:

```text
Threshold = 127
```

It is implemented using:

```python
cv2.THRESH_BINARY
```

---

## 2. Adaptive Thresholding

Adaptive thresholding determines the threshold based on local regions of the image.

The notebook uses:

```python
cv2.ADAPTIVE_THRESH_GAUSSIAN_C
```

with:

```text
Block Size = 11
C = 2
```

This method can be useful when different regions of an image have different illumination levels.

---

## 3. Otsu's Method

Otsu's method automatically determines a threshold value from the image.

It is implemented using:

```python
cv2.THRESH_BINARY + cv2.THRESH_OTSU
```

The threshold value supplied to the function is `0`, allowing Otsu's method to calculate the threshold automatically.

---

# Comparison

| Method | Threshold Selection | Main Characteristic |
|---|---|---|
| Global Thresholding | Fixed value: 127 | Uses one threshold for the entire image |
| Adaptive Thresholding | Local regions | Uses locally calculated thresholds |
| Otsu's Method | Automatically calculated | Automatically selects an optimal threshold |

---

# Expected Output

The final Matplotlib figure contains four outputs:

1. **Original Image**
2. **Global Thresholding**
3. **Adaptive Thresholding**
4. **Otsu's Method**

### Final Output Screenshot

> **Paste the complete 2×2 output screenshot here**
>
> **[ INSERT FINAL OUTPUT IMAGE HERE ]**

---

# Applications

Image thresholding is commonly used in:

- Image segmentation
- Object detection
- Document processing
- Character recognition
- Industrial inspection
- Image preprocessing
- Binary image generation

---

# Advantages

### Global Thresholding

- Simple to implement.
- Fast for processing images.
- Works well when image illumination is relatively uniform.

### Adaptive Thresholding

- Handles varying illumination.
- Uses local image information.
- Useful for images with non-uniform lighting.

### Otsu's Method

- Automatically selects the threshold.
- Reduces the need for manually selecting a threshold value.
- Useful for separating foreground and background in suitable images.

---

# Limitations

### Global Thresholding

- A single threshold may not work well when illumination varies across the image.

### Adaptive Thresholding

- Requires selection of block size and constant values.
- Can be computationally more expensive than simple global thresholding.

### Otsu's Method

- Works best when the image has suitable foreground and background intensity distributions.
- May not perform well on complex images with multiple intensity regions.

---

# Result

Thus, the image thresholding techniques **Global Thresholding, Adaptive Thresholding, and Otsu's Method** were successfully implemented using OpenCV.

The input image `chip.png` was converted to grayscale and segmented using the three thresholding methods. The resulting images were displayed together for comparison.

---

## Developed By

**Name:** Roshan V

**Register No:** 212225240124
