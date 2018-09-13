---
title: Develop modules for Azure IoT Edge | Microsoft Docs
description: Learn how to create custom modules for Azure IoT Edge
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 10/05/2017
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: dbbd07e93602855afb0c9755e8872e0b46557611
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865652"
---
# <a name="understand-the-requirements-and-tools-for-developing-iot-edge-modules"></a><span data-ttu-id="91729-103">Understand the requirements and tools for developing IoT Edge modules</span><span class="sxs-lookup"><span data-stu-id="91729-103">Understand the requirements and tools for developing IoT Edge modules</span></span>

<span data-ttu-id="91729-104">This article explains what functionalities are available when writing applications that run as IoT Edge module, and how to take advantage of them.</span><span class="sxs-lookup"><span data-stu-id="91729-104">This article explains what functionalities are available when writing applications that run as IoT Edge module, and how to take advantage of them.</span></span>

## <a name="iot-edge-runtime-environment"></a><span data-ttu-id="91729-105">IoT Edge runtime environment</span><span class="sxs-lookup"><span data-stu-id="91729-105">IoT Edge runtime environment</span></span>
<span data-ttu-id="91729-106">The IoT Edge runtime provides the infrastructure to integrate the functionality of multiple IoT Edge modules and to deploy them onto IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="91729-106">The IoT Edge runtime provides the infrastructure to integrate the functionality of multiple IoT Edge modules and to deploy them onto IoT Edge devices.</span></span> <span data-ttu-id="91729-107">At a high level, any program can be packaged as an IoT Edge module.</span><span class="sxs-lookup"><span data-stu-id="91729-107">At a high level, any program can be packaged as an IoT Edge module.</span></span> <span data-ttu-id="91729-108">However, to take full advantage of IoT Edge communication and management functionalities, a program running in a module can connect to the local IoT Edge hub, integrated in the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="91729-108">However, to take full advantage of IoT Edge communication and management functionalities, a program running in a module can connect to the local IoT Edge hub, integrated in the IoT Edge runtime.</span></span>

## <a name="using-the-iot-edge-hub"></a><span data-ttu-id="91729-109">Using the IoT Edge hub</span><span class="sxs-lookup"><span data-stu-id="91729-109">Using the IoT Edge hub</span></span>
<span data-ttu-id="91729-110">The IoT Edge hub provides two main functionalities: proxy to IoT Hub, and local communications.</span><span class="sxs-lookup"><span data-stu-id="91729-110">The IoT Edge hub provides two main functionalities: proxy to IoT Hub, and local communications.</span></span>

### <a name="iot-hub-primitives"></a><span data-ttu-id="91729-111">IoT Hub primitives</span><span class="sxs-lookup"><span data-stu-id="91729-111">IoT Hub primitives</span></span>
<span data-ttu-id="91729-112">IoT Hub sees a module instance analogously to a device, in the sense that it:</span><span class="sxs-lookup"><span data-stu-id="91729-112">IoT Hub sees a module instance analogously to a device, in the sense that it:</span></span>

* <span data-ttu-id="91729-113">it has a module twin, that is distinct and isolated from the [device twin][lnk-devicetwin] and the other module twins of that device;</span><span class="sxs-lookup"><span data-stu-id="91729-113">it has a module twin, that is distinct and isolated from the [device twin][lnk-devicetwin] and the other module twins of that device;</span></span>
* <span data-ttu-id="91729-114">it can send [device-to-cloud messages][lnk-iothub-messaging];</span><span class="sxs-lookup"><span data-stu-id="91729-114">it can send [device-to-cloud messages][lnk-iothub-messaging];</span></span>
* <span data-ttu-id="91729-115">it can receive [direct methods][lnk-methods] targeted specifically at its identity.</span><span class="sxs-lookup"><span data-stu-id="91729-115">it can receive [direct methods][lnk-methods] targeted specifically at its identity.</span></span>

<span data-ttu-id="91729-116">Currently, a module cannot receive cloud-to-device messages nor use the file upload feature.</span><span class="sxs-lookup"><span data-stu-id="91729-116">Currently, a module cannot receive cloud-to-device messages nor use the file upload feature.</span></span>

<span data-ttu-id="91729-117">When writing a module, you can simply use the [Azure IoT Device SDK][lnk-devicesdk] to connect to the IoT Edge hub and use the above functionality as you would when using IoT Hub with a device application, the only difference being that, from your application back-end, you have to refer to the module identity instead of the device identity.</span><span class="sxs-lookup"><span data-stu-id="91729-117">When writing a module, you can simply use the [Azure IoT Device SDK][lnk-devicesdk] to connect to the IoT Edge hub and use the above functionality as you would when using IoT Hub with a device application, the only difference being that, from your application back-end, you have to refer to the module identity instead of the device identity.</span></span>

