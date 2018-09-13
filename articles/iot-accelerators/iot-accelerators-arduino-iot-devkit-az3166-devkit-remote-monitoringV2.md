---
title: IoT DevKit to cloud -- Connect IoT DevKit AZ3166 to Remote Monitoring IoT solution accelerator | Microsoft Docs
description: In this tutorial, learn how to send status of sensors on IoT DevKit AZ3166 to Remote Monitoring IoT solution accelerator for monitoring and visualization.
author: isabelcabezasm
manager: ''
ms.service: iot-accelerators
services: iot-accelerators
ms.devlang: c
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: isacabe
ms.openlocfilehash: 35ef6ef02e5ae8a4b9231121615f44e0dc00ad15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870323"
---
# <a name="connect-mxchip-iot-devkit-az3166-to-the-iot-remote-monitoring-solution-accelerator"></a><span data-ttu-id="429ae-103">Connect MXChip IoT DevKit AZ3166 to the IoT Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="429ae-103">Connect MXChip IoT DevKit AZ3166 to the IoT Remote Monitoring solution accelerator</span></span>

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

<span data-ttu-id="429ae-104">In this tutorial, you learn how to run a sample app on your DevKit to send sensor data to your solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="429ae-104">In this tutorial, you learn how to run a sample app on your DevKit to send sensor data to your solution accelerator.</span></span>

<span data-ttu-id="429ae-105">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors.</span><span class="sxs-lookup"><span data-stu-id="429ae-105">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors.</span></span> <span data-ttu-id="429ae-106">You can develop for it using [Azure IoT Workbench](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-iot-workbench) in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="429ae-106">You can develop for it using [Azure IoT Workbench](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-iot-workbench) in Visual Studio Code.</span></span> <span data-ttu-id="429ae-107">And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span><span class="sxs-lookup"><span data-stu-id="429ae-107">And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="429ae-108">What you need</span><span class="sxs-lookup"><span data-stu-id="429ae-108">What you need</span></span>

<span data-ttu-id="429ae-109">Go through the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) and **finish the following sections only**:</span><span class="sxs-lookup"><span data-stu-id="429ae-109">Go through the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) and **finish the following sections only**:</span></span>

* <span data-ttu-id="429ae-110">Prepare your hardware</span><span class="sxs-lookup"><span data-stu-id="429ae-110">Prepare your hardware</span></span>
* <span data-ttu-id="429ae-111">Configure Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="429ae-111">Configure Wi-Fi</span></span>
* <span data-ttu-id="429ae-112">Start using the DevKit</span><span class="sxs-lookup"><span data-stu-id="429ae-112">Start using the DevKit</span></span>
* <span data-ttu-id="429ae-113">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="429ae-113">Prepare the development environment</span></span>


## <a name="create-an-azure-iot-remote-monitoring-solution-accelerator"></a><span data-ttu-id="429ae-114">Create an Azure IoT Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="429ae-114">Create an Azure IoT Remote Monitoring solution accelerator</span></span>

