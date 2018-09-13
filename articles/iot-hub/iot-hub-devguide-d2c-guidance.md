---
title: Azure IoT Hub device-to-cloud options | Microsoft Docs
description: Developer guide - guidance on when to use device-to-cloud messages, reported properties, or file upload for cloud-to-device communications.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: ''
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: elioda
ms.openlocfilehash: aa3704fe844a41fef22b8cdd35838c68aebc7752
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661599"
---
# <a name="device-to-cloud-communications-guidance"></a><span data-ttu-id="0bde3-103">Device-to-cloud communications guidance</span><span class="sxs-lookup"><span data-stu-id="0bde3-103">Device-to-cloud communications guidance</span></span>
<span data-ttu-id="0bde3-104">When sending information from the device app to the solution back end, IoT Hub exposes three options:</span><span class="sxs-lookup"><span data-stu-id="0bde3-104">When sending information from the device app to the solution back end, IoT Hub exposes three options:</span></span>

* <span data-ttu-id="0bde3-105">[Device-to-cloud messages][lnk-d2c] for time series telemetry and alerts.</span><span class="sxs-lookup"><span data-stu-id="0bde3-105">[Device-to-cloud messages][lnk-d2c] for time series telemetry and alerts.</span></span>
* <span data-ttu-id="0bde3-106">[Reported properties][lnk-twins] for reporting device state information such as available capabilities, conditions, or the state of long-running workflows.</span><span class="sxs-lookup"><span data-stu-id="0bde3-106">[Reported properties][lnk-twins] for reporting device state information such as available capabilities, conditions, or the state of long-running workflows.</span></span> <span data-ttu-id="0bde3-107">For example, configuration and software updates.</span><span class="sxs-lookup"><span data-stu-id="0bde3-107">For example, configuration and software updates.</span></span>
* <span data-ttu-id="0bde3-108">[File uploads][lnk-fileupload] for media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span><span class="sxs-lookup"><span data-stu-id="0bde3-108">[File uploads][lnk-fileupload] for media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="0bde3-109">Here is a detailed comparison of the various device-to-cloud communication options.</span><span class="sxs-lookup"><span data-stu-id="0bde3-109">Here is a detailed comparison of the various device-to-cloud communication options.</span></span>

