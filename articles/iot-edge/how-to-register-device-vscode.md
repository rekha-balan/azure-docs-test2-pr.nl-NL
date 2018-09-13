---
title: Register a new Azure IoT Edge device (VS Code) | Microsoft Docs
description: Use Visual Studio Code to create a new IoT Edge device in your Azure IoT hub
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/14/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 7902461f58df1b4fe0c3ed3b577f668fe8be4cc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870703"
---
# <a name="register-a-new-azure-iot-edge-device-from-visual-studio-code"></a><span data-ttu-id="116a0-103">Register a new Azure IoT Edge device from Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="116a0-103">Register a new Azure IoT Edge device from Visual Studio Code</span></span>

<span data-ttu-id="116a0-104">Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="116a0-104">Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub.</span></span> <span data-ttu-id="116a0-105">Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads.</span><span class="sxs-lookup"><span data-stu-id="116a0-105">Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads.</span></span> 

<span data-ttu-id="116a0-106">This article shows how to register a new IoT Edge device using Visual Studio Code (VS Code).</span><span class="sxs-lookup"><span data-stu-id="116a0-106">This article shows how to register a new IoT Edge device using Visual Studio Code (VS Code).</span></span> <span data-ttu-id="116a0-107">There are multiple ways to perform most operations in VS Code.</span><span class="sxs-lookup"><span data-stu-id="116a0-107">There are multiple ways to perform most operations in VS Code.</span></span> <span data-ttu-id="116a0-108">This article uses the Explorer, but you can also use the Command Palette to run most of the steps.</span><span class="sxs-lookup"><span data-stu-id="116a0-108">This article uses the Explorer, but you can also use the Command Palette to run most of the steps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="116a0-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="116a0-109">Prerequisites</span></span>

