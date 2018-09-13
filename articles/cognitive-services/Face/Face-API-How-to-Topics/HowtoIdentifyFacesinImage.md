---
title: Identify faces in images with the Face API | Microsoft Docs
description: Use the Face API in Cognitive Services to identify faces in images.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 02/06/2017
ms.author: anroth
ms.openlocfilehash: c2454c0797a693aa3934757d20d81b3860d22313
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550709"
---
# <a name="how-to-identify-faces-in-image"></a><span data-ttu-id="491d9-103">How to Identify Faces in Image</span><span class="sxs-lookup"><span data-stu-id="491d9-103">How to Identify Faces in Image</span></span>

<span data-ttu-id="491d9-104">This guide will demonstrate how to identify unknown faces using person groups, which are created from known people in advance.</span><span class="sxs-lookup"><span data-stu-id="491d9-104">This guide will demonstrate how to identify unknown faces using person groups, which are created from known people in advance.</span></span> <span data-ttu-id="491d9-105">The samples are written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="491d9-105">The samples are written in C# using the Face API client library.</span></span>

## <a name="concepts"></a> <span data-ttu-id="491d9-106">Concepts</span><span class="sxs-lookup"><span data-stu-id="491d9-106">Concepts</span></span>

<span data-ttu-id="491d9-107">If you are not familiar with the following concepts in this guide, please search for the definitions in our [glossary](../Glossary.md) at any time:</span><span class="sxs-lookup"><span data-stu-id="491d9-107">If you are not familiar with the following concepts in this guide, please search for the definitions in our [glossary](../Glossary.md) at any time:</span></span>

- <span data-ttu-id="491d9-108">Face - Detect</span><span class="sxs-lookup"><span data-stu-id="491d9-108">Face - Detect</span></span>
- <span data-ttu-id="491d9-109">Face - Identify</span><span class="sxs-lookup"><span data-stu-id="491d9-109">Face - Identify</span></span>
- <span data-ttu-id="491d9-110">Person Group</span><span class="sxs-lookup"><span data-stu-id="491d9-110">Person Group</span></span>

## <a name="preparation"></a> <span data-ttu-id="491d9-111">Preparation</span><span class="sxs-lookup"><span data-stu-id="491d9-111">Preparation</span></span>

<span data-ttu-id="491d9-112">In this sample, we will demonstrate the following:</span><span class="sxs-lookup"><span data-stu-id="491d9-112">In this sample, we will demonstrate the following:</span></span>

- <span data-ttu-id="491d9-113">How to create a person group - This person group contains a list of known people.</span><span class="sxs-lookup"><span data-stu-id="491d9-113">How to create a person group - This person group contains a list of known people.</span></span>
- <span data-ttu-id="491d9-114">How to assign faces to each person - These faces are used as a baseline to identify people.</span><span class="sxs-lookup"><span data-stu-id="491d9-114">How to assign faces to each person - These faces are used as a baseline to identify people.</span></span> <span data-ttu-id="491d9-115">It is recommended to use clear front faces, just like your photo ID.</span><span class="sxs-lookup"><span data-stu-id="491d9-115">It is recommended to use clear front faces, just like your photo ID.</span></span> <span data-ttu-id="491d9-116">A good set of photos should contain faces of the same person, yet have different poses, clothes colors or hair styles.</span><span class="sxs-lookup"><span data-stu-id="491d9-116">A good set of photos should contain faces of the same person, yet have different poses, clothes colors or hair styles.</span></span>

<span data-ttu-id="491d9-117">To carry out the demonstration of this sample, you will need to prepare a bunch of pictures:</span><span class="sxs-lookup"><span data-stu-id="491d9-117">To carry out the demonstration of this sample, you will need to prepare a bunch of pictures:</span></span>

- <span data-ttu-id="491d9-118">A few photos with the person's face.</span><span class="sxs-lookup"><span data-stu-id="491d9-118">A few photos with the person's face.</span></span> <span data-ttu-id="491d9-119">[Click here to download sample photos](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data) for Anna, Bill and Clare.</span><span class="sxs-lookup"><span data-stu-id="491d9-119">[Click here to download sample photos](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data) for Anna, Bill and Clare.</span></span>
- <span data-ttu-id="491d9-120">A series of test photos, which may or may not contain the faces of Anna, Bill or Clare used to test their identification.</span><span class="sxs-lookup"><span data-stu-id="491d9-120">A series of test photos, which may or may not contain the faces of Anna, Bill or Clare used to test their identification.</span></span> <span data-ttu-id="491d9-121">You can also select some sample images from the link above.</span><span class="sxs-lookup"><span data-stu-id="491d9-121">You can also select some sample images from the link above.</span></span>

