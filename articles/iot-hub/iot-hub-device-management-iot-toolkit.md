---
title: Azure IoT device management with Azure IoT Toolkit extension for Visual Studio Code | Microsoft Docs
description: Use the Azure IoT Toolkit extension for Visual Studio Code for Azure IoT Hub device management, featuring the Direct methods and the Twin's desired properties management options.
author: formulahendry
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 8/3/2018
ms.author: junhan
ms.openlocfilehash: e3a0d63fa3f2f4bdef85a95810fd6c4eb090b70b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856523"
---
# <a name="use-azure-iot-toolkit-extension-for-visual-studio-code-for-azure-iot-hub-device-management"></a><span data-ttu-id="9c735-103">Use Azure IoT Toolkit extension for Visual Studio Code for Azure IoT Hub device management</span><span class="sxs-lookup"><span data-stu-id="9c735-103">Use Azure IoT Toolkit extension for Visual Studio Code for Azure IoT Hub device management</span></span>

![End-to-end diagram](media/iot-hub-get-started-e2e-diagram/2.png)

<span data-ttu-id="9c735-105">[Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) is a useful Visual Studio Code extension that makes IoT Hub management easier.</span><span class="sxs-lookup"><span data-stu-id="9c735-105">[Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) is a useful Visual Studio Code extension that makes IoT Hub management easier.</span></span> <span data-ttu-id="9c735-106">It comes with management options that you can use to perform various tasks.</span><span class="sxs-lookup"><span data-stu-id="9c735-106">It comes with management options that you can use to perform various tasks.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

| <span data-ttu-id="9c735-107">Management option</span><span class="sxs-lookup"><span data-stu-id="9c735-107">Management option</span></span>          | <span data-ttu-id="9c735-108">Task</span><span class="sxs-lookup"><span data-stu-id="9c735-108">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9c735-109">Direct methods</span><span class="sxs-lookup"><span data-stu-id="9c735-109">Direct methods</span></span>             | <span data-ttu-id="9c735-110">Make a device act such as starting or stopping sending messages or rebooting the device.</span><span class="sxs-lookup"><span data-stu-id="9c735-110">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="9c735-111">Read device twin</span><span class="sxs-lookup"><span data-stu-id="9c735-111">Read device twin</span></span>           | <span data-ttu-id="9c735-112">Get the reported state of a device.</span><span class="sxs-lookup"><span data-stu-id="9c735-112">Get the reported state of a device.</span></span> <span data-ttu-id="9c735-113">For example, the device reports the LED is blinking now.</span><span class="sxs-lookup"><span data-stu-id="9c735-113">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="9c735-114">Update device twin</span><span class="sxs-lookup"><span data-stu-id="9c735-114">Update device twin</span></span>         | <span data-ttu-id="9c735-115">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="9c735-115">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="9c735-116">Cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="9c735-116">Cloud-to-device messages</span></span>   | <span data-ttu-id="9c735-117">Send notifications to a device.</span><span class="sxs-lookup"><span data-stu-id="9c735-117">Send notifications to a device.</span></span> <span data-ttu-id="9c735-118">For example, "It is very likely to rain today.</span><span class="sxs-lookup"><span data-stu-id="9c735-118">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="9c735-119">Don't forget to bring an umbrella."</span><span class="sxs-lookup"><span data-stu-id="9c735-119">Don't forget to bring an umbrella."</span></span>              |

<span data-ttu-id="9c735-120">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="9c735-120">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

<span data-ttu-id="9c735-121">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span><span class="sxs-lookup"><span data-stu-id="9c735-121">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="9c735-122">IoT Hub persists a device twin for each device that connects to it.</span><span class="sxs-lookup"><span data-stu-id="9c735-122">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="9c735-123">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="9c735-123">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9c735-124">What you learn</span><span class="sxs-lookup"><span data-stu-id="9c735-124">What you learn</span></span>

<span data-ttu-id="9c735-125">You learn using Azure IoT Toolkit extension for Visual Studio Code with various management options on your development machine.</span><span class="sxs-lookup"><span data-stu-id="9c735-125">You learn using Azure IoT Toolkit extension for Visual Studio Code with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9c735-126">What you do</span><span class="sxs-lookup"><span data-stu-id="9c735-126">What you do</span></span>

<span data-ttu-id="9c735-127">Run Azure IoT Toolkit extension for Visual Studio Code with various management options.</span><span class="sxs-lookup"><span data-stu-id="9c735-127">Run Azure IoT Toolkit extension for Visual Studio Code with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9c735-128">What you need</span><span class="sxs-lookup"><span data-stu-id="9c735-128">What you need</span></span>

