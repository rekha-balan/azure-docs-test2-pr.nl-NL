---
title: Device schema in device simulation solution - Azure | Microsoft Docs
description: This article describes the JSON schema that defines a simulated device in the device simulation solution.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 01/29/2018
ms.topic: conceptual
ms.openlocfilehash: b325873819caff139727ec15d6aecd2d4be89c9e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858100"
---
# <a name="understand-the-device-model-schema"></a><span data-ttu-id="b7c7c-103">Understand the device model schema</span><span class="sxs-lookup"><span data-stu-id="b7c7c-103">Understand the device model schema</span></span>

<span data-ttu-id="b7c7c-104">You can use the Device Simulation solution accelerator to generate test loads for solutions that use IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-104">You can use the Device Simulation solution accelerator to generate test loads for solutions that use IoT Hub.</span></span> <span data-ttu-id="b7c7c-105">When you deploy the Device Simulation solution, a collection of simulated devices is provisioned automatically.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-105">When you deploy the Device Simulation solution, a collection of simulated devices is provisioned automatically.</span></span> <span data-ttu-id="b7c7c-106">You can customize the existing simulated devices or create your own.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-106">You can customize the existing simulated devices or create your own.</span></span>

<span data-ttu-id="b7c7c-107">This article describes the device model schema that specifies the capabilities and behavior of a simulated device.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-107">This article describes the device model schema that specifies the capabilities and behavior of a simulated device.</span></span> <span data-ttu-id="b7c7c-108">The device model is stored in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-108">The device model is stored in a JSON file.</span></span>

<span data-ttu-id="b7c7c-109">The following articles are related to the current article:</span><span class="sxs-lookup"><span data-stu-id="b7c7c-109">The following articles are related to the current article:</span></span>

* <span data-ttu-id="b7c7c-110">[Implement the device model behavior](iot-accelerators-device-simulation-device-behavior.md) describes the JavaScript files you use to implement the behavior of a simulated device.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-110">[Implement the device model behavior](iot-accelerators-device-simulation-device-behavior.md) describes the JavaScript files you use to implement the behavior of a simulated device.</span></span>
* <span data-ttu-id="b7c7c-111">[Create a new simulated device](iot-accelerators-device-simulation-create-simulated-device.md) puts it all together and shows you how to deploy a new simulated device type to your solution.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-111">[Create a new simulated device](iot-accelerators-device-simulation-create-simulated-device.md) puts it all together and shows you how to deploy a new simulated device type to your solution.</span></span>

<span data-ttu-id="b7c7c-112">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="b7c7c-112">In this article, you learn how to:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="b7c7c-113">Use a JSON file to define a simulated device model</span><span class="sxs-lookup"><span data-stu-id="b7c7c-113">Use a JSON file to define a simulated device model</span></span>
> * <span data-ttu-id="b7c7c-114">Specify the properties the simulated device</span><span class="sxs-lookup"><span data-stu-id="b7c7c-114">Specify the properties the simulated device</span></span>
> * <span data-ttu-id="b7c7c-115">Specify the telemetry the simulated device sends</span><span class="sxs-lookup"><span data-stu-id="b7c7c-115">Specify the telemetry the simulated device sends</span></span>
> * <span data-ttu-id="b7c7c-116">Specify the cloud-to-device methods the device responds to</span><span class="sxs-lookup"><span data-stu-id="b7c7c-116">Specify the cloud-to-device methods the device responds to</span></span>

[!INCLUDE [iot-accelerators-device-schema](../../includes/iot-accelerators-device-schema.md)]

## <a name="next-steps"></a><span data-ttu-id="b7c7c-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7c7c-117">Next steps</span></span>

<span data-ttu-id="b7c7c-118">This article described how to create your own custom simulated device model.</span><span class="sxs-lookup"><span data-stu-id="b7c7c-118">This article described how to create your own custom simulated device model.</span></span> <span data-ttu-id="b7c7c-119">This article showed you how to:</span><span class="sxs-lookup"><span data-stu-id="b7c7c-119">This article showed you how to:</span></span>

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * <span data-ttu-id="b7c7c-120">Use a JSON file to define a simulated device model</span><span class="sxs-lookup"><span data-stu-id="b7c7c-120">Use a JSON file to define a simulated device model</span></span>
> * <span data-ttu-id="b7c7c-121">Specify the properties the simulated device</span><span class="sxs-lookup"><span data-stu-id="b7c7c-121">Specify the properties the simulated device</span></span>
> * <span data-ttu-id="b7c7c-122">Specify the telemetry the simulated device sends</span><span class="sxs-lookup"><span data-stu-id="b7c7c-122">Specify the telemetry the simulated device sends</span></span>
> * <span data-ttu-id="b7c7c-123">Specify the cloud-to-device methods the device responds to</span><span class="sxs-lookup"><span data-stu-id="b7c7c-123">Specify the cloud-to-device methods the device responds to</span></span>

<span data-ttu-id="b7c7c-124">Now that you've learned about the JSON schema, the suggested next step is to learn how to [implement the behavior of your simulated device](iot-accelerators-device-simulation-device-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b7c7c-124">Now that you've learned about the JSON schema, the suggested next step is to learn how to [implement the behavior of your simulated device](iot-accelerators-device-simulation-device-behavior.md).</span></span>

<span data-ttu-id="b7c7c-125">For more developer information about the Device Simulation solution, see the [Developer Reference Guide](https://github.com/Azure/device-simulation-dotnet/wiki/Simulation-Service-Developer-Reference-Guide).</span><span class="sxs-lookup"><span data-stu-id="b7c7c-125">For more developer information about the Device Simulation solution, see the [Developer Reference Guide](https://github.com/Azure/device-simulation-dotnet/wiki/Simulation-Service-Developer-Reference-Guide).</span></span>
