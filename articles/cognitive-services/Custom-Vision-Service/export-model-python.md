---
title: Run TensorFlow model in Python - Custom Vision Service - Azure Cognitive Services | Microsoft Docs
description: Run TensorFlow model in Python
services: cognitive-services
author: areddish
manager: chbuehle
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 05/17/2018
ms.author: areddish
ms.openlocfilehash: d31036404604104ca28328b6c8bc5d3ca74d83ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866148"
---
# <a name="run-tensorflow-model-in-python"></a><span data-ttu-id="75d77-103">Run TensorFlow model in Python</span><span class="sxs-lookup"><span data-stu-id="75d77-103">Run TensorFlow model in Python</span></span>

<span data-ttu-id="75d77-104">After you have [exported your TensorFlow model](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) from the Custom Vision Service, this quickstart will show you how to use this model locally to classify images.</span><span class="sxs-lookup"><span data-stu-id="75d77-104">After you have [exported your TensorFlow model](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) from the Custom Vision Service, this quickstart will show you how to use this model locally to classify images.</span></span>

## <a name="install-required-components"></a><span data-ttu-id="75d77-105">Install required components</span><span class="sxs-lookup"><span data-stu-id="75d77-105">Install required components</span></span>

### <a name="prerequisites"></a><span data-ttu-id="75d77-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="75d77-106">Prerequisites</span></span>

<span data-ttu-id="75d77-107">To use the tutorial, you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="75d77-107">To use the tutorial, you need to do the following:</span></span>

- <span data-ttu-id="75d77-108">Install either Python 2.7+ or Python 3.5+.</span><span class="sxs-lookup"><span data-stu-id="75d77-108">Install either Python 2.7+ or Python 3.5+.</span></span>
- <span data-ttu-id="75d77-109">Install pip.</span><span class="sxs-lookup"><span data-stu-id="75d77-109">Install pip.</span></span>

<span data-ttu-id="75d77-110">Also you will need to install the following packages:</span><span class="sxs-lookup"><span data-stu-id="75d77-110">Also you will need to install the following packages:</span></span>

```
pip install tensorflow
pip install pillow
pip install numpy
pip install opencv-python
```

## <a name="load-your-model-and-tags"></a><span data-ttu-id="75d77-111">Load your model and tags</span><span class="sxs-lookup"><span data-stu-id="75d77-111">Load your model and tags</span></span>

<span data-ttu-id="75d77-112">The downloaded zip file contains a model.pb and a labels.txt.</span><span class="sxs-lookup"><span data-stu-id="75d77-112">The downloaded zip file contains a model.pb and a labels.txt.</span></span> <span data-ttu-id="75d77-113">These files represent the trained model and the classification labels.</span><span class="sxs-lookup"><span data-stu-id="75d77-113">These files represent the trained model and the classification labels.</span></span> <span data-ttu-id="75d77-114">The first step is to load the model into your project.</span><span class="sxs-lookup"><span data-stu-id="75d77-114">The first step is to load the model into your project.</span></span>

```Python
import tensorflow as tf
import os

graph_def = tf.GraphDef()
labels = []

# Import the TF graph
with tf.gfile.FastGFile(filename, 'rb') as f:
    graph_def.ParseFromString(f.read())
    tf.import_graph_def(graph_def, name='')

# Create a list of labels.
with open(labels_filename, 'rt') as lf:
    for l in lf:
        labels.append(l.strip())
```

## <a name="prepare-an-image-for-prediction"></a><span data-ttu-id="75d77-115">Prepare an image for prediction</span><span class="sxs-lookup"><span data-stu-id="75d77-115">Prepare an image for prediction</span></span>

<span data-ttu-id="75d77-116">There are a few steps for preparing the image so that it's the right shape for prediction.</span><span class="sxs-lookup"><span data-stu-id="75d77-116">There are a few steps for preparing the image so that it's the right shape for prediction.</span></span> <span data-ttu-id="75d77-117">These steps mimic the image manipulation performed during training:</span><span class="sxs-lookup"><span data-stu-id="75d77-117">These steps mimic the image manipulation performed during training:</span></span>

### <a name="open-the-file-and-create-an-image-in-the-bgr-color-space"></a><span data-ttu-id="75d77-118">Open the file and create an image in the BGR color space</span><span class="sxs-lookup"><span data-stu-id="75d77-118">Open the file and create an image in the BGR color space</span></span>

```Python
from PIL import Image
import numpy as np
import cv2

# Load from a file
imageFile = "<path to your image file>"
image = Image.open(imageFile)

# Update orientation based on EXIF tags, if the file has orientation info.
image = update_orientation(image)

# Convert to OpenCV format
image = convert_to_opencv(image)
```

### <a name="deal-with-images-with-a-dimension-1600"></a><span data-ttu-id="75d77-119">Deal with images with a dimension >1600</span><span class="sxs-lookup"><span data-stu-id="75d77-119">Deal with images with a dimension >1600</span></span>

```Python
# If the image has either w or h greater than 1600 we resize it down respecting
# aspect ratio such that the largest dimension is 1600
image = resize_down_to_1600_max_dim(image)
```

### <a name="crop-the-largest-center-square"></a><span data-ttu-id="75d77-120">Crop the largest center square</span><span class="sxs-lookup"><span data-stu-id="75d77-120">Crop the largest center square</span></span>

```Python
# We next get the largest center square
h, w = image.shape[:2]
min_dim = min(w,h)
max_square_image = crop_center(image, min_dim, min_dim)
```

