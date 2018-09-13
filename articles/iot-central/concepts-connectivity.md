---
title: Device connectivity in Azure IoT Central | Microsoft Docs
description: This article introduces key concepts relating to device connectivity in Azure IoT Central
author: dominicbetts
ms.author: dobett
ms.date: 11/30/2017
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: timlt
ms.openlocfilehash: dc9fe144c2258f33ce59c61ce63c15835cc3fa53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865220"
---
# <a name="device-connectivity-in-azure-iot-central"></a><span data-ttu-id="9ee71-103">Device connectivity in Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="9ee71-103">Device connectivity in Azure IoT Central</span></span>

<span data-ttu-id="9ee71-104">This article introduces key concepts relating to device connectivity in Microsoft Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="9ee71-104">This article introduces key concepts relating to device connectivity in Microsoft Azure IoT Central.</span></span>

<span data-ttu-id="9ee71-105">Every device that connects to your Azure IoT Central application, connects to the [endpoints](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-endpoints) that are exposed by the IoT hub Azure IoT Central uses.</span><span class="sxs-lookup"><span data-stu-id="9ee71-105">Every device that connects to your Azure IoT Central application, connects to the [endpoints](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-endpoints) that are exposed by the IoT hub Azure IoT Central uses.</span></span> <span data-ttu-id="9ee71-106">IoT Hub enables scalable, secure, and reliable connections from your connected devices.</span><span class="sxs-lookup"><span data-stu-id="9ee71-106">IoT Hub enables scalable, secure, and reliable connections from your connected devices.</span></span>

## <a name="sdk-support"></a><span data-ttu-id="9ee71-107">SDK support</span><span class="sxs-lookup"><span data-stu-id="9ee71-107">SDK support</span></span>

<span data-ttu-id="9ee71-108">The Azure Device SDKs offer the easiest way for you implement the code on your devices that connects to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="9ee71-108">The Azure Device SDKs offer the easiest way for you implement the code on your devices that connects to your Azure IoT Central application.</span></span> <span data-ttu-id="9ee71-109">The following device SDKs are available:</span><span class="sxs-lookup"><span data-stu-id="9ee71-109">The following device SDKs are available:</span></span>

