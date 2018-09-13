---
title: Detect faces in images with the Face API | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Use the Face API in Cognitive Services to detect faces in images.
services: cognitive-services
author: SteveMSFT
manager: corncar
ms.service: cognitive-services
ms.component: face-api
ms.topic: article
ms.date: 03/01/2018
ms.author: sbowles
ms.openlocfilehash: 57cd0915450428399fd680638aa4fae2cdbe17c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793460"
---
# <a name="how-to-detect-faces-in-image"></a><span data-ttu-id="02800-103">How to Detect Faces in Image</span><span class="sxs-lookup"><span data-stu-id="02800-103">How to Detect Faces in Image</span></span>

<span data-ttu-id="02800-104">This guide will demonstrate how to detect faces from an image, with face attributes like gender, age, or pose extracted.</span><span class="sxs-lookup"><span data-stu-id="02800-104">This guide will demonstrate how to detect faces from an image, with face attributes like gender, age, or pose extracted.</span></span> <span data-ttu-id="02800-105">The samples are written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="02800-105">The samples are written in C# using the Face API client library.</span></span> 

## <a name="concepts"></a> <span data-ttu-id="02800-106">Concepts</span><span class="sxs-lookup"><span data-stu-id="02800-106">Concepts</span></span>

<span data-ttu-id="02800-107">If you are not familiar with any of the following concepts in this guide, please refer to the definitions in our [Glossary](../Glossary.md) at any time:</span><span class="sxs-lookup"><span data-stu-id="02800-107">If you are not familiar with any of the following concepts in this guide, please refer to the definitions in our [Glossary](../Glossary.md) at any time:</span></span> 

- <span data-ttu-id="02800-108">Face detection</span><span class="sxs-lookup"><span data-stu-id="02800-108">Face detection</span></span>
- <span data-ttu-id="02800-109">Face landmarks</span><span class="sxs-lookup"><span data-stu-id="02800-109">Face landmarks</span></span>
- <span data-ttu-id="02800-110">Head pose</span><span class="sxs-lookup"><span data-stu-id="02800-110">Head pose</span></span>
- <span data-ttu-id="02800-111">Face attributes</span><span class="sxs-lookup"><span data-stu-id="02800-111">Face attributes</span></span>

## <a name="preparation"></a> <span data-ttu-id="02800-112">Preparation</span><span class="sxs-lookup"><span data-stu-id="02800-112">Preparation</span></span>

<span data-ttu-id="02800-113">In this sample, we will demonstrate the following features:</span><span class="sxs-lookup"><span data-stu-id="02800-113">In this sample, we will demonstrate the following features:</span></span> 

- <span data-ttu-id="02800-114">Detecting faces from an image, and marking them using rectangular framing</span><span class="sxs-lookup"><span data-stu-id="02800-114">Detecting faces from an image, and marking them using rectangular framing</span></span>
- <span data-ttu-id="02800-115">Analyzing the locations of pupils, the nose or mouth, and then marking them in the image</span><span class="sxs-lookup"><span data-stu-id="02800-115">Analyzing the locations of pupils, the nose or mouth, and then marking them in the image</span></span>
- <span data-ttu-id="02800-116">Analyzing the head pose, gender and age of the face</span><span class="sxs-lookup"><span data-stu-id="02800-116">Analyzing the head pose, gender and age of the face</span></span>

<span data-ttu-id="02800-117">In order to execute these features, you will need to prepare an image with at least one clear face.</span><span class="sxs-lookup"><span data-stu-id="02800-117">In order to execute these features, you will need to prepare an image with at least one clear face.</span></span> 

## <a name="step1"></a> <span data-ttu-id="02800-118">Step 1: Authorize the API call</span><span class="sxs-lookup"><span data-stu-id="02800-118">Step 1: Authorize the API call</span></span>

<span data-ttu-id="02800-119">Every call to the Face API requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="02800-119">Every call to the Face API requires a subscription key.</span></span> <span data-ttu-id="02800-120">This key needs to be either passed through a query string parameter, or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="02800-120">This key needs to be either passed through a query string parameter, or specified in the request header.</span></span> <span data-ttu-id="02800-121">To pass the subscription key through query string, please refer to the request URL for the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) as an example:</span><span class="sxs-lookup"><span data-stu-id="02800-121">To pass the subscription key through query string, please refer to the request URL for the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) as an example:</span></span>

