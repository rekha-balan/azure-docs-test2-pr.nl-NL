---
title: Understand the Azure IoT SDKs | Microsoft Docs
description: Developer guide - information about and links to the various Azure IoT device and service SDKs that you can use to build device apps and back-end apps.
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bf9d7d42b89e33c59f3fdef649abcb0fbb4dfaa5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564131"
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="72972-103">Understand and use Azure IoT SDKs</span><span class="sxs-lookup"><span data-stu-id="72972-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="72972-104">There are three categories of SDK for working with IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="72972-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="72972-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="72972-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="72972-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="72972-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="72972-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="72972-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="72972-108">**Gateway SDKs** enable you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span><span class="sxs-lookup"><span data-stu-id="72972-108">**Gateway SDKs** enable you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="72972-109">SDKs are provided to support multiple programming languages.</span><span class="sxs-lookup"><span data-stu-id="72972-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="72972-110">Azure IoT device SDKs</span><span class="sxs-lookup"><span data-stu-id="72972-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="72972-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span><span class="sxs-lookup"><span data-stu-id="72972-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="72972-112">The following Azure IoT device SDKs are available to download from GitHub:</span><span class="sxs-lookup"><span data-stu-id="72972-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="72972-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span><span class="sxs-lookup"><span data-stu-id="72972-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span>
* <span data-ttu-id="72972-114">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-114">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="72972-115">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-115">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="72972-116">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-116">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="72972-117">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-117">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="72972-118">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span><span class="sxs-lookup"><span data-stu-id="72972-118">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="72972-119">OS platform and hardware compatibility</span><span class="sxs-lookup"><span data-stu-id="72972-119">OS platform and hardware compatibility</span></span>

<span data-ttu-id="72972-120">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="72972-120">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="72972-121">Azure IoT service SDKs</span><span class="sxs-lookup"><span data-stu-id="72972-121">Azure IoT service SDKs</span></span>

<span data-ttu-id="72972-122">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span><span class="sxs-lookup"><span data-stu-id="72972-122">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="72972-123">The following Azure IoT service SDKs are available to download from GitHub:</span><span class="sxs-lookup"><span data-stu-id="72972-123">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="72972-124">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-124">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="72972-125">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-125">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="72972-126">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-126">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="72972-127">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="72972-127">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>


> [!NOTE]
> <span data-ttu-id="72972-128">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span><span class="sxs-lookup"><span data-stu-id="72972-128">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-gateway-sdks"></a><span data-ttu-id="72972-129">Azure IoT Gateway SDKs</span><span class="sxs-lookup"><span data-stu-id="72972-129">Azure IoT Gateway SDKs</span></span>

<span data-ttu-id="72972-130">This Azure IoT Gateway SDK contains the infrastructure and modules to create IoT gateway solutions.</span><span class="sxs-lookup"><span data-stu-id="72972-130">This Azure IoT Gateway SDK contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="72972-131">You can extend the SDK to create gateways tailored to any end-to-end scenario.</span><span class="sxs-lookup"><span data-stu-id="72972-131">You can extend the SDK to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="72972-132">You can download the [Azure IoT Gateway SDK][lnk-gateway-sdk] from GitHub.</span><span class="sxs-lookup"><span data-stu-id="72972-132">You can download the [Azure IoT Gateway SDK][lnk-gateway-sdk] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="72972-133">Online API reference documentation</span><span class="sxs-lookup"><span data-stu-id="72972-133">Online API reference documentation</span></span>

<span data-ttu-id="72972-134">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span><span class="sxs-lookup"><span data-stu-id="72972-134">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="72972-135">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-135">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="72972-136">[IoT Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-136">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="72972-137">[Azure IoT device SDK for C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-137">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="72972-138">[Azure IoT device SDK for Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-138">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="72972-139">[Azure IoT service SDK for Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-139">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="72972-140">[Azure IoT device SDK for Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-140">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="72972-141">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-141">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="72972-142">[Azure IoT gateway SDK][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="72972-142">[Azure IoT gateway SDK][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="72972-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="72972-143">Next steps</span></span>

<span data-ttu-id="72972-144">Other reference topics in this IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="72972-144">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="72972-145">[IoT Hub endpoints][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="72972-145">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="72972-146">[IoT Hub query language for device twins and jobs][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="72972-146">[IoT Hub query language for device twins and jobs][lnk-devguide-query]</span></span>
* <span data-ttu-id="72972-147">[Quotas and throttling][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="72972-147">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="72972-148">[IoT Hub MQTT support][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="72972-148">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/azure-iot-device/1.1.9/index.html
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/azure-iothub/1.1.9/index.html
[lnk-gateway-ref]: http://azure.github.io/azure-iot-gateway-sdk/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
