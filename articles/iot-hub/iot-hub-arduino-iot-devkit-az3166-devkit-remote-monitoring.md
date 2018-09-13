---
title: IoT DevKit to cloud -- Connect IoT MXChip DevKit to Azure IoT Hub | Microsoft Docs
description: In this tutorial, learn how to send status of sensors on IoT DevKit AZ3166 to the Azure IoT Remote Monitoring solution accelerator.
author: liydu
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 02/02/2018
ms.author: liydu
ms.openlocfilehash: 79a44e3f5303aaf0d337333b482c2df670e0b3da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870214"
---
# <a name="connect-mxchip-iot-devkit-to-azure-iot-remote-monitoring-solution-accelerator"></a><span data-ttu-id="c3c4a-103">Connect MXChip IoT DevKit to Azure IoT Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="c3c4a-103">Connect MXChip IoT DevKit to Azure IoT Remote Monitoring solution accelerator</span></span>

<span data-ttu-id="c3c4a-104">In this tutorial, you learn how to run a sample app on your DevKit to send sensor data to your Azure IoT Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-104">In this tutorial, you learn how to run a sample app on your DevKit to send sensor data to your Azure IoT Remote Monitoring solution accelerator.</span></span>

<span data-ttu-id="c3c4a-105">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-105">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors.</span></span> <span data-ttu-id="c3c4a-106">You can develop for it using [Visual Studio Code extension for Arduino](https://aka.ms/arduino).</span><span class="sxs-lookup"><span data-stu-id="c3c4a-106">You can develop for it using [Visual Studio Code extension for Arduino](https://aka.ms/arduino).</span></span> <span data-ttu-id="c3c4a-107">And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-107">And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c3c4a-108">What you need</span><span class="sxs-lookup"><span data-stu-id="c3c4a-108">What you need</span></span>

<span data-ttu-id="c3c4a-109">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span><span class="sxs-lookup"><span data-stu-id="c3c4a-109">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span></span>

* <span data-ttu-id="c3c4a-110">Have your DevKit connected to Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="c3c4a-110">Have your DevKit connected to Wi-Fi</span></span>
* <span data-ttu-id="c3c4a-111">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="c3c4a-111">Prepare the development environment</span></span>

<span data-ttu-id="c3c4a-112">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-112">An active Azure subscription.</span></span> <span data-ttu-id="c3c4a-113">If you do not have one, you can register via one of these two methods:</span><span class="sxs-lookup"><span data-stu-id="c3c4a-113">If you do not have one, you can register via one of these two methods:</span></span>

* <span data-ttu-id="c3c4a-114">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="c3c4a-114">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/)</span></span>

* <span data-ttu-id="c3c4a-115">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are MSDN or Visual Studio subscriber</span><span class="sxs-lookup"><span data-stu-id="c3c4a-115">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are MSDN or Visual Studio subscriber</span></span>

## <a name="create-an-azure-iot-remote-monitoring-solution-accelerator"></a><span data-ttu-id="c3c4a-116">Create an Azure IoT Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="c3c4a-116">Create an Azure IoT Remote Monitoring solution accelerator</span></span>

