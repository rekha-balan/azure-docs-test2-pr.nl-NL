---
title: Use the a Custom Vision Service REST API - Azure Cognitive Services | Microsoft Docs
description: Use the REST API to create, train, test, and export a custom vision model.
services: cognitive-services
author: blackmist
manager: cgronlun
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 08/07/2018
ms.author: larryfr
ms.openlocfilehash: 44fa4d45c33f3064c089724ee761a70d0a8421ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969286"
---
# <a name="tutorial-use-the-custom-vision-rest-api"></a><span data-ttu-id="7d7b7-103">Tutorial: Use the Custom Vision REST API</span><span class="sxs-lookup"><span data-stu-id="7d7b7-103">Tutorial: Use the Custom Vision REST API</span></span>

<span data-ttu-id="7d7b7-104">Learn how to use the Custom Vision REST API to create, train, test, and export a model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-104">Learn how to use the Custom Vision REST API to create, train, test, and export a model.</span></span>

<span data-ttu-id="7d7b7-105">The information in this document demonstrates how to use a REST client to work with the REST API for training the Custom Vision service.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-105">The information in this document demonstrates how to use a REST client to work with the REST API for training the Custom Vision service.</span></span> <span data-ttu-id="7d7b7-106">The examples show how to use the API using the `curl` utility from a bash environment and `Invoke-WebRequest` from Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-106">The examples show how to use the API using the `curl` utility from a bash environment and `Invoke-WebRequest` from Windows PowerShell.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d7b7-107">Get keys</span><span class="sxs-lookup"><span data-stu-id="7d7b7-107">Get keys</span></span>
> * <span data-ttu-id="7d7b7-108">Create a project</span><span class="sxs-lookup"><span data-stu-id="7d7b7-108">Create a project</span></span>
> * <span data-ttu-id="7d7b7-109">Create tags</span><span class="sxs-lookup"><span data-stu-id="7d7b7-109">Create tags</span></span>
> * <span data-ttu-id="7d7b7-110">Add images</span><span class="sxs-lookup"><span data-stu-id="7d7b7-110">Add images</span></span>
> * <span data-ttu-id="7d7b7-111">Train and test the model</span><span class="sxs-lookup"><span data-stu-id="7d7b7-111">Train and test the model</span></span>
> * <span data-ttu-id="7d7b7-112">Export the model</span><span class="sxs-lookup"><span data-stu-id="7d7b7-112">Export the model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d7b7-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7d7b7-113">Prerequisites</span></span>

* <span data-ttu-id="7d7b7-114">A basic familiarity with Representational State Transfer (REST).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-114">A basic familiarity with Representational State Transfer (REST).</span></span> <span data-ttu-id="7d7b7-115">This document does not go into details on things like HTTP verbs, JSON, or other things commonly used with REST.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-115">This document does not go into details on things like HTTP verbs, JSON, or other things commonly used with REST.</span></span>