- <span data-ttu-id="9c735-129">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9c735-129">An active Azure subscription.</span></span>
- <span data-ttu-id="9c735-130">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="9c735-130">An Azure IoT hub under your subscription.</span></span>
- [<span data-ttu-id="9c735-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9c735-131">Visual Studio Code</span></span>](https://code.visualstudio.com/)
- [<span data-ttu-id="9c735-132">Azure IoT Toolkit</span><span class="sxs-lookup"><span data-stu-id="9c735-132">Azure IoT Toolkit</span></span>](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit)

## <a name="sign-in-to-access-your-iot-hub"></a><span data-ttu-id="9c735-133">Sign in to access your IoT hub</span><span class="sxs-lookup"><span data-stu-id="9c735-133">Sign in to access your IoT hub</span></span>

1. <span data-ttu-id="9c735-134">In **Explorer** view of VS Code, expand **Azure IoT Hub Devices** section in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="9c735-134">In **Explorer** view of VS Code, expand **Azure IoT Hub Devices** section in the bottom left corner.</span></span>
1. <span data-ttu-id="9c735-135">Click **Select IoT Hub** in context menu.</span><span class="sxs-lookup"><span data-stu-id="9c735-135">Click **Select IoT Hub** in context menu.</span></span>
1. <span data-ttu-id="9c735-136">A pop-up will show in the bottom right corner to let you sign in to Azure for the first time.</span><span class="sxs-lookup"><span data-stu-id="9c735-136">A pop-up will show in the bottom right corner to let you sign in to Azure for the first time.</span></span>
1. <span data-ttu-id="9c735-137">After you sign in, your Azure Subscription list will be shown, then select Azure Subscription and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9c735-137">After you sign in, your Azure Subscription list will be shown, then select Azure Subscription and IoT Hub.</span></span>
1. <span data-ttu-id="9c735-138">The device list will be shown in **Azure IoT Hub Devices** tab in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="9c735-138">The device list will be shown in **Azure IoT Hub Devices** tab in a few seconds.</span></span>

   > [!Note]
   > <span data-ttu-id="9c735-139">You can also complete the set up by choosing **Set IoT Hub Connection String**.</span><span class="sxs-lookup"><span data-stu-id="9c735-139">You can also complete the set up by choosing **Set IoT Hub Connection String**.</span></span> <span data-ttu-id="9c735-140">Enter the connection string for the IoT hub that your IoT device connects to in the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="9c735-140">Enter the connection string for the IoT hub that your IoT device connects to in the pop-up window.</span></span>

## <a name="direct-methods"></a><span data-ttu-id="9c735-141">Direct methods</span><span class="sxs-lookup"><span data-stu-id="9c735-141">Direct methods</span></span>

1. <span data-ttu-id="9c735-142">Right-click your device and select **Invoke Direct Method**.</span><span class="sxs-lookup"><span data-stu-id="9c735-142">Right-click your device and select **Invoke Direct Method**.</span></span> 
1. <span data-ttu-id="9c735-143">Enter the method name and payload in input box.</span><span class="sxs-lookup"><span data-stu-id="9c735-143">Enter the method name and payload in input box.</span></span>
1. <span data-ttu-id="9c735-144">Results will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span><span class="sxs-lookup"><span data-stu-id="9c735-144">Results will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span></span>

## <a name="read-device-twin"></a><span data-ttu-id="9c735-145">Read device twin</span><span class="sxs-lookup"><span data-stu-id="9c735-145">Read device twin</span></span>

1. <span data-ttu-id="9c735-146">Right-click your device and select **Edit Device Twin**.</span><span class="sxs-lookup"><span data-stu-id="9c735-146">Right-click your device and select **Edit Device Twin**.</span></span> 
1. <span data-ttu-id="9c735-147">An **azure-iot-device-twin.json** file will be opened with the content of device twin.</span><span class="sxs-lookup"><span data-stu-id="9c735-147">An **azure-iot-device-twin.json** file will be opened with the content of device twin.</span></span>

## <a name="update-device-twin"></a><span data-ttu-id="9c735-148">Update device twin</span><span class="sxs-lookup"><span data-stu-id="9c735-148">Update device twin</span></span>

1. <span data-ttu-id="9c735-149">Make some edits of **tags** or **properties.desired** field.</span><span class="sxs-lookup"><span data-stu-id="9c735-149">Make some edits of **tags** or **properties.desired** field.</span></span>
1. <span data-ttu-id="9c735-150">Right-click on the **azure-iot-device-twin.json** file.</span><span class="sxs-lookup"><span data-stu-id="9c735-150">Right-click on the **azure-iot-device-twin.json** file.</span></span>
1. <span data-ttu-id="9c735-151">Select **Update Device Twin** to update the device twin.</span><span class="sxs-lookup"><span data-stu-id="9c735-151">Select **Update Device Twin** to update the device twin.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="9c735-152">Send cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="9c735-152">Send cloud-to-device messages</span></span>

<span data-ttu-id="9c735-153">To send a message from your IoT hub to your device, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="9c735-153">To send a message from your IoT hub to your device, follow these steps:</span></span>
 
1. <span data-ttu-id="9c735-154">Right-click your device and select **Send C2D Message to Device**.</span><span class="sxs-lookup"><span data-stu-id="9c735-154">Right-click your device and select **Send C2D Message to Device**.</span></span> 
1. <span data-ttu-id="9c735-155">Enter the message in input box.</span><span class="sxs-lookup"><span data-stu-id="9c735-155">Enter the message in input box.</span></span>
1. <span data-ttu-id="9c735-156">Results will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span><span class="sxs-lookup"><span data-stu-id="9c735-156">Results will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c735-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c735-157">Next steps</span></span>

<span data-ttu-id="9c735-158">You've learned how to use Azure IoT Toolkit extension for Visual Studio Code with various management options.</span><span class="sxs-lookup"><span data-stu-id="9c735-158">You've learned how to use Azure IoT Toolkit extension for Visual Studio Code with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
