---
title: Create a Custom Vision Service Java tutorial - Azure Cognitive Services | Microsoft Docs
description: Explore a basic Java app that uses the Custom Vision API in Microsoft Cognitive Services. Create a project, add tags, upload images, train your project, and make a prediction using the default endpoint.
services: cognitive-services
author: areddish
manager: chbuehle
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 08/28/2018
ms.author: areddish
ms.openlocfilehash: a83a2f5cac9281a4cd79c1a0cead0f2af82d73df
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867323"
---
# <a name="use-custom-vision-api-to-build-an-image-classification-project-with-java"></a><span data-ttu-id="a1390-104">Use Custom Vision API to build an image classification project with Java</span><span class="sxs-lookup"><span data-stu-id="a1390-104">Use Custom Vision API to build an image classification project with Java</span></span>

<span data-ttu-id="a1390-105">Learn how to create an image classification project with the Custom Vision Service using Java.</span><span class="sxs-lookup"><span data-stu-id="a1390-105">Learn how to create an image classification project with the Custom Vision Service using Java.</span></span> <span data-ttu-id="a1390-106">After it's created, you can add tags, upload images, train the project, get the project's default prediction endpoint URL, and use it to programmatically test an image.</span><span class="sxs-lookup"><span data-stu-id="a1390-106">After it's created, you can add tags, upload images, train the project, get the project's default prediction endpoint URL, and use it to programmatically test an image.</span></span> <span data-ttu-id="a1390-107">Use this open-source example as a template for building your own app by using the Custom Vision API.</span><span class="sxs-lookup"><span data-stu-id="a1390-107">Use this open-source example as a template for building your own app by using the Custom Vision API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1390-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1390-108">Prerequisites</span></span>

- <span data-ttu-id="a1390-109">JDK 7 or 8 installed.</span><span class="sxs-lookup"><span data-stu-id="a1390-109">JDK 7 or 8 installed.</span></span>
- <span data-ttu-id="a1390-110">Maven installed.</span><span class="sxs-lookup"><span data-stu-id="a1390-110">Maven installed.</span></span>

## <a name="get-the-training-and-prediction-keys"></a><span data-ttu-id="a1390-111">Get the training and prediction keys</span><span class="sxs-lookup"><span data-stu-id="a1390-111">Get the training and prediction keys</span></span>

