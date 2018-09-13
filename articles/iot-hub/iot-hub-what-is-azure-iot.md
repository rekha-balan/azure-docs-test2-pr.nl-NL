---
title: Azure solutions for Internet of Things (IoT Suite) | Microsoft Docs
description: Overview of a sample IoT solution architecture and how it relates to devices, the Azure IoT Hub service, Azure IoT device SDKs, Azure IoT service SDKs, and other Azure services.
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: dobett
ms.openlocfilehash: a0f3107636b2839abada4db3e1eb48ee11f321fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660703"
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="62e38-103">Next steps</span><span class="sxs-lookup"><span data-stu-id="62e38-103">Next steps</span></span>

<span data-ttu-id="62e38-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span><span class="sxs-lookup"><span data-stu-id="62e38-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="62e38-105">It enables the solution back end to:</span><span class="sxs-lookup"><span data-stu-id="62e38-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="62e38-106">Receive telemetry at scale from your devices.</span><span class="sxs-lookup"><span data-stu-id="62e38-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="62e38-107">Route data from your devices to a stream event processor.</span><span class="sxs-lookup"><span data-stu-id="62e38-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="62e38-108">Receive file uploads from devices.</span><span class="sxs-lookup"><span data-stu-id="62e38-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="62e38-109">Send cloud-to-device messages to specific devices.</span><span class="sxs-lookup"><span data-stu-id="62e38-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="62e38-110">You can use IoT Hub to implement your own solution back end.</span><span class="sxs-lookup"><span data-stu-id="62e38-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="62e38-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="62e38-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="62e38-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="62e38-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="62e38-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="62e38-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="62e38-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="62e38-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="62e38-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="62e38-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="62e38-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62e38-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="62e38-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="62e38-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="62e38-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span><span class="sxs-lookup"><span data-stu-id="62e38-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="62e38-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span><span class="sxs-lookup"><span data-stu-id="62e38-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="62e38-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span><span class="sxs-lookup"><span data-stu-id="62e38-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
