---
title: Connect a Windows IoT Core device to your Azure IoT Central application | Microsoft Docs
description: As a device developer, learn how to connect an MXChip IoT DevKit device to your Azure IoT Central application.
author: miriambrus
ms.author: miriamb
ms.date: 04/09/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 73a23ace23d2373e238c6887c4a41c6037d233de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967318"
---
# <a name="connect-a-windows-iot-core-device-to-your-azure-iot-central-application"></a><span data-ttu-id="06e6b-103">Connect a Windows IoT Core device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="06e6b-103">Connect a Windows IoT Core device to your Azure IoT Central application</span></span>

<span data-ttu-id="06e6b-104">This article describes how, as a device developer, to connect a Windows IoT Core device to your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="06e6b-104">This article describes how, as a device developer, to connect a Windows IoT Core device to your Microsoft Azure IoT Central application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="06e6b-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="06e6b-105">Before you begin</span></span>

<span data-ttu-id="06e6b-106">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="06e6b-106">To complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="06e6b-107">An Azure IoT Central application created from the **Sample Devkits** application template.</span><span class="sxs-lookup"><span data-stu-id="06e6b-107">An Azure IoT Central application created from the **Sample Devkits** application template.</span></span> <span data-ttu-id="06e6b-108">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="06e6b-108">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span></span>
2. <span data-ttu-id="06e6b-109">A device running the Windows 10 IoT Core operating system.</span><span class="sxs-lookup"><span data-stu-id="06e6b-109">A device running the Windows 10 IoT Core operating system.</span></span> <span data-ttu-id="06e6b-110">For this walkthrough, we will use a Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="06e6b-110">For this walkthrough, we will use a Raspberry Pi.</span></span>


## <a name="sample-devkits-application"></a><span data-ttu-id="06e6b-111">**Sample Devkits** application</span><span class="sxs-lookup"><span data-stu-id="06e6b-111">**Sample Devkits** application</span></span>

<span data-ttu-id="06e6b-112">An application created from the **Sample Devkits** application template includes a **Windows IoT Core** device template with the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="06e6b-112">An application created from the **Sample Devkits** application template includes a **Windows IoT Core** device template with the following characteristics:</span></span> 

- <span data-ttu-id="06e6b-113">Telemetry which contains the measurements for the device **Humidity**, **Temperature** and **Pressure**.</span><span class="sxs-lookup"><span data-stu-id="06e6b-113">Telemetry which contains the measurements for the device **Humidity**, **Temperature** and **Pressure**.</span></span> 
- <span data-ttu-id="06e6b-114">Settings showing **Fan Speed**.</span><span class="sxs-lookup"><span data-stu-id="06e6b-114">Settings showing **Fan Speed**.</span></span>
- <span data-ttu-id="06e6b-115">Properties containing device property **die number** and **location** cloud property.</span><span class="sxs-lookup"><span data-stu-id="06e6b-115">Properties containing device property **die number** and **location** cloud property.</span></span>


