# bwconncomp Function in Scilab

## Description
`bwconncomp` labels connected components in a binary image using a queue-based flood-fill algorithm. It assigns a unique label to each connected component, making it easier to analyze and process segmented regions in the image.

## Calling Sequence

```scilab
labels = bwconncomp(x, y, label, distThresh, labels, rows, cols)
```

# Parameters
1. x, y: Coordinates of the starting pixel for the flood-fill algorithm.
2. label: The label to assign to the connected component being processed.
3. distThresh: A binary matrix obtained by thresholding the distance transform, where non-zero pixels represent potential components.
4. labels: A matrix to store the labels of connected components.
rows, cols: Dimensions of the binary image.

# Function Details
- The bwconncomp function processes the binary image using a queue-based flood-fill approach:
- Initialization: The queue is initialized with the starting pixel coordinates.
- Flood-fill Process: The function iteratively checks neighboring pixels (up, down, left, right) and enqueues them if they belong to the same connected component.
- Label Assignment: Each pixel in the connected component is assigned the same label.

# Notes
- This function identifies connected components in binary images effectively, supporting image segmentation and analysis tasks.
- The resulting labeled image can be normalized and visualized as a grayscale image.

# Test Cases
## Test Case 1


# Example Usage
```scilab
// Load the image
img = imread("your_image_path");

// Convert to grayscale if needed
if size(img, 3) == 3 then
    img_gray = rgb2gray(img);
else
    img_gray = img;
end

// Apply thresholding to obtain a binary image
threshold_value = 120; // This value can be modified according to users requirement
binary_img = img_gray < threshold_value;

// Dilate the binary image using a 3x3 kernel
dilated_img = imdilate(binary_img, ones(3, 3));

// Compute the distance transform and threshold it
distance_img = bwdist(dilated_img);
threshold_value = 3;
distThresh = distance_img > threshold_value;

// Initialize label matrix and label counter
[rows, cols] = size(distThresh);
labels = zeros(rows, cols);
label_counter = 1;

// Label the connected components
for i = 1:rows
    for j = 1:cols
        if distThresh(i, j) & labels(i, j) == 0 then
            labels = bwconncomp(i, j, label_counter, distThresh, labels, rows, cols);
            label_counter = label_counter + 1;
        end
    end
end

// Display the labeled image
imshow(labels);
```
