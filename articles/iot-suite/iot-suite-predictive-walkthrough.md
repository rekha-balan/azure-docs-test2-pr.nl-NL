---
title: Predictive maintenance walkthrough | Microsoft Docs
description: A walkthrough of the Azure IoT predictive maintenance preconfigured solution.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: dobett
ms.openlocfilehash: 7cfe03de467064c5a6875b7de87a586a80d08fd9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550724"
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a><span data-ttu-id="1c630-103">Predictive maintenance preconfigured solution walkthrough</span><span class="sxs-lookup"><span data-stu-id="1c630-103">Predictive maintenance preconfigured solution walkthrough</span></span>

## <a name="introduction"></a><span data-ttu-id="1c630-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="1c630-104">Introduction</span></span>

<span data-ttu-id="1c630-105">The IoT Suite predictive maintenance preconfigured solution is an end-to-end solution for a business scenario that predicts the point at which a failure is likely to occur.</span><span class="sxs-lookup"><span data-stu-id="1c630-105">The IoT Suite predictive maintenance preconfigured solution is an end-to-end solution for a business scenario that predicts the point at which a failure is likely to occur.</span></span> <span data-ttu-id="1c630-106">You can use this preconfigured solution proactively for activities such as optimizing maintenance.</span><span class="sxs-lookup"><span data-stu-id="1c630-106">You can use this preconfigured solution proactively for activities such as optimizing maintenance.</span></span> <span data-ttu-id="1c630-107">The solution combines key Azure IoT Suite services, such as IoT Hub, Stream analytics, and an [Azure Machine Learning][lnk-machine-learning] workspace.</span><span class="sxs-lookup"><span data-stu-id="1c630-107">The solution combines key Azure IoT Suite services, such as IoT Hub, Stream analytics, and an [Azure Machine Learning][lnk-machine-learning] workspace.</span></span> <span data-ttu-id="1c630-108">This workspace contains a model, based on a public sample data set, to predict the Remaining Useful Life (RUL) of an aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="1c630-108">This workspace contains a model, based on a public sample data set, to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="1c630-109">The solution fully implements the IoT business scenario as a starting point for you to plan and implement a solution that meets your own specific business requirements.</span><span class="sxs-lookup"><span data-stu-id="1c630-109">The solution fully implements the IoT business scenario as a starting point for you to plan and implement a solution that meets your own specific business requirements.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="1c630-110">Logical architecture</span><span class="sxs-lookup"><span data-stu-id="1c630-110">Logical architecture</span></span>

<span data-ttu-id="1c630-111">The following diagram outlines the logical components of the preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="1c630-111">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![][img-architecture]