* <span data-ttu-id="7d7b7-116">Either a bash (Bourne Again Shell) with the [curl](https://curl.haxx.se) utility or Windows PowerShell 3.0 (or greater).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-116">Either a bash (Bourne Again Shell) with the [curl](https://curl.haxx.se) utility or Windows PowerShell 3.0 (or greater).</span></span>

* <span data-ttu-id="7d7b7-117">A Custom Vision account.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-117">A Custom Vision account.</span></span> <span data-ttu-id="7d7b7-118">For more information, see the [Build a classifier](getting-started-build-a-classifier.md) document.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-118">For more information, see the [Build a classifier](getting-started-build-a-classifier.md) document.</span></span>

## <a name="get-keys"></a><span data-ttu-id="7d7b7-119">Get keys</span><span class="sxs-lookup"><span data-stu-id="7d7b7-119">Get keys</span></span>

<span data-ttu-id="7d7b7-120">When using the REST API, you must authenticate using a key.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-120">When using the REST API, you must authenticate using a key.</span></span> <span data-ttu-id="7d7b7-121">When performing management or training operations, you use the __training key__.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-121">When performing management or training operations, you use the __training key__.</span></span> <span data-ttu-id="7d7b7-122">When using the model to make predictions, you use the __prediction key__.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-122">When using the model to make predictions, you use the __prediction key__.</span></span>

<span data-ttu-id="7d7b7-123">When making a request, the key is sent as a request header.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-123">When making a request, the key is sent as a request header.</span></span>

<span data-ttu-id="7d7b7-124">To get the keys for your account, visit the [Custom Vision web page](https://customvision.ai) and select the __gear icon__ in the upper right.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-124">To get the keys for your account, visit the [Custom Vision web page](https://customvision.ai) and select the __gear icon__ in the upper right.</span></span> <span data-ttu-id="7d7b7-125">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-125">In the __Accounts__ section, copy the values from the __Training Key__ and __Prediction Key__ fields.</span></span>

![Image of the keys UI](./media/rest-api-tutorial/training-prediction-keys.png)

> [!IMPORTANT]
> <span data-ttu-id="7d7b7-127">Since the keys are used to authenticate every request, the examples in this document assume that the key values are contained in environment variables.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-127">Since the keys are used to authenticate every request, the examples in this document assume that the key values are contained in environment variables.</span></span> <span data-ttu-id="7d7b7-128">Use the following commands to store the keys to environment variables before using any other snippets in this document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-128">Use the following commands to store the keys to environment variables before using any other snippets in this document:</span></span>
>
> ```bash
> read -p "Enter the training key: " TRAININGKEY
> read -p "Enter the prediction key: " PREDICTIONKEY
> ```
>
> ```powershell
> $trainingKey = Read-Host 'Enter the training key'
> $predictionKey = Read-Host 'Enter the prediction key'
> ```

## <a name="create-a-new-project"></a><span data-ttu-id="7d7b7-129">Create a new project</span><span class="sxs-lookup"><span data-stu-id="7d7b7-129">Create a new project</span></span>

<span data-ttu-id="7d7b7-130">The following examples create a new project named `myproject` in your Custom Vision service instance.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-130">The following examples create a new project named `myproject` in your Custom Vision service instance.</span></span> <span data-ttu-id="7d7b7-131">This service defaults to the `General` domain:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-131">This service defaults to the `General` domain:</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects?name=myproject" -H "Training-Key: $TRAININGKEY" --data-ascii ""
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects?name=myproject" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey" }
$resp.Content
```

<span data-ttu-id="7d7b7-132">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-132">The response to the request is similar to the following JSON document:</span></span>

```json
{
  "id":"45d1b19b-69b6-4a22-8e7e-d1ca37504686",
  "name":"myproject",
  "description":"",
  "settings":{
    "domainId":"ee85a72c-405e-4adc-bb47-ffa8ca0c9f31",
    "useNegativeSet":true,
    "classificationType":"Multilabel",
    "detectionParameters":null
  },
  "created":"2018-08-10T17:39:02.5633333",
  "lastModified":"2018-08-10T17:39:02.5633333",
  "thumbnailUri":null
}
```

> [!TIP]
> <span data-ttu-id="7d7b7-133">The `id` entry in the response is the ID of the new project.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-133">The `id` entry in the response is the ID of the new project.</span></span> <span data-ttu-id="7d7b7-134">This is used in other examples later in this document.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-134">This is used in other examples later in this document.</span></span>

<span data-ttu-id="7d7b7-135">For more information on this request, see [CreateProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a8290).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-135">For more information on this request, see [CreateProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a8290).</span></span>

### <a name="specific-domains"></a><span data-ttu-id="7d7b7-136">Specific domains</span><span class="sxs-lookup"><span data-stu-id="7d7b7-136">Specific domains</span></span>

<span data-ttu-id="7d7b7-137">To create a project for a specific domain, you can provide the __domain ID__ as an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-137">To create a project for a specific domain, you can provide the __domain ID__ as an optional parameter.</span></span> <span data-ttu-id="7d7b7-138">The following examples show how to retrieve a list of available domains:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-138">The following examples show how to retrieve a list of available domains:</span></span>

```bash
curl -X GET "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/domains" -H "Training-Key: $TRAININGKEY" --data-ascii ""
```

```powershell
$resp = Invoke-WebRequest -Method 'GET' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/domains" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey" }
$resp.Content
```

<span data-ttu-id="7d7b7-139">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-139">The response to the request is similar to the following JSON document:</span></span>

```json
[
    {
        "id": "ee85a74c-405e-4adc-bb47-ffa8ca0c9f31",
        "name": "General",
        "type": "Classification",
        "exportable": false,
        "enabled": true
    },
    {
        "id": "c151d5b5-dd07-472a-acc8-15d29dea8518",
        "name": "Food",
        "type": "Classification",
        "exportable": false,
        "enabled": true
    },
    {
        "id": "ca455789-012d-4b50-9fec-5bb63841c793",
        "name": "Landmarks",
        "type": "Classification",
        "exportable": false,
        "enabled": true
    },
    ...
]
```

<span data-ttu-id="7d7b7-140">For more information on this request, see [GetDomains](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a827d).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-140">For more information on this request, see [GetDomains](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a827d).</span></span>

<span data-ttu-id="7d7b7-141">The following example demonstrates creating a new project that uses the __Landmarks__ domain:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-141">The following example demonstrates creating a new project that uses the __Landmarks__ domain:</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects?name=myproject&domainId=ca455789-012d-4b50-9fec-5bb63841c793" -H "Training-Key: $TRAININGKEY" --data-ascii ""
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects?name=myproject&domainId=ca455789-012d-4b50-9fec-5bb63841c793" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey" }
$resp.Content
```

