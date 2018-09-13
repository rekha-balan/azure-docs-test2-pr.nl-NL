---
title: Add faces with the Face API | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Use the Face API in Cognitive Services to add faces in images.
services: cognitive-services
author: SteveMSFT
manager: corncar
ms.service: cognitive-services
ms.component: face-api
ms.topic: article
ms.date: 03/01/2018
ms.author: sbowles
ms.openlocfilehash: 3306c13d6c3d231ddbda38cfcbc5419fcdbd30db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867603"
---
# <a name="how-to-add-faces"></a><span data-ttu-id="07b4c-103">How to add faces</span><span class="sxs-lookup"><span data-stu-id="07b4c-103">How to add faces</span></span>

<span data-ttu-id="07b4c-104">This guide demonstrates the best practice to add massive number of persons and faces to a PersonGroup.</span><span class="sxs-lookup"><span data-stu-id="07b4c-104">This guide demonstrates the best practice to add massive number of persons and faces to a PersonGroup.</span></span>
<span data-ttu-id="07b4c-105">The same strategy also applies to FaceList and LargePersonGroup.</span><span class="sxs-lookup"><span data-stu-id="07b4c-105">The same strategy also applies to FaceList and LargePersonGroup.</span></span>
<span data-ttu-id="07b4c-106">The samples are written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="07b4c-106">The samples are written in C# using the Face API client library.</span></span>

## <a name="step1"></a> <span data-ttu-id="07b4c-107">Step 1: Initialization</span><span class="sxs-lookup"><span data-stu-id="07b4c-107">Step 1: Initialization</span></span>

<span data-ttu-id="07b4c-108">Several variables are declared and a helper function is implemented to schedule the requests.</span><span class="sxs-lookup"><span data-stu-id="07b4c-108">Several variables are declared and a helper function is implemented to schedule the requests.</span></span>

- <span data-ttu-id="07b4c-109">`PersonCount` is the total number of persons.</span><span class="sxs-lookup"><span data-stu-id="07b4c-109">`PersonCount` is the total number of persons.</span></span>
- <span data-ttu-id="07b4c-110">`CallLimitPerSecond` is the maximum calls per second according to the subscription tier.</span><span class="sxs-lookup"><span data-stu-id="07b4c-110">`CallLimitPerSecond` is the maximum calls per second according to the subscription tier.</span></span>
- <span data-ttu-id="07b4c-111">`_timeStampQueue` is a Queue to record the request timestamps.</span><span class="sxs-lookup"><span data-stu-id="07b4c-111">`_timeStampQueue` is a Queue to record the request timestamps.</span></span>
- <span data-ttu-id="07b4c-112">`await WaitCallLimitPerSecondAsync()` will wait until it is valid to send next request.</span><span class="sxs-lookup"><span data-stu-id="07b4c-112">`await WaitCallLimitPerSecondAsync()` will wait until it is valid to send next request.</span></span>

```CSharp
const int PersonCount = 10000;
const int CallLimitPerSecond = 10;
static Queue<DateTime> _timeStampQueue = new Queue<DateTime>(CallLimitPerSecond);

static async Task WaitCallLimitPerSecondAsync()
{
    Monitor.Enter(_timeStampQueue);
    try
    {
        if (_timeStampQueue.Count >= CallLimitPerSecond)
        {
            TimeSpan timeInterval = DateTime.UtcNow - _timeStampQueue.Peek();
            if (timeInterval < TimeSpan.FromSeconds(1))
            {
                await Task.Delay(TimeSpan.FromSeconds(1) - timeInterval);
            }
            _timeStampQueue.Dequeue();
        }
        _timeStampQueue.Enqueue(DateTime.UtcNow);
    }
    finally
    {
        Monitor.Exit(_timeStampQueue);
    }
}
```

## <a name="step2"></a> <span data-ttu-id="07b4c-113">Step 2: Authorize the API call</span><span class="sxs-lookup"><span data-stu-id="07b4c-113">Step 2: Authorize the API call</span></span>