<span data-ttu-id="91729-118">See [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2] for an example of a module application that sends device-to-cloud messages, and uses the module twin.</span><span class="sxs-lookup"><span data-stu-id="91729-118">See [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2] for an example of a module application that sends device-to-cloud messages, and uses the module twin.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="91729-119">Device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="91729-119">Device-to-cloud messages</span></span>
<span data-ttu-id="91729-120">In order to enable complex processing of device-to-cloud messages, IoT Edge hub provides declarative routing of messages between modules, and between modules and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="91729-120">In order to enable complex processing of device-to-cloud messages, IoT Edge hub provides declarative routing of messages between modules, and between modules and IoT Hub.</span></span>
<span data-ttu-id="91729-121">This allows modules to intercept and process messages sent by other modules and propagate them into complex pipelines.</span><span class="sxs-lookup"><span data-stu-id="91729-121">This allows modules to intercept and process messages sent by other modules and propagate them into complex pipelines.</span></span>
<span data-ttu-id="91729-122">The article [Module composition][lnk-module-comp] explains how to compose modules into complex pipelines using routes.</span><span class="sxs-lookup"><span data-stu-id="91729-122">The article [Module composition][lnk-module-comp] explains how to compose modules into complex pipelines using routes.</span></span>

<span data-ttu-id="91729-123">An IoT Edge module, differently than a normal IoT Hub device application, can receive device-to-cloud messages that are being proxied by its local IoT Edge hub, in order to process them.</span><span class="sxs-lookup"><span data-stu-id="91729-123">An IoT Edge module, differently than a normal IoT Hub device application, can receive device-to-cloud messages that are being proxied by its local IoT Edge hub, in order to process them.</span></span>

<span data-ttu-id="91729-124">IoT Edge hub propagates the messages to your module based on declarative routes described in the [Module composition][lnk-module-comp] article.</span><span class="sxs-lookup"><span data-stu-id="91729-124">IoT Edge hub propagates the messages to your module based on declarative routes described in the [Module composition][lnk-module-comp] article.</span></span> <span data-ttu-id="91729-125">When developing an IoT Edge module, you can receive these messages by setting message handlers, as shown in the tutorial [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2].</span><span class="sxs-lookup"><span data-stu-id="91729-125">When developing an IoT Edge module, you can receive these messages by setting message handlers, as shown in the tutorial [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2].</span></span>

<span data-ttu-id="91729-126">In order to simplify the creation of routes, IoT Edge adds the concept of module *input* and *output* endpoints.</span><span class="sxs-lookup"><span data-stu-id="91729-126">In order to simplify the creation of routes, IoT Edge adds the concept of module *input* and *output* endpoints.</span></span> <span data-ttu-id="91729-127">A module can receive all device-to-cloud messages routed to it without specifying any input, and can send device-to-cloud messages without specifying any output.</span><span class="sxs-lookup"><span data-stu-id="91729-127">A module can receive all device-to-cloud messages routed to it without specifying any input, and can send device-to-cloud messages without specifying any output.</span></span>
<span data-ttu-id="91729-128">Using explicit inputs and outputs, though, makes routing rules simpler to understand.</span><span class="sxs-lookup"><span data-stu-id="91729-128">Using explicit inputs and outputs, though, makes routing rules simpler to understand.</span></span> <span data-ttu-id="91729-129">See [Module composition][lnk-module-comp] for more information on routing rules and input and output endpoints for modules.</span><span class="sxs-lookup"><span data-stu-id="91729-129">See [Module composition][lnk-module-comp] for more information on routing rules and input and output endpoints for modules.</span></span>

<span data-ttu-id="91729-130">Finally, device-to-cloud messages handled by the Edge hub are stamped with the following system properties:</span><span class="sxs-lookup"><span data-stu-id="91729-130">Finally, device-to-cloud messages handled by the Edge hub are stamped with the following system properties:</span></span>

