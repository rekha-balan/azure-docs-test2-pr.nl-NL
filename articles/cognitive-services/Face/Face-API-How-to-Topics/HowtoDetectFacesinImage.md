---
title: Detect faces in images with the Face API | Microsoft Docs
description: Use the Face API in Cognitive Services to detect faces in images.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 02/06/2017
ms.author: anroth
ms.openlocfilehash: f994a9207944997176e02d238bbb8430e58cdd93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661594"
---
# <a name="how-to-detect-faces-in-image"></a><span data-ttu-id="45b66-103">How to Detect Faces in Image</span><span class="sxs-lookup"><span data-stu-id="45b66-103">How to Detect Faces in Image</span></span>

<span data-ttu-id="45b66-104">This guide will demonstrate how to detect faces from an image, with face attributes like gender, age, or pose extracted.</span><span class="sxs-lookup"><span data-stu-id="45b66-104">This guide will demonstrate how to detect faces from an image, with face attributes like gender, age, or pose extracted.</span></span> <span data-ttu-id="45b66-105">The samples are written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="45b66-105">The samples are written in C# using the Face API client library.</span></span> 

## <a name="concepts"></a> <span data-ttu-id="45b66-106">Concepts</span><span class="sxs-lookup"><span data-stu-id="45b66-106">Concepts</span></span>

<span data-ttu-id="45b66-107">If you are not familiar with any of the following concepts in this guide, please refer to the definitions in our [Glossary](../Glossary.md) at any time:</span><span class="sxs-lookup"><span data-stu-id="45b66-107">If you are not familiar with any of the following concepts in this guide, please refer to the definitions in our [Glossary](../Glossary.md) at any time:</span></span> 

- <span data-ttu-id="45b66-108">Face detection</span><span class="sxs-lookup"><span data-stu-id="45b66-108">Face detection</span></span>
- <span data-ttu-id="45b66-109">Face landmarks</span><span class="sxs-lookup"><span data-stu-id="45b66-109">Face landmarks</span></span>
- <span data-ttu-id="45b66-110">Head pose</span><span class="sxs-lookup"><span data-stu-id="45b66-110">Head pose</span></span>
- <span data-ttu-id="45b66-111">Face attributes</span><span class="sxs-lookup"><span data-stu-id="45b66-111">Face attributes</span></span>

## <a name="preparation"></a> <span data-ttu-id="45b66-112">Preparation</span><span class="sxs-lookup"><span data-stu-id="45b66-112">Preparation</span></span>

<span data-ttu-id="45b66-113">In this sample, we will demonstrate the following features:</span><span class="sxs-lookup"><span data-stu-id="45b66-113">In this sample, we will demonstrate the following features:</span></span> 

- <span data-ttu-id="45b66-114">Detecting faces from an image, and marking them using rectangular framing</span><span class="sxs-lookup"><span data-stu-id="45b66-114">Detecting faces from an image, and marking them using rectangular framing</span></span>
- <span data-ttu-id="45b66-115">Analyzing the locations of pupils, the nose or mouth, and then marking them in the image</span><span class="sxs-lookup"><span data-stu-id="45b66-115">Analyzing the locations of pupils, the nose or mouth, and then marking them in the image</span></span>
- <span data-ttu-id="45b66-116">Analyzing the head pose, gender and age of the face</span><span class="sxs-lookup"><span data-stu-id="45b66-116">Analyzing the head pose, gender and age of the face</span></span>

<span data-ttu-id="45b66-117">In order to execute these features, you will need to prepare an image with at least one clear face.</span><span class="sxs-lookup"><span data-stu-id="45b66-117">In order to execute these features, you will need to prepare an image with at least one clear face.</span></span> 

## <a name="step1"></a> <span data-ttu-id="45b66-118">Step 1: Authorize the API call</span><span class="sxs-lookup"><span data-stu-id="45b66-118">Step 1: Authorize the API call</span></span>

