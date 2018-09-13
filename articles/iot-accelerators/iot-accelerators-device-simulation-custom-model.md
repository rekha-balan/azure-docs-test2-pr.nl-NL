---
title: Configure a custom device model - Azure | Microsoft Docs
description: This article describes how to configure a custom device model in the Device Simulation solution accelerator.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 07/06/2018
ms.topic: conceptual
ms.openlocfilehash: 61a7c5314df541b4b44a286efe982f4bf93256e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855920"
---
# <a name="device-models"></a><span data-ttu-id="d8c5f-103">Device models</span><span class="sxs-lookup"><span data-stu-id="d8c5f-103">Device models</span></span>

<span data-ttu-id="d8c5f-104">When you configure a simulation you can choose to use an existing device model with a predefined set of sensors, or create a custom device model with your choice of simulated sensors.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-104">When you configure a simulation you can choose to use an existing device model with a predefined set of sensors, or create a custom device model with your choice of simulated sensors.</span></span> <span data-ttu-id="d8c5f-105">Custom sensors let you more closely model your real devices.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-105">Custom sensors let you more closely model your real devices.</span></span>

## <a name="pre-configured-device-models"></a><span data-ttu-id="d8c5f-106">Pre-configured device models</span><span class="sxs-lookup"><span data-stu-id="d8c5f-106">Pre-configured device models</span></span>

<span data-ttu-id="d8c5f-107">The Device Simulation solution accelerator provides three pre-configured device models: Chillers, Elevators, and Trucks.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-107">The Device Simulation solution accelerator provides three pre-configured device models: Chillers, Elevators, and Trucks.</span></span>

<span data-ttu-id="d8c5f-108">Pre-configured device models have multiple sensors with advanced behaviors defined in a JavaScript file.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-108">Pre-configured device models have multiple sensors with advanced behaviors defined in a JavaScript file.</span></span> <span data-ttu-id="d8c5f-109">You cannot configure these behaviors in the web UI.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-109">You cannot configure these behaviors in the web UI.</span></span>

<span data-ttu-id="d8c5f-110">The following table shows the configurations for each pre-configured device model:</span><span class="sxs-lookup"><span data-stu-id="d8c5f-110">The following table shows the configurations for each pre-configured device model:</span></span>

| <span data-ttu-id="d8c5f-111">Device model</span><span class="sxs-lookup"><span data-stu-id="d8c5f-111">Device model</span></span>  | <span data-ttu-id="d8c5f-112">Sensor</span><span class="sxs-lookup"><span data-stu-id="d8c5f-112">Sensor</span></span>           | <span data-ttu-id="d8c5f-113">Unit</span><span class="sxs-lookup"><span data-stu-id="d8c5f-113">Unit</span></span>  |
| ------------- | ---------------- | ----- |
| <span data-ttu-id="d8c5f-114">Chiller</span><span class="sxs-lookup"><span data-stu-id="d8c5f-114">Chiller</span></span>       | <span data-ttu-id="d8c5f-115">humidity</span><span class="sxs-lookup"><span data-stu-id="d8c5f-115">humidity</span></span>         | %     |
|               | <span data-ttu-id="d8c5f-116">pressure</span><span class="sxs-lookup"><span data-stu-id="d8c5f-116">pressure</span></span>         | <span data-ttu-id="d8c5f-117">psig</span><span class="sxs-lookup"><span data-stu-id="d8c5f-117">psig</span></span>  |
|               | <span data-ttu-id="d8c5f-118">temperature</span><span class="sxs-lookup"><span data-stu-id="d8c5f-118">temperature</span></span>      | <span data-ttu-id="d8c5f-119">F</span><span class="sxs-lookup"><span data-stu-id="d8c5f-119">F</span></span>     |
| <span data-ttu-id="d8c5f-120">Elevator</span><span class="sxs-lookup"><span data-stu-id="d8c5f-120">Elevator</span></span>      | <span data-ttu-id="d8c5f-121">Floor</span><span class="sxs-lookup"><span data-stu-id="d8c5f-121">Floor</span></span>            |       |
|               | <span data-ttu-id="d8c5f-122">Vibration</span><span class="sxs-lookup"><span data-stu-id="d8c5f-122">Vibration</span></span>        | <span data-ttu-id="d8c5f-123">mm</span><span class="sxs-lookup"><span data-stu-id="d8c5f-123">mm</span></span>    |
|               | <span data-ttu-id="d8c5f-124">Temperature</span><span class="sxs-lookup"><span data-stu-id="d8c5f-124">Temperature</span></span>      | <span data-ttu-id="d8c5f-125">F</span><span class="sxs-lookup"><span data-stu-id="d8c5f-125">F</span></span>     |
| <span data-ttu-id="d8c5f-126">Truck</span><span class="sxs-lookup"><span data-stu-id="d8c5f-126">Truck</span></span>         | <span data-ttu-id="d8c5f-127">Latitude</span><span class="sxs-lookup"><span data-stu-id="d8c5f-127">Latitude</span></span>         |       |
|               | <span data-ttu-id="d8c5f-128">Longitude</span><span class="sxs-lookup"><span data-stu-id="d8c5f-128">Longitude</span></span>        |       |
|               | <span data-ttu-id="d8c5f-129">speed</span><span class="sxs-lookup"><span data-stu-id="d8c5f-129">speed</span></span>            | <span data-ttu-id="d8c5f-130">mph</span><span class="sxs-lookup"><span data-stu-id="d8c5f-130">mph</span></span>   |
|               | <span data-ttu-id="d8c5f-131">cargotemperature</span><span class="sxs-lookup"><span data-stu-id="d8c5f-131">cargotemperature</span></span> | <span data-ttu-id="d8c5f-132">F</span><span class="sxs-lookup"><span data-stu-id="d8c5f-132">F</span></span>     |

