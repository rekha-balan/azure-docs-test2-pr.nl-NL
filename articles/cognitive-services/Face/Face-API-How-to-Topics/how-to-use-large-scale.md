---
title: Use the Large-Scale Feature in the Face API | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Use the large-scale feature in the Face API of Cognitive Services.
services: cognitive-services
author: SteveMSFT
manager: corncar
ms.service: cognitive-services
ms.component: face-api
ms.topic: article
ms.date: 03/01/2018
ms.author: sbowles
ms.openlocfilehash: f7b3ac57cf6b24c8a90b4ea59757d3a2cfafd781
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871202"
---
# <a name="how-to-use-the-large-scale-feature"></a><span data-ttu-id="97b02-103">How to use the large-scale feature</span><span class="sxs-lookup"><span data-stu-id="97b02-103">How to use the large-scale feature</span></span>

<span data-ttu-id="97b02-104">This guide is an advanced article on code migration to scale up from existing PersonGroup and FaceList to LargePersonGroup and LargeFaceList respectively.</span><span class="sxs-lookup"><span data-stu-id="97b02-104">This guide is an advanced article on code migration to scale up from existing PersonGroup and FaceList to LargePersonGroup and LargeFaceList respectively.</span></span>
<span data-ttu-id="97b02-105">This guide demonstrates the migration process with assumption of knowing basic usage of PersonGroup and FaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-105">This guide demonstrates the migration process with assumption of knowing basic usage of PersonGroup and FaceList.</span></span>
<span data-ttu-id="97b02-106">For getting familiar with basic operations, please see other tutorials such as [How to identify faces in images](HowtoIdentifyFacesinImage.md),</span><span class="sxs-lookup"><span data-stu-id="97b02-106">For getting familiar with basic operations, please see other tutorials such as [How to identify faces in images](HowtoIdentifyFacesinImage.md),</span></span>

<span data-ttu-id="97b02-107">Microsoft Face API recently released two features to enable large-scale scenarios, LargePersonGroup and LargeFaceList, collectively referred to as Large-scale operations.</span><span class="sxs-lookup"><span data-stu-id="97b02-107">Microsoft Face API recently released two features to enable large-scale scenarios, LargePersonGroup and LargeFaceList, collectively referred to as Large-scale operations.</span></span>
<span data-ttu-id="97b02-108">LargePersonGroup can contain up to 1,000,000 persons each with a maximum of 248 faces, and LargeFaceList can hold up to 1,000,000 faces.</span><span class="sxs-lookup"><span data-stu-id="97b02-108">LargePersonGroup can contain up to 1,000,000 persons each with a maximum of 248 faces, and LargeFaceList can hold up to 1,000,000 faces.</span></span>

<span data-ttu-id="97b02-109">The large-scale operations are similar to the conventional PersonGroup and FaceList, but have some notable differences due to the new architecture.</span><span class="sxs-lookup"><span data-stu-id="97b02-109">The large-scale operations are similar to the conventional PersonGroup and FaceList, but have some notable differences due to the new architecture.</span></span>
<span data-ttu-id="97b02-110">This guide demonstrates the migration process with assumption of knowing basic usage of PersonGroup and FaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-110">This guide demonstrates the migration process with assumption of knowing basic usage of PersonGroup and FaceList.</span></span>
<span data-ttu-id="97b02-111">The samples are written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="97b02-111">The samples are written in C# using the Face API client library.</span></span>

<span data-ttu-id="97b02-112">To enable Face search performance for Identification and FindSimilar in the large scale, you need to introduce a Train operation to pre-process the LargeFaceList and LargePersonGroup.</span><span class="sxs-lookup"><span data-stu-id="97b02-112">To enable Face search performance for Identification and FindSimilar in the large scale, you need to introduce a Train operation to pre-process the LargeFaceList and LargePersonGroup.</span></span>
<span data-ttu-id="97b02-113">The training time varies from seconds to about half an hour depending on the actual capacity.</span><span class="sxs-lookup"><span data-stu-id="97b02-113">The training time varies from seconds to about half an hour depending on the actual capacity.</span></span>
<span data-ttu-id="97b02-114">During the training period, it is still possible to perform Identification and FindSimilar if a successful training is done before.</span><span class="sxs-lookup"><span data-stu-id="97b02-114">During the training period, it is still possible to perform Identification and FindSimilar if a successful training is done before.</span></span>
<span data-ttu-id="97b02-115">However, the drawback is that the new added persons/faces will not appear in the result until a new post migration to large-scale training is completed.</span><span class="sxs-lookup"><span data-stu-id="97b02-115">However, the drawback is that the new added persons/faces will not appear in the result until a new post migration to large-scale training is completed.</span></span>

