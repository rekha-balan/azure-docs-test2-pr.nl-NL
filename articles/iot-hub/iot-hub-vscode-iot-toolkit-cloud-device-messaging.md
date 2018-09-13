---
title: Manage Azure IoT Hub cloud device messaging with Azure IoT Toolkit extension for Visual Studio Code | Microsoft Docs
description: Learn how to use Azure IoT Toolkit extension for Visual Studio Code to monitor device to cloud messages and send cloud to device messages in Azure IoT Hub.
author: formulahendry
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 7/20/2018
ms.author: junhan
ms.openlocfilehash: 1f38b094351e1613a9afbd6266cd54bef32824fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855599"
---
# <a name="use-azure-iot-toolkit-extension-for-visual-studio-code-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="89af9-103">Use Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and IoT Hub</span><span class="sxs-lookup"><span data-stu-id="89af9-103">Use Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and IoT Hub</span></span>

![End-to-end diagram](media/iot-hub-get-started-e2e-diagram/2.png)

<span data-ttu-id="89af9-105">[Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) is a useful Visual Studio Code extension that makes IoT Hub management easier.</span><span class="sxs-lookup"><span data-stu-id="89af9-105">[Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) is a useful Visual Studio Code extension that makes IoT Hub management easier.</span></span> <span data-ttu-id="89af9-106">This article focuses on how to use Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="89af9-106">This article focuses on how to use Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and your IoT hub.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-partial.md)]

## <a name="what-you-will-learn"></a><span data-ttu-id="89af9-107">What you will learn</span><span class="sxs-lookup"><span data-stu-id="89af9-107">What you will learn</span></span>

<span data-ttu-id="89af9-108">You learn how to use Azure IoT Toolkit extension for Visual Studio Code to monitor device-to-cloud messages and to send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="89af9-108">You learn how to use Azure IoT Toolkit extension for Visual Studio Code to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="89af9-109">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="89af9-109">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="89af9-110">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span><span class="sxs-lookup"><span data-stu-id="89af9-110">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="89af9-111">What you will do</span><span class="sxs-lookup"><span data-stu-id="89af9-111">What you will do</span></span>

- <span data-ttu-id="89af9-112">Use Azure IoT Toolkit extension for Visual Studio Code to monitor device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="89af9-112">Use Azure IoT Toolkit extension for Visual Studio Code to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="89af9-113">Use Azure IoT Toolkit extension for Visual Studio Code to send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="89af9-113">Use Azure IoT Toolkit extension for Visual Studio Code to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="89af9-114">What you need</span><span class="sxs-lookup"><span data-stu-id="89af9-114">What you need</span></span>

- <span data-ttu-id="89af9-115">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="89af9-115">An active Azure subscription.</span></span>
- <span data-ttu-id="89af9-116">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="89af9-116">An Azure IoT hub under your subscription.</span></span>
- [<span data-ttu-id="89af9-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="89af9-117">Visual Studio Code</span></span>](https://code.visualstudio.com/)
- [<span data-ttu-id="89af9-118">Azure IoT Toolkit</span><span class="sxs-lookup"><span data-stu-id="89af9-118">Azure IoT Toolkit</span></span>](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit)

## <a name="sign-in-to-access-your-iot-hub"></a><span data-ttu-id="89af9-119">Sign in to access your IoT hub</span><span class="sxs-lookup"><span data-stu-id="89af9-119">Sign in to access your IoT hub</span></span>

1. <span data-ttu-id="89af9-120">In **Explorer** view of VS Code, expand **Azure IoT Hub Devices** section in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="89af9-120">In **Explorer** view of VS Code, expand **Azure IoT Hub Devices** section in the bottom left corner.</span></span>
1. <span data-ttu-id="89af9-121">Click **Select IoT Hub** in context menu.</span><span class="sxs-lookup"><span data-stu-id="89af9-121">Click **Select IoT Hub** in context menu.</span></span>
1. <span data-ttu-id="89af9-122">A pop-up will show in the bottom right corner to let you sign in to Azure for the first time.</span><span class="sxs-lookup"><span data-stu-id="89af9-122">A pop-up will show in the bottom right corner to let you sign in to Azure for the first time.</span></span>
1. <span data-ttu-id="89af9-123">After you sign in, your Azure Subscription list will be shown, then select Azure Subscription and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="89af9-123">After you sign in, your Azure Subscription list will be shown, then select Azure Subscription and IoT Hub.</span></span>
1. <span data-ttu-id="89af9-124">The device list will be shown in **Azure IoT Hub Devices** tab in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="89af9-124">The device list will be shown in **Azure IoT Hub Devices** tab in a few seconds.</span></span>

   > [!Note]
   > <span data-ttu-id="89af9-125">You can also complete the set up by choosing **Set IoT Hub Connection String**.</span><span class="sxs-lookup"><span data-stu-id="89af9-125">You can also complete the set up by choosing **Set IoT Hub Connection String**.</span></span> <span data-ttu-id="89af9-126">Enter the connection string for the IoT hub that your IoT device connects to in the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="89af9-126">Enter the connection string for the IoT hub that your IoT device connects to in the pop-up window.</span></span>
   
## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="89af9-127">Monitor device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="89af9-127">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="89af9-128">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="89af9-128">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="89af9-129">Right-click your device and select **Start Monitoring D2C Message**.</span><span class="sxs-lookup"><span data-stu-id="89af9-129">Right-click your device and select **Start Monitoring D2C Message**.</span></span>
1. <span data-ttu-id="89af9-130">The monitored messages will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span><span class="sxs-lookup"><span data-stu-id="89af9-130">The monitored messages will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span></span>
1. <span data-ttu-id="89af9-131">To stop monitoring, right-click the **OUTPUT** view and select **Stop Monitoring D2C Message**.</span><span class="sxs-lookup"><span data-stu-id="89af9-131">To stop monitoring, right-click the **OUTPUT** view and select **Stop Monitoring D2C Message**.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="89af9-132">Send cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="89af9-132">Send cloud-to-device messages</span></span>

<span data-ttu-id="89af9-133">To send a message from your IoT hub to your device, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="89af9-133">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="89af9-134">Right-click your device and select **Send C2D Message to Device**.</span><span class="sxs-lookup"><span data-stu-id="89af9-134">Right-click your device and select **Send C2D Message to Device**.</span></span> 
1. <span data-ttu-id="89af9-135">Enter the message in input box.</span><span class="sxs-lookup"><span data-stu-id="89af9-135">Enter the message in input box.</span></span>
1. <span data-ttu-id="89af9-136">Results will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span><span class="sxs-lookup"><span data-stu-id="89af9-136">Results will be shown in **OUTPUT** > **Azure IoT Toolkit** view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89af9-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="89af9-137">Next steps</span></span>

<span data-ttu-id="89af9-138">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="89af9-138">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
