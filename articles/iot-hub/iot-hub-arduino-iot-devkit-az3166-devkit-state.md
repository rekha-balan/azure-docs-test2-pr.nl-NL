---
title: Use Azure device twins to control MXChip IoT DevKit user LED | Microsoft Docs
description: In this tutorial, learn how to monitor DevKit states and control the user LED with Azure IoT Hub device twins.
author: liydu
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 04/04/2018
ms.author: liydu
ms.openlocfilehash: 6bc1255c5bbb9cf74c97b88600f34e7fcd90ae4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864737"
---
# <a name="mxchip-iot-devkit"></a><span data-ttu-id="98754-103">MXChip IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="98754-103">MXChip IoT DevKit</span></span>

<span data-ttu-id="98754-104">You can use this example to monitor the MXChip IoT DevKit WiFi information and sensor states and to control the color of the user LED using Azure IoT Hub device twins.</span><span class="sxs-lookup"><span data-stu-id="98754-104">You can use this example to monitor the MXChip IoT DevKit WiFi information and sensor states and to control the color of the user LED using Azure IoT Hub device twins.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="98754-105">What you learn</span><span class="sxs-lookup"><span data-stu-id="98754-105">What you learn</span></span>

- <span data-ttu-id="98754-106">How to monitor the MXChip IoT DevKit sensor states.</span><span class="sxs-lookup"><span data-stu-id="98754-106">How to monitor the MXChip IoT DevKit sensor states.</span></span>

- <span data-ttu-id="98754-107">How to use Azure device twins to control the color of the DevKit's RGB LED.</span><span class="sxs-lookup"><span data-stu-id="98754-107">How to use Azure device twins to control the color of the DevKit's RGB LED.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="98754-108">What you need</span><span class="sxs-lookup"><span data-stu-id="98754-108">What you need</span></span>

- <span data-ttu-id="98754-109">Set up your development environment by following the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started).</span><span class="sxs-lookup"><span data-stu-id="98754-109">Set up your development environment by following the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started).</span></span>

- <span data-ttu-id="98754-110">From your GitBash terminal window (or other Git command-line interface), type the following commands:</span><span class="sxs-lookup"><span data-stu-id="98754-110">From your GitBash terminal window (or other Git command-line interface), type the following commands:</span></span>

   ```bash
   git clone https://github.com/DevKitExamples/DevKitState.git
   cd DevKitState
   code .
   ```

## <a name="provision-azure-services"></a><span data-ttu-id="98754-111">Provision Azure Services</span><span class="sxs-lookup"><span data-stu-id="98754-111">Provision Azure Services</span></span>

1. <span data-ttu-id="98754-112">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Task...** - **cloud-provision**.</span><span class="sxs-lookup"><span data-stu-id="98754-112">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Task...** - **cloud-provision**.</span></span>

2. <span data-ttu-id="98754-113">Your progress is displayed under the **TERMINAL** tab of the **Welcome** panel.</span><span class="sxs-lookup"><span data-stu-id="98754-113">Your progress is displayed under the **TERMINAL** tab of the **Welcome** panel.</span></span>

3. <span data-ttu-id="98754-114">When prompted with the message *What subscription would you like to choose*, select a subscription.</span><span class="sxs-lookup"><span data-stu-id="98754-114">When prompted with the message *What subscription would you like to choose*, select a subscription.</span></span>

4. <span data-ttu-id="98754-115">Select or choose a resource group.</span><span class="sxs-lookup"><span data-stu-id="98754-115">Select or choose a resource group.</span></span> 
 
   > [!NOTE]
   > <span data-ttu-id="98754-116">If you already have a free IoT Hub, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="98754-116">If you already have a free IoT Hub, you can skip this step.</span></span>

5. <span data-ttu-id="98754-117">When prompted with the message *What IoT hub would you like to choose*, select or create an IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="98754-117">When prompted with the message *What IoT hub would you like to choose*, select or create an IoT Hub.</span></span>