<span data-ttu-id="1c630-112">The blue items are Azure services that are provisioned in the region you select when you provision the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="1c630-112">The blue items are Azure services that are provisioned in the region you select when you provision the preconfigured solution.</span></span> <span data-ttu-id="1c630-113">The list of regions where you can deploy the preconfigured solution displays on the [provisioning page][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="1c630-113">The list of regions where you can deploy the preconfigured solution displays on the [provisioning page][lnk-azureiotsuite].</span></span>

<span data-ttu-id="1c630-114">The green item is a simulated device that represents an aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="1c630-114">The green item is a simulated device that represents an aircraft engine.</span></span> <span data-ttu-id="1c630-115">You can learn more about these simulated devices in the following section.</span><span class="sxs-lookup"><span data-stu-id="1c630-115">You can learn more about these simulated devices in the following section.</span></span>

<span data-ttu-id="1c630-116">The gray items represent components that implement *device management* capabilities.</span><span class="sxs-lookup"><span data-stu-id="1c630-116">The gray items represent components that implement *device management* capabilities.</span></span> <span data-ttu-id="1c630-117">The current release of the predictive maintenance preconfigured solution does not provision these resources.</span><span class="sxs-lookup"><span data-stu-id="1c630-117">The current release of the predictive maintenance preconfigured solution does not provision these resources.</span></span> <span data-ttu-id="1c630-118">To learn more about device management, refer to the [remote monitoring pre-configured solution][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="1c630-118">To learn more about device management, refer to the [remote monitoring pre-configured solution][lnk-remote-monitoring].</span></span>

## <a name="simulated-devices"></a><span data-ttu-id="1c630-119">Simulated devices</span><span class="sxs-lookup"><span data-stu-id="1c630-119">Simulated devices</span></span>

<span data-ttu-id="1c630-120">In the preconfigured solution, a simulated device represents an aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="1c630-120">In the preconfigured solution, a simulated device represents an aircraft engine.</span></span> <span data-ttu-id="1c630-121">The solution is provisioned with two engines that map to a single aircraft.</span><span class="sxs-lookup"><span data-stu-id="1c630-121">The solution is provisioned with two engines that map to a single aircraft.</span></span> <span data-ttu-id="1c630-122">Each engine emits four types of telemetry: Sensor 9, Sensor 11, Sensor 14, and Sensor 15 provide the data necessary for the Machine Learning model to calculate the RUL for the engine.</span><span class="sxs-lookup"><span data-stu-id="1c630-122">Each engine emits four types of telemetry: Sensor 9, Sensor 11, Sensor 14, and Sensor 15 provide the data necessary for the Machine Learning model to calculate the RUL for the engine.</span></span> <span data-ttu-id="1c630-123">Each simulated device sends the following telemetry messages to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="1c630-123">Each simulated device sends the following telemetry messages to IoT Hub:</span></span>

<span data-ttu-id="1c630-124">*Cycle count*.</span><span class="sxs-lookup"><span data-stu-id="1c630-124">*Cycle count*.</span></span> <span data-ttu-id="1c630-125">A cycle represents a completed flight with a duration between two and ten hours.</span><span class="sxs-lookup"><span data-stu-id="1c630-125">A cycle represents a completed flight with a duration between two and ten hours.</span></span> <span data-ttu-id="1c630-126">During the flight, telemetry data is captured every half hour.</span><span class="sxs-lookup"><span data-stu-id="1c630-126">During the flight, telemetry data is captured every half hour.</span></span>

<span data-ttu-id="1c630-127">*Telemetry*.</span><span class="sxs-lookup"><span data-stu-id="1c630-127">*Telemetry*.</span></span> <span data-ttu-id="1c630-128">There are four sensors that represent engine attributes.</span><span class="sxs-lookup"><span data-stu-id="1c630-128">There are four sensors that represent engine attributes.</span></span> <span data-ttu-id="1c630-129">The sensors are generically labeled Sensor 9, Sensor 11, Sensor 14, and Sensor 15.</span><span class="sxs-lookup"><span data-stu-id="1c630-129">The sensors are generically labeled Sensor 9, Sensor 11, Sensor 14, and Sensor 15.</span></span> <span data-ttu-id="1c630-130">These four sensors represent telemetry sufficient to obtain useful results from the RUL model.</span><span class="sxs-lookup"><span data-stu-id="1c630-130">These four sensors represent telemetry sufficient to obtain useful results from the RUL model.</span></span> <span data-ttu-id="1c630-131">The model used in the preconfigured solution is created from a public data set that includes real engine sensor data.</span><span class="sxs-lookup"><span data-stu-id="1c630-131">The model used in the preconfigured solution is created from a public data set that includes real engine sensor data.</span></span> <span data-ttu-id="1c630-132">For more information on how the model was created from the original data set, see the [Cortana Intelligence Gallery Predictive Maintenance Template][lnk-cortana-analytics].</span><span class="sxs-lookup"><span data-stu-id="1c630-132">For more information on how the model was created from the original data set, see the [Cortana Intelligence Gallery Predictive Maintenance Template][lnk-cortana-analytics].</span></span>

<span data-ttu-id="1c630-133">The simulated devices can handle the following commands sent from the IoT hub in the solution:</span><span class="sxs-lookup"><span data-stu-id="1c630-133">The simulated devices can handle the following commands sent from the IoT hub in the solution:</span></span>

| <span data-ttu-id="1c630-134">Command</span><span class="sxs-lookup"><span data-stu-id="1c630-134">Command</span></span> | <span data-ttu-id="1c630-135">Description</span><span class="sxs-lookup"><span data-stu-id="1c630-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c630-136">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="1c630-136">StartTelemetry</span></span> |<span data-ttu-id="1c630-137">Controls the state of the simulation.</span><span class="sxs-lookup"><span data-stu-id="1c630-137">Controls the state of the simulation.</span></span><br/><span data-ttu-id="1c630-138">Starts the device sending telemetry</span><span class="sxs-lookup"><span data-stu-id="1c630-138">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="1c630-139">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="1c630-139">StopTelemetry</span></span> |<span data-ttu-id="1c630-140">Controls the state of the simulation.</span><span class="sxs-lookup"><span data-stu-id="1c630-140">Controls the state of the simulation.</span></span><br/><span data-ttu-id="1c630-141">Stops the device sending telemetry</span><span class="sxs-lookup"><span data-stu-id="1c630-141">Stops the device sending telemetry</span></span> |

<span data-ttu-id="1c630-142">IoT Hub provides device command acknowledgment.</span><span class="sxs-lookup"><span data-stu-id="1c630-142">IoT Hub provides device command acknowledgment.</span></span>

## <a name="azure-stream-analytics-job"></a><span data-ttu-id="1c630-143">Azure Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c630-143">Azure Stream Analytics job</span></span>
<span data-ttu-id="1c630-144">**Job: Telemetry** operates on the incoming device telemetry stream using two statements.</span><span class="sxs-lookup"><span data-stu-id="1c630-144">**Job: Telemetry** operates on the incoming device telemetry stream using two statements.</span></span> <span data-ttu-id="1c630-145">The first selects all telemetry from the devices and sends this data to blob storage from where it is visualized in the web app.</span><span class="sxs-lookup"><span data-stu-id="1c630-145">The first selects all telemetry from the devices and sends this data to blob storage from where it is visualized in the web app.</span></span> <span data-ttu-id="1c630-146">The second statement computes average sensor values over a two-minute sliding window and sends this data through the Event hub to an **event processor**.</span><span class="sxs-lookup"><span data-stu-id="1c630-146">The second statement computes average sensor values over a two-minute sliding window and sends this data through the Event hub to an **event processor**.</span></span>

## <a name="event-processor"></a><span data-ttu-id="1c630-147">Event processor</span><span class="sxs-lookup"><span data-stu-id="1c630-147">Event processor</span></span>
<span data-ttu-id="1c630-148">The **event processor host** runs in an Azure Web Job.</span><span class="sxs-lookup"><span data-stu-id="1c630-148">The **event processor host** runs in an Azure Web Job.</span></span> <span data-ttu-id="1c630-149">The **event processor** takes the average sensor values for a completed cycle.</span><span class="sxs-lookup"><span data-stu-id="1c630-149">The **event processor** takes the average sensor values for a completed cycle.</span></span> <span data-ttu-id="1c630-150">It then passes those values to an API that exposes trained model to calculate the RUL for an engine.</span><span class="sxs-lookup"><span data-stu-id="1c630-150">It then passes those values to an API that exposes trained model to calculate the RUL for an engine.</span></span> <span data-ttu-id="1c630-151">The API is exposed by a Machine Learning workspace that is provisioned as part of the solution.</span><span class="sxs-lookup"><span data-stu-id="1c630-151">The API is exposed by a Machine Learning workspace that is provisioned as part of the solution.</span></span>

## <a name="machine-learning"></a><span data-ttu-id="1c630-152">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1c630-152">Machine Learning</span></span>
<span data-ttu-id="1c630-153">The Machine Learning component uses a model derived from data collected from real aircraft engines.</span><span class="sxs-lookup"><span data-stu-id="1c630-153">The Machine Learning component uses a model derived from data collected from real aircraft engines.</span></span> <span data-ttu-id="1c630-154">You can navigate to the Machine Learning workspace from the tile on the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution when it’s in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="1c630-154">You can navigate to the Machine Learning workspace from the tile on the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution when it’s in the **Ready** state.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1c630-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c630-155">Next steps</span></span>
<span data-ttu-id="1c630-156">Now you've seen the key components of the predictive maintenance preconfigured solution, you may want to customize it.</span><span class="sxs-lookup"><span data-stu-id="1c630-156">Now you've seen the key components of the predictive maintenance preconfigured solution, you may want to customize it.</span></span> <span data-ttu-id="1c630-157">See [Guidance on customizing preconfigured solutions][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="1c630-157">See [Guidance on customizing preconfigured solutions][lnk-customize].</span></span>

<span data-ttu-id="1c630-158">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="1c630-158">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="1c630-159">[Frequently asked questions for IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="1c630-159">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="1c630-160">[IoT security from the ground up][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="1c630-160">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-architecture]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/