```
https://westus.api.cognitive.microsoft.com/face/v1.0/detect[?returnFaceId][&returnFaceLandmarks][&returnFaceAttributes]
&subscription-key=<Subscription Key>
```

<span data-ttu-id="02800-122">As an alternative, the subscription key can also be specified in the HTTP request header: **ocp-apim-subscription-key: &lt;Subscription Key&gt;** When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="02800-122">As an alternative, the subscription key can also be specified in the HTTP request header: **ocp-apim-subscription-key: &lt;Subscription Key&gt;** When using a client library, the subscription key is passed in through the constructor of the FaceServiceClient class.</span></span> <span data-ttu-id="02800-123">For example:</span><span class="sxs-lookup"><span data-stu-id="02800-123">For example:</span></span>
```CSharp
faceServiceClient = new FaceServiceClient("<Subscription Key>");
```

## <a name="step2"></a> <span data-ttu-id="02800-124">Step 2: Upload an image to the service and execute face detection</span><span class="sxs-lookup"><span data-stu-id="02800-124">Step 2: Upload an image to the service and execute face detection</span></span>

<span data-ttu-id="02800-125">The most basic way to perform face detection is by uploading an image directly.</span><span class="sxs-lookup"><span data-stu-id="02800-125">The most basic way to perform face detection is by uploading an image directly.</span></span> <span data-ttu-id="02800-126">This is done by sending a "POST" request with application/octet-stream content type, with the data read from a JPEG image.</span><span class="sxs-lookup"><span data-stu-id="02800-126">This is done by sending a "POST" request with application/octet-stream content type, with the data read from a JPEG image.</span></span> <span data-ttu-id="02800-127">The maximum size of the image is 4 MB.</span><span class="sxs-lookup"><span data-stu-id="02800-127">The maximum size of the image is 4 MB.</span></span>

<span data-ttu-id="02800-128">Using the client library, face detection by means of uploading is done by passing in a Stream object.</span><span class="sxs-lookup"><span data-stu-id="02800-128">Using the client library, face detection by means of uploading is done by passing in a Stream object.</span></span> <span data-ttu-id="02800-129">See the example below:</span><span class="sxs-lookup"><span data-stu-id="02800-129">See the example below:</span></span>
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

<span data-ttu-id="02800-130">Note that the DetectAsync method of FaceServiceClient is async.</span><span class="sxs-lookup"><span data-stu-id="02800-130">Note that the DetectAsync method of FaceServiceClient is async.</span></span> <span data-ttu-id="02800-131">The calling method should be marked as async as well, in order to use the await clause.</span><span class="sxs-lookup"><span data-stu-id="02800-131">The calling method should be marked as async as well, in order to use the await clause.</span></span>
<span data-ttu-id="02800-132">If the image is already on the web and has a URL, face detection can be executed by also providing the URL.</span><span class="sxs-lookup"><span data-stu-id="02800-132">If the image is already on the web and has a URL, face detection can be executed by also providing the URL.</span></span> <span data-ttu-id="02800-133">In this example, the request body will be a JSON string, which contains the URL.</span><span class="sxs-lookup"><span data-stu-id="02800-133">In this example, the request body will be a JSON string, which contains the URL.</span></span>
<span data-ttu-id="02800-134">Using the client library, face detection by means of a URL can be executed easily using another overload of the DetectAsync method.</span><span class="sxs-lookup"><span data-stu-id="02800-134">Using the client library, face detection by means of a URL can be executed easily using another overload of the DetectAsync method.</span></span>
```CSharp
string imageUrl = "http://news.microsoft.com/ceo/assets/photos/06_web.jpg";
var faces = await faceServiceClient.DetectAsync(imageUrl, true, true);
 
foreach (var face in faces)
{
    var rect = face.FaceRectangle;
    var landmarks = face.FaceLandmarks;
}
``` 