## <a name="step1"></a> <span data-ttu-id="491d9-122">Step 1: Authorize the API call</span><span class="sxs-lookup"><span data-stu-id="491d9-122">Step 1: Authorize the API call</span></span>

<span data-ttu-id="491d9-123">Every call to the Face API requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="491d9-123">Every call to the Face API requires a subscription key.</span></span> <span data-ttu-id="491d9-124">This key needs to be either passed through a query string parameter, or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="491d9-124">This key needs to be either passed through a query string parameter, or specified in the request header.</span></span> <span data-ttu-id="491d9-125">To pass the subscription key through query string, please refer to the request URL for the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) as an example:</span><span class="sxs-lookup"><span data-stu-id="491d9-125">To pass the subscription key through query string, please refer to the request URL for the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) as an example:</span></span>
```
https://westus.api.cognitive.microsoft.com/face/v1.0/detect[?returnFaceId][&returnFaceLandmarks][&returnFaceAttributes]
&subscription-key=<Your subscription key>
```

<span data-ttu-id="491d9-126">As an alternative, the subscription key can also be specified in the HTTP request header: **ocp-apim-subscription-key: &lt;Your subscription key&gt;** When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="491d9-126">As an alternative, the subscription key can also be specified in the HTTP request header: **ocp-apim-subscription-key: &lt;Your subscription key&gt;** When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span></span> <span data-ttu-id="491d9-127">For example:</span><span class="sxs-lookup"><span data-stu-id="491d9-127">For example:</span></span>
 
```CSharp 
faceServiceClient = new FaceServiceClient("Your subscription key");
```
 
<span data-ttu-id="491d9-128">The subscription key can be obtained from the Marketplace page of your Azure management portal.</span><span class="sxs-lookup"><span data-stu-id="491d9-128">The subscription key can be obtained from the Marketplace page of your Azure management portal.</span></span> <span data-ttu-id="491d9-129">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="491d9-129">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span>

## <a name="step2"></a> <span data-ttu-id="491d9-130">Step 2: Create the person group</span><span class="sxs-lookup"><span data-stu-id="491d9-130">Step 2: Create the person group</span></span>

<span data-ttu-id="491d9-131">In this step, we created a person group named "MyFriends" that contains three people: Anna, Bill and Chare.</span><span class="sxs-lookup"><span data-stu-id="491d9-131">In this step, we created a person group named "MyFriends" that contains three people: Anna, Bill and Chare.</span></span> <span data-ttu-id="491d9-132">Each person will have several faces registered.</span><span class="sxs-lookup"><span data-stu-id="491d9-132">Each person will have several faces registered.</span></span> <span data-ttu-id="491d9-133">The faces need to be detected from the images.</span><span class="sxs-lookup"><span data-stu-id="491d9-133">The faces need to be detected from the images.</span></span> <span data-ttu-id="491d9-134">After all of these steps, you will have a person group like the image below:</span><span class="sxs-lookup"><span data-stu-id="491d9-134">After all of these steps, you will have a person group like the image below:</span></span>

![HowToIdentify1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/group.image.1.jpg)

### <a name="step2-1"></a> <span data-ttu-id="491d9-136">2.1 Define people for the person group</span><span class="sxs-lookup"><span data-stu-id="491d9-136">2.1 Define people for the person group</span></span>
<span data-ttu-id="491d9-137">A person is a basic unit of identify.</span><span class="sxs-lookup"><span data-stu-id="491d9-137">A person is a basic unit of identify.</span></span> <span data-ttu-id="491d9-138">A person can have one or more known faces registered.</span><span class="sxs-lookup"><span data-stu-id="491d9-138">A person can have one or more known faces registered.</span></span> <span data-ttu-id="491d9-139">However, a person group is a collection of people, and each person is defined within a particular person group.</span><span class="sxs-lookup"><span data-stu-id="491d9-139">However, a person group is a collection of people, and each person is defined within a particular person group.</span></span> <span data-ttu-id="491d9-140">The identify is done against a person group.</span><span class="sxs-lookup"><span data-stu-id="491d9-140">The identify is done against a person group.</span></span> <span data-ttu-id="491d9-141">So, the task is to create a person group, and then create people in it, such as Anna, Bill, and Clare.</span><span class="sxs-lookup"><span data-stu-id="491d9-141">So, the task is to create a person group, and then create people in it, such as Anna, Bill, and Clare.</span></span>

