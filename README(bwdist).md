# bwdist Function in Scilab

## Description
`bwdist` computes the distance transform of a binary image, providing the minimum distance from each pixel to the nearest non-zero pixel (foreground) in the binary image. This implementation uses a Chamfer distance approach with diagonal connections.

## Calling Sequence
```scilab
D = bwdist(binary_img)
```
# Parameters
binary_img: A binary matrix (image) where non-zero pixels represent the foreground, and zero pixels represent the background.
D: The output distance matrix, where each pixel's value is the distance to the nearest foreground pixel.

# Function Details
The function bwdist operates in two passes:

- First Pass: Processes the image from top-left to bottom-right, updating the distance matrix based on neighboring pixels to the north and west, including diagonals.
-  Second Pass: Processes from bottom-right to top-left, ensuring minimal distances are computed by considering neighboring pixels to the south and east, including diagonals.

The Chamfer distance approach considers both vertical/horizontal (distance of 1) and diagonal (distance of √2) connections.

# Notes

- The function normalizes the distance matrix for visualization purposes, converting it to an 8-bit integer format.
- The visualization step (optional) displays the normalized distance matrix using imshow.


# Test Cases
## Test case 1

![Screenshot 2025-01-13 021856](https://github.com/user-attachments/assets/849e1d27-42d2-415e-b2dc-dc5a97a42c09)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 2

![Screenshot 2025-01-13 022202](https://github.com/user-attachments/assets/1e4e5562-222e-4da3-8262-fd25922d38e3)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.


## Test case 3

![Screenshot 2025-01-13 022413](https://github.com/user-attachments/assets/6b0cd119-1d13-4d90-8e95-d45614c3ea2b)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.

## Test case 4

![Screenshot 2025-01-13 022651](https://github.com/user-attachments/assets/2e00ea83-c870-4a7b-a3c7-cbf47eff7c37)

### Image-1 (Graphic Window number 0 (Left)) : The custom implementation in Scilab, designed to match the given Octave figure's output. 

### Image-2 (Figure 1 (Right)) : The reference figure generated using Octave.


# Example Usage
```scilab
// Load and process an image
img = imread("your_image_path");
if size(img, 3) == 3 then
  img_gray = rgb2gray(img);
else
  img_gray = img;
end

// Apply thresholding
threshold_value = 120; // This value can be modified according to users requirement
binary_img = img_gray < threshold_value;

// Dilate the binary image using a 3x3 kernel
dilated_img = imdilate(binary_img, ones(3, 3));

// Compute the distance transform
distance_img = bwdist(dilated_img);

// Display the result
imshow(distance_img);
```
