# Image Enhancement Project Report

## Table of Contents
1. [Introduction](#introduction)
2. [Objectives](#objectives)
3. [Methodology](#methodology)
    - [Component Extraction](#component-extraction)
    - [Blurry Image Enhancement](#blurry-image-enhancement)
    - [Noise Removal](#noise-removal)
    - [Visual Enhancement](#visual-enhancement)
4. [Techniques Applied](#techniques-applied)
    - [Morphological Operations](#morphological-operations)
    - [High-Pass Filtering](#high-pass-filtering)
    - [Noise Removal Techniques](#noise-removal-techniques)
    - [Histogram Equalization](#histogram-equalization)
5. [Results](#results)
6. [Discussion](#discussion)
7. [Conclusion](#conclusion)
8. [Future Work](#future-work)

---

## Introduction

The image enhancement project focuses on applying a variety of techniques to improve the quality of images that suffer from issues like blurriness, noise, and poor contrast. By utilizing filters, morphological operations, and denoising methods, this project aims to enhance images in terms of sharpness, clarity, and overall visual quality. The project utilizes Python and OpenCV to process the images.

---

## Objectives

The main objectives of the project are:
1. To extract specific components (e.g., circles, structures) from images.
2. To enhance blurry images, particularly by sharpening and filtering.
3. To remove noise from images using various noise reduction techniques.
4. To enhance the overall visual quality of challenging images.

---

## Methodology

### Component Extraction

The first objective is to extract components like circles from the given images. For this, morphological operations and Hough Circle Transforms are used. These techniques help detect and isolate specific structures like circles from noisy or cluttered backgrounds.

### Blurry Image Enhancement

Images such as the ones of a building and a dog suffer from blurriness. To improve their sharpness, high-pass filtering and sharpening techniques are applied. The high-pass filter emphasizes edges in the images, making them appear clearer.

### Noise Removal

Some images, such as the noisy text or rocket images, contain noise that hampers clarity. To address this, various noise removal techniques are employed, including:
- **Gaussian Blur**: A method that smooths out noise while maintaining important features in the image.
- **Median Filtering**: Helps in removing salt-and-pepper noise.
- **Non-Local Means Denoising**: A more advanced method that preserves image details while reducing noise.

### Visual Enhancement

Images with poor contrast, such as the nameplate or newspaper images, can benefit from histogram equalization and sharpening. Histogram equalization improves the contrast of the images, making the details clearer, while sharpening enhances the visual quality.

---

## Techniques Applied

### Morphological Operations

Morphological operations are used to extract components from images. In this project, circles in the image are detected using the Hough Circle Transform method.

**Example Code for Circle Extraction:**
```python
detected_circles = cv2.HoughCircles(blurred, cv2.HOUGH_GRADIENT, dp=1.2, minDist=40, param1=50, param2=30, minRadius=10, maxRadius=40)
````

**Reason for Selection**: Morphological operations were chosen because they are highly effective in detecting shapes and components from noisy backgrounds. The Hough Circle Transform, in particular, is excellent for detecting circles in an image, even if they are partially obscured.

**Output**:

* Before: The circles were difficult to distinguish from the background.
* After: The circles were successfully isolated, making them more visible and defined.

**Discussion**:

* **Pros**: Effective for shape detection, particularly circles.
* **Cons**: Performance may be reduced for images with complex backgrounds or overlapping objects.
* **Quality Achieved**: The quality of component extraction was high, but the result depends on the clarity of the original image.
* **Failure Reasons**: Performance may degrade if the background noise is too severe.
* **Suggestions**: Explore other shape detection techniques like contour detection for more complex shapes.

### High-Pass Filtering

To enhance blurry images, high-pass filters are used. These filters help sharpen the edges of the image by subtracting low-frequency components and retaining high-frequency details.

**Example Code for High-Pass Filtering:**

```python
high_pass_kernel = np.array([[-1, -1, -1], [-1, 8, -1], [-1, -1, -1]])
filtered_building = cv2.filter2D(gray_building, -1, high_pass_kernel)
```

**Reason for Selection**: High-pass filters were selected because they are effective at enhancing edge details in blurry images. This method works well for sharpening images with slight blurring.

**Output**:

* Before: The building image was blurry, making the structure unclear.
* After: The building structure became sharper, with clearer edges.

**Discussion**:

* **Pros**: Simple and effective for sharpening blurred images.
* **Cons**: May cause artifacts in images with high-frequency noise.
* **Quality Achieved**: The building image showed significant improvements, but there were some artifacts in images with complex textures.
* **Failure Reasons**: The dog image, being more complex and blurry, did not achieve optimal clarity.
* **Suggestions**: Combine high-pass filtering with other techniques like unsharp masking for better results.

### Noise Removal Techniques

Different noise removal techniques were used for various images:

* **Gaussian Blur**: Applied to smooth out image noise while maintaining important details.
* **Median Filtering**: Used to remove salt-and-pepper noise.
* **Non-Local Means Denoising**: This advanced method reduces noise while preserving fine details.

**Example Code for Gaussian Blur**:

```python
gaussian_text = cv2.GaussianBlur(text_img_rgb, (5, 5), 0)
```

**Reason for Selection**: These methods were chosen because they provide robust noise reduction while maintaining key image details. Non-Local Means Denoising is particularly good at handling complex noise patterns without losing texture.

**Output**:

* Before: The noisy text and rocket images were cluttered with noise, making it difficult to read or identify details.
* After: The images became much clearer, with significant noise reduction and improved readability.

**Discussion**:

* **Pros**: Gaussian blur is fast and simple; median filtering is effective for salt-and-pepper noise; non-local means denoising preserves fine details.
* **Cons**: Overuse of Gaussian blur can cause some image details to be lost; median filtering may blur fine structures.
* **Quality Achieved**: The noise removal significantly improved the quality of images like the noisy text and rocket images.
* **Failure Reasons**: Some fine details were still lost, particularly in areas of high-frequency noise.
* **Suggestions**: Use advanced denoising algorithms like deep learning-based methods for better noise reduction.

### Histogram Equalization

For images with poor contrast, histogram equalization is used to improve visibility. It redistributes the intensity levels of the image, ensuring that the dark areas become more distinguishable.

**Example Code for Histogram Equalization**:

```python
img_nameplate_eq = cv2.equalizeHist(img_nameplate)
```

**Reason for Selection**: Histogram equalization was selected because it effectively enhances image contrast, making details more visible in images with poor contrast.

**Output**:

* Before: The nameplate image had poor contrast, making the text difficult to read.
* After: The contrast was enhanced, and the text became more distinguishable.

**Discussion**:

* **Pros**: Simple and effective for contrast enhancement.
* **Cons**: Can lead to over-enhancement in some areas, resulting in loss of details.
* **Quality Achieved**: The nameplate image showed a marked improvement in contrast and readability.
* **Failure Reasons**: Images with extreme lighting conditions may still face issues after histogram equalization.
* **Suggestions**: Combine histogram equalization with adaptive methods for better control over the contrast enhancement.

---

## Results

The following results were obtained from applying the techniques to the original images:

* **Circles Image**: The circles were successfully extracted, making them more defined.
* **Building Image**: Sharpness improved significantly after applying high-pass filtering.
* **Dog Image**: Some improvement was observed, but the result was not ideal due to the severe blurriness.
* **Noisy Text Image**: Median filtering and non-local means denoising improved readability.
* **Noisy Rocket Image**: Noise was reduced effectively, but some fine details were still lost.
* **Noisy Wind Chart**: Noise reduction techniques significantly enhanced the clarity and contrast.
* **Newspaper Image**: The text became clearer and more readable after applying non-local means denoising and sharpening.
* **Nameplate Image**: Histogram equalization enhanced contrast, making the text more readable.

---

## Discussion

The techniques applied showed promising results in improving image quality. Morphological operations helped isolate specific components (like circles), and high-pass filtering successfully sharpened blurry images. Noise removal methods, particularly non-local means denoising, proved to be highly effective in maintaining the quality of the image while reducing noise.

However, there were limitations. For example, in highly noisy images (like the rocket or text), some fine details were still lost after denoising. The performance of sharpening and high-pass filtering varied depending on the image content.

---

## Conclusion

In conclusion, the project successfully demonstrated various image enhancement techniques, including morphological operations, high-pass filtering, noise removal, and histogram equalization. These techniques were applied to improve images with different issues, such as blurriness, noise, and poor contrast.

The results showed clear improvements in the visual quality of most of the images. For example, the building and rocket images saw significant improvements in sharpness and clarity, while the noisy wind chart and nameplate images had their contrast and readability enhanced.

However, the techniques applied did not fully resolve issues in the dog and text images. While some improvement was observed, these images did not reach the desired clarity due to their inherent challenges, such as severe blurriness or complex noise patterns.

Overall, the methods proved effective for most images, though further optimization, especially for highly complex or noisy images, is necessary.

---

## Future Work

1. **Advanced Denoising**: Further explore advanced denoising algorithms such as deep learning-based approaches.
2. **Edge Detection**: Apply edge detection techniques like Canny edge detection to enhance image features.

```