## <a name="create-tags"></a><span data-ttu-id="7d7b7-142">Create tags</span><span class="sxs-lookup"><span data-stu-id="7d7b7-142">Create tags</span></span>

<span data-ttu-id="7d7b7-143">To tag images, you must use a tag ID.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-143">To tag images, you must use a tag ID.</span></span> <span data-ttu-id="7d7b7-144">The following example demonstrates how to create a new tag named `cat` and get a tag ID.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-144">The following example demonstrates how to create a new tag named `cat` and get a tag ID.</span></span> <span data-ttu-id="7d7b7-145">Replace `{projectId}` with the ID of your project.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-145">Replace `{projectId}` with the ID of your project.</span></span> <span data-ttu-id="7d7b7-146">Use the `name=` parameter to specify the name of the tag:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-146">Use the `name=` parameter to specify the name of the tag:</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/tags?name=cat" -H "Training-Key: $TRAININGKEY" --data-ascii ""
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/tags?name=cat" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey" }
$resp.Content
```

<span data-ttu-id="7d7b7-147">The response to the request is similar to the JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-147">The response to the request is similar to the JSON document:</span></span> 

```json
{"id":"ed6f7ab6-5132-47ad-8649-3ec42ee62d43","name":"cat","description":null,"imageCount":0}
```

<span data-ttu-id="7d7b7-148">Save the `id` value, as it is used when tagging images.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-148">Save the `id` value, as it is used when tagging images.</span></span>

<span data-ttu-id="7d7b7-149">For more information on this request, see [CreateTag](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a829d).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-149">For more information on this request, see [CreateTag](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a829d).</span></span>

## <a name="add-images"></a><span data-ttu-id="7d7b7-150">Add images</span><span class="sxs-lookup"><span data-stu-id="7d7b7-150">Add images</span></span>

<span data-ttu-id="7d7b7-151">The following examples demonstrate adding a file from URL.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-151">The following examples demonstrate adding a file from URL.</span></span> <span data-ttu-id="7d7b7-152">Replace `{projectId}` with the ID of your project.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-152">Replace `{projectId}` with the ID of your project.</span></span> <span data-ttu-id="7d7b7-153">Replace `{tagId}` with the ID of the tag for the image:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-153">Replace `{tagId}` with the ID of the tag for the image:</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/images/urls" -H "Training-Key: $TRAININGKEY" -H "Content-Type: application/json" --data-ascii '{"images": [{"url": "http://myimages/cat.jpg","tagIds": ["{tagId}"],"regions": [{"tagId": "{tagId}","left": 119.0,"top": 94.0,"width": 240.0,"height": 140.0}]}], "tagIds": ["{tagId}"]}'
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/images/urls" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey"; "Content-Type"="application/json" } `
    -Body '{"images": [{"url": "http://myimages/cat.jpg","tagIds": ["{tagId}"],"regions": [{"tagId": "{tagId}","left": 119.0,"top": 94.0,"width": 240.0,"height": 140.0}]}], "tagIds": ["{tagId}"]}'
