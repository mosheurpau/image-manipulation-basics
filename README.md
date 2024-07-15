# Svelte Image Manipulation

This project is a Svelte-based web application that allows users to add, transform, and layer multiple images. Users can apply various transformations, such as rotation, scaling, skewing, and more, to individual images.

## Features

- **Add Images**: Add images by entering their URLs.
- **Transform Images**: Apply transformations like rotate, scale, skew, perspective, grayscale, and sepia.
- **Layering**: Manage the order of images using move up and move down functionality.
- **Responsive Design**: Ensures the application is usable on various screen sizes.

## Usage

1. Enter the URL of an image in the input field and click "Add Image".
2. Use the provided controls to transform the image.
   - Rotate: Adjust the rotation angle of the image.
   - Scale: Adjust the scale of the image.
   - Grayscale: Apply a grayscale filter to the image.
   - Sepia: Apply a sepia filter to the image.
   - Skew X: Adjust the skew angle on the X-axis.
   - Skew Y: Adjust the skew angle on the Y-axis.
   - Perspective: Adjust the perspective of the image.
   - Rotate X (3D): Adjust the rotation angle on the X-axis.
3. Use the "Move Up" and "Move Down" buttons to change the layering order of the images.
4. Click the "Remove" button to delete an image.

## Code Explanation

The project is implemented in Svelte and uses reactive variables and components to manage the state and render the UI. Here's a brief overview of the key functions:

- **addImage**: Adds a new image to the list with initial transformation properties.
- **removeImage**: Removes an image from the list by its ID.
- **moveImageUp**: Moves an image up in the z-index order.
- **moveImageDown**: Moves an image down in the z-index order.
- **updateZIndices**: Updates the z-index of each image to reflect their order in the list.