<span data-ttu-id="491d9-142">First, you need to create a new person group.</span><span class="sxs-lookup"><span data-stu-id="491d9-142">First, you need to create a new person group.</span></span> <span data-ttu-id="491d9-143">This is executed by using the [Person Group - Create a Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) API.</span><span class="sxs-lookup"><span data-stu-id="491d9-143">This is executed by using the [Person Group - Create a Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) API.</span></span> <span data-ttu-id="491d9-144">The corresponding client library API is the CreatePersonGroupAsync method for the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="491d9-144">The corresponding client library API is the CreatePersonGroupAsync method for the FaceServiceClient class.</span></span> <span data-ttu-id="491d9-145">The group ID specified to create the group is unique for each subscription –you can also get, update or delete person groups using other person group APIs.</span><span class="sxs-lookup"><span data-stu-id="491d9-145">The group ID specified to create the group is unique for each subscription –you can also get, update or delete person groups using other person group APIs.</span></span> <span data-ttu-id="491d9-146">Once a group is defined, people can then be defined within it by using the [Person - Create a Person](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c) API.</span><span class="sxs-lookup"><span data-stu-id="491d9-146">Once a group is defined, people can then be defined within it by using the [Person - Create a Person](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c) API.</span></span> <span data-ttu-id="491d9-147">The client library method is CreatePersonAsync.</span><span class="sxs-lookup"><span data-stu-id="491d9-147">The client library method is CreatePersonAsync.</span></span> <span data-ttu-id="491d9-148">You can add face to each person after they're created.</span><span class="sxs-lookup"><span data-stu-id="491d9-148">You can add face to each person after they're created.</span></span>

```CSharp 
// Create an empty person group
string personGroupId = "myfriends";
await faceServiceClient.CreatePersonGroupAsync(personGroupId, "My Friends");
 
// Define Anna
CreatePersonResult friend1 = await faceServiceClient.CreatePersonAsync(
    // Id of the person group that the person belonged to
    personGroupId,    
    // Name of the person
    "Anna"            
);
 
// Define Bill and Clare in the same way
```
### <a name="step2-2"></a> <span data-ttu-id="491d9-149">2.2 Detect faces and register them to correct person</span><span class="sxs-lookup"><span data-stu-id="491d9-149">2.2 Detect faces and register them to correct person</span></span>
<span data-ttu-id="491d9-150">Detection is done by sending a "POST" web request to the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API with the image file in the HTTP request body.</span><span class="sxs-lookup"><span data-stu-id="491d9-150">Detection is done by sending a "POST" web request to the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API with the image file in the HTTP request body.</span></span> <span data-ttu-id="491d9-151">When using the client library, face detection is executed through the DetectAsync method for the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="491d9-151">When using the client library, face detection is executed through the DetectAsync method for the FaceServiceClient class.</span></span>

<span data-ttu-id="491d9-152">For each face detected you can call [Person – Add a Person Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) to add it to the correct person.</span><span class="sxs-lookup"><span data-stu-id="491d9-152">For each face detected you can call [Person – Add a Person Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) to add it to the correct person.</span></span>

<span data-ttu-id="491d9-153">The following code below demonstrates the process of how to detect a face from an image and add it to a person:</span><span class="sxs-lookup"><span data-stu-id="491d9-153">The following code below demonstrates the process of how to detect a face from an image and add it to a person:</span></span>
```CSharp 
// Directory contains image files of Anna
const string friend1ImageDir = @"D:\Pictures\MyFriends\Anna\";
 
foreach (string imagePath in Directory.GetFiles(friend1ImageDir, "*.jpg"))
{
    using (Stream s = File.OpenRead(imagePath))
    {
        // Detect faces in the image and add to Anna
        await faceServiceClient.AddPersonFaceAsync(
            personGroupId, friend1.PersonId, s);
    }
}
// Do the same for Bill and Clare
``` 
<span data-ttu-id="491d9-154">Notice that if the image contains more than one face, only the largest face will be added.</span><span class="sxs-lookup"><span data-stu-id="491d9-154">Notice that if the image contains more than one face, only the largest face will be added.</span></span> <span data-ttu-id="491d9-155">You can add other faces to the person by passing a string in the format of "targetFace = left, top, width, height" to [Person – Add a Person Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) API's targetFace query parameter, or using the targetFace optional parameter for the AddPersonFaceAsync method to add other faces.</span><span class="sxs-lookup"><span data-stu-id="491d9-155">You can add other faces to the person by passing a string in the format of "targetFace = left, top, width, height" to [Person – Add a Person Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) API's targetFace query parameter, or using the targetFace optional parameter for the AddPersonFaceAsync method to add other faces.</span></span> <span data-ttu-id="491d9-156">Each face added to the person will be given a unique persisted face ID, which can be used in [Person – Delete a Person Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523e) and [Face – Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).</span><span class="sxs-lookup"><span data-stu-id="491d9-156">Each face added to the person will be given a unique persisted face ID, which can be used in [Person – Delete a Person Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523e) and [Face – Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).</span></span>
## <a name="step3"></a> <span data-ttu-id="491d9-157">Step 3: Train the person group</span><span class="sxs-lookup"><span data-stu-id="491d9-157">Step 3: Train the person group</span></span>

