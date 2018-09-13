---
title: Object detection with Python and Custom Vision API - Azure Cognitive Services | Microsoft Docs
description: Explore a basic Windows app that uses the Custom Vision API in Microsoft Cognitive Services. Create a project, add tags, upload images, train your project, and make a prediction using the default endpoint.
services: cognitive-services
author: areddish
manager: chbuehle
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 05/03/2018
ms.author: areddish
ms.openlocfilehash: 37bdb9ebf7c74586c728e171a9897903b8ad2ee8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867519"
---
# <a name="use-custom-vision-api-to-build-an-object-detection-project-with-python"></a><span data-ttu-id="eee13-104">Use Custom Vision API to build an object detection project with Python</span><span class="sxs-lookup"><span data-stu-id="eee13-104">Use Custom Vision API to build an object detection project with Python</span></span>

<span data-ttu-id="eee13-105">Explore a basic Python script that uses the Computer Vision API to create an object detection project.</span><span class="sxs-lookup"><span data-stu-id="eee13-105">Explore a basic Python script that uses the Computer Vision API to create an object detection project.</span></span> <span data-ttu-id="eee13-106">After it's created, you can add tagged regions, upload images, train the project, obtain the project's default prediction endpoint URL, and use the endpoint to programmatically test an image.</span><span class="sxs-lookup"><span data-stu-id="eee13-106">After it's created, you can add tagged regions, upload images, train the project, obtain the project's default prediction endpoint URL, and use the endpoint to programmatically test an image.</span></span> <span data-ttu-id="eee13-107">Use this open-source example as a template for building your own app by using the Custom Vision API.</span><span class="sxs-lookup"><span data-stu-id="eee13-107">Use this open-source example as a template for building your own app by using the Custom Vision API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eee13-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eee13-108">Prerequisites</span></span>

<span data-ttu-id="eee13-109">To use the tutorial, you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="eee13-109">To use the tutorial, you need to do the following:</span></span>

- <span data-ttu-id="eee13-110">Install either Python 2.7+ or Python 3.5+.</span><span class="sxs-lookup"><span data-stu-id="eee13-110">Install either Python 2.7+ or Python 3.5+.</span></span>
- <span data-ttu-id="eee13-111">Install pip.</span><span class="sxs-lookup"><span data-stu-id="eee13-111">Install pip.</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="eee13-112">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="eee13-112">Platform requirements</span></span>
<span data-ttu-id="eee13-113">This example has been developed for Python.</span><span class="sxs-lookup"><span data-stu-id="eee13-113">This example has been developed for Python.</span></span>

### <a name="get-the-custom-vision-sdk"></a><span data-ttu-id="eee13-114">Get the Custom Vision SDK</span><span class="sxs-lookup"><span data-stu-id="eee13-114">Get the Custom Vision SDK</span></span>

<span data-ttu-id="eee13-115">To build this example, you need to install the Python SDK for the Custom Vision API:</span><span class="sxs-lookup"><span data-stu-id="eee13-115">To build this example, you need to install the Python SDK for the Custom Vision API:</span></span>

