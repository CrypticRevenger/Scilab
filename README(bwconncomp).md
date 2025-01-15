# bwconncomp Function in Scilab

## How to include library file 

1. change the current dict  to function dict

```scilab
cd C:\Users\PRASANT\Desktop\scilab
```

## Description
`bwconncomp` labels connected components in a binary image using a queue-based flood-fill algorithm. It assigns a unique label to each connected component, making it easier to analyze and process segmented regions in the image.

## Calling Sequence

```scilab
labels = bwconncomp(x, y, label, distThresh, labels, rows, cols)
```

# Parameters
-   x, y: Coordinates of the starting pixel for the flood-fill algorithm.
-   label: The label to assign to the connected component being processed.
-   distThresh: A binary matrix obtained by thresholding the distance transform, where non-zero pixels represent potential components.
-   labels: A matrix to store the labels of connected components.
-   rows, cols: Dimensions of the binary image.

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

![Screenshot 2025-01-14 010724](https://github.com/user-attachments/assets/111ffc0e-66fa-4d2a-bbe6-d4055813421e)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 2

![Screenshot 2025-01-14 011344](https://github.com/user-attachments/assets/34afe463-4195-4b69-91e2-af5cf1f70abe)


### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.



## Test case 3

![Screenshot 2025-01-14 011820](https://github.com/user-attachments/assets/5e6468e9-1d70-484f-a3b9-6f10225c0319)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 4

![Screenshot 2025-01-13 235114](https://github.com/user-attachments/assets/47161408-6989-4a00-a048-d16c1b0baa84)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

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