<span data-ttu-id="02800-135">The FaceRectangle property that is returned with detected faces is essentially locations on the face in pixels.</span><span class="sxs-lookup"><span data-stu-id="02800-135">The FaceRectangle property that is returned with detected faces is essentially locations on the face in pixels.</span></span> <span data-ttu-id="02800-136">Usually, this rectangle contains the eyes, eyebrows, the nose, and the mouth –the top of head, ears, and the chin are not included.</span><span class="sxs-lookup"><span data-stu-id="02800-136">Usually, this rectangle contains the eyes, eyebrows, the nose, and the mouth –the top of head, ears, and the chin are not included.</span></span> <span data-ttu-id="02800-137">If you crop a complete head or mid-shot portrait (a photo ID type image), you may want to expand the area of the rectangular face frame because the area of the face may be too small for some applications.</span><span class="sxs-lookup"><span data-stu-id="02800-137">If you crop a complete head or mid-shot portrait (a photo ID type image), you may want to expand the area of the rectangular face frame because the area of the face may be too small for some applications.</span></span> <span data-ttu-id="02800-138">To locate a face more precisely, using face landmarks (locate face features or face direction mechanisms) described in the next section will prove to be useful.</span><span class="sxs-lookup"><span data-stu-id="02800-138">To locate a face more precisely, using face landmarks (locate face features or face direction mechanisms) described in the next section will prove to be useful.</span></span>

## <a name="step3"></a> <span data-ttu-id="02800-139">Step 3: Understanding and using face landmarks</span><span class="sxs-lookup"><span data-stu-id="02800-139">Step 3: Understanding and using face landmarks</span></span>

<span data-ttu-id="02800-140">Face landmarks are a series of detailed points on a face; typically points of face components like the pupils, canthus, or nose.</span><span class="sxs-lookup"><span data-stu-id="02800-140">Face landmarks are a series of detailed points on a face; typically points of face components like the pupils, canthus, or nose.</span></span> <span data-ttu-id="02800-141">Face landmarks are optional attributes that can be analyzed during face detection.</span><span class="sxs-lookup"><span data-stu-id="02800-141">Face landmarks are optional attributes that can be analyzed during face detection.</span></span> <span data-ttu-id="02800-142">You can either pass 'true' as a Boolean value to the returnFaceLandmarks query parameter when calling the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), or use the returnFaceLandmarks optional parameter for the FaceServiceClient class DetectAsync method in order to include the face landmarks in the detection results.</span><span class="sxs-lookup"><span data-stu-id="02800-142">You can either pass 'true' as a Boolean value to the returnFaceLandmarks query parameter when calling the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), or use the returnFaceLandmarks optional parameter for the FaceServiceClient class DetectAsync method in order to include the face landmarks in the detection results.</span></span>

<span data-ttu-id="02800-143">By default, there are 27 predefined landmark points.</span><span class="sxs-lookup"><span data-stu-id="02800-143">By default, there are 27 predefined landmark points.</span></span> <span data-ttu-id="02800-144">The following figure shows how all 27 points are defined:</span><span class="sxs-lookup"><span data-stu-id="02800-144">The following figure shows how all 27 points are defined:</span></span>

![HowToDetectFace](../Images/landmarks.1.jpg)

<span data-ttu-id="02800-146">The points returned are in units of pixels, just like the face rectangular frame.</span><span class="sxs-lookup"><span data-stu-id="02800-146">The points returned are in units of pixels, just like the face rectangular frame.</span></span> <span data-ttu-id="02800-147">Therefore making it easier to mark specific points of interest in the image.</span><span class="sxs-lookup"><span data-stu-id="02800-147">Therefore making it easier to mark specific points of interest in the image.</span></span> <span data-ttu-id="02800-148">The following code demonstrates retrieving the locations of the nose and pupils:</span><span class="sxs-lookup"><span data-stu-id="02800-148">The following code demonstrates retrieving the locations of the nose and pupils:</span></span>
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

<span data-ttu-id="02800-149">In addition to marking face features in an image, face landmarks can also be used to accurately calculate the direction of the face.</span><span class="sxs-lookup"><span data-stu-id="02800-149">In addition to marking face features in an image, face landmarks can also be used to accurately calculate the direction of the face.</span></span> <span data-ttu-id="02800-150">For example, we can define the direction of the face as a vector from the center of the mouth to the center of the eyes.</span><span class="sxs-lookup"><span data-stu-id="02800-150">For example, we can define the direction of the face as a vector from the center of the mouth to the center of the eyes.</span></span> <span data-ttu-id="02800-151">The code below explains this in detail:</span><span class="sxs-lookup"><span data-stu-id="02800-151">The code below explains this in detail:</span></span>

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

