---
title: Deep dive into how to predict vehicle health and driving habits - Azure | Microsoft Docs
description: Use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2018
ms.author: deguhath
ms.openlocfilehash: 991e4b86a1d3e75c02e5ed8fe97727c625f174a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868050"
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="87ce5-103">Vehicle Telemetry Analytics Solution playbook: Deep dive into the solution</span><span class="sxs-lookup"><span data-stu-id="87ce5-103">Vehicle Telemetry Analytics Solution playbook: Deep dive into the solution</span></span>
<span data-ttu-id="87ce5-104">This menu links to the sections of this playbook:</span><span class="sxs-lookup"><span data-stu-id="87ce5-104">This menu links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="87ce5-105">This document drills down into each of the stages depicted in the solution architecture.</span><span class="sxs-lookup"><span data-stu-id="87ce5-105">This document drills down into each of the stages depicted in the solution architecture.</span></span> <span data-ttu-id="87ce5-106">Instructions and pointers for customization are included.</span><span class="sxs-lookup"><span data-stu-id="87ce5-106">Instructions and pointers for customization are included.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="87ce5-107">Data sources</span><span class="sxs-lookup"><span data-stu-id="87ce5-107">Data sources</span></span>
<span data-ttu-id="87ce5-108">The solution uses two different data sources:</span><span class="sxs-lookup"><span data-stu-id="87ce5-108">The solution uses two different data sources:</span></span>

* <span data-ttu-id="87ce5-109">Simulated vehicle signals and diagnostic data set</span><span class="sxs-lookup"><span data-stu-id="87ce5-109">Simulated vehicle signals and diagnostic data set</span></span>
* <span data-ttu-id="87ce5-110">Vehicle catalog</span><span class="sxs-lookup"><span data-stu-id="87ce5-110">Vehicle catalog</span></span>

<span data-ttu-id="87ce5-111">A vehicle telematics simulator is included as part of this solution, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="87ce5-111">A vehicle telematics simulator is included as part of this solution, as shown in the following screenshot.</span></span> <span data-ttu-id="87ce5-112">It emits diagnostic information and signals that correspond to the state of the vehicle and to the driving pattern at a given point in time.</span><span class="sxs-lookup"><span data-stu-id="87ce5-112">It emits diagnostic information and signals that correspond to the state of the vehicle and to the driving pattern at a given point in time.</span></span>  <span data-ttu-id="87ce5-113">The vehicle catalog contains a reference data set that maps vehicle identification numbers (VINs) to models.</span><span class="sxs-lookup"><span data-stu-id="87ce5-113">The vehicle catalog contains a reference data set that maps vehicle identification numbers (VINs) to models.</span></span> <span data-ttu-id="87ce5-114">Note: The Vehicle Telematics Simulator Visual Studio Solution data set is no longer available.</span><span class="sxs-lookup"><span data-stu-id="87ce5-114">Note: The Vehicle Telematics Simulator Visual Studio Solution data set is no longer available.</span></span> 

![Vehicle telematics simulator](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)


<span data-ttu-id="87ce5-116">This JSON-formatted data set contains the following schema.</span><span class="sxs-lookup"><span data-stu-id="87ce5-116">This JSON-formatted data set contains the following schema.</span></span>

