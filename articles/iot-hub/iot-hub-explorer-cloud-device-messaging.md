---
title: Manage Azure IoT Hub cloud device messaging with iothub-explorer | Microsoft Docs
description: Learn how to use the iothub-explorer CLI tool to monitor device to cloud (D2C) messages and send cloud to device (C2D) messages in Azure IoT Hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iothub explorer, cloud device messaging, iot hub cloud to device, cloud to device messaging
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: xshi
ms.openlocfilehash: 94e71fd5cb3a59aac1f2b634c5d70432a65456f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661058"
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="c067a-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c067a-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="c067a-105">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span><span class="sxs-lookup"><span data-stu-id="c067a-105">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="c067a-106">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c067a-106">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c067a-107">What you will learn</span><span class="sxs-lookup"><span data-stu-id="c067a-107">What you will learn</span></span>

<span data-ttu-id="c067a-108">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="c067a-108">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="c067a-109">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c067a-109">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="c067a-110">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span><span class="sxs-lookup"><span data-stu-id="c067a-110">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c067a-111">What you will do</span><span class="sxs-lookup"><span data-stu-id="c067a-111">What you will do</span></span>

- <span data-ttu-id="c067a-112">Use iothub-explorer to monitor device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="c067a-112">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="c067a-113">Use iothub-explorer to send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="c067a-113">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c067a-114">What you need</span><span class="sxs-lookup"><span data-stu-id="c067a-114">What you need</span></span>

- <span data-ttu-id="c067a-115">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="c067a-115">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="c067a-116">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c067a-116">An active Azure subscription.</span></span>
  - <span data-ttu-id="c067a-117">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="c067a-117">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="c067a-118">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c067a-118">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="c067a-119">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="c067a-119">iothub-explorer.</span></span> <span data-ttu-id="c067a-120">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="c067a-120">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="c067a-121">Monitor device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="c067a-121">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="c067a-122">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="c067a-122">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="c067a-123">Open a console window.</span><span class="sxs-lookup"><span data-stu-id="c067a-123">Open a console window.</span></span>
1. <span data-ttu-id="c067a-124">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="c067a-124">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login <IoTHubConnectionString>
   ```

   > [!Note]
   > <span data-ttu-id="c067a-125">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c067a-125">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="c067a-126">Make sure you've finished the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="c067a-126">Make sure you've finished the previous tutorial.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="c067a-127">Send cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="c067a-127">Send cloud-to-device messages</span></span>

<span data-ttu-id="c067a-128">To send a message from your IoT hub to your device, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="c067a-128">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="c067a-129">Open a console window.</span><span class="sxs-lookup"><span data-stu-id="c067a-129">Open a console window.</span></span>
1. <span data-ttu-id="c067a-130">Start a session on your IoT hub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="c067a-130">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login <IoTHubConnectionString>
   ```

1. <span data-ttu-id="c067a-131">Send a message to your device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="c067a-131">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="c067a-132">The command blinks the LED that is connected to your device and sends the message to your device.</span><span class="sxs-lookup"><span data-stu-id="c067a-132">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="c067a-133">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span><span class="sxs-lookup"><span data-stu-id="c067a-133">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c067a-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="c067a-134">Next steps</span></span>

<span data-ttu-id="c067a-135">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c067a-135">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]