<span data-ttu-id="45b66-119">Every call to the Face API requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="45b66-119">Every call to the Face API requires a subscription key.</span></span> <span data-ttu-id="45b66-120">This key needs to be either passed through a query string parameter, or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="45b66-120">This key needs to be either passed through a query string parameter, or specified in the request header.</span></span> <span data-ttu-id="45b66-121">To pass the subscription key through query string, please refer to the request URL for the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) as an example:</span><span class="sxs-lookup"><span data-stu-id="45b66-121">To pass the subscription key through query string, please refer to the request URL for the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) as an example:</span></span>

```
https://westus.api.cognitive.microsoft.com/face/v1.0/detect[?returnFaceId][&returnFaceLandmarks][&returnFaceAttributes]
&subscription-key=<Your subscription key>
```

<span data-ttu-id="45b66-122">As an alternative, the subscription key can also be specified in the HTTP request header: **ocp-apim-subscription-key: &lt;Your subscription key&gt;** When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="45b66-122">As an alternative, the subscription key can also be specified in the HTTP request header: **ocp-apim-subscription-key: &lt;Your subscription key&gt;** When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span></span> <span data-ttu-id="45b66-123">For example:</span><span class="sxs-lookup"><span data-stu-id="45b66-123">For example:</span></span>
```CSharp
faceServiceClient = new FaceServiceClient("Your subscription key");
```
<span data-ttu-id="45b66-124">See [subscription and key management](https://www.microsoft.com/cognitive-services/en-US/subscriptions).</span><span class="sxs-lookup"><span data-stu-id="45b66-124">See [subscription and key management](https://www.microsoft.com/cognitive-services/en-US/subscriptions).</span></span>

## <a name="step2"></a> <span data-ttu-id="45b66-125">Step 2: Upload an image to the service and execute face detection</span><span class="sxs-lookup"><span data-stu-id="45b66-125">Step 2: Upload an image to the service and execute face detection</span></span>

<span data-ttu-id="45b66-126">The most basic way to perform face detection is by uploading an image directly.</span><span class="sxs-lookup"><span data-stu-id="45b66-126">The most basic way to perform face detection is by uploading an image directly.</span></span> <span data-ttu-id="45b66-127">This is done by sending a "POST" request with application/octet-stream content type, with the data read from a JPEG image.</span><span class="sxs-lookup"><span data-stu-id="45b66-127">This is done by sending a "POST" request with application/octet-stream content type, with the data read from a JPEG image.</span></span> <span data-ttu-id="45b66-128">The maximum size of the image is 4MB.</span><span class="sxs-lookup"><span data-stu-id="45b66-128">The maximum size of the image is 4MB.</span></span>

<span data-ttu-id="45b66-129">Using the client library, face detection by means of uploading is done by passing in a Stream object.</span><span class="sxs-lookup"><span data-stu-id="45b66-129">Using the client library, face detection by means of uploading is done by passing in a Stream object.</span></span> <span data-ttu-id="45b66-130">See the example below:</span><span class="sxs-lookup"><span data-stu-id="45b66-130">See the example below:</span></span>
```CSharp
using (Stream s = File.OpenRead(@"D:\MyPictures\image1.jpg"))
{
    var faces = await faceServiceClient.DetectAsync(s, true, true);
 
    foreach (var face in faces)
    {
        var rect = face.FaceRectangle;
        var landmarks = face.FaceLandmarks;
    }
}
```

<span data-ttu-id="45b66-131">Please note that the DetectAsync method of FaceServiceClient is async.</span><span class="sxs-lookup"><span data-stu-id="45b66-131">Please note that the DetectAsync method of FaceServiceClient is async.</span></span> <span data-ttu-id="45b66-132">The calling method should be marked as async as well, in order to use the await clause.</span><span class="sxs-lookup"><span data-stu-id="45b66-132">The calling method should be marked as async as well, in order to use the await clause.</span></span>
<span data-ttu-id="45b66-133">If the image is already on the web and has an URL, face detection can be executed by also providing the URL.</span><span class="sxs-lookup"><span data-stu-id="45b66-133">If the image is already on the web and has an URL, face detection can be executed by also providing the URL.</span></span> <span data-ttu-id="45b66-134">In this example, the request body will be a JSON string which contains the URL.</span><span class="sxs-lookup"><span data-stu-id="45b66-134">In this example, the request body will be a JSON string which contains the URL.</span></span>
<span data-ttu-id="45b66-135">Using the client library, face detection by means of a URL can be executed easily using another overload of the DetectAsync method.</span><span class="sxs-lookup"><span data-stu-id="45b66-135">Using the client library, face detection by means of a URL can be executed easily using another overload of the DetectAsync method.</span></span>
```CSharp
string imageUrl = "http://news.microsoft.com/ceo/assets/photos/06_web.jpg";
var faces = await faceServiceClient.DetectAsync(imageUrl, true, true);
 
foreach (var face in faces)
{
    var rect = face.FaceRectangle;
    var landmarks = face.FaceLandmarks;
}
``` 

<span data-ttu-id="45b66-136">The FaceRectangle property that is returned with detected faces is essentially locations on the face in pixels.</span><span class="sxs-lookup"><span data-stu-id="45b66-136">The FaceRectangle property that is returned with detected faces is essentially locations on the face in pixels.</span></span> <span data-ttu-id="45b66-137">Usually, this rectangle contains the eyes, eyebrows, the nose and the mouth –the top of head, ears and the chin are not included.</span><span class="sxs-lookup"><span data-stu-id="45b66-137">Usually, this rectangle contains the eyes, eyebrows, the nose and the mouth –the top of head, ears and the chin are not included.</span></span> <span data-ttu-id="45b66-138">If you crop a complete head or mid-shot portrait (a photo ID type image), you may want to expand the area of the rectangular face frame because the area of the face may be too small for some applications.</span><span class="sxs-lookup"><span data-stu-id="45b66-138">If you crop a complete head or mid-shot portrait (a photo ID type image), you may want to expand the area of the rectangular face frame because the area of the face may be too small for some applications.</span></span> <span data-ttu-id="45b66-139">To locate a face more precisely, using face landmarks (locate face features or face direction mechanisms) described in the next section will prove to be very useful.</span><span class="sxs-lookup"><span data-stu-id="45b66-139">To locate a face more precisely, using face landmarks (locate face features or face direction mechanisms) described in the next section will prove to be very useful.</span></span>

## <a name="step3"></a> <span data-ttu-id="45b66-140">Step 3: Understanding and using face landmarks</span><span class="sxs-lookup"><span data-stu-id="45b66-140">Step 3: Understanding and using face landmarks</span></span>

<span data-ttu-id="45b66-141">Face landmarks are a series of specifically detailed points on a face; typically points of face components like the pupils, canthus or nose.</span><span class="sxs-lookup"><span data-stu-id="45b66-141">Face landmarks are a series of specifically detailed points on a face; typically points of face components like the pupils, canthus or nose.</span></span> <span data-ttu-id="45b66-142">Face landmarks are optional attributes that can be analyzed during face detection.</span><span class="sxs-lookup"><span data-stu-id="45b66-142">Face landmarks are optional attributes that can be analyzed during face detection.</span></span> <span data-ttu-id="45b66-143">You can either pass 'true' as a Boolean value to the returnFaceLandmarks query parameter when calling the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), or use the returnFaceLandmarks optional parameter for the FaceServiceClient class DetectAsync method in order to include the face landmarks in the detection results.</span><span class="sxs-lookup"><span data-stu-id="45b66-143">You can either pass 'true' as a Boolean value to the returnFaceLandmarks query parameter when calling the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), or use the returnFaceLandmarks optional parameter for the FaceServiceClient class DetectAsync method in order to include the face landmarks in the detection results.</span></span>

