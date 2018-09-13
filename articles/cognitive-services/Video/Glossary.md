---
title: Glossary for Video API in Microsoft Cognitive Services | Microsoft Docs
description: Get definitions of key terms used in the Video API in Cognitive Services.
services: cognitive-services
author: CYokel
manager: ytkuo
ms.service: cognitive-services
ms.technology: video
ms.topic: article
ms.date: 05/23/2016
ms.author: chbryant
ms.openlocfilehash: 81f9a88541818193d4efdcf51e5909c480bbe058
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556500"
---
# <a name="glossary"></a><span data-ttu-id="cf428-103">Glossary</span><span class="sxs-lookup"><span data-stu-id="cf428-103">Glossary</span></span>

## <a name="a"></a><span data-ttu-id="cf428-104">A</span><span class="sxs-lookup"><span data-stu-id="cf428-104">A</span></span>

## <a name="b"></a><span data-ttu-id="cf428-105">B</span><span class="sxs-lookup"><span data-stu-id="cf428-105">B</span></span>

## <a name="c"></a><span data-ttu-id="cf428-106">C</span><span class="sxs-lookup"><span data-stu-id="cf428-106">C</span></span>

## <a name="d"></a><span data-ttu-id="cf428-107">D</span><span class="sxs-lookup"><span data-stu-id="cf428-107">D</span></span>

### <a name="duration"></a><span data-ttu-id="cf428-108">Duration</span><span class="sxs-lookup"><span data-stu-id="cf428-108">Duration</span></span>

<span data-ttu-id="cf428-109">The length of the fragment, in ticks (within the JSON result).</span><span class="sxs-lookup"><span data-stu-id="cf428-109">The length of the fragment, in ticks (within the JSON result).</span></span>

## <a name="e"></a><span data-ttu-id="cf428-110">E</span><span class="sxs-lookup"><span data-stu-id="cf428-110">E</span></span>

### <a name="events"></a><span data-ttu-id="cf428-111">Events</span><span class="sxs-lookup"><span data-stu-id="cf428-111">Events</span></span>

<span data-ttu-id="cf428-112">An array of events (within the JSON result).</span><span class="sxs-lookup"><span data-stu-id="cf428-112">An array of events (within the JSON result).</span></span> <span data-ttu-id="cf428-113">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="cf428-113">The outer array represents one interval of time.</span></span> <span data-ttu-id="cf428-114">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="cf428-114">The inner array consists of 0 or more events that happened at that point in time.</span></span> 

## <a name="f"></a><span data-ttu-id="cf428-115">F</span><span class="sxs-lookup"><span data-stu-id="cf428-115">F</span></span>

### <a name="face-detectiontracking"></a><span data-ttu-id="cf428-116">Face Detection/Tracking</span><span class="sxs-lookup"><span data-stu-id="cf428-116">Face Detection/Tracking</span></span>

<span data-ttu-id="cf428-117">This is derived from the video face detection and tracking results (this is different from the Face API’s Face ID).</span><span class="sxs-lookup"><span data-stu-id="cf428-117">This is derived from the video face detection and tracking results (this is different from the Face API’s Face ID).</span></span> <span data-ttu-id="cf428-118">This is the index of a face.</span><span class="sxs-lookup"><span data-stu-id="cf428-118">This is the index of a face.</span></span> <span data-ttu-id="cf428-119">A given individual should have the same ID throughout the overall video.</span><span class="sxs-lookup"><span data-stu-id="cf428-119">A given individual should have the same ID throughout the overall video.</span></span> <span data-ttu-id="cf428-120">Due to limitations in the detection algorithm (e.g. occlusion) this cannot be guaranteed.</span><span class="sxs-lookup"><span data-stu-id="cf428-120">Due to limitations in the detection algorithm (e.g. occlusion) this cannot be guaranteed.</span></span>

### <a name="fragments"></a><span data-ttu-id="cf428-121">Fragments</span><span class="sxs-lookup"><span data-stu-id="cf428-121">Fragments</span></span>

<span data-ttu-id="cf428-122">The JSON metadata is chunked up into different segments called fragments.</span><span class="sxs-lookup"><span data-stu-id="cf428-122">The JSON metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="cf428-123">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="cf428-123">Each fragment contains a start, duration, interval number, and event(s).</span></span> 

### <a name="framerate"></a><span data-ttu-id="cf428-124">Framerate</span><span class="sxs-lookup"><span data-stu-id="cf428-124">Framerate</span></span>

<span data-ttu-id="cf428-125">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="cf428-125">Frames per second of the video.</span></span>

## <a name="g"></a><span data-ttu-id="cf428-126">G</span><span class="sxs-lookup"><span data-stu-id="cf428-126">G</span></span>

## <a name="h"></a><span data-ttu-id="cf428-127">H</span><span class="sxs-lookup"><span data-stu-id="cf428-127">H</span></span>


## <a name="i"></a><span data-ttu-id="cf428-128">I</span><span class="sxs-lookup"><span data-stu-id="cf428-128">I</span></span>

