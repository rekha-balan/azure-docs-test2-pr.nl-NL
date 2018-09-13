---
title: Build an IoT solution by using Stream Analytics | Microsoft Docs
description: Getting-started tutorial for the Stream Analytics IoT solution of a tollbooth scenario
keywords: iot solution, window functions
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 950b277d08453fa2d262687ce07c43fe1e621904
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553551"
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a><span data-ttu-id="0e3b2-104">Build an IoT solution by using Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0e3b2-104">Build an IoT solution by using Stream Analytics</span></span>
## <a name="introduction"></a><span data-ttu-id="0e3b2-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="0e3b2-105">Introduction</span></span>
<span data-ttu-id="0e3b2-106">In this tutorial, you will learn how to use Azure Stream Analytics to get real-time insights from your data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-106">In this tutorial, you will learn how to use Azure Stream Analytics to get real-time insights from your data.</span></span> <span data-ttu-id="0e3b2-107">Developers can easily combine streams of data, such as click-streams, logs, and device-generated events, with historical records or reference data to derive business insights.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-107">Developers can easily combine streams of data, such as click-streams, logs, and device-generated events, with historical records or reference data to derive business insights.</span></span> <span data-ttu-id="0e3b2-108">As a fully managed, real-time stream computation service that's hosted in Microsoft Azure, Azure Stream Analytics provides built-in resiliency, low latency, and scalability to get you up and running in minutes.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-108">As a fully managed, real-time stream computation service that's hosted in Microsoft Azure, Azure Stream Analytics provides built-in resiliency, low latency, and scalability to get you up and running in minutes.</span></span>

<span data-ttu-id="0e3b2-109">After completing this tutorial, you will be able to:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-109">After completing this tutorial, you will be able to:</span></span>

* <span data-ttu-id="0e3b2-110">Familiarize yourself with the Azure Stream Analytics portal.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-110">Familiarize yourself with the Azure Stream Analytics portal.</span></span>
* <span data-ttu-id="0e3b2-111">Configure and deploy a streaming job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-111">Configure and deploy a streaming job.</span></span>
* <span data-ttu-id="0e3b2-112">Articulate real-world problems and solve them by using the Stream Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-112">Articulate real-world problems and solve them by using the Stream Analytics query language.</span></span>
* <span data-ttu-id="0e3b2-113">Develop streaming solutions for your customers by using Stream Analytics with confidence.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-113">Develop streaming solutions for your customers by using Stream Analytics with confidence.</span></span>
* <span data-ttu-id="0e3b2-114">Use the monitoring and logging experience to troubleshoot issues.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-114">Use the monitoring and logging experience to troubleshoot issues.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e3b2-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e3b2-115">Prerequisites</span></span>
<span data-ttu-id="0e3b2-116">You will need the following prerequisites to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-116">You will need the following prerequisites to complete this tutorial:</span></span>