<span data-ttu-id="45b66-144">By default, there are 27 predefined landmark points.</span><span class="sxs-lookup"><span data-stu-id="45b66-144">By default, there are 27 predefined landmark points.</span></span> <span data-ttu-id="45b66-145">The following figure shows how all 27 points are defined:</span><span class="sxs-lookup"><span data-stu-id="45b66-145">The following figure shows how all 27 points are defined:</span></span>

![HowToDetectFace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/landmarks.1.jpg)

<span data-ttu-id="45b66-147">The points returned are in units of pixels, just like the face rectangular frame.</span><span class="sxs-lookup"><span data-stu-id="45b66-147">The points returned are in units of pixels, just like the face rectangular frame.</span></span> <span data-ttu-id="45b66-148">Therefore making it easier to mark specific points of interest in the image.</span><span class="sxs-lookup"><span data-stu-id="45b66-148">Therefore making it easier to mark specific points of interest in the image.</span></span> <span data-ttu-id="45b66-149">The following code demonstrates retrieving the locations of the nose and pupils:</span><span class="sxs-lookup"><span data-stu-id="45b66-149">The following code demonstrates retrieving the locations of the nose and pupils:</span></span>
```CSharp
var faces = await faceServiceClient.DetectAsync(imageUrl, returnFaceLandmarks:true);
 
foreach (var face in faces)
{
    var rect = face.FaceRectangle;
    var landmarks = face.FaceLandmarks;
 
    double noseX = landmarks.NoseTip.X;
    double noseY = landmarks.NoseTip.Y;
 
    double leftPupilX = landmarks.PupilLeft.X;
    double leftPupilY = landmarks.PupilLeft.Y;
 
    double rightPupilX = landmarks.PupilRight.X;
    double rightPupilY = landmarks.PupilRight.Y;
}
``` 

