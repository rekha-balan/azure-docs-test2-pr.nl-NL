---
title: Deep dive into predict vehicle health and driving habits - Azure | Microsoft Docs
description: Use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b5fc93f071e40614aa1dbb292709c5bb806b6613
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551534"
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="2cfd2-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span><span class="sxs-lookup"><span data-stu-id="2cfd2-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="2cfd2-104">This **menu** links to the sections of this playbook:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="2cfd2-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="2cfd2-106">Data Sources</span><span class="sxs-lookup"><span data-stu-id="2cfd2-106">Data Sources</span></span>
<span data-ttu-id="2cfd2-107">The solution uses two different data sources:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="2cfd2-108">**simulated vehicle signals and diagnostic dataset** and</span><span class="sxs-lookup"><span data-stu-id="2cfd2-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="2cfd2-109">**vehicle catalog**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-109">**vehicle catalog**</span></span>

<span data-ttu-id="2cfd2-110">A vehicle telematics simulator is included as part of this solution.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="2cfd2-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="2cfd2-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="2cfd2-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Vehicle telematics simulator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="2cfd2-115">*Figure 1 – Vehicle Telematics Simulator*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="2cfd2-116">This is a JSON-formatted dataset that contains the following schema.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="2cfd2-117">Column</span><span class="sxs-lookup"><span data-stu-id="2cfd2-117">Column</span></span> | <span data-ttu-id="2cfd2-118">Description</span><span class="sxs-lookup"><span data-stu-id="2cfd2-118">Description</span></span> | <span data-ttu-id="2cfd2-119">Values</span><span class="sxs-lookup"><span data-stu-id="2cfd2-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2cfd2-120">VIN</span><span class="sxs-lookup"><span data-stu-id="2cfd2-120">VIN</span></span> |<span data-ttu-id="2cfd2-121">Randomly generated Vehicle Identification Number</span><span class="sxs-lookup"><span data-stu-id="2cfd2-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="2cfd2-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="2cfd2-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="2cfd2-123">Outside temperature</span></span> |<span data-ttu-id="2cfd2-124">The outside temperature where the vehicle is driving</span><span class="sxs-lookup"><span data-stu-id="2cfd2-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="2cfd2-125">Randomly generated number from 0-100</span><span class="sxs-lookup"><span data-stu-id="2cfd2-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="2cfd2-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="2cfd2-126">Engine temperature</span></span> |<span data-ttu-id="2cfd2-127">The engine temperature of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="2cfd2-128">Randomly generated number from 0-500</span><span class="sxs-lookup"><span data-stu-id="2cfd2-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="2cfd2-129">Speed</span><span class="sxs-lookup"><span data-stu-id="2cfd2-129">Speed</span></span> |<span data-ttu-id="2cfd2-130">The engine speed at which the vehicle is driving</span><span class="sxs-lookup"><span data-stu-id="2cfd2-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="2cfd2-131">Randomly generated number from 0-100</span><span class="sxs-lookup"><span data-stu-id="2cfd2-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="2cfd2-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="2cfd2-132">Fuel</span></span> |<span data-ttu-id="2cfd2-133">The fuel level of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="2cfd2-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span><span class="sxs-lookup"><span data-stu-id="2cfd2-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="2cfd2-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="2cfd2-135">EngineOil</span></span> |<span data-ttu-id="2cfd2-136">The engine oil level of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="2cfd2-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span><span class="sxs-lookup"><span data-stu-id="2cfd2-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="2cfd2-138">Tire pressure</span><span class="sxs-lookup"><span data-stu-id="2cfd2-138">Tire pressure</span></span> |<span data-ttu-id="2cfd2-139">The tire pressure of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="2cfd2-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span><span class="sxs-lookup"><span data-stu-id="2cfd2-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="2cfd2-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="2cfd2-141">Odometer</span></span> |<span data-ttu-id="2cfd2-142">The odometer reading of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="2cfd2-143">Randomly generated number from 0-200000</span><span class="sxs-lookup"><span data-stu-id="2cfd2-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="2cfd2-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="2cfd2-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="2cfd2-145">The accelerator pedal position of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="2cfd2-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span><span class="sxs-lookup"><span data-stu-id="2cfd2-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="2cfd2-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="2cfd2-147">Parking_brake_status</span></span> |<span data-ttu-id="2cfd2-148">Indicates whether the vehicle is parked or not</span><span class="sxs-lookup"><span data-stu-id="2cfd2-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="2cfd2-149">True or False</span><span class="sxs-lookup"><span data-stu-id="2cfd2-149">True or False</span></span> |
| <span data-ttu-id="2cfd2-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="2cfd2-150">Headlamp_status</span></span> |<span data-ttu-id="2cfd2-151">Indicates where the headlamp is on or not</span><span class="sxs-lookup"><span data-stu-id="2cfd2-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="2cfd2-152">True or False</span><span class="sxs-lookup"><span data-stu-id="2cfd2-152">True or False</span></span> |
| <span data-ttu-id="2cfd2-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="2cfd2-153">Brake_pedal_status</span></span> |<span data-ttu-id="2cfd2-154">Indicates whether the brake pedal is pressed or not</span><span class="sxs-lookup"><span data-stu-id="2cfd2-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="2cfd2-155">True or False</span><span class="sxs-lookup"><span data-stu-id="2cfd2-155">True or False</span></span> |
| <span data-ttu-id="2cfd2-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="2cfd2-156">Transmission_gear_position</span></span> |<span data-ttu-id="2cfd2-157">The transmission gear position of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="2cfd2-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span><span class="sxs-lookup"><span data-stu-id="2cfd2-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="2cfd2-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="2cfd2-159">Ignition_status</span></span> |<span data-ttu-id="2cfd2-160">Indicates whether the vehicle is running or stopped</span><span class="sxs-lookup"><span data-stu-id="2cfd2-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="2cfd2-161">True or False</span><span class="sxs-lookup"><span data-stu-id="2cfd2-161">True or False</span></span> |
| <span data-ttu-id="2cfd2-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="2cfd2-162">Windshield_wiper_status</span></span> |<span data-ttu-id="2cfd2-163">Indicates whether the windshield wiper is turned or not</span><span class="sxs-lookup"><span data-stu-id="2cfd2-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="2cfd2-164">True or False</span><span class="sxs-lookup"><span data-stu-id="2cfd2-164">True or False</span></span> |
| <span data-ttu-id="2cfd2-165">ABS</span><span class="sxs-lookup"><span data-stu-id="2cfd2-165">ABS</span></span> |<span data-ttu-id="2cfd2-166">Indicates whether ABS is engaged or not</span><span class="sxs-lookup"><span data-stu-id="2cfd2-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="2cfd2-167">True or False</span><span class="sxs-lookup"><span data-stu-id="2cfd2-167">True or False</span></span> |
| <span data-ttu-id="2cfd2-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2cfd2-168">Timestamp</span></span> |<span data-ttu-id="2cfd2-169">The timestamp when the data point is created</span><span class="sxs-lookup"><span data-stu-id="2cfd2-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="2cfd2-170">Date</span><span class="sxs-lookup"><span data-stu-id="2cfd2-170">Date</span></span> |
| <span data-ttu-id="2cfd2-171">City</span><span class="sxs-lookup"><span data-stu-id="2cfd2-171">City</span></span> |<span data-ttu-id="2cfd2-172">The location of the vehicle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-172">The location of the vehicle</span></span> |<span data-ttu-id="2cfd2-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="2cfd2-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="2cfd2-174">The vehicle model reference dataset contains VIN to the model mapping.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="2cfd2-175">VIN</span><span class="sxs-lookup"><span data-stu-id="2cfd2-175">VIN</span></span> | <span data-ttu-id="2cfd2-176">Model</span><span class="sxs-lookup"><span data-stu-id="2cfd2-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="2cfd2-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="2cfd2-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="2cfd2-178">Sedan</span><span class="sxs-lookup"><span data-stu-id="2cfd2-178">Sedan</span></span> |
| <span data-ttu-id="2cfd2-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="2cfd2-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="2cfd2-180">Hybrid</span><span class="sxs-lookup"><span data-stu-id="2cfd2-180">Hybrid</span></span> |
| <span data-ttu-id="2cfd2-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="2cfd2-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="2cfd2-182">Family Saloon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-182">Family Saloon</span></span> |
| <span data-ttu-id="2cfd2-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="2cfd2-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="2cfd2-184">Sedan</span><span class="sxs-lookup"><span data-stu-id="2cfd2-184">Sedan</span></span> |
| <span data-ttu-id="2cfd2-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="2cfd2-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="2cfd2-186">Hybrid</span><span class="sxs-lookup"><span data-stu-id="2cfd2-186">Hybrid</span></span> |
| <span data-ttu-id="2cfd2-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="2cfd2-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="2cfd2-188">Family Saloon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-188">Family Saloon</span></span> |
| <span data-ttu-id="2cfd2-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="2cfd2-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="2cfd2-190">Sedan</span><span class="sxs-lookup"><span data-stu-id="2cfd2-190">Sedan</span></span> |
| <span data-ttu-id="2cfd2-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="2cfd2-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="2cfd2-192">Hybrid</span><span class="sxs-lookup"><span data-stu-id="2cfd2-192">Hybrid</span></span> |
| <span data-ttu-id="2cfd2-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="2cfd2-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="2cfd2-194">Family Saloon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-194">Family Saloon</span></span> |
| <span data-ttu-id="2cfd2-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="2cfd2-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="2cfd2-196">Convertible</span><span class="sxs-lookup"><span data-stu-id="2cfd2-196">Convertible</span></span> |
| <span data-ttu-id="2cfd2-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="2cfd2-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="2cfd2-198">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-198">Station Wagon</span></span> |
| <span data-ttu-id="2cfd2-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="2cfd2-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="2cfd2-200">Compact Car</span><span class="sxs-lookup"><span data-stu-id="2cfd2-200">Compact Car</span></span> |
| <span data-ttu-id="2cfd2-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="2cfd2-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="2cfd2-202">Small SUV</span><span class="sxs-lookup"><span data-stu-id="2cfd2-202">Small SUV</span></span> |
| <span data-ttu-id="2cfd2-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="2cfd2-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="2cfd2-204">Sports Car</span><span class="sxs-lookup"><span data-stu-id="2cfd2-204">Sports Car</span></span> |
| <span data-ttu-id="2cfd2-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="2cfd2-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="2cfd2-206">Medium SUV</span><span class="sxs-lookup"><span data-stu-id="2cfd2-206">Medium SUV</span></span> |
| <span data-ttu-id="2cfd2-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="2cfd2-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="2cfd2-208">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-208">Station Wagon</span></span> |
| <span data-ttu-id="2cfd2-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="2cfd2-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="2cfd2-210">Large SUV</span><span class="sxs-lookup"><span data-stu-id="2cfd2-210">Large SUV</span></span> |
| <span data-ttu-id="2cfd2-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="2cfd2-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="2cfd2-212">Large SUV</span><span class="sxs-lookup"><span data-stu-id="2cfd2-212">Large SUV</span></span> |
| <span data-ttu-id="2cfd2-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="2cfd2-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="2cfd2-214">Coupe</span><span class="sxs-lookup"><span data-stu-id="2cfd2-214">Coupe</span></span> |
| <span data-ttu-id="2cfd2-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="2cfd2-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="2cfd2-216">Sedan</span><span class="sxs-lookup"><span data-stu-id="2cfd2-216">Sedan</span></span> |
| <span data-ttu-id="2cfd2-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="2cfd2-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="2cfd2-218">Hybrid</span><span class="sxs-lookup"><span data-stu-id="2cfd2-218">Hybrid</span></span> |
| <span data-ttu-id="2cfd2-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="2cfd2-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="2cfd2-220">Family Saloon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-220">Family Saloon</span></span> |
| <span data-ttu-id="2cfd2-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="2cfd2-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="2cfd2-222">Sedan</span><span class="sxs-lookup"><span data-stu-id="2cfd2-222">Sedan</span></span> |
| <span data-ttu-id="2cfd2-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="2cfd2-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="2cfd2-224">Hybrid</span><span class="sxs-lookup"><span data-stu-id="2cfd2-224">Hybrid</span></span> |
| <span data-ttu-id="2cfd2-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="2cfd2-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="2cfd2-226">Family Saloon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-226">Family Saloon</span></span> |
| <span data-ttu-id="2cfd2-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="2cfd2-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="2cfd2-228">Sedan</span><span class="sxs-lookup"><span data-stu-id="2cfd2-228">Sedan</span></span> |
| <span data-ttu-id="2cfd2-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="2cfd2-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="2cfd2-230">Hybrid</span><span class="sxs-lookup"><span data-stu-id="2cfd2-230">Hybrid</span></span> |
| <span data-ttu-id="2cfd2-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="2cfd2-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="2cfd2-232">Family Saloon</span><span class="sxs-lookup"><span data-stu-id="2cfd2-232">Family Saloon</span></span> |
| <span data-ttu-id="2cfd2-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="2cfd2-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="2cfd2-234">Convertible</span><span class="sxs-lookup"><span data-stu-id="2cfd2-234">Convertible</span></span> |
| <span data-ttu-id="2cfd2-235">…….</span><span class="sxs-lookup"><span data-stu-id="2cfd2-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="2cfd2-236">References</span><span class="sxs-lookup"><span data-stu-id="2cfd2-236">References</span></span>
[<span data-ttu-id="2cfd2-237">Vehicle Telematics Simulator Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="2cfd2-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="2cfd2-238">Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="2cfd2-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="2cfd2-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2cfd2-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="2cfd2-240">Ingestion</span><span class="sxs-lookup"><span data-stu-id="2cfd2-240">Ingestion</span></span>
<span data-ttu-id="2cfd2-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="2cfd2-242">All these components are created and configured as part of the solution deployment.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="2cfd2-243">Real-time analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-243">Real-time analysis</span></span>
<span data-ttu-id="2cfd2-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="2cfd2-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Event hub dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="2cfd2-247">*Figure 4 - Event Hub dashboard*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-247">*Figure 4 - Event Hub dashboard*</span></span>

![Stream Analytics job processing data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="2cfd2-249">*Figure 5 - Stream Analytics job processing data*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="2cfd2-250">The Stream Analytics job;</span><span class="sxs-lookup"><span data-stu-id="2cfd2-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="2cfd2-251">ingests data from the Event Hub</span><span class="sxs-lookup"><span data-stu-id="2cfd2-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="2cfd2-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span><span class="sxs-lookup"><span data-stu-id="2cfd2-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="2cfd2-253">persists them into Azure blob storage for rich batch analytics.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="2cfd2-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Stream Analytics job query for data ingestion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="2cfd2-256">*Figure 6 - Stream Analytics job query for data ingestion*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="2cfd2-257">Batch analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-257">Batch analysis</span></span>
<span data-ttu-id="2cfd2-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="2cfd2-259">This is required to ensure a good representative data volume for batch processing.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="2cfd2-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="2cfd2-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Prepare sample data for batch processing workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="2cfd2-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="2cfd2-264">The pipeline consists of a custom ADF .Net Activity, show here:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="2cfd2-266">*Figure 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="2cfd2-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="2cfd2-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![PrepareSampleDataPipeline output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="2cfd2-270">*Figure 9 - PrepareSampleDataPipeline Output*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="2cfd2-271">References</span><span class="sxs-lookup"><span data-stu-id="2cfd2-271">References</span></span>
[<span data-ttu-id="2cfd2-272">Azure Event Hub SDK for stream ingestion</span><span class="sxs-lookup"><span data-stu-id="2cfd2-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="2cfd2-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="2cfd2-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="2cfd2-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span><span class="sxs-lookup"><span data-stu-id="2cfd2-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="2cfd2-275">Partition the dataset</span><span class="sxs-lookup"><span data-stu-id="2cfd2-275">Partition the dataset</span></span>
<span data-ttu-id="2cfd2-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="2cfd2-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="2cfd2-278">This step in the solution is applicable only to batch processing.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="2cfd2-279">Input and output data data management:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-279">Input and output data data management:</span></span>

* <span data-ttu-id="2cfd2-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span><span class="sxs-lookup"><span data-stu-id="2cfd2-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="2cfd2-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Partition car events workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="2cfd2-283">*Figure 10 – Partition Car Events workflow*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="2cfd2-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="2cfd2-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="2cfd2-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="2cfd2-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="2cfd2-288">*Figure 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="2cfd2-289">***PartitionConnectedCarEvents Hive Script***</span><span class="sxs-lookup"><span data-stu-id="2cfd2-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="2cfd2-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="2cfd2-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Partitioned output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="2cfd2-293">*Figure 12 - Partitioned Output*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="2cfd2-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="2cfd2-295">Data Analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-295">Data Analysis</span></span>
<span data-ttu-id="2cfd2-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="2cfd2-297">There are three subsections here:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-297">There are three subsections here:</span></span>

1. <span data-ttu-id="2cfd2-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="2cfd2-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="2cfd2-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="2cfd2-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2cfd2-301">Machine Learning</span></span>
<span data-ttu-id="2cfd2-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="2cfd2-303">We make the following assumptions</span><span class="sxs-lookup"><span data-stu-id="2cfd2-303">We make the following assumptions</span></span>

* <span data-ttu-id="2cfd2-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="2cfd2-305">Tire pressure is low</span><span class="sxs-lookup"><span data-stu-id="2cfd2-305">Tire pressure is low</span></span>
  * <span data-ttu-id="2cfd2-306">Engine oil level is low</span><span class="sxs-lookup"><span data-stu-id="2cfd2-306">Engine oil level is low</span></span>
  * <span data-ttu-id="2cfd2-307">Engine temperature is high</span><span class="sxs-lookup"><span data-stu-id="2cfd2-307">Engine temperature is high</span></span>
* <span data-ttu-id="2cfd2-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="2cfd2-309">Engine temperature is high but outside temperature is low</span><span class="sxs-lookup"><span data-stu-id="2cfd2-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="2cfd2-310">Engine temperature is low but outside temperature is high</span><span class="sxs-lookup"><span data-stu-id="2cfd2-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="2cfd2-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="2cfd2-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="2cfd2-313">**Maintenance detection model**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-313">**Maintenance detection model**</span></span>

<span data-ttu-id="2cfd2-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="2cfd2-315">As a result, we only need to consider these three variables in building the model.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="2cfd2-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="2cfd2-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="2cfd2-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="2cfd2-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="2cfd2-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="2cfd2-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="2cfd2-322">This normalized error is the anomaly score.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="2cfd2-323">The higher the error, the more anomalous the instance is.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="2cfd2-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="2cfd2-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="2cfd2-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="2cfd2-327">This parameter plays an important role in applying PCA-based anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="2cfd2-328">After projecting data using PCA, we can identify these anomalies more easily.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="2cfd2-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="2cfd2-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="2cfd2-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="2cfd2-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="2cfd2-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="2cfd2-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="2cfd2-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="2cfd2-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="2cfd2-337">Real-time analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-337">Real-time analysis</span></span>
<span data-ttu-id="2cfd2-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="2cfd2-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Stream Analytics query for real-time processing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="2cfd2-341">*Figure 13 – Stream Analytics query for real-time processing*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="2cfd2-342">All the averages are calculated over a 3-second TumblingWindow.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="2cfd2-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="2cfd2-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cfd2-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="2cfd2-345">**Real-time prediction**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-345">**Real-time prediction**</span></span>

<span data-ttu-id="2cfd2-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="2cfd2-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="2cfd2-348">The application performs the following:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-348">The application performs the following:</span></span>

1. <span data-ttu-id="2cfd2-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="2cfd2-350">![Stream Analytics query for publishing the data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-350">![Stream Analytics query for publishing the data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="2cfd2-351">For every event that this application receives:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="2cfd2-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="2cfd2-353">The RRS endpoint is automatically published as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="2cfd2-354">The RRS output is published to a Power BI dataset using the push APIs.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="2cfd2-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="2cfd2-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="2cfd2-357">**To execute the Real-time Dashboard Application**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="2cfd2-358">Extract and save locally ![RealtimeDashboardApp folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-358">Extract and save locally ![RealtimeDashboardApp folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="2cfd2-359">Execute the application RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="2cfd2-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="2cfd2-360">Provide valid Power BI credentials, sign in and click Accept</span><span class="sxs-lookup"><span data-stu-id="2cfd2-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Real-time dashboard app sign-in to Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Real-time dashboard app finish sign-in to Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="2cfd2-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="2cfd2-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="2cfd2-365">Batch analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-365">Batch analysis</span></span>
<span data-ttu-id="2cfd2-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="2cfd2-367">This makes it possible to:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-367">This makes it possible to:</span></span>

* <span data-ttu-id="2cfd2-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span><span class="sxs-lookup"><span data-stu-id="2cfd2-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="2cfd2-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span><span class="sxs-lookup"><span data-stu-id="2cfd2-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="2cfd2-370">In this solution, we are targeting the following metrics:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="2cfd2-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="2cfd2-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="2cfd2-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="2cfd2-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="2cfd2-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span><span class="sxs-lookup"><span data-stu-id="2cfd2-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="2cfd2-376">Let's look into the details of each of these metrics,</span><span class="sxs-lookup"><span data-stu-id="2cfd2-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="2cfd2-377">**Aggressive driving pattern**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="2cfd2-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="2cfd2-379">![Aggressive driving pattern workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-379">![Aggressive driving pattern workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="2cfd2-380">***Aggressive driving pattern Hive query***</span><span class="sxs-lookup"><span data-stu-id="2cfd2-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="2cfd2-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="2cfd2-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="2cfd2-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![AggressiveDrivingPatternPipeline output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="2cfd2-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="2cfd2-386">**Fuel efficient driving pattern**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="2cfd2-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="2cfd2-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="2cfd2-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Fuel-efficient driving pattern](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="2cfd2-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="2cfd2-391">***Fuel efficient driving pattern Hive query***</span><span class="sxs-lookup"><span data-stu-id="2cfd2-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="2cfd2-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="2cfd2-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="2cfd2-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![FuelEfficientDrivingPatternPipeline output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="2cfd2-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="2cfd2-397">**Recall Predictions**</span><span class="sxs-lookup"><span data-stu-id="2cfd2-397">**Recall Predictions**</span></span>

<span data-ttu-id="2cfd2-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="2cfd2-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Machine Learning endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="2cfd2-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="2cfd2-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Machine Learning batch scoring activity in data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="2cfd2-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="2cfd2-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline for predicting vehicles requiring recalls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="2cfd2-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="2cfd2-408">***Anomaly detection Hive query***</span><span class="sxs-lookup"><span data-stu-id="2cfd2-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="2cfd2-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="2cfd2-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![DetectAnomalyPipeline output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="2cfd2-412">*Figure 25 – DetectAnomalyPipeline output*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="2cfd2-413">Publish</span><span class="sxs-lookup"><span data-stu-id="2cfd2-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="2cfd2-414">Real-time analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-414">Real-time analysis</span></span>
<span data-ttu-id="2cfd2-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Stream Analytics job publishes to an output Event Hub instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="2cfd2-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Stream Analytics query to publish to the output Event Hub instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="2cfd2-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="2cfd2-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="2cfd2-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="2cfd2-422">Batch analysis</span><span class="sxs-lookup"><span data-stu-id="2cfd2-422">Batch analysis</span></span>
<span data-ttu-id="2cfd2-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="2cfd2-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Batch processing results copy to data mart workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="2cfd2-426">*Figure 28 – Batch processing results copy to data mart workflow*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Stream Analytics job publishes to data mart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="2cfd2-428">*Figure 29 – Stream Analytics job publishes to data mart*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Data mart setting in Stream Analytics job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="2cfd2-430">*Figure 30 – Data mart setting in Stream Analytics job*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="2cfd2-431">Consume</span><span class="sxs-lookup"><span data-stu-id="2cfd2-431">Consume</span></span>
<span data-ttu-id="2cfd2-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="2cfd2-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="2cfd2-434">The final dashboard looks like this:</span><span class="sxs-lookup"><span data-stu-id="2cfd2-434">The final dashboard looks like this:</span></span>

![Power BI dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="2cfd2-436">*Figure 31 - Power BI Dashboard*</span><span class="sxs-lookup"><span data-stu-id="2cfd2-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="2cfd2-437">Summary</span><span class="sxs-lookup"><span data-stu-id="2cfd2-437">Summary</span></span>
<span data-ttu-id="2cfd2-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="2cfd2-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="2cfd2-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span><span class="sxs-lookup"><span data-stu-id="2cfd2-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 






