## <a name="custom-device-models"></a><span data-ttu-id="d8c5f-133">Custom device models</span><span class="sxs-lookup"><span data-stu-id="d8c5f-133">Custom device models</span></span>

<span data-ttu-id="d8c5f-134">Custom device models let you model sensors that more closely model your own devices.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-134">Custom device models let you model sensors that more closely model your own devices.</span></span> <span data-ttu-id="d8c5f-135">A custom device can have up to 10 custom sensors.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-135">A custom device can have up to 10 custom sensors.</span></span>

<span data-ttu-id="d8c5f-136">When you select the custom device model type, you add new sensors by clicking **+Add sensor**.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-136">When you select the custom device model type, you add new sensors by clicking **+Add sensor**.</span></span>

<span data-ttu-id="d8c5f-137">[![Configure sensors](./media/iot-accelerators-device-simulation-custom-model/configuresensors-inline.png)](./media/iot-accelerators-device-simulation-custom-model/configuresensors-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d8c5f-137">[![Configure sensors](./media/iot-accelerators-device-simulation-custom-model/configuresensors-inline.png)](./media/iot-accelerators-device-simulation-custom-model/configuresensors-expanded.png#lightbox)</span></span>

<span data-ttu-id="d8c5f-138">Custom sensors have the following properties:</span><span class="sxs-lookup"><span data-stu-id="d8c5f-138">Custom sensors have the following properties:</span></span>

| <span data-ttu-id="d8c5f-139">Field</span><span class="sxs-lookup"><span data-stu-id="d8c5f-139">Field</span></span>     | <span data-ttu-id="d8c5f-140">Description</span><span class="sxs-lookup"><span data-stu-id="d8c5f-140">Description</span></span> |
| --------- | ----------- |
| <span data-ttu-id="d8c5f-141">Sensor Name</span><span class="sxs-lookup"><span data-stu-id="d8c5f-141">Sensor Name</span></span> | <span data-ttu-id="d8c5f-142">A friendly name for the sensor such as **temperature** or **speed**.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-142">A friendly name for the sensor such as **temperature** or **speed**.</span></span>  |
| <span data-ttu-id="d8c5f-143">Behavior</span><span class="sxs-lookup"><span data-stu-id="d8c5f-143">Behavior</span></span>  | <span data-ttu-id="d8c5f-144">Behaviors enable telemetry data to vary from one message to the next to simulate real-world data.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-144">Behaviors enable telemetry data to vary from one message to the next to simulate real-world data.</span></span> <span data-ttu-id="d8c5f-145">**Increment** increases the value by one in each message sent starting at the minimum value.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-145">**Increment** increases the value by one in each message sent starting at the minimum value.</span></span> <span data-ttu-id="d8c5f-146">Once the maximum value is met, then it starts over again at the minimum value.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-146">Once the maximum value is met, then it starts over again at the minimum value.</span></span> <span data-ttu-id="d8c5f-147">**Decrement** behaves in the same way as **Increment** but counts down.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-147">**Decrement** behaves in the same way as **Increment** but counts down.</span></span> <span data-ttu-id="d8c5f-148">The **Random** behavior generates a random value between the minimum value and maximum values.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-148">The **Random** behavior generates a random value between the minimum value and maximum values.</span></span> |
| <span data-ttu-id="d8c5f-149">Min Value</span><span class="sxs-lookup"><span data-stu-id="d8c5f-149">Min Value</span></span> | <span data-ttu-id="d8c5f-150">The lowest number in your acceptable range.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-150">The lowest number in your acceptable range.</span></span> |
| <span data-ttu-id="d8c5f-151">Max Value</span><span class="sxs-lookup"><span data-stu-id="d8c5f-151">Max Value</span></span> | <span data-ttu-id="d8c5f-152">The largest number in your acceptable range.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-152">The largest number in your acceptable range.</span></span> |
| <span data-ttu-id="d8c5f-153">Unit</span><span class="sxs-lookup"><span data-stu-id="d8c5f-153">Unit</span></span>      | <span data-ttu-id="d8c5f-154">The unit of measurement for the sensor such as °F or MPH.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-154">The unit of measurement for the sensor such as °F or MPH.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d8c5f-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8c5f-155">Next steps</span></span>

<span data-ttu-id="d8c5f-156">In this how-to guide, you've learned how to configure a custom device model for a simulation.</span><span class="sxs-lookup"><span data-stu-id="d8c5f-156">In this how-to guide, you've learned how to configure a custom device model for a simulation.</span></span> <span data-ttu-id="d8c5f-157">Next, you may want to explore some of the other [IoT solution accelerators](about-iot-accelerators.md).</span><span class="sxs-lookup"><span data-stu-id="d8c5f-157">Next, you may want to explore some of the other [IoT solution accelerators](about-iot-accelerators.md).</span></span>