### <a name="interval"></a><span data-ttu-id="cf428-129">Interval</span><span class="sxs-lookup"><span data-stu-id="cf428-129">Interval</span></span>

<span data-ttu-id="cf428-130">The length of each event within the fragment, in ticks (within the JSON result).</span><span class="sxs-lookup"><span data-stu-id="cf428-130">The length of each event within the fragment, in ticks (within the JSON result).</span></span>


## <a name="j"></a><span data-ttu-id="cf428-131">J</span><span class="sxs-lookup"><span data-stu-id="cf428-131">J</span></span>

## <a name="k"></a><span data-ttu-id="cf428-132">K</span><span class="sxs-lookup"><span data-stu-id="cf428-132">K</span></span>

## <a name="l"></a><span data-ttu-id="cf428-133">L</span><span class="sxs-lookup"><span data-stu-id="cf428-133">L</span></span>

## <a name="m"></a><span data-ttu-id="cf428-134">M</span><span class="sxs-lookup"><span data-stu-id="cf428-134">M</span></span>

### <a name="motion-detection"></a><span data-ttu-id="cf428-135">Motion Detection</span><span class="sxs-lookup"><span data-stu-id="cf428-135">Motion Detection</span></span>

<span data-ttu-id="cf428-136">Motion detection is the action of detecting motion in a video.</span><span class="sxs-lookup"><span data-stu-id="cf428-136">Motion detection is the action of detecting motion in a video.</span></span>

## <a name="n"></a><span data-ttu-id="cf428-137">N</span><span class="sxs-lookup"><span data-stu-id="cf428-137">N</span></span>


## <a name="o"></a><span data-ttu-id="cf428-138">O</span><span class="sxs-lookup"><span data-stu-id="cf428-138">O</span></span>

### <a name="offset"></a><span data-ttu-id="cf428-139">Offset</span><span class="sxs-lookup"><span data-stu-id="cf428-139">Offset</span></span>

<span data-ttu-id="cf428-140">This is the time offset for timestamps (within the JSON result).</span><span class="sxs-lookup"><span data-stu-id="cf428-140">This is the time offset for timestamps (within the JSON result).</span></span> <span data-ttu-id="cf428-141">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="cf428-141">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="cf428-142">In future scenarios we support, this value may change.</span><span class="sxs-lookup"><span data-stu-id="cf428-142">In future scenarios we support, this value may change.</span></span>


## <a name="p"></a><span data-ttu-id="cf428-143">P</span><span class="sxs-lookup"><span data-stu-id="cf428-143">P</span></span>


## <a name="q"></a><span data-ttu-id="cf428-144">Q</span><span class="sxs-lookup"><span data-stu-id="cf428-144">Q</span></span>

## <a name="r"></a><span data-ttu-id="cf428-145">R</span><span class="sxs-lookup"><span data-stu-id="cf428-145">R</span></span>

### <a name="region-of-interest"></a><span data-ttu-id="cf428-146">Region of Interest</span><span class="sxs-lookup"><span data-stu-id="cf428-146">Region of Interest</span></span>

<span data-ttu-id="cf428-147">This is derived from the motion detection JSON results.</span><span class="sxs-lookup"><span data-stu-id="cf428-147">This is derived from the motion detection JSON results.</span></span> <span data-ttu-id="cf428-148">Regions refers to the area in your video where you care about motion.</span><span class="sxs-lookup"><span data-stu-id="cf428-148">Regions refers to the area in your video where you care about motion.</span></span>  

## <a name="s"></a><span data-ttu-id="cf428-149">S</span><span class="sxs-lookup"><span data-stu-id="cf428-149">S</span></span>

### <a name="sensitivity"></a><span data-ttu-id="cf428-150">Sensitivity</span><span class="sxs-lookup"><span data-stu-id="cf428-150">Sensitivity</span></span> 

<span data-ttu-id="cf428-151">User can specify ‘sensitivity level’ for motion detection, which are high, medium, and low, default is medium.</span><span class="sxs-lookup"><span data-stu-id="cf428-151">User can specify ‘sensitivity level’ for motion detection, which are high, medium, and low, default is medium.</span></span> <span data-ttu-id="cf428-152">Higher sensitivity means more motions will be detected at a cost that more false alarms will be reported.</span><span class="sxs-lookup"><span data-stu-id="cf428-152">Higher sensitivity means more motions will be detected at a cost that more false alarms will be reported.</span></span>

### <a name="stabilization"></a><span data-ttu-id="cf428-153">Stabilization</span><span class="sxs-lookup"><span data-stu-id="cf428-153">Stabilization</span></span>

<span data-ttu-id="cf428-154">Stabilization takes a shaky video and smooths and stabilizes it.</span><span class="sxs-lookup"><span data-stu-id="cf428-154">Stabilization takes a shaky video and smooths and stabilizes it.</span></span>

### <a name="start"></a><span data-ttu-id="cf428-155">Start</span><span class="sxs-lookup"><span data-stu-id="cf428-155">Start</span></span>