| <span data-ttu-id="91729-131">Property</span><span class="sxs-lookup"><span data-stu-id="91729-131">Property</span></span> | <span data-ttu-id="91729-132">Description</span><span class="sxs-lookup"><span data-stu-id="91729-132">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="91729-133">$connectionDeviceId</span><span class="sxs-lookup"><span data-stu-id="91729-133">$connectionDeviceId</span></span> | <span data-ttu-id="91729-134">The device ID of the client that sent the message</span><span class="sxs-lookup"><span data-stu-id="91729-134">The device ID of the client that sent the message</span></span> |
| <span data-ttu-id="91729-135">$connectionModuleId</span><span class="sxs-lookup"><span data-stu-id="91729-135">$connectionModuleId</span></span> | <span data-ttu-id="91729-136">The module ID of the module that sent the message</span><span class="sxs-lookup"><span data-stu-id="91729-136">The module ID of the module that sent the message</span></span> |
| <span data-ttu-id="91729-137">$inputName</span><span class="sxs-lookup"><span data-stu-id="91729-137">$inputName</span></span> | <span data-ttu-id="91729-138">The input that received this message.</span><span class="sxs-lookup"><span data-stu-id="91729-138">The input that received this message.</span></span> <span data-ttu-id="91729-139">Can be empty.</span><span class="sxs-lookup"><span data-stu-id="91729-139">Can be empty.</span></span> |
| <span data-ttu-id="91729-140">$outputName</span><span class="sxs-lookup"><span data-stu-id="91729-140">$outputName</span></span> | <span data-ttu-id="91729-141">The output used to send the message.</span><span class="sxs-lookup"><span data-stu-id="91729-141">The output used to send the message.</span></span> <span data-ttu-id="91729-142">Can be empty.</span><span class="sxs-lookup"><span data-stu-id="91729-142">Can be empty.</span></span> |

### <a name="connecting-to-iot-edge-hub-from-a-module"></a><span data-ttu-id="91729-143">Connecting to IoT Edge hub from a module</span><span class="sxs-lookup"><span data-stu-id="91729-143">Connecting to IoT Edge hub from a module</span></span>
<span data-ttu-id="91729-144">Connecting to the local IoT Edge hub from a module involves two steps: use the connection string provided by the IoT Edge runtime when your module starts, and make sure your application accepts the certificate presented by the IoT Edge hub on that device.</span><span class="sxs-lookup"><span data-stu-id="91729-144">Connecting to the local IoT Edge hub from a module involves two steps: use the connection string provided by the IoT Edge runtime when your module starts, and make sure your application accepts the certificate presented by the IoT Edge hub on that device.</span></span>

<span data-ttu-id="91729-145">The connecting string to use is injected by the IoT Edge runtime in the environment variable `EdgeHubConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="91729-145">The connecting string to use is injected by the IoT Edge runtime in the environment variable `EdgeHubConnectionString`.</span></span> <span data-ttu-id="91729-146">This makes it available to any program that wants to use it.</span><span class="sxs-lookup"><span data-stu-id="91729-146">This makes it available to any program that wants to use it.</span></span>

<span data-ttu-id="91729-147">Analogously, the certificate to use to validate the IoT Edge hub connection is injected by the IoT Edge runtime in a file whose path is available in the environment variable `EdgeModuleCACertificateFile`.</span><span class="sxs-lookup"><span data-stu-id="91729-147">Analogously, the certificate to use to validate the IoT Edge hub connection is injected by the IoT Edge runtime in a file whose path is available in the environment variable `EdgeModuleCACertificateFile`.</span></span>

<span data-ttu-id="91729-148">The tutorial [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2] shows how to make sure that the certificate is in the machine store in your module application.</span><span class="sxs-lookup"><span data-stu-id="91729-148">The tutorial [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2] shows how to make sure that the certificate is in the machine store in your module application.</span></span> <span data-ttu-id="91729-149">Clearly, any other method to trust connections using that certificate work.</span><span class="sxs-lookup"><span data-stu-id="91729-149">Clearly, any other method to trust connections using that certificate work.</span></span>

## <a name="packaging-as-an-image"></a><span data-ttu-id="91729-150">Packaging as an image</span><span class="sxs-lookup"><span data-stu-id="91729-150">Packaging as an image</span></span>
<span data-ttu-id="91729-151">IoT Edge modules are packaged as Docker images.</span><span class="sxs-lookup"><span data-stu-id="91729-151">IoT Edge modules are packaged as Docker images.</span></span>
<span data-ttu-id="91729-152">You can use Docker toolchain directly, or Visual Studio Code as shown in the tutorial [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2].</span><span class="sxs-lookup"><span data-stu-id="91729-152">You can use Docker toolchain directly, or Visual Studio Code as shown in the tutorial [Develop and deploy an IoT Edge module to a simulated device][lnk-tutorial2].</span></span>

## <a name="next-steps"></a><span data-ttu-id="91729-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="91729-153">Next steps</span></span>

<span data-ttu-id="91729-154">After you develop a module, learn how to [Deploy and monitor IoT Edge modules at scale][lnk-howto-deploy].</span><span class="sxs-lookup"><span data-stu-id="91729-154">After you develop a module, learn how to [Deploy and monitor IoT Edge modules at scale][lnk-howto-deploy].</span></span>

[lnk-devicesdk]: ../iot-hub/iot-hub-devguide-sdks.md
[lnk-devicetwin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-iothub-messaging]: ../iot-hub/iot-hub-devguide-messaging.md
[lnk-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-tutorial2]: tutorial-csharp-module.md
[lnk-module-comp]: module-composition.md
[lnk-howto-deploy]: how-to-deploy-monitor.md