```
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="eee13-116">You can download the images with the [Python Samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="eee13-116">You can download the images with the [Python Samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples).</span></span>

## <a name="step-1-get-the-training-and-prediction-keys"></a><span data-ttu-id="eee13-117">Step 1: Get the training and prediction keys</span><span class="sxs-lookup"><span data-stu-id="eee13-117">Step 1: Get the training and prediction keys</span></span>

<span data-ttu-id="eee13-118">To get the keys used in this example, visit the [Custom Vision site](https://customvision.ai) and select the __gear icon__ in the upper right.</span><span class="sxs-lookup"><span data-stu-id="eee13-118">To get the keys used in this example, visit the [Custom Vision site](https://customvision.ai) and select the __gear icon__ in the upper right.</span></span> <span data-ttu-id="eee13-119">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span><span class="sxs-lookup"><span data-stu-id="eee13-119">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span></span>

![Image of the keys UI](./media/python-tutorial/training-prediction-keys.png)

<span data-ttu-id="eee13-121">This example uses the images from [this location](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/tree/master/samples/vision/images).</span><span class="sxs-lookup"><span data-stu-id="eee13-121">This example uses the images from [this location](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/tree/master/samples/vision/images).</span></span>

## <a name="step-2-create-a-custom-vision-service-project"></a><span data-ttu-id="eee13-122">Step 2: Create a Custom Vision Service project</span><span class="sxs-lookup"><span data-stu-id="eee13-122">Step 2: Create a Custom Vision Service project</span></span>

<span data-ttu-id="eee13-123">To create a new Custom Vision Service project, create a sample.py script file and add the following contents.</span><span class="sxs-lookup"><span data-stu-id="eee13-123">To create a new Custom Vision Service project, create a sample.py script file and add the following contents.</span></span> <span data-ttu-id="eee13-124">Note the difference between creating an object detection and image classification project is the domain that is specified to the create_project call.</span><span class="sxs-lookup"><span data-stu-id="eee13-124">Note the difference between creating an object detection and image classification project is the domain that is specified to the create_project call.</span></span>

```Python
from azure.cognitiveservices.vision.customvision.training import training_api
from azure.cognitiveservices.vision.customvision.training.models import ImageFileCreateEntry, Region

# Replace with a valid key
training_key = "<your training key>"
prediction_key = "<your prediction key>"

trainer = training_api.TrainingApi(training_key)

# Find the object detection domain
obj_detection_domain = next(domain for domain in trainer.get_domains() if domain.type == "ObjectDetection")

# Create a new project
print ("Creating project...")
project = trainer.create_project("My Detection Project", domain_id=obj_detection_domain.id)
```

## <a name="step-3-add-tags-to-your-project"></a><span data-ttu-id="eee13-125">Step 3: Add tags to your project</span><span class="sxs-lookup"><span data-stu-id="eee13-125">Step 3: Add tags to your project</span></span>

<span data-ttu-id="eee13-126">To add tags to your project, insert the following code to create two tags:</span><span class="sxs-lookup"><span data-stu-id="eee13-126">To add tags to your project, insert the following code to create two tags:</span></span>

```Python
# Make two tags in the new project
fork_tag = trainer.create_tag(project.id, "fork")
scissors_tag = trainer.create_tag(project.id, "scissors")
```

## <a name="step-4-upload-images-to-the-project"></a><span data-ttu-id="eee13-127">Step 4: Upload images to the project</span><span class="sxs-lookup"><span data-stu-id="eee13-127">Step 4: Upload images to the project</span></span>

<span data-ttu-id="eee13-128">For object detection project you need to upload image, regions, and tags.</span><span class="sxs-lookup"><span data-stu-id="eee13-128">For object detection project you need to upload image, regions, and tags.</span></span> <span data-ttu-id="eee13-129">The region is in normalized coordiantes and specifies the location of the tagged object.</span><span class="sxs-lookup"><span data-stu-id="eee13-129">The region is in normalized coordiantes and specifies the location of the tagged object.</span></span>

<span data-ttu-id="eee13-130">To add the images, region, and tags to the project, insert the following code after the tag creation.</span><span class="sxs-lookup"><span data-stu-id="eee13-130">To add the images, region, and tags to the project, insert the following code after the tag creation.</span></span> <span data-ttu-id="eee13-131">Note that for this tutorial the regions are hardcoded inline with the code.</span><span class="sxs-lookup"><span data-stu-id="eee13-131">Note that for this tutorial the regions are hardcoded inline with the code.</span></span> <span data-ttu-id="eee13-132">The regions specify the bounding box in normalized coordinates.</span><span class="sxs-lookup"><span data-stu-id="eee13-132">The regions specify the bounding box in normalized coordinates.</span></span>

```Python