<span data-ttu-id="07b4c-114">When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="07b4c-114">When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span></span> <span data-ttu-id="07b4c-115">For example:</span><span class="sxs-lookup"><span data-stu-id="07b4c-115">For example:</span></span>

```CSharp
FaceServiceClient faceServiceClient = new FaceServiceClient("<Subscription Key>");
```

<span data-ttu-id="07b4c-116">The subscription key can be obtained from the Marketplace page of your Azure portal.</span><span class="sxs-lookup"><span data-stu-id="07b4c-116">The subscription key can be obtained from the Marketplace page of your Azure portal.</span></span> <span data-ttu-id="07b4c-117">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="07b4c-117">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span>

## <a name="step3"></a> <span data-ttu-id="07b4c-118">Step 3: Create the PersonGroup</span><span class="sxs-lookup"><span data-stu-id="07b4c-118">Step 3: Create the PersonGroup</span></span>

<span data-ttu-id="07b4c-119">A PersonGroup named "MyPersonGroup" is created to save the persons.</span><span class="sxs-lookup"><span data-stu-id="07b4c-119">A PersonGroup named "MyPersonGroup" is created to save the persons.</span></span>
<span data-ttu-id="07b4c-120">The request time is enqueued to `_timeStampQueue` to ensure the overall validation.</span><span class="sxs-lookup"><span data-stu-id="07b4c-120">The request time is enqueued to `_timeStampQueue` to ensure the overall validation.</span></span>

```CSharp
const string personGroupId = "mypersongroupid";
const string personGroupName = "MyPersonGroup";
_timeStampQueue.Enqueue(DateTime.UtcNow);
await faceServiceClient.CreatePersonGroupAsync(personGroupId, personGroupName);
```

## <a name="step4"></a> <span data-ttu-id="07b4c-121">Step 4: Create the persons to the PersonGroup</span><span class="sxs-lookup"><span data-stu-id="07b4c-121">Step 4: Create the persons to the PersonGroup</span></span>

<span data-ttu-id="07b4c-122">Persons are created concurrently and `await WaitCallLimitPerSecondAsync()` is also applied to avoid exceeding the call limit.</span><span class="sxs-lookup"><span data-stu-id="07b4c-122">Persons are created concurrently and `await WaitCallLimitPerSecondAsync()` is also applied to avoid exceeding the call limit.</span></span>

```CSharp
CreatePersonResult[] persons = new CreatePersonResult[PersonCount];
Parallel.For(0, PersonCount, async i =>
{
    await WaitCallLimitPerSecondAsync();

    string personName = $"PersonName#{i}";
    persons[i] = await faceServiceClient.CreatePersonAsync(personGroupId, personName);
});
```

## <a name="step5"></a> <span data-ttu-id="07b4c-123">Step 5: Add faces to the persons</span><span class="sxs-lookup"><span data-stu-id="07b4c-123">Step 5: Add faces to the persons</span></span>

<span data-ttu-id="07b4c-124">Adding faces to different persons are processed concurrently, while for one specific person is sequential.</span><span class="sxs-lookup"><span data-stu-id="07b4c-124">Adding faces to different persons are processed concurrently, while for one specific person is sequential.</span></span>
<span data-ttu-id="07b4c-125">Again, `await WaitCallLimitPerSecondAsync()` is invoked to ensure the request frequency is within the scope of limitation.</span><span class="sxs-lookup"><span data-stu-id="07b4c-125">Again, `await WaitCallLimitPerSecondAsync()` is invoked to ensure the request frequency is within the scope of limitation.</span></span>

```CSharp
Parallel.For(0, PersonCount, async i =>
{
    Guid personId = persons[i].PersonId;
    string personImageDir = @"/path/to/person/i/images";

    foreach (string imagePath in Directory.GetFiles(personImageDir, "*.jpg"))
    {
        await WaitCallLimitPerSecondAsync();

        using (Stream stream = File.OpenRead(imagePath))
        {
            await faceServiceClient.AddPersonFaceAsync(personGroupId, personId, stream);
        }
    }
});
```

