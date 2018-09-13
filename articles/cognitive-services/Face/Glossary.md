---
title: Glossary for the Face API Service | Microsoft Docs
description: The glossary explains terms that you might encounter as you work with the Face API Service.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 01/18/2017
ms.author: anroth
ms.openlocfilehash: 374887ec4db4ed59b7636087eeef6c9d4ed2c4f5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555052"
---
# <a name="glossary"></a><span data-ttu-id="82a8b-103">Glossary</span><span class="sxs-lookup"><span data-stu-id="82a8b-103">Glossary</span></span>

## <a name="a"></a><span data-ttu-id="82a8b-104">A</span><span class="sxs-lookup"><span data-stu-id="82a8b-104">A</span></span>

#### <a name="Attributes"></a><span data-ttu-id="82a8b-105">Attributes</span><span class="sxs-lookup"><span data-stu-id="82a8b-105">Attributes</span></span>

<span data-ttu-id="82a8b-106">Attributes are optional in the [detection](#Detection-Face-Detection) results, such as [age](#Age-Attribute), [gender](#Gender-Attribute), [head pose](#Head-Pose-Attribute), [facial hair](#Facial-Hair-Attribute), [smiling](#Smile-Attribute).</span><span class="sxs-lookup"><span data-stu-id="82a8b-106">Attributes are optional in the [detection](#Detection-Face-Detection) results, such as [age](#Age-Attribute), [gender](#Gender-Attribute), [head pose](#Head-Pose-Attribute), [facial hair](#Facial-Hair-Attribute), [smiling](#Smile-Attribute).</span></span>
<span data-ttu-id="82a8b-107">They can be obtained from the [detection](#Detection-Face-Detection) API by specifying the query parameters: returnFaceAttributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-107">They can be obtained from the [detection](#Detection-Face-Detection) API by specifying the query parameters: returnFaceAttributes.</span></span> <span data-ttu-id="82a8b-108">Attributes give extra information regarding selected [faces](#Face); in addition to the [face ID](#Face-ID) and the [rectangle](#Face-Rectangle).</span><span class="sxs-lookup"><span data-stu-id="82a8b-108">Attributes give extra information regarding selected [faces](#Face); in addition to the [face ID](#Face-ID) and the [rectangle](#Face-Rectangle).</span></span>

<span data-ttu-id="82a8b-109">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-109">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="Age-Attribute"></a><span data-ttu-id="82a8b-110">Age (Attribute)</span><span class="sxs-lookup"><span data-stu-id="82a8b-110">Age (Attribute)</span></span>

<span data-ttu-id="82a8b-111">Age is one of the [attributes](#Attributes) that describes the age of a particular face.</span><span class="sxs-lookup"><span data-stu-id="82a8b-111">Age is one of the [attributes](#Attributes) that describes the age of a particular face.</span></span> <span data-ttu-id="82a8b-112">The age attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by specifying the returnFaceAttributes parameter.</span><span class="sxs-lookup"><span data-stu-id="82a8b-112">The age attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by specifying the returnFaceAttributes parameter.</span></span>

<span data-ttu-id="82a8b-113">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-113">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

## <a name="b"></a><span data-ttu-id="82a8b-114">B</span><span class="sxs-lookup"><span data-stu-id="82a8b-114">B</span></span>

## <a name="c"></a><span data-ttu-id="82a8b-115">C</span><span class="sxs-lookup"><span data-stu-id="82a8b-115">C</span></span>

#### <a name="Candidate"></a><span data-ttu-id="82a8b-116">Candidate</span><span class="sxs-lookup"><span data-stu-id="82a8b-116">Candidate</span></span>

<span data-ttu-id="82a8b-117">Candidates are essentially [identification](#Identification) results (e.g. identified persons and level of confidence in detections).</span><span class="sxs-lookup"><span data-stu-id="82a8b-117">Candidates are essentially [identification](#Identification) results (e.g. identified persons and level of confidence in detections).</span></span> <span data-ttu-id="82a8b-118">A candidate is represented by the [personID](#Person-ID) and [confidence](#Confidence), indicating that the person is identified with a high level of confidence.</span><span class="sxs-lookup"><span data-stu-id="82a8b-118">A candidate is represented by the [personID](#Person-ID) and [confidence](#Confidence), indicating that the person is identified with a high level of confidence.</span></span>

<span data-ttu-id="82a8b-119">For more details, please refer to the guide [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).</span><span class="sxs-lookup"><span data-stu-id="82a8b-119">For more details, please refer to the guide [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).</span></span>

#### <a name="Confidence"></a><span data-ttu-id="82a8b-120">Confidence</span><span class="sxs-lookup"><span data-stu-id="82a8b-120">Confidence</span></span>

<span data-ttu-id="82a8b-121">Confidence is a measurement revealing the similarity between [faces](#Face) or [people](#Person) in numerical values –which is used in [identification](#Identification), and [verification](#Verification) to indicate the similarities of searched, identified and verified results.</span><span class="sxs-lookup"><span data-stu-id="82a8b-121">Confidence is a measurement revealing the similarity between [faces](#Face) or [people](#Person) in numerical values –which is used in [identification](#Identification), and [verification](#Verification) to indicate the similarities of searched, identified and verified results.</span></span>

<span data-ttu-id="82a8b-122">For more details, please refer to the following guides: [Face - Find Similar](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a)</span><span class="sxs-lookup"><span data-stu-id="82a8b-122">For more details, please refer to the following guides: [Face - Find Similar](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a)</span></span>

## <a name="d"></a><span data-ttu-id="82a8b-123">D</span><span class="sxs-lookup"><span data-stu-id="82a8b-123">D</span></span>

#### <a name="Detection-Face-Detection"></a><span data-ttu-id="82a8b-124">Detection/Face Detection</span><span class="sxs-lookup"><span data-stu-id="82a8b-124">Detection/Face Detection</span></span>

<span data-ttu-id="82a8b-125">Face detection is the action of locating faces in images.</span><span class="sxs-lookup"><span data-stu-id="82a8b-125">Face detection is the action of locating faces in images.</span></span> <span data-ttu-id="82a8b-126">Users can upload an image or specify an image URL in the request.</span><span class="sxs-lookup"><span data-stu-id="82a8b-126">Users can upload an image or specify an image URL in the request.</span></span> <span data-ttu-id="82a8b-127">The detected faces are returned with [face IDs](#Face-ID)   indicating a unique identity in Face API.</span><span class="sxs-lookup"><span data-stu-id="82a8b-127">The detected faces are returned with [face IDs](#Face-ID)   indicating a unique identity in Face API.</span></span> <span data-ttu-id="82a8b-128">The rectangles indicate the face locations in the image in pixels, as well as the optional [attributes](#Attributes) for each face such as [age](#Age-Attribute), [gender](#Gender-Attribute), [head pose](#Head-Pose-Attribute), [facial hair](#Facial-Hair-Attribute) and [smiling](#Smile-Attribute).</span><span class="sxs-lookup"><span data-stu-id="82a8b-128">The rectangles indicate the face locations in the image in pixels, as well as the optional [attributes](#Attributes) for each face such as [age](#Age-Attribute), [gender](#Gender-Attribute), [head pose](#Head-Pose-Attribute), [facial hair](#Facial-Hair-Attribute) and [smiling](#Smile-Attribute).</span></span>

<span data-ttu-id="82a8b-129">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-129">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

## <a name="e"></a><span data-ttu-id="82a8b-130">E</span><span class="sxs-lookup"><span data-stu-id="82a8b-130">E</span></span>

## <a name="f"></a><span data-ttu-id="82a8b-131">F</span><span class="sxs-lookup"><span data-stu-id="82a8b-131">F</span></span>

#### <a name="Face"></a><span data-ttu-id="82a8b-132">Face</span><span class="sxs-lookup"><span data-stu-id="82a8b-132">Face</span></span>

<span data-ttu-id="82a8b-133">Face is a unified term for the results derived from Face API related with detected faces.</span><span class="sxs-lookup"><span data-stu-id="82a8b-133">Face is a unified term for the results derived from Face API related with detected faces.</span></span> <span data-ttu-id="82a8b-134">Ultimately, face is represented by a unified identity ([Face ID](#Face-ID)), a specified region in images ([Face Rectangle](#Face-Rectangle)), and extra face related [attributes](#Face-Attributes-Facial-Attributes), such as [age](#Age-Attribute), [gender](#Gender-Attribute), [landmarks](#Face-Landmarks-Facial-Landmarks) and [head pose](#Head-Pose-Attribute).</span><span class="sxs-lookup"><span data-stu-id="82a8b-134">Ultimately, face is represented by a unified identity ([Face ID](#Face-ID)), a specified region in images ([Face Rectangle](#Face-Rectangle)), and extra face related [attributes](#Face-Attributes-Facial-Attributes), such as [age](#Age-Attribute), [gender](#Gender-Attribute), [landmarks](#Face-Landmarks-Facial-Landmarks) and [head pose](#Head-Pose-Attribute).</span></span> <span data-ttu-id="82a8b-135">Additionally, faces can be returned from [detection](#Detection-Face-Detection).</span><span class="sxs-lookup"><span data-stu-id="82a8b-135">Additionally, faces can be returned from [detection](#Detection-Face-Detection).</span></span>

<span data-ttu-id="82a8b-136">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-136">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="Face-API"></a><span data-ttu-id="82a8b-137">Face API</span><span class="sxs-lookup"><span data-stu-id="82a8b-137">Face API</span></span>

<span data-ttu-id="82a8b-138">Face API is a cloud-based API that provides the most advanced algorithms for face detection and recognition.</span><span class="sxs-lookup"><span data-stu-id="82a8b-138">Face API is a cloud-based API that provides the most advanced algorithms for face detection and recognition.</span></span> <span data-ttu-id="82a8b-139">The main functionality of Face API can be divided into two categories: face [detection](#Detection-Face-Detection) with [attributes](#Face-Attributes-Facial-Attributes), and face [recognition](#Recognition).</span><span class="sxs-lookup"><span data-stu-id="82a8b-139">The main functionality of Face API can be divided into two categories: face [detection](#Detection-Face-Detection) with [attributes](#Face-Attributes-Facial-Attributes), and face [recognition](#Recognition).</span></span>

<span data-ttu-id="82a8b-140">For more details, please refer to the following guides: [Face API Overview](./Overview.md), [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [Face - Find Similar Faces](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238), [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a)</span><span class="sxs-lookup"><span data-stu-id="82a8b-140">For more details, please refer to the following guides: [Face API Overview](./Overview.md), [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [Face - Find Similar Faces](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238), [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a)</span></span>

#### <a name="Face-Attributes-Facial-Attributes"></a><span data-ttu-id="82a8b-141">Face Attributes/Facial Attributes</span><span class="sxs-lookup"><span data-stu-id="82a8b-141">Face Attributes/Facial Attributes</span></span>

<span data-ttu-id="82a8b-142">Please see [Attributes](#Attributes).</span><span class="sxs-lookup"><span data-stu-id="82a8b-142">Please see [Attributes](#Attributes).</span></span>

#### <a name="Face-ID"></a><span data-ttu-id="82a8b-143">Face ID</span><span class="sxs-lookup"><span data-stu-id="82a8b-143">Face ID</span></span>

<span data-ttu-id="82a8b-144">Face ID is derived from the [detection](#Detection-Face-Detection) results, in which a string represents a [face](#Face) in [Face API](#Face-API).</span><span class="sxs-lookup"><span data-stu-id="82a8b-144">Face ID is derived from the [detection](#Detection-Face-Detection) results, in which a string represents a [face](#Face) in [Face API](#Face-API).</span></span>

<span data-ttu-id="82a8b-145">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-145">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="Face-Landmarks-Facial-Landmarks"></a><span data-ttu-id="82a8b-146">Face Landmarks/Facial Landmarks</span><span class="sxs-lookup"><span data-stu-id="82a8b-146">Face Landmarks/Facial Landmarks</span></span>

<span data-ttu-id="82a8b-147">Landmarks are optional in the [detection](#Detection-Face-Detection) results; which are semantic facial points, such as the eyes, nose and mouth (illustrated in following figure).</span><span class="sxs-lookup"><span data-stu-id="82a8b-147">Landmarks are optional in the [detection](#Detection-Face-Detection) results; which are semantic facial points, such as the eyes, nose and mouth (illustrated in following figure).</span></span> <span data-ttu-id="82a8b-148">Landmarks can be controlled with a [detection](#Detection-Face-Detection) request by the Boolean number returnFaceLandmarks.</span><span class="sxs-lookup"><span data-stu-id="82a8b-148">Landmarks can be controlled with a [detection](#Detection-Face-Detection) request by the Boolean number returnFaceLandmarks.</span></span> <span data-ttu-id="82a8b-149">If returnFaceLandmarks is set as true, the returned faces will have landmark attributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-149">If returnFaceLandmarks is set as true, the returned faces will have landmark attributes.</span></span>

<span data-ttu-id="82a8b-150">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-150">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

![HowToDetectFace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/landmarks.1.jpg)

#### <a name="Face-Rectangle"></a><span data-ttu-id="82a8b-152">Face Rectangle</span><span class="sxs-lookup"><span data-stu-id="82a8b-152">Face Rectangle</span></span>

<span data-ttu-id="82a8b-153">Face rectangle is derived from the [detection](#Detection-Face-Detection) results, which is an upright rectangle (left, top, width, height) in images in pixels.</span><span class="sxs-lookup"><span data-stu-id="82a8b-153">Face rectangle is derived from the [detection](#Detection-Face-Detection) results, which is an upright rectangle (left, top, width, height) in images in pixels.</span></span> <span data-ttu-id="82a8b-154">The top-left corner of a [face](#Face) (left, top), besides the width and height, indicates face sizes in x and y axes respectively.</span><span class="sxs-lookup"><span data-stu-id="82a8b-154">The top-left corner of a [face](#Face) (left, top), besides the width and height, indicates face sizes in x and y axes respectively.</span></span>

<span data-ttu-id="82a8b-155">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-155">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="Facial-Hair-Attribute"></a><span data-ttu-id="82a8b-156">Facial Hair (Attribute)</span><span class="sxs-lookup"><span data-stu-id="82a8b-156">Facial Hair (Attribute)</span></span>

<span data-ttu-id="82a8b-157">Facial hair is one of the [attributes](#Attributes) used to describe the facial hair length of the available faces.</span><span class="sxs-lookup"><span data-stu-id="82a8b-157">Facial hair is one of the [attributes](#Attributes) used to describe the facial hair length of the available faces.</span></span> <span data-ttu-id="82a8b-158">The facial hair attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by returnFaceAttributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-158">The facial hair attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by returnFaceAttributes.</span></span> <span data-ttu-id="82a8b-159">If returnfaceAttributes contains 'facialHair', the returned faces will have facial hair attributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-159">If returnfaceAttributes contains 'facialHair', the returned faces will have facial hair attributes.</span></span>

<span data-ttu-id="82a8b-160">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-160">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="Find-Similar-Faces"></a><span data-ttu-id="82a8b-161">Find Similar Faces</span><span class="sxs-lookup"><span data-stu-id="82a8b-161">Find Similar Faces</span></span>

<span data-ttu-id="82a8b-162">This API is used to search/query similar faces based on a collection of faces.</span><span class="sxs-lookup"><span data-stu-id="82a8b-162">This API is used to search/query similar faces based on a collection of faces.</span></span> <span data-ttu-id="82a8b-163">Query faces and face collections are represented as [face IDs](#Face-ID) in the request.</span><span class="sxs-lookup"><span data-stu-id="82a8b-163">Query faces and face collections are represented as [face IDs](#Face-ID) in the request.</span></span> <span data-ttu-id="82a8b-164">Returned results are searched similar faces, represented by [face IDs](#Face-ID).</span><span class="sxs-lookup"><span data-stu-id="82a8b-164">Returned results are searched similar faces, represented by [face IDs](#Face-ID).</span></span>

<span data-ttu-id="82a8b-165">For more details, please refer to the guide [Face - Find Similar Faces](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237).</span><span class="sxs-lookup"><span data-stu-id="82a8b-165">For more details, please refer to the guide [Face - Find Similar Faces](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237).</span></span>

## <a name="g"></a><span data-ttu-id="82a8b-166">G</span><span class="sxs-lookup"><span data-stu-id="82a8b-166">G</span></span>

#### <a name="Gender-Attribute"></a><span data-ttu-id="82a8b-167">Gender (Attribute)</span><span class="sxs-lookup"><span data-stu-id="82a8b-167">Gender (Attribute)</span></span>

<span data-ttu-id="82a8b-168">Gender is one of the [attributes](#Attributes) used to describe the genders of the available faces.</span><span class="sxs-lookup"><span data-stu-id="82a8b-168">Gender is one of the [attributes](#Attributes) used to describe the genders of the available faces.</span></span> <span data-ttu-id="82a8b-169">The gender attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by returnFaceAttributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-169">The gender attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by returnFaceAttributes.</span></span> <span data-ttu-id="82a8b-170">If returnfaceAttributes contains 'gender', the returned faces will have gender attributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-170">If returnfaceAttributes contains 'gender', the returned faces will have gender attributes.</span></span>

<span data-ttu-id="82a8b-171">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-171">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="Grouping"></a><span data-ttu-id="82a8b-172">Grouping</span><span class="sxs-lookup"><span data-stu-id="82a8b-172">Grouping</span></span>

<span data-ttu-id="82a8b-173">Face grouping is the grouping of a collection of faces according to facial similarities.</span><span class="sxs-lookup"><span data-stu-id="82a8b-173">Face grouping is the grouping of a collection of faces according to facial similarities.</span></span> <span data-ttu-id="82a8b-174">Face collections are indicated by the face ID collections in the request.</span><span class="sxs-lookup"><span data-stu-id="82a8b-174">Face collections are indicated by the face ID collections in the request.</span></span> <span data-ttu-id="82a8b-175">As a result of grouping, similar faces are grouped together as [groups](#Groups), and faces that are not similar to any other face are merged together as a messy group.</span><span class="sxs-lookup"><span data-stu-id="82a8b-175">As a result of grouping, similar faces are grouped together as [groups](#Groups), and faces that are not similar to any other face are merged together as a messy group.</span></span> <span data-ttu-id="82a8b-176">There is at the most, one [messy group](#Messy-Group) in the grouping result.</span><span class="sxs-lookup"><span data-stu-id="82a8b-176">There is at the most, one [messy group](#Messy-Group) in the grouping result.</span></span>

<span data-ttu-id="82a8b-177">For more details, please refer to the guide [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).</span><span class="sxs-lookup"><span data-stu-id="82a8b-177">For more details, please refer to the guide [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).</span></span>

#### <a name="Groups"></a><span data-ttu-id="82a8b-178">Groups</span><span class="sxs-lookup"><span data-stu-id="82a8b-178">Groups</span></span>

<span data-ttu-id="82a8b-179">Groups are derived from the [grouping](#Grouping) results.</span><span class="sxs-lookup"><span data-stu-id="82a8b-179">Groups are derived from the [grouping](#Grouping) results.</span></span> <span data-ttu-id="82a8b-180">Each group contains a collection of similar faces, where faces are indicated by [face IDs](#Face-ID).</span><span class="sxs-lookup"><span data-stu-id="82a8b-180">Each group contains a collection of similar faces, where faces are indicated by [face IDs](#Face-ID).</span></span>

<span data-ttu-id="82a8b-181">For more details, please refer to the guide [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).</span><span class="sxs-lookup"><span data-stu-id="82a8b-181">For more details, please refer to the guide [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).</span></span>

## <a name="h"></a><span data-ttu-id="82a8b-182">H</span><span class="sxs-lookup"><span data-stu-id="82a8b-182">H</span></span>

#### <a name="Head-Pose-Attribute"></a><span data-ttu-id="82a8b-183">Head Pose (Attribute)</span><span class="sxs-lookup"><span data-stu-id="82a8b-183">Head Pose (Attribute)</span></span>

<span data-ttu-id="82a8b-184">Head pose is one of the [attributes](#Attributes) that represents face orientation in 3D space according to roll, pitch and yaw angles, as shown in following figure.</span><span class="sxs-lookup"><span data-stu-id="82a8b-184">Head pose is one of the [attributes](#Attributes) that represents face orientation in 3D space according to roll, pitch and yaw angles, as shown in following figure.</span></span> <span data-ttu-id="82a8b-185">The value ranges of roll and yaw are [-180, 180] and [-90, 90] in degrees.</span><span class="sxs-lookup"><span data-stu-id="82a8b-185">The value ranges of roll and yaw are [-180, 180] and [-90, 90] in degrees.</span></span> <span data-ttu-id="82a8b-186">In the current version, the pitch value returned from detection is always 0.</span><span class="sxs-lookup"><span data-stu-id="82a8b-186">In the current version, the pitch value returned from detection is always 0.</span></span> <span data-ttu-id="82a8b-187">The head pose attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by the returnFaceAttributes parameter.</span><span class="sxs-lookup"><span data-stu-id="82a8b-187">The head pose attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by the returnFaceAttributes parameter.</span></span> <span data-ttu-id="82a8b-188">If returnFaceAttributes parameter contains 'headPose', the returned faces will have head pose attributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-188">If returnFaceAttributes parameter contains 'headPose', the returned faces will have head pose attributes.</span></span>

<span data-ttu-id="82a8b-189">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-189">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

![GlossaryHeadPose](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/headpose.1.jpg)

## <a name="i"></a><span data-ttu-id="82a8b-191">I</span><span class="sxs-lookup"><span data-stu-id="82a8b-191">I</span></span>

#### <a name="Identification"></a><span data-ttu-id="82a8b-192">Identification</span><span class="sxs-lookup"><span data-stu-id="82a8b-192">Identification</span></span>

<span data-ttu-id="82a8b-193">Identification is to identify one or more faces from a person group.</span><span class="sxs-lookup"><span data-stu-id="82a8b-193">Identification is to identify one or more faces from a person group.</span></span> <span data-ttu-id="82a8b-194">A [person group](#Person-Group) is a collection of [persons](#Person).</span><span class="sxs-lookup"><span data-stu-id="82a8b-194">A [person group](#Person-Group) is a collection of [persons](#Person).</span></span> <span data-ttu-id="82a8b-195">Faces and the person group are represented by [face IDs](#Face-ID) and [person group IDs](#Person-Group-ID) respectively in the request.</span><span class="sxs-lookup"><span data-stu-id="82a8b-195">Faces and the person group are represented by [face IDs](#Face-ID) and [person group IDs](#Person-Group-ID) respectively in the request.</span></span> <span data-ttu-id="82a8b-196">Identified results are [candidates](#Candidate), represented by [persons](#Person) with confidence.</span><span class="sxs-lookup"><span data-stu-id="82a8b-196">Identified results are [candidates](#Candidate), represented by [persons](#Person) with confidence.</span></span> <span data-ttu-id="82a8b-197">Multiple faces in the input are considered separately, and each face will have its own identified result.</span><span class="sxs-lookup"><span data-stu-id="82a8b-197">Multiple faces in the input are considered separately, and each face will have its own identified result.</span></span>

<span data-ttu-id="82a8b-198">**Please Note:** the person group should be trained successfully before identification.</span><span class="sxs-lookup"><span data-stu-id="82a8b-198">**Please Note:** the person group should be trained successfully before identification.</span></span> <span data-ttu-id="82a8b-199">If the person group is not trained, or the training [status](#Status-Train) is not shown as 'succeeded' (i.e. 'running', 'failed', or 'timeout'), the request response is 400.</span><span class="sxs-lookup"><span data-stu-id="82a8b-199">If the person group is not trained, or the training [status](#Status-Train) is not shown as 'succeeded' (i.e. 'running', 'failed', or 'timeout'), the request response is 400.</span></span>

<span data-ttu-id="82a8b-200">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-200">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-201">Face - Identify</span><span class="sxs-lookup"><span data-stu-id="82a8b-201">Face - Identify</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)  
[<span data-ttu-id="82a8b-202">Person - Create a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-202">Person - Create a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[<span data-ttu-id="82a8b-203">Person Group - Create a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-203">Person Group - Create a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[<span data-ttu-id="82a8b-204">Person Group - Train Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-204">Person Group - Train Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249)  

#### <a name="Is-Identical"></a><span data-ttu-id="82a8b-205">IsIdentical</span><span class="sxs-lookup"><span data-stu-id="82a8b-205">IsIdentical</span></span>

<span data-ttu-id="82a8b-206">IsIdentical is a Boolean field of [verification](#Verification) results indicating whether two faces belong to the same person.</span><span class="sxs-lookup"><span data-stu-id="82a8b-206">IsIdentical is a Boolean field of [verification](#Verification) results indicating whether two faces belong to the same person.</span></span>

<span data-ttu-id="82a8b-207">For more details, please refer to the guide [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).</span><span class="sxs-lookup"><span data-stu-id="82a8b-207">For more details, please refer to the guide [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).</span></span>

## <a name="j"></a><span data-ttu-id="82a8b-208">J</span><span class="sxs-lookup"><span data-stu-id="82a8b-208">J</span></span>

## <a name="k"></a><span data-ttu-id="82a8b-209">K</span><span class="sxs-lookup"><span data-stu-id="82a8b-209">K</span></span>

## <a name="l"></a><span data-ttu-id="82a8b-210">L</span><span class="sxs-lookup"><span data-stu-id="82a8b-210">L</span></span>

#### <a name="landmarks"></a><span data-ttu-id="82a8b-211">Landmarks</span><span class="sxs-lookup"><span data-stu-id="82a8b-211">Landmarks</span></span>

<span data-ttu-id="82a8b-212">Please see [face landmarks](#Face-Landmarks-Facial-Landmarks).</span><span class="sxs-lookup"><span data-stu-id="82a8b-212">Please see [face landmarks](#Face-Landmarks-Facial-Landmarks).</span></span>

## <a name="m"></a><span data-ttu-id="82a8b-213">M</span><span class="sxs-lookup"><span data-stu-id="82a8b-213">M</span></span>

#### <a name="Messy-Group"></a><span data-ttu-id="82a8b-214">Messy group</span><span class="sxs-lookup"><span data-stu-id="82a8b-214">Messy group</span></span>

<span data-ttu-id="82a8b-215">Messy group is derived from the [grouping](#Grouping) results; which contains faces not similar to any other face.</span><span class="sxs-lookup"><span data-stu-id="82a8b-215">Messy group is derived from the [grouping](#Grouping) results; which contains faces not similar to any other face.</span></span> <span data-ttu-id="82a8b-216">Each face in a messy group is indicated by the [face ID](#Face-ID).</span><span class="sxs-lookup"><span data-stu-id="82a8b-216">Each face in a messy group is indicated by the [face ID](#Face-ID).</span></span>

<span data-ttu-id="82a8b-217">For more details, please refer to the guide [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).</span><span class="sxs-lookup"><span data-stu-id="82a8b-217">For more details, please refer to the guide [Face - Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).</span></span>

## <a name="n"></a><span data-ttu-id="82a8b-218">N</span><span class="sxs-lookup"><span data-stu-id="82a8b-218">N</span></span>

#### <a name="name-person"></a><span data-ttu-id="82a8b-219">Name (Person)</span><span class="sxs-lookup"><span data-stu-id="82a8b-219">Name (Person)</span></span>

<span data-ttu-id="82a8b-220">Name is a user friendly descriptive string for [Person](#Person).</span><span class="sxs-lookup"><span data-stu-id="82a8b-220">Name is a user friendly descriptive string for [Person](#Person).</span></span> <span data-ttu-id="82a8b-221">Unlike the [Person ID](#Person-ID), the name of people can be duplicated within a group.</span><span class="sxs-lookup"><span data-stu-id="82a8b-221">Unlike the [Person ID](#Person-ID), the name of people can be duplicated within a group.</span></span>

<span data-ttu-id="82a8b-222">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-222">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-223">Person - Create a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-223">Person - Create a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[<span data-ttu-id="82a8b-224">Person - Get a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-224">Person - Get a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523f)

#### <a name="Name-Person-Group"></a><span data-ttu-id="82a8b-225">Name (Person Group)</span><span class="sxs-lookup"><span data-stu-id="82a8b-225">Name (Person Group)</span></span>

<span data-ttu-id="82a8b-226">Name is also a user friendly descriptive string for [Person Group](#Person-Group).</span><span class="sxs-lookup"><span data-stu-id="82a8b-226">Name is also a user friendly descriptive string for [Person Group](#Person-Group).</span></span> <span data-ttu-id="82a8b-227">Unlike the [Person Group ID](#Person-Group-ID), the name of person groups can be duplicated within a subscription.</span><span class="sxs-lookup"><span data-stu-id="82a8b-227">Unlike the [Person Group ID](#Person-Group-ID), the name of person groups can be duplicated within a subscription.</span></span>

<span data-ttu-id="82a8b-228">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-228">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-229">Person Group - Create a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-229">Person Group - Create a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[<span data-ttu-id="82a8b-230">Person Group - Get a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-230">Person Group - Get a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395246)

## <a name="o"></a><span data-ttu-id="82a8b-231">O</span><span class="sxs-lookup"><span data-stu-id="82a8b-231">O</span></span>

## <a name="p"></a><span data-ttu-id="82a8b-232">P</span><span class="sxs-lookup"><span data-stu-id="82a8b-232">P</span></span>

#### <a name="Person"></a><span data-ttu-id="82a8b-233">Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-233">Person</span></span>

<span data-ttu-id="82a8b-234">Person is a data structure managed in Face API.</span><span class="sxs-lookup"><span data-stu-id="82a8b-234">Person is a data structure managed in Face API.</span></span> <span data-ttu-id="82a8b-235">Person comes with a [Person ID](#Person-ID), as well as other attributes such as [Name](#Name-Person-Group), a collection of [Face IDs](#Face-ID), and [User Data](#UserData-User-Data).</span><span class="sxs-lookup"><span data-stu-id="82a8b-235">Person comes with a [Person ID](#Person-ID), as well as other attributes such as [Name](#Name-Person-Group), a collection of [Face IDs](#Face-ID), and [User Data](#UserData-User-Data).</span></span>

<span data-ttu-id="82a8b-236">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-236">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-237">Person - Create a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-237">Person - Create a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[<span data-ttu-id="82a8b-238">Person - Get a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-238">Person - Get a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523f)

#### <a name="Person-ID"></a><span data-ttu-id="82a8b-239">Person ID</span><span class="sxs-lookup"><span data-stu-id="82a8b-239">Person ID</span></span>

<span data-ttu-id="82a8b-240">Person ID is generated when a [person](#Person) is created successfully.</span><span class="sxs-lookup"><span data-stu-id="82a8b-240">Person ID is generated when a [person](#Person) is created successfully.</span></span> <span data-ttu-id="82a8b-241">A string is created to represent this person in [Face API](#Face-API).</span><span class="sxs-lookup"><span data-stu-id="82a8b-241">A string is created to represent this person in [Face API](#Face-API).</span></span>

<span data-ttu-id="82a8b-242">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-242">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-243">Person - Create a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-243">Person - Create a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[<span data-ttu-id="82a8b-244">Person - Get a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-244">Person - Get a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523f)

#### <a name="Person-Group"></a><span data-ttu-id="82a8b-245">Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-245">Person Group</span></span>

<span data-ttu-id="82a8b-246">Person group is a collection of [Persons](#Person) and is the unit of [Identification](#Identification).</span><span class="sxs-lookup"><span data-stu-id="82a8b-246">Person group is a collection of [Persons](#Person) and is the unit of [Identification](#Identification).</span></span> <span data-ttu-id="82a8b-247">A person group comes with a [Person Group ID](#Person-Group-ID), as well as other attributes such as [Name](#Name-Person-Group) and [User Data](#UserData-User-Data).</span><span class="sxs-lookup"><span data-stu-id="82a8b-247">A person group comes with a [Person Group ID](#Person-Group-ID), as well as other attributes such as [Name](#Name-Person-Group) and [User Data](#UserData-User-Data).</span></span>

<span data-ttu-id="82a8b-248">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-248">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-249">Person Group - Create a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-249">Person Group - Create a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[<span data-ttu-id="82a8b-250">Person Group - Get a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-250">Person Group - Get a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395246)  
[<span data-ttu-id="82a8b-251">Person - List Persons in a PersonGroup</span><span class="sxs-lookup"><span data-stu-id="82a8b-251">Person - List Persons in a PersonGroup</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395241)  

#### <a name="a-nameperson-group-idperson-group-id"></a><span data-ttu-id="82a8b-252"><a name="Person-Group-ID">Person Group ID</span><span class="sxs-lookup"><span data-stu-id="82a8b-252"><a name="Person-Group-ID">Person Group ID</span></span>

<span data-ttu-id="82a8b-253">Person group ID is a user provided string used as an identifier of a [person group](#Person-Group).</span><span class="sxs-lookup"><span data-stu-id="82a8b-253">Person group ID is a user provided string used as an identifier of a [person group](#Person-Group).</span></span> <span data-ttu-id="82a8b-254">The group ID must be unique within the subscription.</span><span class="sxs-lookup"><span data-stu-id="82a8b-254">The group ID must be unique within the subscription.</span></span>

<span data-ttu-id="82a8b-255">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-255">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-256">PersonGroup - Create a PersonGroup</span><span class="sxs-lookup"><span data-stu-id="82a8b-256">PersonGroup - Create a PersonGroup</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[<span data-ttu-id="82a8b-257">PersonGroup - Get a PersonGroup</span><span class="sxs-lookup"><span data-stu-id="82a8b-257">PersonGroup - Get a PersonGroup</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395246)

#### <a name="pose-attribute"></a><span data-ttu-id="82a8b-258">Pose (Attribute)</span><span class="sxs-lookup"><span data-stu-id="82a8b-258">Pose (Attribute)</span></span>

<span data-ttu-id="82a8b-259">Please see [Head Pose](#Head-Pose-Attribute).</span><span class="sxs-lookup"><span data-stu-id="82a8b-259">Please see [Head Pose](#Head-Pose-Attribute).</span></span>

## <a name="q"></a><span data-ttu-id="82a8b-260">Q</span><span class="sxs-lookup"><span data-stu-id="82a8b-260">Q</span></span>

## <a name="r"></a><span data-ttu-id="82a8b-261">R</span><span class="sxs-lookup"><span data-stu-id="82a8b-261">R</span></span>

#### <a name="Recognition"></a><span data-ttu-id="82a8b-262">Recognition</span><span class="sxs-lookup"><span data-stu-id="82a8b-262">Recognition</span></span>

<span data-ttu-id="82a8b-263">Recognition is a popular application area for face technologies, such as [Find Similar Faces](#Find-Similar-Faces), [Grouping](#Grouping), [Identify](#Identification),[verifying two faces same or not](#Verification).</span><span class="sxs-lookup"><span data-stu-id="82a8b-263">Recognition is a popular application area for face technologies, such as [Find Similar Faces](#Find-Similar-Faces), [Grouping](#Grouping), [Identify](#Identification),[verifying two faces same or not](#Verification).</span></span>

<span data-ttu-id="82a8b-264">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-264">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-265">Face - Find Similar Faces</span><span class="sxs-lookup"><span data-stu-id="82a8b-265">Face - Find Similar Faces</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237)  
[<span data-ttu-id="82a8b-266">Face - Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-266">Face - Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238)  
[<span data-ttu-id="82a8b-267">Face - Identify</span><span class="sxs-lookup"><span data-stu-id="82a8b-267">Face - Identify</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)  
[<span data-ttu-id="82a8b-268">Face - Verify</span><span class="sxs-lookup"><span data-stu-id="82a8b-268">Face - Verify</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a)

#### <a name="rectangle-face"></a><span data-ttu-id="82a8b-269">Rectangle (Face)</span><span class="sxs-lookup"><span data-stu-id="82a8b-269">Rectangle (Face)</span></span>

<span data-ttu-id="82a8b-270">Please see [face rectangle](#Face-Rectangle).</span><span class="sxs-lookup"><span data-stu-id="82a8b-270">Please see [face rectangle](#Face-Rectangle).</span></span>

## <a name="s"></a><span data-ttu-id="82a8b-271">S</span><span class="sxs-lookup"><span data-stu-id="82a8b-271">S</span></span>

#### <a name="Smile-Attribute"></a><span data-ttu-id="82a8b-272">Smile (Attribute)</span><span class="sxs-lookup"><span data-stu-id="82a8b-272">Smile (Attribute)</span></span>

<span data-ttu-id="82a8b-273">Smile is one of the [attributes](#Attributes) used to describe the smile expression of the available faces.</span><span class="sxs-lookup"><span data-stu-id="82a8b-273">Smile is one of the [attributes](#Attributes) used to describe the smile expression of the available faces.</span></span> <span data-ttu-id="82a8b-274">The smile attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by returnFaceAttributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-274">The smile attribute is optional in the [detection](#Detection-Face-Detection) results, and can be controlled with a [detection](#Detection-Face-Detection) request by returnFaceAttributes.</span></span> <span data-ttu-id="82a8b-275">If returnfaceAttributes contains 'smile', the returned faces will have smile attributes.</span><span class="sxs-lookup"><span data-stu-id="82a8b-275">If returnfaceAttributes contains 'smile', the returned faces will have smile attributes.</span></span>

<span data-ttu-id="82a8b-276">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="82a8b-276">For more details, please refer to the guide [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

#### <a name="similar-face-searching"></a><span data-ttu-id="82a8b-277">Similar Face Searching</span><span class="sxs-lookup"><span data-stu-id="82a8b-277">Similar Face Searching</span></span>

<span data-ttu-id="82a8b-278">Please see [Find Similar Faces](#Find-Similar-Faces).</span><span class="sxs-lookup"><span data-stu-id="82a8b-278">Please see [Find Similar Faces](#Find-Similar-Faces).</span></span>

#### <a name="Status-Train"></a><span data-ttu-id="82a8b-279">Status (Train)</span><span class="sxs-lookup"><span data-stu-id="82a8b-279">Status (Train)</span></span>

<span data-ttu-id="82a8b-280">Status is a string used to describe the procedure for [Training Person Groups](#Train-Person-Group), including 'notstarted', 'running', 'succeeded', 'failed'.</span><span class="sxs-lookup"><span data-stu-id="82a8b-280">Status is a string used to describe the procedure for [Training Person Groups](#Train-Person-Group), including 'notstarted', 'running', 'succeeded', 'failed'.</span></span>

<span data-ttu-id="82a8b-281">For more details, please refer to the guide [Person Group - Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249).</span><span class="sxs-lookup"><span data-stu-id="82a8b-281">For more details, please refer to the guide [Person Group - Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249).</span></span>

#### <a name="subscription-key"></a><span data-ttu-id="82a8b-282">Subscription key</span><span class="sxs-lookup"><span data-stu-id="82a8b-282">Subscription key</span></span>

<span data-ttu-id="82a8b-283">Subscription key is a string that you need to specify as a query string parameter in order to invoke any Face API.</span><span class="sxs-lookup"><span data-stu-id="82a8b-283">Subscription key is a string that you need to specify as a query string parameter in order to invoke any Face API.</span></span> <span data-ttu-id="82a8b-284">The subscription key can be found in My Subscriptions page after you sign in to Microsoft Cognitive Services portal.</span><span class="sxs-lookup"><span data-stu-id="82a8b-284">The subscription key can be found in My Subscriptions page after you sign in to Microsoft Cognitive Services portal.</span></span> <span data-ttu-id="82a8b-285">There will be two keys associated with each subscription: one primary key and one secondary key.</span><span class="sxs-lookup"><span data-stu-id="82a8b-285">There will be two keys associated with each subscription: one primary key and one secondary key.</span></span> <span data-ttu-id="82a8b-286">Both can be used to invoke API identically.</span><span class="sxs-lookup"><span data-stu-id="82a8b-286">Both can be used to invoke API identically.</span></span> <span data-ttu-id="82a8b-287">You need to keep the subscription keys secure, and you can regenerate subscription keys at any time from My Subscriptions page as well.</span><span class="sxs-lookup"><span data-stu-id="82a8b-287">You need to keep the subscription keys secure, and you can regenerate subscription keys at any time from My Subscriptions page as well.</span></span>

## <a name="t"></a><span data-ttu-id="82a8b-288">T</span><span class="sxs-lookup"><span data-stu-id="82a8b-288">T</span></span>

#### <a name="Train-Person-Group"></a><span data-ttu-id="82a8b-289">Train (Person Group)</span><span class="sxs-lookup"><span data-stu-id="82a8b-289">Train (Person Group)</span></span>

<span data-ttu-id="82a8b-290">This API is used to train a particular model for a specified [person group](#Person-Group) to facilitate identification.</span><span class="sxs-lookup"><span data-stu-id="82a8b-290">This API is used to train a particular model for a specified [person group](#Person-Group) to facilitate identification.</span></span> <span data-ttu-id="82a8b-291">If the training is not operated, or the [Training Status](#Status-Train) is not shown as succeeded, the identification for this person group will result in failure.</span><span class="sxs-lookup"><span data-stu-id="82a8b-291">If the training is not operated, or the [Training Status](#Status-Train) is not shown as succeeded, the identification for this person group will result in failure.</span></span>

<span data-ttu-id="82a8b-292">For more details, please refer to the following guides: [Person Group - Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249), [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)</span><span class="sxs-lookup"><span data-stu-id="82a8b-292">For more details, please refer to the following guides: [Person Group - Train Person Group](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249), [Face - Identify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)</span></span>

## <a name="u"></a><span data-ttu-id="82a8b-293">U</span><span class="sxs-lookup"><span data-stu-id="82a8b-293">U</span></span>

#### <a name="UserData-User-Data"></a><span data-ttu-id="82a8b-294">UserData/User Data</span><span class="sxs-lookup"><span data-stu-id="82a8b-294">UserData/User Data</span></span>

<span data-ttu-id="82a8b-295">User data is extra information associated with [person](#Person) and [person group](#Person-Group).</span><span class="sxs-lookup"><span data-stu-id="82a8b-295">User data is extra information associated with [person](#Person) and [person group](#Person-Group).</span></span> <span data-ttu-id="82a8b-296">User data is set by users to make data easier to use, understand and remember.</span><span class="sxs-lookup"><span data-stu-id="82a8b-296">User data is set by users to make data easier to use, understand and remember.</span></span>

<span data-ttu-id="82a8b-297">For more details, please refer to the following guides:</span><span class="sxs-lookup"><span data-stu-id="82a8b-297">For more details, please refer to the following guides:</span></span>  
[<span data-ttu-id="82a8b-298">Person - Create a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-298">Person - Create a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[<span data-ttu-id="82a8b-299">Person Group - Create a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-299">Person Group - Create a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[<span data-ttu-id="82a8b-300">Person - Update a Person</span><span class="sxs-lookup"><span data-stu-id="82a8b-300">Person - Update a Person</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395242)  
[<span data-ttu-id="82a8b-301">Person Group - Update a Person Group</span><span class="sxs-lookup"><span data-stu-id="82a8b-301">Person Group - Update a Person Group</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524a)

## <a name="v"></a><span data-ttu-id="82a8b-302">V</span><span class="sxs-lookup"><span data-stu-id="82a8b-302">V</span></span>

#### <a name="Verification"></a><span data-ttu-id="82a8b-303">Verification</span><span class="sxs-lookup"><span data-stu-id="82a8b-303">Verification</span></span>

<span data-ttu-id="82a8b-304">This API is used to verify whether two faces are the same or not.</span><span class="sxs-lookup"><span data-stu-id="82a8b-304">This API is used to verify whether two faces are the same or not.</span></span> <span data-ttu-id="82a8b-305">Both faces are represented as face IDs in the request.</span><span class="sxs-lookup"><span data-stu-id="82a8b-305">Both faces are represented as face IDs in the request.</span></span> <span data-ttu-id="82a8b-306">Verified results contain a Boolean field ([isIdentical](#Is-Identical)) indicating same if true and a number field ([confidence](#Confidence)) indicating the level of confidence.</span><span class="sxs-lookup"><span data-stu-id="82a8b-306">Verified results contain a Boolean field ([isIdentical](#Is-Identical)) indicating same if true and a number field ([confidence](#Confidence)) indicating the level of confidence.</span></span>

<span data-ttu-id="82a8b-307">For more details, please refer to the guide [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).</span><span class="sxs-lookup"><span data-stu-id="82a8b-307">For more details, please refer to the guide [Face - Verify](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).</span></span>

## <a name="w"></a><span data-ttu-id="82a8b-308">W</span><span class="sxs-lookup"><span data-stu-id="82a8b-308">W</span></span>

## <a name="x"></a><span data-ttu-id="82a8b-309">X</span><span class="sxs-lookup"><span data-stu-id="82a8b-309">X</span></span>

## <a name="y"></a><span data-ttu-id="82a8b-310">Y</span><span class="sxs-lookup"><span data-stu-id="82a8b-310">Y</span></span>

## <a name="z"></a><span data-ttu-id="82a8b-311">Z</span><span class="sxs-lookup"><span data-stu-id="82a8b-311">Z</span></span>