fork_image_regions = {
    "fork_1": [ 0.145833328, 0.3509314, 0.5894608, 0.238562092 ],
    "fork_2": [ 0.294117659, 0.216944471, 0.534313738, 0.5980392 ],
    "fork_3": [ 0.09191177, 0.0682516545, 0.757352948, 0.6143791 ],
    "fork_4": [ 0.254901975, 0.185898721, 0.5232843, 0.594771266 ],
    "fork_5": [ 0.2365196, 0.128709182, 0.5845588, 0.71405226 ],
    "fork_6": [ 0.115196079, 0.133611143, 0.676470637, 0.6993464 ],
    "fork_7": [ 0.164215669, 0.31008172, 0.767156839, 0.410130739 ],
    "fork_8": [ 0.118872553, 0.318251669, 0.817401946, 0.225490168 ],
    "fork_9": [ 0.18259804, 0.2136765, 0.6335784, 0.643790841 ],
    "fork_10": [ 0.05269608, 0.282303959, 0.8088235, 0.452614367 ],
    "fork_11": [ 0.05759804, 0.0894935, 0.9007353, 0.3251634 ],
    "fork_12": [ 0.3345588, 0.07315363, 0.375, 0.9150327 ],
    "fork_13": [ 0.269607842, 0.194068655, 0.4093137, 0.6732026 ],
    "fork_14": [ 0.143382356, 0.218578458, 0.7977941, 0.295751631 ],
    "fork_15": [ 0.19240196, 0.0633497, 0.5710784, 0.8398692 ],
    "fork_16": [ 0.140931368, 0.480016381, 0.6838235, 0.240196079 ],
    "fork_17": [ 0.305147052, 0.2512582, 0.4791667, 0.5408496 ],
    "fork_18": [ 0.234068632, 0.445702642, 0.6127451, 0.344771236 ],
    "fork_19": [ 0.219362751, 0.141781077, 0.5919118, 0.6683006 ],
    "fork_20": [ 0.180147052, 0.239820287, 0.6887255, 0.235294119 ]
}

scissors_image_regions = {
    "scissors_1": [ 0.4007353, 0.194068655, 0.259803921, 0.6617647 ],
    "scissors_2": [ 0.426470578, 0.185898721, 0.172794119, 0.5539216 ],
    "scissors_3": [ 0.289215684, 0.259428144, 0.403186262, 0.421568632 ],
    "scissors_4": [ 0.343137264, 0.105833367, 0.332107842, 0.8055556 ],
    "scissors_5": [ 0.3125, 0.09766343, 0.435049027, 0.71405226 ],
    "scissors_6": [ 0.379901975, 0.24308826, 0.32107842, 0.5718954 ],
    "scissors_7": [ 0.341911763, 0.20714055, 0.3137255, 0.6356209 ],
    "scissors_8": [ 0.231617644, 0.08459154, 0.504901946, 0.8480392 ],
    "scissors_9": [ 0.170343131, 0.332957536, 0.767156839, 0.403594762 ],
    "scissors_10": [ 0.204656869, 0.120539248, 0.5245098, 0.743464053 ],
    "scissors_11": [ 0.05514706, 0.159754932, 0.799019635, 0.730392158 ],
    "scissors_12": [ 0.265931368, 0.169558853, 0.5061275, 0.606209159 ],
    "scissors_13": [ 0.241421565, 0.184264734, 0.448529422, 0.6830065 ],
    "scissors_14": [ 0.05759804, 0.05027781, 0.75, 0.882352948 ],
    "scissors_15": [ 0.191176474, 0.169558853, 0.6936275, 0.6748366 ],
    "scissors_16": [ 0.1004902, 0.279036, 0.6911765, 0.477124184 ],
    "scissors_17": [ 0.2720588, 0.131977156, 0.4987745, 0.6911765 ],
    "scissors_18": [ 0.180147052, 0.112369314, 0.6262255, 0.6666667 ],
    "scissors_19": [ 0.333333343, 0.0274019931, 0.443627447, 0.852941155 ],
    "scissors_20": [ 0.158088237, 0.04047389, 0.6691176, 0.843137264 ]
}

# Go through the data table above and create the images
print ("Adding images...")
tagged_images_with_regions = []