<span data-ttu-id="491d9-158">The person group must be trained before an identification can be performed using it.</span><span class="sxs-lookup"><span data-stu-id="491d9-158">The person group must be trained before an identification can be performed using it.</span></span> <span data-ttu-id="491d9-159">Moreover, it has to be re-trained after adding or removing any person, or if any person has their registered face edited.</span><span class="sxs-lookup"><span data-stu-id="491d9-159">Moreover, it has to be re-trained after adding or removing any person, or if any person has their registered face edited.</span></span> <span data-ttu-id="491d9-160">The training is done by the [Person Group – Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249) API.</span><span class="sxs-lookup"><span data-stu-id="491d9-160">The training is done by the [Person Group – Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249) API.</span></span> <span data-ttu-id="491d9-161">When using the client library, it is simply a call to the TrainPersonGroupAsync method:</span><span class="sxs-lookup"><span data-stu-id="491d9-161">When using the client library, it is simply a call to the TrainPersonGroupAsync method:</span></span>
 
```CSharp 
await faceServiceClient.TrainPersonGroupAsync(personGroupId);
```
 
<span data-ttu-id="491d9-162">Please note that the training is an asynchronous process.</span><span class="sxs-lookup"><span data-stu-id="491d9-162">Please note that the training is an asynchronous process.</span></span> <span data-ttu-id="491d9-163">It may not be finished even after the the TrainPersonGroupAsync method returned.</span><span class="sxs-lookup"><span data-stu-id="491d9-163">It may not be finished even after the the TrainPersonGroupAsync method returned.</span></span> <span data-ttu-id="491d9-164">You may need to query the training status by [Person Group - Get Person Group Training Status](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395247) API or GetPersonGroupTrainingStatusAsync method of the client library.</span><span class="sxs-lookup"><span data-stu-id="491d9-164">You may need to query the training status by [Person Group - Get Person Group Training Status](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395247) API or GetPersonGroupTrainingStatusAsync method of the client library.</span></span> <span data-ttu-id="491d9-165">The following code demonstrates a simple logic of waiting person group training to finish:</span><span class="sxs-lookup"><span data-stu-id="491d9-165">The following code demonstrates a simple logic of waiting person group training to finish:</span></span>
 
```CSharp 
TrainingStatus trainingStatus = null;
while(true)
{
    trainingStatus = await faceServiceClient.GetPersonGroupTrainingStatusAsync(personGroupId);
 
    if (trainingStatus.Status != "running")
    {
        break;
    }
 
    await Task.Delay(1000);
} 
``` 

## <a name="step4"></a> <span data-ttu-id="491d9-166">Step 4: Identify a face against a defined person group</span><span class="sxs-lookup"><span data-stu-id="491d9-166">Step 4: Identify a face against a defined person group</span></span>
<span data-ttu-id="491d9-167">When performing identify, the Face API can compute the similarity of a test face among all the faces within a group, and returns the most comparable person(s) for that testing face.</span><span class="sxs-lookup"><span data-stu-id="491d9-167">When performing identify, the Face API can compute the similarity of a test face among all the faces within a group, and returns the most comparable person(s) for that testing face.</span></span> <span data-ttu-id="491d9-168">This is done through the [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) API or the IdentifyAsync method of the client library.</span><span class="sxs-lookup"><span data-stu-id="491d9-168">This is done through the [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) API or the IdentifyAsync method of the client library.</span></span>

