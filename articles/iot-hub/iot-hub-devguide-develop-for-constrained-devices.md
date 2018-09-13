---
title: Azure IoT Hub Develop for Constrained Devices| Microsoft Docs
description: Developer guide - guidance on how to develop using Azure IoT SDKs for constrained devices.
services: iot-hub
documentationcenter: c
author: yzhong94
manager: timlt
editor: ''
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2018
ms.author: yizhon
ms.openlocfilehash: 15fc5794c71428b5fb1036060af3e9c4a6890f4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857772"
---
# <a name="develop-for-constrained-devices-using-azure-iot-sdks"></a><span data-ttu-id="5770a-103">Develop for constrained devices using Azure IoT SDKs</span><span class="sxs-lookup"><span data-stu-id="5770a-103">Develop for constrained devices using Azure IoT SDKs</span></span>

## <a name="develop-using-azure-iot-hub-c-sdk"></a><span data-ttu-id="5770a-104">Develop using Azure IoT Hub C SDK</span><span class="sxs-lookup"><span data-stu-id="5770a-104">Develop using Azure IoT Hub C SDK</span></span>
<span data-ttu-id="5770a-105">Azure IoT Hub C SDK is written in ANSI C (C99), which makes it well-suited to operate a variety of platforms with small disk and memory footprint.</span><span class="sxs-lookup"><span data-stu-id="5770a-105">Azure IoT Hub C SDK is written in ANSI C (C99), which makes it well-suited to operate a variety of platforms with small disk and memory footprint.</span></span>  <span data-ttu-id="5770a-106">The recommended RAM is at least 64 KB, but the exact memory footprint depends on the protocol used, the number of connections opened, as well as the platform targeted.</span><span class="sxs-lookup"><span data-stu-id="5770a-106">The recommended RAM is at least 64 KB, but the exact memory footprint depends on the protocol used, the number of connections opened, as well as the platform targeted.</span></span>

<span data-ttu-id="5770a-107">C SDK is available in package form from apt-get, NuGet, and MBED.</span><span class="sxs-lookup"><span data-stu-id="5770a-107">C SDK is available in package form from apt-get, NuGet, and MBED.</span></span>  <span data-ttu-id="5770a-108">To target constrained devices, you may want to build the SDK locally for your target platform.</span><span class="sxs-lookup"><span data-stu-id="5770a-108">To target constrained devices, you may want to build the SDK locally for your target platform.</span></span> <span data-ttu-id="5770a-109">This documentation demonstrates how to remove certain features to shrink the footprint of the C SDK using [cmake][lnk-cmake].</span><span class="sxs-lookup"><span data-stu-id="5770a-109">This documentation demonstrates how to remove certain features to shrink the footprint of the C SDK using [cmake][lnk-cmake].</span></span>  <span data-ttu-id="5770a-110">In addition, this documentation discusses the best practice programming models for working with constrained devices.</span><span class="sxs-lookup"><span data-stu-id="5770a-110">In addition, this documentation discusses the best practice programming models for working with constrained devices.</span></span>

### <a name="building-the-c-sdk-for-constrained-devices"></a><span data-ttu-id="5770a-111">Building the C SDK for constrained devices</span><span class="sxs-lookup"><span data-stu-id="5770a-111">Building the C SDK for constrained devices</span></span>
#### <a name="prerequisites"></a><span data-ttu-id="5770a-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5770a-112">Prerequisites</span></span>
<span data-ttu-id="5770a-113">Follow this [setup guide][lnk-devbox-setup] to prepare your development environment for building the C SDK.</span><span class="sxs-lookup"><span data-stu-id="5770a-113">Follow this [setup guide][lnk-devbox-setup] to prepare your development environment for building the C SDK.</span></span>  <span data-ttu-id="5770a-114">Before you get to the step for building with cmake, you can invoke cmake flags to remove unused features.</span><span class="sxs-lookup"><span data-stu-id="5770a-114">Before you get to the step for building with cmake, you can invoke cmake flags to remove unused features.</span></span>

