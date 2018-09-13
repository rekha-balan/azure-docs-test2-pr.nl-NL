---
title: Azure IoT protocol gateway | Microsoft Docs
description: How to use an Azure IoT protocol gateway to extend IoT Hub capabilities and protocol support to enable devices to connect to your hub using protocols not supported by IoT Hub natively.
services: iot-hub
documentationcenter: ''
author: kdotchkoff
manager: timlt
editor: ''
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: kdotchko
ms.openlocfilehash: e0a7c813da53bc6ab49a456f13227b62725c5fc4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553566"
---
# <a name="support-additional-protocols-for-iot-hub"></a><span data-ttu-id="606a1-103">Support additional protocols for IoT Hub</span><span class="sxs-lookup"><span data-stu-id="606a1-103">Support additional protocols for IoT Hub</span></span>
<span data-ttu-id="606a1-104">Azure IoT Hub natively supports communication over the MQTT, AMQP, and HTTP protocols.</span><span class="sxs-lookup"><span data-stu-id="606a1-104">Azure IoT Hub natively supports communication over the MQTT, AMQP, and HTTP protocols.</span></span> <span data-ttu-id="606a1-105">In some cases, devices or field gateways might not be able to use one of these standard protocols and will require protocol adaptation.</span><span class="sxs-lookup"><span data-stu-id="606a1-105">In some cases, devices or field gateways might not be able to use one of these standard protocols and will require protocol adaptation.</span></span> <span data-ttu-id="606a1-106">In such cases, you can use a custom gateway.</span><span class="sxs-lookup"><span data-stu-id="606a1-106">In such cases, you can use a custom gateway.</span></span> <span data-ttu-id="606a1-107">A custom gateway can enable protocol adaptation for IoT Hub endpoints by bridging the traffic to and from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="606a1-107">A custom gateway can enable protocol adaptation for IoT Hub endpoints by bridging the traffic to and from IoT Hub.</span></span> <span data-ttu-id="606a1-108">You can use the [Azure IoT protocol gateway](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) as a custom gateway to enable protocol adaptation for IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="606a1-108">You can use the [Azure IoT protocol gateway](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) as a custom gateway to enable protocol adaptation for IoT Hub.</span></span>

## <a name="azure-iot-protocol-gateway"></a><span data-ttu-id="606a1-109">Azure IoT protocol gateway</span><span class="sxs-lookup"><span data-stu-id="606a1-109">Azure IoT protocol gateway</span></span>
<span data-ttu-id="606a1-110">The Azure IoT protocol gateway is a framework for protocol adaptation that is designed for high-scale, bidirectional device communication with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="606a1-110">The Azure IoT protocol gateway is a framework for protocol adaptation that is designed for high-scale, bidirectional device communication with IoT Hub.</span></span> <span data-ttu-id="606a1-111">The protocol gateway is a pass-through component that accepts device connections over a specific protocol.</span><span class="sxs-lookup"><span data-stu-id="606a1-111">The protocol gateway is a pass-through component that accepts device connections over a specific protocol.</span></span> <span data-ttu-id="606a1-112">It bridges the traffic to IoT Hub over AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="606a1-112">It bridges the traffic to IoT Hub over AMQP 1.0.</span></span> <span data-ttu-id="606a1-113">The Azure IoT protocol gateway is available as an open-source software project to provide flexibility for adding support for various protocols and protocol versions.</span><span class="sxs-lookup"><span data-stu-id="606a1-113">The Azure IoT protocol gateway is available as an open-source software project to provide flexibility for adding support for various protocols and protocol versions.</span></span>

<span data-ttu-id="606a1-114">You can deploy the protocol gateway in Azure in a highly scalable way by using Azure Service Fabric, Azure Cloud Services worker roles, or Windows Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="606a1-114">You can deploy the protocol gateway in Azure in a highly scalable way by using Azure Service Fabric, Azure Cloud Services worker roles, or Windows Virtual Machines.</span></span> <span data-ttu-id="606a1-115">In addition, the protocol gateway can be deployed in on-premises environments, such as field gateways.</span><span class="sxs-lookup"><span data-stu-id="606a1-115">In addition, the protocol gateway can be deployed in on-premises environments, such as field gateways.</span></span>

<span data-ttu-id="606a1-116">The Azure IoT protocol gateway includes an MQTT protocol adapter that enables you to customize the MQTT protocol behavior if necessary.</span><span class="sxs-lookup"><span data-stu-id="606a1-116">The Azure IoT protocol gateway includes an MQTT protocol adapter that enables you to customize the MQTT protocol behavior if necessary.</span></span> <span data-ttu-id="606a1-117">Since IoT Hub provides built-in support for the MQTT v3.1.1 protocol, you should only consider using the MQTT protocol adapter if protocol customizations or specific requirements for additional functionality are required.</span><span class="sxs-lookup"><span data-stu-id="606a1-117">Since IoT Hub provides built-in support for the MQTT v3.1.1 protocol, you should only consider using the MQTT protocol adapter if protocol customizations or specific requirements for additional functionality are required.</span></span>

<span data-ttu-id="606a1-118">The MQTT adapter also demonstrates the programming model for building protocol adapters for other protocols.</span><span class="sxs-lookup"><span data-stu-id="606a1-118">The MQTT adapter also demonstrates the programming model for building protocol adapters for other protocols.</span></span> <span data-ttu-id="606a1-119">In addition, the Azure IoT protocol gateway programming model allows you to plug in custom components for specialized processing such as custom authentication, message transformations, compression/decompression, or encryption/decryption of traffic between the devices and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="606a1-119">In addition, the Azure IoT protocol gateway programming model allows you to plug in custom components for specialized processing such as custom authentication, message transformations, compression/decompression, or encryption/decryption of traffic between the devices and IoT Hub.</span></span>

<span data-ttu-id="606a1-120">For flexibility, the protocol gateway and MQTT implementation are provided in an open-source software project.</span><span class="sxs-lookup"><span data-stu-id="606a1-120">For flexibility, the protocol gateway and MQTT implementation are provided in an open-source software project.</span></span> <span data-ttu-id="606a1-121">This allows you to customize the implementation as needed.</span><span class="sxs-lookup"><span data-stu-id="606a1-121">This allows you to customize the implementation as needed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="606a1-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="606a1-122">Next steps</span></span>
<span data-ttu-id="606a1-123">To learn more about the Azure IoT protocol gateway and how to use and deploy it as part of your IoT solution, see:</span><span class="sxs-lookup"><span data-stu-id="606a1-123">To learn more about the Azure IoT protocol gateway and how to use and deploy it as part of your IoT solution, see:</span></span>

* [<span data-ttu-id="606a1-124">Azure IoT protocol gateway repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="606a1-124">Azure IoT protocol gateway repository on GitHub</span></span>](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [<span data-ttu-id="606a1-125">Azure IoT protocol gateway developer guide</span><span class="sxs-lookup"><span data-stu-id="606a1-125">Azure IoT protocol gateway developer guide</span></span>](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

<span data-ttu-id="606a1-126">To learn more about planning your IoT Hub deployment, see:</span><span class="sxs-lookup"><span data-stu-id="606a1-126">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="606a1-127">[Compare with Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="606a1-127">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="606a1-128">[Scaling, HA and DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="606a1-128">[Scaling, HA and DR][lnk-scaling]</span></span>
* <span data-ttu-id="606a1-129">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="606a1-129">[IoT Hub developer guide][lnk-devguide]</span></span>

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