6. <span data-ttu-id="98754-118">Something similar to *function app: function app name: xxx*, is displayed.</span><span class="sxs-lookup"><span data-stu-id="98754-118">Something similar to *function app: function app name: xxx*, is displayed.</span></span> <span data-ttu-id="98754-119">Write down the function app name; it will be used in a later step.</span><span class="sxs-lookup"><span data-stu-id="98754-119">Write down the function app name; it will be used in a later step.</span></span>

7. <span data-ttu-id="98754-120">Wait for the Azure Resource Manager template deployment to finish, which is indicated when the message *Resource Manager template deployment: Done* is displayed.</span><span class="sxs-lookup"><span data-stu-id="98754-120">Wait for the Azure Resource Manager template deployment to finish, which is indicated when the message *Resource Manager template deployment: Done* is displayed.</span></span>

## <a name="deploy-function-app"></a><span data-ttu-id="98754-121">Deploy Function App</span><span class="sxs-lookup"><span data-stu-id="98754-121">Deploy Function App</span></span>

1. <span data-ttu-id="98754-122">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Task...** - **cloud-deploy**.</span><span class="sxs-lookup"><span data-stu-id="98754-122">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Task...** - **cloud-deploy**.</span></span>

2. <span data-ttu-id="98754-123">Wait for function app code uploading process to finish; the message *function app deploys: Done* is displayed.</span><span class="sxs-lookup"><span data-stu-id="98754-123">Wait for function app code uploading process to finish; the message *function app deploys: Done* is displayed.</span></span>

## <a name="configure-iot-hub-device-connection-string-in-devkit"></a><span data-ttu-id="98754-124">Configure IoT Hub Device Connection String in DevKit</span><span class="sxs-lookup"><span data-stu-id="98754-124">Configure IoT Hub Device Connection String in DevKit</span></span>

1. <span data-ttu-id="98754-125">Connect your MXChip IoT DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="98754-125">Connect your MXChip IoT DevKit to your computer.</span></span>

2. <span data-ttu-id="98754-126">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Task...** - **config-device-connection**</span><span class="sxs-lookup"><span data-stu-id="98754-126">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Task...** - **config-device-connection**</span></span>

3. <span data-ttu-id="98754-127">On the MXChip IoT DevKit, press and hold button **A**, press the **Reset** button, and then release button **A** to make the DekKit enter configuration mode.</span><span class="sxs-lookup"><span data-stu-id="98754-127">On the MXChip IoT DevKit, press and hold button **A**, press the **Reset** button, and then release button **A** to make the DekKit enter configuration mode.</span></span>

4. <span data-ttu-id="98754-128">Wait for connection string configuration process to be completed.</span><span class="sxs-lookup"><span data-stu-id="98754-128">Wait for connection string configuration process to be completed.</span></span>

## <a name="upload-arduino-code-to-devkit"></a><span data-ttu-id="98754-129">Upload Arduino Code to DevKit</span><span class="sxs-lookup"><span data-stu-id="98754-129">Upload Arduino Code to DevKit</span></span>

<span data-ttu-id="98754-130">With your MXChip IoT DevKit connected to your computer:</span><span class="sxs-lookup"><span data-stu-id="98754-130">With your MXChip IoT DevKit connected to your computer:</span></span>

1. <span data-ttu-id="98754-131">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Build Task...** The Arduino sketch is compiled and uploaded to the DevKit.</span><span class="sxs-lookup"><span data-stu-id="98754-131">Click the **Tasks** drop-down menu in Visual Studio Code and select **Run Build Task...** The Arduino sketch is compiled and uploaded to the DevKit.</span></span>

2. <span data-ttu-id="98754-132">When the sketch has been uploaded successfully, a *Build & Upload Sketch: success* message is displayed.</span><span class="sxs-lookup"><span data-stu-id="98754-132">When the sketch has been uploaded successfully, a *Build & Upload Sketch: success* message is displayed.</span></span>

## <a name="monitor-devkit-state-in-browser"></a><span data-ttu-id="98754-133">Monitor DevKit State in Browser</span><span class="sxs-lookup"><span data-stu-id="98754-133">Monitor DevKit State in Browser</span></span>