1. <span data-ttu-id="c3c4a-117">Go to [Azure IoT solution accelerators site](https://www.azureiotsolutions.com/) and click **Create a new solution**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-117">Go to [Azure IoT solution accelerators site](https://www.azureiotsolutions.com/) and click **Create a new solution**.</span></span>

   ![Select Azure IoT solution accelerator type](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-solution-types.png)

   > [!WARNING]
   > <span data-ttu-id="c3c4a-119">By default, this sample creates an S2 IoT Hub after it creates one IoT Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-119">By default, this sample creates an S2 IoT Hub after it creates one IoT Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="c3c4a-120">If this IoT hub is not used with massive number of devices, we highly recommend you downgrade it from S2 to S1, and delete the IoT Remote Monitoring solution accelerator so the related IoT Hub can also be deleted, when you no longer need it.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-120">If this IoT hub is not used with massive number of devices, we highly recommend you downgrade it from S2 to S1, and delete the IoT Remote Monitoring solution accelerator so the related IoT Hub can also be deleted, when you no longer need it.</span></span> 

2. <span data-ttu-id="c3c4a-121">Select **Remote monitoring**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-121">Select **Remote monitoring**.</span></span>

3. <span data-ttu-id="c3c4a-122">Enter a solution name, select a subscription and a region, and then click **Create solution**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-122">Enter a solution name, select a subscription and a region, and then click **Create solution**.</span></span> <span data-ttu-id="c3c4a-123">The solution may take a while to be provisioned.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-123">The solution may take a while to be provisioned.</span></span>
  
   ![Create solution](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-solution.png)

4. <span data-ttu-id="c3c4a-125">After provisioning finishes, click **Launch**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-125">After provisioning finishes, click **Launch**.</span></span> <span data-ttu-id="c3c4a-126">Some simulated devices are created for the solution during the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-126">Some simulated devices are created for the solution during the provisioning process.</span></span> <span data-ttu-id="c3c4a-127">Click **DEVICES** to check them out.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-127">Click **DEVICES** to check them out.</span></span>

   ![Dashboard](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-solution-created.png)
  
   ![Console](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-console.png)

5. <span data-ttu-id="c3c4a-130">Click **ADD A DEVICE**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-130">Click **ADD A DEVICE**.</span></span>

6. <span data-ttu-id="c3c4a-131">Click **Add New** for **Custom Device**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-131">Click **Add New** for **Custom Device**.</span></span>
  
   ![Add new device](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-add-new-device.png)

7. <span data-ttu-id="c3c4a-133">Click **Let me define my own Device ID**, enter `AZ3166`, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-133">Click **Let me define my own Device ID**, enter `AZ3166`, and then click **Create**.</span></span>
  
   ![Create device with ID](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-device-configuration.png)

8. <span data-ttu-id="c3c4a-135">Make a note of **IoT Hub Hostname**, and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-135">Make a note of **IoT Hub Hostname**, and click **Done**.</span></span>

## <a name="open-the-remotemonitoring-sample"></a><span data-ttu-id="c3c4a-136">Open the RemoteMonitoring sample</span><span class="sxs-lookup"><span data-stu-id="c3c4a-136">Open the RemoteMonitoring sample</span></span>

1. <span data-ttu-id="c3c4a-137">Disconnect the DevKit from your computer, if it is connected.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-137">Disconnect the DevKit from your computer, if it is connected.</span></span>

2. <span data-ttu-id="c3c4a-138">Start VS Code.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-138">Start VS Code.</span></span>

3. <span data-ttu-id="c3c4a-139">Connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-139">Connect the DevKit to your computer.</span></span> <span data-ttu-id="c3c4a-140">VS Code automatically detects your DevKit and opens the following pages:</span><span class="sxs-lookup"><span data-stu-id="c3c4a-140">VS Code automatically detects your DevKit and opens the following pages:</span></span>

  * <span data-ttu-id="c3c4a-141">The DevKit introduction page.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-141">The DevKit introduction page.</span></span>
  * <span data-ttu-id="c3c4a-142">Arduino Examples: Hands-on samples to get started with DevKit.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-142">Arduino Examples: Hands-on samples to get started with DevKit.</span></span>

4. <span data-ttu-id="c3c4a-143">Expand left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > AzureIoT**, and select **RemoteMonitoring**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-143">Expand left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > AzureIoT**, and select **RemoteMonitoring**.</span></span> <span data-ttu-id="c3c4a-144">It opens a new VS Code window with a project folder in it.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-144">It opens a new VS Code window with a project folder in it.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3c4a-145">If you happen to close the pane, you can reopen it.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-145">If you happen to close the pane, you can reopen it.</span></span> <span data-ttu-id="c3c4a-146">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-146">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span></span>

## <a name="provision-required-azure-services"></a><span data-ttu-id="c3c4a-147">Provision required Azure services</span><span class="sxs-lookup"><span data-stu-id="c3c4a-147">Provision required Azure services</span></span>

<span data-ttu-id="c3c4a-148">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by entering `task cloud-provision` in the provided text box.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-148">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by entering `task cloud-provision` in the provided text box.</span></span>

<span data-ttu-id="c3c4a-149">In the VS Code terminal, an interactive command line guides you through provisioning the required Azure services.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-149">In the VS Code terminal, an interactive command line guides you through provisioning the required Azure services.</span></span>

![Provision Azure resources](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/provision.png)

## <a name="build-and-upload-the-device-code"></a><span data-ttu-id="c3c4a-151">Build and upload the device code</span><span class="sxs-lookup"><span data-stu-id="c3c4a-151">Build and upload the device code</span></span>

1. <span data-ttu-id="c3c4a-152">Use `Ctrl+P` (macOS: `Cmd + P`) and type **task config-device-connection**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-152">Use `Ctrl+P` (macOS: `Cmd + P`) and type **task config-device-connection**.</span></span>

2. <span data-ttu-id="c3c4a-153">The terminal asks whether you want to use a connection string that it retrieves from the `task cloud-provision` step.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-153">The terminal asks whether you want to use a connection string that it retrieves from the `task cloud-provision` step.</span></span> <span data-ttu-id="c3c4a-154">You could also input your own device connection string by clicking 'Create New...'</span><span class="sxs-lookup"><span data-stu-id="c3c4a-154">You could also input your own device connection string by clicking 'Create New...'</span></span>

3. <span data-ttu-id="c3c4a-155">The terminal prompts you to enter configuration mode.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-155">The terminal prompts you to enter configuration mode.</span></span> <span data-ttu-id="c3c4a-156">To do so, hold down button A, then push and release the reset button.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-156">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="c3c4a-157">The screen displays the DevKit ID and 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-157">The screen displays the DevKit ID and 'Configuration'.</span></span>

   ![Input connection string](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/config-device-connection.png)

4. <span data-ttu-id="c3c4a-159">After `task config-device-connection` finishes, click `F1` to load VS Code commands and select `Arduino: Upload`.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-159">After `task config-device-connection` finishes, click `F1` to load VS Code commands and select `Arduino: Upload`.</span></span> <span data-ttu-id="c3c4a-160">VS Code starts verifying and uploading the Arduino sketch.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-160">VS Code starts verifying and uploading the Arduino sketch.</span></span>
  
   ![Verification and upload of the Arduino sketch](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/arduino-upload.png)

<span data-ttu-id="c3c4a-162">The DevKit reboots and starts running the code.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-162">The DevKit reboots and starts running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="c3c4a-163">Test the project</span><span class="sxs-lookup"><span data-stu-id="c3c4a-163">Test the project</span></span>

<span data-ttu-id="c3c4a-164">When the sample app runs, DevKit sends sensor data over WiFi to your Azure IoT Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-164">When the sample app runs, DevKit sends sensor data over WiFi to your Azure IoT Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="c3c4a-165">To see the result, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="c3c4a-165">To see the result, follow these steps:</span></span>

1. <span data-ttu-id="c3c4a-166">Go to your Azure IoT Remote Monitoring solution accelerator, and click **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-166">Go to your Azure IoT Remote Monitoring solution accelerator, and click **DASHBOARD**.</span></span>

2. <span data-ttu-id="c3c4a-167">On the Remote Monitoring solution console, you will see your DevKit sensor status.</span><span class="sxs-lookup"><span data-stu-id="c3c4a-167">On the Remote Monitoring solution console, you will see your DevKit sensor status.</span></span>

   ![Sensor data in Azure IoT Remote Monitoring solution accelerator](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/sensor-status.png)

## <a name="change-device-id"></a><span data-ttu-id="c3c4a-169">Change device ID</span><span class="sxs-lookup"><span data-stu-id="c3c4a-169">Change device ID</span></span>

<span data-ttu-id="c3c4a-170">If you want to change the hardcoded **AZ3166** to a customized device ID in the code, modify the line of code displayed in the [remote monitoring example](https://github.com/Microsoft/devkit-sdk/blob/master/AZ3166/src/libraries/AzureIoT/examples/RemoteMonitoring/RemoteMonitoring.ino#L23).</span><span class="sxs-lookup"><span data-stu-id="c3c4a-170">If you want to change the hardcoded **AZ3166** to a customized device ID in the code, modify the line of code displayed in the [remote monitoring example](https://github.com/Microsoft/devkit-sdk/blob/master/AZ3166/src/libraries/AzureIoT/examples/RemoteMonitoring/RemoteMonitoring.ino#L23).</span></span>

## <a name="problems-and-feedback"></a><span data-ttu-id="c3c4a-171">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="c3c4a-171">Problems and feedback</span></span>

<span data-ttu-id="c3c4a-172">If you encounter problems, refer to [the IoT developer kit FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:</span><span class="sxs-lookup"><span data-stu-id="c3c4a-172">If you encounter problems, refer to [the IoT developer kit FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:</span></span>

* [<span data-ttu-id="c3c4a-173">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="c3c4a-173">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="c3c4a-174">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="c3c4a-174">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a><span data-ttu-id="c3c4a-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3c4a-175">Next steps</span></span>

<span data-ttu-id="c3c4a-176">Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and visualize the sensor data, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="c3c4a-176">Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and visualize the sensor data, here are the suggested next steps:</span></span>

* [<span data-ttu-id="c3c4a-177">Azure IoT solution accelerators overview</span><span class="sxs-lookup"><span data-stu-id="c3c4a-177">Azure IoT solution accelerators overview</span></span>](https://docs.microsoft.com/azure/iot-suite/)

* [<span data-ttu-id="c3c4a-178">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="c3c4a-178">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span></span>](https://docs.microsoft.com/microsoft-iot-central/howto-connect-devkit)

* [<span data-ttu-id="c3c4a-179">IoT developer kit</span><span class="sxs-lookup"><span data-stu-id="c3c4a-179">IoT developer kit</span></span>](https://microsoft.github.io/azure-iot-developer-kit/) 
