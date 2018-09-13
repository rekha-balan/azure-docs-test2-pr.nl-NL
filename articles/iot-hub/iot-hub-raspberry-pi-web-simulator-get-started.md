---
title: Simulated Raspberry Pi to cloud (Node.js) - Connect Raspberry Pi web simulator to Azure IoT Hub | Microsoft Docs
description: Connect Raspberry Pi web simulator to Azure IoT Hub for Raspberry Pi to send data to the Azure cloud.
author: rangv
manager: ''
keywords: raspberry pi simulator, azure iot raspberry pi, raspberry pi iot hub, raspberry pi send data to cloud, raspberry pi to cloud
ms.service: iot-hub
services: iot-hub
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: 2dd9b14ebd7e64a1073ab773b2f1ac8d8c05ac0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856707"
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="58e78-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="58e78-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="58e78-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="58e78-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="58e78-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](about-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="58e78-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](about-iot-hub.md).</span></span> 

<span data-ttu-id="58e78-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span><span class="sxs-lookup"><span data-stu-id="58e78-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="58e78-108">What you do</span><span class="sxs-lookup"><span data-stu-id="58e78-108">What you do</span></span>

* <span data-ttu-id="58e78-109">Learn the basics of Raspberry Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="58e78-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="58e78-110">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-110">Create an IoT hub.</span></span>
* <span data-ttu-id="58e78-111">Register a device for Pi in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="58e78-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="58e78-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="58e78-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="58e78-114">Then you run a sample application with the simulator to generate sensor data.</span><span class="sxs-lookup"><span data-stu-id="58e78-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="58e78-115">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="58e78-116">What you learn</span><span class="sxs-lookup"><span data-stu-id="58e78-116">What you learn</span></span>

* <span data-ttu-id="58e78-117">How to create an Azure IoT hub and get your new device connection string.</span><span class="sxs-lookup"><span data-stu-id="58e78-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="58e78-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="58e78-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="58e78-119">How to work with Raspberry Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="58e78-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="58e78-120">How to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="58e78-121">Overview of Raspberry Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="58e78-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="58e78-122">Click the button to launch Raspberry Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="58e78-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="58e78-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span><span class="sxs-lookup"><span data-stu-id="58e78-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="58e78-124">There are three areas in the web simulator.</span><span class="sxs-lookup"><span data-stu-id="58e78-124">There are three areas in the web simulator.</span></span>
1. <span data-ttu-id="58e78-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span><span class="sxs-lookup"><span data-stu-id="58e78-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="58e78-126">The area is locked in preview version so currently you cannot do customization.</span><span class="sxs-lookup"><span data-stu-id="58e78-126">The area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="58e78-127">Coding area - An online code editor for you to code with Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="58e78-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="58e78-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="58e78-129">The application is fully compatible with real Pi devices.</span><span class="sxs-lookup"><span data-stu-id="58e78-129">The application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="58e78-130">Integrated console window - It shows the output of your code.</span><span class="sxs-lookup"><span data-stu-id="58e78-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="58e78-131">At the top of this window, there are three buttons.</span><span class="sxs-lookup"><span data-stu-id="58e78-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="58e78-132">**Run** - Run the application in the coding area.</span><span class="sxs-lookup"><span data-stu-id="58e78-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="58e78-133">**Reset** - Reset the coding area to the default sample application.</span><span class="sxs-lookup"><span data-stu-id="58e78-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="58e78-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span><span class="sxs-lookup"><span data-stu-id="58e78-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="58e78-135">The Raspberry Pi web simulator is now available in preview version.</span><span class="sxs-lookup"><span data-stu-id="58e78-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="58e78-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="58e78-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="58e78-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="58e78-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Overview of Pi online simulator](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="58e78-139">Run a sample application on Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="58e78-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="58e78-140">In coding area, make sure you are working on the default sample application.</span><span class="sxs-lookup"><span data-stu-id="58e78-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="58e78-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span><span class="sxs-lookup"><span data-stu-id="58e78-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="58e78-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="58e78-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="58e78-143">Click **Run** or type `npm start` to run the application.</span><span class="sxs-lookup"><span data-stu-id="58e78-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="58e78-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="58e78-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="58e78-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="58e78-145">Next steps</span></span>

<span data-ttu-id="58e78-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="58e78-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