<span data-ttu-id="02800-152">By knowing the direction that the face is in, you can then rotate the rectangular face frame to align it with the face.</span><span class="sxs-lookup"><span data-stu-id="02800-152">By knowing the direction that the face is in, you can then rotate the rectangular face frame to align it with the face.</span></span> <span data-ttu-id="02800-153">It is clear that using face landmarks can provide more detail and utility.</span><span class="sxs-lookup"><span data-stu-id="02800-153">It is clear that using face landmarks can provide more detail and utility.</span></span>

## <a name="step4"></a> <span data-ttu-id="02800-154">Step 4: Using other face attributes</span><span class="sxs-lookup"><span data-stu-id="02800-154">Step 4: Using other face attributes</span></span>

<span data-ttu-id="02800-155">Besides face landmarks, Face – Detect API can also analyze several other attributes on a face.</span><span class="sxs-lookup"><span data-stu-id="02800-155">Besides face landmarks, Face – Detect API can also analyze several other attributes on a face.</span></span> <span data-ttu-id="02800-156">These attributes include:</span><span class="sxs-lookup"><span data-stu-id="02800-156">These attributes include:</span></span>

- <span data-ttu-id="02800-157">Age</span><span class="sxs-lookup"><span data-stu-id="02800-157">Age</span></span>
- <span data-ttu-id="02800-158">Gender</span><span class="sxs-lookup"><span data-stu-id="02800-158">Gender</span></span>
- <span data-ttu-id="02800-159">Smile intensity</span><span class="sxs-lookup"><span data-stu-id="02800-159">Smile intensity</span></span>
- <span data-ttu-id="02800-160">Facial hair</span><span class="sxs-lookup"><span data-stu-id="02800-160">Facial hair</span></span>
- <span data-ttu-id="02800-161">A 3D head pose</span><span class="sxs-lookup"><span data-stu-id="02800-161">A 3D head pose</span></span>

<span data-ttu-id="02800-162">These attributes are predicted by using statistical algorithms and may not always be 100% precise.</span><span class="sxs-lookup"><span data-stu-id="02800-162">These attributes are predicted by using statistical algorithms and may not always be 100% precise.</span></span> <span data-ttu-id="02800-163">However, they are still helpful when you want to classify faces by these attributes.</span><span class="sxs-lookup"><span data-stu-id="02800-163">However, they are still helpful when you want to classify faces by these attributes.</span></span> <span data-ttu-id="02800-164">For more information about each of the attributes, please refer to the [Glossary](../Glossary.md).</span><span class="sxs-lookup"><span data-stu-id="02800-164">For more information about each of the attributes, please refer to the [Glossary](../Glossary.md).</span></span>

<span data-ttu-id="02800-165">Below is a simple example of extracting face attributes during face detection:</span><span class="sxs-lookup"><span data-stu-id="02800-165">Below is a simple example of extracting face attributes during face detection:</span></span>
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
## <a name="summary"></a> <span data-ttu-id="02800-166">Summary</span><span class="sxs-lookup"><span data-stu-id="02800-166">Summary</span></span>

<span data-ttu-id="02800-167">In this guide you have learned the functionalities of [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API, how it can detect faces for local uploaded images or image URLs on the web; how it can detect faces by returning rectangular face frames; and how it can also analyze face landmarks, 3D head poses and other face attributes as well.</span><span class="sxs-lookup"><span data-stu-id="02800-167">In this guide you have learned the functionalities of [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API, how it can detect faces for local uploaded images or image URLs on the web; how it can detect faces by returning rectangular face frames; and how it can also analyze face landmarks, 3D head poses and other face attributes as well.</span></span>

<span data-ttu-id="02800-168">For more information about API details, please refer to the API reference guide for [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="02800-168">For more information about API details, please refer to the API reference guide for [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

## <a name="related"></a> <span data-ttu-id="02800-169">Related Topics</span><span class="sxs-lookup"><span data-stu-id="02800-169">Related Topics</span></span>

[<span data-ttu-id="02800-170">How to Identify Faces in Image</span><span class="sxs-lookup"><span data-stu-id="02800-170">How to Identify Faces in Image</span></span>](HowtoIdentifyFacesinImage.md)