1. <span data-ttu-id="98754-134">In a Web browser, open the `DevKitState\web\index.html` file--which was created during the [What you need](#whatyouneed) step.</span><span class="sxs-lookup"><span data-stu-id="98754-134">In a Web browser, open the `DevKitState\web\index.html` file--which was created during the [What you need](#whatyouneed) step.</span></span>

2. <span data-ttu-id="98754-135">The following Web page appears:</span><span class="sxs-lookup"><span data-stu-id="98754-135">The following Web page appears:</span></span>![Specify the function app name.](media/iot-hub-arduino-iot-devkit-az3166-devkit-state/devkit-state-function-app-name.png)

3. <span data-ttu-id="98754-137">Input the function app name you wrote down earlier.</span><span class="sxs-lookup"><span data-stu-id="98754-137">Input the function app name you wrote down earlier.</span></span>

4. <span data-ttu-id="98754-138">Click the **Connect** button</span><span class="sxs-lookup"><span data-stu-id="98754-138">Click the **Connect** button</span></span>

5. <span data-ttu-id="98754-139">Within a few seconds, the page refreshes and displays the DevKit's WiFi connection status and the state of each of the onboard sensors.</span><span class="sxs-lookup"><span data-stu-id="98754-139">Within a few seconds, the page refreshes and displays the DevKit's WiFi connection status and the state of each of the onboard sensors.</span></span>

## <a name="control-the-devkits-user-led"></a><span data-ttu-id="98754-140">Control the DevKit's User LED</span><span class="sxs-lookup"><span data-stu-id="98754-140">Control the DevKit's User LED</span></span>

1. <span data-ttu-id="98754-141">Click the user LED graphic on the Web page illustration.</span><span class="sxs-lookup"><span data-stu-id="98754-141">Click the user LED graphic on the Web page illustration.</span></span>

2. <span data-ttu-id="98754-142">Within a few seconds, the screen refreshes and shows the current color status of the user LED.</span><span class="sxs-lookup"><span data-stu-id="98754-142">Within a few seconds, the screen refreshes and shows the current color status of the user LED.</span></span>

3. <span data-ttu-id="98754-143">Try changing the color value of the RGB LED by clicking in various locations on the RGB slider controls.</span><span class="sxs-lookup"><span data-stu-id="98754-143">Try changing the color value of the RGB LED by clicking in various locations on the RGB slider controls.</span></span>

## <a name="example-operation"></a><span data-ttu-id="98754-144">Example operation</span><span class="sxs-lookup"><span data-stu-id="98754-144">Example operation</span></span>

![Example test procedure](media/iot-hub-arduino-iot-devkit-az3166-devkit-state/devkit-state.gif)

> [!NOTE]
> <span data-ttu-id="98754-146">You can see raw data of device twin in Azure portal: IoT Hub -\> IoT devices -\> *\<your device\>* -\> Device Twin.</span><span class="sxs-lookup"><span data-stu-id="98754-146">You can see raw data of device twin in Azure portal: IoT Hub -\> IoT devices -\> *\<your device\>* -\> Device Twin.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98754-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="98754-147">Next steps</span></span>

<span data-ttu-id="98754-148">You have learned how to:</span><span class="sxs-lookup"><span data-stu-id="98754-148">You have learned how to:</span></span>
- <span data-ttu-id="98754-149">Connect an MXChip IoT DevKit device to your Azure IoT Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="98754-149">Connect an MXChip IoT DevKit device to your Azure IoT Remote Monitoring solution accelerator.</span></span>
- <span data-ttu-id="98754-150">Use the Azure IoT device twins function to sense and control the color of the DevKit's RGB LED.</span><span class="sxs-lookup"><span data-stu-id="98754-150">Use the Azure IoT device twins function to sense and control the color of the DevKit's RGB LED.</span></span>

<span data-ttu-id="98754-151">Here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="98754-151">Here are the suggested next steps:</span></span>

* [<span data-ttu-id="98754-152">Azure IoT Remote Monitoring solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="98754-152">Azure IoT Remote Monitoring solution accelerator overview</span></span>](https://docs.microsoft.com/azure/iot-suite/)
* [<span data-ttu-id="98754-153">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="98754-153">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span></span>](https://docs.microsoft.com/microsoft-iot-central/howto-connect-devkit)
