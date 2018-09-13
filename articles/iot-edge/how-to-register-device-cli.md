---
title: Register a new Azure IoT Edge device (CLI) | Microsoft Docs
description: Use the IoT extension for Azure CLI 2.0 to register a new IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/27/2018
ms.topic: conceptual
ms.reviewer: menchi
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 451f4df31cd1c520b14227829923f72fe80c38c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965504"
---
# <a name="register-a-new-azure-iot-edge-device-with-azure-cli-20"></a><span data-ttu-id="d512c-103">Register a new Azure IoT Edge device with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d512c-103">Register a new Azure IoT Edge device with Azure CLI 2.0</span></span>

<span data-ttu-id="d512c-104">Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d512c-104">Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub.</span></span> <span data-ttu-id="d512c-105">Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads.</span><span class="sxs-lookup"><span data-stu-id="d512c-105">Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads.</span></span> 

<span data-ttu-id="d512c-106">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="d512c-106">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge.</span></span> <span data-ttu-id="d512c-107">It enables you to manage Azure IoT Hub resources, device provisioning service instances, and linked-hubs out of the box.</span><span class="sxs-lookup"><span data-stu-id="d512c-107">It enables you to manage Azure IoT Hub resources, device provisioning service instances, and linked-hubs out of the box.</span></span> <span data-ttu-id="d512c-108">The new IoT extension enriches Azure CLI 2.0 with features such as device management and full IoT Edge capability.</span><span class="sxs-lookup"><span data-stu-id="d512c-108">The new IoT extension enriches Azure CLI 2.0 with features such as device management and full IoT Edge capability.</span></span>

<span data-ttu-id="d512c-109">This article shows how to register a new IoT Edge device using Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="d512c-109">This article shows how to register a new IoT Edge device using Azure CLI 2.0.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d512c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d512c-110">Prerequisites</span></span>

* <span data-ttu-id="d512c-111">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d512c-111">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span></span> 
* <span data-ttu-id="d512c-112">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span><span class="sxs-lookup"><span data-stu-id="d512c-112">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span></span> <span data-ttu-id="d512c-113">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span><span class="sxs-lookup"><span data-stu-id="d512c-113">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span></span> <span data-ttu-id="d512c-114">Use `az –-version` to validate.</span><span class="sxs-lookup"><span data-stu-id="d512c-114">Use `az –-version` to validate.</span></span> <span data-ttu-id="d512c-115">This version supports az extension commands and introduces the Knack command framework.</span><span class="sxs-lookup"><span data-stu-id="d512c-115">This version supports az extension commands and introduces the Knack command framework.</span></span> 
* <span data-ttu-id="d512c-116">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span><span class="sxs-lookup"><span data-stu-id="d512c-116">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span></span>

## <a name="create-a-device"></a><span data-ttu-id="d512c-117">Create a device</span><span class="sxs-lookup"><span data-stu-id="d512c-117">Create a device</span></span>

<span data-ttu-id="d512c-118">Use the following command to create a new device identity in your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d512c-118">Use the following command to create a new device identity in your IoT hub:</span></span> 

   ```cli
   az iot hub device-identity create --device-id [device id] --hub-name [hub name] --edge-enabled
   ```

<span data-ttu-id="d512c-119">This command includes three parameters:</span><span class="sxs-lookup"><span data-stu-id="d512c-119">This command includes three parameters:</span></span>
* <span data-ttu-id="d512c-120">**device-id**: Provide a descriptive name that's unique to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d512c-120">**device-id**: Provide a descriptive name that's unique to your IoT hub.</span></span>
* <span data-ttu-id="d512c-121">**hub-name**: Provide the name of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d512c-121">**hub-name**: Provide the name of your IoT hub.</span></span>
* <span data-ttu-id="d512c-122">**edge-enabled**: This parameter declares that the device is for use with IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="d512c-122">**edge-enabled**: This parameter declares that the device is for use with IoT Edge.</span></span>

   ![Create IoT Edge device](./media/how-to-register-device-cli/Create-edge-device.png)

## <a name="view-all-devices"></a><span data-ttu-id="d512c-124">View all devices</span><span class="sxs-lookup"><span data-stu-id="d512c-124">View all devices</span></span>

<span data-ttu-id="d512c-125">Use the following command to view all devices in your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d512c-125">Use the following command to view all devices in your IoT hub:</span></span>

   ```cli
   az iot hub device-identity list --hub-name [hub name]
   ```

<span data-ttu-id="d512c-126">Any device that is registered as an IoT Edge device will have the property **capabilities.iotEdge** set to **true**.</span><span class="sxs-lookup"><span data-stu-id="d512c-126">Any device that is registered as an IoT Edge device will have the property **capabilities.iotEdge** set to **true**.</span></span> 

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="d512c-127">Retrieve the connection string</span><span class="sxs-lookup"><span data-stu-id="d512c-127">Retrieve the connection string</span></span>

<span data-ttu-id="d512c-128">When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d512c-128">When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.</span></span> <span data-ttu-id="d512c-129">Use the following command to return the connection string for a single device:</span><span class="sxs-lookup"><span data-stu-id="d512c-129">Use the following command to return the connection string for a single device:</span></span>

   ```cli
   az iot hub device-identity show-connection-string --device-id [device id] --hub-name [hub name] 
   ```

<span data-ttu-id="d512c-130">The device id parameter is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="d512c-130">The device id parameter is case-sensitive.</span></span> <span data-ttu-id="d512c-131">Don't copy the quotation marks around the connection string.</span><span class="sxs-lookup"><span data-stu-id="d512c-131">Don't copy the quotation marks around the connection string.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d512c-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="d512c-132">Next steps</span></span>

<span data-ttu-id="d512c-133">Learn how to [Deploy modules to a device with Azure CLI 2.0](how-to-deploy-modules-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d512c-133">Learn how to [Deploy modules to a device with Azure CLI 2.0](how-to-deploy-modules-cli.md)</span></span>