<span data-ttu-id="45b66-150">In addition to marking face features in an image, face landmarks can also be used to accurately calculate the direction of the face.</span><span class="sxs-lookup"><span data-stu-id="45b66-150">In addition to marking face features in an image, face landmarks can also be used to accurately calculate the direction of the face.</span></span> <span data-ttu-id="45b66-151">For example, we can define the direction of the face as a vector from the center of the mouth to the center of the eyes.</span><span class="sxs-lookup"><span data-stu-id="45b66-151">For example, we can define the direction of the face as a vector from the center of the mouth to the center of the eyes.</span></span> <span data-ttu-id="45b66-152">The code below explains this in detail:</span><span class="sxs-lookup"><span data-stu-id="45b66-152">The code below explains this in detail:</span></span>

```CSharp
var landmarks = face.FaceLandmarks;
 
var upperLipBottom = landmarks.UpperLipBottom;
var underLipTop = landmarks.UnderLipTop;
 
var centerOfMouth = new Point(
    (upperLipBottom.X + underLipTop.X) / 2,
    (upperLipBottom.Y + underLipTop.Y) / 2);
 
var eyeLeftInner = landmarks.EyeLeftInner;
var eyeRightInner = landmarks.EyeRightInner;
 
var centerOfTwoEyes = new Point(
    (eyeLeftInner.X + eyeRightInner.X) / 2,
    (eyeLeftInner.Y + eyeRightInner.Y) / 2);
 
Vector faceDirection = new Vector(
    centerOfTwoEyes.X - centerOfMouth.X,
    centerOfTwoEyes.Y - centerOfMouth.Y);
``` 

<span data-ttu-id="45b66-153">By knowing the direction that the face is in, you can then rotate the rectangular face frame to align it with the face.</span><span class="sxs-lookup"><span data-stu-id="45b66-153">By knowing the direction that the face is in, you can then rotate the rectangular face frame to align it with the face.</span></span> <span data-ttu-id="45b66-154">It is clear that using face landmarks can provide more detail and utility.</span><span class="sxs-lookup"><span data-stu-id="45b66-154">It is clear that using face landmarks can provide more detail and utility.</span></span>

## <a name="step4"></a> <span data-ttu-id="45b66-155">Step 4: Using other face attributes</span><span class="sxs-lookup"><span data-stu-id="45b66-155">Step 4: Using other face attributes</span></span>

<span data-ttu-id="45b66-156">Besides face landmarks, Face – Detect API can also analyze several other attributes on a face.</span><span class="sxs-lookup"><span data-stu-id="45b66-156">Besides face landmarks, Face – Detect API can also analyze several other attributes on a face.</span></span> <span data-ttu-id="45b66-157">These attributes include:</span><span class="sxs-lookup"><span data-stu-id="45b66-157">These attributes include:</span></span>

