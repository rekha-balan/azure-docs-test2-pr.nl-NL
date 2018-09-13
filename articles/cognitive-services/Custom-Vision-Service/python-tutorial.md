---
title: Create a Custom Vision Service Python tutorial - Azure Cognitive Services | Microsoft Docs
description: Explore a basic Python app that uses the Custom Vision API in Microsoft Cognitive Services. Create a project, add tags, upload images, train your project, and make a prediction using the default endpoint.
services: cognitive-services
author: areddish
manager: chbuehle
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 08/28/2018
ms.author: areddish
ms.openlocfilehash: df0bdc0bbd2768566336323851f366c9ae280a88
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864652"
---
# <a name="custom-vision-api-python-tutorial"></a><span data-ttu-id="c1ea4-104">Custom Vision API Python tutorial</span><span class="sxs-lookup"><span data-stu-id="c1ea4-104">Custom Vision API Python tutorial</span></span>

<span data-ttu-id="c1ea4-105">Learn how to create an image classification project with the Custom Vision Service and a basic Python script.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-105">Learn how to create an image classification project with the Custom Vision Service and a basic Python script.</span></span> <span data-ttu-id="c1ea4-106">After it's created, you can add tags, upload images, train the project, get the project's default prediction endpoint URL, and use it to programmatically test an image.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-106">After it's created, you can add tags, upload images, train the project, get the project's default prediction endpoint URL, and use it to programmatically test an image.</span></span> <span data-ttu-id="c1ea4-107">Use this open-source example as a template for building your own app by using the Custom Vision API.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-107">Use this open-source example as a template for building your own app by using the Custom Vision API.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c1ea4-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c1ea4-108">Prerequisites</span></span>

- <span data-ttu-id="c1ea4-109">Python 2.7+ or Python 3.5+.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-109">Python 2.7+ or Python 3.5+.</span></span>
- <span data-ttu-id="c1ea4-110">The pip tool.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-110">The pip tool.</span></span>

## <a name="get-the-training-and-prediction-keys"></a><span data-ttu-id="c1ea4-111">Get the training and prediction keys</span><span class="sxs-lookup"><span data-stu-id="c1ea4-111">Get the training and prediction keys</span></span>

