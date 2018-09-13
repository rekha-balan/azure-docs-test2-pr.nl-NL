---
title: 'Getting recommendations in batches: Machine learning recommendations API | Microsoft Docs'
description: Azure machine learning recommendations--getting recommendations in batches
services: cognitive-services
documentationcenter: ''
author: luiscabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 325d4922-8a07-4e67-99e0-f513201f14f7
ms.service: cognitive-services
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: luisca
ms.openlocfilehash: e63218d9c882d84342a3992f05e0a8c9f306d9c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554881"
---
# <a name="get-recommendations-in-batches"></a><span data-ttu-id="3d64c-103">Get recommendations in batches</span><span class="sxs-lookup"><span data-stu-id="3d64c-103">Get recommendations in batches</span></span>
> [!NOTE]
> <span data-ttu-id="3d64c-104">Getting recommendations in batches is more complicated than getting recommendations one at a time.</span><span class="sxs-lookup"><span data-stu-id="3d64c-104">Getting recommendations in batches is more complicated than getting recommendations one at a time.</span></span> <span data-ttu-id="3d64c-105">Check the APIs for information about how to get recommendations for a single request:</span><span class="sxs-lookup"><span data-stu-id="3d64c-105">Check the APIs for information about how to get recommendations for a single request:</span></span>
> 
> [<span data-ttu-id="3d64c-106">Item-to-Item recommendations</span><span class="sxs-lookup"><span data-stu-id="3d64c-106">Item-to-Item recommendations</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/operations/56f30d77eda5650db055a3d4)<br>
> [<span data-ttu-id="3d64c-107">User-to-Item recommendations</span><span class="sxs-lookup"><span data-stu-id="3d64c-107">User-to-Item recommendations</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/operations/56f30d77eda5650db055a3dd)
> 
> <span data-ttu-id="3d64c-108">Batch scoring only works for builds that were created after July 21, 2016.</span><span class="sxs-lookup"><span data-stu-id="3d64c-108">Batch scoring only works for builds that were created after July 21, 2016.</span></span>
> 
> 

<span data-ttu-id="3d64c-109">There are situations in which you need to get recommendations for more than one item at a time.</span><span class="sxs-lookup"><span data-stu-id="3d64c-109">There are situations in which you need to get recommendations for more than one item at a time.</span></span> <span data-ttu-id="3d64c-110">For instance, you might be interested in creating a recommendations cache or even analyzing the types of recommendations that you are getting.</span><span class="sxs-lookup"><span data-stu-id="3d64c-110">For instance, you might be interested in creating a recommendations cache or even analyzing the types of recommendations that you are getting.</span></span>

<span data-ttu-id="3d64c-111">Batch scoring operations, as we call them, are asynchronous operations.</span><span class="sxs-lookup"><span data-stu-id="3d64c-111">Batch scoring operations, as we call them, are asynchronous operations.</span></span> <span data-ttu-id="3d64c-112">You need to submit the request, wait for the operation to finish, and then gather your results.</span><span class="sxs-lookup"><span data-stu-id="3d64c-112">You need to submit the request, wait for the operation to finish, and then gather your results.</span></span>  

<span data-ttu-id="3d64c-113">To be more precise, these are the steps to follow:</span><span class="sxs-lookup"><span data-stu-id="3d64c-113">To be more precise, these are the steps to follow:</span></span>

1. <span data-ttu-id="3d64c-114">Create an Azure Storage container if you don’t have one already.</span><span class="sxs-lookup"><span data-stu-id="3d64c-114">Create an Azure Storage container if you don’t have one already.</span></span>
2. <span data-ttu-id="3d64c-115">Upload an input file that describes each of your recommendation requests to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3d64c-115">Upload an input file that describes each of your recommendation requests to Azure Blob storage.</span></span>
3. <span data-ttu-id="3d64c-116">Kick-start the scoring batch job.</span><span class="sxs-lookup"><span data-stu-id="3d64c-116">Kick-start the scoring batch job.</span></span>
4. <span data-ttu-id="3d64c-117">Wait for the asynchronous operation to finish.</span><span class="sxs-lookup"><span data-stu-id="3d64c-117">Wait for the asynchronous operation to finish.</span></span>
5. <span data-ttu-id="3d64c-118">When the operation has finished, gather the results from Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3d64c-118">When the operation has finished, gather the results from Blob storage.</span></span>

<span data-ttu-id="3d64c-119">Let’s walk through each of these steps.</span><span class="sxs-lookup"><span data-stu-id="3d64c-119">Let’s walk through each of these steps.</span></span>

