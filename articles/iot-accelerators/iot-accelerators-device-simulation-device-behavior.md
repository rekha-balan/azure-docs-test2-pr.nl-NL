---
title: Simulated device behavior in device simulation solution - Azure | Microsoft Docs
description: This article describes how to use JavaScript to define the behavior of a simulated device in the device simulation solution.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 01/29/2018
ms.topic: conceptual
ms.openlocfilehash: 43edbc653ddbd55aab5e722071de1f2cf4bcd1c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857274"
---
# <a name="implement-the-device-model-behavior"></a><span data-ttu-id="cc487-103">Implement the device model behavior</span><span class="sxs-lookup"><span data-stu-id="cc487-103">Implement the device model behavior</span></span>

<span data-ttu-id="cc487-104">The article [Understand the device model schema](iot-accelerators-device-simulation-device-schema.md) described the schema that defines a simulated device model.</span><span class="sxs-lookup"><span data-stu-id="cc487-104">The article [Understand the device model schema](iot-accelerators-device-simulation-device-schema.md) described the schema that defines a simulated device model.</span></span> <span data-ttu-id="cc487-105">That article referred to two types of JavaScript file that implement the behavior of a simulated device:</span><span class="sxs-lookup"><span data-stu-id="cc487-105">That article referred to two types of JavaScript file that implement the behavior of a simulated device:</span></span>

- <span data-ttu-id="cc487-106">**State**: JavaScript files that run at fixed intervals to update the internal state of the device.</span><span class="sxs-lookup"><span data-stu-id="cc487-106">**State**: JavaScript files that run at fixed intervals to update the internal state of the device.</span></span>
- <span data-ttu-id="cc487-107">**Method**: JavaScript files that run when the solution invokes a method on the device.</span><span class="sxs-lookup"><span data-stu-id="cc487-107">**Method**: JavaScript files that run when the solution invokes a method on the device.</span></span>

<span data-ttu-id="cc487-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="cc487-108">In this article, you learn how to:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="cc487-109">Control the state of a simulated device</span><span class="sxs-lookup"><span data-stu-id="cc487-109">Control the state of a simulated device</span></span>
> * <span data-ttu-id="cc487-110">Define how a simulated device responds to a method call from the IoT hub it's connected to</span><span class="sxs-lookup"><span data-stu-id="cc487-110">Define how a simulated device responds to a method call from the IoT hub it's connected to</span></span>
> * <span data-ttu-id="cc487-111">Debug your scripts</span><span class="sxs-lookup"><span data-stu-id="cc487-111">Debug your scripts</span></span>

[!INCLUDE [iot-accelerators-device-schema](../../includes/iot-accelerators-device-schema.md)]

## <a name="next-steps"></a><span data-ttu-id="cc487-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc487-112">Next steps</span></span>

<span data-ttu-id="cc487-113">This article described how to define the behavior of your own custom simulated device model.</span><span class="sxs-lookup"><span data-stu-id="cc487-113">This article described how to define the behavior of your own custom simulated device model.</span></span> <span data-ttu-id="cc487-114">This article showed you how to:</span><span class="sxs-lookup"><span data-stu-id="cc487-114">This article showed you how to:</span></span>

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * <span data-ttu-id="cc487-115">Control the state of a simulated device</span><span class="sxs-lookup"><span data-stu-id="cc487-115">Control the state of a simulated device</span></span>
> * <span data-ttu-id="cc487-116">Define how a simulated device responds to a method call from the IoT hub it's connected to</span><span class="sxs-lookup"><span data-stu-id="cc487-116">Define how a simulated device responds to a method call from the IoT hub it's connected to</span></span>
> * <span data-ttu-id="cc487-117">Debug your scripts</span><span class="sxs-lookup"><span data-stu-id="cc487-117">Debug your scripts</span></span>

<span data-ttu-id="cc487-118">Now that you've learned how to specify the behavior of a simulated device, the suggested next step is to learn how to [Create a simulated device](iot-accelerators-device-simulation-create-simulated-device.md).</span><span class="sxs-lookup"><span data-stu-id="cc487-118">Now that you've learned how to specify the behavior of a simulated device, the suggested next step is to learn how to [Create a simulated device](iot-accelerators-device-simulation-create-simulated-device.md).</span></span>

<span data-ttu-id="cc487-119">For more developer information about the Device Simulation solution, see the [Developer Reference Guide](https://github.com/Azure/device-simulation-dotnet/wiki/Simulation-Service-Developer-Reference-Guide).</span><span class="sxs-lookup"><span data-stu-id="cc487-119">For more developer information about the Device Simulation solution, see the [Developer Reference Guide](https://github.com/Azure/device-simulation-dotnet/wiki/Simulation-Service-Developer-Reference-Guide).</span></span>
