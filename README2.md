# bwlabel Function in Scilab

# Description
The bwlabel function labels connected components in a binary image. It assigns unique labels to distinct regions of connected pixels, simplifying segmentation and analysis tasks. This implementation supports both 4-connectivity and 8-connectivity.

# Calling Sequence
```scilab
labels = bwlabel(binary_img)
```

# Parameters
- binary_img: A binary matrix where non-zero elements represent foreground pixels, and zeros represent background pixels.
   
# Returns
- labels:A matrix of the same size as the input binary image, where each connected component is assigned a unique integer label.

# Function Details
- Input Validation: The input must be a binary matrix. Foreground pixels are non-zero, and background pixels are zero.
-Flood-Fill Algorithm: The function internally uses a helper function (bwconncomp) to perform the labeling.
- Initialization: A queue is used to store pixel coordinates for processing.
- Labeling: Pixels belonging to the same connected component are assigned the same label.
- Connectivity: Both 4-connectivity (horizontal and vertical neighbors) and 8-connectivity (diagonal neighbors) are supported.
- Iterative Labeling: The function iterates through every pixel in the binary image. If a foreground pixel is unprocessed, it is assigned a new label, and the connected component is identified using the bwconncomp helper function.

# Notes
- Connectivity: The default implementation includes 8-connectivity. Adjustments can be made for 4-connectivity by modifying the neighbors considered.
- Performance: The queue-based flood-fill ensures efficient processing of connected components, even for large images.
- Visualization: The output labels can be scaled and visualized as grayscale or colored images.

# Test Cases
## Test case 1

![Screenshot 2025-01-13 013321](https://github.com/user-attachments/assets/4efaca3a-6f93-4684-847b-4e92a9283ac4)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 2


### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 3


### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 4

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

# Example Usage
```scilab
// Load a binary image
img = imread("path/to/image");
if size(img, 3) == 3 then
    binary_img = rgb2gray(img) < 120; // Convert to binary
else
    binary_img = img < 120; // Binary thresholding
end

// Label the connected components
labeled_img = bwlabel(binary_img);

// Scale the labels for visualization
scaled_img = labeled_img * (255 / max(labeled_img(:)));

// Display the result
imshow(scaled_img);
xtitle("Labeled Connected Components");
```