<span data-ttu-id="a1390-112">To get the keys used in this example, visit the [Custom Vision web page](https://customvision.ai) and select the __gear icon__ in the upper right.</span><span class="sxs-lookup"><span data-stu-id="a1390-112">To get the keys used in this example, visit the [Custom Vision web page](https://customvision.ai) and select the __gear icon__ in the upper right.</span></span> <span data-ttu-id="a1390-113">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span><span class="sxs-lookup"><span data-stu-id="a1390-113">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span></span>

![Image of the keys UI](./media/python-tutorial/training-prediction-keys.png)

## <a name="install-the-custom-vision-service-sdk"></a><span data-ttu-id="a1390-115">Install the Custom Vision Service SDK</span><span class="sxs-lookup"><span data-stu-id="a1390-115">Install the Custom Vision Service SDK</span></span>

<span data-ttu-id="a1390-116">You can install the Custom Vision SDK from maven central repository:</span><span class="sxs-lookup"><span data-stu-id="a1390-116">You can install the Custom Vision SDK from maven central repository:</span></span>
* [<span data-ttu-id="a1390-117">Training SDK</span><span class="sxs-lookup"><span data-stu-id="a1390-117">Training SDK</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure.cognitiveservices/azure-cognitiveservices-customvision-training)
* [<span data-ttu-id="a1390-118">Prediction SDK</span><span class="sxs-lookup"><span data-stu-id="a1390-118">Prediction SDK</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure.cognitiveservices/azure-cognitiveservices-customvision-prediction)

## <a name="understand-the-code"></a><span data-ttu-id="a1390-119">Understand the code</span><span class="sxs-lookup"><span data-stu-id="a1390-119">Understand the code</span></span>

<span data-ttu-id="a1390-120">The full project, including images, is available from the [Custom Vision Azure samples for Java repository](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master).</span><span class="sxs-lookup"><span data-stu-id="a1390-120">The full project, including images, is available from the [Custom Vision Azure samples for Java repository](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master).</span></span> 

<span data-ttu-id="a1390-121">Use your favorite Java IDE to open the `Vision/CustomVision` project.</span><span class="sxs-lookup"><span data-stu-id="a1390-121">Use your favorite Java IDE to open the `Vision/CustomVision` project.</span></span> 

<span data-ttu-id="a1390-122">This application uses the training key you retrieved earlier to create a new project named __Sample Java Project__.</span><span class="sxs-lookup"><span data-stu-id="a1390-122">This application uses the training key you retrieved earlier to create a new project named __Sample Java Project__.</span></span> <span data-ttu-id="a1390-123">It then uploads images to train and test a classifier.</span><span class="sxs-lookup"><span data-stu-id="a1390-123">It then uploads images to train and test a classifier.</span></span> <span data-ttu-id="a1390-124">The classifier identifies whether a tree is a __Hemlock__ or a __Japanese Cherry__.</span><span class="sxs-lookup"><span data-stu-id="a1390-124">The classifier identifies whether a tree is a __Hemlock__ or a __Japanese Cherry__.</span></span>

<span data-ttu-id="a1390-125">The following code snippets implement the primary functionality of this example:</span><span class="sxs-lookup"><span data-stu-id="a1390-125">The following code snippets implement the primary functionality of this example:</span></span>

## <a name="create-a-custom-vision-service-project"></a><span data-ttu-id="a1390-126">Create a Custom Vision Service project</span><span class="sxs-lookup"><span data-stu-id="a1390-126">Create a Custom Vision Service project</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1390-127">Set the `trainingApiKey` to the training key value you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="a1390-127">Set the `trainingApiKey` to the training key value you retrieved earlier.</span></span>

```java
final String trainingApiKey = "insert your training key here";
TrainingApi trainClient = CustomVisionTrainingManager.authenticate(trainingApiKey);

Trainings trainer = trainClient.trainings();

System.out.println("Creating project...");
Project project = trainer.createProject()
            .withName("Sample Java Project")
            .execute();
```

## <a name="add-tags-to-your-project"></a><span data-ttu-id="a1390-128">Add tags to your project</span><span class="sxs-lookup"><span data-stu-id="a1390-128">Add tags to your project</span></span>

```java
// create hemlock tag
Tag hemlockTag = trainer.createTag()
    .withProjectId(project.id())
    .withName("Hemlock")
    .execute();

// create cherry tag
Tag cherryTag = trainer.createTag()
    .withProjectId(project.id())
    .withName("Japanese Cherry")
    .execute();
```

## <a name="upload-images-to-the-project"></a><span data-ttu-id="a1390-129">Upload images to the project</span><span class="sxs-lookup"><span data-stu-id="a1390-129">Upload images to the project</span></span>

<span data-ttu-id="a1390-130">The sample is setup to include the images in the final package.</span><span class="sxs-lookup"><span data-stu-id="a1390-130">The sample is setup to include the images in the final package.</span></span> <span data-ttu-id="a1390-131">Images are read from the resources section of the jar and uploaded to the service.</span><span class="sxs-lookup"><span data-stu-id="a1390-131">Images are read from the resources section of the jar and uploaded to the service.</span></span>

```java
System.out.println("Adding images...");
for (int i = 1; i <= 10; i++) {
    String fileName = "hemlock_" + i + ".jpg";
    byte[] contents = GetImage("/Hemlock", fileName);
    AddImageToProject(trainer, project, fileName, contents, hemlockTag.id(), null);
}

for (int i = 1; i <= 10; i++) {
    String fileName = "japanese_cherry_" + i + ".jpg";
    byte[] contents = GetImage("/Japanese Cherry", fileName);
    AddImageToProject(trainer, project, fileName, contents, cherryTag.id(), null);
}
```

<span data-ttu-id="a1390-132">The previous snippet code makes use of two helper functions that retrieve the images as resource streams and upload them to the service.</span><span class="sxs-lookup"><span data-stu-id="a1390-132">The previous snippet code makes use of two helper functions that retrieve the images as resource streams and upload them to the service.</span></span>

```java
private static void AddImageToProject(Trainings trainer, Project project, String fileName, byte[] contents, UUID tag)
{
    System.out.println("Adding image: " + fileName);

    ImageFileCreateEntry file = new ImageFileCreateEntry()
        .withName(fileName)
        .withContents(contents);

    ImageFileCreateBatch batch = new ImageFileCreateBatch()
        .withImages(Collections.singletonList(file));

    batch = batch.withTagIds(Collections.singletonList(tag));

    trainer.createImagesFromFiles(project.id(), batch);
}

private static byte[] GetImage(String folder, String fileName)
{
    try {
        return ByteStreams.toByteArray(CustomVisionSamples.class.getResourceAsStream(folder + "/" + fileName));
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    return null;
}
```

## <a name="train-the-project"></a><span data-ttu-id="a1390-133">Train the project</span><span class="sxs-lookup"><span data-stu-id="a1390-133">Train the project</span></span>

<span data-ttu-id="a1390-134">This creates the first iteration in the project and marks this iteration as the default iteration.</span><span class="sxs-lookup"><span data-stu-id="a1390-134">This creates the first iteration in the project and marks this iteration as the default iteration.</span></span> 

```java
System.out.println("Training...");
Iteration iteration = trainer.trainProject(project.id());

while (iteration.status().equals("Training"))
{
    System.out.println("Training Status: "+ iteration.status());
    Thread.sleep(1000);
    iteration = trainer.getIteration(project.id(), iteration.id());
}

System.out.println("Training Status: "+ iteration.status());
trainer.updateIteration(project.id(), iteration.id(), iteration.withIsDefault(true));
```

## <a name="get-and-use-the-default-prediction-endpoint"></a><span data-ttu-id="a1390-135">Get and use the default prediction endpoint</span><span class="sxs-lookup"><span data-stu-id="a1390-135">Get and use the default prediction endpoint</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1390-136">Set the `predictionApiKey` to the prediction key value you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="a1390-136">Set the `predictionApiKey` to the prediction key value you retrieved earlier.</span></span>

```java
final String predictionApiKey = "insert your prediction key here";
PredictionEndpoint predictClient = CustomVisionPredictionManager.authenticate(predictionApiKey);

// Use below for predictions from a url
// String url = "some url";
// ImagePrediction results = predictor.predictions().predictImage()
//                         .withProjectId(project.id())
//                         .withUrl(url)
//                         .execute();

// load test image
byte[] testImage = GetImage("/Test", "test_image.jpg");

// predict
ImagePrediction results = predictor.predictions().predictImage()
    .withProjectId(project.id())
    .withImageData(testImage)
    .execute();

for (Prediction prediction: results.predictions())
{
    System.out.println(String.format("\t%s: %.2f%%", prediction.tagName(), prediction.probability() * 100.0f));
}
```

## <a name="run-the-example"></a><span data-ttu-id="a1390-137">Run the example</span><span class="sxs-lookup"><span data-stu-id="a1390-137">Run the example</span></span>

<span data-ttu-id="a1390-138">To compile and run the solution using maven:</span><span class="sxs-lookup"><span data-stu-id="a1390-138">To compile and run the solution using maven:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="a1390-139">The output of the application is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="a1390-139">The output of the application is similar to the following text:</span></span>

```
Creating project...
Adding images...
Adding image: hemlock_1.jpg
Adding image: hemlock_2.jpg
Adding image: hemlock_3.jpg
Adding image: hemlock_4.jpg
Adding image: hemlock_5.jpg
Adding image: hemlock_6.jpg
Adding image: hemlock_7.jpg
Adding image: hemlock_8.jpg
Adding image: hemlock_9.jpg
Adding image: hemlock_10.jpg
Adding image: japanese_cherry_1.jpg
Adding image: japanese_cherry_2.jpg
Adding image: japanese_cherry_3.jpg
Adding image: japanese_cherry_4.jpg
Adding image: japanese_cherry_5.jpg
Adding image: japanese_cherry_6.jpg
Adding image: japanese_cherry_7.jpg
Adding image: japanese_cherry_8.jpg
Adding image: japanese_cherry_9.jpg
Adding image: japanese_cherry_10.jpg
Training...
Training status: Training
Training status: Training
Training status: Completed
Done!
        Hemlock: 93.53%
        Japanese Cherry: 0.01%
```