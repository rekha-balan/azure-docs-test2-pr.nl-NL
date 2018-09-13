---
title: Introduction to Azure IoT Hub | Microsoft Docs
description: Learn about Azure IoT Hub. This IoT service is built for scalable data ingestion, device management, and security.
author: nberdy
ms.author: nberdy
ms.date: 07/04/2018
ms.topic: overview
ms.custom: mvc
ms.service: iot-hub
services: iot-hub
manager: briz
ms.openlocfilehash: f4254cd90d8cf3b9f4cd206b729a3d44784b377a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969431"
---
# <a name="what-is-azure-iot-hub"></a><span data-ttu-id="c94e6-104">What is Azure IoT Hub?</span><span class="sxs-lookup"><span data-stu-id="c94e6-104">What is Azure IoT Hub?</span></span>

<span data-ttu-id="c94e6-105">IoT Hub is a managed service, hosted in the cloud, that acts as a central message hub for bi-directional communication between your IoT application and the devices it manages.</span><span class="sxs-lookup"><span data-stu-id="c94e6-105">IoT Hub is a managed service, hosted in the cloud, that acts as a central message hub for bi-directional communication between your IoT application and the devices it manages.</span></span> <span data-ttu-id="c94e6-106">You can use Azure IoT Hub to build IoT solutions with reliable and secure communications between millions of IoT devices and a cloud-hosted solution backend.</span><span class="sxs-lookup"><span data-stu-id="c94e6-106">You can use Azure IoT Hub to build IoT solutions with reliable and secure communications between millions of IoT devices and a cloud-hosted solution backend.</span></span> <span data-ttu-id="c94e6-107">You can connect virtually any device to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c94e6-107">You can connect virtually any device to IoT Hub.</span></span>

<span data-ttu-id="c94e6-108">IoT Hub supports communications both from the device to the cloud and from the cloud to the device.</span><span class="sxs-lookup"><span data-stu-id="c94e6-108">IoT Hub supports communications both from the device to the cloud and from the cloud to the device.</span></span> <span data-ttu-id="c94e6-109">IoT Hub supports multiple messaging patterns such as device-to-cloud telemetry, file upload from devices, and request-reply methods to control your devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="c94e6-109">IoT Hub supports multiple messaging patterns such as device-to-cloud telemetry, file upload from devices, and request-reply methods to control your devices from the cloud.</span></span> <span data-ttu-id="c94e6-110">IoT Hub monitoring helps you maintain the health of your solution by tracking events such as device creation, device failures, and device connections.</span><span class="sxs-lookup"><span data-stu-id="c94e6-110">IoT Hub monitoring helps you maintain the health of your solution by tracking events such as device creation, device failures, and device connections.</span></span>

<span data-ttu-id="c94e6-111">IoT Hub's capabilities help you build scalable, full-featured IoT solutions such as managing industrial equipment used in manufacturing, tracking valuable assets in healthcare, and monitoring office building usage.</span><span class="sxs-lookup"><span data-stu-id="c94e6-111">IoT Hub's capabilities help you build scalable, full-featured IoT solutions such as managing industrial equipment used in manufacturing, tracking valuable assets in healthcare, and monitoring office building usage.</span></span>

## <a name="scale-your-solution"></a><span data-ttu-id="c94e6-112">Scale your solution</span><span class="sxs-lookup"><span data-stu-id="c94e6-112">Scale your solution</span></span>