for file_name in fork_image_regions.keys():
    x,y,w,h = fork_image_regions[file_name]
    regions = [ Region(tag_id=fork_tag.id, left=x,top=y,width=w,height=h) ]

    with open("images/fork/" + file_name + ".jpg", mode="rb") as image_contents:
        tagged_images_with_regions.append(ImageFileCreateEntry(name=file_name, contents=image_contents.read(), regions=regions))

for file_name in scissors_image_regions.keys():
    x,y,w,h = scissors_image_regions[file_name]
    regions = [ Region(tag_id=scissors_tag.id, left=x,top=y,width=w,height=h) ]

    with open("images/scissors/" + file_name + ".jpg", mode="rb") as image_contents:
        tagged_images_with_regions.append(ImageFileCreateEntry(name=file_name, contents=image_contents.read(), regions=regions))


trainer.create_images_from_files(project.id, images=tagged_images_with_regions)
```

## <a name="step-5-train-the-project"></a><span data-ttu-id="eee13-133">Step 5: Train the project</span><span class="sxs-lookup"><span data-stu-id="eee13-133">Step 5: Train the project</span></span>

<span data-ttu-id="eee13-134">Now that you've added tags and images to the project, you can train it:</span><span class="sxs-lookup"><span data-stu-id="eee13-134">Now that you've added tags and images to the project, you can train it:</span></span> 

1. <span data-ttu-id="eee13-135">Insert the following code.</span><span class="sxs-lookup"><span data-stu-id="eee13-135">Insert the following code.</span></span> <span data-ttu-id="eee13-136">This creates the first iteration in the project.</span><span class="sxs-lookup"><span data-stu-id="eee13-136">This creates the first iteration in the project.</span></span> 
2. <span data-ttu-id="eee13-137">Mark this iteration as the default iteration.</span><span class="sxs-lookup"><span data-stu-id="eee13-137">Mark this iteration as the default iteration.</span></span>

```Python
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

## <a name="step-6-get-and-use-the-default-prediction-endpoint"></a><span data-ttu-id="eee13-138">Step 6: Get and use the default prediction endpoint</span><span class="sxs-lookup"><span data-stu-id="eee13-138">Step 6: Get and use the default prediction endpoint</span></span>

<span data-ttu-id="eee13-139">You're now ready to use the model for prediction:</span><span class="sxs-lookup"><span data-stu-id="eee13-139">You're now ready to use the model for prediction:</span></span> 

1. <span data-ttu-id="eee13-140">Obtain the endpoint associated with the default iteration.</span><span class="sxs-lookup"><span data-stu-id="eee13-140">Obtain the endpoint associated with the default iteration.</span></span> 
2. <span data-ttu-id="eee13-141">Send a test image to the project using that endpoint.</span><span class="sxs-lookup"><span data-stu-id="eee13-141">Send a test image to the project using that endpoint.</span></span>

```Python
from azure.cognitiveservices.vision.customvision.prediction import prediction_endpoint
from azure.cognitiveservices.vision.customvision.prediction.prediction_endpoint import models

# Now there is a trained endpoint that can be used to make a prediction

predictor = prediction_endpoint.PredictionEndpoint(prediction_key)

# Open the sample image and get back the prediction results.
with open("images/Test/test_od_image.jpg", mode="rb") as test_data:
    results = predictor.predict_image(project.id, test_data, iteration.id)

# Display the results.
for prediction in results.predictions:
    print ("\t" + prediction.tag_name + ": {0:.2f}%".format(prediction.probability * 100), prediction.bounding_box.left, prediction.bounding_box.top, prediction.bounding_box.width, prediction.bounding_box.height)
```

## <a name="step-7-run-the-example"></a><span data-ttu-id="eee13-142">Step 7: Run the example</span><span class="sxs-lookup"><span data-stu-id="eee13-142">Step 7: Run the example</span></span>

<span data-ttu-id="eee13-143">Run the solution.</span><span class="sxs-lookup"><span data-stu-id="eee13-143">Run the solution.</span></span> <span data-ttu-id="eee13-144">The prediction results appear on the console.</span><span class="sxs-lookup"><span data-stu-id="eee13-144">The prediction results appear on the console.</span></span>

```
python sample.py
```