$resp.Content
```

<span data-ttu-id="7d7b7-154">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-154">The response to the request is similar to the following JSON document:</span></span>

```json
{
    "isBatchSuccessful": true,
    "images": [
        {
            "sourceUrl": "http://myimages/cat.jpg",
            "status": "OK",
            "image": {
                "id": "081adaee-a76b-4d94-a70e-e4fd0935a28f",
                "created": "2018-08-13T13:24:22.0815638",
                "width": 640,
                "height": 480,
                "imageUri": "https://linktoimage",
                "thumbnailUri": "https://linktothumbnail",
                "tags": [
                    {
                        "tagId": "ed6f7ab6-5132-47ad-8649-3ec42ee62d43",
                        "tagName": null,
                        "created": "2018-08-13T13:24:22.104936"
                    }
                ],
                "regions": [
                    {
                        "regionId": "40f206a1-3f8a-4de7-a6c3-c7b4643117df",
                        "tagName": null,
                        "created": "2018-08-13T13:24:22.104936",
                        "tagId": "ed6f7ab6-5132-47ad-8649-3ec42ee62d43",
                        "left": 119,
                        "top": 94,
                        "width": 240,
                        "height": 140
                    }
                ]
            }
        }
    ]
}
```

<span data-ttu-id="7d7b7-155">For more information on this request, see [CreateImagesFromUrls](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a8287).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-155">For more information on this request, see [CreateImagesFromUrls](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a8287).</span></span>

## <a name="train-the-model"></a><span data-ttu-id="7d7b7-156">Train the model</span><span class="sxs-lookup"><span data-stu-id="7d7b7-156">Train the model</span></span>

<span data-ttu-id="7d7b7-157">The following examples demonstrate how to train the model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-157">The following examples demonstrate how to train the model.</span></span> <span data-ttu-id="7d7b7-158">Replace `{projectId}` with the ID of your project:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-158">Replace `{projectId}` with the ID of your project:</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/train" -H "Training-Key: $TRAININGKEY" -H "Content-Type: application/json" --data-ascii ""
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/train" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey"; "Content-Type"="application/json" } 
$resp.Content
```

<span data-ttu-id="7d7b7-159">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-159">The response to the request is similar to the following JSON document:</span></span>

```json
{
    "id": "23de09d6-42a1-413e-839e-8db6ee6d3496",
    "name": "Iteration 1",
    "isDefault": false,
    "status": "Training",
    "created": "2018-08-10T17:39:02.5766667",
    "lastModified": "2018-08-16T17:15:07.5250661",
    "projectId": "45d1b19b-69b8-4b22-8e7e-d1ca37504686",
    "exportable": false,
    "domainId": null
}
```

<span data-ttu-id="7d7b7-160">Save the `id` value, as it is used to test and export the model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-160">Save the `id` value, as it is used to test and export the model.</span></span>

<span data-ttu-id="7d7b7-161">For more information, see [TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a8294).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-161">For more information, see [TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a8294).</span></span>

## <a name="test-the-model"></a><span data-ttu-id="7d7b7-162">Test the model</span><span class="sxs-lookup"><span data-stu-id="7d7b7-162">Test the model</span></span>

<span data-ttu-id="7d7b7-163">The following examples demonstrate how to perform a test of the model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-163">The following examples demonstrate how to perform a test of the model.</span></span> <span data-ttu-id="7d7b7-164">Replace `{projectId}` with the ID of your project.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-164">Replace `{projectId}` with the ID of your project.</span></span> <span data-ttu-id="7d7b7-165">Replace `{iterationId}` with the ID returned from training the model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-165">Replace `{iterationId}` with the ID returned from training the model.</span></span> <span data-ttu-id="7d7b7-166">Replace `https://linktotestimage` with the path to the test image.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-166">Replace `https://linktotestimage` with the path to the test image.</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/quicktest/url?iterationId={iterationId}" -H "Training-Key: $TRAININGKEY" -H "Content-Type: application/json" --data-ascii '{"url":"https://linktotestimage"}'
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/quicktest/url?iterationId={iterationId}" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey"; "Content-Type"="application/json" } `
    -Body '{"url":"https://linktotestimage"}'
$resp.Content
```

<span data-ttu-id="7d7b7-167">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-167">The response to the request is similar to the following JSON document:</span></span>