## <a name="concepts"></a> <span data-ttu-id="97b02-116">Concepts</span><span class="sxs-lookup"><span data-stu-id="97b02-116">Concepts</span></span>

<span data-ttu-id="97b02-117">If you are not familiar with the following concepts in this guide, the definitions can be found in the [glossary](../Glossary.md):</span><span class="sxs-lookup"><span data-stu-id="97b02-117">If you are not familiar with the following concepts in this guide, the definitions can be found in the [glossary](../Glossary.md):</span></span>

- <span data-ttu-id="97b02-118">LargePersonGroup: A collection of Persons with capacity up to 1,000,000.</span><span class="sxs-lookup"><span data-stu-id="97b02-118">LargePersonGroup: A collection of Persons with capacity up to 1,000,000.</span></span>
- <span data-ttu-id="97b02-119">LargeFaceList: A collection of Faces with capacity up to 1,000,000.</span><span class="sxs-lookup"><span data-stu-id="97b02-119">LargeFaceList: A collection of Faces with capacity up to 1,000,000.</span></span>
- <span data-ttu-id="97b02-120">Train: A pre-process to ensure Identification/FindSimilar performance.</span><span class="sxs-lookup"><span data-stu-id="97b02-120">Train: A pre-process to ensure Identification/FindSimilar performance.</span></span>
- <span data-ttu-id="97b02-121">Identification: Identify one or more faces from a PersonGroup or LargePersonGroup.</span><span class="sxs-lookup"><span data-stu-id="97b02-121">Identification: Identify one or more faces from a PersonGroup or LargePersonGroup.</span></span>
- <span data-ttu-id="97b02-122">FindSimilar: Search similar faces from a FaceList or LargeFaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-122">FindSimilar: Search similar faces from a FaceList or LargeFaceList.</span></span>

## <a name="initialization"></a> <span data-ttu-id="97b02-123">Step 1: Authorize the API call</span><span class="sxs-lookup"><span data-stu-id="97b02-123">Step 1: Authorize the API call</span></span>

<span data-ttu-id="97b02-124">When using the Face API client library, the subscription key and subscription endpoint are passed in through the constructor of the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="97b02-124">When using the Face API client library, the subscription key and subscription endpoint are passed in through the constructor of the FaceServiceClient class.</span></span> <span data-ttu-id="97b02-125">For example:</span><span class="sxs-lookup"><span data-stu-id="97b02-125">For example:</span></span>

```CSharp
string SubscriptionKey = "<Subscription Key>";
// Use your own subscription endpoint corresponding to the subscription key.
string SubscriptionRegion = "https://westcentralus.api.cognitive.microsoft.com/face/v1.0/";
FaceServiceClient FaceServiceClient = new FaceServiceClient(SubscriptionKey, SubscriptionRegion);
```