<span data-ttu-id="491d9-169">The testing face needs to be detected using the previous steps listed above, and then the face ID is passed to the identify API as a second argument.</span><span class="sxs-lookup"><span data-stu-id="491d9-169">The testing face needs to be detected using the previous steps listed above, and then the face ID is passed to the identify API as a second argument.</span></span> <span data-ttu-id="491d9-170">Multiple face IDs can be identified at once, and the result will contain all the identify results.</span><span class="sxs-lookup"><span data-stu-id="491d9-170">Multiple face IDs can be identified at once, and the result will contain all the identify results.</span></span> <span data-ttu-id="491d9-171">By default, the identify returns only one person which matches the test face best.</span><span class="sxs-lookup"><span data-stu-id="491d9-171">By default, the identify returns only one person which matches the test face best.</span></span> <span data-ttu-id="491d9-172">If you prefer, you can specify the optional parameter maxNumOfCandidatesReturned to let the identify return more candidates.</span><span class="sxs-lookup"><span data-stu-id="491d9-172">If you prefer, you can specify the optional parameter maxNumOfCandidatesReturned to let the identify return more candidates.</span></span>

<span data-ttu-id="491d9-173">The following code below demonstrates the process of identify:</span><span class="sxs-lookup"><span data-stu-id="491d9-173">The following code below demonstrates the process of identify:</span></span>
```CSharp 
string testImageFile = @"D:\Pictures\test_img1.jpg";

using (Stream s = File.OpenRead(testImageFile))
{
    var faces = await faceServiceClient.DetectAsync(s);
    var faceIds = faces.Select(face => face.FaceId).ToArray();
 
    var results = await faceServiceClient.IdentifyAsync(personGroupId, faceIds);
    foreach (var identifyResult in results)
    {
        Console.WriteLine("Result of face: {0}", identifyResult.FaceId);
        if (identifyResult.Candidates.Length == 0)
        {
            Console.WriteLine("No one identified");
        }
        else
        {
            // Get top 1 among all candidates returned
            var candidateId = identifyResult.Candidates[0].PersonId;
            var person = await faceServiceClient.GetPersonAsync(personGroupId, candidateId);
            Console.WriteLine("Identified as {0}", person.Name);
        }
    }
}
``` 

<span data-ttu-id="491d9-174">When you have finished the steps, you can try to identify different faces and see if the faces of Anna, Bill or Clare can be correctly identified, according to the image(s) uploaded for face detection.</span><span class="sxs-lookup"><span data-stu-id="491d9-174">When you have finished the steps, you can try to identify different faces and see if the faces of Anna, Bill or Clare can be correctly identified, according to the image(s) uploaded for face detection.</span></span> <span data-ttu-id="491d9-175">See the examples below :</span><span class="sxs-lookup"><span data-stu-id="491d9-175">See the examples below :</span></span>

![HowToIdentify2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/identificationResult.1.jpg )

## <a name="summary"></a> <span data-ttu-id="491d9-177">Summary</span><span class="sxs-lookup"><span data-stu-id="491d9-177">Summary</span></span>

<span data-ttu-id="491d9-178">In this guide you have learned the process of creating a person group and identifying a person.</span><span class="sxs-lookup"><span data-stu-id="491d9-178">In this guide you have learned the process of creating a person group and identifying a person.</span></span> <span data-ttu-id="491d9-179">The following are a quick reminder of the features previously explained and demonstrated:</span><span class="sxs-lookup"><span data-stu-id="491d9-179">The following are a quick reminder of the features previously explained and demonstrated:</span></span>

- <span data-ttu-id="491d9-180">Detecting faces using the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d) API</span><span class="sxs-lookup"><span data-stu-id="491d9-180">Detecting faces using the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d) API</span></span>
- <span data-ttu-id="491d9-181">Creating person groups using the [Person Group - Create a Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) API</span><span class="sxs-lookup"><span data-stu-id="491d9-181">Creating person groups using the [Person Group - Create a Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) API</span></span>
- <span data-ttu-id="491d9-182">Creating persons using the [Person - Create a Person](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c) API</span><span class="sxs-lookup"><span data-stu-id="491d9-182">Creating persons using the [Person - Create a Person](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c) API</span></span>
- <span data-ttu-id="491d9-183">Train a person group using the [Person Group – Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249) API</span><span class="sxs-lookup"><span data-stu-id="491d9-183">Train a person group using the [Person Group – Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249) API</span></span>
- <span data-ttu-id="491d9-184">Identifying unknown faces against the person group using the [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) API</span><span class="sxs-lookup"><span data-stu-id="491d9-184">Identifying unknown faces against the person group using the [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) API</span></span>

## <a name="related"></a> <span data-ttu-id="491d9-185">Related Topics</span><span class="sxs-lookup"><span data-stu-id="491d9-185">Related Topics</span></span>

[<span data-ttu-id="491d9-186">How to Detect Faces in Image</span><span class="sxs-lookup"><span data-stu-id="491d9-186">How to Detect Faces in Image</span></span>](HowtoDetectFacesinImage.md)