## <a name="summary"></a> <span data-ttu-id="07b4c-126">Summary</span><span class="sxs-lookup"><span data-stu-id="07b4c-126">Summary</span></span>

<span data-ttu-id="07b4c-127">In this guide, you have learned the process of creating a PersonGroup with massive number of persons and faces.</span><span class="sxs-lookup"><span data-stu-id="07b4c-127">In this guide, you have learned the process of creating a PersonGroup with massive number of persons and faces.</span></span> <span data-ttu-id="07b4c-128">Several reminders:</span><span class="sxs-lookup"><span data-stu-id="07b4c-128">Several reminders:</span></span>

- <span data-ttu-id="07b4c-129">This strategy also applies to FaceList and LargePersonGroup.</span><span class="sxs-lookup"><span data-stu-id="07b4c-129">This strategy also applies to FaceList and LargePersonGroup.</span></span>
- <span data-ttu-id="07b4c-130">Adding/Deleting faces to different FaceLists or Persons in LargePersonGroup can be processed concurrently.</span><span class="sxs-lookup"><span data-stu-id="07b4c-130">Adding/Deleting faces to different FaceLists or Persons in LargePersonGroup can be processed concurrently.</span></span>
- <span data-ttu-id="07b4c-131">Same operations to one specific FaceList or Person in LargePersonGroup should be done sequentially.</span><span class="sxs-lookup"><span data-stu-id="07b4c-131">Same operations to one specific FaceList or Person in LargePersonGroup should be done sequentially.</span></span>
- <span data-ttu-id="07b4c-132">To keep the simplicity, the handling of potential exception is omitted in this guide.</span><span class="sxs-lookup"><span data-stu-id="07b4c-132">To keep the simplicity, the handling of potential exception is omitted in this guide.</span></span> <span data-ttu-id="07b4c-133">If you want to enhance more robustness, proper retry policy should be applied.</span><span class="sxs-lookup"><span data-stu-id="07b4c-133">If you want to enhance more robustness, proper retry policy should be applied.</span></span>

<span data-ttu-id="07b4c-134">The following are a quick reminder of the features previously explained and demonstrated:</span><span class="sxs-lookup"><span data-stu-id="07b4c-134">The following are a quick reminder of the features previously explained and demonstrated:</span></span>

- <span data-ttu-id="07b4c-135">Creating PersonGroups using the [PersonGroup - Create](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) API</span><span class="sxs-lookup"><span data-stu-id="07b4c-135">Creating PersonGroups using the [PersonGroup - Create](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) API</span></span>
- <span data-ttu-id="07b4c-136">Creating persons using the [PersonGroup Person - Create](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c) API</span><span class="sxs-lookup"><span data-stu-id="07b4c-136">Creating persons using the [PersonGroup Person - Create](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c) API</span></span>
- <span data-ttu-id="07b4c-137">Adding faces to persons using the [PersonGroup Person - Add Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) API</span><span class="sxs-lookup"><span data-stu-id="07b4c-137">Adding faces to persons using the [PersonGroup Person - Add Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) API</span></span>

## <a name="related"></a> <span data-ttu-id="07b4c-138">Related Topics</span><span class="sxs-lookup"><span data-stu-id="07b4c-138">Related Topics</span></span>
- [<span data-ttu-id="07b4c-139">How to Identify Faces in Image</span><span class="sxs-lookup"><span data-stu-id="07b4c-139">How to Identify Faces in Image</span></span>](HowtoIdentifyFacesinImage.md)
- [<span data-ttu-id="07b4c-140">How to Detect Faces in Image</span><span class="sxs-lookup"><span data-stu-id="07b4c-140">How to Detect Faces in Image</span></span>](HowtoDetectFacesinImage.md)
- [<span data-ttu-id="07b4c-141">How to use the large-scale feature</span><span class="sxs-lookup"><span data-stu-id="07b4c-141">How to use the large-scale feature</span></span>](how-to-use-large-scale.md)
