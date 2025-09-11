# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Program:

## Developed by:k.pujitha
## Register No:212223240074
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the Face Image
faceImage = cv2.imread('PHOTO.JPG')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape

#resized_faceImage.shape
faceImage.shape

# Load the Sunglass image with Alpha channel
glassPNG = cv2.imread('sun glass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")

# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[135:185,130:300]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[135:185,130:300]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

plt.figure(figsize=[20,20]);
```

## Output:

<img width="480" height="574" alt="image" src="https://github.com/user-attachments/assets/4c42c62c-45fd-4c3e-a0b9-e807b01453b9" />

<img width="713" height="382" alt="image" src="https://github.com/user-attachments/assets/5d8453f9-c43c-4bc6-bd7d-0b1025234ea3" />

<img width="1361" height="247" alt="image" src="https://github.com/user-attachments/assets/cdd81fdb-e80b-491d-b769-ae194d1f8588" />

<img width="462" height="546" alt="image" src="https://github.com/user-attachments/assets/4d4f98a3-3b65-4185-ab8b-0b7dc5d713ee" />

<img width="1369" height="210" alt="image" src="https://github.com/user-attachments/assets/ffffd4dc-db36-40df-b31c-b7cc264818e6" />

<img width="1081" height="665" alt="image" src="https://github.com/user-attachments/assets/7b6c8617-8abc-44b0-992e-de0f378a6cdf" />