#### <a name="remove-additional-protocol-libraries"></a><span data-ttu-id="5770a-115">Remove additional protocol libraries</span><span class="sxs-lookup"><span data-stu-id="5770a-115">Remove additional protocol libraries</span></span>
<span data-ttu-id="5770a-116">C SDK supports five protocols today: MQTT, MQTT over WebSocket, AMQPs, AMQP over WebSocket, and HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5770a-116">C SDK supports five protocols today: MQTT, MQTT over WebSocket, AMQPs, AMQP over WebSocket, and HTTPS.</span></span>    <span data-ttu-id="5770a-117">Most scenarios require one to two protocols running on a client, hence you can remove the protocol library you are not using from the SDK.</span><span class="sxs-lookup"><span data-stu-id="5770a-117">Most scenarios require one to two protocols running on a client, hence you can remove the protocol library you are not using from the SDK.</span></span>  <span data-ttu-id="5770a-118">Additional information about choosing the appropriate communication protocol for your scenario can be found in this [document][lnk-choosing-protocol].</span><span class="sxs-lookup"><span data-stu-id="5770a-118">Additional information about choosing the appropriate communication protocol for your scenario can be found in this [document][lnk-choosing-protocol].</span></span>  <span data-ttu-id="5770a-119">For example, MQTT is a lightweight protocol that is often better suited for constrained devices.</span><span class="sxs-lookup"><span data-stu-id="5770a-119">For example, MQTT is a lightweight protocol that is often better suited for constrained devices.</span></span>

<span data-ttu-id="5770a-120">You can remove AMQP and HTTP libraries using the following cmake command:</span><span class="sxs-lookup"><span data-stu-id="5770a-120">You can remove AMQP and HTTP libraries using the following cmake command:</span></span>
```
cmake -Duse_amqp=OFF -Duse_http=OFF <Path_to_cmake>
```

#### <a name="remove-sdk-logging-capability"></a><span data-ttu-id="5770a-121">Remove SDK logging capability</span><span class="sxs-lookup"><span data-stu-id="5770a-121">Remove SDK logging capability</span></span>
<span data-ttu-id="5770a-122">The C SDK provides extensive logging throughout to help with debugging.</span><span class="sxs-lookup"><span data-stu-id="5770a-122">The C SDK provides extensive logging throughout to help with debugging.</span></span> <span data-ttu-id="5770a-123">You can remove the logging capability for production devices using the following cmake command:</span><span class="sxs-lookup"><span data-stu-id="5770a-123">You can remove the logging capability for production devices using the following cmake command:</span></span>
```
cmake -Dno_logging=OFF <Path_to_cmake>
```

#### <a name="remove-upload-to-blob-capability"></a><span data-ttu-id="5770a-124">Remove upload to blob capability</span><span class="sxs-lookup"><span data-stu-id="5770a-124">Remove upload to blob capability</span></span>
<span data-ttu-id="5770a-125">You can upload large files to Azure Storage using the built-in capability in the SDK.</span><span class="sxs-lookup"><span data-stu-id="5770a-125">You can upload large files to Azure Storage using the built-in capability in the SDK.</span></span>  <span data-ttu-id="5770a-126">Azure IoT Hub acts as a dispatcher to an associated Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="5770a-126">Azure IoT Hub acts as a dispatcher to an associated Azure Storage account.</span></span>  <span data-ttu-id="5770a-127">You can use this feature to send media files, large telemetry batches, and logs.</span><span class="sxs-lookup"><span data-stu-id="5770a-127">You can use this feature to send media files, large telemetry batches, and logs.</span></span>  <span data-ttu-id="5770a-128">Learn more about upload files with IoT Hub in this [document][lnk-hub-file-upload].</span><span class="sxs-lookup"><span data-stu-id="5770a-128">Learn more about upload files with IoT Hub in this [document][lnk-hub-file-upload].</span></span>  <span data-ttu-id="5770a-129">If your application does not require this functionality, you can remove this feature using the following cmake command:</span><span class="sxs-lookup"><span data-stu-id="5770a-129">If your application does not require this functionality, you can remove this feature using the following cmake command:</span></span>
```
cmake -Ddont_use_uploadtoblob=ON <Path_to_cmake>
```
#### <a name="running-strip-on-linux-environment"></a><span data-ttu-id="5770a-130">Running strip on Linux environment</span><span class="sxs-lookup"><span data-stu-id="5770a-130">Running strip on Linux environment</span></span>
<span data-ttu-id="5770a-131">If your binaries run on Linux system, you can leverage the [strip command][lnk-strip] to reduce the size of the final application after compiling.</span><span class="sxs-lookup"><span data-stu-id="5770a-131">If your binaries run on Linux system, you can leverage the [strip command][lnk-strip] to reduce the size of the final application after compiling.</span></span>
```
strip -s <Path_to_executable>
```