| <span data-ttu-id="87ce5-117">Column</span><span class="sxs-lookup"><span data-stu-id="87ce5-117">Column</span></span> | <span data-ttu-id="87ce5-118">Description</span><span class="sxs-lookup"><span data-stu-id="87ce5-118">Description</span></span> | <span data-ttu-id="87ce5-119">Values</span><span class="sxs-lookup"><span data-stu-id="87ce5-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87ce5-120">VIN</span><span class="sxs-lookup"><span data-stu-id="87ce5-120">VIN</span></span> |<span data-ttu-id="87ce5-121">Randomly generated VIN</span><span class="sxs-lookup"><span data-stu-id="87ce5-121">Randomly generated VIN</span></span> |<span data-ttu-id="87ce5-122">Obtained from a master list of 10,000 randomly generated VINs</span><span class="sxs-lookup"><span data-stu-id="87ce5-122">Obtained from a master list of 10,000 randomly generated VINs</span></span> |
| <span data-ttu-id="87ce5-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="87ce5-123">Outside temperature</span></span> |<span data-ttu-id="87ce5-124">The outside temperature where the vehicle is driving</span><span class="sxs-lookup"><span data-stu-id="87ce5-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="87ce5-125">Randomly generated number from 0 to 100</span><span class="sxs-lookup"><span data-stu-id="87ce5-125">Randomly generated number from 0 to 100</span></span> |
| <span data-ttu-id="87ce5-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="87ce5-126">Engine temperature</span></span> |<span data-ttu-id="87ce5-127">The engine temperature of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="87ce5-128">Randomly generated number from 0 to 500</span><span class="sxs-lookup"><span data-stu-id="87ce5-128">Randomly generated number from 0 to 500</span></span> |
| <span data-ttu-id="87ce5-129">Speed</span><span class="sxs-lookup"><span data-stu-id="87ce5-129">Speed</span></span> |<span data-ttu-id="87ce5-130">The engine speed at which the vehicle is driving</span><span class="sxs-lookup"><span data-stu-id="87ce5-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="87ce5-131">Randomly generated number from 0 to 100</span><span class="sxs-lookup"><span data-stu-id="87ce5-131">Randomly generated number from 0 to 100</span></span> |
| <span data-ttu-id="87ce5-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="87ce5-132">Fuel</span></span> |<span data-ttu-id="87ce5-133">The fuel level of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="87ce5-134">Randomly generated number from 0 to 100 (indicates fuel level percentage)</span><span class="sxs-lookup"><span data-stu-id="87ce5-134">Randomly generated number from 0 to 100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="87ce5-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="87ce5-135">EngineOil</span></span> |<span data-ttu-id="87ce5-136">The engine oil level of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="87ce5-137">Randomly generated number from 0 to 100 (indicates engine oil level percentage)</span><span class="sxs-lookup"><span data-stu-id="87ce5-137">Randomly generated number from 0 to 100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="87ce5-138">Tire pressure</span><span class="sxs-lookup"><span data-stu-id="87ce5-138">Tire pressure</span></span> |<span data-ttu-id="87ce5-139">The tire pressure of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="87ce5-140">Randomly generated number from 0 to 50 (indicates tire pressure level percentage)</span><span class="sxs-lookup"><span data-stu-id="87ce5-140">Randomly generated number from 0 to 50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="87ce5-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="87ce5-141">Odometer</span></span> |<span data-ttu-id="87ce5-142">The odometer reading of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="87ce5-143">Randomly generated number from 0 to 200,000</span><span class="sxs-lookup"><span data-stu-id="87ce5-143">Randomly generated number from 0 to 200,000</span></span> |
| <span data-ttu-id="87ce5-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="87ce5-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="87ce5-145">The accelerator pedal position of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="87ce5-146">Randomly generated number from 0 to 100 (indicates accelerator level percentage)</span><span class="sxs-lookup"><span data-stu-id="87ce5-146">Randomly generated number from 0 to 100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="87ce5-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="87ce5-147">Parking_brake_status</span></span> |<span data-ttu-id="87ce5-148">Indicates whether the vehicle is parked or not</span><span class="sxs-lookup"><span data-stu-id="87ce5-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="87ce5-149">True or False</span><span class="sxs-lookup"><span data-stu-id="87ce5-149">True or False</span></span> |
| <span data-ttu-id="87ce5-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="87ce5-150">Headlamp_status</span></span> |<span data-ttu-id="87ce5-151">Indicates whether the headlamp is on or not</span><span class="sxs-lookup"><span data-stu-id="87ce5-151">Indicates whether the headlamp is on or not</span></span> |<span data-ttu-id="87ce5-152">True or False</span><span class="sxs-lookup"><span data-stu-id="87ce5-152">True or False</span></span> |
| <span data-ttu-id="87ce5-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="87ce5-153">Brake_pedal_status</span></span> |<span data-ttu-id="87ce5-154">Indicates whether the brake pedal is pressed or not</span><span class="sxs-lookup"><span data-stu-id="87ce5-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="87ce5-155">True or False</span><span class="sxs-lookup"><span data-stu-id="87ce5-155">True or False</span></span> |
| <span data-ttu-id="87ce5-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="87ce5-156">Transmission_gear_position</span></span> |<span data-ttu-id="87ce5-157">The transmission gear position of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="87ce5-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span><span class="sxs-lookup"><span data-stu-id="87ce5-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="87ce5-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="87ce5-159">Ignition_status</span></span> |<span data-ttu-id="87ce5-160">Indicates whether the vehicle is running or stopped</span><span class="sxs-lookup"><span data-stu-id="87ce5-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="87ce5-161">True or False</span><span class="sxs-lookup"><span data-stu-id="87ce5-161">True or False</span></span> |
| <span data-ttu-id="87ce5-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="87ce5-162">Windshield_wiper_status</span></span> |<span data-ttu-id="87ce5-163">Indicates whether the windshield wiper is turned on or not</span><span class="sxs-lookup"><span data-stu-id="87ce5-163">Indicates whether the windshield wiper is turned on or not</span></span> |<span data-ttu-id="87ce5-164">True or False</span><span class="sxs-lookup"><span data-stu-id="87ce5-164">True or False</span></span> |
| <span data-ttu-id="87ce5-165">ABS</span><span class="sxs-lookup"><span data-stu-id="87ce5-165">ABS</span></span> |<span data-ttu-id="87ce5-166">Indicates whether ABS is engaged or not</span><span class="sxs-lookup"><span data-stu-id="87ce5-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="87ce5-167">True or False</span><span class="sxs-lookup"><span data-stu-id="87ce5-167">True or False</span></span> |
| <span data-ttu-id="87ce5-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="87ce5-168">Timestamp</span></span> |<span data-ttu-id="87ce5-169">The time stamp when the data point is created</span><span class="sxs-lookup"><span data-stu-id="87ce5-169">The time stamp when the data point is created</span></span> |<span data-ttu-id="87ce5-170">Date</span><span class="sxs-lookup"><span data-stu-id="87ce5-170">Date</span></span> |
| <span data-ttu-id="87ce5-171">City</span><span class="sxs-lookup"><span data-stu-id="87ce5-171">City</span></span> |<span data-ttu-id="87ce5-172">The location of the vehicle</span><span class="sxs-lookup"><span data-stu-id="87ce5-172">The location of the vehicle</span></span> |<span data-ttu-id="87ce5-173">Four cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="87ce5-173">Four cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="87ce5-174">The vehicle model reference data set maps VINs to models.</span><span class="sxs-lookup"><span data-stu-id="87ce5-174">The vehicle model reference data set maps VINs to models.</span></span> 

| <span data-ttu-id="87ce5-175">VIN</span><span class="sxs-lookup"><span data-stu-id="87ce5-175">VIN</span></span> | <span data-ttu-id="87ce5-176">Model</span><span class="sxs-lookup"><span data-stu-id="87ce5-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="87ce5-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="87ce5-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="87ce5-178">Sedan</span><span class="sxs-lookup"><span data-stu-id="87ce5-178">Sedan</span></span> |
| <span data-ttu-id="87ce5-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="87ce5-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="87ce5-180">Hybrid</span><span class="sxs-lookup"><span data-stu-id="87ce5-180">Hybrid</span></span> |
| <span data-ttu-id="87ce5-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="87ce5-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="87ce5-182">Family saloon</span><span class="sxs-lookup"><span data-stu-id="87ce5-182">Family saloon</span></span> |
| <span data-ttu-id="87ce5-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="87ce5-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="87ce5-184">Sedan</span><span class="sxs-lookup"><span data-stu-id="87ce5-184">Sedan</span></span> |
| <span data-ttu-id="87ce5-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="87ce5-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="87ce5-186">Hybrid</span><span class="sxs-lookup"><span data-stu-id="87ce5-186">Hybrid</span></span> |
| <span data-ttu-id="87ce5-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="87ce5-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="87ce5-188">Family saloon</span><span class="sxs-lookup"><span data-stu-id="87ce5-188">Family saloon</span></span> |
| <span data-ttu-id="87ce5-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="87ce5-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="87ce5-190">Sedan</span><span class="sxs-lookup"><span data-stu-id="87ce5-190">Sedan</span></span> |
| <span data-ttu-id="87ce5-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="87ce5-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="87ce5-192">Hybrid</span><span class="sxs-lookup"><span data-stu-id="87ce5-192">Hybrid</span></span> |
| <span data-ttu-id="87ce5-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="87ce5-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="87ce5-194">Family saloon</span><span class="sxs-lookup"><span data-stu-id="87ce5-194">Family saloon</span></span> |
| <span data-ttu-id="87ce5-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="87ce5-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="87ce5-196">Convertible</span><span class="sxs-lookup"><span data-stu-id="87ce5-196">Convertible</span></span> |
| <span data-ttu-id="87ce5-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="87ce5-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="87ce5-198">Station wagon</span><span class="sxs-lookup"><span data-stu-id="87ce5-198">Station wagon</span></span> |
| <span data-ttu-id="87ce5-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="87ce5-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="87ce5-200">Compact car</span><span class="sxs-lookup"><span data-stu-id="87ce5-200">Compact car</span></span> |
| <span data-ttu-id="87ce5-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="87ce5-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="87ce5-202">Small SUV</span><span class="sxs-lookup"><span data-stu-id="87ce5-202">Small SUV</span></span> |
| <span data-ttu-id="87ce5-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="87ce5-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="87ce5-204">Sports car</span><span class="sxs-lookup"><span data-stu-id="87ce5-204">Sports car</span></span> |
| <span data-ttu-id="87ce5-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="87ce5-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="87ce5-206">Medium SUV</span><span class="sxs-lookup"><span data-stu-id="87ce5-206">Medium SUV</span></span> |
| <span data-ttu-id="87ce5-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="87ce5-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="87ce5-208">Station wagon</span><span class="sxs-lookup"><span data-stu-id="87ce5-208">Station wagon</span></span> |
| <span data-ttu-id="87ce5-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="87ce5-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="87ce5-210">Large SUV</span><span class="sxs-lookup"><span data-stu-id="87ce5-210">Large SUV</span></span> |
| <span data-ttu-id="87ce5-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="87ce5-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="87ce5-212">Large SUV</span><span class="sxs-lookup"><span data-stu-id="87ce5-212">Large SUV</span></span> |
| <span data-ttu-id="87ce5-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="87ce5-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="87ce5-214">Coupe</span><span class="sxs-lookup"><span data-stu-id="87ce5-214">Coupe</span></span> |
| <span data-ttu-id="87ce5-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="87ce5-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="87ce5-216">Sedan</span><span class="sxs-lookup"><span data-stu-id="87ce5-216">Sedan</span></span> |
| <span data-ttu-id="87ce5-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="87ce5-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="87ce5-218">Hybrid</span><span class="sxs-lookup"><span data-stu-id="87ce5-218">Hybrid</span></span> |
| <span data-ttu-id="87ce5-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="87ce5-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="87ce5-220">Family saloon</span><span class="sxs-lookup"><span data-stu-id="87ce5-220">Family saloon</span></span> |
| <span data-ttu-id="87ce5-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="87ce5-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="87ce5-222">Sedan</span><span class="sxs-lookup"><span data-stu-id="87ce5-222">Sedan</span></span> |
| <span data-ttu-id="87ce5-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="87ce5-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="87ce5-224">Hybrid</span><span class="sxs-lookup"><span data-stu-id="87ce5-224">Hybrid</span></span> |
| <span data-ttu-id="87ce5-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="87ce5-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="87ce5-226">Family saloon</span><span class="sxs-lookup"><span data-stu-id="87ce5-226">Family saloon</span></span> |
| <span data-ttu-id="87ce5-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="87ce5-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="87ce5-228">Sedan</span><span class="sxs-lookup"><span data-stu-id="87ce5-228">Sedan</span></span> |
| <span data-ttu-id="87ce5-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="87ce5-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="87ce5-230">Hybrid</span><span class="sxs-lookup"><span data-stu-id="87ce5-230">Hybrid</span></span> |
| <span data-ttu-id="87ce5-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="87ce5-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="87ce5-232">Family saloon</span><span class="sxs-lookup"><span data-stu-id="87ce5-232">Family saloon</span></span> |
| <span data-ttu-id="87ce5-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="87ce5-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="87ce5-234">Convertible</span><span class="sxs-lookup"><span data-stu-id="87ce5-234">Convertible</span></span> |
| <span data-ttu-id="87ce5-235">…….</span><span class="sxs-lookup"><span data-stu-id="87ce5-235">…….</span></span> | |