<span data-ttu-id="c94e6-113">IoT Hub scales to millions of simultaneously connected devices and millions of events per second to support your IoT workloads.</span><span class="sxs-lookup"><span data-stu-id="c94e6-113">IoT Hub scales to millions of simultaneously connected devices and millions of events per second to support your IoT workloads.</span></span> <span data-ttu-id="c94e6-114">IoT Hub offers several tiers of service to best fit your scalability needs.</span><span class="sxs-lookup"><span data-stu-id="c94e6-114">IoT Hub offers several tiers of service to best fit your scalability needs.</span></span> <span data-ttu-id="c94e6-115">Learn more by checking out the [pricing page](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="c94e6-115">Learn more by checking out the [pricing page](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

## <a name="secure-your-communications"></a><span data-ttu-id="c94e6-116">Secure your communications</span><span class="sxs-lookup"><span data-stu-id="c94e6-116">Secure your communications</span></span>

<span data-ttu-id="c94e6-117">IoT Hub gives you a secure communication channel for your devices to send data.</span><span class="sxs-lookup"><span data-stu-id="c94e6-117">IoT Hub gives you a secure communication channel for your devices to send data.</span></span>

* <span data-ttu-id="c94e6-118">Per-device authentication enables each device to connect securely to IoT Hub and for each device to be managed securely.</span><span class="sxs-lookup"><span data-stu-id="c94e6-118">Per-device authentication enables each device to connect securely to IoT Hub and for each device to be managed securely.</span></span>

* <span data-ttu-id="c94e6-119">You have complete control over device access and can control connections at the per-device level.</span><span class="sxs-lookup"><span data-stu-id="c94e6-119">You have complete control over device access and can control connections at the per-device level.</span></span>

* <span data-ttu-id="c94e6-120">The [IoT Hub Device Provisioning Service](https://docs.microsoft.com/azure/iot-dps/) automatically provisions devices to the right IoT hub when the device first boots up.</span><span class="sxs-lookup"><span data-stu-id="c94e6-120">The [IoT Hub Device Provisioning Service](https://docs.microsoft.com/azure/iot-dps/) automatically provisions devices to the right IoT hub when the device first boots up.</span></span>

* <span data-ttu-id="c94e6-121">Multiple authentication types support a variety of device capabilities:</span><span class="sxs-lookup"><span data-stu-id="c94e6-121">Multiple authentication types support a variety of device capabilities:</span></span>

  * <span data-ttu-id="c94e6-122">SAS token-based authentication to quickly get started with your IoT solution.</span><span class="sxs-lookup"><span data-stu-id="c94e6-122">SAS token-based authentication to quickly get started with your IoT solution.</span></span>

  * <span data-ttu-id="c94e6-123">Individual X.509 certificate authentication for secure, standards-based authentication.</span><span class="sxs-lookup"><span data-stu-id="c94e6-123">Individual X.509 certificate authentication for secure, standards-based authentication.</span></span>

  * <span data-ttu-id="c94e6-124">X.509 CA authentication for simple, standards-based enrollment.</span><span class="sxs-lookup"><span data-stu-id="c94e6-124">X.509 CA authentication for simple, standards-based enrollment.</span></span>

## <a name="route-device-data"></a><span data-ttu-id="c94e6-125">Route device data</span><span class="sxs-lookup"><span data-stu-id="c94e6-125">Route device data</span></span>

<span data-ttu-id="c94e6-126">Built-in message routing functionality gives you flexibility to set up automatic rules-based message fan-out:</span><span class="sxs-lookup"><span data-stu-id="c94e6-126">Built-in message routing functionality gives you flexibility to set up automatic rules-based message fan-out:</span></span>

* <span data-ttu-id="c94e6-127">Use message routing to control where your hub sends device telemetry.</span><span class="sxs-lookup"><span data-stu-id="c94e6-127">Use message routing to control where your hub sends device telemetry.</span></span>

* <span data-ttu-id="c94e6-128">There is no additional cost to route messages to multiple endpoints.</span><span class="sxs-lookup"><span data-stu-id="c94e6-128">There is no additional cost to route messages to multiple endpoints.</span></span>

* <span data-ttu-id="c94e6-129">No-code routing rules take the place of custom message dispatcher code.</span><span class="sxs-lookup"><span data-stu-id="c94e6-129">No-code routing rules take the place of custom message dispatcher code.</span></span>

## <a name="integrate-with-other-services"></a><span data-ttu-id="c94e6-130">Integrate with other services</span><span class="sxs-lookup"><span data-stu-id="c94e6-130">Integrate with other services</span></span>

<span data-ttu-id="c94e6-131">You can integrate IoT Hub with other Azure services to build complete, end-to-end solutions.</span><span class="sxs-lookup"><span data-stu-id="c94e6-131">You can integrate IoT Hub with other Azure services to build complete, end-to-end solutions.</span></span> <span data-ttu-id="c94e6-132">For example, use:</span><span class="sxs-lookup"><span data-stu-id="c94e6-132">For example, use:</span></span>

* <span data-ttu-id="c94e6-133">[Azure Event Grid](https://docs.microsoft.com/azure/event-grid/) to enable your business to react quickly to critical events in a reliable, scalable, and secure manner.</span><span class="sxs-lookup"><span data-stu-id="c94e6-133">[Azure Event Grid](https://docs.microsoft.com/azure/event-grid/) to enable your business to react quickly to critical events in a reliable, scalable, and secure manner.</span></span>

* <span data-ttu-id="c94e6-134">[Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/) to automate business processes.</span><span class="sxs-lookup"><span data-stu-id="c94e6-134">[Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/) to automate business processes.</span></span>

* <span data-ttu-id="c94e6-135">[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/) to add machine learning and AI models to your solution.</span><span class="sxs-lookup"><span data-stu-id="c94e6-135">[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/) to add machine learning and AI models to your solution.</span></span>

* <span data-ttu-id="c94e6-136">[Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) to run real-time analytic computations on the data streaming from your devices.</span><span class="sxs-lookup"><span data-stu-id="c94e6-136">[Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) to run real-time analytic computations on the data streaming from your devices.</span></span>

## <a name="configure-and-control-your-devices"></a><span data-ttu-id="c94e6-137">Configure and control your devices</span><span class="sxs-lookup"><span data-stu-id="c94e6-137">Configure and control your devices</span></span>

<span data-ttu-id="c94e6-138">You can manage your devices connected to IoT Hub with an array of built-in functionality.</span><span class="sxs-lookup"><span data-stu-id="c94e6-138">You can manage your devices connected to IoT Hub with an array of built-in functionality.</span></span>

* <span data-ttu-id="c94e6-139">Store, synchronize, and query device metadata and state information for all your devices.</span><span class="sxs-lookup"><span data-stu-id="c94e6-139">Store, synchronize, and query device metadata and state information for all your devices.</span></span>

* <span data-ttu-id="c94e6-140">Set device state either per-device or based on common characteristics of devices.</span><span class="sxs-lookup"><span data-stu-id="c94e6-140">Set device state either per-device or based on common characteristics of devices.</span></span>

* <span data-ttu-id="c94e6-141">Automatically respond to a device-reported state change with message routing integration.</span><span class="sxs-lookup"><span data-stu-id="c94e6-141">Automatically respond to a device-reported state change with message routing integration.</span></span>

## <a name="make-your-solution-highly-available"></a><span data-ttu-id="c94e6-142">Make your solution highly available</span><span class="sxs-lookup"><span data-stu-id="c94e6-142">Make your solution highly available</span></span>

<span data-ttu-id="c94e6-143">There's a 99.9% [Service Level Agreement for IoT Hub](https://azure.microsoft.com/support/legal/sla/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="c94e6-143">There's a 99.9% [Service Level Agreement for IoT Hub](https://azure.microsoft.com/support/legal/sla/iot-hub/).</span></span> <span data-ttu-id="c94e6-144">The full [Azure SLA](https://azure.microsoft.com/support/legal/sla/) explains the guaranteed availability of Azure as a whole.</span><span class="sxs-lookup"><span data-stu-id="c94e6-144">The full [Azure SLA](https://azure.microsoft.com/support/legal/sla/) explains the guaranteed availability of Azure as a whole.</span></span>

## <a name="connect-your-devices"></a><span data-ttu-id="c94e6-145">Connect your devices</span><span class="sxs-lookup"><span data-stu-id="c94e6-145">Connect your devices</span></span>

<span data-ttu-id="c94e6-146">Use the [Azure IoT device SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) libraries to build applications that run on your devices and interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c94e6-146">Use the [Azure IoT device SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) libraries to build applications that run on your devices and interact with IoT Hub.</span></span> <span data-ttu-id="c94e6-147">Supported platforms include multiple Linux distributions, Windows, and real-time operating systems.</span><span class="sxs-lookup"><span data-stu-id="c94e6-147">Supported platforms include multiple Linux distributions, Windows, and real-time operating systems.</span></span> <span data-ttu-id="c94e6-148">Supported languages include:</span><span class="sxs-lookup"><span data-stu-id="c94e6-148">Supported languages include:</span></span>

* <span data-ttu-id="c94e6-149">C</span><span class="sxs-lookup"><span data-stu-id="c94e6-149">C</span></span>
* <span data-ttu-id="c94e6-150">C#</span><span class="sxs-lookup"><span data-stu-id="c94e6-150">C#</span></span>
* <span data-ttu-id="c94e6-151">Java</span><span class="sxs-lookup"><span data-stu-id="c94e6-151">Java</span></span>
* <span data-ttu-id="c94e6-152">Python</span><span class="sxs-lookup"><span data-stu-id="c94e6-152">Python</span></span>
* <span data-ttu-id="c94e6-153">Node.js.</span><span class="sxs-lookup"><span data-stu-id="c94e6-153">Node.js.</span></span>

<span data-ttu-id="c94e6-154">IoT Hub and the device SDKs support the following protocols for connecting devices:</span><span class="sxs-lookup"><span data-stu-id="c94e6-154">IoT Hub and the device SDKs support the following protocols for connecting devices:</span></span>

* <span data-ttu-id="c94e6-155">HTTPS</span><span class="sxs-lookup"><span data-stu-id="c94e6-155">HTTPS</span></span>
* <span data-ttu-id="c94e6-156">AMQP</span><span class="sxs-lookup"><span data-stu-id="c94e6-156">AMQP</span></span>
* <span data-ttu-id="c94e6-157">AMQP over WebSockets</span><span class="sxs-lookup"><span data-stu-id="c94e6-157">AMQP over WebSockets</span></span>
* <span data-ttu-id="c94e6-158">MQTT</span><span class="sxs-lookup"><span data-stu-id="c94e6-158">MQTT</span></span>
* <span data-ttu-id="c94e6-159">MQTT over WebSockets</span><span class="sxs-lookup"><span data-stu-id="c94e6-159">MQTT over WebSockets</span></span>

<span data-ttu-id="c94e6-160">If your solution cannot use the device libraries, devices can use the MQTT v3.1.1, HTTPS 1.1, or AMQP 1.0 protocols to connect natively to your hub.</span><span class="sxs-lookup"><span data-stu-id="c94e6-160">If your solution cannot use the device libraries, devices can use the MQTT v3.1.1, HTTPS 1.1, or AMQP 1.0 protocols to connect natively to your hub.</span></span>

<span data-ttu-id="c94e6-161">If your solution cannot use one of the supported protocols, you can extend IoT Hub to support custom protocols:</span><span class="sxs-lookup"><span data-stu-id="c94e6-161">If your solution cannot use one of the supported protocols, you can extend IoT Hub to support custom protocols:</span></span>

* <span data-ttu-id="c94e6-162">Use [Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/) to create a field gateway to perform protocol translation on the edge.</span><span class="sxs-lookup"><span data-stu-id="c94e6-162">Use [Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/) to create a field gateway to perform protocol translation on the edge.</span></span>

* <span data-ttu-id="c94e6-163">Customize the [Azure IoT protocol gateway](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) to perform protocol translation in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c94e6-163">Customize the [Azure IoT protocol gateway](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) to perform protocol translation in the cloud.</span></span>

## <a name="quotas-and-limits"></a><span data-ttu-id="c94e6-164">Quotas and limits</span><span class="sxs-lookup"><span data-stu-id="c94e6-164">Quotas and limits</span></span>

<span data-ttu-id="c94e6-165">Each Azure subscription has default quota limits in place to prevent service abuse, and these limits could impact the scope of your IoT solution.</span><span class="sxs-lookup"><span data-stu-id="c94e6-165">Each Azure subscription has default quota limits in place to prevent service abuse, and these limits could impact the scope of your IoT solution.</span></span> <span data-ttu-id="c94e6-166">The current limit on a per-subscription basis is 10 IoT hubs per subscription.</span><span class="sxs-lookup"><span data-stu-id="c94e6-166">The current limit on a per-subscription basis is 10 IoT hubs per subscription.</span></span> <span data-ttu-id="c94e6-167">You can request quota increases by contacting support.</span><span class="sxs-lookup"><span data-stu-id="c94e6-167">You can request quota increases by contacting support.</span></span> <span data-ttu-id="c94e6-168">For more details on quota limits:</span><span class="sxs-lookup"><span data-stu-id="c94e6-168">For more details on quota limits:</span></span>

* [<span data-ttu-id="c94e6-169">Azure subscription service limits</span><span class="sxs-lookup"><span data-stu-id="c94e6-169">Azure subscription service limits</span></span>](../azure-subscription-service-limits.md)

* [<span data-ttu-id="c94e6-170">IoT Hub throttling and you</span><span class="sxs-lookup"><span data-stu-id="c94e6-170">IoT Hub throttling and you</span></span>](https://azure.microsoft.com/blog/iot-hub-throttling-and-you/)

## <a name="next-steps"></a><span data-ttu-id="c94e6-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="c94e6-171">Next steps</span></span>

<span data-ttu-id="c94e6-172">To try out an end-to-end IoT solution, check out the IoT Hub quickstarts:</span><span class="sxs-lookup"><span data-stu-id="c94e6-172">To try out an end-to-end IoT solution, check out the IoT Hub quickstarts:</span></span>

* [<span data-ttu-id="c94e6-173">Quickstart: Send telemetry from a device to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="c94e6-173">Quickstart: Send telemetry from a device to an IoT hub</span></span>](quickstart-send-telemetry-node.md)