<span data-ttu-id="429ae-115">The AZ3166 device you create in this tutorial sends data to an instance of the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="429ae-115">The AZ3166 device you create in this tutorial sends data to an instance of the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="429ae-116">If you haven't yet provisioned an instance in your Azure account, follow the [Quickstart](https://docs.microsoft.com/azure/iot-accelerators/quickstart-remote-monitoring-deploy) guide to do so.</span><span class="sxs-lookup"><span data-stu-id="429ae-116">If you haven't yet provisioned an instance in your Azure account, follow the [Quickstart](https://docs.microsoft.com/azure/iot-accelerators/quickstart-remote-monitoring-deploy) guide to do so.</span></span>

<span data-ttu-id="429ae-117">When the deployment for the Remote Monitoring solution finishes, open the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="429ae-117">When the deployment for the Remote Monitoring solution finishes, open the solution dashboard.</span></span>

![The solution dashboard](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-dashboard-info.png)

## <a name="add-a-device-to-the-remote-monitoring-solution"></a><span data-ttu-id="429ae-119">Add a device to the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="429ae-119">Add a device to the Remote Monitoring solution</span></span>

1. <span data-ttu-id="429ae-120">In the dashboard, go to **Devices** section and click the **New Device**.</span><span class="sxs-lookup"><span data-stu-id="429ae-120">In the dashboard, go to **Devices** section and click the **New Device**.</span></span>
   <span data-ttu-id="429ae-121">![Adding a new device](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-add-device.png)</span><span class="sxs-lookup"><span data-stu-id="429ae-121">![Adding a new device](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-add-device.png)</span></span>

2. <span data-ttu-id="429ae-122">Configure the device by using information below and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="429ae-122">Configure the device by using information below and click **Apply**.</span></span>
  * <span data-ttu-id="429ae-123">Device Type: **Physical**</span><span class="sxs-lookup"><span data-stu-id="429ae-123">Device Type: **Physical**</span></span>
  * <span data-ttu-id="429ae-124">Device ID: **AZ3166**</span><span class="sxs-lookup"><span data-stu-id="429ae-124">Device ID: **AZ3166**</span></span>
  * <span data-ttu-id="429ae-125">Authentication Type: **Symmetric Key**</span><span class="sxs-lookup"><span data-stu-id="429ae-125">Authentication Type: **Symmetric Key**</span></span>
  * <span data-ttu-id="429ae-126">Authentication Key: **Auto generate keys**</span><span class="sxs-lookup"><span data-stu-id="429ae-126">Authentication Key: **Auto generate keys**</span></span>
  
  ![Adding a new device form](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-add-new-device-form.png)

3. <span data-ttu-id="429ae-128">After the new device is created, copy the **Connection String primary key**.</span><span class="sxs-lookup"><span data-stu-id="429ae-128">After the new device is created, copy the **Connection String primary key**.</span></span> <span data-ttu-id="429ae-129">This is the device that is just created in Azure IoT Hub underneath.</span><span class="sxs-lookup"><span data-stu-id="429ae-129">This is the device that is just created in Azure IoT Hub underneath.</span></span>
  
  ![Device Connection String](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-new-device-connstring.png)

## <a name="open-the-remote-monitoring-sample-in-vs-code"></a><span data-ttu-id="429ae-131">Open the Remote Monitoring sample in VS Code</span><span class="sxs-lookup"><span data-stu-id="429ae-131">Open the Remote Monitoring sample in VS Code</span></span>

1. <span data-ttu-id="429ae-132">Make sure your IoT DevKit is **not connected** to your computer.</span><span class="sxs-lookup"><span data-stu-id="429ae-132">Make sure your IoT DevKit is **not connected** to your computer.</span></span> <span data-ttu-id="429ae-133">Start VS Code first, and then connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="429ae-133">Start VS Code first, and then connect the DevKit to your computer.</span></span>

1. <span data-ttu-id="429ae-134">Click `F1` to open the command palette, type and select **IoT Workbench: Examples**.</span><span class="sxs-lookup"><span data-stu-id="429ae-134">Click `F1` to open the command palette, type and select **IoT Workbench: Examples**.</span></span> <span data-ttu-id="429ae-135">Then select **IoT DevKit** as board.</span><span class="sxs-lookup"><span data-stu-id="429ae-135">Then select **IoT DevKit** as board.</span></span>

1. <span data-ttu-id="429ae-136">Find **Remote Monitoring** and click **Open Sample**.</span><span class="sxs-lookup"><span data-stu-id="429ae-136">Find **Remote Monitoring** and click **Open Sample**.</span></span> <span data-ttu-id="429ae-137">It opens a new VS Code window with project folder in it.</span><span class="sxs-lookup"><span data-stu-id="429ae-137">It opens a new VS Code window with project folder in it.</span></span>
  <span data-ttu-id="429ae-138">![IoT Workbench, select Remote Monitoring example](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-example.png)</span><span class="sxs-lookup"><span data-stu-id="429ae-138">![IoT Workbench, select Remote Monitoring example](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-example.png)</span></span>

## <a name="configure-iot-hub-device-connection-string"></a><span data-ttu-id="429ae-139">Configure IoT Hub device connection string</span><span class="sxs-lookup"><span data-stu-id="429ae-139">Configure IoT Hub device connection string</span></span>

1. <span data-ttu-id="429ae-140">Switch the IoT DevKit into **Configuration mode**.</span><span class="sxs-lookup"><span data-stu-id="429ae-140">Switch the IoT DevKit into **Configuration mode**.</span></span> <span data-ttu-id="429ae-141">To do so:</span><span class="sxs-lookup"><span data-stu-id="429ae-141">To do so:</span></span>
   * <span data-ttu-id="429ae-142">Hold down button **A**.</span><span class="sxs-lookup"><span data-stu-id="429ae-142">Hold down button **A**.</span></span>
   * <span data-ttu-id="429ae-143">Push and release the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="429ae-143">Push and release the **Reset** button.</span></span>

2. <span data-ttu-id="429ae-144">The screen displays the DevKit ID and 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="429ae-144">The screen displays the DevKit ID and 'Configuration'.</span></span>
   
  ![IoT DevKit Configuration Mode](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/devkit-configuration-mode.png)

3. <span data-ttu-id="429ae-146">Click `F1` to open the command palette, type and select **IoT Workbench: Device > Config Device Settings**.</span><span class="sxs-lookup"><span data-stu-id="429ae-146">Click `F1` to open the command palette, type and select **IoT Workbench: Device > Config Device Settings**.</span></span>

4. <span data-ttu-id="429ae-147">Paste the connection string you just copied click `Enter` to configure it.</span><span class="sxs-lookup"><span data-stu-id="429ae-147">Paste the connection string you just copied click `Enter` to configure it.</span></span>

## <a name="build-and-upload-the-device-code"></a><span data-ttu-id="429ae-148">Build and upload the device code</span><span class="sxs-lookup"><span data-stu-id="429ae-148">Build and upload the device code</span></span>

1. <span data-ttu-id="429ae-149">Click `F1` to open the command palette, type and select **IoT Workbench: Device > Device Upload**.</span><span class="sxs-lookup"><span data-stu-id="429ae-149">Click `F1` to open the command palette, type and select **IoT Workbench: Device > Device Upload**.</span></span>
  <span data-ttu-id="429ae-150">![IoT Workbench: Device - > Upload](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-device-upload.png)</span><span class="sxs-lookup"><span data-stu-id="429ae-150">![IoT Workbench: Device - > Upload](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-device-upload.png)</span></span>

1. <span data-ttu-id="429ae-151">VS Code then starts compiling and uploading the code to your DevKit.</span><span class="sxs-lookup"><span data-stu-id="429ae-151">VS Code then starts compiling and uploading the code to your DevKit.</span></span>
  <span data-ttu-id="429ae-152">![IoT Workbench: Device - > Uploaded](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-device-uploaded.png)</span><span class="sxs-lookup"><span data-stu-id="429ae-152">![IoT Workbench: Device - > Uploaded](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-device-uploaded.png)</span></span>

<span data-ttu-id="429ae-153">The DevKit reboots and starts running the code.</span><span class="sxs-lookup"><span data-stu-id="429ae-153">The DevKit reboots and starts running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="429ae-154">Test the project</span><span class="sxs-lookup"><span data-stu-id="429ae-154">Test the project</span></span>

### <a name="view-the-telemetry-sent-to-remote-monitoring-solution"></a><span data-ttu-id="429ae-155">View the telemetry sent to Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="429ae-155">View the telemetry sent to Remote Monitoring solution</span></span>

<span data-ttu-id="429ae-156">When the sample app runs, DevKit sends sensor data over Wi-Fi to your Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="429ae-156">When the sample app runs, DevKit sends sensor data over Wi-Fi to your Remote Monitoring solution.</span></span> <span data-ttu-id="429ae-157">To see the result, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="429ae-157">To see the result, follow these steps:</span></span>

1. <span data-ttu-id="429ae-158">Go to your solution dashboard, and click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="429ae-158">Go to your solution dashboard, and click **Devices**.</span></span>

1. <span data-ttu-id="429ae-159">Click on the device name (AZ3166) a tab opens on the right side of the dashboard, where you can see the sensor status on DevKit in real time.</span><span class="sxs-lookup"><span data-stu-id="429ae-159">Click on the device name (AZ3166) a tab opens on the right side of the dashboard, where you can see the sensor status on DevKit in real time.</span></span>
  <span data-ttu-id="429ae-160">![Sensor data in Azure IoT Suite](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="429ae-160">![Sensor data in Azure IoT Suite](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-dashboard.png)</span></span>

### <a name="send-a-c2d-message"></a><span data-ttu-id="429ae-161">Send a C2D message</span><span class="sxs-lookup"><span data-stu-id="429ae-161">Send a C2D message</span></span>

<span data-ttu-id="429ae-162">Remote Monitoring solution allows you to invoke remote method on the device.</span><span class="sxs-lookup"><span data-stu-id="429ae-162">Remote Monitoring solution allows you to invoke remote method on the device.</span></span> <span data-ttu-id="429ae-163">The sxample code publishes three methods that you can see in the **Method** section when the sensor is selected.</span><span class="sxs-lookup"><span data-stu-id="429ae-163">The sxample code publishes three methods that you can see in the **Method** section when the sensor is selected.</span></span>

![IoT DevKit Methods](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-methods.png)

<span data-ttu-id="429ae-165">Let us try change the color of one of the DevKit LEDs using the method "LedColor".</span><span class="sxs-lookup"><span data-stu-id="429ae-165">Let us try change the color of one of the DevKit LEDs using the method "LedColor".</span></span>

1. <span data-ttu-id="429ae-166">Select the **AZ3166** from device list and click on the **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="429ae-166">Select the **AZ3166** from device list and click on the **Jobs**.</span></span>

  ![Create a Job](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-job.png)

2. <span data-ttu-id="429ae-168">Configure the Jobs as below and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="429ae-168">Configure the Jobs as below and click **Apply**.</span></span>
  * <span data-ttu-id="429ae-169">Select Job: **Run method**</span><span class="sxs-lookup"><span data-stu-id="429ae-169">Select Job: **Run method**</span></span>
  * <span data-ttu-id="429ae-170">Method name: **LedColor**</span><span class="sxs-lookup"><span data-stu-id="429ae-170">Method name: **LedColor**</span></span>
  * <span data-ttu-id="429ae-171">Job Name: **ChangeLedColor**</span><span class="sxs-lookup"><span data-stu-id="429ae-171">Job Name: **ChangeLedColor**</span></span>
  
  ![Job settings](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-suite-change-color.png)

<span data-ttu-id="429ae-173">In several seconds, your DevKit should change the color of the RGB LED (below the button A).</span><span class="sxs-lookup"><span data-stu-id="429ae-173">In several seconds, your DevKit should change the color of the RGB LED (below the button A).</span></span>

![IoT DevKit red led](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-devkit-led.png)

## <a name="clean-up-resources"></a><span data-ttu-id="429ae-175">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="429ae-175">Clean up resources</span></span>

<span data-ttu-id="429ae-176">If you plan to move on to the tutorials, leave the Remote Monitoring solution accelerator deployed.</span><span class="sxs-lookup"><span data-stu-id="429ae-176">If you plan to move on to the tutorials, leave the Remote Monitoring solution accelerator deployed.</span></span>

<span data-ttu-id="429ae-177">If you no longer need the solution accelerator, delete it from the Provisioned solutions page, by selecting it, and then clicking Delete Solution:</span><span class="sxs-lookup"><span data-stu-id="429ae-177">If you no longer need the solution accelerator, delete it from the Provisioned solutions page, by selecting it, and then clicking Delete Solution:</span></span>

![Delete solution](media/quickstart-remote-monitoring-deploy/deletesolution.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="429ae-179">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="429ae-179">Problems and feedback</span></span>

<span data-ttu-id="429ae-180">If you encounter problems, refer to [the IoT DevKit FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:</span><span class="sxs-lookup"><span data-stu-id="429ae-180">If you encounter problems, refer to [the IoT DevKit FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:</span></span>

* [<span data-ttu-id="429ae-181">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="429ae-181">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="429ae-182">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="429ae-182">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a><span data-ttu-id="429ae-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="429ae-183">Next steps</span></span>

<span data-ttu-id="429ae-184">Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and visualize the sensor data, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="429ae-184">Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and visualize the sensor data, here are the suggested next steps:</span></span>

* [<span data-ttu-id="429ae-185">Azure IoT solution accelerators overview</span><span class="sxs-lookup"><span data-stu-id="429ae-185">Azure IoT solution accelerators overview</span></span>](https://docs.microsoft.com/azure/iot-suite/)
* [<span data-ttu-id="429ae-186">Customize the UI</span><span class="sxs-lookup"><span data-stu-id="429ae-186">Customize the UI</span></span>](../iot-accelerators/iot-accelerators-remote-monitoring-customize.md)
* [<span data-ttu-id="429ae-187">Connect IoT DevKit to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="429ae-187">Connect IoT DevKit to your Azure IoT Central application</span></span>](../iot-central/howto-connect-devkit.md)