<span data-ttu-id="97b02-126">The subscription key with corresponding endpoint can be obtained from the Marketplace page of your Azure portal.</span><span class="sxs-lookup"><span data-stu-id="97b02-126">The subscription key with corresponding endpoint can be obtained from the Marketplace page of your Azure portal.</span></span>
<span data-ttu-id="97b02-127">See [Subscriptions](https://azure.microsoft.com/services/cognitive-services/directory/vision/).</span><span class="sxs-lookup"><span data-stu-id="97b02-127">See [Subscriptions](https://azure.microsoft.com/services/cognitive-services/directory/vision/).</span></span>

## <a name="migrate"></a> <span data-ttu-id="97b02-128">Step 2: Code Migration in action</span><span class="sxs-lookup"><span data-stu-id="97b02-128">Step 2: Code Migration in action</span></span>

<span data-ttu-id="97b02-129">This section only focuses on migrating PersonGroup/FaceList implementation to LargePersonGroup/LargeFaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-129">This section only focuses on migrating PersonGroup/FaceList implementation to LargePersonGroup/LargeFaceList.</span></span>
<span data-ttu-id="97b02-130">Although LargePersonGroup/LargeFaceList differs from PersonGroup/FaceList in design and internal implementation, the API interfaces are similar for back-compatibility.</span><span class="sxs-lookup"><span data-stu-id="97b02-130">Although LargePersonGroup/LargeFaceList differs from PersonGroup/FaceList in design and internal implementation, the API interfaces are similar for back-compatibility.</span></span>

<span data-ttu-id="97b02-131">Data migration is not supported, you have to recreate the LargePersonGroup/LargeFaceList instead.</span><span class="sxs-lookup"><span data-stu-id="97b02-131">Data migration is not supported, you have to recreate the LargePersonGroup/LargeFaceList instead.</span></span>

## <a name="largepersongroup"></a> <span data-ttu-id="97b02-132">Step 2.1: Migrate PersonGroup to LargePersonGroup</span><span class="sxs-lookup"><span data-stu-id="97b02-132">Step 2.1: Migrate PersonGroup to LargePersonGroup</span></span>

<span data-ttu-id="97b02-133">The migration from PersonGroup to LargePersonGroup is smooth as they share exactly the same group-level operations.</span><span class="sxs-lookup"><span data-stu-id="97b02-133">The migration from PersonGroup to LargePersonGroup is smooth as they share exactly the same group-level operations.</span></span>

<span data-ttu-id="97b02-134">For PersonGroup/Person related implementation, it is only necessary to change the API paths or SDK class/module to LargePersonGroup and LargePersonGroup Person.</span><span class="sxs-lookup"><span data-stu-id="97b02-134">For PersonGroup/Person related implementation, it is only necessary to change the API paths or SDK class/module to LargePersonGroup and LargePersonGroup Person.</span></span>

<span data-ttu-id="97b02-135">In terms of data migration, see [How to Add Faces](how-to-add-faces.md) for reference.</span><span class="sxs-lookup"><span data-stu-id="97b02-135">In terms of data migration, see [How to Add Faces](how-to-add-faces.md) for reference.</span></span>

## <a name="largefacelist"></a> <span data-ttu-id="97b02-136">Step 2.2: Migrate FaceList to LargeFaceList</span><span class="sxs-lookup"><span data-stu-id="97b02-136">Step 2.2: Migrate FaceList to LargeFaceList</span></span>

| <span data-ttu-id="97b02-137">FaceList APIs</span><span class="sxs-lookup"><span data-stu-id="97b02-137">FaceList APIs</span></span> | <span data-ttu-id="97b02-138">LargeFaceList APIs</span><span class="sxs-lookup"><span data-stu-id="97b02-138">LargeFaceList APIs</span></span> |
|:---:|:---:|
| <span data-ttu-id="97b02-139">Create</span><span class="sxs-lookup"><span data-stu-id="97b02-139">Create</span></span> | <span data-ttu-id="97b02-140">Create</span><span class="sxs-lookup"><span data-stu-id="97b02-140">Create</span></span> |
| <span data-ttu-id="97b02-141">Delete</span><span class="sxs-lookup"><span data-stu-id="97b02-141">Delete</span></span> | <span data-ttu-id="97b02-142">Delete</span><span class="sxs-lookup"><span data-stu-id="97b02-142">Delete</span></span> |
| <span data-ttu-id="97b02-143">Get</span><span class="sxs-lookup"><span data-stu-id="97b02-143">Get</span></span> | <span data-ttu-id="97b02-144">Get</span><span class="sxs-lookup"><span data-stu-id="97b02-144">Get</span></span> |
| <span data-ttu-id="97b02-145">List</span><span class="sxs-lookup"><span data-stu-id="97b02-145">List</span></span> | <span data-ttu-id="97b02-146">List</span><span class="sxs-lookup"><span data-stu-id="97b02-146">List</span></span> |
| <span data-ttu-id="97b02-147">Update</span><span class="sxs-lookup"><span data-stu-id="97b02-147">Update</span></span> | <span data-ttu-id="97b02-148">Update</span><span class="sxs-lookup"><span data-stu-id="97b02-148">Update</span></span> |
| - | <span data-ttu-id="97b02-149">Train</span><span class="sxs-lookup"><span data-stu-id="97b02-149">Train</span></span> |
| - | <span data-ttu-id="97b02-150">Get Training Status</span><span class="sxs-lookup"><span data-stu-id="97b02-150">Get Training Status</span></span> |

<span data-ttu-id="97b02-151">The preceding table is a comparison of list-level operations between FaceList and LargeFaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-151">The preceding table is a comparison of list-level operations between FaceList and LargeFaceList.</span></span>
<span data-ttu-id="97b02-152">As is shown, LargeFaceList comes with new operations, Train, and Get Training Status, when compared with FaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-152">As is shown, LargeFaceList comes with new operations, Train, and Get Training Status, when compared with FaceList.</span></span>
<span data-ttu-id="97b02-153">Getting the LargeFaceList trained is a precondition of [FindSimilar](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237) operation while there is no Train required for FaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-153">Getting the LargeFaceList trained is a precondition of [FindSimilar](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237) operation while there is no Train required for FaceList.</span></span>
<span data-ttu-id="97b02-154">The following snippet is a helper function to wait for the training of a LargeFaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-154">The following snippet is a helper function to wait for the training of a LargeFaceList.</span></span>

```CSharp
/// <summary>
/// Helper function to train LargeFaceList and wait for finish.
/// </summary>
/// <remarks>
/// The time interval can be adjusted considering the following factors:
/// - The training time which depends on the capacity of the LargeFaceList.
/// - The acceptable latency for getting the training status.
/// - The call frequency and cost.
///
/// Estimated training time for LargeFaceList in different scale:
/// -     1,000 faces cost about  1 to  2 seconds.
/// -    10,000 faces cost about  5 to 10 seconds.
/// -   100,000 faces cost about  1 to  2 minutes.
/// - 1,000,000 faces cost about 10 to 30 minutes.
/// </remarks>
/// <param name="largeFaceListId">The Id of the LargeFaceList for training.</param>
/// <param name="timeIntervalInMilliseconds">The time interval for getting training status in milliseconds.</param>
/// <returns>A task of waiting for LargeFaceList training finish.</returns>
private static async Task TrainLargeFaceList(
    string largeFaceListId,
    int timeIntervalInMilliseconds = 1000)
{
    // Trigger a train call.
    await FaceServiceClient.TrainLargeFaceListAsync(largeFaceListId);

    // Wait for training finish.
    while (true)
    {
        Task.Delay(timeIntervalInMilliseconds).Wait();
        var status = await FaceServiceClient.GetLargeFaceListTrainingStatusAsync(largeFaceListId);

        if (status.Status == Status.Running)
        {
            continue;
        }
        else if (status.Status == Status.Succeeded)
        {
            break;
        }
        else
        {
            throw new Exception("The train operation is failed!");
        }
    }
}
```

<span data-ttu-id="97b02-155">Previously, a typical usage of FaceList with adding faces and FindSimilar would be</span><span class="sxs-lookup"><span data-stu-id="97b02-155">Previously, a typical usage of FaceList with adding faces and FindSimilar would be</span></span>

```CSharp
// Create a FaceList.
const string FaceListId = "myfacelistid_001";
const string FaceListName = "MyFaceListDisplayName";
const string ImageDir = @"/path/to/FaceList/images";
FaceServiceClient.CreateFaceListAsync(FaceListId, FaceListName).Wait();

// Add Faces to the FaceList.
Parallel.ForEach(
    Directory.GetFiles(ImageDir, "*.jpg"),
    async imagePath =>
        {
            using (Stream stream = File.OpenRead(imagePath))
            {
                await FaceServiceClient.AddFaceToFaceListAsync(FaceListId, stream);
            }
        });

// Perform FindSimilar.
const string QueryImagePath = @"/path/to/query/image";
var results = new List<SimilarPersistedFace[]>();
using (Stream stream = File.OpenRead(QueryImagePath))
{
    var faces = FaceServiceClient.DetectAsync(stream).Result;
    foreach (var face in faces)
    {
        results.Add(await FaceServiceClient.FindSimilarAsync(face.FaceId, FaceListId, 20));
    }
}
```

<span data-ttu-id="97b02-156">When migrating it to LargeFaceList, it should become</span><span class="sxs-lookup"><span data-stu-id="97b02-156">When migrating it to LargeFaceList, it should become</span></span>

```CSharp
// Create a LargeFaceList.
const string LargeFaceListId = "mylargefacelistid_001";
const string LargeFaceListName = "MyLargeFaceListDisplayName";
const string ImageDir = @"/path/to/FaceList/images";
FaceServiceClient.CreateLargeFaceListAsync(LargeFaceListId, LargeFaceListName).Wait();

// Add Faces to the LargeFaceList.
Parallel.ForEach(
    Directory.GetFiles(ImageDir, "*.jpg"),
    async imagePath =>
        {
            using (Stream stream = File.OpenRead(imagePath))
            {
                await FaceServiceClient.AddFaceToLargeFaceListAsync(LargeFaceListId, stream);
            }
        });

// Train() is newly added operation for LargeFaceList.
// Must call it before FindSimilarAsync() to ensure the newly added faces searchable.
await TrainLargeFaceList(LargeFaceListId);

// Perform FindSimilar.
const string QueryImagePath = @"/path/to/query/image";
var results = new List<SimilarPersistedFace[]>();
using (Stream stream = File.OpenRead(QueryImagePath))
{
    var faces = FaceServiceClient.DetectAsync(stream).Result;
    foreach (var face in faces)
    {
        results.Add(await FaceServiceClient.FindSimilarAsync(face.FaceId, largeFaceListId: LargeFaceListId));
    }
}
```

<span data-ttu-id="97b02-157">As is shown above, the data management and the FindSimilar part are almost the same.</span><span class="sxs-lookup"><span data-stu-id="97b02-157">As is shown above, the data management and the FindSimilar part are almost the same.</span></span>
<span data-ttu-id="97b02-158">The only exception is that a fresh pre-processing Train operation must complete in the LargeFaceList before FindSimilar works.</span><span class="sxs-lookup"><span data-stu-id="97b02-158">The only exception is that a fresh pre-processing Train operation must complete in the LargeFaceList before FindSimilar works.</span></span>

## <a name="train"></a><span data-ttu-id="97b02-159">Step 3: Train Suggestions</span><span class="sxs-lookup"><span data-stu-id="97b02-159">Step 3: Train Suggestions</span></span>

<span data-ttu-id="97b02-160">Although the Train operation speeds up the [FindSimilar](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237) and [Identification](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), the training time suffers especially when coming to large scale.</span><span class="sxs-lookup"><span data-stu-id="97b02-160">Although the Train operation speeds up the [FindSimilar](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237) and [Identification](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), the training time suffers especially when coming to large scale.</span></span>
<span data-ttu-id="97b02-161">The estimated training time in different scales is listed in the following table:</span><span class="sxs-lookup"><span data-stu-id="97b02-161">The estimated training time in different scales is listed in the following table:</span></span>

| <span data-ttu-id="97b02-162">Scale (faces or persons)</span><span class="sxs-lookup"><span data-stu-id="97b02-162">Scale (faces or persons)</span></span> | <span data-ttu-id="97b02-163">Estimated Training Time</span><span class="sxs-lookup"><span data-stu-id="97b02-163">Estimated Training Time</span></span> |
|:---:|:---:|
| <span data-ttu-id="97b02-164">1,000</span><span class="sxs-lookup"><span data-stu-id="97b02-164">1,000</span></span> | <span data-ttu-id="97b02-165">1-2 s</span><span class="sxs-lookup"><span data-stu-id="97b02-165">1-2 s</span></span> |
| <span data-ttu-id="97b02-166">10,000</span><span class="sxs-lookup"><span data-stu-id="97b02-166">10,000</span></span> | <span data-ttu-id="97b02-167">5-10 s</span><span class="sxs-lookup"><span data-stu-id="97b02-167">5-10 s</span></span> |
| <span data-ttu-id="97b02-168">100,000</span><span class="sxs-lookup"><span data-stu-id="97b02-168">100,000</span></span> | <span data-ttu-id="97b02-169">1 - 2 min</span><span class="sxs-lookup"><span data-stu-id="97b02-169">1 - 2 min</span></span> |
| <span data-ttu-id="97b02-170">1,000,000</span><span class="sxs-lookup"><span data-stu-id="97b02-170">1,000,000</span></span> | <span data-ttu-id="97b02-171">10 - 30 min</span><span class="sxs-lookup"><span data-stu-id="97b02-171">10 - 30 min</span></span> |

<span data-ttu-id="97b02-172">To better utilize the large-scale feature, some strategies are recommended to take into consideration.</span><span class="sxs-lookup"><span data-stu-id="97b02-172">To better utilize the large-scale feature, some strategies are recommended to take into consideration.</span></span>

## <a name="interval"></a><span data-ttu-id="97b02-173">Step 3.1: Customize Time Interval</span><span class="sxs-lookup"><span data-stu-id="97b02-173">Step 3.1: Customize Time Interval</span></span>

<span data-ttu-id="97b02-174">As is shown in the `TrainLargeFaceList()`, there is a `timeIntervalInMilliseconds` to delay the infinite training status checking process.</span><span class="sxs-lookup"><span data-stu-id="97b02-174">As is shown in the `TrainLargeFaceList()`, there is a `timeIntervalInMilliseconds` to delay the infinite training status checking process.</span></span>
<span data-ttu-id="97b02-175">For LargeFaceList with more faces, using a larger interval reduces the call counts and cost.</span><span class="sxs-lookup"><span data-stu-id="97b02-175">For LargeFaceList with more faces, using a larger interval reduces the call counts and cost.</span></span>
<span data-ttu-id="97b02-176">The time interval should be customized according to the expected capacity of the LargeFaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-176">The time interval should be customized according to the expected capacity of the LargeFaceList.</span></span>

<span data-ttu-id="97b02-177">Same strategy also applies to LargePersonGroup.</span><span class="sxs-lookup"><span data-stu-id="97b02-177">Same strategy also applies to LargePersonGroup.</span></span>
<span data-ttu-id="97b02-178">For example, when training a LargePersonGroup with 1,000,000 persons, the `timeIntervalInMilliseconds` could be 60,000 (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="97b02-178">For example, when training a LargePersonGroup with 1,000,000 persons, the `timeIntervalInMilliseconds` could be 60,000 (a.k.a.</span></span> <span data-ttu-id="97b02-179">1-minute interval).</span><span class="sxs-lookup"><span data-stu-id="97b02-179">1-minute interval).</span></span>

## <a name="buffer"></a><span data-ttu-id="97b02-180">Step 3.2 Small-scale buffer</span><span class="sxs-lookup"><span data-stu-id="97b02-180">Step 3.2 Small-scale buffer</span></span>

<span data-ttu-id="97b02-181">Persons/Faces in LargePersonGroup/LargeFaceList are searchable only after being trained.</span><span class="sxs-lookup"><span data-stu-id="97b02-181">Persons/Faces in LargePersonGroup/LargeFaceList are searchable only after being trained.</span></span>
<span data-ttu-id="97b02-182">In a dynamic scenario, new persons/faces are constantly added and need to be immediately searchable, yet training could take longer than desired.</span><span class="sxs-lookup"><span data-stu-id="97b02-182">In a dynamic scenario, new persons/faces are constantly added and need to be immediately searchable, yet training could take longer than desired.</span></span>
<span data-ttu-id="97b02-183">To mitigate this problem, you can use an extra small-scale LargePersonGroup/LargeFaceList as a buffer only for the newly added entries.</span><span class="sxs-lookup"><span data-stu-id="97b02-183">To mitigate this problem, you can use an extra small-scale LargePersonGroup/LargeFaceList as a buffer only for the newly added entries.</span></span>
<span data-ttu-id="97b02-184">This buffer takes shorter time to train because of much smaller size and the immediate search on this temporary buffer should work.</span><span class="sxs-lookup"><span data-stu-id="97b02-184">This buffer takes shorter time to train because of much smaller size and the immediate search on this temporary buffer should work.</span></span>
<span data-ttu-id="97b02-185">Use this buffer in combination with training on the master LargePersonGroup/LargeFaceList by executing the master training on a more sparse interval, for example, in the mid-night, and daily.</span><span class="sxs-lookup"><span data-stu-id="97b02-185">Use this buffer in combination with training on the master LargePersonGroup/LargeFaceList by executing the master training on a more sparse interval, for example, in the mid-night, and daily.</span></span>

<span data-ttu-id="97b02-186">An example workflow:</span><span class="sxs-lookup"><span data-stu-id="97b02-186">An example workflow:</span></span>
1. <span data-ttu-id="97b02-187">Create a master LargePersonGroup/LargeFaceList (master collection) and a buffer LargePersonGroup/LargeFaceList (buffer collection).</span><span class="sxs-lookup"><span data-stu-id="97b02-187">Create a master LargePersonGroup/LargeFaceList (master collection) and a buffer LargePersonGroup/LargeFaceList (buffer collection).</span></span> <span data-ttu-id="97b02-188">The buffer collection is only for newly added Persons/Faces.</span><span class="sxs-lookup"><span data-stu-id="97b02-188">The buffer collection is only for newly added Persons/Faces.</span></span>
1. <span data-ttu-id="97b02-189">Add new Persons/Faces to both the master collection and the buffer collection.</span><span class="sxs-lookup"><span data-stu-id="97b02-189">Add new Persons/Faces to both the master collection and the buffer collection.</span></span>
1. <span data-ttu-id="97b02-190">Only train the buffer collection with a short time interval to ensure the newly added entries taking effect.</span><span class="sxs-lookup"><span data-stu-id="97b02-190">Only train the buffer collection with a short time interval to ensure the newly added entries taking effect.</span></span>
1. <span data-ttu-id="97b02-191">Call Identification/FindSimilar against both the master collection and the buffer collection, and merge the results.</span><span class="sxs-lookup"><span data-stu-id="97b02-191">Call Identification/FindSimilar against both the master collection and the buffer collection, and merge the results.</span></span>
1. <span data-ttu-id="97b02-192">When buffer collection size increases to a threshold or at a system idle time, create a new buffer collection and trigger the train on master collection.</span><span class="sxs-lookup"><span data-stu-id="97b02-192">When buffer collection size increases to a threshold or at a system idle time, create a new buffer collection and trigger the train on master collection.</span></span>
1. <span data-ttu-id="97b02-193">Delete the old buffer collection after the finish of training on the master collection.</span><span class="sxs-lookup"><span data-stu-id="97b02-193">Delete the old buffer collection after the finish of training on the master collection.</span></span>

## <a name="standalone"></a><span data-ttu-id="97b02-194">Step 3.3 Standalone Training</span><span class="sxs-lookup"><span data-stu-id="97b02-194">Step 3.3 Standalone Training</span></span>

<span data-ttu-id="97b02-195">If a relatively long latency is acceptable, it is not necessary to trigger the Train operation right after adding new data.</span><span class="sxs-lookup"><span data-stu-id="97b02-195">If a relatively long latency is acceptable, it is not necessary to trigger the Train operation right after adding new data.</span></span>
<span data-ttu-id="97b02-196">Instead, the Train operation can be split from the main logic and triggered regularly.</span><span class="sxs-lookup"><span data-stu-id="97b02-196">Instead, the Train operation can be split from the main logic and triggered regularly.</span></span>
<span data-ttu-id="97b02-197">This strategy is suitable for dynamic scenarios with acceptable latency, and can be applied to static scenarios to further reduce the Train frequency.</span><span class="sxs-lookup"><span data-stu-id="97b02-197">This strategy is suitable for dynamic scenarios with acceptable latency, and can be applied to static scenarios to further reduce the Train frequency.</span></span>

<span data-ttu-id="97b02-198">Suppose there is a `TrainLargePersonGroup` function similar to the `TrainLargeFaceList`.</span><span class="sxs-lookup"><span data-stu-id="97b02-198">Suppose there is a `TrainLargePersonGroup` function similar to the `TrainLargeFaceList`.</span></span>
<span data-ttu-id="97b02-199">A typical implementation of the standalone Training on LargePersonGroup by invoking the [`Timer`](https://msdn.microsoft.com/library/system.timers.timer(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="97b02-199">A typical implementation of the standalone Training on LargePersonGroup by invoking the [`Timer`](https://msdn.microsoft.com/library/system.timers.timer(v=vs.110).aspx)</span></span>
<span data-ttu-id="97b02-200">class in `System.Timers` would be:</span><span class="sxs-lookup"><span data-stu-id="97b02-200">class in `System.Timers` would be:</span></span>

```CSharp
private static void Main()
{
    // Create a LargePersonGroup.
    const string LargePersonGroupId = "mylargepersongroupid_001";
    const string LargePersonGroupName = "MyLargePersonGroupDisplayName";
    FaceServiceClient.CreateLargePersonGroupAsync(LargePersonGroupId, LargePersonGroupName).Wait();

    // Setup a standalone training at regular intervals.
    const int TimeIntervalForStatus = 1000 * 60; // 1 minute interval for getting training status.
    const double TimeIntervalForTrain = 1000 * 60 * 60; // 1 hour interval for training.
    var trainTimer = new Timer(TimeIntervalForTrain);
    trainTimer.Elapsed += (sender, args) => TrainTimerOnElapsed(LargePersonGroupId, TimeIntervalForStatus);
    trainTimer.AutoReset = true;
    trainTimer.Enabled = true;

    // Other operations like creating persons, adding faces and Identification except for Train.
    // ...
}

private static void TrainTimerOnElapsed(string largePersonGroupId, int timeIntervalInMilliseconds)
{
    TrainLargePersonGroup(largePersonGroupId, timeIntervalInMilliseconds).Wait();
}
```

<span data-ttu-id="97b02-201">More information about data management and identification-related implementations, see [How to Add Faces](how-to-add-faces.md) and [How to Identify Faces in Image](HowtoIdentifyFacesinImage.md).</span><span class="sxs-lookup"><span data-stu-id="97b02-201">More information about data management and identification-related implementations, see [How to Add Faces](how-to-add-faces.md) and [How to Identify Faces in Image](HowtoIdentifyFacesinImage.md).</span></span>

## <a name="summary"></a> <span data-ttu-id="97b02-202">Summary</span><span class="sxs-lookup"><span data-stu-id="97b02-202">Summary</span></span>

<span data-ttu-id="97b02-203">In this guide, you have learned how to migrate the existing PersonGroup/FaceList code (not data) to the LargePersonGroup/LargeFaceList:</span><span class="sxs-lookup"><span data-stu-id="97b02-203">In this guide, you have learned how to migrate the existing PersonGroup/FaceList code (not data) to the LargePersonGroup/LargeFaceList:</span></span>

- <span data-ttu-id="97b02-204">LargePersonGroup and LargeFaceList works similar to the PersonGroup/FaceList, except Train operation is required by LargeFaceList.</span><span class="sxs-lookup"><span data-stu-id="97b02-204">LargePersonGroup and LargeFaceList works similar to the PersonGroup/FaceList, except Train operation is required by LargeFaceList.</span></span>
- <span data-ttu-id="97b02-205">Take proper train strategy to dynamic data update for large-scale dataset.</span><span class="sxs-lookup"><span data-stu-id="97b02-205">Take proper train strategy to dynamic data update for large-scale dataset.</span></span>

## <a name="related"></a> <span data-ttu-id="97b02-206">Related Topics</span><span class="sxs-lookup"><span data-stu-id="97b02-206">Related Topics</span></span>

- [<span data-ttu-id="97b02-207">How to Identify Faces in Image</span><span class="sxs-lookup"><span data-stu-id="97b02-207">How to Identify Faces in Image</span></span>](HowtoIdentifyFacesinImage.md)
- [<span data-ttu-id="97b02-208">How to Add Faces</span><span class="sxs-lookup"><span data-stu-id="97b02-208">How to Add Faces</span></span>](how-to-add-faces.md)