* <span data-ttu-id="116a0-110">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="116a0-110">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription</span></span>
* [<span data-ttu-id="116a0-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="116a0-111">Visual Studio Code</span></span>](https://code.visualstudio.com/) 
* <span data-ttu-id="116a0-112">[Azure IoT Edge extension](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="116a0-112">[Azure IoT Edge extension](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) for Visual Studio Code</span></span>

## <a name="sign-in-to-access-your-iot-hub"></a><span data-ttu-id="116a0-113">Sign in to access your IoT hub</span><span class="sxs-lookup"><span data-stu-id="116a0-113">Sign in to access your IoT hub</span></span>

<span data-ttu-id="116a0-114">You can use the Azure IoT extensions for Visual Studio Code to perform operations with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="116a0-114">You can use the Azure IoT extensions for Visual Studio Code to perform operations with your IoT hub.</span></span> <span data-ttu-id="116a0-115">For these operations to work, you need to sign in to your Azure account and select the IoT hub that you are working on.</span><span class="sxs-lookup"><span data-stu-id="116a0-115">For these operations to work, you need to sign in to your Azure account and select the IoT hub that you are working on.</span></span>

1. <span data-ttu-id="116a0-116">In Visual Studio Code, open the **Explorer** view.</span><span class="sxs-lookup"><span data-stu-id="116a0-116">In Visual Studio Code, open the **Explorer** view.</span></span>

2. <span data-ttu-id="116a0-117">At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="116a0-117">At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.</span></span> 

   ![Expand Azure IoT Hub Devices](./media/how-to-register-device-vscode/azure-iot-hub-devices.png)

3. <span data-ttu-id="116a0-119">Click on the **...** in the **Azure IoT Hub Devices** section header.</span><span class="sxs-lookup"><span data-stu-id="116a0-119">Click on the **...** in the **Azure IoT Hub Devices** section header.</span></span> <span data-ttu-id="116a0-120">If you don't see the ellipsis, hover over the header.</span><span class="sxs-lookup"><span data-stu-id="116a0-120">If you don't see the ellipsis, hover over the header.</span></span> 

4. <span data-ttu-id="116a0-121">Choose **Select IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="116a0-121">Choose **Select IoT Hub**.</span></span>

5. <span data-ttu-id="116a0-122">If you are not signed in to your Azure account, follow the prompts to do so.</span><span class="sxs-lookup"><span data-stu-id="116a0-122">If you are not signed in to your Azure account, follow the prompts to do so.</span></span> 

6. <span data-ttu-id="116a0-123">Select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="116a0-123">Select your Azure subscription.</span></span> 

7. <span data-ttu-id="116a0-124">Select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="116a0-124">Select your IoT hub.</span></span> 

## <a name="create-a-device"></a><span data-ttu-id="116a0-125">Create a device</span><span class="sxs-lookup"><span data-stu-id="116a0-125">Create a device</span></span>

1. <span data-ttu-id="116a0-126">In the VS Code Explorer, expand the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="116a0-126">In the VS Code Explorer, expand the **Azure IoT Hub Devices** section.</span></span> 

2. <span data-ttu-id="116a0-127">Click on the **...** in the **Azure IoT Hub Devices** section header.</span><span class="sxs-lookup"><span data-stu-id="116a0-127">Click on the **...** in the **Azure IoT Hub Devices** section header.</span></span> <span data-ttu-id="116a0-128">If you don't see the ellipsis, hover over the header.</span><span class="sxs-lookup"><span data-stu-id="116a0-128">If you don't see the ellipsis, hover over the header.</span></span> 

3. <span data-ttu-id="116a0-129">Select **Create IoT Edge Device**.</span><span class="sxs-lookup"><span data-stu-id="116a0-129">Select **Create IoT Edge Device**.</span></span> 

4. <span data-ttu-id="116a0-130">In the text box that opens, give your device an ID.</span><span class="sxs-lookup"><span data-stu-id="116a0-130">In the text box that opens, give your device an ID.</span></span> 

<span data-ttu-id="116a0-131">In the output screen, you see the result of the command.</span><span class="sxs-lookup"><span data-stu-id="116a0-131">In the output screen, you see the result of the command.</span></span> <span data-ttu-id="116a0-132">The device info is printed, which includes the **deviceId** that you provided and the **connectionString** that you can use to connect your physical device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="116a0-132">The device info is printed, which includes the **deviceId** that you provided and the **connectionString** that you can use to connect your physical device to your IoT hub.</span></span> 

## <a name="view-all-devices"></a><span data-ttu-id="116a0-133">View all devices</span><span class="sxs-lookup"><span data-stu-id="116a0-133">View all devices</span></span>

<span data-ttu-id="116a0-134">All the devices that connect to your IoT hub are listed in the **Azure IoT Hub Devices** section of the Visual Studio Code Explorer.</span><span class="sxs-lookup"><span data-stu-id="116a0-134">All the devices that connect to your IoT hub are listed in the **Azure IoT Hub Devices** section of the Visual Studio Code Explorer.</span></span> <span data-ttu-id="116a0-135">IoT Edge devices are distinguishable from non-Edge devices with a different icon, and the fact that they can be expanded to show the modules deployed to each device.</span><span class="sxs-lookup"><span data-stu-id="116a0-135">IoT Edge devices are distinguishable from non-Edge devices with a different icon, and the fact that they can be expanded to show the modules deployed to each device.</span></span> 

   ![View devices in VS Code](./media/how-to-register-device-vscode/view-devices.png)

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="116a0-137">Retrieve the connection string</span><span class="sxs-lookup"><span data-stu-id="116a0-137">Retrieve the connection string</span></span>

<span data-ttu-id="116a0-138">When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="116a0-138">When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.</span></span>

1. <span data-ttu-id="116a0-139">Right-click on the ID of your device in the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="116a0-139">Right-click on the ID of your device in the **Azure IoT Hub Devices** section.</span></span> 
2. <span data-ttu-id="116a0-140">Select **Copy Device Connection String**.</span><span class="sxs-lookup"><span data-stu-id="116a0-140">Select **Copy Device Connection String**.</span></span>

   <span data-ttu-id="116a0-141">The connection string is copied to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="116a0-141">The connection string is copied to your clipboard.</span></span> 

<span data-ttu-id="116a0-142">You can also select **Get Device Info** from the right-click menu to see all the device info, including the connection string, in the output window.</span><span class="sxs-lookup"><span data-stu-id="116a0-142">You can also select **Get Device Info** from the right-click menu to see all the device info, including the connection string, in the output window.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="116a0-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="116a0-143">Next steps</span></span>

<span data-ttu-id="116a0-144">Learn how to [Deploy modules to a device with Visual Studio Code](how-to-deploy-modules-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="116a0-144">Learn how to [Deploy modules to a device with Visual Studio Code](how-to-deploy-modules-vscode.md).</span></span>