|  | <span data-ttu-id="0bde3-110">Device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="0bde3-110">Device-to-cloud messages</span></span> | <span data-ttu-id="0bde3-111">Reported properties</span><span class="sxs-lookup"><span data-stu-id="0bde3-111">Reported properties</span></span> | <span data-ttu-id="0bde3-112">File uploads</span><span class="sxs-lookup"><span data-stu-id="0bde3-112">File uploads</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="0bde3-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="0bde3-113">Scenario</span></span> | <span data-ttu-id="0bde3-114">Telemetry time series and alerts.</span><span class="sxs-lookup"><span data-stu-id="0bde3-114">Telemetry time series and alerts.</span></span> <span data-ttu-id="0bde3-115">For example, 256KB sensor data batches sent every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="0bde3-115">For example, 256KB sensor data batches sent every 5 minutes.</span></span> | <span data-ttu-id="0bde3-116">Available capabilities and conditions.</span><span class="sxs-lookup"><span data-stu-id="0bde3-116">Available capabilities and conditions.</span></span> <span data-ttu-id="0bde3-117">For example, the current device connectivity mode such as cellular or WiFi.</span><span class="sxs-lookup"><span data-stu-id="0bde3-117">For example, the current device connectivity mode such as cellular or WiFi.</span></span> <span data-ttu-id="0bde3-118">Synchronizing long-running workflows, such as configuration and software updates.</span><span class="sxs-lookup"><span data-stu-id="0bde3-118">Synchronizing long-running workflows, such as configuration and software updates.</span></span> | <span data-ttu-id="0bde3-119">Media files.</span><span class="sxs-lookup"><span data-stu-id="0bde3-119">Media files.</span></span> <span data-ttu-id="0bde3-120">Large (typically compressed) telemetry batches.</span><span class="sxs-lookup"><span data-stu-id="0bde3-120">Large (typically compressed) telemetry batches.</span></span> |
| <span data-ttu-id="0bde3-121">Storage and retrieval</span><span class="sxs-lookup"><span data-stu-id="0bde3-121">Storage and retrieval</span></span> | <span data-ttu-id="0bde3-122">Temporarily stored by IoT Hub, up to 7 days.</span><span class="sxs-lookup"><span data-stu-id="0bde3-122">Temporarily stored by IoT Hub, up to 7 days.</span></span> <span data-ttu-id="0bde3-123">Only sequential reading.</span><span class="sxs-lookup"><span data-stu-id="0bde3-123">Only sequential reading.</span></span> | <span data-ttu-id="0bde3-124">Stored by IoT Hub in the device twin.</span><span class="sxs-lookup"><span data-stu-id="0bde3-124">Stored by IoT Hub in the device twin.</span></span> <span data-ttu-id="0bde3-125">Retrievable using the [IoT Hub query language][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="0bde3-125">Retrievable using the [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="0bde3-126">Stored in user-provided Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0bde3-126">Stored in user-provided Azure Storage account.</span></span> |
| <span data-ttu-id="0bde3-127">Size</span><span class="sxs-lookup"><span data-stu-id="0bde3-127">Size</span></span> | <span data-ttu-id="0bde3-128">Up to 256KB messages.</span><span class="sxs-lookup"><span data-stu-id="0bde3-128">Up to 256KB messages.</span></span> | <span data-ttu-id="0bde3-129">Maximum reported properties size is 8KB.</span><span class="sxs-lookup"><span data-stu-id="0bde3-129">Maximum reported properties size is 8KB.</span></span> | <span data-ttu-id="0bde3-130">Maximum file size supported by Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0bde3-130">Maximum file size supported by Azure Blob Storage.</span></span> |
| <span data-ttu-id="0bde3-131">Frequency</span><span class="sxs-lookup"><span data-stu-id="0bde3-131">Frequency</span></span> | <span data-ttu-id="0bde3-132">High.</span><span class="sxs-lookup"><span data-stu-id="0bde3-132">High.</span></span> <span data-ttu-id="0bde3-133">For more information, see [IoT Hub limits][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="0bde3-133">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="0bde3-134">Medium.</span><span class="sxs-lookup"><span data-stu-id="0bde3-134">Medium.</span></span> <span data-ttu-id="0bde3-135">For more information, see [IoT Hub limits][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="0bde3-135">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="0bde3-136">Low.</span><span class="sxs-lookup"><span data-stu-id="0bde3-136">Low.</span></span> <span data-ttu-id="0bde3-137">For more information, see [IoT Hub limits][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="0bde3-137">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="0bde3-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="0bde3-138">Protocol</span></span> | <span data-ttu-id="0bde3-139">Available on all protocols.</span><span class="sxs-lookup"><span data-stu-id="0bde3-139">Available on all protocols.</span></span> | <span data-ttu-id="0bde3-140">Currently available only when using MQTT.</span><span class="sxs-lookup"><span data-stu-id="0bde3-140">Currently available only when using MQTT.</span></span> | <span data-ttu-id="0bde3-141">Available when using any protocol, but requires HTTP on the device.</span><span class="sxs-lookup"><span data-stu-id="0bde3-141">Available when using any protocol, but requires HTTP on the device.</span></span> |

<span data-ttu-id="0bde3-142">It is possible that an application requires to both send information as a telemetry time series or alert and also to make it available in the device twin.</span><span class="sxs-lookup"><span data-stu-id="0bde3-142">It is possible that an application requires to both send information as a telemetry time series or alert and also to make it available in the device twin.</span></span> <span data-ttu-id="0bde3-143">In this scenario, you can chose one of the following options:</span><span class="sxs-lookup"><span data-stu-id="0bde3-143">In this scenario, you can chose one of the following options:</span></span>

* <span data-ttu-id="0bde3-144">Either, the device app sends a device-to-cloud message and reports a property change.</span><span class="sxs-lookup"><span data-stu-id="0bde3-144">Either, the device app sends a device-to-cloud message and reports a property change.</span></span> 
* <span data-ttu-id="0bde3-145">Or, the solution back end can store the information in the device twin's tags when it receives the message.</span><span class="sxs-lookup"><span data-stu-id="0bde3-145">Or, the solution back end can store the information in the device twin's tags when it receives the message.</span></span> 

<span data-ttu-id="0bde3-146">Since device-to-cloud messages enable a much higher throughput than device twin updates, it is sometimes desirable to avoid updating the device twin for every device-to-cloud message.</span><span class="sxs-lookup"><span data-stu-id="0bde3-146">Since device-to-cloud messages enable a much higher throughput than device twin updates, it is sometimes desirable to avoid updating the device twin for every device-to-cloud message.</span></span>


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