## <a name="create-a-storage-container-if-you-dont-have-one-already"></a><span data-ttu-id="3d64c-120">Create a Storage container if you don’t have one already</span><span class="sxs-lookup"><span data-stu-id="3d64c-120">Create a Storage container if you don’t have one already</span></span>
<span data-ttu-id="3d64c-121">Go to the [Azure portal](https://portal.azure.com) and create a new storage account if you don’t have one already.</span><span class="sxs-lookup"><span data-stu-id="3d64c-121">Go to the [Azure portal](https://portal.azure.com) and create a new storage account if you don’t have one already.</span></span> <span data-ttu-id="3d64c-122">To do this, navigate to **New** > **Data** + **Storage** > **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="3d64c-122">To do this, navigate to **New** > **Data** + **Storage** > **Storage Account**.</span></span>

<span data-ttu-id="3d64c-123">After you have a storage account, you need to create the blob containers where you will store the input and output of the batch execution.</span><span class="sxs-lookup"><span data-stu-id="3d64c-123">After you have a storage account, you need to create the blob containers where you will store the input and output of the batch execution.</span></span>

<span data-ttu-id="3d64c-124">Upload an input file that describes each of your recommendation requests to Blob storage--let's call the file input.json here.</span><span class="sxs-lookup"><span data-stu-id="3d64c-124">Upload an input file that describes each of your recommendation requests to Blob storage--let's call the file input.json here.</span></span>
<span data-ttu-id="3d64c-125">After you have a container, you need to upload a file that describes each of the requests that you need to perform from the recommendations service.</span><span class="sxs-lookup"><span data-stu-id="3d64c-125">After you have a container, you need to upload a file that describes each of the requests that you need to perform from the recommendations service.</span></span>

<span data-ttu-id="3d64c-126">A batch can perform only one type of request from a specific build.</span><span class="sxs-lookup"><span data-stu-id="3d64c-126">A batch can perform only one type of request from a specific build.</span></span> <span data-ttu-id="3d64c-127">We will explain how to define this information in the next section.</span><span class="sxs-lookup"><span data-stu-id="3d64c-127">We will explain how to define this information in the next section.</span></span> <span data-ttu-id="3d64c-128">For now, let’s assume that we will be performing item recommendations out of a specific build.</span><span class="sxs-lookup"><span data-stu-id="3d64c-128">For now, let’s assume that we will be performing item recommendations out of a specific build.</span></span> <span data-ttu-id="3d64c-129">The input file then contains the input information (in this case, the seed items) for each of the requests.</span><span class="sxs-lookup"><span data-stu-id="3d64c-129">The input file then contains the input information (in this case, the seed items) for each of the requests.</span></span>

<span data-ttu-id="3d64c-130">This is an example of what the input.json file looks like:</span><span class="sxs-lookup"><span data-stu-id="3d64c-130">This is an example of what the input.json file looks like:</span></span>

    {
      "requests": [
      { "SeedItems": [ "C9F-00163", "FKF-00689" ] },
      { "SeedItems": [ "F34-03453" ] },
      { "SeedItems": [ "D16-3244" ] },
      { "SeedItems": [ "C9F-00163", "FKF-00689" ] },
      { "SeedItems": [ "F43-01467" ] },
      { "SeedItems": [ "BD5-06013" ] },
      { "SeedItems": [ "P45-00163", "FKF-00689" ] },
      { "SeedItems": [ "C9A-69320" ] }
      ]
    }

<span data-ttu-id="3d64c-131">As you can see, the file is a JSON file, where each of the requests has the information that's necessary to send a recommendations request.</span><span class="sxs-lookup"><span data-stu-id="3d64c-131">As you can see, the file is a JSON file, where each of the requests has the information that's necessary to send a recommendations request.</span></span> <span data-ttu-id="3d64c-132">Create a similar JSON file for the requests that you need to fulfill, and copy it to the container that you just created in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3d64c-132">Create a similar JSON file for the requests that you need to fulfill, and copy it to the container that you just created in Blob storage.</span></span>

## <a name="kick-start-the-batch-job"></a><span data-ttu-id="3d64c-133">Kick-start the batch job</span><span class="sxs-lookup"><span data-stu-id="3d64c-133">Kick-start the batch job</span></span>
<span data-ttu-id="3d64c-134">The next step is to submit a new batch job.</span><span class="sxs-lookup"><span data-stu-id="3d64c-134">The next step is to submit a new batch job.</span></span> <span data-ttu-id="3d64c-135">For more information, check the [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/).</span><span class="sxs-lookup"><span data-stu-id="3d64c-135">For more information, check the [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/).</span></span>

<span data-ttu-id="3d64c-136">The request body of the API needs to define the locations where the input, output, and error files need to be stored.</span><span class="sxs-lookup"><span data-stu-id="3d64c-136">The request body of the API needs to define the locations where the input, output, and error files need to be stored.</span></span> <span data-ttu-id="3d64c-137">It also needs to define the credentials that are necessary to access those locations.</span><span class="sxs-lookup"><span data-stu-id="3d64c-137">It also needs to define the credentials that are necessary to access those locations.</span></span> <span data-ttu-id="3d64c-138">In addition, you need to specify some parameters that apply to the whole batch (the type of recommendations to request, the model/build to use, the number of results per call, and so on.)</span><span class="sxs-lookup"><span data-stu-id="3d64c-138">In addition, you need to specify some parameters that apply to the whole batch (the type of recommendations to request, the model/build to use, the number of results per call, and so on.)</span></span>

<span data-ttu-id="3d64c-139">This is an example of what the request body should look like:</span><span class="sxs-lookup"><span data-stu-id="3d64c-139">This is an example of what the request body should look like:</span></span>

    {
      "input": {
        "authenticationType": "PublicOrSas",
        "baseLocation": "https://mystorage1.blob.core.windows.net/",
        "relativeLocation": "container1/batchInput.json",
        "sasBlobToken": "?sv=2015-07_restofToken_…4Z&sp=rw"
      },
      "output": {
        "authenticationType": "PublicOrSas",
        "baseLocation": "https://mystorage1.blob.core.windows.net/",
        "relativeLocation": "container1/batchOutput.json ",
        "sasBlobToken": "?sv=2015-07_restofToken_…4Z&sp=rw"
      },
      "error": {
        "authenticationType": "PublicOrSas",
        "baseLocation": "https://mystorage1.blob.core.windows.net/",
        "relativeLocation": "container1/errors.txt",
        "sasBlobToken": "?sv=2015-07_restofToken_…4Z&sp=rw"
      },
      "job": {
        "apiName": "ItemRecommend",
        "modelId": "9ac12a0a-1add-4bdc-bf42-c6517942b3a6",
        "buildId": 1015703,
        "numberOfResults": 10,
        "includeMetadata": true,
        "minimalScore": 0.0
      }
    }

<span data-ttu-id="3d64c-140">Here a few important things to note:</span><span class="sxs-lookup"><span data-stu-id="3d64c-140">Here a few important things to note:</span></span>

* <span data-ttu-id="3d64c-141">Currently, **authenticationType** should always be set to **PublicOrSas**.</span><span class="sxs-lookup"><span data-stu-id="3d64c-141">Currently, **authenticationType** should always be set to **PublicOrSas**.</span></span>
* <span data-ttu-id="3d64c-142">You need to get a Shared Access Signature (SAS) token to allow the Recommendations API to read and write from/to your Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="3d64c-142">You need to get a Shared Access Signature (SAS) token to allow the Recommendations API to read and write from/to your Blob storage account.</span></span> <span data-ttu-id="3d64c-143">More information about how to generate SAS tokens can be found on [the Recommendations API page](../storage/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="3d64c-143">More information about how to generate SAS tokens can be found on [the Recommendations API page](../storage/storage-dotnet-shared-access-signature-part-1.md).</span></span>
* <span data-ttu-id="3d64c-144">The only **apiName** that's currently supported is **ItemRecommend**, which is used for Item-to-Item  recommendations.</span><span class="sxs-lookup"><span data-stu-id="3d64c-144">The only **apiName** that's currently supported is **ItemRecommend**, which is used for Item-to-Item  recommendations.</span></span> <span data-ttu-id="3d64c-145">Batching doesn't currently support User-to-Item recommendations.</span><span class="sxs-lookup"><span data-stu-id="3d64c-145">Batching doesn't currently support User-to-Item recommendations.</span></span>

## <a name="wait-for-the-asynchronous-operation-to-finish"></a><span data-ttu-id="3d64c-146">Wait for the asynchronous operation to finish</span><span class="sxs-lookup"><span data-stu-id="3d64c-146">Wait for the asynchronous operation to finish</span></span>
<span data-ttu-id="3d64c-147">When you start the batch operation, the response returns the Operation-Location header that gives you the information that's necessary to track the operation.</span><span class="sxs-lookup"><span data-stu-id="3d64c-147">When you start the batch operation, the response returns the Operation-Location header that gives you the information that's necessary to track the operation.</span></span>
<span data-ttu-id="3d64c-148">You track the operation by using the [Retrieve Operation Status API](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/operations/56f30d77eda5650db055a3da), just like you do for tracking the operation of a build operation.</span><span class="sxs-lookup"><span data-stu-id="3d64c-148">You track the operation by using the [Retrieve Operation Status API](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/operations/56f30d77eda5650db055a3da), just like you do for tracking the operation of a build operation.</span></span>

## <a name="get-the-results"></a><span data-ttu-id="3d64c-149">Get the results</span><span class="sxs-lookup"><span data-stu-id="3d64c-149">Get the results</span></span>
<span data-ttu-id="3d64c-150">After the operation has finished, assuming that there were no errors, you can gather the results from your output Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3d64c-150">After the operation has finished, assuming that there were no errors, you can gather the results from your output Blob storage.</span></span>

<span data-ttu-id="3d64c-151">The example below show what the output might look like.</span><span class="sxs-lookup"><span data-stu-id="3d64c-151">The example below show what the output might look like.</span></span> <span data-ttu-id="3d64c-152">In this example, we show results for a batch with only two requests (for brevity).</span><span class="sxs-lookup"><span data-stu-id="3d64c-152">In this example, we show results for a batch with only two requests (for brevity).</span></span>

    {
      "results":
      [   
        {
          "request": { "seedItems": [ "DAF-00500", "P3T-00003" ] },
          "recommendations": [
            {
              "items": [
                {
                  "itemId": "F5U-00011",
                  "name": "L2 Ethernet Adapter-Win8Pro SC EN/XD/XX Hdwr",
                  "metadata": ""
                }
              ],
              "rating": 0.722,
              "reasoning": [ "People who like the selected items also like 'L2 Ethernet Adapter-Win8Pro SC EN/XD/XX Hdwr'" ]
            },
            {
              "items": [
                {
                  "itemId": "G5Y-00001",
                  "name": "Docking Station for Srf Pro/Pro2 SC EN/XD/ES Hdwr",
                  "metadata": ""
                }
              ],
              "rating": 0.718,
              "reasoning": [ "People who like the selected items also like 'Docking Station for Srf Pro/Pro2 SC EN/XD/ES Hdwr'" ]
            }
          ]
        },
        {
          "request": { "seedItems": [ "C9F-00163" ] },
          "recommendations": [
            {
              "items": [
                {
                  "itemId": "C9F-00172",
                  "name": "Nokia 2K Shell for Nokia Lumia 630/635 - Green",
                  "metadata": ""
                }
              ],
              "rating": 0.649,
              "reasoning": [ "People who like 'MOZO Flip Cover for Nokia Lumia 635 - White' also like 'Nokia 2K Shell for Nokia Lumia 630/635 - Green'" ]
            },
            {
              "items": [
                {
                  "itemId": "C9F-00171",
                  "name": "Nokia 2K Shell for Nokia Lumia 630/635 - Orange",
                  "metadata": ""
                }
              ],
              "rating": 0.647,
              "reasoning": [ "People who like 'MOZO Flip Cover for Nokia Lumia 635 - White' also like 'Nokia 2K Shell for Nokia Lumia 630/635 - Orange'" ]
            },
            {
              "items": [
                {
                  "itemId": "C9F-00170",
                  "name": "Nokia 2K Shell for Nokia Lumia 630/635 - Yellow",
                  "metadata": ""
                }
              ],
              "rating": 0.646,
              "reasoning": [ "People who like 'MOZO Flip Cover for Nokia Lumia 635 - White' also like 'Nokia 2K Shell for Nokia Lumia 630/635 - Yellow'" ]
            }       
          ]
        }
    ]}


## <a name="learn-about-the-limitations"></a><span data-ttu-id="3d64c-153">Learn about the limitations</span><span class="sxs-lookup"><span data-stu-id="3d64c-153">Learn about the limitations</span></span>
* <span data-ttu-id="3d64c-154">Only one batch job can be called per subscription at a time.</span><span class="sxs-lookup"><span data-stu-id="3d64c-154">Only one batch job can be called per subscription at a time.</span></span>
* <span data-ttu-id="3d64c-155">A batch job input file cannot be more than 2 MB.</span><span class="sxs-lookup"><span data-stu-id="3d64c-155">A batch job input file cannot be more than 2 MB.</span></span>