## <a name="ingestion"></a><span data-ttu-id="87ce5-236">Ingestion</span><span class="sxs-lookup"><span data-stu-id="87ce5-236">Ingestion</span></span>
<span data-ttu-id="87ce5-237">Combinations of Azure Event Hubs, Azure Stream Analytics, and Azure Data Factory are used to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span><span class="sxs-lookup"><span data-stu-id="87ce5-237">Combinations of Azure Event Hubs, Azure Stream Analytics, and Azure Data Factory are used to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="87ce5-238">All these components are created and configured as part of the solution deployment.</span><span class="sxs-lookup"><span data-stu-id="87ce5-238">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="87ce5-239">Real-time analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-239">Real-time analysis</span></span>
<span data-ttu-id="87ce5-240">The events generated by the vehicle telematics simulator are published to the event hub by using the event hub SDK.</span><span class="sxs-lookup"><span data-stu-id="87ce5-240">The events generated by the vehicle telematics simulator are published to the event hub by using the event hub SDK.</span></span>  

![Event hub dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="87ce5-242">The Stream Analytics job ingests these events from the event hub and processes the data in real time to analyze the vehicle health.</span><span class="sxs-lookup"><span data-stu-id="87ce5-242">The Stream Analytics job ingests these events from the event hub and processes the data in real time to analyze the vehicle health.</span></span>

![Stream Analytics job processing data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 


<span data-ttu-id="87ce5-244">The Stream Analytics job:</span><span class="sxs-lookup"><span data-stu-id="87ce5-244">The Stream Analytics job:</span></span>

* <span data-ttu-id="87ce5-245">Ingests data from the event hub.</span><span class="sxs-lookup"><span data-stu-id="87ce5-245">Ingests data from the event hub.</span></span>
* <span data-ttu-id="87ce5-246">Performs a join with the reference data to map the vehicle VIN to the corresponding model.</span><span class="sxs-lookup"><span data-stu-id="87ce5-246">Performs a join with the reference data to map the vehicle VIN to the corresponding model.</span></span> 
* <span data-ttu-id="87ce5-247">Persists them into Azure Blob storage for rich batch analytics.</span><span class="sxs-lookup"><span data-stu-id="87ce5-247">Persists them into Azure Blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="87ce5-248">The following Stream Analytics query is used to persist the data into Blob storage:</span><span class="sxs-lookup"><span data-stu-id="87ce5-248">The following Stream Analytics query is used to persist the data into Blob storage:</span></span> 

![Stream Analytics job query for data ingestion](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 


### <a name="batch-analysis"></a><span data-ttu-id="87ce5-250">Batch analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-250">Batch analysis</span></span>
<span data-ttu-id="87ce5-251">An additional volume of simulated vehicle signals and diagnostic data set is also generated for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="87ce5-251">An additional volume of simulated vehicle signals and diagnostic data set is also generated for richer batch analytics.</span></span> <span data-ttu-id="87ce5-252">This additional volume is required to ensure a good representative data volume for batch processing.</span><span class="sxs-lookup"><span data-stu-id="87ce5-252">This additional volume is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="87ce5-253">For this purpose, PrepareSampleDataPipeline is used in the Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic data set.</span><span class="sxs-lookup"><span data-stu-id="87ce5-253">For this purpose, PrepareSampleDataPipeline is used in the Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic data set.</span></span> <span data-ttu-id="87ce5-254">To download the Data Factory custom .NET activity Visual Studio solution for customizations based on your requirements, go to the [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) webpage.</span><span class="sxs-lookup"><span data-stu-id="87ce5-254">To download the Data Factory custom .NET activity Visual Studio solution for customizations based on your requirements, go to the [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) webpage.</span></span> 

<span data-ttu-id="87ce5-255">This workflow shows sample data prepared for batch processing.</span><span class="sxs-lookup"><span data-stu-id="87ce5-255">This workflow shows sample data prepared for batch processing.</span></span>

![Sample data prepared for batch processing workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 


<span data-ttu-id="87ce5-257">The pipeline consists of a custom Data Factory .NET activity.</span><span class="sxs-lookup"><span data-stu-id="87ce5-257">The pipeline consists of a custom Data Factory .NET activity.</span></span>

![PrepareSampleDataPipeline activity](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="87ce5-259">After the pipeline executes successfully and the RawCarEventsTable data set is marked "Ready," one year's worth of simulated vehicle signals and diagnostic data are produced.</span><span class="sxs-lookup"><span data-stu-id="87ce5-259">After the pipeline executes successfully and the RawCarEventsTable data set is marked "Ready," one year's worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="87ce5-260">You see the following folder and file created in your storage account under the connectedcar container:</span><span class="sxs-lookup"><span data-stu-id="87ce5-260">You see the following folder and file created in your storage account under the connectedcar container:</span></span>

![PrepareSampleDataPipeline output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

## <a name="partition-the-data-set"></a><span data-ttu-id="87ce5-262">Partition the data set</span><span class="sxs-lookup"><span data-stu-id="87ce5-262">Partition the data set</span></span>
<span data-ttu-id="87ce5-263">In the data preparation step, the raw semi-structured vehicle signals and diagnostic data set are partitioned into a YEAR/MONTH format.</span><span class="sxs-lookup"><span data-stu-id="87ce5-263">In the data preparation step, the raw semi-structured vehicle signals and diagnostic data set are partitioned into a YEAR/MONTH format.</span></span> <span data-ttu-id="87ce5-264">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over.</span><span class="sxs-lookup"><span data-stu-id="87ce5-264">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over.</span></span> <span data-ttu-id="87ce5-265">For example, as the first blob account fills up, it faults over to the next account.</span><span class="sxs-lookup"><span data-stu-id="87ce5-265">For example, as the first blob account fills up, it faults over to the next account.</span></span> 

>[!NOTE] 
><span data-ttu-id="87ce5-266">This step in the solution applies only to batch processing.</span><span class="sxs-lookup"><span data-stu-id="87ce5-266">This step in the solution applies only to batch processing.</span></span>

<span data-ttu-id="87ce5-267">Input and output data management:</span><span class="sxs-lookup"><span data-stu-id="87ce5-267">Input and output data management:</span></span>

* <span data-ttu-id="87ce5-268">**Output data** (labeled PartitionedCarEventsTable) is kept for a long period of time as the foundational/"rawest" form of data in the customer's data lake.</span><span class="sxs-lookup"><span data-stu-id="87ce5-268">**Output data** (labeled PartitionedCarEventsTable) is kept for a long period of time as the foundational/"rawest" form of data in the customer's data lake.</span></span> 
* <span data-ttu-id="87ce5-269">**Input data** to this pipeline is typically discarded because the output data has full fidelity to the input.</span><span class="sxs-lookup"><span data-stu-id="87ce5-269">**Input data** to this pipeline is typically discarded because the output data has full fidelity to the input.</span></span> <span data-ttu-id="87ce5-270">It's stored (partitioned) better for subsequent use.</span><span class="sxs-lookup"><span data-stu-id="87ce5-270">It's stored (partitioned) better for subsequent use.</span></span>

<span data-ttu-id="87ce5-271">The partition car events workflow.</span><span class="sxs-lookup"><span data-stu-id="87ce5-271">The partition car events workflow.</span></span>

![Partition car events workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)


<span data-ttu-id="87ce5-273">The raw data is partitioned by using a Hive Azure HDInsight activity in PartitionCarEventsPipeline, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="87ce5-273">The raw data is partitioned by using a Hive Azure HDInsight activity in PartitionCarEventsPipeline, as shown in the following screenshot.</span></span> <span data-ttu-id="87ce5-274">The sample data generated for a year in the data preparation step is partitioned by YEAR/MONTH.</span><span class="sxs-lookup"><span data-stu-id="87ce5-274">The sample data generated for a year in the data preparation step is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="87ce5-275">The partitions are used to generate vehicle signals and diagnostic data for each month (total of 12 partitions) of a year.</span><span class="sxs-lookup"><span data-stu-id="87ce5-275">The partitions are used to generate vehicle signals and diagnostic data for each month (total of 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline activity](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)


<span data-ttu-id="87ce5-277">**PartitionConnectedCarEvents Hive script**</span><span class="sxs-lookup"><span data-stu-id="87ce5-277">**PartitionConnectedCarEvents Hive script**</span></span>

<span data-ttu-id="87ce5-278">The Hive script partitioncarevents.hql is used for partitioning.</span><span class="sxs-lookup"><span data-stu-id="87ce5-278">The Hive script partitioncarevents.hql is used for partitioning.</span></span> <span data-ttu-id="87ce5-279">It's located in the \demo\src\connectedcar\scripts folder of the downloaded zip file.</span><span class="sxs-lookup"><span data-stu-id="87ce5-279">It's located in the \demo\src\connectedcar\scripts folder of the downloaded zip file.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="87ce5-280">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span><span class="sxs-lookup"><span data-stu-id="87ce5-280">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span></span>

![Partitioned output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="87ce5-282">The data is now optimized, more manageable, and ready for further processing to gain rich batch insights.</span><span class="sxs-lookup"><span data-stu-id="87ce5-282">The data is now optimized, more manageable, and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="87ce5-283">Data analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-283">Data analysis</span></span>
<span data-ttu-id="87ce5-284">In this section, you see how to combine Stream Analytics, Azure Machine Learning, Data Factory, and HDInsight for rich advanced analytics on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="87ce5-284">In this section, you see how to combine Stream Analytics, Azure Machine Learning, Data Factory, and HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="87ce5-285">Machine learning</span><span class="sxs-lookup"><span data-stu-id="87ce5-285">Machine learning</span></span>
<span data-ttu-id="87ce5-286">The goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics, based on the following assumptions:</span><span class="sxs-lookup"><span data-stu-id="87ce5-286">The goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics, based on the following assumptions:</span></span>

* <span data-ttu-id="87ce5-287">If one of the following three conditions is true, the vehicles require servicing maintenance:</span><span class="sxs-lookup"><span data-stu-id="87ce5-287">If one of the following three conditions is true, the vehicles require servicing maintenance:</span></span>
  
  * <span data-ttu-id="87ce5-288">The tire pressure is low.</span><span class="sxs-lookup"><span data-stu-id="87ce5-288">The tire pressure is low.</span></span>
  * <span data-ttu-id="87ce5-289">The engine oil level is low.</span><span class="sxs-lookup"><span data-stu-id="87ce5-289">The engine oil level is low.</span></span>
  * <span data-ttu-id="87ce5-290">The engine temperature is high.</span><span class="sxs-lookup"><span data-stu-id="87ce5-290">The engine temperature is high.</span></span>

* <span data-ttu-id="87ce5-291">If one of the following conditions is true, the vehicles might have a safety issue and require recall:</span><span class="sxs-lookup"><span data-stu-id="87ce5-291">If one of the following conditions is true, the vehicles might have a safety issue and require recall:</span></span>
  
  * <span data-ttu-id="87ce5-292">The engine temperature is high, but the outside temperature is low.</span><span class="sxs-lookup"><span data-stu-id="87ce5-292">The engine temperature is high, but the outside temperature is low.</span></span>
  * <span data-ttu-id="87ce5-293">The engine temperature is low, but the outside temperature is high.</span><span class="sxs-lookup"><span data-stu-id="87ce5-293">The engine temperature is low, but the outside temperature is high.</span></span>

<span data-ttu-id="87ce5-294">Based on the previous requirements, two separate models detect anomalies.</span><span class="sxs-lookup"><span data-stu-id="87ce5-294">Based on the previous requirements, two separate models detect anomalies.</span></span> <span data-ttu-id="87ce5-295">One model is for vehicle maintenance detection, and one model is for vehicle recall detection.</span><span class="sxs-lookup"><span data-stu-id="87ce5-295">One model is for vehicle maintenance detection, and one model is for vehicle recall detection.</span></span> <span data-ttu-id="87ce5-296">In both models, the built-in principal component analysis (PCA) algorithm is used for anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="87ce5-296">In both models, the built-in principal component analysis (PCA) algorithm is used for anomaly detection.</span></span> 

#### <a name="maintenance-detection-model"></a><span data-ttu-id="87ce5-297">**Maintenance detection model**</span><span class="sxs-lookup"><span data-stu-id="87ce5-297">**Maintenance detection model**</span></span>

<span data-ttu-id="87ce5-298">If one of three indicators--tire pressure, engine oil, or engine temperature--satisfies its respective condition, the maintenance detection model reports an anomaly.</span><span class="sxs-lookup"><span data-stu-id="87ce5-298">If one of three indicators--tire pressure, engine oil, or engine temperature--satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="87ce5-299">As a result, only these three variables need to be consider in building the model.</span><span class="sxs-lookup"><span data-stu-id="87ce5-299">As a result, only these three variables need to be consider in building the model.</span></span> <span data-ttu-id="87ce5-300">In the experiment in machine learning, the **Select Columns in Dataset** module is used to extract these three variables.</span><span class="sxs-lookup"><span data-stu-id="87ce5-300">In the experiment in machine learning, the **Select Columns in Dataset** module is used to extract these three variables.</span></span> <span data-ttu-id="87ce5-301">Next, the PCA-based anomaly detection module is used to build the anomaly detection model.</span><span class="sxs-lookup"><span data-stu-id="87ce5-301">Next, the PCA-based anomaly detection module is used to build the anomaly detection model.</span></span> 

<span data-ttu-id="87ce5-302">PCA is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="87ce5-302">PCA is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="87ce5-303">PCA converts a set of cases that contain possibly correlated variables into a set of values called principal components.</span><span class="sxs-lookup"><span data-stu-id="87ce5-303">PCA converts a set of cases that contain possibly correlated variables into a set of values called principal components.</span></span> <span data-ttu-id="87ce5-304">The key idea of PCA-based modeling is to project data onto a lower-dimensional space to more easily identify features and anomalies.</span><span class="sxs-lookup"><span data-stu-id="87ce5-304">The key idea of PCA-based modeling is to project data onto a lower-dimensional space to more easily identify features and anomalies.</span></span>

<span data-ttu-id="87ce5-305">For each new input to the detection model, the anomaly detector first computes its projection on the eigenvectors.</span><span class="sxs-lookup"><span data-stu-id="87ce5-305">For each new input to the detection model, the anomaly detector first computes its projection on the eigenvectors.</span></span> <span data-ttu-id="87ce5-306">It then computes the normalized reconstruction error.</span><span class="sxs-lookup"><span data-stu-id="87ce5-306">It then computes the normalized reconstruction error.</span></span> <span data-ttu-id="87ce5-307">This normalized error is the anomaly score: the higher the error, the more anomalous the instance.</span><span class="sxs-lookup"><span data-stu-id="87ce5-307">This normalized error is the anomaly score: the higher the error, the more anomalous the instance.</span></span> 

<span data-ttu-id="87ce5-308">In the maintenance detection problem, each record is considered as a point in a three-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span><span class="sxs-lookup"><span data-stu-id="87ce5-308">In the maintenance detection problem, each record is considered as a point in a three-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="87ce5-309">To capture these anomalies, PCA is used to project the original data in the three-dimensional space onto a two-dimensional space.</span><span class="sxs-lookup"><span data-stu-id="87ce5-309">To capture these anomalies, PCA is used to project the original data in the three-dimensional space onto a two-dimensional space.</span></span> <span data-ttu-id="87ce5-310">Thus, the parameter number of components to use in PCA is set to two.</span><span class="sxs-lookup"><span data-stu-id="87ce5-310">Thus, the parameter number of components to use in PCA is set to two.</span></span> <span data-ttu-id="87ce5-311">This parameter plays an important role in applying PCA-based anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="87ce5-311">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="87ce5-312">After using PCA to project data, these anomalies are identified more easily.</span><span class="sxs-lookup"><span data-stu-id="87ce5-312">After using PCA to project data, these anomalies are identified more easily.</span></span>

#### <a name="recall-anomaly-detection-model"></a><span data-ttu-id="87ce5-313">**Recall anomaly detection model**</span><span class="sxs-lookup"><span data-stu-id="87ce5-313">**Recall anomaly detection model**</span></span>

<span data-ttu-id="87ce5-314">In the recall anomaly detection model, the **Select Columns in Dataset** and PCA-based anomaly detection modules are used in a similar way.</span><span class="sxs-lookup"><span data-stu-id="87ce5-314">In the recall anomaly detection model, the **Select Columns in Dataset** and PCA-based anomaly detection modules are used in a similar way.</span></span> <span data-ttu-id="87ce5-315">Specifically, three variables--engine temperature, outside temperature, and speed--are extracted first by using the **Select Columns in Dataset** module.</span><span class="sxs-lookup"><span data-stu-id="87ce5-315">Specifically, three variables--engine temperature, outside temperature, and speed--are extracted first by using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="87ce5-316">The speed variable also is included, because the engine temperature typically correlates to the speed.</span><span class="sxs-lookup"><span data-stu-id="87ce5-316">The speed variable also is included, because the engine temperature typically correlates to the speed.</span></span> <span data-ttu-id="87ce5-317">Next, the PCA-based anomaly detection module is used to project the data from the three-dimensional space onto a two-dimensional space.</span><span class="sxs-lookup"><span data-stu-id="87ce5-317">Next, the PCA-based anomaly detection module is used to project the data from the three-dimensional space onto a two-dimensional space.</span></span> <span data-ttu-id="87ce5-318">The recall criteria are satisfied.</span><span class="sxs-lookup"><span data-stu-id="87ce5-318">The recall criteria are satisfied.</span></span> <span data-ttu-id="87ce5-319">The vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span><span class="sxs-lookup"><span data-stu-id="87ce5-319">The vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="87ce5-320">After PCA is performed, the PCA-based anomaly detection algorithm is used to capture the anomalies.</span><span class="sxs-lookup"><span data-stu-id="87ce5-320">After PCA is performed, the PCA-based anomaly detection algorithm is used to capture the anomalies.</span></span> 

<span data-ttu-id="87ce5-321">When training either model, normal data is used as the input data to train the PCA-based anomaly detection model.</span><span class="sxs-lookup"><span data-stu-id="87ce5-321">When training either model, normal data is used as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="87ce5-322">(Normal data doesn't require maintenance or recall.) In the scoring experiment, the trained anomaly detection model is used to detect whether the vehicle requires maintenance or recall.</span><span class="sxs-lookup"><span data-stu-id="87ce5-322">(Normal data doesn't require maintenance or recall.) In the scoring experiment, the trained anomaly detection model is used to detect whether the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="87ce5-323">Real-time analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-323">Real-time analysis</span></span>
<span data-ttu-id="87ce5-324">The following Stream Analytics SQL query is used to get the average of all the important vehicle parameters.</span><span class="sxs-lookup"><span data-stu-id="87ce5-324">The following Stream Analytics SQL query is used to get the average of all the important vehicle parameters.</span></span> <span data-ttu-id="87ce5-325">These parameters include vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span><span class="sxs-lookup"><span data-stu-id="87ce5-325">These parameters include vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="87ce5-326">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in a specific region.</span><span class="sxs-lookup"><span data-stu-id="87ce5-326">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in a specific region.</span></span> <span data-ttu-id="87ce5-327">The averages are then correlated to demographics.</span><span class="sxs-lookup"><span data-stu-id="87ce5-327">The averages are then correlated to demographics.</span></span> 

![Stream Analytics query for real-time processing](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="87ce5-329">All the averages are calculated over a three-second tumbling window.</span><span class="sxs-lookup"><span data-stu-id="87ce5-329">All the averages are calculated over a three-second tumbling window.</span></span> <span data-ttu-id="87ce5-330">A tumbling window is used because non-overlapping and contiguous time intervals are required.</span><span class="sxs-lookup"><span data-stu-id="87ce5-330">A tumbling window is used because non-overlapping and contiguous time intervals are required.</span></span> 

<span data-ttu-id="87ce5-331">To learn more about the windowing capabilities in Stream Analytics, see [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="87ce5-331">To learn more about the windowing capabilities in Stream Analytics, see [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

#### <a name="real-time-prediction"></a><span data-ttu-id="87ce5-332">**Real-time prediction**</span><span class="sxs-lookup"><span data-stu-id="87ce5-332">**Real-time prediction**</span></span>

<span data-ttu-id="87ce5-333">An application is included as part of the solution to operationalize the machine learning model in real time.</span><span class="sxs-lookup"><span data-stu-id="87ce5-333">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="87ce5-334">The application RealTimeDashboardApp is created and configured as part of the solution deployment.</span><span class="sxs-lookup"><span data-stu-id="87ce5-334">The application RealTimeDashboardApp is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="87ce5-335">The application:</span><span class="sxs-lookup"><span data-stu-id="87ce5-335">The application:</span></span>

* <span data-ttu-id="87ce5-336">Listens to an event hub instance where Stream Analytics publishes the events in a pattern continuously.</span><span class="sxs-lookup"><span data-stu-id="87ce5-336">Listens to an event hub instance where Stream Analytics publishes the events in a pattern continuously.</span></span>

    ![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) 

* <span data-ttu-id="87ce5-338">Receives events.</span><span class="sxs-lookup"><span data-stu-id="87ce5-338">Receives events.</span></span> <span data-ttu-id="87ce5-339">For every event that this application receives:</span><span class="sxs-lookup"><span data-stu-id="87ce5-339">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="87ce5-340">The data is processed by using a machine learning request-response scoring (RRS) endpoint.</span><span class="sxs-lookup"><span data-stu-id="87ce5-340">The data is processed by using a machine learning request-response scoring (RRS) endpoint.</span></span> <span data-ttu-id="87ce5-341">The RRS endpoint is automatically published as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="87ce5-341">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="87ce5-342">The RRS output is published to a Power BI data set by using the push APIs.</span><span class="sxs-lookup"><span data-stu-id="87ce5-342">The RRS output is published to a Power BI data set by using the push APIs.</span></span>

<span data-ttu-id="87ce5-343">This pattern is also applicable to scenarios in which you want to integrate a line-of-business application with the real-time analytics flow.</span><span class="sxs-lookup"><span data-stu-id="87ce5-343">This pattern is also applicable to scenarios in which you want to integrate a line-of-business application with the real-time analytics flow.</span></span> <span data-ttu-id="87ce5-344">These scenarios include alerts, notifications, and messaging.</span><span class="sxs-lookup"><span data-stu-id="87ce5-344">These scenarios include alerts, notifications, and messaging.</span></span>

<span data-ttu-id="87ce5-345">Note: that the data for the RealtimeDashboardApp Visual Studio solution is no longer available.</span><span class="sxs-lookup"><span data-stu-id="87ce5-345">Note: that the data for the RealtimeDashboardApp Visual Studio solution is no longer available.</span></span>

#### <a name="execute-the-real-time-dashboard-application"></a><span data-ttu-id="87ce5-346">**Execute the real-time dashboard application**</span><span class="sxs-lookup"><span data-stu-id="87ce5-346">**Execute the real-time dashboard application**</span></span>
1. <span data-ttu-id="87ce5-347">Extract the RealtimeDashboardApp, and save it locally.</span><span class="sxs-lookup"><span data-stu-id="87ce5-347">Extract the RealtimeDashboardApp, and save it locally.</span></span>

    ![RealTimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) 

2. <span data-ttu-id="87ce5-349">Execute the application RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="87ce5-349">Execute the application RealtimeDashboardApp.exe.</span></span>

3. <span data-ttu-id="87ce5-350">Enter your valid Power BI credentials, and select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="87ce5-350">Enter your valid Power BI credentials, and select **Sign in**.</span></span>  

    ![Real-time dashboard app sign-in window](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 
    
4. <span data-ttu-id="87ce5-352">Select **Accept**.</span><span class="sxs-lookup"><span data-stu-id="87ce5-352">Select **Accept**.</span></span>

    ![Real-time dashboard app final sign-in window](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

>[!NOTE] 
><span data-ttu-id="87ce5-354">If you want to flush the Power BI data set, execute the RealtimeDashboardApp with the "flushdata" parameter.</span><span class="sxs-lookup"><span data-stu-id="87ce5-354">If you want to flush the Power BI data set, execute the RealtimeDashboardApp with the "flushdata" parameter.</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="87ce5-355">Batch analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-355">Batch analysis</span></span>
<span data-ttu-id="87ce5-356">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data.</span><span class="sxs-lookup"><span data-stu-id="87ce5-356">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data.</span></span> <span data-ttu-id="87ce5-357">This data reveals rich insights on driving patterns, usage behavior, and vehicle health.</span><span class="sxs-lookup"><span data-stu-id="87ce5-357">This data reveals rich insights on driving patterns, usage behavior, and vehicle health.</span></span> <span data-ttu-id="87ce5-358">This information makes it possible to:</span><span class="sxs-lookup"><span data-stu-id="87ce5-358">This information makes it possible to:</span></span>

* <span data-ttu-id="87ce5-359">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel-efficient driving behaviors.</span><span class="sxs-lookup"><span data-stu-id="87ce5-359">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel-efficient driving behaviors.</span></span>
* <span data-ttu-id="87ce5-360">Learn proactively about customers and their driving patterns to govern business decisions and provide best-in-class products and services.</span><span class="sxs-lookup"><span data-stu-id="87ce5-360">Learn proactively about customers and their driving patterns to govern business decisions and provide best-in-class products and services.</span></span>

<span data-ttu-id="87ce5-361">In this solution, the following metrics are targeted:</span><span class="sxs-lookup"><span data-stu-id="87ce5-361">In this solution, the following metrics are targeted:</span></span>

* <span data-ttu-id="87ce5-362">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of year to gain insights on aggressive driving patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-362">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="87ce5-363">Contoso Motors can use these insights for marketing campaigns to introduce new personalized features and usage-based insurance.</span><span class="sxs-lookup"><span data-stu-id="87ce5-363">Contoso Motors can use these insights for marketing campaigns to introduce new personalized features and usage-based insurance.</span></span>
* <span data-ttu-id="87ce5-364">**Fuel-efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of year to gain insights on fuel-efficient driving patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-364">**Fuel-efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of year to gain insights on fuel-efficient driving patterns.</span></span> <span data-ttu-id="87ce5-365">Contoso Motors can use these insights for marketing campaigns to introduce new features and proactive reporting to drivers for cost-effective and environment-friendly driving habits.</span><span class="sxs-lookup"><span data-stu-id="87ce5-365">Contoso Motors can use these insights for marketing campaigns to introduce new features and proactive reporting to drivers for cost-effective and environment-friendly driving habits.</span></span>
* <span data-ttu-id="87ce5-366">**Recall models**: Identifies models that require recalls by operationalizing the anomaly detection machine learning experiment.</span><span class="sxs-lookup"><span data-stu-id="87ce5-366">**Recall models**: Identifies models that require recalls by operationalizing the anomaly detection machine learning experiment.</span></span>

<span data-ttu-id="87ce5-367">Let's look into the details of each of these metrics.</span><span class="sxs-lookup"><span data-stu-id="87ce5-367">Let's look into the details of each of these metrics.</span></span>

#### <a name="aggressive-driving-behavior-patterns"></a><span data-ttu-id="87ce5-368">**Aggressive driving behavior patterns**</span><span class="sxs-lookup"><span data-stu-id="87ce5-368">**Aggressive driving behavior patterns**</span></span>

<span data-ttu-id="87ce5-369">The partitioned vehicle signals and diagnostic data are processed in AggresiveDrivingPatternPipeline, as shown in the following workflow.</span><span class="sxs-lookup"><span data-stu-id="87ce5-369">The partitioned vehicle signals and diagnostic data are processed in AggresiveDrivingPatternPipeline, as shown in the following workflow.</span></span> <span data-ttu-id="87ce5-370">Hive is used to determine the models, location, vehicle, driving conditions, and other parameters that exhibit aggressive driving patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-370">Hive is used to determine the models, location, vehicle, driving conditions, and other parameters that exhibit aggressive driving patterns.</span></span>

![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 

<span data-ttu-id="87ce5-372">***Aggressive driving pattern Hive query***</span><span class="sxs-lookup"><span data-stu-id="87ce5-372">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="87ce5-373">The Hive script aggresivedriving.hql is used to analyze aggressive driving condition patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-373">The Hive script aggresivedriving.hql is used to analyze aggressive driving condition patterns.</span></span> <span data-ttu-id="87ce5-374">It's located in the \demo\src\connectedcar\scripts folder of the downloaded zip file.</span><span class="sxs-lookup"><span data-stu-id="87ce5-374">It's located in the \demo\src\connectedcar\scripts folder of the downloaded zip file.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="87ce5-375">The script uses the combination of a vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking patterns at high speed.</span><span class="sxs-lookup"><span data-stu-id="87ce5-375">The script uses the combination of a vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking patterns at high speed.</span></span> 

<span data-ttu-id="87ce5-376">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span><span class="sxs-lookup"><span data-stu-id="87ce5-376">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span></span>

![AggressiveDrivingPatternPipeline output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 


#### <a name="fuel-efficient-driving-behavior-patterns"></a><span data-ttu-id="87ce5-378">**Fuel-efficient driving behavior patterns**</span><span class="sxs-lookup"><span data-stu-id="87ce5-378">**Fuel-efficient driving behavior patterns**</span></span>

<span data-ttu-id="87ce5-379">The partitioned vehicle signals and diagnostic data are processed in FuelEfficientDrivingPatternPipeline, as shown in the following workflow.</span><span class="sxs-lookup"><span data-stu-id="87ce5-379">The partitioned vehicle signals and diagnostic data are processed in FuelEfficientDrivingPatternPipeline, as shown in the following workflow.</span></span> <span data-ttu-id="87ce5-380">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel-efficient driving patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-380">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel-efficient driving patterns.</span></span>

![Fuel-efficient driving patterns](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="87ce5-382">***Fuel-efficient driving pattern Hive query***</span><span class="sxs-lookup"><span data-stu-id="87ce5-382">***Fuel-efficient driving pattern Hive query***</span></span>

<span data-ttu-id="87ce5-383">The Hive script fuelefficientdriving.hql is used to analyze fuel-efficient driving condition patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-383">The Hive script fuelefficientdriving.hql is used to analyze fuel-efficient driving condition patterns.</span></span> <span data-ttu-id="87ce5-384">It's located in the \demo\src\connectedcar\scripts folder of the downloaded zip file.</span><span class="sxs-lookup"><span data-stu-id="87ce5-384">It's located in the \demo\src\connectedcar\scripts folder of the downloaded zip file.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="87ce5-385">The script uses the combination of a vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel-efficient driving behavior based on acceleration, braking, and speed patterns.</span><span class="sxs-lookup"><span data-stu-id="87ce5-385">The script uses the combination of a vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel-efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="87ce5-386">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span><span class="sxs-lookup"><span data-stu-id="87ce5-386">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span></span>

![FuelEfficientDrivingPatternPipeline output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="87ce5-388">**Recall model predictions**</span><span class="sxs-lookup"><span data-stu-id="87ce5-388">**Recall model predictions**</span></span>

<span data-ttu-id="87ce5-389">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span><span class="sxs-lookup"><span data-stu-id="87ce5-389">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="87ce5-390">The batch scoring endpoint is used in this workflow.</span><span class="sxs-lookup"><span data-stu-id="87ce5-390">The batch scoring endpoint is used in this workflow.</span></span> <span data-ttu-id="87ce5-391">It's registered as a data factory linked service and operationalized by using the data factory batch scoring activity.</span><span class="sxs-lookup"><span data-stu-id="87ce5-391">It's registered as a data factory linked service and operationalized by using the data factory batch scoring activity.</span></span>

![Machine learning endpoint](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="87ce5-393">The registered linked service is used in DetectAnomalyPipeline to score the data by using the anomaly detection model.</span><span class="sxs-lookup"><span data-stu-id="87ce5-393">The registered linked service is used in DetectAnomalyPipeline to score the data by using the anomaly detection model.</span></span> 

![Machine learning batch scoring activity in data factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png)  

<span data-ttu-id="87ce5-395">A few steps are performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span><span class="sxs-lookup"><span data-stu-id="87ce5-395">A few steps are performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline for recall prediction](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png)  

<span data-ttu-id="87ce5-397">***Anomaly detection Hive query***</span><span class="sxs-lookup"><span data-stu-id="87ce5-397">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="87ce5-398">After the scoring is finished, an HDInsight activity processes and aggregates the data that the model categorized as anomalies.</span><span class="sxs-lookup"><span data-stu-id="87ce5-398">After the scoring is finished, an HDInsight activity processes and aggregates the data that the model categorized as anomalies.</span></span> <span data-ttu-id="87ce5-399">The model uses a probability score of 0.60 or higher.</span><span class="sxs-lookup"><span data-stu-id="87ce5-399">The model uses a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="87ce5-400">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span><span class="sxs-lookup"><span data-stu-id="87ce5-400">After the pipeline executes successfully, you see the following partitions generated in your storage account under the connectedcar container:</span></span>

![DetectAnomalyPipeline output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

## <a name="publish"></a><span data-ttu-id="87ce5-402">Publish</span><span class="sxs-lookup"><span data-stu-id="87ce5-402">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="87ce5-403">Real-time analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-403">Real-time analysis</span></span>
<span data-ttu-id="87ce5-404">One of the queries in the Stream Analytics job publishes the events to an output event hub instance.</span><span class="sxs-lookup"><span data-stu-id="87ce5-404">One of the queries in the Stream Analytics job publishes the events to an output event hub instance.</span></span> 

![Stream Analytics job published to an output event hub instance](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="87ce5-406">The following Stream Analytics query is used to publish to the output event hub instance:</span><span class="sxs-lookup"><span data-stu-id="87ce5-406">The following Stream Analytics query is used to publish to the output event hub instance:</span></span>

![Stream Analytics query to publish to the output event hub instance](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="87ce5-408">This stream of events is consumed by the RealTimeDashboardApp that's included in the solution.</span><span class="sxs-lookup"><span data-stu-id="87ce5-408">This stream of events is consumed by the RealTimeDashboardApp that's included in the solution.</span></span> <span data-ttu-id="87ce5-409">This application uses the machine learning request-response web service for real-time scoring.</span><span class="sxs-lookup"><span data-stu-id="87ce5-409">This application uses the machine learning request-response web service for real-time scoring.</span></span> <span data-ttu-id="87ce5-410">It publishes the resultant data to a Power BI data set for consumption.</span><span class="sxs-lookup"><span data-stu-id="87ce5-410">It publishes the resultant data to a Power BI data set for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="87ce5-411">Batch analysis</span><span class="sxs-lookup"><span data-stu-id="87ce5-411">Batch analysis</span></span>
<span data-ttu-id="87ce5-412">The results of the batch and real-time processing are published to Azure SQL Database tables for consumption.</span><span class="sxs-lookup"><span data-stu-id="87ce5-412">The results of the batch and real-time processing are published to Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="87ce5-413">The SQL server, the database, and the tables are created automatically as part of the setup script.</span><span class="sxs-lookup"><span data-stu-id="87ce5-413">The SQL server, the database, and the tables are created automatically as part of the setup script.</span></span> 

<span data-ttu-id="87ce5-414">The batch processing results are copied to the data mart workflow.</span><span class="sxs-lookup"><span data-stu-id="87ce5-414">The batch processing results are copied to the data mart workflow.</span></span>

![Batch processing results copied to data mart workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="87ce5-416">The Stream Analytics job is published to the data mart.</span><span class="sxs-lookup"><span data-stu-id="87ce5-416">The Stream Analytics job is published to the data mart.</span></span>

![Stream Analytics job published to data mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="87ce5-418">The data mart setting is in the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="87ce5-418">The data mart setting is in the Stream Analytics job.</span></span>

![Data mart setting in Stream Analytics job](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

## <a name="consume"></a><span data-ttu-id="87ce5-420">Consume</span><span class="sxs-lookup"><span data-stu-id="87ce5-420">Consume</span></span>
<span data-ttu-id="87ce5-421">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="87ce5-421">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="87ce5-422">The final dashboard looks like this example:</span><span class="sxs-lookup"><span data-stu-id="87ce5-422">The final dashboard looks like this example:</span></span>

![Power BI dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

## <a name="summary"></a><span data-ttu-id="87ce5-424">Summary</span><span class="sxs-lookup"><span data-stu-id="87ce5-424">Summary</span></span>
<span data-ttu-id="87ce5-425">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span><span class="sxs-lookup"><span data-stu-id="87ce5-425">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="87ce5-426">The lambda architecture pattern is used for real-time and batch analytics with predictions and actions.</span><span class="sxs-lookup"><span data-stu-id="87ce5-426">The lambda architecture pattern is used for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="87ce5-427">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span><span class="sxs-lookup"><span data-stu-id="87ce5-427">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

### <a name="references"></a><span data-ttu-id="87ce5-428">References</span><span class="sxs-lookup"><span data-stu-id="87ce5-428">References</span></span>

* [<span data-ttu-id="87ce5-429">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="87ce5-429">Azure Event Hubs</span></span>](https://azure.microsoft.com/services/event-hubs/)
* [<span data-ttu-id="87ce5-430">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="87ce5-430">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)
* [<span data-ttu-id="87ce5-431">Azure Event Hubs SDK for stream ingestion</span><span class="sxs-lookup"><span data-stu-id="87ce5-431">Azure Event Hubs SDK for stream ingestion</span></span>](../../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
* [<span data-ttu-id="87ce5-432">Azure Data Factory data movement capabilities</span><span class="sxs-lookup"><span data-stu-id="87ce5-432">Azure Data Factory data movement capabilities</span></span>](../../data-factory/copy-activity-overview.md)
* [<span data-ttu-id="87ce5-433">Azure Data Factory .NET activity</span><span class="sxs-lookup"><span data-stu-id="87ce5-433">Azure Data Factory .NET activity</span></span>](../../data-factory/transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="87ce5-434">Azure Data Factory .NET activity Visual Studio solution used to prepare sample data</span><span class="sxs-lookup"><span data-stu-id="87ce5-434">Azure Data Factory .NET activity Visual Studio solution used to prepare sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 