<span data-ttu-id="c1ea4-112">To get the keys used in this example, visit the [Custom Vision web page](https://customvision.ai) and select the __gear icon__ in the upper right.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-112">To get the keys used in this example, visit the [Custom Vision web page](https://customvision.ai) and select the __gear icon__ in the upper right.</span></span> <span data-ttu-id="c1ea4-113">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-113">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span></span>

![Image of the keys UI](./media/python-tutorial/training-prediction-keys.png)

## <a name="install-the-custom-vision-service-sdk"></a><span data-ttu-id="c1ea4-115">Install the Custom Vision Service SDK</span><span class="sxs-lookup"><span data-stu-id="c1ea4-115">Install the Custom Vision Service SDK</span></span>

<span data-ttu-id="c1ea4-116">To install the Custom Vision Service SDK, use the following command:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-116">To install the Custom Vision Service SDK, use the following command:</span></span>

```
pip install azure-cognitiveservices-vision-customvision
```

## <a name="get-example-images"></a><span data-ttu-id="c1ea4-117">Get example images</span><span class="sxs-lookup"><span data-stu-id="c1ea4-117">Get example images</span></span>

<span data-ttu-id="c1ea4-118">This example uses the images from the `Samples/Images` directory of the [https://github.com/Microsoft/Cognitive-CustomVision-Windows](https://github.com/Microsoft/Cognitive-CustomVision-Windows/tree/master/Samples/Images) project.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-118">This example uses the images from the `Samples/Images` directory of the [https://github.com/Microsoft/Cognitive-CustomVision-Windows](https://github.com/Microsoft/Cognitive-CustomVision-Windows/tree/master/Samples/Images) project.</span></span> <span data-ttu-id="c1ea4-119">Clone or download and extract the project to your development environment.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-119">Clone or download and extract the project to your development environment.</span></span>

## <a name="create-a-custom-vision-service-project"></a><span data-ttu-id="c1ea4-120">Create a Custom Vision Service project</span><span class="sxs-lookup"><span data-stu-id="c1ea4-120">Create a Custom Vision Service project</span></span>

<span data-ttu-id="c1ea4-121">To create a new Custom Vision Service project, create new file named `sample.py`.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-121">To create a new Custom Vision Service project, create new file named `sample.py`.</span></span> <span data-ttu-id="c1ea4-122">Use the following code as the file contents:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-122">Use the following code as the file contents:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1ea4-123">Set the `training_key` to the training key value you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-123">Set the `training_key` to the training key value you retrieved earlier.</span></span>
>
> <span data-ttu-id="c1ea4-124">Set the `prediction_key` to the prediction key value you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-124">Set the `prediction_key` to the prediction key value you retrieved earlier.</span></span>

```python
from azure.cognitiveservices.vision.customvision.training import training_api
from azure.cognitiveservices.vision.customvision.training.models import ImageUrlCreateEntry

# Replace with a valid key
training_key = "<your training key>"
prediction_key = "<your prediction key>"

trainer = training_api.TrainingApi(training_key)

# Create a new project
print ("Creating project...")
project = trainer.create_project("My Project")
```

## <a name="add-tags-to-your-project"></a><span data-ttu-id="c1ea4-125">Add tags to your project</span><span class="sxs-lookup"><span data-stu-id="c1ea4-125">Add tags to your project</span></span>

<span data-ttu-id="c1ea4-126">To add tags to your project, add the following code to the end of the `sample.py` file:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-126">To add tags to your project, add the following code to the end of the `sample.py` file:</span></span>

```python
# Make two tags in the new project
hemlock_tag = trainer.create_tag(project.id, "Hemlock")
cherry_tag = trainer.create_tag(project.id, "Japanese Cherry")
```

## <a name="upload-images-to-the-project"></a><span data-ttu-id="c1ea4-127">Upload images to the project</span><span class="sxs-lookup"><span data-stu-id="c1ea4-127">Upload images to the project</span></span>

<span data-ttu-id="c1ea4-128">To add the sample images to the project, insert the following code after the tag creation.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-128">To add the sample images to the project, insert the following code after the tag creation.</span></span> <span data-ttu-id="c1ea4-129">This code uploads the image with the corresponding tag:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-129">This code uploads the image with the corresponding tag:</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="c1ea4-130">Change path to the images based on where you downloaded the Cognitive-CustomVision-Windows project earlier.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-130">Change path to the images based on where you downloaded the Cognitive-CustomVision-Windows project earlier.</span></span>

```python
base_image_url = "https://raw.githubusercontent.com/Microsoft/Cognitive-CustomVision-Windows/master/Samples/"

print ("Adding images...")
for image_num in range(1,10):
    image_url = base_image_url + "Images/Hemlock/hemlock_{}.jpg".format(image_num)
    trainer.create_images_from_urls(project.id, [ ImageUrlCreateEntry(url=image_url, tag_ids=[ hemlock_tag.id ] ) ])

for image_num in range(1,10):
    image_url = base_image_url + "Images/Japanese Cherry/japanese_cherry_{}.jpg".format(image_num)
    trainer.create_images_from_urls(project.id, [ ImageUrlCreateEntry(url=image_url, tag_ids=[ cherry_tag.id ] ) ])


# Alternatively, if the images were on disk in a folder called Images alongside the sample.py, then
# they can be added by using the following:
#
#import os
#hemlock_dir = "Images\\Hemlock"
#for image in os.listdir(os.fsencode("Images\\Hemlock")):
#    with open(hemlock_dir + "\\" + os.fsdecode(image), mode="rb") as img_data: 
#        trainer.create_images_from_data(project.id, img_data, [ hemlock_tag.id ])
#
#cherry_dir = "Images\\Japanese Cherry"
#for image in os.listdir(os.fsencode("Images\\Japanese Cherry")):
#    with open(cherry_dir + "\\" + os.fsdecode(image), mode="rb") as img_data: 
#        trainer.create_images_from_data(project.id, img_data, [ cherry_tag.id ])
```

## <a name="train-the-project"></a><span data-ttu-id="c1ea4-131">Train the project</span><span class="sxs-lookup"><span data-stu-id="c1ea4-131">Train the project</span></span>

<span data-ttu-id="c1ea4-132">To train the classifier, add the following code to the end of the `sample.py` file:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-132">To train the classifier, add the following code to the end of the `sample.py` file:</span></span>

```python
import time

print ("Training...")
iteration = trainer.train_project(project.id)
while (iteration.status != "Completed"):
    iteration = trainer.get_iteration(project.id, iteration.id)
    print ("Training status: " + iteration.status)
    time.sleep(1)

# The iteration is now trained. Make it the default project endpoint
trainer.update_iteration(project.id, iteration.id, is_default=True)
print ("Done!")
```

## <a name="get-and-use-the-default-prediction-endpoint"></a><span data-ttu-id="c1ea4-133">Get and use the default prediction endpoint</span><span class="sxs-lookup"><span data-stu-id="c1ea4-133">Get and use the default prediction endpoint</span></span>

<span data-ttu-id="c1ea4-134">To send an image to the prediction endpoint and retrieve the prediction, add the following code to the end of the `sample.py` file:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-134">To send an image to the prediction endpoint and retrieve the prediction, add the following code to the end of the `sample.py` file:</span></span>

```python
from azure.cognitiveservices.vision.customvision.prediction import prediction_endpoint
from azure.cognitiveservices.vision.customvision.prediction.prediction_endpoint import models

# Now there is a trained endpoint that can be used to make a prediction

predictor = prediction_endpoint.PredictionEndpoint(prediction_key)

test_img_url = base_image_url + "Images/Test/test_image.jpg"
results = predictor.predict_image_url(project.id, iteration.id, url=test_img_url)

# Alternatively, if the images were on disk in a folder called Images alongside the sample.py, then
# they can be added by using the following.
#
# Open the sample image and get back the prediction results.
# with open("Images\\test\\test_image.jpg", mode="rb") as test_data:
#     results = predictor.predict_image(project.id, test_data, iteration.id)

# Display the results.
for prediction in results.predictions:
    print ("\t" + prediction.tag_name + ": {0:.2f}%".format(prediction.probability * 100))
```

## <a name="run-the-example"></a><span data-ttu-id="c1ea4-135">Run the example</span><span class="sxs-lookup"><span data-stu-id="c1ea4-135">Run the example</span></span>

<span data-ttu-id="c1ea4-136">Run the solution.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-136">Run the solution.</span></span> <span data-ttu-id="c1ea4-137">The prediction results appear on the console.</span><span class="sxs-lookup"><span data-stu-id="c1ea4-137">The prediction results appear on the console.</span></span>

```
python sample.py
```

<span data-ttu-id="c1ea4-138">The output of the application is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="c1ea4-138">The output of the application is similar to the following text:</span></span>

```
Creating project...
Adding images...
Training...
Training status: Training
Training status: Completed
Done!
        Hemlock: 93.53%
        Japanese Cherry: 0.01%
```