#GITHUB REPO LINK

https://github.com/CrypticRevenger/Scilab/blob/main/README(bwlabel).md

# bwlabel Function in Scilab

## How to include library file 

1.  change the current directory to the directory where imagelib.sci is stored in Scilab, use the cd command. For example:

```scilab
cd('path_to_directory_containing_imagelib.sci');
```

Replace 'path_to_directory_containing_imagelib.sci' with the actual path where the file is located.

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

![Screenshot 2025-01-13 014655](https://github.com/user-attachments/assets/f5a81b83-604c-4384-8d2e-8d2cf72109d4)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 3

![Screenshot 2025-01-13 015143](https://github.com/user-attachments/assets/e6c75c47-b30d-4366-9f7e-ca64604ed0c0)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 4


![Screenshot 2025-01-11 195354](https://github.com/user-attachments/assets/b4bfc972-20f0-47ee-b9bf-55fb03e328a2)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

# Example Usage
```scilab
// Load a binary image
img = imread("path/to/image");
if size(img, 3) == 3 then
    binary_img = rgb2gray(img) < 120; // Convert to binary
else
   threshold_value = 120; // This value can be modified according to users requirement
   binary_img = img < threshold_value; // Binary thresholding
end

// Label the connected components
labeled_img = bwlabel(binary_img);

// Scale the labels for visualization
scaled_img = labeled_img * (255 / max(labeled_img(:)));

// Display the result
imshow(scaled_img);
xtitle("Labeled Connected Components");
```