<span data-ttu-id="06e6b-116">For full details on the configuration of the device template refer to [Windows IoT Core Device template details](howto-connect-windowsiotcore.md#windows-iot-core-device-template-details)</span><span class="sxs-lookup"><span data-stu-id="06e6b-116">For full details on the configuration of the device template refer to [Windows IoT Core Device template details](howto-connect-windowsiotcore.md#windows-iot-core-device-template-details)</span></span>

## <a name="add-a-real-device"></a><span data-ttu-id="06e6b-117">Add a real device</span><span class="sxs-lookup"><span data-stu-id="06e6b-117">Add a real device</span></span>

<span data-ttu-id="06e6b-118">In your Azure IoT Central application, add a real device from the **Windows IoT Core** device template and make a note of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="06e6b-118">In your Azure IoT Central application, add a real device from the **Windows IoT Core** device template and make a note of the device connection string.</span></span> <span data-ttu-id="06e6b-119">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span><span class="sxs-lookup"><span data-stu-id="06e6b-119">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span></span>

### <a name="prepare-the-windows-iot-core-device"></a><span data-ttu-id="06e6b-120">Prepare the Windows IoT Core device</span><span class="sxs-lookup"><span data-stu-id="06e6b-120">Prepare the Windows IoT Core device</span></span>

<span data-ttu-id="06e6b-121">To set up a Windows IoT Core device please follow the step by step guide at [Set up a Windows IoT Core device] (https://github.com/Azure/iot-central-firmware/tree/master/WindowsIoT#setup-a-physical-device).</span><span class="sxs-lookup"><span data-stu-id="06e6b-121">To set up a Windows IoT Core device please follow the step by step guide at [Set up a Windows IoT Core device] (https://github.com/Azure/iot-central-firmware/tree/master/WindowsIoT#setup-a-physical-device).</span></span>

### <a name="add-a-real-device"></a><span data-ttu-id="06e6b-122">Add a real device</span><span class="sxs-lookup"><span data-stu-id="06e6b-122">Add a real device</span></span>

<span data-ttu-id="06e6b-123">In your Azure IoT Central application, add a real device from the **Windows IoT Core** device template and make a note of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="06e6b-123">In your Azure IoT Central application, add a real device from the **Windows IoT Core** device template and make a note of the device connection string.</span></span> <span data-ttu-id="06e6b-124">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span><span class="sxs-lookup"><span data-stu-id="06e6b-124">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span></span>

## <a name="prepare-the-windows-10-iot-core-device"></a><span data-ttu-id="06e6b-125">Prepare the Windows 10 IoT Core device</span><span class="sxs-lookup"><span data-stu-id="06e6b-125">Prepare the Windows 10 IoT Core device</span></span>

### <a name="what-youll-need"></a><span data-ttu-id="06e6b-126">What you'll need</span><span class="sxs-lookup"><span data-stu-id="06e6b-126">What you'll need</span></span>

<span data-ttu-id="06e6b-127">To set up a physical Windows 10 IoT Core device, you will need to first have a device running Windows 10 IoT Core.</span><span class="sxs-lookup"><span data-stu-id="06e6b-127">To set up a physical Windows 10 IoT Core device, you will need to first have a device running Windows 10 IoT Core.</span></span> <span data-ttu-id="06e6b-128">Learn how to set up a Windows 10 IoT Core device [here](https://developer.microsoft.com/en-us/windows/iot/getstarted/prototype/setupdevice).</span><span class="sxs-lookup"><span data-stu-id="06e6b-128">Learn how to set up a Windows 10 IoT Core device [here](https://developer.microsoft.com/en-us/windows/iot/getstarted/prototype/setupdevice).</span></span>

<span data-ttu-id="06e6b-129">You will also need a client application that can communicate with Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="06e6b-129">You will also need a client application that can communicate with Azure IoT Central.</span></span> <span data-ttu-id="06e6b-130">You can either build your own custom application using the Azure SDK and deploy it to your device using Visual Studio, or you can download a [pre-built sample](https://developer.microsoft.com/en-us/windows/iot/samples) and simply deploy and run it on the device.</span><span class="sxs-lookup"><span data-stu-id="06e6b-130">You can either build your own custom application using the Azure SDK and deploy it to your device using Visual Studio, or you can download a [pre-built sample](https://developer.microsoft.com/en-us/windows/iot/samples) and simply deploy and run it on the device.</span></span> 

### <a name="deploying-the-sample-client-application"></a><span data-ttu-id="06e6b-131">Deploying the sample client application</span><span class="sxs-lookup"><span data-stu-id="06e6b-131">Deploying the sample client application</span></span>

<span data-ttu-id="06e6b-132">To deploy the client application from the previous step to your Windows 10 IoT device in order to prepare it:</span><span class="sxs-lookup"><span data-stu-id="06e6b-132">To deploy the client application from the previous step to your Windows 10 IoT device in order to prepare it:</span></span>

<span data-ttu-id="06e6b-133">**Ensure the connection string is stored on the device for the client application to use**</span><span class="sxs-lookup"><span data-stu-id="06e6b-133">**Ensure the connection string is stored on the device for the client application to use**</span></span>
* <span data-ttu-id="06e6b-134">On the desktop, save the connection string in a text file named connection.string.iothub.</span><span class="sxs-lookup"><span data-stu-id="06e6b-134">On the desktop, save the connection string in a text file named connection.string.iothub.</span></span>
* <span data-ttu-id="06e6b-135">Copy the text file to the device’s document folder: `[device-IP-address]\C$\Data\Users\DefaultAccount\Documents\connection.string.iothub`</span><span class="sxs-lookup"><span data-stu-id="06e6b-135">Copy the text file to the device’s document folder: `[device-IP-address]\C$\Data\Users\DefaultAccount\Documents\connection.string.iothub`</span></span>

<span data-ttu-id="06e6b-136">Once you've done that, you'll need to open the [Windows Device Portal](https://docs.microsoft.com/en-us/windows/iot-core/manage-your-device/deviceportal) by typing in http://[device-IP-address]:8080 into any browser.</span><span class="sxs-lookup"><span data-stu-id="06e6b-136">Once you've done that, you'll need to open the [Windows Device Portal](https://docs.microsoft.com/en-us/windows/iot-core/manage-your-device/deviceportal) by typing in http://[device-IP-address]:8080 into any browser.</span></span>

<span data-ttu-id="06e6b-137">From there and, as shown in the if below, you'll want to:</span><span class="sxs-lookup"><span data-stu-id="06e6b-137">From there and, as shown in the if below, you'll want to:</span></span>
1. <span data-ttu-id="06e6b-138">Expand the "Apps" node on the left.</span><span class="sxs-lookup"><span data-stu-id="06e6b-138">Expand the "Apps" node on the left.</span></span>
2. <span data-ttu-id="06e6b-139">Click "Quick-run samples".</span><span class="sxs-lookup"><span data-stu-id="06e6b-139">Click "Quick-run samples".</span></span>
3. <span data-ttu-id="06e6b-140">Click "Azure IoT Hub Client".</span><span class="sxs-lookup"><span data-stu-id="06e6b-140">Click "Azure IoT Hub Client".</span></span>
4. <span data-ttu-id="06e6b-141">Click "Deploy and run".</span><span class="sxs-lookup"><span data-stu-id="06e6b-141">Click "Deploy and run".</span></span>

![Gif of Azure IoT Hub Client on Windows Device Portal](./media/howto-connect-windowsiotcore/iothubapp.gif)

<span data-ttu-id="06e6b-143">When successful, the application will launch on the device and look like this:</span><span class="sxs-lookup"><span data-stu-id="06e6b-143">When successful, the application will launch on the device and look like this:</span></span>

![Screenshot of Azure IoT Hub Client app](./media/howto-connect-windowsiotcore/IoTHubForegroundClientScreenshot.png)

<span data-ttu-id="06e6b-145">In Azure IoT Central, you can see how the code running on the Raspberry Pi interacts with the application:</span><span class="sxs-lookup"><span data-stu-id="06e6b-145">In Azure IoT Central, you can see how the code running on the Raspberry Pi interacts with the application:</span></span>

* <span data-ttu-id="06e6b-146">On the **Measurements** page for your real device, you can see the telemetry.</span><span class="sxs-lookup"><span data-stu-id="06e6b-146">On the **Measurements** page for your real device, you can see the telemetry.</span></span>
* <span data-ttu-id="06e6b-147">On the **Properties** page, you can see the value of the reported Die Number property.</span><span class="sxs-lookup"><span data-stu-id="06e6b-147">On the **Properties** page, you can see the value of the reported Die Number property.</span></span>
* <span data-ttu-id="06e6b-148">On the **Settings** page, you can change various settings on the Raspberry Pi such as voltage and fan speed.</span><span class="sxs-lookup"><span data-stu-id="06e6b-148">On the **Settings** page, you can change various settings on the Raspberry Pi such as voltage and fan speed.</span></span>

## <a name="download-the-source-code"></a><span data-ttu-id="06e6b-149">Download the source code</span><span class="sxs-lookup"><span data-stu-id="06e6b-149">Download the source code</span></span>

<span data-ttu-id="06e6b-150">If you want to explore and modify the source code for the client application, you can download it from GitHub [here](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/Azure/IoTHubClients).</span><span class="sxs-lookup"><span data-stu-id="06e6b-150">If you want to explore and modify the source code for the client application, you can download it from GitHub [here](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/Azure/IoTHubClients).</span></span> <span data-ttu-id="06e6b-151">If you plan to modify the code, you should follow these instructions in the readme file [here](https://github.com/Microsoft/Windows-iotcore-samples) for your desktop operating system.</span><span class="sxs-lookup"><span data-stu-id="06e6b-151">If you plan to modify the code, you should follow these instructions in the readme file [here](https://github.com/Microsoft/Windows-iotcore-samples) for your desktop operating system.</span></span>

> [!NOTE]
> <span data-ttu-id="06e6b-152">If **git** is not installed in your development environment, you can download it from [https://git-scm.com/download](https://git-scm.com/download).</span><span class="sxs-lookup"><span data-stu-id="06e6b-152">If **git** is not installed in your development environment, you can download it from [https://git-scm.com/download](https://git-scm.com/download).</span></span>

## <a name="windows-iot-core-device-template-details"></a><span data-ttu-id="06e6b-153">Windows IoT Core Device template details</span><span class="sxs-lookup"><span data-stu-id="06e6b-153">Windows IoT Core Device template details</span></span>

<span data-ttu-id="06e6b-154">An application created from the **Sample Devkits** application template includes a **Windows IoT Core** device template with the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="06e6b-154">An application created from the **Sample Devkits** application template includes a **Windows IoT Core** device template with the following characteristics:</span></span>

### <a name="telemetry-measurements"></a><span data-ttu-id="06e6b-155">Telemetry measurements</span><span class="sxs-lookup"><span data-stu-id="06e6b-155">Telemetry measurements</span></span>

| <span data-ttu-id="06e6b-156">Field name</span><span class="sxs-lookup"><span data-stu-id="06e6b-156">Field name</span></span>     | <span data-ttu-id="06e6b-157">Units</span><span class="sxs-lookup"><span data-stu-id="06e6b-157">Units</span></span>  | <span data-ttu-id="06e6b-158">Minimum</span><span class="sxs-lookup"><span data-stu-id="06e6b-158">Minimum</span></span> | <span data-ttu-id="06e6b-159">Maximum</span><span class="sxs-lookup"><span data-stu-id="06e6b-159">Maximum</span></span> | <span data-ttu-id="06e6b-160">Decimal places</span><span class="sxs-lookup"><span data-stu-id="06e6b-160">Decimal places</span></span> |
| -------------- | ------ | ------- | ------- | -------------- |
| <span data-ttu-id="06e6b-161">humidity</span><span class="sxs-lookup"><span data-stu-id="06e6b-161">humidity</span></span>       | %      | <span data-ttu-id="06e6b-162">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-162">0</span></span>       | <span data-ttu-id="06e6b-163">100</span><span class="sxs-lookup"><span data-stu-id="06e6b-163">100</span></span>     | <span data-ttu-id="06e6b-164">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-164">0</span></span>              |
| <span data-ttu-id="06e6b-165">temp</span><span class="sxs-lookup"><span data-stu-id="06e6b-165">temp</span></span>           | <span data-ttu-id="06e6b-166">°C</span><span class="sxs-lookup"><span data-stu-id="06e6b-166">°C</span></span>     | <span data-ttu-id="06e6b-167">-40</span><span class="sxs-lookup"><span data-stu-id="06e6b-167">-40</span></span>     | <span data-ttu-id="06e6b-168">120</span><span class="sxs-lookup"><span data-stu-id="06e6b-168">120</span></span>     | <span data-ttu-id="06e6b-169">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-169">0</span></span>              |
| <span data-ttu-id="06e6b-170">pressure</span><span class="sxs-lookup"><span data-stu-id="06e6b-170">pressure</span></span>       | <span data-ttu-id="06e6b-171">hPa</span><span class="sxs-lookup"><span data-stu-id="06e6b-171">hPa</span></span>    | <span data-ttu-id="06e6b-172">260</span><span class="sxs-lookup"><span data-stu-id="06e6b-172">260</span></span>     | <span data-ttu-id="06e6b-173">1260</span><span class="sxs-lookup"><span data-stu-id="06e6b-173">1260</span></span>    | <span data-ttu-id="06e6b-174">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-174">0</span></span>              |

### <a name="settings"></a><span data-ttu-id="06e6b-175">Settings</span><span class="sxs-lookup"><span data-stu-id="06e6b-175">Settings</span></span>

<span data-ttu-id="06e6b-176">Numeric settings</span><span class="sxs-lookup"><span data-stu-id="06e6b-176">Numeric settings</span></span>

| <span data-ttu-id="06e6b-177">Display name</span><span class="sxs-lookup"><span data-stu-id="06e6b-177">Display name</span></span> | <span data-ttu-id="06e6b-178">Field name</span><span class="sxs-lookup"><span data-stu-id="06e6b-178">Field name</span></span> | <span data-ttu-id="06e6b-179">Units</span><span class="sxs-lookup"><span data-stu-id="06e6b-179">Units</span></span> | <span data-ttu-id="06e6b-180">Decimal places</span><span class="sxs-lookup"><span data-stu-id="06e6b-180">Decimal places</span></span> | <span data-ttu-id="06e6b-181">Minimum</span><span class="sxs-lookup"><span data-stu-id="06e6b-181">Minimum</span></span> | <span data-ttu-id="06e6b-182">Maximum</span><span class="sxs-lookup"><span data-stu-id="06e6b-182">Maximum</span></span> | <span data-ttu-id="06e6b-183">Initial</span><span class="sxs-lookup"><span data-stu-id="06e6b-183">Initial</span></span> |
| ------------ | ---------- | ----- | -------------- | ------- | ------- | ------- |
| <span data-ttu-id="06e6b-184">Fan Speed</span><span class="sxs-lookup"><span data-stu-id="06e6b-184">Fan Speed</span></span>    | <span data-ttu-id="06e6b-185">fanSpeed</span><span class="sxs-lookup"><span data-stu-id="06e6b-185">fanSpeed</span></span>   | <span data-ttu-id="06e6b-186">RPM</span><span class="sxs-lookup"><span data-stu-id="06e6b-186">RPM</span></span>   | <span data-ttu-id="06e6b-187">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-187">0</span></span>              | <span data-ttu-id="06e6b-188">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-188">0</span></span>       | <span data-ttu-id="06e6b-189">1000</span><span class="sxs-lookup"><span data-stu-id="06e6b-189">1000</span></span>    | <span data-ttu-id="06e6b-190">0</span><span class="sxs-lookup"><span data-stu-id="06e6b-190">0</span></span>       |


### <a name="properties"></a><span data-ttu-id="06e6b-191">Properties</span><span class="sxs-lookup"><span data-stu-id="06e6b-191">Properties</span></span>

| <span data-ttu-id="06e6b-192">Type</span><span class="sxs-lookup"><span data-stu-id="06e6b-192">Type</span></span>            | <span data-ttu-id="06e6b-193">Display name</span><span class="sxs-lookup"><span data-stu-id="06e6b-193">Display name</span></span> | <span data-ttu-id="06e6b-194">Field name</span><span class="sxs-lookup"><span data-stu-id="06e6b-194">Field name</span></span> | <span data-ttu-id="06e6b-195">Data type</span><span class="sxs-lookup"><span data-stu-id="06e6b-195">Data type</span></span> |
| --------------- | ------------ | ---------- | --------- |
| <span data-ttu-id="06e6b-196">Device property</span><span class="sxs-lookup"><span data-stu-id="06e6b-196">Device property</span></span> | <span data-ttu-id="06e6b-197">Die number</span><span class="sxs-lookup"><span data-stu-id="06e6b-197">Die number</span></span>   | <span data-ttu-id="06e6b-198">dieNumber</span><span class="sxs-lookup"><span data-stu-id="06e6b-198">dieNumber</span></span>  | <span data-ttu-id="06e6b-199">number</span><span class="sxs-lookup"><span data-stu-id="06e6b-199">number</span></span>    |
| <span data-ttu-id="06e6b-200">Text</span><span class="sxs-lookup"><span data-stu-id="06e6b-200">Text</span></span>            | <span data-ttu-id="06e6b-201">Location</span><span class="sxs-lookup"><span data-stu-id="06e6b-201">Location</span></span>     | <span data-ttu-id="06e6b-202">location</span><span class="sxs-lookup"><span data-stu-id="06e6b-202">location</span></span>   | <span data-ttu-id="06e6b-203">N/A</span><span class="sxs-lookup"><span data-stu-id="06e6b-203">N/A</span></span>       |