<span data-ttu-id="cf428-156">The start time of the first event, in ticks (within the JSON result).</span><span class="sxs-lookup"><span data-stu-id="cf428-156">The start time of the first event, in ticks (within the JSON result).</span></span>

### <a name="subscription-key"></a><span data-ttu-id="cf428-157">Subscription key</span><span class="sxs-lookup"><span data-stu-id="cf428-157">Subscription key</span></span>

<span data-ttu-id="cf428-158">Subscription key is a string that you need to specify as a query string parameter in order to invoke any Face API.</span><span class="sxs-lookup"><span data-stu-id="cf428-158">Subscription key is a string that you need to specify as a query string parameter in order to invoke any Face API.</span></span> <span data-ttu-id="cf428-159">The subscription key can be found in My Subscriptions page after you sign in the Microsoft Cognitive Services portal.</span><span class="sxs-lookup"><span data-stu-id="cf428-159">The subscription key can be found in My Subscriptions page after you sign in the Microsoft Cognitive Services portal.</span></span> <span data-ttu-id="cf428-160">There will be two keys associated with each subscription: one primary key and one secondary key.</span><span class="sxs-lookup"><span data-stu-id="cf428-160">There will be two keys associated with each subscription: one primary key and one secondary key.</span></span> <span data-ttu-id="cf428-161">Both can be used to invoke API identically.</span><span class="sxs-lookup"><span data-stu-id="cf428-161">Both can be used to invoke API identically.</span></span> <span data-ttu-id="cf428-162">You need to keep the subscription keys secure, and you can regenerate subscription keys at any time from My Subscriptions page as well.</span><span class="sxs-lookup"><span data-stu-id="cf428-162">You need to keep the subscription keys secure, and you can regenerate subscription keys at any time from My Subscriptions page as well.</span></span> 

## <a name="t"></a><span data-ttu-id="cf428-163">T</span><span class="sxs-lookup"><span data-stu-id="cf428-163">T</span></span>

### <a name="timescale"></a><span data-ttu-id="cf428-164">Timescale</span><span class="sxs-lookup"><span data-stu-id="cf428-164">Timescale</span></span>

<span data-ttu-id="cf428-165">The “ticks” per second of the video (within the JSON result).</span><span class="sxs-lookup"><span data-stu-id="cf428-165">The “ticks” per second of the video (within the JSON result).</span></span>

### <a name="type"></a><span data-ttu-id="cf428-166">Type</span><span class="sxs-lookup"><span data-stu-id="cf428-166">Type</span></span>

<span data-ttu-id="cf428-167">This is derived from the motion detection JSON results.</span><span class="sxs-lookup"><span data-stu-id="cf428-167">This is derived from the motion detection JSON results.</span></span>  <span data-ttu-id="cf428-168">2 refers to motion, 4 refers to light change.</span><span class="sxs-lookup"><span data-stu-id="cf428-168">2 refers to motion, 4 refers to light change.</span></span> 

## <a name="u"></a><span data-ttu-id="cf428-169">U</span><span class="sxs-lookup"><span data-stu-id="cf428-169">U</span></span>

## <a name="v"></a><span data-ttu-id="cf428-170">V</span><span class="sxs-lookup"><span data-stu-id="cf428-170">V</span></span>

### <a name="video-api"></a><span data-ttu-id="cf428-171">Video API</span><span class="sxs-lookup"><span data-stu-id="cf428-171">Video API</span></span>

<span data-ttu-id="cf428-172">Video API is a cloud-based API that provides the most advanced algorithms for stabilization, face detection and tracking, and motion detection in video.</span><span class="sxs-lookup"><span data-stu-id="cf428-172">Video API is a cloud-based API that provides the most advanced algorithms for stabilization, face detection and tracking, and motion detection in video.</span></span> 

## <a name="w"></a><span data-ttu-id="cf428-173">W</span><span class="sxs-lookup"><span data-stu-id="cf428-173">W</span></span>

## <a name="x"></a><span data-ttu-id="cf428-174">X</span><span class="sxs-lookup"><span data-stu-id="cf428-174">X</span></span>

## <a name="y"></a><span data-ttu-id="cf428-175">Y</span><span class="sxs-lookup"><span data-stu-id="cf428-175">Y</span></span>

## <a name="z"></a><span data-ttu-id="cf428-176">Z</span><span class="sxs-lookup"><span data-stu-id="cf428-176">Z</span></span>

 * [<span data-ttu-id="cf428-177">Link back to Overview</span><span class="sxs-lookup"><span data-stu-id="cf428-177">Link back to Overview</span></span>](Home.md)
 * [<span data-ttu-id="cf428-178">Link back to Get Started with Video API</span><span class="sxs-lookup"><span data-stu-id="cf428-178">Link back to Get Started with Video API</span></span>](GetStarted.md)
 * [<span data-ttu-id="cf428-179">Link back to How to Call Video API</span><span class="sxs-lookup"><span data-stu-id="cf428-179">Link back to How to Call Video API</span></span>](./How-To/HowtoCallVideoAPIs.md)
