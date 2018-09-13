---
title: Simulated device behavior in remote monitoring solution - Azure | Microsoft Docs
description: This article describes how to use JavaScript to define the behavior of a simulated device in the remote monitoring solution.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 01/29/2018
ms.topic: conceptual
ms.openlocfilehash: a983c7307308534140ab8999593ac4c8c6992a42
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865340"
---
# <a name="implement-the-device-model-behavior"></a><span data-ttu-id="9a050-103">Implement the device model behavior</span><span class="sxs-lookup"><span data-stu-id="9a050-103">Implement the device model behavior</span></span>

<span data-ttu-id="9a050-104">The article [Understand the device model schema](iot-accelerators-remote-monitoring-device-schema.md) described the schema that defines a simulated device model.</span><span class="sxs-lookup"><span data-stu-id="9a050-104">The article [Understand the device model schema](iot-accelerators-remote-monitoring-device-schema.md) described the schema that defines a simulated device model.</span></span> <span data-ttu-id="9a050-105">That article referred to two types of JavaScript file that implement the behavior of a simulated device:</span><span class="sxs-lookup"><span data-stu-id="9a050-105">That article referred to two types of JavaScript file that implement the behavior of a simulated device:</span></span>

- <span data-ttu-id="9a050-106">**State** JavaScript files that run at fixed intervals to update the internal state of the device.</span><span class="sxs-lookup"><span data-stu-id="9a050-106">**State** JavaScript files that run at fixed intervals to update the internal state of the device.</span></span>
- <span data-ttu-id="9a050-107">**Method** JavaScript files that run when the solution invokes a method on the device.</span><span class="sxs-lookup"><span data-stu-id="9a050-107">**Method** JavaScript files that run when the solution invokes a method on the device.</span></span>

<span data-ttu-id="9a050-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="9a050-108">In this article, you learn how to:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="9a050-109">Control the state of a simulated device</span><span class="sxs-lookup"><span data-stu-id="9a050-109">Control the state of a simulated device</span></span>
> * <span data-ttu-id="9a050-110">Define how a simulated device responds to a method call from the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="9a050-110">Define how a simulated device responds to a method call from the Remote Monitoring solution</span></span>
> * <span data-ttu-id="9a050-111">Debug your scripts</span><span class="sxs-lookup"><span data-stu-id="9a050-111">Debug your scripts</span></span>

[!INCLUDE [iot-accelerators-device-schema](../../includes/iot-accelerators-device-schema.md)]

## <a name="next-steps"></a><span data-ttu-id="9a050-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a050-112">Next steps</span></span>

<span data-ttu-id="9a050-113">This article described how to define the behavior of your own custom simulated device model.</span><span class="sxs-lookup"><span data-stu-id="9a050-113">This article described how to define the behavior of your own custom simulated device model.</span></span> <span data-ttu-id="9a050-114">This article showed you how to:</span><span class="sxs-lookup"><span data-stu-id="9a050-114">This article showed you how to:</span></span>

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * <span data-ttu-id="9a050-115">Control the state of a simulated device</span><span class="sxs-lookup"><span data-stu-id="9a050-115">Control the state of a simulated device</span></span>
> * <span data-ttu-id="9a050-116">Define how a simulated device responds to a method call from the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="9a050-116">Define how a simulated device responds to a method call from the Remote Monitoring solution</span></span>
> * <span data-ttu-id="9a050-117">Debug your scripts</span><span class="sxs-lookup"><span data-stu-id="9a050-117">Debug your scripts</span></span>

<span data-ttu-id="9a050-118">Now that you've learned how to specify the behavior of a simulated device, the suggested next step is to learn how to [Create a simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md).</span><span class="sxs-lookup"><span data-stu-id="9a050-118">Now that you've learned how to specify the behavior of a simulated device, the suggested next step is to learn how to [Create a simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md).</span></span>

<span data-ttu-id="9a050-119">For more developer information about the Remote Monitoring solution, see:</span><span class="sxs-lookup"><span data-stu-id="9a050-119">For more developer information about the Remote Monitoring solution, see:</span></span>

* [<span data-ttu-id="9a050-120">Developer Reference Guide</span><span class="sxs-lookup"><span data-stu-id="9a050-120">Developer Reference Guide</span></span>](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
* [<span data-ttu-id="9a050-121">Developer Troubleshooting Guide</span><span class="sxs-lookup"><span data-stu-id="9a050-121">Developer Troubleshooting Guide</span></span>](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Troubleshooting-Guide)

<!-- Next tutorials in the sequence -->