- [<span data-ttu-id="9ee71-110">Azure IoT SDK for C</span><span class="sxs-lookup"><span data-stu-id="9ee71-110">Azure IoT SDK for C</span></span>](https://github.com/azure/azure-iot-sdk-c)
- [<span data-ttu-id="9ee71-111">Azure IoT SDK for Python</span><span class="sxs-lookup"><span data-stu-id="9ee71-111">Azure IoT SDK for Python</span></span>](https://github.com/azure/azure-iot-sdk-python)
- [<span data-ttu-id="9ee71-112">Azure IoT SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="9ee71-112">Azure IoT SDK for Node.js</span></span>](https://github.com/azure/azure-iot-sdk-node)
- [<span data-ttu-id="9ee71-113">Azure IoT SDK for Java</span><span class="sxs-lookup"><span data-stu-id="9ee71-113">Azure IoT SDK for Java</span></span>](https://github.com/azure/azure-iot-sdk-java)
- [<span data-ttu-id="9ee71-114">Azure IoT SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="9ee71-114">Azure IoT SDK for .NET</span></span>](https://github.com/azure/azure-iot-sdk-csharp)

<span data-ttu-id="9ee71-115">Each device connects using a unique connection string that identifies the device.</span><span class="sxs-lookup"><span data-stu-id="9ee71-115">Each device connects using a unique connection string that identifies the device.</span></span> <span data-ttu-id="9ee71-116">A device can only connect to the IoT hub where it is registered.</span><span class="sxs-lookup"><span data-stu-id="9ee71-116">A device can only connect to the IoT hub where it is registered.</span></span> <span data-ttu-id="9ee71-117">When you create a real device in your Azure IoT Central application, the application generates a connection string for you to use.</span><span class="sxs-lookup"><span data-stu-id="9ee71-117">When you create a real device in your Azure IoT Central application, the application generates a connection string for you to use.</span></span>

## <a name="sdk-features-and-iot-hub-connectivity"></a><span data-ttu-id="9ee71-118">SDK features and IoT Hub connectivity</span><span class="sxs-lookup"><span data-stu-id="9ee71-118">SDK features and IoT Hub connectivity</span></span>

<span data-ttu-id="9ee71-119">All device communication with IoT Hub uses the following IoT Hub connectivity options:</span><span class="sxs-lookup"><span data-stu-id="9ee71-119">All device communication with IoT Hub uses the following IoT Hub connectivity options:</span></span>

- [<span data-ttu-id="9ee71-120">Device-to-cloud messaging</span><span class="sxs-lookup"><span data-stu-id="9ee71-120">Device-to-cloud messaging</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-messages-d2c)
- [<span data-ttu-id="9ee71-121">Device twins</span><span class="sxs-lookup"><span data-stu-id="9ee71-121">Device twins</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-device-twins)

<span data-ttu-id="9ee71-122">The following table summarizes how Azure IoT Central device features map on to IoT Hub features:</span><span class="sxs-lookup"><span data-stu-id="9ee71-122">The following table summarizes how Azure IoT Central device features map on to IoT Hub features:</span></span>

| <span data-ttu-id="9ee71-123">Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="9ee71-123">Azure IoT Central</span></span> | <span data-ttu-id="9ee71-124">Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9ee71-124">Azure IoT Hub</span></span> |
| ----------- | ------- |
| <span data-ttu-id="9ee71-125">Measurement: Telemetry</span><span class="sxs-lookup"><span data-stu-id="9ee71-125">Measurement: Telemetry</span></span> | <span data-ttu-id="9ee71-126">Device-to-cloud messaging</span><span class="sxs-lookup"><span data-stu-id="9ee71-126">Device-to-cloud messaging</span></span> |
| <span data-ttu-id="9ee71-127">Device properties</span><span class="sxs-lookup"><span data-stu-id="9ee71-127">Device properties</span></span> | <span data-ttu-id="9ee71-128">Device twin reported properties</span><span class="sxs-lookup"><span data-stu-id="9ee71-128">Device twin reported properties</span></span> |
| <span data-ttu-id="9ee71-129">Settings</span><span class="sxs-lookup"><span data-stu-id="9ee71-129">Settings</span></span> | <span data-ttu-id="9ee71-130">Device twin desired and reported properties</span><span class="sxs-lookup"><span data-stu-id="9ee71-130">Device twin desired and reported properties</span></span> |

<span data-ttu-id="9ee71-131">To learn more about using the Device SDKs, see one of the following articles for example code:</span><span class="sxs-lookup"><span data-stu-id="9ee71-131">To learn more about using the Device SDKs, see one of the following articles for example code:</span></span>

- [<span data-ttu-id="9ee71-132">Connect a generic Node.js client to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="9ee71-132">Connect a generic Node.js client to your Azure IoT Central application</span></span>](howto-connect-nodejs.md)
- [<span data-ttu-id="9ee71-133">Connect a Raspberry Pi device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="9ee71-133">Connect a Raspberry Pi device to your Azure IoT Central application</span></span>](howto-connect-raspberry-pi-python.md)
- <span data-ttu-id="9ee71-134">[Connect a DevDiv kit device to your Azure IoT Central application](howto-connect-devkit.md).</span><span class="sxs-lookup"><span data-stu-id="9ee71-134">[Connect a DevDiv kit device to your Azure IoT Central application](howto-connect-devkit.md).</span></span>

<span data-ttu-id="9ee71-135">The following video presents an overview of how to connect a real device to Azure IoT Central:</span><span class="sxs-lookup"><span data-stu-id="9ee71-135">The following video presents an overview of how to connect a real device to Azure IoT Central:</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Internet-of-Things-Show/Connect-real-devices-to-Microsoft-IoT-Central/Player]

## <a name="protocols"></a><span data-ttu-id="9ee71-136">Protocols</span><span class="sxs-lookup"><span data-stu-id="9ee71-136">Protocols</span></span>

<span data-ttu-id="9ee71-137">The Device SDKs support the following network protocols for connecting to an IoT hub:</span><span class="sxs-lookup"><span data-stu-id="9ee71-137">The Device SDKs support the following network protocols for connecting to an IoT hub:</span></span>

- <span data-ttu-id="9ee71-138">MQTT</span><span class="sxs-lookup"><span data-stu-id="9ee71-138">MQTT</span></span>
- <span data-ttu-id="9ee71-139">AMQP</span><span class="sxs-lookup"><span data-stu-id="9ee71-139">AMQP</span></span>
- <span data-ttu-id="9ee71-140">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9ee71-140">HTTPS</span></span>

<span data-ttu-id="9ee71-141">For information about these difference protocols and guidance on choosing one, see [Choose a communication protocol](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-protocols).</span><span class="sxs-lookup"><span data-stu-id="9ee71-141">For information about these difference protocols and guidance on choosing one, see [Choose a communication protocol](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-protocols).</span></span>

<span data-ttu-id="9ee71-142">If your device can't use any of the supported protocols, you can use Azure IoT Edge to do protocol conversion.</span><span class="sxs-lookup"><span data-stu-id="9ee71-142">If your device can't use any of the supported protocols, you can use Azure IoT Edge to do protocol conversion.</span></span> <span data-ttu-id="9ee71-143">IoT Edge supports other intelligence-on-the-edge scenarios to offload processing to the edge from the Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="9ee71-143">IoT Edge supports other intelligence-on-the-edge scenarios to offload processing to the edge from the Azure IoT Central application.</span></span>

## <a name="security"></a><span data-ttu-id="9ee71-144">Security</span><span class="sxs-lookup"><span data-stu-id="9ee71-144">Security</span></span>

<span data-ttu-id="9ee71-145">All data exchanged between devices and your Azure IoT Central is encrypted.</span><span class="sxs-lookup"><span data-stu-id="9ee71-145">All data exchanged between devices and your Azure IoT Central is encrypted.</span></span> <span data-ttu-id="9ee71-146">IoT Hub authenticates every request from a device that connects to any of the device-facing IoT Hub endpoints.</span><span class="sxs-lookup"><span data-stu-id="9ee71-146">IoT Hub authenticates every request from a device that connects to any of the device-facing IoT Hub endpoints.</span></span> <span data-ttu-id="9ee71-147">To avoid exchanging credentials over the wire, a device uses signed tokens to authenticate.</span><span class="sxs-lookup"><span data-stu-id="9ee71-147">To avoid exchanging credentials over the wire, a device uses signed tokens to authenticate.</span></span> <span data-ttu-id="9ee71-148">For more information, see, [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).</span><span class="sxs-lookup"><span data-stu-id="9ee71-148">For more information, see, [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).</span></span>

> [!NOTE]
> <span data-ttu-id="9ee71-149">Currently, devices that connect to Azure IoT Central must use SAS tokens.</span><span class="sxs-lookup"><span data-stu-id="9ee71-149">Currently, devices that connect to Azure IoT Central must use SAS tokens.</span></span> <span data-ttu-id="9ee71-150">X.509 certificates are not supported for devices that connect to Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="9ee71-150">X.509 certificates are not supported for devices that connect to Azure IoT Central.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ee71-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ee71-151">Next steps</span></span>

<span data-ttu-id="9ee71-152">Now that you have learned about device connectivity in Azure IoT Central, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="9ee71-152">Now that you have learned about device connectivity in Azure IoT Central, here are the suggested next steps:</span></span>

- [<span data-ttu-id="9ee71-153">Prepare and connect a DevKit device</span><span class="sxs-lookup"><span data-stu-id="9ee71-153">Prepare and connect a DevKit device</span></span>](howto-connect-devkit.md)
- [<span data-ttu-id="9ee71-154">Prepare and connect a Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9ee71-154">Prepare and connect a Raspberry Pi</span></span>](howto-connect-raspberry-pi-python.md)
- [<span data-ttu-id="9ee71-155">Connect a generic Node.js client to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="9ee71-155">Connect a generic Node.js client to your Azure IoT Central application</span></span>](howto-connect-nodejs.md)
