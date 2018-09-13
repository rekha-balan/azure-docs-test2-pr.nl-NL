---
title: Developer guide for Azure IoT Hub | Microsoft Docs
description: The Azure IoT Hub developer guide includes discussions of endpoints, security, the identity registry, device management, direct methods, device twins, file uploads, jobs, the IoT Hub query language, and messaging.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/31/2017
ms.author: dobett
ms.openlocfilehash: 4f12a4b3ba9c1d0b7ed10cf5d766bcea60205d24
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540816"
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="0fdc4-103">Azure IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="0fdc4-103">Azure IoT Hub developer guide</span></span>
<span data-ttu-id="0fdc4-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="0fdc4-105">Azure IoT Hub provides you with:</span><span class="sxs-lookup"><span data-stu-id="0fdc4-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="0fdc4-106">Secure communications by using per-device security credentials and access control.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="0fdc4-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="0fdc4-108">Queryable storage of per-device state information and meta-data.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="0fdc4-109">Easy device connectivity with device libraries for the most popular languages and platforms.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-109">Easy device connectivity with device libraries for the most popular languages and platforms.</span></span>

<span data-ttu-id="0fdc4-110">This IoT Hub developer guide includes the following articles:</span><span class="sxs-lookup"><span data-stu-id="0fdc4-110">This IoT Hub developer guide includes the following articles:</span></span>

* <span data-ttu-id="0fdc4-111">[Send and receive messages with IoT Hub][devguide-messaging] describes the messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-111">[Send and receive messages with IoT Hub][devguide-messaging] describes the messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span> <span data-ttu-id="0fdc4-112">The article also includes information about topics such as message routing, message formats, and the supported communications protocols and the port numbers they use.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-112">The article also includes information about topics such as message routing, message formats, and the supported communications protocols and the port numbers they use.</span></span>
* <span data-ttu-id="0fdc4-113">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-113">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="0fdc4-114">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-114">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="0fdc4-115">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-115">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="0fdc4-116">The article also includes information about topics such as the notifications the upload process can send.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-116">The article also includes information about topics such as the notifications the upload process can send.</span></span>
* <span data-ttu-id="0fdc4-117">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-117">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="0fdc4-118">[Control access to IoT Hub][devguide-security] describes the security model used to grant access to IoT Hub functionality for both devices and cloud components.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-118">[Control access to IoT Hub][devguide-security] describes the security model used to grant access to IoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="0fdc4-119">The article includes information about using tokens and X.509 certificates, and details of the permissions you can grant.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-119">The article includes information about using tokens and X.509 certificates, and details of the permissions you can grant.</span></span>
* <span data-ttu-id="0fdc4-120">[Use device twins to synchronize state and configurations][devguide-device-twins] describes the *device twin* concept and the functionality it exposes such as synchronizing a device with its device twin.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-120">[Use device twins to synchronize state and configurations][devguide-device-twins] describes the *device twin* concept and the functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="0fdc4-121">The article includes information about the data stored in a device twin.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-121">The article includes information about the data stored in a device twin.</span></span>
* <span data-ttu-id="0fdc4-122">[Invoke a direct method on a device][devguide-directmethods] describes the lifecycle of a direct method, information about how to invoke methods on a device from your back-end app and handle the direct method on your device.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-122">[Invoke a direct method on a device][devguide-directmethods] describes the lifecycle of a direct method, information about how to invoke methods on a device from your back-end app and handle the direct method on your device.</span></span>
* <span data-ttu-id="0fdc4-123">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-123">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="0fdc4-124">The article describes how to submit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-124">The article describes how to submit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="0fdc4-125">It also describes how to query the status of a job.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-125">It also describes how to query the status of a job.</span></span>
* <span data-ttu-id="0fdc4-126">[Reference - IoT Hub endpoints][devguide-endpoints] describes the various endpoints that each IoT hub exposes for runtime and management operations.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-126">[Reference - IoT Hub endpoints][devguide-endpoints] describes the various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="0fdc4-127">The article also describes how you can create additional endpoints in your IoT hub, and how to use a field gateway to enable devices connectivity to your IoT Hub endpoints in non-standard scenarios.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-127">The article also describes how you can create additional endpoints in your IoT hub, and how to use a field gateway to enable devices connectivity to your IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="0fdc4-128">[Reference - IoT Hub query language for device twins and jobs][devguide-query] describes that IoT Hub query language that enables you to retrieve information from your hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-128">[Reference - IoT Hub query language for device twins and jobs][devguide-query] describes that IoT Hub query language that enables you to retrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="0fdc4-129">[Reference - quotas and throttling][devguide-quotas] summarizes the quotas set in the IoT Hub service and the throttling behavior you can expect to see when you exceed a quota.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-129">[Reference - quotas and throttling][devguide-quotas] summarizes the quotas set in the IoT Hub service and the throttling behavior you can expect to see when you exceed a quota.</span></span>
* <span data-ttu-id="0fdc4-130">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-130">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="0fdc4-131">[Reference - Device and service SDKs][devguide-sdks] lists the Azure IoT SDKs you can use to develop both device and service apps that interact with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-131">[Reference - Device and service SDKs][devguide-sdks] lists the Azure IoT SDKs you can use to develop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="0fdc4-132">The article includes links to online API documentation.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-132">The article includes links to online API documentation.</span></span>
* <span data-ttu-id="0fdc4-133">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-133">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports the MQTT protocol.</span></span> <span data-ttu-id="0fdc4-134">The article describes the support for the MQTT protocol built-in to the Azure IoT SDKs and provides information about using the MQTT protocol directly.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-134">The article describes the support for the MQTT protocol built-in to the Azure IoT SDKs and provides information about using the MQTT protocol directly.</span></span>
* <span data-ttu-id="0fdc4-135">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span><span class="sxs-lookup"><span data-stu-id="0fdc4-135">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

