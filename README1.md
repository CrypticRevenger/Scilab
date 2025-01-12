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
