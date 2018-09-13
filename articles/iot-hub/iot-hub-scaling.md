---
title: Azure IoT Hub scaling | Microsoft Docs
description: How to scale your IoT hub to support your anticipated message throughput. Includes a summary of the supported throughput for each tier and options for sharding.
services: iot-hub
documentationcenter: ''
author: fsautomata
manager: timlt
editor: ''
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/19/2016
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cbff931e7acc88b29ed6f51a16156b44c1596d3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553485"
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="45833-104">Scale your IoT hub solution</span><span class="sxs-lookup"><span data-stu-id="45833-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="45833-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span><span class="sxs-lookup"><span data-stu-id="45833-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="45833-106">For more information, see [IoT Hub pricing][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="45833-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="45833-107">Each IoT Hub unit allows a certain number of daily messages.</span><span class="sxs-lookup"><span data-stu-id="45833-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="45833-108">To properly scale your solution, consider your particular use of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="45833-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="45833-109">In particular, consider the required peak throughput for the following categories of operations:</span><span class="sxs-lookup"><span data-stu-id="45833-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="45833-110">Device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="45833-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="45833-111">Cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="45833-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="45833-112">Identity registry operations</span><span class="sxs-lookup"><span data-stu-id="45833-112">Identity registry operations</span></span>

<span data-ttu-id="45833-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span><span class="sxs-lookup"><span data-stu-id="45833-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="45833-114">Device-to-cloud and cloud-to-device message throughput</span><span class="sxs-lookup"><span data-stu-id="45833-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="45833-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span><span class="sxs-lookup"><span data-stu-id="45833-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="45833-116">Device-to-cloud messages follow these sustained throughput guidelines.</span><span class="sxs-lookup"><span data-stu-id="45833-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="45833-117">Tier</span><span class="sxs-lookup"><span data-stu-id="45833-117">Tier</span></span> | <span data-ttu-id="45833-118">Sustained throughput</span><span class="sxs-lookup"><span data-stu-id="45833-118">Sustained throughput</span></span> | <span data-ttu-id="45833-119">Sustained send rate</span><span class="sxs-lookup"><span data-stu-id="45833-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="45833-120">S1</span><span class="sxs-lookup"><span data-stu-id="45833-120">S1</span></span> |<span data-ttu-id="45833-121">Up to 1111 KB/minute per unit</span><span class="sxs-lookup"><span data-stu-id="45833-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="45833-122">(1.5 GB/day/unit)</span><span class="sxs-lookup"><span data-stu-id="45833-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="45833-123">Average of 278 messages/minute per unit</span><span class="sxs-lookup"><span data-stu-id="45833-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="45833-124">(400,000 messages/day per unit)</span><span class="sxs-lookup"><span data-stu-id="45833-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="45833-125">S2</span><span class="sxs-lookup"><span data-stu-id="45833-125">S2</span></span> |<span data-ttu-id="45833-126">Up to 16 MB/minute per unit</span><span class="sxs-lookup"><span data-stu-id="45833-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="45833-127">(22.8 GB/day/unit)</span><span class="sxs-lookup"><span data-stu-id="45833-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="45833-128">Average of 4167 messages/minute per unit</span><span class="sxs-lookup"><span data-stu-id="45833-128">Average of 4167 messages/minute per unit</span></span><br/><span data-ttu-id="45833-129">(6 million messages/day per unit)</span><span class="sxs-lookup"><span data-stu-id="45833-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="45833-130">S3</span><span class="sxs-lookup"><span data-stu-id="45833-130">S3</span></span> |<span data-ttu-id="45833-131">Up to 814 MB/minute per unit</span><span class="sxs-lookup"><span data-stu-id="45833-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="45833-132">(1144.4 GB/day/unit)</span><span class="sxs-lookup"><span data-stu-id="45833-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="45833-133">Average of 208,333 messages/minute per unit</span><span class="sxs-lookup"><span data-stu-id="45833-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="45833-134">(300 million messages/day per unit)</span><span class="sxs-lookup"><span data-stu-id="45833-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="45833-135">Identity registry operation throughput</span><span class="sxs-lookup"><span data-stu-id="45833-135">Identity registry operation throughput</span></span>
<span data-ttu-id="45833-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span><span class="sxs-lookup"><span data-stu-id="45833-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="45833-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="45833-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="45833-138">Sharding</span><span class="sxs-lookup"><span data-stu-id="45833-138">Sharding</span></span>
<span data-ttu-id="45833-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span><span class="sxs-lookup"><span data-stu-id="45833-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="45833-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="45833-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="45833-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span><span class="sxs-lookup"><span data-stu-id="45833-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45833-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="45833-142">Next steps</span></span>
<span data-ttu-id="45833-143">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="45833-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="45833-144">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="45833-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="45833-145">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="45833-145">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