* <span data-ttu-id="0e3b2-117">The latest version of [Azure PowerShell](/powershell/azureps-cmdlets-docs)</span><span class="sxs-lookup"><span data-stu-id="0e3b2-117">The latest version of [Azure PowerShell](/powershell/azureps-cmdlets-docs)</span></span>
* <span data-ttu-id="0e3b2-118">Visual Studio 2017, 2015, or the free [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="0e3b2-118">Visual Studio 2017, 2015, or the free [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)</span></span>
* <span data-ttu-id="0e3b2-119">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="0e3b2-119">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="0e3b2-120">Administrative privileges on the computer</span><span class="sxs-lookup"><span data-stu-id="0e3b2-120">Administrative privileges on the computer</span></span>
* <span data-ttu-id="0e3b2-121">Download of [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) from the Microsoft Download Center</span><span class="sxs-lookup"><span data-stu-id="0e3b2-121">Download of [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) from the Microsoft Download Center</span></span>
* <span data-ttu-id="0e3b2-122">Optional: Source code for the TollApp event generator in [GitHub](https://aka.ms/azure-stream-analytics-toll-source)</span><span class="sxs-lookup"><span data-stu-id="0e3b2-122">Optional: Source code for the TollApp event generator in [GitHub](https://aka.ms/azure-stream-analytics-toll-source)</span></span>

## <a name="scenario-introduction-hello-toll"></a><span data-ttu-id="0e3b2-123">Scenario introduction: “Hello, Toll!”</span><span class="sxs-lookup"><span data-stu-id="0e3b2-123">Scenario introduction: “Hello, Toll!”</span></span>
<span data-ttu-id="0e3b2-124">A toll station is a common phenomenon.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-124">A toll station is a common phenomenon.</span></span> <span data-ttu-id="0e3b2-125">You encounter them on many expressways, bridges, and tunnels across the world.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-125">You encounter them on many expressways, bridges, and tunnels across the world.</span></span> <span data-ttu-id="0e3b2-126">Each toll station has multiple toll booths.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-126">Each toll station has multiple toll booths.</span></span> <span data-ttu-id="0e3b2-127">At manual booths, you stop to pay the toll to an attendant.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-127">At manual booths, you stop to pay the toll to an attendant.</span></span> <span data-ttu-id="0e3b2-128">At automated booths, a sensor on top of each booth scans an RFID card that's affixed to the windshield of your vehicle as you pass the toll booth.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-128">At automated booths, a sensor on top of each booth scans an RFID card that's affixed to the windshield of your vehicle as you pass the toll booth.</span></span> <span data-ttu-id="0e3b2-129">It is easy to visualize the passage of vehicles through these toll stations as an event stream over which interesting operations can be performed.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-129">It is easy to visualize the passage of vehicles through these toll stations as an event stream over which interesting operations can be performed.</span></span>

![Picture of cars at toll booths](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a><span data-ttu-id="0e3b2-131">Incoming data</span><span class="sxs-lookup"><span data-stu-id="0e3b2-131">Incoming data</span></span>
<span data-ttu-id="0e3b2-132">This tutorial works with two streams of data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-132">This tutorial works with two streams of data.</span></span> <span data-ttu-id="0e3b2-133">Sensors installed in the entrance and exit of the toll stations produce the first stream.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-133">Sensors installed in the entrance and exit of the toll stations produce the first stream.</span></span> <span data-ttu-id="0e3b2-134">The second stream is a static lookup dataset that has vehicle registration data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-134">The second stream is a static lookup dataset that has vehicle registration data.</span></span>

### <a name="entry-data-stream"></a><span data-ttu-id="0e3b2-135">Entry data stream</span><span class="sxs-lookup"><span data-stu-id="0e3b2-135">Entry data stream</span></span>
<span data-ttu-id="0e3b2-136">The entry data stream contains information about cars as they enter toll stations.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-136">The entry data stream contains information about cars as they enter toll stations.</span></span>

| <span data-ttu-id="0e3b2-137">TollID</span><span class="sxs-lookup"><span data-stu-id="0e3b2-137">TollID</span></span> | <span data-ttu-id="0e3b2-138">EntryTime</span><span class="sxs-lookup"><span data-stu-id="0e3b2-138">EntryTime</span></span> | <span data-ttu-id="0e3b2-139">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="0e3b2-139">LicensePlate</span></span> | <span data-ttu-id="0e3b2-140">State</span><span class="sxs-lookup"><span data-stu-id="0e3b2-140">State</span></span> | <span data-ttu-id="0e3b2-141">Make</span><span class="sxs-lookup"><span data-stu-id="0e3b2-141">Make</span></span> | <span data-ttu-id="0e3b2-142">Model</span><span class="sxs-lookup"><span data-stu-id="0e3b2-142">Model</span></span> | <span data-ttu-id="0e3b2-143">VehicleType</span><span class="sxs-lookup"><span data-stu-id="0e3b2-143">VehicleType</span></span> | <span data-ttu-id="0e3b2-144">VehicleWeight</span><span class="sxs-lookup"><span data-stu-id="0e3b2-144">VehicleWeight</span></span> | <span data-ttu-id="0e3b2-145">Toll</span><span class="sxs-lookup"><span data-stu-id="0e3b2-145">Toll</span></span> | <span data-ttu-id="0e3b2-146">Tag</span><span class="sxs-lookup"><span data-stu-id="0e3b2-146">Tag</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0e3b2-147">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-147">1</span></span> |<span data-ttu-id="0e3b2-148">2014-09-10 12:01:00.000</span><span class="sxs-lookup"><span data-stu-id="0e3b2-148">2014-09-10 12:01:00.000</span></span> |<span data-ttu-id="0e3b2-149">JNB 7001</span><span class="sxs-lookup"><span data-stu-id="0e3b2-149">JNB 7001</span></span> |<span data-ttu-id="0e3b2-150">NY</span><span class="sxs-lookup"><span data-stu-id="0e3b2-150">NY</span></span> |<span data-ttu-id="0e3b2-151">Honda</span><span class="sxs-lookup"><span data-stu-id="0e3b2-151">Honda</span></span> |<span data-ttu-id="0e3b2-152">CRV</span><span class="sxs-lookup"><span data-stu-id="0e3b2-152">CRV</span></span> |<span data-ttu-id="0e3b2-153">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-153">1</span></span> |<span data-ttu-id="0e3b2-154">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-154">0</span></span> |<span data-ttu-id="0e3b2-155">7</span><span class="sxs-lookup"><span data-stu-id="0e3b2-155">7</span></span> | |
| <span data-ttu-id="0e3b2-156">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-156">1</span></span> |<span data-ttu-id="0e3b2-157">2014-09-10 12:02:00.000</span><span class="sxs-lookup"><span data-stu-id="0e3b2-157">2014-09-10 12:02:00.000</span></span> |<span data-ttu-id="0e3b2-158">YXZ 1001</span><span class="sxs-lookup"><span data-stu-id="0e3b2-158">YXZ 1001</span></span> |<span data-ttu-id="0e3b2-159">NY</span><span class="sxs-lookup"><span data-stu-id="0e3b2-159">NY</span></span> |<span data-ttu-id="0e3b2-160">Toyota</span><span class="sxs-lookup"><span data-stu-id="0e3b2-160">Toyota</span></span> |<span data-ttu-id="0e3b2-161">Camry</span><span class="sxs-lookup"><span data-stu-id="0e3b2-161">Camry</span></span> |<span data-ttu-id="0e3b2-162">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-162">1</span></span> |<span data-ttu-id="0e3b2-163">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-163">0</span></span> |<span data-ttu-id="0e3b2-164">4</span><span class="sxs-lookup"><span data-stu-id="0e3b2-164">4</span></span> |<span data-ttu-id="0e3b2-165">123456789</span><span class="sxs-lookup"><span data-stu-id="0e3b2-165">123456789</span></span> |
| <span data-ttu-id="0e3b2-166">3</span><span class="sxs-lookup"><span data-stu-id="0e3b2-166">3</span></span> |<span data-ttu-id="0e3b2-167">2014-09-10 12:02:00.000</span><span class="sxs-lookup"><span data-stu-id="0e3b2-167">2014-09-10 12:02:00.000</span></span> |<span data-ttu-id="0e3b2-168">ABC 1004</span><span class="sxs-lookup"><span data-stu-id="0e3b2-168">ABC 1004</span></span> |<span data-ttu-id="0e3b2-169">CT</span><span class="sxs-lookup"><span data-stu-id="0e3b2-169">CT</span></span> |<span data-ttu-id="0e3b2-170">Ford</span><span class="sxs-lookup"><span data-stu-id="0e3b2-170">Ford</span></span> |<span data-ttu-id="0e3b2-171">Taurus</span><span class="sxs-lookup"><span data-stu-id="0e3b2-171">Taurus</span></span> |<span data-ttu-id="0e3b2-172">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-172">1</span></span> |<span data-ttu-id="0e3b2-173">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-173">0</span></span> |<span data-ttu-id="0e3b2-174">5</span><span class="sxs-lookup"><span data-stu-id="0e3b2-174">5</span></span> |<span data-ttu-id="0e3b2-175">456789123</span><span class="sxs-lookup"><span data-stu-id="0e3b2-175">456789123</span></span> |
| <span data-ttu-id="0e3b2-176">2</span><span class="sxs-lookup"><span data-stu-id="0e3b2-176">2</span></span> |<span data-ttu-id="0e3b2-177">2014-09-10 12:03:00.000</span><span class="sxs-lookup"><span data-stu-id="0e3b2-177">2014-09-10 12:03:00.000</span></span> |<span data-ttu-id="0e3b2-178">XYZ 1003</span><span class="sxs-lookup"><span data-stu-id="0e3b2-178">XYZ 1003</span></span> |<span data-ttu-id="0e3b2-179">CT</span><span class="sxs-lookup"><span data-stu-id="0e3b2-179">CT</span></span> |<span data-ttu-id="0e3b2-180">Toyota</span><span class="sxs-lookup"><span data-stu-id="0e3b2-180">Toyota</span></span> |<span data-ttu-id="0e3b2-181">Corolla</span><span class="sxs-lookup"><span data-stu-id="0e3b2-181">Corolla</span></span> |<span data-ttu-id="0e3b2-182">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-182">1</span></span> |<span data-ttu-id="0e3b2-183">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-183">0</span></span> |<span data-ttu-id="0e3b2-184">4</span><span class="sxs-lookup"><span data-stu-id="0e3b2-184">4</span></span> | |
| <span data-ttu-id="0e3b2-185">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-185">1</span></span> |<span data-ttu-id="0e3b2-186">2014-09-10 12:03:00.000</span><span class="sxs-lookup"><span data-stu-id="0e3b2-186">2014-09-10 12:03:00.000</span></span> |<span data-ttu-id="0e3b2-187">BNJ 1007</span><span class="sxs-lookup"><span data-stu-id="0e3b2-187">BNJ 1007</span></span> |<span data-ttu-id="0e3b2-188">NY</span><span class="sxs-lookup"><span data-stu-id="0e3b2-188">NY</span></span> |<span data-ttu-id="0e3b2-189">Honda</span><span class="sxs-lookup"><span data-stu-id="0e3b2-189">Honda</span></span> |<span data-ttu-id="0e3b2-190">CRV</span><span class="sxs-lookup"><span data-stu-id="0e3b2-190">CRV</span></span> |<span data-ttu-id="0e3b2-191">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-191">1</span></span> |<span data-ttu-id="0e3b2-192">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-192">0</span></span> |<span data-ttu-id="0e3b2-193">5</span><span class="sxs-lookup"><span data-stu-id="0e3b2-193">5</span></span> |<span data-ttu-id="0e3b2-194">789123456</span><span class="sxs-lookup"><span data-stu-id="0e3b2-194">789123456</span></span> |
| <span data-ttu-id="0e3b2-195">2</span><span class="sxs-lookup"><span data-stu-id="0e3b2-195">2</span></span> |<span data-ttu-id="0e3b2-196">2014-09-10 12:05:00.000</span><span class="sxs-lookup"><span data-stu-id="0e3b2-196">2014-09-10 12:05:00.000</span></span> |<span data-ttu-id="0e3b2-197">CDE 1007</span><span class="sxs-lookup"><span data-stu-id="0e3b2-197">CDE 1007</span></span> |<span data-ttu-id="0e3b2-198">NJ</span><span class="sxs-lookup"><span data-stu-id="0e3b2-198">NJ</span></span> |<span data-ttu-id="0e3b2-199">Toyota</span><span class="sxs-lookup"><span data-stu-id="0e3b2-199">Toyota</span></span> |<span data-ttu-id="0e3b2-200">4x4</span><span class="sxs-lookup"><span data-stu-id="0e3b2-200">4x4</span></span> |<span data-ttu-id="0e3b2-201">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-201">1</span></span> |<span data-ttu-id="0e3b2-202">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-202">0</span></span> |<span data-ttu-id="0e3b2-203">6</span><span class="sxs-lookup"><span data-stu-id="0e3b2-203">6</span></span> |<span data-ttu-id="0e3b2-204">321987654</span><span class="sxs-lookup"><span data-stu-id="0e3b2-204">321987654</span></span> |

<span data-ttu-id="0e3b2-205">Here is a short description of the columns:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-205">Here is a short description of the columns:</span></span>

| <span data-ttu-id="0e3b2-206">Column</span><span class="sxs-lookup"><span data-stu-id="0e3b2-206">Column</span></span> | <span data-ttu-id="0e3b2-207">Description</span><span class="sxs-lookup"><span data-stu-id="0e3b2-207">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0e3b2-208">TollID</span><span class="sxs-lookup"><span data-stu-id="0e3b2-208">TollID</span></span> |<span data-ttu-id="0e3b2-209">The toll booth ID that uniquely identifies a toll booth</span><span class="sxs-lookup"><span data-stu-id="0e3b2-209">The toll booth ID that uniquely identifies a toll booth</span></span> |
| <span data-ttu-id="0e3b2-210">EntryTime</span><span class="sxs-lookup"><span data-stu-id="0e3b2-210">EntryTime</span></span> |<span data-ttu-id="0e3b2-211">The date and time of entry of the vehicle to the toll booth in UTC</span><span class="sxs-lookup"><span data-stu-id="0e3b2-211">The date and time of entry of the vehicle to the toll booth in UTC</span></span> |
| <span data-ttu-id="0e3b2-212">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="0e3b2-212">LicensePlate</span></span> |<span data-ttu-id="0e3b2-213">The license plate number of the vehicle</span><span class="sxs-lookup"><span data-stu-id="0e3b2-213">The license plate number of the vehicle</span></span> |
| <span data-ttu-id="0e3b2-214">State</span><span class="sxs-lookup"><span data-stu-id="0e3b2-214">State</span></span> |<span data-ttu-id="0e3b2-215">A state in United States</span><span class="sxs-lookup"><span data-stu-id="0e3b2-215">A state in United States</span></span> |
| <span data-ttu-id="0e3b2-216">Make</span><span class="sxs-lookup"><span data-stu-id="0e3b2-216">Make</span></span> |<span data-ttu-id="0e3b2-217">The manufacturer of the automobile</span><span class="sxs-lookup"><span data-stu-id="0e3b2-217">The manufacturer of the automobile</span></span> |
| <span data-ttu-id="0e3b2-218">Model</span><span class="sxs-lookup"><span data-stu-id="0e3b2-218">Model</span></span> |<span data-ttu-id="0e3b2-219">The model number of the automobile</span><span class="sxs-lookup"><span data-stu-id="0e3b2-219">The model number of the automobile</span></span> |
| <span data-ttu-id="0e3b2-220">VehicleType</span><span class="sxs-lookup"><span data-stu-id="0e3b2-220">VehicleType</span></span> |<span data-ttu-id="0e3b2-221">Either 1 for passenger vehicles or 2 for commercial vehicles</span><span class="sxs-lookup"><span data-stu-id="0e3b2-221">Either 1 for passenger vehicles or 2 for commercial vehicles</span></span> |
| <span data-ttu-id="0e3b2-222">WeightType</span><span class="sxs-lookup"><span data-stu-id="0e3b2-222">WeightType</span></span> |<span data-ttu-id="0e3b2-223">Vehicle weight in tons; 0 for passenger vehicles</span><span class="sxs-lookup"><span data-stu-id="0e3b2-223">Vehicle weight in tons; 0 for passenger vehicles</span></span> |
| <span data-ttu-id="0e3b2-224">Toll</span><span class="sxs-lookup"><span data-stu-id="0e3b2-224">Toll</span></span> |<span data-ttu-id="0e3b2-225">The toll value in USD</span><span class="sxs-lookup"><span data-stu-id="0e3b2-225">The toll value in USD</span></span> |
| <span data-ttu-id="0e3b2-226">Tag</span><span class="sxs-lookup"><span data-stu-id="0e3b2-226">Tag</span></span> |<span data-ttu-id="0e3b2-227">The e-Tag on the automobile that automates payment; blank where the payment was done manually</span><span class="sxs-lookup"><span data-stu-id="0e3b2-227">The e-Tag on the automobile that automates payment; blank where the payment was done manually</span></span> |

### <a name="exit-data-stream"></a><span data-ttu-id="0e3b2-228">Exit data stream</span><span class="sxs-lookup"><span data-stu-id="0e3b2-228">Exit data stream</span></span>
<span data-ttu-id="0e3b2-229">The exit data stream contains information about cars leaving the toll station.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-229">The exit data stream contains information about cars leaving the toll station.</span></span>

| <span data-ttu-id="0e3b2-230">**TollId**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-230">**TollId**</span></span> | <span data-ttu-id="0e3b2-231">**ExitTime**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-231">**ExitTime**</span></span> | <span data-ttu-id="0e3b2-232">**LicensePlate**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-232">**LicensePlate**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e3b2-233">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-233">1</span></span> |<span data-ttu-id="0e3b2-234">2014-09-10T12:03:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="0e3b2-234">2014-09-10T12:03:00.0000000Z</span></span> |<span data-ttu-id="0e3b2-235">JNB 7001</span><span class="sxs-lookup"><span data-stu-id="0e3b2-235">JNB 7001</span></span> |
| <span data-ttu-id="0e3b2-236">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-236">1</span></span> |<span data-ttu-id="0e3b2-237">2014-09-10T12:03:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="0e3b2-237">2014-09-10T12:03:00.0000000Z</span></span> |<span data-ttu-id="0e3b2-238">YXZ 1001</span><span class="sxs-lookup"><span data-stu-id="0e3b2-238">YXZ 1001</span></span> |
| <span data-ttu-id="0e3b2-239">3</span><span class="sxs-lookup"><span data-stu-id="0e3b2-239">3</span></span> |<span data-ttu-id="0e3b2-240">2014-09-10T12:04:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="0e3b2-240">2014-09-10T12:04:00.0000000Z</span></span> |<span data-ttu-id="0e3b2-241">ABC 1004</span><span class="sxs-lookup"><span data-stu-id="0e3b2-241">ABC 1004</span></span> |
| <span data-ttu-id="0e3b2-242">2</span><span class="sxs-lookup"><span data-stu-id="0e3b2-242">2</span></span> |<span data-ttu-id="0e3b2-243">2014-09-10T12:07:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="0e3b2-243">2014-09-10T12:07:00.0000000Z</span></span> |<span data-ttu-id="0e3b2-244">XYZ 1003</span><span class="sxs-lookup"><span data-stu-id="0e3b2-244">XYZ 1003</span></span> |
| <span data-ttu-id="0e3b2-245">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-245">1</span></span> |<span data-ttu-id="0e3b2-246">2014-09-10T12:08:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="0e3b2-246">2014-09-10T12:08:00.0000000Z</span></span> |<span data-ttu-id="0e3b2-247">BNJ 1007</span><span class="sxs-lookup"><span data-stu-id="0e3b2-247">BNJ 1007</span></span> |
| <span data-ttu-id="0e3b2-248">2</span><span class="sxs-lookup"><span data-stu-id="0e3b2-248">2</span></span> |<span data-ttu-id="0e3b2-249">2014-09-10T12:07:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="0e3b2-249">2014-09-10T12:07:00.0000000Z</span></span> |<span data-ttu-id="0e3b2-250">CDE 1007</span><span class="sxs-lookup"><span data-stu-id="0e3b2-250">CDE 1007</span></span> |

<span data-ttu-id="0e3b2-251">Here is a short description of the columns:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-251">Here is a short description of the columns:</span></span>

| <span data-ttu-id="0e3b2-252">Column</span><span class="sxs-lookup"><span data-stu-id="0e3b2-252">Column</span></span> | <span data-ttu-id="0e3b2-253">Description</span><span class="sxs-lookup"><span data-stu-id="0e3b2-253">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0e3b2-254">TollID</span><span class="sxs-lookup"><span data-stu-id="0e3b2-254">TollID</span></span> |<span data-ttu-id="0e3b2-255">The toll booth ID that uniquely identifies a toll booth</span><span class="sxs-lookup"><span data-stu-id="0e3b2-255">The toll booth ID that uniquely identifies a toll booth</span></span> |
| <span data-ttu-id="0e3b2-256">ExitTime</span><span class="sxs-lookup"><span data-stu-id="0e3b2-256">ExitTime</span></span> |<span data-ttu-id="0e3b2-257">The date and time of exit of the vehicle from toll booth in UTC</span><span class="sxs-lookup"><span data-stu-id="0e3b2-257">The date and time of exit of the vehicle from toll booth in UTC</span></span> |
| <span data-ttu-id="0e3b2-258">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="0e3b2-258">LicensePlate</span></span> |<span data-ttu-id="0e3b2-259">The license plate number of the vehicle</span><span class="sxs-lookup"><span data-stu-id="0e3b2-259">The license plate number of the vehicle</span></span> |

### <a name="commercial-vehicle-registration-data"></a><span data-ttu-id="0e3b2-260">Commercial vehicle registration data</span><span class="sxs-lookup"><span data-stu-id="0e3b2-260">Commercial vehicle registration data</span></span>
<span data-ttu-id="0e3b2-261">The tutorial uses a static snapshot of a commercial vehicle registration database.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-261">The tutorial uses a static snapshot of a commercial vehicle registration database.</span></span>

| <span data-ttu-id="0e3b2-262">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="0e3b2-262">LicensePlate</span></span> | <span data-ttu-id="0e3b2-263">RegistrationId</span><span class="sxs-lookup"><span data-stu-id="0e3b2-263">RegistrationId</span></span> | <span data-ttu-id="0e3b2-264">Expired</span><span class="sxs-lookup"><span data-stu-id="0e3b2-264">Expired</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e3b2-265">SVT 6023</span><span class="sxs-lookup"><span data-stu-id="0e3b2-265">SVT 6023</span></span> |<span data-ttu-id="0e3b2-266">285429838</span><span class="sxs-lookup"><span data-stu-id="0e3b2-266">285429838</span></span> |<span data-ttu-id="0e3b2-267">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-267">1</span></span> |
| <span data-ttu-id="0e3b2-268">XLZ 3463</span><span class="sxs-lookup"><span data-stu-id="0e3b2-268">XLZ 3463</span></span> |<span data-ttu-id="0e3b2-269">362715656</span><span class="sxs-lookup"><span data-stu-id="0e3b2-269">362715656</span></span> |<span data-ttu-id="0e3b2-270">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-270">0</span></span> |
| <span data-ttu-id="0e3b2-271">BAC 1005</span><span class="sxs-lookup"><span data-stu-id="0e3b2-271">BAC 1005</span></span> |<span data-ttu-id="0e3b2-272">876133137</span><span class="sxs-lookup"><span data-stu-id="0e3b2-272">876133137</span></span> |<span data-ttu-id="0e3b2-273">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-273">1</span></span> |
| <span data-ttu-id="0e3b2-274">RIV 8632</span><span class="sxs-lookup"><span data-stu-id="0e3b2-274">RIV 8632</span></span> |<span data-ttu-id="0e3b2-275">992711956</span><span class="sxs-lookup"><span data-stu-id="0e3b2-275">992711956</span></span> |<span data-ttu-id="0e3b2-276">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-276">0</span></span> |
| <span data-ttu-id="0e3b2-277">SNY 7188</span><span class="sxs-lookup"><span data-stu-id="0e3b2-277">SNY 7188</span></span> |<span data-ttu-id="0e3b2-278">592133890</span><span class="sxs-lookup"><span data-stu-id="0e3b2-278">592133890</span></span> |<span data-ttu-id="0e3b2-279">0</span><span class="sxs-lookup"><span data-stu-id="0e3b2-279">0</span></span> |
| <span data-ttu-id="0e3b2-280">ELH 9896</span><span class="sxs-lookup"><span data-stu-id="0e3b2-280">ELH 9896</span></span> |<span data-ttu-id="0e3b2-281">678427724</span><span class="sxs-lookup"><span data-stu-id="0e3b2-281">678427724</span></span> |<span data-ttu-id="0e3b2-282">1</span><span class="sxs-lookup"><span data-stu-id="0e3b2-282">1</span></span> |

<span data-ttu-id="0e3b2-283">Here is a short description of the columns:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-283">Here is a short description of the columns:</span></span>

| <span data-ttu-id="0e3b2-284">Column</span><span class="sxs-lookup"><span data-stu-id="0e3b2-284">Column</span></span> | <span data-ttu-id="0e3b2-285">Description</span><span class="sxs-lookup"><span data-stu-id="0e3b2-285">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0e3b2-286">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="0e3b2-286">LicensePlate</span></span> |<span data-ttu-id="0e3b2-287">The license plate number of the vehicle</span><span class="sxs-lookup"><span data-stu-id="0e3b2-287">The license plate number of the vehicle</span></span> |
| <span data-ttu-id="0e3b2-288">RegistrationId</span><span class="sxs-lookup"><span data-stu-id="0e3b2-288">RegistrationId</span></span> |<span data-ttu-id="0e3b2-289">The vehicle's registration ID</span><span class="sxs-lookup"><span data-stu-id="0e3b2-289">The vehicle's registration ID</span></span> |
| <span data-ttu-id="0e3b2-290">Expired</span><span class="sxs-lookup"><span data-stu-id="0e3b2-290">Expired</span></span> |<span data-ttu-id="0e3b2-291">The registration status of the vehicle: 0 if vehicle registration is active, 1 if registration is expired</span><span class="sxs-lookup"><span data-stu-id="0e3b2-291">The registration status of the vehicle: 0 if vehicle registration is active, 1 if registration is expired</span></span> |

## <a name="set-up-the-environment-for-azure-stream-analytics"></a><span data-ttu-id="0e3b2-292">Set up the environment for Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0e3b2-292">Set up the environment for Azure Stream Analytics</span></span>
<span data-ttu-id="0e3b2-293">To complete this tutorial, you need a Microsoft Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-293">To complete this tutorial, you need a Microsoft Azure subscription.</span></span> <span data-ttu-id="0e3b2-294">Microsoft offers free trial for Microsoft Azure services.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-294">Microsoft offers free trial for Microsoft Azure services.</span></span>

<span data-ttu-id="0e3b2-295">If you do not have an Azure account, you can [request a free trial version](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-295">If you do not have an Azure account, you can [request a free trial version](http://azure.microsoft.com/pricing/free-trial/).</span></span>

> [!NOTE]
> <span data-ttu-id="0e3b2-296">To sign up for a free trial, you need a mobile device that can receive text messages and a valid credit card.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-296">To sign up for a free trial, you need a mobile device that can receive text messages and a valid credit card.</span></span>
> 
> 

<span data-ttu-id="0e3b2-297">Be sure to follow the steps in the “Clean up your Azure account” section at the end of this article so that you can make the best use of your $200 free Azure credit.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-297">Be sure to follow the steps in the “Clean up your Azure account” section at the end of this article so that you can make the best use of your $200 free Azure credit.</span></span>

## <a name="provision-azure-resources-required-for-the-tutorial"></a><span data-ttu-id="0e3b2-298">Provision Azure resources required for the tutorial</span><span class="sxs-lookup"><span data-stu-id="0e3b2-298">Provision Azure resources required for the tutorial</span></span>
<span data-ttu-id="0e3b2-299">This tutorial requires two event hubs to receive *entry* and *exit* data streams.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-299">This tutorial requires two event hubs to receive *entry* and *exit* data streams.</span></span> <span data-ttu-id="0e3b2-300">Azure SQL Database outputs the results of the Stream Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-300">Azure SQL Database outputs the results of the Stream Analytics jobs.</span></span> <span data-ttu-id="0e3b2-301">Azure Storage stores reference data about vehicle registrations.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-301">Azure Storage stores reference data about vehicle registrations.</span></span>

<span data-ttu-id="0e3b2-302">You can use the Setup.ps1 script in the TollApp folder on GitHub to create all required resources.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-302">You can use the Setup.ps1 script in the TollApp folder on GitHub to create all required resources.</span></span> <span data-ttu-id="0e3b2-303">In the interest of time, we recommend that you run it.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-303">In the interest of time, we recommend that you run it.</span></span> <span data-ttu-id="0e3b2-304">If you would like to learn more about how to configure these resources in the Azure portal, refer to the “Configuring tutorial resources in Azure portal” appendix.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-304">If you would like to learn more about how to configure these resources in the Azure portal, refer to the “Configuring tutorial resources in Azure portal” appendix.</span></span>

<span data-ttu-id="0e3b2-305">Download and save the supporting [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) folder and files.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-305">Download and save the supporting [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) folder and files.</span></span>

<span data-ttu-id="0e3b2-306">Open a **Microsoft Azure PowerShell** window *as an administrator*.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-306">Open a **Microsoft Azure PowerShell** window *as an administrator*.</span></span> <span data-ttu-id="0e3b2-307">If you do not yet have Azure PowerShell, follow the instructions in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install it.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-307">If you do not yet have Azure PowerShell, follow the instructions in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install it.</span></span>

<span data-ttu-id="0e3b2-308">Because Windows automatically blocks .ps1, .dll, and .exe files, you need to set the execution policy before you run the script.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-308">Because Windows automatically blocks .ps1, .dll, and .exe files, you need to set the execution policy before you run the script.</span></span> <span data-ttu-id="0e3b2-309">Make sure the Azure PowerShell window is running *as an administrator*.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-309">Make sure the Azure PowerShell window is running *as an administrator*.</span></span> <span data-ttu-id="0e3b2-310">Run **Set-ExecutionPolicy unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-310">Run **Set-ExecutionPolicy unrestricted**.</span></span> <span data-ttu-id="0e3b2-311">When prompted, type **Y**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-311">When prompted, type **Y**.</span></span>

![Screenshot of "Set-ExecutionPolicy unrestricted" running in Azure PowerShell window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

<span data-ttu-id="0e3b2-313">Run **Get-ExecutionPolicy** to make sure that the command worked.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-313">Run **Get-ExecutionPolicy** to make sure that the command worked.</span></span>

![Screenshot of "Get-ExecutionPolicy" running in Azure PowerShell window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

<span data-ttu-id="0e3b2-315">Go to the directory that has the scripts and generator application.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-315">Go to the directory that has the scripts and generator application.</span></span>

![Screenshot of "cd .\TollApp\TollApp" running in the Azure PowerShell window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

<span data-ttu-id="0e3b2-317">Type **.\\Setup.ps1** to set up your Azure account, create and configure all required resources, and start to generate events.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-317">Type **.\\Setup.ps1** to set up your Azure account, create and configure all required resources, and start to generate events.</span></span> <span data-ttu-id="0e3b2-318">The script randomly picks up a region to create your resources.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-318">The script randomly picks up a region to create your resources.</span></span> <span data-ttu-id="0e3b2-319">To explicitly specify a region, you can pass the **-location** parameter as in the following example:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-319">To explicitly specify a region, you can pass the **-location** parameter as in the following example:</span></span>

<span data-ttu-id="0e3b2-320">**.\\Setup.ps1 -location “Central US”**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-320">**.\\Setup.ps1 -location “Central US”**</span></span>

![Screenshot of the Azure sign-in page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

<span data-ttu-id="0e3b2-322">The script opens the **Sign In** page for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-322">The script opens the **Sign In** page for Microsoft Azure.</span></span> <span data-ttu-id="0e3b2-323">Enter your account credentials.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-323">Enter your account credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="0e3b2-324">If your account has access to multiple subscriptions, you will be asked to enter the subscription name that you want to use for the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-324">If your account has access to multiple subscriptions, you will be asked to enter the subscription name that you want to use for the tutorial.</span></span>
> 
> 

<span data-ttu-id="0e3b2-325">The script can take several minutes to run.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-325">The script can take several minutes to run.</span></span> <span data-ttu-id="0e3b2-326">After it finishes, the output should look like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-326">After it finishes, the output should look like the following screenshot.</span></span>

![Screenshot of output of the script in the Azure PowerShell window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

<span data-ttu-id="0e3b2-328">You will also see another window that's similar to the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-328">You will also see another window that's similar to the following screenshot.</span></span> <span data-ttu-id="0e3b2-329">This application is sending events to Azure Event Hubs, which is required to run the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-329">This application is sending events to Azure Event Hubs, which is required to run the tutorial.</span></span> <span data-ttu-id="0e3b2-330">So, do not stop the application or close this window until you finish the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-330">So, do not stop the application or close this window until you finish the tutorial.</span></span>

![Screenshot of "Sending event hub data"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

<span data-ttu-id="0e3b2-332">You should be able to see your resources in Azure portal now.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-332">You should be able to see your resources in Azure portal now.</span></span> <span data-ttu-id="0e3b2-333">Go to <https://portal.azure.com>, and sign in with your account credentials.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-333">Go to <https://portal.azure.com>, and sign in with your account credentials.</span></span> <span data-ttu-id="0e3b2-334">Note that currently some functionality utilizes the classic portal.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-334">Note that currently some functionality utilizes the classic portal.</span></span> <span data-ttu-id="0e3b2-335">These steps will be clearly indicated.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-335">These steps will be clearly indicated.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="0e3b2-336">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0e3b2-336">Azure Event Hubs</span></span>
<span data-ttu-id="0e3b2-337">In the Azure portal, click **More services** on the bottom of the left management pane.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-337">In the Azure portal, click **More services** on the bottom of the left management pane.</span></span> <span data-ttu-id="0e3b2-338">Type **Event hubs** in the field provided and click **Event hubs**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-338">Type **Event hubs** in the field provided and click **Event hubs**.</span></span> <span data-ttu-id="0e3b2-339">This launches a new browser window to display the **SERVICE BUS** area in the **classic portal**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-339">This launches a new browser window to display the **SERVICE BUS** area in the **classic portal**.</span></span> <span data-ttu-id="0e3b2-340">Here you can see the Event Hub created by the Setup.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-340">Here you can see the Event Hub created by the Setup.ps1 script.</span></span>

![Service Bus](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

<span data-ttu-id="0e3b2-342">Click the one that starts with *tolldata*.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-342">Click the one that starts with *tolldata*.</span></span> <span data-ttu-id="0e3b2-343">Click the **EVENT HUBS** tab. You will see two event hubs named *entry* and *exit* created in this namespace.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-343">Click the **EVENT HUBS** tab. You will see two event hubs named *entry* and *exit* created in this namespace.</span></span>

![Event Hubs tab in the classic portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a><span data-ttu-id="0e3b2-345">Azure Storage container</span><span class="sxs-lookup"><span data-stu-id="0e3b2-345">Azure Storage container</span></span>
1. <span data-ttu-id="0e3b2-346">Go back to the tab in your browser open to Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-346">Go back to the tab in your browser open to Azure portal.</span></span> <span data-ttu-id="0e3b2-347">Click **STORAGE** on the left side of the Azure portal to see the Azure Storage container that's used in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-347">Click **STORAGE** on the left side of the Azure portal to see the Azure Storage container that's used in the tutorial.</span></span>
   
    ![Storage menu item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. <span data-ttu-id="0e3b2-349">Click the one that start with *tolldata*.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-349">Click the one that start with *tolldata*.</span></span> <span data-ttu-id="0e3b2-350">Click the **CONTAINERS** tab to see the created container.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-350">Click the **CONTAINERS** tab to see the created container.</span></span>
   
    ![Containers tab in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. <span data-ttu-id="0e3b2-352">Click the **tolldata** container to see the uploaded JSON file that has vehicle registration data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-352">Click the **tolldata** container to see the uploaded JSON file that has vehicle registration data.</span></span>
   
    ![Screenshot of the registration.json file in the container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a><span data-ttu-id="0e3b2-354">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0e3b2-354">Azure SQL Database</span></span>
1. <span data-ttu-id="0e3b2-355">Go back to the Azure portal on the first tab that was opened in the browser.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-355">Go back to the Azure portal on the first tab that was opened in the browser.</span></span> <span data-ttu-id="0e3b2-356">Click **SQL DATABASES** on the left side of the Azure portal to see the SQL database that will be used in the tutorial and click **tolldatadb**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-356">Click **SQL DATABASES** on the left side of the Azure portal to see the SQL database that will be used in the tutorial and click **tolldatadb**.</span></span>
   
    ![Screenshot of the created SQL database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. <span data-ttu-id="0e3b2-358">Copy the server name without the port number (*servername*.database.windows.net, for example).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-358">Copy the server name without the port number (*servername*.database.windows.net, for example).</span></span>
    <span data-ttu-id="0e3b2-359">![Screenshot of the created SQL database db](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)</span><span class="sxs-lookup"><span data-stu-id="0e3b2-359">![Screenshot of the created SQL database db](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)</span></span>

## <a name="connect-to-the-database-from-visual-studio"></a><span data-ttu-id="0e3b2-360">Connect to the database from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e3b2-360">Connect to the database from Visual Studio</span></span>
<span data-ttu-id="0e3b2-361">Use Visual Studio to access query results in the output database.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-361">Use Visual Studio to access query results in the output database.</span></span>

<span data-ttu-id="0e3b2-362">Connect to the SQL database (the destination) from Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-362">Connect to the SQL database (the destination) from Visual Studio:</span></span>

1. <span data-ttu-id="0e3b2-363">Open Visual Studio, and then click **Tools** > **Connect to Database**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-363">Open Visual Studio, and then click **Tools** > **Connect to Database**.</span></span>
2. <span data-ttu-id="0e3b2-364">If asked, click **Microsoft SQL Server** as a data source.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-364">If asked, click **Microsoft SQL Server** as a data source.</span></span>
   
    ![Change Data Source dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. <span data-ttu-id="0e3b2-366">In the **Server name** field, paste the name that you copied in the previous section from the Azure portal (that is, *servername*.database.windows.net).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-366">In the **Server name** field, paste the name that you copied in the previous section from the Azure portal (that is, *servername*.database.windows.net).</span></span>
4. <span data-ttu-id="0e3b2-367">Click **Use SQL Server Authentication**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-367">Click **Use SQL Server Authentication**.</span></span>
5. <span data-ttu-id="0e3b2-368">Enter **tolladmin** in the **User name** field and **123toll!**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-368">Enter **tolladmin** in the **User name** field and **123toll!**</span></span> <span data-ttu-id="0e3b2-369">in the **Password** field.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-369">in the **Password** field.</span></span>
6. <span data-ttu-id="0e3b2-370">Click **Select or enter a database name**, and select **TollDataDB** as the database.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-370">Click **Select or enter a database name**, and select **TollDataDB** as the database.</span></span>
   
    ![Add Connection dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. <span data-ttu-id="0e3b2-372">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-372">Click **OK**.</span></span>
8. <span data-ttu-id="0e3b2-373">Open Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-373">Open Server Explorer.</span></span>
   
    ![Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. <span data-ttu-id="0e3b2-375">See four tables in the TollDataDB database.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-375">See four tables in the TollDataDB database.</span></span>
   
    ![Tables in the TollDataDB database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a><span data-ttu-id="0e3b2-377">Event generator: TollApp sample project</span><span class="sxs-lookup"><span data-stu-id="0e3b2-377">Event generator: TollApp sample project</span></span>
<span data-ttu-id="0e3b2-378">The PowerShell script automatically starts to send events by using the TollApp sample application program.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-378">The PowerShell script automatically starts to send events by using the TollApp sample application program.</span></span> <span data-ttu-id="0e3b2-379">You don’t need to perform any additional steps.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-379">You don’t need to perform any additional steps.</span></span>

<span data-ttu-id="0e3b2-380">However, if you are interested in implementation details, you can find the source code of the TollApp application in GitHub [samples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-380">However, if you are interested in implementation details, you can find the source code of the TollApp application in GitHub [samples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).</span></span>

![Screenshot of sample code displayed in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="0e3b2-382">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="0e3b2-382">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="0e3b2-383">In the Azure portal, click the green plus sign in the top-left corner of the page to create a new Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-383">In the Azure portal, click the green plus sign in the top-left corner of the page to create a new Stream Analytics job.</span></span> <span data-ttu-id="0e3b2-384">Select **Intelligence + Analytics** and then click **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-384">Select **Intelligence + Analytics** and then click **Stream Analytics job**.</span></span>
   
    ![New button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. <span data-ttu-id="0e3b2-386">Provide a job name, validate the subscription is correct and then create a new Resource group in the same region as the Event hub storage (default is South Central US for the script).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-386">Provide a job name, validate the subscription is correct and then create a new Resource group in the same region as the Event hub storage (default is South Central US for the script).</span></span>
3. <span data-ttu-id="0e3b2-387">Click **Pin to dashboard** and then **CREATE** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-387">Click **Pin to dashboard** and then **CREATE** at the bottom of the page.</span></span>
   
    ![Create Stream Analytics Job option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a><span data-ttu-id="0e3b2-389">Define input sources</span><span class="sxs-lookup"><span data-stu-id="0e3b2-389">Define input sources</span></span>
1. <span data-ttu-id="0e3b2-390">The job will create and open the job page.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-390">The job will create and open the job page.</span></span> <span data-ttu-id="0e3b2-391">Or you can click the created analytics job on the portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-391">Or you can click the created analytics job on the portal dashboard.</span></span>

2. <span data-ttu-id="0e3b2-392">Click the **INPUTS** tab to define the source data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-392">Click the **INPUTS** tab to define the source data.</span></span>
   
    ![The Inputs tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. <span data-ttu-id="0e3b2-394">Click **ADD AN INPUT**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-394">Click **ADD AN INPUT**.</span></span>
   
    ![The Add an Input option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. <span data-ttu-id="0e3b2-396">Enter **EntryStream** as **INPUT ALIAS**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-396">Enter **EntryStream** as **INPUT ALIAS**.</span></span>
5. <span data-ttu-id="0e3b2-397">Source Type is **Data Stream**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-397">Source Type is **Data Stream**</span></span>
6. <span data-ttu-id="0e3b2-398">Source is **Event hub**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-398">Source is **Event hub**.</span></span>
7. <span data-ttu-id="0e3b2-399">**Service bus namespace** should be the TollData one in the drop down.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-399">**Service bus namespace** should be the TollData one in the drop down.</span></span>
8. <span data-ttu-id="0e3b2-400">**Event hub name** should be set to **entry**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-400">**Event hub name** should be set to **entry**.</span></span>
9. <span data-ttu-id="0e3b2-401">\**Event hub policy name*is **RootManageSharedAccessKey**  (the default value).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-401">\**Event hub policy name*is **RootManageSharedAccessKey**  (the default value).</span></span>
10. <span data-ttu-id="0e3b2-402">Select **JSON** for **EVENT SERIALIZATION FORMAT** and **UTF8** for **ENCODING**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-402">Select **JSON** for **EVENT SERIALIZATION FORMAT** and **UTF8** for **ENCODING**.</span></span>
   
    <span data-ttu-id="0e3b2-403">Your settings will look like:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-403">Your settings will look like:</span></span>
   
    ![Event hub settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. <span data-ttu-id="0e3b2-405">Click **Create** at the bottom of the page to finish the wizard.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-405">Click **Create** at the bottom of the page to finish the wizard.</span></span>
    
    <span data-ttu-id="0e3b2-406">Now that you've created the entry stream, you will follow the same steps to create the exit stream.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-406">Now that you've created the entry stream, you will follow the same steps to create the exit stream.</span></span> <span data-ttu-id="0e3b2-407">Be sure to enter values as on the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-407">Be sure to enter values as on the following screenshot.</span></span>
    
    ![Settings for the exit stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    <span data-ttu-id="0e3b2-409">You have defined two input streams:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-409">You have defined two input streams:</span></span>
    
    ![Defined input streams in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    <span data-ttu-id="0e3b2-411">Next, you will add reference data input for the blob file that contains car registration data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-411">Next, you will add reference data input for the blob file that contains car registration data.</span></span>
11. <span data-ttu-id="0e3b2-412">Click **ADD**, and then follow the same process for the stream inputs but select **REFERENCE DATA** instead of **Data Stream** and the **Input Alias** is **Registration**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-412">Click **ADD**, and then follow the same process for the stream inputs but select **REFERENCE DATA** instead of **Data Stream** and the **Input Alias** is **Registration**.</span></span>

12. <span data-ttu-id="0e3b2-413">storage account that starts with **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-413">storage account that starts with **tolldata**.</span></span> <span data-ttu-id="0e3b2-414">The container name should be **tolldata**, and the **PATH PATTERN** should be **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-414">The container name should be **tolldata**, and the **PATH PATTERN** should be **registration.json**.</span></span> <span data-ttu-id="0e3b2-415">This file name is case sensitive and should be **lowercase**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-415">This file name is case sensitive and should be **lowercase**.</span></span>
    
    ![Blog storage settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. <span data-ttu-id="0e3b2-417">Click **Create** to finish the wizard.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-417">Click **Create** to finish the wizard.</span></span>

<span data-ttu-id="0e3b2-418">Now all inputs are defined.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-418">Now all inputs are defined.</span></span>

## <a name="define-output"></a><span data-ttu-id="0e3b2-419">Define output</span><span class="sxs-lookup"><span data-stu-id="0e3b2-419">Define output</span></span>
1. <span data-ttu-id="0e3b2-420">On the Stream Analytics job overview pane, select **OUTPUTS**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-420">On the Stream Analytics job overview pane, select **OUTPUTS**.</span></span>
   
    ![The Output tab and "Add an output" option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. <span data-ttu-id="0e3b2-422">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-422">Click **Add**.</span></span>
3. <span data-ttu-id="0e3b2-423">Set the **Output alias** to 'output' and then **Sink** to **SQL database**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-423">Set the **Output alias** to 'output' and then **Sink** to **SQL database**.</span></span>
3. <span data-ttu-id="0e3b2-424">Select the server name that was used in the “Connect to Database from Visual Studio” section of the article.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-424">Select the server name that was used in the “Connect to Database from Visual Studio” section of the article.</span></span> <span data-ttu-id="0e3b2-425">The database name is **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-425">The database name is **TollDataDB**.</span></span>
4. <span data-ttu-id="0e3b2-426">Enter **tolladmin** in the **USERNAME** field, **123toll!**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-426">Enter **tolladmin** in the **USERNAME** field, **123toll!**</span></span> <span data-ttu-id="0e3b2-427">in the **PASSWORD** field, and **TollDataRefJoin** in the **TABLE** field.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-427">in the **PASSWORD** field, and **TollDataRefJoin** in the **TABLE** field.</span></span>
   
    ![SQL Database settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. <span data-ttu-id="0e3b2-429">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-429">Click **Create**.</span></span>

## <a name="azure-stream-analytics-query"></a><span data-ttu-id="0e3b2-430">Azure Stream analytics query</span><span class="sxs-lookup"><span data-stu-id="0e3b2-430">Azure Stream analytics query</span></span>
<span data-ttu-id="0e3b2-431">The **QUERY** tab contains a SQL query that transforms the incoming data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-431">The **QUERY** tab contains a SQL query that transforms the incoming data.</span></span>

![A query added to the Query tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

<span data-ttu-id="0e3b2-433">This tutorial attempts to answer several business questions that are related to toll data and constructs Stream Analytics queries that can be used in Azure Stream Analytics to provide a relevant answer.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-433">This tutorial attempts to answer several business questions that are related to toll data and constructs Stream Analytics queries that can be used in Azure Stream Analytics to provide a relevant answer.</span></span>

<span data-ttu-id="0e3b2-434">Before you start your first Stream Analytics job, let’s explore a few scenarios and the query syntax.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-434">Before you start your first Stream Analytics job, let’s explore a few scenarios and the query syntax.</span></span>

## <a name="introduction-to-azure-stream-analytics-query-language"></a><span data-ttu-id="0e3b2-435">Introduction to Azure Stream Analytics query language</span><span class="sxs-lookup"><span data-stu-id="0e3b2-435">Introduction to Azure Stream Analytics query language</span></span>
- - -
<span data-ttu-id="0e3b2-436">Let’s say that you need to count the number of vehicles that enter a toll booth.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-436">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="0e3b2-437">Because this is a continuous stream of events, you have to define a “period of time.”</span><span class="sxs-lookup"><span data-stu-id="0e3b2-437">Because this is a continuous stream of events, you have to define a “period of time.”</span></span> <span data-ttu-id="0e3b2-438">Let's modify the question to be “How many vehicles enter a toll booth every three minutes?”.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-438">Let's modify the question to be “How many vehicles enter a toll booth every three minutes?”.</span></span> <span data-ttu-id="0e3b2-439">This is commonly referred to as the tumbling count.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-439">This is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="0e3b2-440">Let’s look at the Azure Stream Analytics query that answers this question:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-440">Let’s look at the Azure Stream Analytics query that answers this question:</span></span>

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

<span data-ttu-id="0e3b2-441">As you can see, Azure Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-441">As you can see, Azure Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="0e3b2-442">For more details, read about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-442">For more details, read about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

## <a name="testing-azure-stream-analytics-queries"></a><span data-ttu-id="0e3b2-443">Testing Azure Stream Analytics queries</span><span class="sxs-lookup"><span data-stu-id="0e3b2-443">Testing Azure Stream Analytics queries</span></span>
<span data-ttu-id="0e3b2-444">Now that you have written your first Azure Stream Analytics query, it is time to test it by using sample data files located in your TollApp folder in the following path:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-444">Now that you have written your first Azure Stream Analytics query, it is time to test it by using sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="0e3b2-445">**..\\TollApp\\TollApp\\Data**</span><span class="sxs-lookup"><span data-stu-id="0e3b2-445">**..\\TollApp\\TollApp\\Data**</span></span>

<span data-ttu-id="0e3b2-446">This folder contains the following files:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-446">This folder contains the following files:</span></span>

* <span data-ttu-id="0e3b2-447">Entry.json</span><span class="sxs-lookup"><span data-stu-id="0e3b2-447">Entry.json</span></span>
* <span data-ttu-id="0e3b2-448">Exit.json</span><span class="sxs-lookup"><span data-stu-id="0e3b2-448">Exit.json</span></span>
* <span data-ttu-id="0e3b2-449">Registration.json</span><span class="sxs-lookup"><span data-stu-id="0e3b2-449">Registration.json</span></span>

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="0e3b2-450">Question 1: Number of vehicles entering a toll booth</span><span class="sxs-lookup"><span data-stu-id="0e3b2-450">Question 1: Number of vehicles entering a toll booth</span></span>
1. <span data-ttu-id="0e3b2-451">Open the Azure portal and go to your created Azure Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-451">Open the Azure portal and go to your created Azure Stream Analytics job.</span></span> <span data-ttu-id="0e3b2-452">Click the **QUERY** tab and paste query from the previous section.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-452">Click the **QUERY** tab and paste query from the previous section.</span></span>

2. <span data-ttu-id="0e3b2-453">To validate this query against sample data, upload the data into the EntryStream input by clicking the ... symbol and selecting **Upload sample data from file**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-453">To validate this query against sample data, upload the data into the EntryStream input by clicking the ... symbol and selecting **Upload sample data from file**.</span></span>

    ![Screenshot of the Entry.json file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. <span data-ttu-id="0e3b2-455">In the pane that appears select the file (Entry.json) on your local machine and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-455">In the pane that appears select the file (Entry.json) on your local machine and click **OK**.</span></span> <span data-ttu-id="0e3b2-456">The **Test** icon will now illuminate and be clickable.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-456">The **Test** icon will now illuminate and be clickable.</span></span>
   
    ![Screenshot of the Entry.json file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. <span data-ttu-id="0e3b2-458">Validate that the output of the query is as expected:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-458">Validate that the output of the query is as expected:</span></span>
   
    ![Results of the test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-to-pass-through-the-toll-booth"></a><span data-ttu-id="0e3b2-460">Question 2: Report total time for each car to pass through the toll booth</span><span class="sxs-lookup"><span data-stu-id="0e3b2-460">Question 2: Report total time for each car to pass through the toll booth</span></span>
<span data-ttu-id="0e3b2-461">The average time that's required for a car to pass through the toll helps to assess the efficiency of the process and the customer experience.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-461">The average time that's required for a car to pass through the toll helps to assess the efficiency of the process and the customer experience.</span></span>

<span data-ttu-id="0e3b2-462">To find the total time, you need to join the EntryTime stream with the ExitTime stream.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-462">To find the total time, you need to join the EntryTime stream with the ExitTime stream.</span></span> <span data-ttu-id="0e3b2-463">You will join the streams on TollId and LicencePlate columns.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-463">You will join the streams on TollId and LicencePlate columns.</span></span> <span data-ttu-id="0e3b2-464">The **JOIN** operator requires you to specify temporal leeway that describes the acceptable time difference between the joined events.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-464">The **JOIN** operator requires you to specify temporal leeway that describes the acceptable time difference between the joined events.</span></span> <span data-ttu-id="0e3b2-465">You will use **DATEDIFF** function to specify that events should be no more than 15 minutes from each other.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-465">You will use **DATEDIFF** function to specify that events should be no more than 15 minutes from each other.</span></span> <span data-ttu-id="0e3b2-466">You will also apply the **DATEDIFF** function to exit and entry times to compute the actual time that a car spends in the toll station.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-466">You will also apply the **DATEDIFF** function to exit and entry times to compute the actual time that a car spends in the toll station.</span></span> <span data-ttu-id="0e3b2-467">Note the difference of the use of **DATEDIFF** when it's used in a **SELECT** statement rather than a **JOIN** condition.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-467">Note the difference of the use of **DATEDIFF** when it's used in a **SELECT** statement rather than a **JOIN** condition.</span></span>

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. <span data-ttu-id="0e3b2-468">To test this query, update the query on the **QUERY** for the job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-468">To test this query, update the query on the **QUERY** for the job.</span></span> <span data-ttu-id="0e3b2-469">Add the test file for **ExitStream** just like **EntryStream** was entered above.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-469">Add the test file for **ExitStream** just like **EntryStream** was entered above.</span></span>
   
2. <span data-ttu-id="0e3b2-470">Click **Test**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-470">Click **Test**.</span></span>

3. <span data-ttu-id="0e3b2-471">Select the check box to test the query and view the output:</span><span class="sxs-lookup"><span data-stu-id="0e3b2-471">Select the check box to test the query and view the output:</span></span>
   
    ![Output of the test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a><span data-ttu-id="0e3b2-473">Question 3: Report all commercial vehicles with expired registration</span><span class="sxs-lookup"><span data-stu-id="0e3b2-473">Question 3: Report all commercial vehicles with expired registration</span></span>
<span data-ttu-id="0e3b2-474">Azure Stream Analytics can use static snapshots of data to join with temporal data streams.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-474">Azure Stream Analytics can use static snapshots of data to join with temporal data streams.</span></span> <span data-ttu-id="0e3b2-475">To demonstrate this capability, use the following sample question.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-475">To demonstrate this capability, use the following sample question.</span></span>

<span data-ttu-id="0e3b2-476">If a commercial vehicle is registered with the toll company, it can pass through the toll booth without being stopped for inspection.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-476">If a commercial vehicle is registered with the toll company, it can pass through the toll booth without being stopped for inspection.</span></span> <span data-ttu-id="0e3b2-477">You will use Commercial Vehicle Registration lookup table to identify all commercial vehicles that have expired registrations.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-477">You will use Commercial Vehicle Registration lookup table to identify all commercial vehicles that have expired registrations.</span></span>

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

<span data-ttu-id="0e3b2-478">To test a query by using reference data, you need to define an input source for the reference data, which you have done already.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-478">To test a query by using reference data, you need to define an input source for the reference data, which you have done already.</span></span>

<span data-ttu-id="0e3b2-479">To test this query, paste the query into the **QUERY** tab, click **Test**, and specify the two input sources and the registration sample data and click **Test**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-479">To test this query, paste the query into the **QUERY** tab, click **Test**, and specify the two input sources and the registration sample data and click **Test**.</span></span>  
   
![Output of the test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="0e3b2-481">Start the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="0e3b2-481">Start the Stream Analytics job</span></span>
<span data-ttu-id="0e3b2-482">Now it's time to finish the configuration and start the job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-482">Now it's time to finish the configuration and start the job.</span></span> <span data-ttu-id="0e3b2-483">Save the query from Question 3, which will produce output that matches the schema of the **TollDataRefJoin** output table.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-483">Save the query from Question 3, which will produce output that matches the schema of the **TollDataRefJoin** output table.</span></span>

<span data-ttu-id="0e3b2-484">Go to the job **DASHBOARD**, and click **START**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-484">Go to the job **DASHBOARD**, and click **START**.</span></span>

![Screenshot of the Start button in the job dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

<span data-ttu-id="0e3b2-486">In the dialog box that opens, change the **START OUTPUT** time to **CUSTOM TIME**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-486">In the dialog box that opens, change the **START OUTPUT** time to **CUSTOM TIME**.</span></span> <span data-ttu-id="0e3b2-487">Change the hour to one hour before the current time.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-487">Change the hour to one hour before the current time.</span></span> <span data-ttu-id="0e3b2-488">This change ensures that all events from the event hub are processed since you started to generate the events at the beginning of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-488">This change ensures that all events from the event hub are processed since you started to generate the events at the beginning of the tutorial.</span></span> <span data-ttu-id="0e3b2-489">Now click the **Start** button to start the job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-489">Now click the **Start** button to start the job.</span></span>

![Selection of custom time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

<span data-ttu-id="0e3b2-491">Starting the job can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-491">Starting the job can take a few minutes.</span></span> <span data-ttu-id="0e3b2-492">You can see the status on the top-level page for Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-492">You can see the status on the top-level page for Stream Analytics.</span></span>

![Screenshot of the status of the job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a><span data-ttu-id="0e3b2-494">Check results in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e3b2-494">Check results in Visual Studio</span></span>
1. <span data-ttu-id="0e3b2-495">Open Visual Studio Server Explorer, and right-click the **TollDataRefJoin** table.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-495">Open Visual Studio Server Explorer, and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="0e3b2-496">Click **Show Table Data** to see the output of your job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-496">Click **Show Table Data** to see the output of your job.</span></span>
   
    ![Selection of "Show Table Data" in Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a><span data-ttu-id="0e3b2-498">Scale out Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="0e3b2-498">Scale out Azure Stream Analytics jobs</span></span>
<span data-ttu-id="0e3b2-499">Azure Stream Analytics is designed to elastically scale so that it can handle a lot of data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-499">Azure Stream Analytics is designed to elastically scale so that it can handle a lot of data.</span></span> <span data-ttu-id="0e3b2-500">The Azure Stream Analytics query can use a **PARTITION BY** clause to tell the system that this step will scale out. **PartitionId** is a special column that the system adds to match the partition ID of the input (event hub).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-500">The Azure Stream Analytics query can use a **PARTITION BY** clause to tell the system that this step will scale out. **PartitionId** is a special column that the system adds to match the partition ID of the input (event hub).</span></span>

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. <span data-ttu-id="0e3b2-501">Stop the current job, update the query in the **QUERY** tab, and open the **Settings** gear in the job dashboard.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-501">Stop the current job, update the query in the **QUERY** tab, and open the **Settings** gear in the job dashboard.</span></span> <span data-ttu-id="0e3b2-502">Click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-502">Click **Scale**.</span></span>
   
    <span data-ttu-id="0e3b2-503">**STREAMING UNITS** define the amount of compute power that the job can receive.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-503">**STREAMING UNITS** define the amount of compute power that the job can receive.</span></span>
2. <span data-ttu-id="0e3b2-504">Change the drop down from 1 from 6.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-504">Change the drop down from 1 from 6.</span></span>
   
    ![Screenshot of selecting 6 streaming units](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. <span data-ttu-id="0e3b2-506">Go to the **OUTPUTS** tab and change the name of the SQL table to **TollDataTumblingCountPartitioned**.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-506">Go to the **OUTPUTS** tab and change the name of the SQL table to **TollDataTumblingCountPartitioned**.</span></span>

<span data-ttu-id="0e3b2-507">If you start the job now, Azure Stream Analytics can distribute work across more compute resources and achieve better throughput.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-507">If you start the job now, Azure Stream Analytics can distribute work across more compute resources and achieve better throughput.</span></span> <span data-ttu-id="0e3b2-508">Please note that the TollApp application is also sending events partitioned by TollId.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-508">Please note that the TollApp application is also sending events partitioned by TollId.</span></span>

## <a name="monitor"></a><span data-ttu-id="0e3b2-509">Monitor</span><span class="sxs-lookup"><span data-stu-id="0e3b2-509">Monitor</span></span>
<span data-ttu-id="0e3b2-510">The **MONITOR** area contains statistics about the running job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-510">The **MONITOR** area contains statistics about the running job.</span></span> <span data-ttu-id="0e3b2-511">First time configuration is needed to use the storage account in the same region (name toll like the rest of this document).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-511">First time configuration is needed to use the storage account in the same region (name toll like the rest of this document).</span></span>   

![Screenshot of monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

<span data-ttu-id="0e3b2-513">You can access **Activity Logs** from the job dashboard **Settings** area as well.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-513">You can access **Activity Logs** from the job dashboard **Settings** area as well.</span></span>


## <a name="conclusion"></a><span data-ttu-id="0e3b2-514">Conclusion</span><span class="sxs-lookup"><span data-stu-id="0e3b2-514">Conclusion</span></span>
<span data-ttu-id="0e3b2-515">This tutorial introduced you to the Azure Stream Analytics service.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-515">This tutorial introduced you to the Azure Stream Analytics service.</span></span> <span data-ttu-id="0e3b2-516">It demonstrated how to configure inputs and outputs for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-516">It demonstrated how to configure inputs and outputs for the Stream Analytics job.</span></span> <span data-ttu-id="0e3b2-517">Using the Toll Data scenario, the tutorial explained common types of problems that arise in the space of data in motion and how they can be solved with simple SQL-like queries in Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-517">Using the Toll Data scenario, the tutorial explained common types of problems that arise in the space of data in motion and how they can be solved with simple SQL-like queries in Azure Stream Analytics.</span></span> <span data-ttu-id="0e3b2-518">The tutorial described SQL extension constructs for working with temporal data.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-518">The tutorial described SQL extension constructs for working with temporal data.</span></span> <span data-ttu-id="0e3b2-519">It showed how to join data streams, how to enrich the data stream with static reference data, and how to scale out a query to achieve higher throughput.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-519">It showed how to join data streams, how to enrich the data stream with static reference data, and how to scale out a query to achieve higher throughput.</span></span>

<span data-ttu-id="0e3b2-520">Although this tutorial provides a good introduction, it is not complete by any means.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-520">Although this tutorial provides a good introduction, it is not complete by any means.</span></span> <span data-ttu-id="0e3b2-521">You can find more query patterns using the SAQL language at [Query examples for common Stream Analytics usage patterns](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="0e3b2-521">You can find more query patterns using the SAQL language at [Query examples for common Stream Analytics usage patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>
<span data-ttu-id="0e3b2-522">Refer to the [online documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) to learn more about Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-522">Refer to the [online documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) to learn more about Azure Stream Analytics.</span></span>

## <a name="clean-up-your-azure-account"></a><span data-ttu-id="0e3b2-523">Clean up your Azure account</span><span class="sxs-lookup"><span data-stu-id="0e3b2-523">Clean up your Azure account</span></span>
1. <span data-ttu-id="0e3b2-524">Stop the Stream Analytics job in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-524">Stop the Stream Analytics job in the Azure portal.</span></span>
   
    <span data-ttu-id="0e3b2-525">The Setup.ps1 script creates two event hubs and a SQL database.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-525">The Setup.ps1 script creates two event hubs and a SQL database.</span></span> <span data-ttu-id="0e3b2-526">The following instructions help you clean up resources at the end of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-526">The following instructions help you clean up resources at the end of the tutorial.</span></span>
2. <span data-ttu-id="0e3b2-527">In a PowerShell window, type **.\\Cleanup.ps1** to start the script that deletes resources used in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-527">In a PowerShell window, type **.\\Cleanup.ps1** to start the script that deletes resources used in the tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0e3b2-528">Resources are identified by the name.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-528">Resources are identified by the name.</span></span> <span data-ttu-id="0e3b2-529">Make sure you carefully review each item before confirming removal.</span><span class="sxs-lookup"><span data-stu-id="0e3b2-529">Make sure you carefully review each item before confirming removal.</span></span>
   > 
   > 











































