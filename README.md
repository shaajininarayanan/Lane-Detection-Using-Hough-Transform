# Line Detection Using Hough Transform – OpenCV

## Aim

To detect lines in an image using OpenCV by applying grayscale conversion, thresholding, Region of Interest (ROI), Canny edge detection, Gaussian blur, and Hough Transform.

## Learning Objectives

- Understand the stages of image processing.
- Learn edge detection using the Canny algorithm.
- Apply Hough Transform to detect lines.
- Draw detected lines on the original image.

## Software Used

- Anaconda – Python
- Jupyter Notebook / VS Code
- OpenCV (`cv2`)
- NumPy
- Matplotlib

## Algorithm & Explanation

### Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### Step 2: Read the Image

```python
image_path = r"C:\Users\acer\images\Eagle_in_Flight.jpg"
img = cv2.imread(image_path)

if img is None:
    raise FileNotFoundError("Image not found. Check the image path.")

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(8, 5))
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")
plt.show()
```

### Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

plt.figure(figsize=(8, 5))
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```

### Step 4: Apply Thresholding

```python
threshold_value, threshold = cv2.threshold(
    gray, 127, 255, cv2.THRESH_BINARY
)

plt.figure(figsize=(8, 5))
plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```

### Step 5: Apply Region of Interest (ROI)

Since the selected image is an eagle image rather than a road image, the entire image is used as the ROI.

```python
mask = np.ones_like(gray, dtype=np.uint8) * 255
roi = cv2.bitwise_and(gray, gray, mask=mask)

plt.figure(figsize=(8, 5))
plt.imshow(roi, cmap="gray")
plt.title("ROI Masked Image")
plt.axis("off")
plt.show()
```

### Step 6: Perform Canny Edge Detection

```python
edges = cv2.Canny(roi, 50, 150)

plt.figure(figsize=(8, 5))
plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```

### Step 7: Apply Gaussian Blur

```python
blurred = cv2.GaussianBlur(edges, (5, 5), 0)

plt.figure(figsize=(8, 5))
plt.imshow(blurred, cmap="gray")
plt.title("Gaussian Blurred Image")
plt.axis("off")
plt.show()
```

### Step 8: Detect Lines Using Hough Transform

```python

lines = cv2.HoughLinesP(
    blurred,
    rho=1,
    theta=np.pi / 180,
    threshold=50,
    minLineLength=30,
    maxLineGap=10
)

line_image = img.copy()

if lines is not None:
    for line in lines:
        coords = np.asarray(line).reshape(-1)

        if len(coords) >= 4:
            x1, y1, x2, y2 = map(int, coords[:4])

            cv2.line(
                line_image,
                (x1, y1),
                (x2, y2),
                (0, 255, 0),
                2
            )

plt.figure(figsize=(8, 5))
plt.imshow(cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB))
plt.title("Detected Lines Using Hough Transform")
plt.axis("off")
plt.show()

```

### Step 9: Display the Processing Pipeline

```python
images = [
    ("Original", cv2.cvtColor(img, cv2.COLOR_BGR2RGB)),
    ("Grayscale", gray),
    ("Threshold", threshold),
    ("ROI", roi),
    ("Canny Edges", edges),
    ("Gaussian Blur", blurred),
    ("Detected Lines", cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB))
]

plt.figure(figsize=(14, 10))

for i, (title, result) in enumerate(images):
    plt.subplot(3, 3, i + 1)
    if len(result.shape) == 2:
        plt.imshow(result, cmap="gray")
    else:
        plt.imshow(result)
    plt.title(title)
    plt.axis("off")

plt.tight_layout()
plt.show()
```

## Expected Output

1. Original image
2. Grayscale image
3. Thresholded image
4. ROI masked image
5. Canny edge-detected image
6. Gaussian blurred image
7. Image with detected lines

## Output Screenshots

Add screenshots of the outputs obtained by running the programs in Jupyter Notebook.

- **Output 1:** Original and grayscale images
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d8a9d81d-d13f-4815-932b-470dfabbe4dc" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ed66470f-e9a6-4414-b78b-9f2c6c3cec28" />
- **Output 2:** Thresholded and ROI images
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c8c00542-7006-4b19-aab7-c176f999fdd6" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f3ae7b32-533a-474e-8121-fc680a0f461a" />
- **Output 3:** Canny edge detection and Gaussian blur
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1eafc21f-1627-4d0e-b19b-36baf79a1ea1" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e3a45ac3-fb9e-4fc3-9d09-37b786d6ecc6" />
- **Output 4:** Detected lines using Hough Transform
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5f98442b-7bac-42ca-bc6f-7e3edda81884" />
- **Output 5:** Complete image-processing pipeline
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3c251a07-cb35-406c-ae13-68dec3c06a41" />

## Result

Thus, line detection was implemented successfully using OpenCV and Hough Transform. The image was processed through grayscale conversion, thresholding, ROI masking, Canny edge detection, and Gaussian blur to identify and highlight detectable lines.

## Developed By

- **Name:** Shaajini N
- **Register No:** 212225040395
