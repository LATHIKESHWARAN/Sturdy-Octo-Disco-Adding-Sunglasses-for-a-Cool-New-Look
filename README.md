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

## Program and Output :
```py
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('my.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

![image](https://github.com/user-attachments/assets/4fba124c-4957-4fad-9424-8acd60092abb)

```py
faceImage.shape
```
![image](https://github.com/user-attachments/assets/a52d701c-a819-42d9-8a65-cf426a011f38)

```py
glassPNG = cv2.imread('1.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```

![image](https://github.com/user-attachments/assets/346995aa-724d-43fd-9395-c7e912f0d205)

```py
glassPNG = cv2.resize(glassPNG,(230,90))
print("image Dimension ={}".format(glassPNG.shape))glassBGR = glassPNG[:,:,0:3]
```

![image](https://github.com/user-attachments/assets/3fd67f0e-fb9b-4a26-900b-f07b43970ea7)

```py
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[20,20])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```

![image](https://github.com/user-attachments/assets/f652a9e0-553d-4443-98ff-540f1af8cd6c)

```py
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[120:170,80:270]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

![image](https://github.com/user-attachments/assets/e7b377a4-6294-4796-aaf6-e83fe57caed3)

```py
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[120:170,80:270]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[30,30])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

![image](https://github.com/user-attachments/assets/2c53054b-c556-436f-9c0c-9f6970ef39aa)
```py
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[120:170,80:270]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

![image](https://github.com/user-attachments/assets/02e2b244-8f2f-4878-b52d-707675ec4b78)

## Result :
Thus, the replacing of sungalss image in another image is replaced successfully executed.
