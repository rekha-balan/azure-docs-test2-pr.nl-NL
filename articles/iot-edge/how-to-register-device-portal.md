---
title: Register a new Azure IoT Edge device (portal) | Microsoft Docs
description: Use the Azure portal to register a new IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/05/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: b61594469df33e11c23c9cbe0b9542da374fefa3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864585"
---
# <a name="register-a-new-azure-iot-edge-device-from-the-azure-portal"></a><span data-ttu-id="59009-103">Register a new Azure IoT Edge device from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="59009-103">Register a new Azure IoT Edge device from the Azure portal</span></span>

<span data-ttu-id="59009-104">Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="59009-104">Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub.</span></span> <span data-ttu-id="59009-105">Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads.</span><span class="sxs-lookup"><span data-stu-id="59009-105">Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads.</span></span> 

<span data-ttu-id="59009-106">This article shows how to register a new IoT Edge device using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59009-106">This article shows how to register a new IoT Edge device using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59009-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59009-107">Prerequisites</span></span>

* <span data-ttu-id="59009-108">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="59009-108">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription.</span></span> 

## <a name="create-a-device"></a><span data-ttu-id="59009-109">Create a device</span><span class="sxs-lookup"><span data-stu-id="59009-109">Create a device</span></span>

<span data-ttu-id="59009-110">In the Azure portal, IoT Edge devices are created and managed separately from devices that connect to your IoT hub but aren't edge-enabled.</span><span class="sxs-lookup"><span data-stu-id="59009-110">In the Azure portal, IoT Edge devices are created and managed separately from devices that connect to your IoT hub but aren't edge-enabled.</span></span> 

1. <span data-ttu-id="59009-111">Sign in to the [Azure portal](https://portal.azure.com) and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="59009-111">Sign in to the [Azure portal](https://portal.azure.com) and navigate to your IoT hub.</span></span> 
2. <span data-ttu-id="59009-112">Select **IoT Edge** from the menu.</span><span class="sxs-lookup"><span data-stu-id="59009-112">Select **IoT Edge** from the menu.</span></span>
3. <span data-ttu-id="59009-113">Select **Add IoT Edge Device**.</span><span class="sxs-lookup"><span data-stu-id="59009-113">Select **Add IoT Edge Device**.</span></span> 
4. <span data-ttu-id="59009-114">Provide a descriptive device ID.</span><span class="sxs-lookup"><span data-stu-id="59009-114">Provide a descriptive device ID.</span></span> 
5. <span data-ttu-id="59009-115">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="59009-115">Select **Save**.</span></span> 

## <a name="view-all-devices"></a><span data-ttu-id="59009-116">View all devices</span><span class="sxs-lookup"><span data-stu-id="59009-116">View all devices</span></span>

<span data-ttu-id="59009-117">All the edge-enabled devices that connect to your IoT hub are listed on the **IoT Edge** page.</span><span class="sxs-lookup"><span data-stu-id="59009-117">All the edge-enabled devices that connect to your IoT hub are listed on the **IoT Edge** page.</span></span> 

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="59009-118">Retrieve the connection string</span><span class="sxs-lookup"><span data-stu-id="59009-118">Retrieve the connection string</span></span>

<span data-ttu-id="59009-119">When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="59009-119">When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.</span></span>

1. <span data-ttu-id="59009-120">From the **IoT Edge** page in the portal, click on the device ID from the list of Edge devices.</span><span class="sxs-lookup"><span data-stu-id="59009-120">From the **IoT Edge** page in the portal, click on the device ID from the list of Edge devices.</span></span> 
2. <span data-ttu-id="59009-121">Copy the value of either **Connection string—primary key** or **Connection string—secondary key**.</span><span class="sxs-lookup"><span data-stu-id="59009-121">Copy the value of either **Connection string—primary key** or **Connection string—secondary key**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="59009-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="59009-122">Next steps</span></span>

<span data-ttu-id="59009-123">Learn how to [Deploy modules to a device with the Azure portal](how-to-deploy-modules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="59009-123">Learn how to [Deploy modules to a device with the Azure portal](how-to-deploy-modules-portal.md)</span></span>