### <a name="programming-models-for-constrained-devices"></a><span data-ttu-id="5770a-132">Programming models for constrained devices</span><span class="sxs-lookup"><span data-stu-id="5770a-132">Programming models for constrained devices</span></span>
#### <a name="avoid-using-the-serializer"></a><span data-ttu-id="5770a-133">Avoid using the Serializer</span><span class="sxs-lookup"><span data-stu-id="5770a-133">Avoid using the Serializer</span></span>
<span data-ttu-id="5770a-134">The C SDK has an optional [serializer][lnk-serializer], which allows you to use declarative mapping tables to define methods and device twin properties.</span><span class="sxs-lookup"><span data-stu-id="5770a-134">The C SDK has an optional [serializer][lnk-serializer], which allows you to use declarative mapping tables to define methods and device twin properties.</span></span>  <span data-ttu-id="5770a-135">The serializer is designed to simplify development, but it adds overhead, which is not optimal for constrained devices.</span><span class="sxs-lookup"><span data-stu-id="5770a-135">The serializer is designed to simplify development, but it adds overhead, which is not optimal for constrained devices.</span></span>  <span data-ttu-id="5770a-136">In this case, consider using primitive client APIs and parse json by using a lightweight parser such as [parson][lnk-parson].</span><span class="sxs-lookup"><span data-stu-id="5770a-136">In this case, consider using primitive client APIs and parse json by using a lightweight parser such as [parson][lnk-parson].</span></span>

#### <a name="use-the-lower-layer-ll"></a><span data-ttu-id="5770a-137">Use the lower layer (_LL_)</span><span class="sxs-lookup"><span data-stu-id="5770a-137">Use the lower layer (_LL_)</span></span>
<span data-ttu-id="5770a-138">The C SDK supports two programming models.</span><span class="sxs-lookup"><span data-stu-id="5770a-138">The C SDK supports two programming models.</span></span>  <span data-ttu-id="5770a-139">One set has APIs with an _LL_ infix, which stands for lower layer.</span><span class="sxs-lookup"><span data-stu-id="5770a-139">One set has APIs with an _LL_ infix, which stands for lower layer.</span></span>  <span data-ttu-id="5770a-140">This set of APIs are lighter weight and do not spin up worker threads, which means the user must manually control scheduling.</span><span class="sxs-lookup"><span data-stu-id="5770a-140">This set of APIs are lighter weight and do not spin up worker threads, which means the user must manually control scheduling.</span></span>  <span data-ttu-id="5770a-141">For example, for the device client, the _LL_ APIs can be found in this [header file](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/inc/iothub_device_client_ll.h).</span><span class="sxs-lookup"><span data-stu-id="5770a-141">For example, for the device client, the _LL_ APIs can be found in this [header file](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/inc/iothub_device_client_ll.h).</span></span>  <span data-ttu-id="5770a-142">Another set of APIs without the _LL_ index is called the convenience layer, where a worker thread is spun automatically.</span><span class="sxs-lookup"><span data-stu-id="5770a-142">Another set of APIs without the _LL_ index is called the convenience layer, where a worker thread is spun automatically.</span></span>  <span data-ttu-id="5770a-143">For example, the convenience layer APIs for the device client can be found in this [header file](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/inc/iothub_device_client.h).</span><span class="sxs-lookup"><span data-stu-id="5770a-143">For example, the convenience layer APIs for the device client can be found in this [header file](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/inc/iothub_device_client.h).</span></span>  <span data-ttu-id="5770a-144">For constrained devices where each extra thread can take a substantial percentage of system resources, consider using _LL_ APIs.</span><span class="sxs-lookup"><span data-stu-id="5770a-144">For constrained devices where each extra thread can take a substantial percentage of system resources, consider using _LL_ APIs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5770a-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="5770a-145">Next steps</span></span>
<span data-ttu-id="5770a-146">To learn more about Azure IoT C SDK architecture:</span><span class="sxs-lookup"><span data-stu-id="5770a-146">To learn more about Azure IoT C SDK architecture:</span></span>
-   [<span data-ttu-id="5770a-147">Azure IoT C SDK source code</span><span class="sxs-lookup"><span data-stu-id="5770a-147">Azure IoT C SDK source code</span></span>](https://github.com/Azure/azure-iot-sdk-c/)
-   [<span data-ttu-id="5770a-148">Azure IoT device SDK for C introduction</span><span class="sxs-lookup"><span data-stu-id="5770a-148">Azure IoT device SDK for C introduction</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-sdk-c-intro)

------
[lnk-cmake]: https://cmake.org/
[lnk-devbox-setup]:  https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-choosing-protocol]: https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-protocols
[lnk-hub-file-upload]: https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-file-upload
[lnk-strip]: https://en.wikipedia.org/wiki/Strip_(Unix)
[lnk-serializer]: https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer
[lnk-parson]: https://github.com/kgabis/parson