```json
{
    "id": "369b010b-2a92-4f48-a918-4c1a0af91888",
    "project": "45d1b19b-69b8-4b22-8e7e-d1ca37504686",
    "iteration": "23de09d6-42a1-413e-839e-8db6ee6d3496",
    "created": "2018-08-16T17:39:20.7944508Z",
    "predictions": [
        {
            "probability": 0.8390652,
            "tagId": "ed6f7ab6-5132-47ad-8649-3ec42ee62d43",
            "tagName": "cat"
        }
    ]
}
```

<span data-ttu-id="7d7b7-168">For more information, see [QuickTestImageUrl](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a828d).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-168">For more information, see [QuickTestImageUrl](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a828d).</span></span>

## <a name="export-the-model"></a><span data-ttu-id="7d7b7-169">Export the model</span><span class="sxs-lookup"><span data-stu-id="7d7b7-169">Export the model</span></span>

<span data-ttu-id="7d7b7-170">Exporting a model is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-170">Exporting a model is a two-step process.</span></span> <span data-ttu-id="7d7b7-171">First you must specify the model format, and then request the URL for the exported model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-171">First you must specify the model format, and then request the URL for the exported model.</span></span>

### <a name="request-a-model-export"></a><span data-ttu-id="7d7b7-172">Request a model export</span><span class="sxs-lookup"><span data-stu-id="7d7b7-172">Request a model export</span></span>

<span data-ttu-id="7d7b7-173">The following examples demonstrate how to export a `coreml` model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-173">The following examples demonstrate how to export a `coreml` model.</span></span> <span data-ttu-id="7d7b7-174">Replace `{projectId}` with the ID of your project.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-174">Replace `{projectId}` with the ID of your project.</span></span> <span data-ttu-id="7d7b7-175">Replace `{iterationId}` with the ID returned from training the model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-175">Replace `{iterationId}` with the ID returned from training the model.</span></span>

```bash
curl -X POST "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/iterations/{iterationId}/export?platform=coreml" -H "Training-Key: $TRAININGKEY" -H "Content-Type: application/json" --data-ascii ''
```

```powershell
$resp = Invoke-WebRequest -Method 'POST' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/iterations/{iterationId}/export?platform=coreml" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey"; "Content-Type"="application/json" }
$resp.Content
```

<span data-ttu-id="7d7b7-176">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-176">The response to the request is similar to the following JSON document:</span></span>

```json
{
    "platform": "CoreML",
    "status": "Exporting",
    "downloadUri": null,
    "flavor": null
}
```

<span data-ttu-id="7d7b7-177">For more information, see [ExportIteration](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a829b).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-177">For more information, see [ExportIteration](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a829b).</span></span>

### <a name="download-the-exported-model"></a><span data-ttu-id="7d7b7-178">Download the exported model</span><span class="sxs-lookup"><span data-stu-id="7d7b7-178">Download the exported model</span></span>

<span data-ttu-id="7d7b7-179">The following examples demonstrate how to retrieve the URL of the exported model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-179">The following examples demonstrate how to retrieve the URL of the exported model.</span></span> <span data-ttu-id="7d7b7-180">Replace `{projectId}` with the ID of your project.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-180">Replace `{projectId}` with the ID of your project.</span></span> <span data-ttu-id="7d7b7-181">Replace `{iterationId}` with the ID returned from training the model.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-181">Replace `{iterationId}` with the ID returned from training the model.</span></span>

```bash
curl -X GET "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/iterations/{iterationId}/export" -H "Training-Key: $TRAININGKEY" -H "Content-Type: application/json" --data-ascii ''
```

```powershell
$resp = Invoke-WebRequest -Method 'GET' `
    -Uri "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Training/projects/{projectId}/iterations/{iterationId}/export" `
    -UseBasicParsing `
    -Headers @{ "Training-Key"="$trainingKey"; "Content-Type"="application/json" }
$resp.Content
```

<span data-ttu-id="7d7b7-182">The response to the request is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="7d7b7-182">The response to the request is similar to the following JSON document:</span></span>

```json
[
    {
        "platform": "CoreML",
        "status": "Done",
        "downloadUri": "https://linktoexportedmodel",
        "flavor": null
    }
]
```

<span data-ttu-id="7d7b7-183">For more information, see [GetExports](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a829a).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-183">For more information, see [GetExports](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d0e77c63c39c4259a298830c15188310/operations/5a59953940d86a0f3c7a829a).</span></span>