- <span data-ttu-id="45b66-158">Age</span><span class="sxs-lookup"><span data-stu-id="45b66-158">Age</span></span>
- <span data-ttu-id="45b66-159">Gender</span><span class="sxs-lookup"><span data-stu-id="45b66-159">Gender</span></span>
- <span data-ttu-id="45b66-160">Smile intensity</span><span class="sxs-lookup"><span data-stu-id="45b66-160">Smile intensity</span></span>
- <span data-ttu-id="45b66-161">Facial hair</span><span class="sxs-lookup"><span data-stu-id="45b66-161">Facial hair</span></span>
- <span data-ttu-id="45b66-162">A 3D head pose</span><span class="sxs-lookup"><span data-stu-id="45b66-162">A 3D head pose</span></span>

<span data-ttu-id="45b66-163">These attributes are predicted by using statistical algorithms and may not always be 100% precise.</span><span class="sxs-lookup"><span data-stu-id="45b66-163">These attributes are predicted by using statistical algorithms and may not always be 100% precise.</span></span> <span data-ttu-id="45b66-164">However, they are still helpful when you want to classify faces by these attributes.</span><span class="sxs-lookup"><span data-stu-id="45b66-164">However, they are still helpful when you want to classify faces by these attributes.</span></span> <span data-ttu-id="45b66-165">For more information about each of the attributes, please refer to the [Glossary](../Glossary.md).</span><span class="sxs-lookup"><span data-stu-id="45b66-165">For more information about each of the attributes, please refer to the [Glossary](../Glossary.md).</span></span>

<span data-ttu-id="45b66-166">Below is a simple example of extracting face attributes during face detection:</span><span class="sxs-lookup"><span data-stu-id="45b66-166">Below is a simple example of extracting face attributes during face detection:</span></span>
```CSharp
var requiredFaceAttributes = new FaceAttributeType[] {
                FaceAttributeType.Age,
                FaceAttributeType.Gender,
                FaceAttributeType.Smile,
                FaceAttributeType.FacialHair,
                FaceAttributeType.HeadPose,
                FaceAttributeType.Glasses
            };
var faces = await faceServiceClient.DetectAsync(imageUrl,
    returnFaceLandmarks: true,
    returnFaceAttributes: requiredFaceAttributes);

foreach (var face in faces)
{
    var id = face.FaceId;
    var attributes = face.FaceAttributes;
    var age = attributes.Age;
    var gender = attributes.Gender;
    var smile = attributes.Smile;
    var facialHair = attributes.FacialHair;
    var headPose = attributes.HeadPose;
    var glasses = attributes.Glasses;
}
``` 
## <a name="summary"></a> <span data-ttu-id="45b66-167">Summary</span><span class="sxs-lookup"><span data-stu-id="45b66-167">Summary</span></span>

<span data-ttu-id="45b66-168">In this guide you have learned the functionalities of [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API, how it can detect faces for local uploaded images or image URLs on the web; how it can detect faces by returning rectangular face frames; and how it can also analyze face landmarks, 3D head poses and other face attributes as well.</span><span class="sxs-lookup"><span data-stu-id="45b66-168">In this guide you have learned the functionalities of [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API, how it can detect faces for local uploaded images or image URLs on the web; how it can detect faces by returning rectangular face frames; and how it can also analyze face landmarks, 3D head poses and other face attributes as well.</span></span>

<span data-ttu-id="45b66-169">For more information about API details, please refer to the API reference guide for [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="45b66-169">For more information about API details, please refer to the API reference guide for [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

## <a name="related"></a> <span data-ttu-id="45b66-170">Related Topics</span><span class="sxs-lookup"><span data-stu-id="45b66-170">Related Topics</span></span>

[<span data-ttu-id="45b66-171">How to Identify Faces in Image</span><span class="sxs-lookup"><span data-stu-id="45b66-171">How to Identify Faces in Image</span></span>](HowtoIdentifyFacesinImage.md)