### <a name="resize-down-to-256x256"></a><span data-ttu-id="75d77-121">Resize down to 256x256</span><span class="sxs-lookup"><span data-stu-id="75d77-121">Resize down to 256x256</span></span>

```Python
# Resize that square down to 256x256
augmented_image = resize_to_256_square(max_square_image)
```


### <a name="crop-the-center-for-the-specific-input-size-for-the-model"></a><span data-ttu-id="75d77-122">Crop the center for the specific input size for the model</span><span class="sxs-lookup"><span data-stu-id="75d77-122">Crop the center for the specific input size for the model</span></span>

```Python
# The compact models have a network size of 227x227, the model requires this size.
network_input_size = 227

# Crop the center for the specified network_input_Size
augmented_image = crop_center(augmented_image, network_input_size, network_input_size)

```

<span data-ttu-id="75d77-123">The steps above use the following helper functions:</span><span class="sxs-lookup"><span data-stu-id="75d77-123">The steps above use the following helper functions:</span></span>

```Python
def convert_to_opencv(image):
    # RGB -> BGR conversion is performed as well.
    r,g,b = np.array(image).T
    opencv_image = np.array([b,g,r]).transpose()
    return opencv_image

def crop_center(img,cropx,cropy):
    h, w = img.shape[:2]
    startx = w//2-(cropx//2)
    starty = h//2-(cropy//2)
    return img[starty:starty+cropy, startx:startx+cropx]

def resize_down_to_1600_max_dim(image):
    h, w = image.shape[:2]
    if (h < 1600 and w < 1600):
        return image

    new_size = (1600 * w // h, 1600) if (h > w) else (1600, 1600 * h // w)
    return cv2.resize(image, new_size, interpolation = cv2.INTER_LINEAR)

def resize_to_256_square(image):
    h, w = image.shape[:2]
    return cv2.resize(image, (256, 256), interpolation = cv2.INTER_LINEAR)

def update_orientation(image):
    exif_orientation_tag = 0x0112
    if hasattr(image, '_getexif'):
        exif = image._getexif()
        if (exif != None and exif_orientation_tag in exif):
            orientation = exif.get(exif_orientation_tag, 1)
            # orientation is 1 based, shift to zero based and flip/transpose based on 0-based values
            orientation -= 1
            if orientation >= 4:
                image = image.transpose(Image.TRANSPOSE)
            if orientation == 2 or orientation == 3 or orientation == 6 or orientation == 7:
                image = image.transpose(Image.FLIP_TOP_BOTTOM)
            if orientation == 1 or orientation == 2 or orientation == 5 or orientation == 6:
                image = image.transpose(Image.FLIP_LEFT_RIGHT)
    return image
```

## <a name="predict-an-image"></a><span data-ttu-id="75d77-124">Predict an image</span><span class="sxs-lookup"><span data-stu-id="75d77-124">Predict an image</span></span>

<span data-ttu-id="75d77-125">Once the image is prepared as a tensor we can send it through the model for a prediction:</span><span class="sxs-lookup"><span data-stu-id="75d77-125">Once the image is prepared as a tensor we can send it through the model for a prediction:</span></span>

```Python

# These names are part of the model and cannot be changed.
output_layer = 'loss:0'
input_node = 'Placeholder:0'

with tf.Session() as sess:
    prob_tensor = sess.graph.get_tensor_by_name(output_layer)
    predictions, = sess.run(prob_tensor, {input_node: [augmented_image] })
```

## <a name="view-the-results"></a><span data-ttu-id="75d77-126">View the results</span><span class="sxs-lookup"><span data-stu-id="75d77-126">View the results</span></span>

<span data-ttu-id="75d77-127">The results of running the image tensor through the model will then need to be mapped back to the labels.</span><span class="sxs-lookup"><span data-stu-id="75d77-127">The results of running the image tensor through the model will then need to be mapped back to the labels.</span></span>

```Python
    # Print the highest probability label
    highest_probability_index = np.argmax(predictions)
    print('Classified as: ' + labels[highest_probability_index])
    print()

    # Or you can print out all of the results mapping labels to probabilities.
    label_index = 0
    for p in predictions:
        truncated_probablity = np.float64(round(p,8))
        print (labels[label_index], truncated_probablity)
        label_index += 1
```
## <a name="next-steps"></a><span data-ttu-id="75d77-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="75d77-128">Next steps</span></span>

<span data-ttu-id="75d77-129">You can also wrap the model into a mobile application:</span><span class="sxs-lookup"><span data-stu-id="75d77-129">You can also wrap the model into a mobile application:</span></span>
* [<span data-ttu-id="75d77-130">Use your exported Tensorflow model in an Android application</span><span class="sxs-lookup"><span data-stu-id="75d77-130">Use your exported Tensorflow model in an Android application</span></span>](https://github.com/Azure-Samples/cognitive-services-android-customvision-sample)
* [<span data-ttu-id="75d77-131">Use your exported CoreML model in an Swift iOS application</span><span class="sxs-lookup"><span data-stu-id="75d77-131">Use your exported CoreML model in an Swift iOS application</span></span>](https://go.microsoft.com/fwlink/?linkid=857726)
* [<span data-ttu-id="75d77-132">Use your exported CoreML model in an iOS application with Xamarin</span><span class="sxs-lookup"><span data-stu-id="75d77-132">Use your exported CoreML model in an iOS application with Xamarin</span></span>](https://github.com/xamarin/ios-samples/tree/master/ios11/CoreMLAzureModel)

