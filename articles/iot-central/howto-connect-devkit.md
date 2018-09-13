---
title: Connect a DevKit device to your Azure IoT Central application | Microsoft Docs
description: As a device developer, learn how to connect an MXChip IoT DevKit device to your Azure IoT Central application.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: ea9ff8f93ede3b9ec5e7eed83c6049b0c23de7e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870200"
---
# <a name="connect-an-mxchip-iot-devkit-device-to-your-azure-iot-central-application"></a><span data-ttu-id="b6cea-103">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="b6cea-103">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span></span>

<span data-ttu-id="b6cea-104">This article describes how, as a device developer, to connect a MXChip IoT DevKit (DevKit) device to your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="b6cea-104">This article describes how, as a device developer, to connect a MXChip IoT DevKit (DevKit) device to your Microsoft Azure IoT Central application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6cea-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b6cea-105">Before you begin</span></span>

<span data-ttu-id="b6cea-106">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="b6cea-106">To complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="b6cea-107">An Azure IoT Central application created from the **Sample Devkits** application template.</span><span class="sxs-lookup"><span data-stu-id="b6cea-107">An Azure IoT Central application created from the **Sample Devkits** application template.</span></span> <span data-ttu-id="b6cea-108">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="b6cea-108">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span></span>
1. <span data-ttu-id="b6cea-109">A DevKit device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-109">A DevKit device.</span></span> <span data-ttu-id="b6cea-110">To purchase a DevKit device, visit [MXChip IoT DevKit](http://mxchip.com/az3166).</span><span class="sxs-lookup"><span data-stu-id="b6cea-110">To purchase a DevKit device, visit [MXChip IoT DevKit](http://mxchip.com/az3166).</span></span>


## <a name="sample-devkits-application"></a><span data-ttu-id="b6cea-111">**Sample Devkits** application</span><span class="sxs-lookup"><span data-stu-id="b6cea-111">**Sample Devkits** application</span></span>

<span data-ttu-id="b6cea-112">An application created from the **Sample Devkits** application template includes a **MXChip** device template with the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="b6cea-112">An application created from the **Sample Devkits** application template includes a **MXChip** device template with the following characteristics:</span></span> 

- <span data-ttu-id="b6cea-113">Telemetry which contains the measurements for the device **Humidity**, **Temperature**, **Pressure**, **Magnometer** (measured along X, Y, Z axis), **Accelorometer** (measured along X, Y, Z axis) and **Gyroscope** (measured along X, Y, Z axis).</span><span class="sxs-lookup"><span data-stu-id="b6cea-113">Telemetry which contains the measurements for the device **Humidity**, **Temperature**, **Pressure**, **Magnometer** (measured along X, Y, Z axis), **Accelorometer** (measured along X, Y, Z axis) and **Gyroscope** (measured along X, Y, Z axis).</span></span>
- <span data-ttu-id="b6cea-114">State which contains an example measurement for **Device State**.</span><span class="sxs-lookup"><span data-stu-id="b6cea-114">State which contains an example measurement for **Device State**.</span></span>
- <span data-ttu-id="b6cea-115">Event measurement with a **Button B Pressed** event.</span><span class="sxs-lookup"><span data-stu-id="b6cea-115">Event measurement with a **Button B Pressed** event.</span></span> 
- <span data-ttu-id="b6cea-116">Settings showing **Voltage**, **Current**, **Fan Speed**, and an **IR** toggle.</span><span class="sxs-lookup"><span data-stu-id="b6cea-116">Settings showing **Voltage**, **Current**, **Fan Speed**, and an **IR** toggle.</span></span>
- <span data-ttu-id="b6cea-117">Properties containing device property **die number** and **Device Location** which is a location property as well as in a **Manufactured In** cloud property.</span><span class="sxs-lookup"><span data-stu-id="b6cea-117">Properties containing device property **die number** and **Device Location** which is a location property as well as in a **Manufactured In** cloud property.</span></span> 


<span data-ttu-id="b6cea-118">For full details on the configuration refer to [MXChip Device template details](howto-connect-devkit.md#mxchip-device-template-details)</span><span class="sxs-lookup"><span data-stu-id="b6cea-118">For full details on the configuration refer to [MXChip Device template details](howto-connect-devkit.md#mxchip-device-template-details)</span></span>


## <a name="add-a-real-device"></a><span data-ttu-id="b6cea-119">Add a real device</span><span class="sxs-lookup"><span data-stu-id="b6cea-119">Add a real device</span></span>

<span data-ttu-id="b6cea-120">In your Azure IoT Central application, add a real device from the **MXChip** device template and make a note of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="b6cea-120">In your Azure IoT Central application, add a real device from the **MXChip** device template and make a note of the device connection string.</span></span> <span data-ttu-id="b6cea-121">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span><span class="sxs-lookup"><span data-stu-id="b6cea-121">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span></span>

### <a name="prepare-the-devkit-device"></a><span data-ttu-id="b6cea-122">Prepare the DevKit device</span><span class="sxs-lookup"><span data-stu-id="b6cea-122">Prepare the DevKit device</span></span>

> [!NOTE]
> <span data-ttu-id="b6cea-123">If you have previously used the device and have wifi credentials stored and would like to reconfigure the device to use a different WiFi network, connection string, or telemetry measurement, press both the **A** and **B** buttons on the board simultaneously.</span><span class="sxs-lookup"><span data-stu-id="b6cea-123">If you have previously used the device and have wifi credentials stored and would like to reconfigure the device to use a different WiFi network, connection string, or telemetry measurement, press both the **A** and **B** buttons on the board simultaneously.</span></span> <span data-ttu-id="b6cea-124">If it doesn't work, press **reset** button and try again.</span><span class="sxs-lookup"><span data-stu-id="b6cea-124">If it doesn't work, press **reset** button and try again.</span></span>

#### <a name="before-you-start-configuring-the-device"></a><span data-ttu-id="b6cea-125">Before you start configuring the device:</span><span class="sxs-lookup"><span data-stu-id="b6cea-125">Before you start configuring the device:</span></span>
1. <span data-ttu-id="b6cea-126">In your IoT Central **Sample Devkits** go to `Device Explorer`-> `select MXChip Template` -> `Click on +New and choose **Real** Device` -> `Connect this device` (on the top right)</span><span class="sxs-lookup"><span data-stu-id="b6cea-126">In your IoT Central **Sample Devkits** go to `Device Explorer`-> `select MXChip Template` -> `Click on +New and choose **Real** Device` -> `Connect this device` (on the top right)</span></span> 
2. <span data-ttu-id="b6cea-127">Copy the primary connection string</span><span class="sxs-lookup"><span data-stu-id="b6cea-127">Copy the primary connection string</span></span>
3. <span data-ttu-id="b6cea-128">Make sure to save the connection string, as you will temporaritly get disconnected from the internet as you prepare the DevKit device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-128">Make sure to save the connection string, as you will temporaritly get disconnected from the internet as you prepare the DevKit device.</span></span> 


#### <a name="to-prepare-the-devkit-device"></a><span data-ttu-id="b6cea-129">To prepare the DevKit device:</span><span class="sxs-lookup"><span data-stu-id="b6cea-129">To prepare the DevKit device:</span></span>


1. <span data-ttu-id="b6cea-130">Download the latest pre-built Azure IoT Central firmware for the MXChip from the [releases](https://github.com/Azure/iot-central-firmware/releases) page on GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6cea-130">Download the latest pre-built Azure IoT Central firmware for the MXChip from the [releases](https://github.com/Azure/iot-central-firmware/releases) page on GitHub.</span></span> <span data-ttu-id="b6cea-131">The download filename on the releases page looks like `AZ3166-IoT-Central-X.X.X.bin`.</span><span class="sxs-lookup"><span data-stu-id="b6cea-131">The download filename on the releases page looks like `AZ3166-IoT-Central-X.X.X.bin`.</span></span>

1. <span data-ttu-id="b6cea-132">Connect the DevKit device to your development machine using a USB cable.</span><span class="sxs-lookup"><span data-stu-id="b6cea-132">Connect the DevKit device to your development machine using a USB cable.</span></span> <span data-ttu-id="b6cea-133">In Windows, a file explorer window opens on a drive mapped to the storage on the DevKit device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-133">In Windows, a file explorer window opens on a drive mapped to the storage on the DevKit device.</span></span> <span data-ttu-id="b6cea-134">For example, the drive might be called **AZ3166 (D:)**.</span><span class="sxs-lookup"><span data-stu-id="b6cea-134">For example, the drive might be called **AZ3166 (D:)**.</span></span>

1. <span data-ttu-id="b6cea-135">Drag the **iotCentral.bin** file onto the drive window.</span><span class="sxs-lookup"><span data-stu-id="b6cea-135">Drag the **iotCentral.bin** file onto the drive window.</span></span> <span data-ttu-id="b6cea-136">When the copying is complete, the device reboots with the new firmware.</span><span class="sxs-lookup"><span data-stu-id="b6cea-136">When the copying is complete, the device reboots with the new firmware.</span></span>

1. <span data-ttu-id="b6cea-137">When the DevKit device restarts, the following screen displays:</span><span class="sxs-lookup"><span data-stu-id="b6cea-137">When the DevKit device restarts, the following screen displays:</span></span>

    ```
    Connect HotSpot:
    AZ3166_??????
    go-> 192.168.0.1 
    PIN CODE xxxxx
    ```

    > [!NOTE]
    > <span data-ttu-id="b6cea-138">If the screen displays anything else, press the **A**  and **B** buttons on the device at the same time to reboot the device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-138">If the screen displays anything else, press the **A**  and **B** buttons on the device at the same time to reboot the device.</span></span> 

1. <span data-ttu-id="b6cea-139">The device is now in access point (AP) mode.</span><span class="sxs-lookup"><span data-stu-id="b6cea-139">The device is now in access point (AP) mode.</span></span> <span data-ttu-id="b6cea-140">You can connect to this WiFi access point from your computer or mobile device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-140">You can connect to this WiFi access point from your computer or mobile device.</span></span>

1. <span data-ttu-id="b6cea-141">On your computer, phone, or tablet connect to the WiFi network name shown on the screen of the device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-141">On your computer, phone, or tablet connect to the WiFi network name shown on the screen of the device.</span></span> <span data-ttu-id="b6cea-142">When you connect to this network, you do not have internet access.</span><span class="sxs-lookup"><span data-stu-id="b6cea-142">When you connect to this network, you do not have internet access.</span></span> <span data-ttu-id="b6cea-143">This state is expected, and you are only connected to this network for a short time while you configure the device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-143">This state is expected, and you are only connected to this network for a short time while you configure the device.</span></span>

1. <span data-ttu-id="b6cea-144">Open your web browser and navigate to [http://192.168.0.1/start](http://192.168.0.1/start).</span><span class="sxs-lookup"><span data-stu-id="b6cea-144">Open your web browser and navigate to [http://192.168.0.1/start](http://192.168.0.1/start).</span></span> <span data-ttu-id="b6cea-145">The following web page displays:</span><span class="sxs-lookup"><span data-stu-id="b6cea-145">The following web page displays:</span></span>

    ![Device configuration page](media/howto-connect-devkit/configpage.png)

    <span data-ttu-id="b6cea-147">In the web page:</span><span class="sxs-lookup"><span data-stu-id="b6cea-147">In the web page:</span></span> 
    - <span data-ttu-id="b6cea-148">add the name of your WiFi network</span><span class="sxs-lookup"><span data-stu-id="b6cea-148">add the name of your WiFi network</span></span> 
    - <span data-ttu-id="b6cea-149">your WiFi network password</span><span class="sxs-lookup"><span data-stu-id="b6cea-149">your WiFi network password</span></span>
    - <span data-ttu-id="b6cea-150">PIN CODE shown on the device LCD</span><span class="sxs-lookup"><span data-stu-id="b6cea-150">PIN CODE shown on the device LCD</span></span> 
    - <span data-ttu-id="b6cea-151">the connection string of your device (you should have already saved this following the steps) You can find the connection string at `https://apps.iotcentral.com` -> `Device Explorer` -> `Device` -> `Select or Create a new Real Device` -> `Connect this device` (on the top right)</span><span class="sxs-lookup"><span data-stu-id="b6cea-151">the connection string of your device (you should have already saved this following the steps) You can find the connection string at `https://apps.iotcentral.com` -> `Device Explorer` -> `Device` -> `Select or Create a new Real Device` -> `Connect this device` (on the top right)</span></span>
    - <span data-ttu-id="b6cea-152">Select all the available telemetry measurements!</span><span class="sxs-lookup"><span data-stu-id="b6cea-152">Select all the available telemetry measurements!</span></span> 

1. <span data-ttu-id="b6cea-153">After you choose **Configure Device**, you see this page:</span><span class="sxs-lookup"><span data-stu-id="b6cea-153">After you choose **Configure Device**, you see this page:</span></span>

    ![Device configured](media/howto-connect-devkit/deviceconfigured.png)

1. <span data-ttu-id="b6cea-155">Press the **Reset** button on your device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-155">Press the **Reset** button on your device.</span></span>



## <a name="view-the-telemetry"></a><span data-ttu-id="b6cea-156">View the telemetry</span><span class="sxs-lookup"><span data-stu-id="b6cea-156">View the telemetry</span></span>

<span data-ttu-id="b6cea-157">When the DevKit device restarts, the screen on the device shows:</span><span class="sxs-lookup"><span data-stu-id="b6cea-157">When the DevKit device restarts, the screen on the device shows:</span></span>

* <span data-ttu-id="b6cea-158">The number of telemetry messages sent.</span><span class="sxs-lookup"><span data-stu-id="b6cea-158">The number of telemetry messages sent.</span></span>
* <span data-ttu-id="b6cea-159">The number of failures.</span><span class="sxs-lookup"><span data-stu-id="b6cea-159">The number of failures.</span></span>
* <span data-ttu-id="b6cea-160">The number of desired properties received and the number of reported properties sent.</span><span class="sxs-lookup"><span data-stu-id="b6cea-160">The number of desired properties received and the number of reported properties sent.</span></span>

<span data-ttu-id="b6cea-161">Shake the device increment the number of reported properties sent.</span><span class="sxs-lookup"><span data-stu-id="b6cea-161">Shake the device increment the number of reported properties sent.</span></span> <span data-ttu-id="b6cea-162">The device sends a random number as the **Die number** device property.</span><span class="sxs-lookup"><span data-stu-id="b6cea-162">The device sends a random number as the **Die number** device property.</span></span>

<span data-ttu-id="b6cea-163">You can view the telemetry measurements and reported property values, and configure settings in Azure IoT Central:</span><span class="sxs-lookup"><span data-stu-id="b6cea-163">You can view the telemetry measurements and reported property values, and configure settings in Azure IoT Central:</span></span>

1. <span data-ttu-id="b6cea-164">Use **Device Explorer** to navigate to the **Measurements** page for the real MXChip device you added:</span><span class="sxs-lookup"><span data-stu-id="b6cea-164">Use **Device Explorer** to navigate to the **Measurements** page for the real MXChip device you added:</span></span>

    ![Navigate to real device](media/howto-connect-devkit/realdevicenew.png)

1. <span data-ttu-id="b6cea-166">On the **Measurements** page, you can see the telemetry coming from the MXChip device:</span><span class="sxs-lookup"><span data-stu-id="b6cea-166">On the **Measurements** page, you can see the telemetry coming from the MXChip device:</span></span>

    ![View telemetry from real device](media/howto-connect-devkit/devicetelemetrynew.png)

1. <span data-ttu-id="b6cea-168">On the **Properties** page, you can view the last die number and the device location reported by the device:</span><span class="sxs-lookup"><span data-stu-id="b6cea-168">On the **Properties** page, you can view the last die number and the device location reported by the device:</span></span>

    ![View device properties](media/howto-connect-devkit/devicepropertynew.png)

1. <span data-ttu-id="b6cea-170">On the **Settings** page, you can update the settings on the MXChip device:</span><span class="sxs-lookup"><span data-stu-id="b6cea-170">On the **Settings** page, you can update the settings on the MXChip device:</span></span>

    ![View device settings](media/howto-connect-devkit/devicesettingsnew.png)

1. <span data-ttu-id="b6cea-172">On the **Dashboard** page, you can see the location map</span><span class="sxs-lookup"><span data-stu-id="b6cea-172">On the **Dashboard** page, you can see the location map</span></span>

    ![View device dashboard](media/howto-connect-devkit/devicedashboardnew.png)


## <a name="download-the-source-code"></a><span data-ttu-id="b6cea-174">Download the source code</span><span class="sxs-lookup"><span data-stu-id="b6cea-174">Download the source code</span></span>

<span data-ttu-id="b6cea-175">If you want to explore and modify the device code, you can download it from GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6cea-175">If you want to explore and modify the device code, you can download it from GitHub.</span></span> <span data-ttu-id="b6cea-176">If you plan to modify the code, you should follow these instructions to [prepare the development environment](https://microsoft.github.io/azure-iot-developer-kit/docs/get-started/#step-5-prepare-the-development-environment) for your desktop operating system.</span><span class="sxs-lookup"><span data-stu-id="b6cea-176">If you plan to modify the code, you should follow these instructions to [prepare the development environment](https://microsoft.github.io/azure-iot-developer-kit/docs/get-started/#step-5-prepare-the-development-environment) for your desktop operating system.</span></span>

<span data-ttu-id="b6cea-177">To download the source code, run the following command on your desktop machine:</span><span class="sxs-lookup"><span data-stu-id="b6cea-177">To download the source code, run the following command on your desktop machine:</span></span>

```cmd/sh
git clone https://github.com/Azure/iot-central-firmware
```

<span data-ttu-id="b6cea-178">The previous command downloads the source code to a folder called `iot-central-firmware`.</span><span class="sxs-lookup"><span data-stu-id="b6cea-178">The previous command downloads the source code to a folder called `iot-central-firmware`.</span></span> 

> [!NOTE]
> <span data-ttu-id="b6cea-179">If **git** is not installed in your development environment, you can download it from [https://git-scm.com/download](https://git-scm.com/download).</span><span class="sxs-lookup"><span data-stu-id="b6cea-179">If **git** is not installed in your development environment, you can download it from [https://git-scm.com/download](https://git-scm.com/download).</span></span>

## <a name="review-the-code"></a><span data-ttu-id="b6cea-180">Review the code</span><span class="sxs-lookup"><span data-stu-id="b6cea-180">Review the code</span></span>

<span data-ttu-id="b6cea-181">Use Visual Studio Code, which was installed when you prepared your development environment, to open the `AZ3166` folder in the `iot-central-firmware` folder:</span><span class="sxs-lookup"><span data-stu-id="b6cea-181">Use Visual Studio Code, which was installed when you prepared your development environment, to open the `AZ3166` folder in the `iot-central-firmware` folder:</span></span> 

![Visual Studio Code](media/howto-connect-devkit/vscodeview.png)

<span data-ttu-id="b6cea-183">To see how the telemetry is sent to the Azure IoT Central application, open the **main_telemetry.cpp** file in the source folder.</span><span class="sxs-lookup"><span data-stu-id="b6cea-183">To see how the telemetry is sent to the Azure IoT Central application, open the **main_telemetry.cpp** file in the source folder.</span></span>

<span data-ttu-id="b6cea-184">The function `buildTelemetryPayload` creates the JSON telemetry payload using data from the sensors on the device.</span><span class="sxs-lookup"><span data-stu-id="b6cea-184">The function `buildTelemetryPayload` creates the JSON telemetry payload using data from the sensors on the device.</span></span>

<span data-ttu-id="b6cea-185">The function `sendTelemetryPayload` calls `sendTelemetry` in the **iotHubClient.cpp** to send the JSON payload to the IoT Hub your Azure IoT Central application uses.</span><span class="sxs-lookup"><span data-stu-id="b6cea-185">The function `sendTelemetryPayload` calls `sendTelemetry` in the **iotHubClient.cpp** to send the JSON payload to the IoT Hub your Azure IoT Central application uses.</span></span>

<span data-ttu-id="b6cea-186">To see how property values are reported to the Azure IoT Central application, open the **main_telemetry.cpp** file in the source folder.</span><span class="sxs-lookup"><span data-stu-id="b6cea-186">To see how property values are reported to the Azure IoT Central application, open the **main_telemetry.cpp** file in the source folder.</span></span>

<span data-ttu-id="b6cea-187">The function `telemetryLoop` sends the **doubleTap** reported property when the accelerometer detects a double tap.</span><span class="sxs-lookup"><span data-stu-id="b6cea-187">The function `telemetryLoop` sends the **doubleTap** reported property when the accelerometer detects a double tap.</span></span> <span data-ttu-id="b6cea-188">It uses the `sendReportedProperty` function in the **iotHubClient.cpp** source file.</span><span class="sxs-lookup"><span data-stu-id="b6cea-188">It uses the `sendReportedProperty` function in the **iotHubClient.cpp** source file.</span></span>

<span data-ttu-id="b6cea-189">The code in the **iotHubClient.cpp** source file uses functions from the [ Microsoft Azure IoT SDKs and libraries for C](https://github.com/Azure/azure-iot-sdk-c) to interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b6cea-189">The code in the **iotHubClient.cpp** source file uses functions from the [ Microsoft Azure IoT SDKs and libraries for C](https://github.com/Azure/azure-iot-sdk-c) to interact with IoT Hub.</span></span>

<span data-ttu-id="b6cea-190">For information about how to modify, build, and upload the sample code to your device, see the **readme.md** file in the `AZ3166` folder.</span><span class="sxs-lookup"><span data-stu-id="b6cea-190">For information about how to modify, build, and upload the sample code to your device, see the **readme.md** file in the `AZ3166` folder.</span></span>

## <a name="mxchip-device-template-details"></a><span data-ttu-id="b6cea-191">MXChip Device template details</span><span class="sxs-lookup"><span data-stu-id="b6cea-191">MXChip Device template details</span></span> 

<span data-ttu-id="b6cea-192">An application created from the Sample Devkits application template includes a MXChip device template with the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="b6cea-192">An application created from the Sample Devkits application template includes a MXChip device template with the following characteristics:</span></span>

### <a name="measurements"></a><span data-ttu-id="b6cea-193">Measurements</span><span class="sxs-lookup"><span data-stu-id="b6cea-193">Measurements</span></span>

#### <a name="telemetry"></a><span data-ttu-id="b6cea-194">Telemetry</span><span class="sxs-lookup"><span data-stu-id="b6cea-194">Telemetry</span></span> 

| <span data-ttu-id="b6cea-195">Field name</span><span class="sxs-lookup"><span data-stu-id="b6cea-195">Field name</span></span>     | <span data-ttu-id="b6cea-196">Units</span><span class="sxs-lookup"><span data-stu-id="b6cea-196">Units</span></span>  | <span data-ttu-id="b6cea-197">Minimum</span><span class="sxs-lookup"><span data-stu-id="b6cea-197">Minimum</span></span> | <span data-ttu-id="b6cea-198">Maximum</span><span class="sxs-lookup"><span data-stu-id="b6cea-198">Maximum</span></span> | <span data-ttu-id="b6cea-199">Decimal places</span><span class="sxs-lookup"><span data-stu-id="b6cea-199">Decimal places</span></span> |
| -------------- | ------ | ------- | ------- | -------------- |
| <span data-ttu-id="b6cea-200">humidity</span><span class="sxs-lookup"><span data-stu-id="b6cea-200">humidity</span></span>       | %      | <span data-ttu-id="b6cea-201">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-201">0</span></span>       | <span data-ttu-id="b6cea-202">100</span><span class="sxs-lookup"><span data-stu-id="b6cea-202">100</span></span>     | <span data-ttu-id="b6cea-203">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-203">0</span></span>              |
| <span data-ttu-id="b6cea-204">temp</span><span class="sxs-lookup"><span data-stu-id="b6cea-204">temp</span></span>           | <span data-ttu-id="b6cea-205">°C</span><span class="sxs-lookup"><span data-stu-id="b6cea-205">°C</span></span>     | <span data-ttu-id="b6cea-206">-40</span><span class="sxs-lookup"><span data-stu-id="b6cea-206">-40</span></span>     | <span data-ttu-id="b6cea-207">120</span><span class="sxs-lookup"><span data-stu-id="b6cea-207">120</span></span>     | <span data-ttu-id="b6cea-208">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-208">0</span></span>              |
| <span data-ttu-id="b6cea-209">pressure</span><span class="sxs-lookup"><span data-stu-id="b6cea-209">pressure</span></span>       | <span data-ttu-id="b6cea-210">hPa</span><span class="sxs-lookup"><span data-stu-id="b6cea-210">hPa</span></span>    | <span data-ttu-id="b6cea-211">260</span><span class="sxs-lookup"><span data-stu-id="b6cea-211">260</span></span>     | <span data-ttu-id="b6cea-212">1260</span><span class="sxs-lookup"><span data-stu-id="b6cea-212">1260</span></span>    | <span data-ttu-id="b6cea-213">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-213">0</span></span>              |
| <span data-ttu-id="b6cea-214">magnetometerX</span><span class="sxs-lookup"><span data-stu-id="b6cea-214">magnetometerX</span></span>  | <span data-ttu-id="b6cea-215">mgauss</span><span class="sxs-lookup"><span data-stu-id="b6cea-215">mgauss</span></span> | <span data-ttu-id="b6cea-216">-1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-216">-1000</span></span>   | <span data-ttu-id="b6cea-217">1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-217">1000</span></span>    | <span data-ttu-id="b6cea-218">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-218">0</span></span>              |
| <span data-ttu-id="b6cea-219">magnetometerY</span><span class="sxs-lookup"><span data-stu-id="b6cea-219">magnetometerY</span></span>  | <span data-ttu-id="b6cea-220">mgauss</span><span class="sxs-lookup"><span data-stu-id="b6cea-220">mgauss</span></span> | <span data-ttu-id="b6cea-221">-1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-221">-1000</span></span>   | <span data-ttu-id="b6cea-222">1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-222">1000</span></span>    | <span data-ttu-id="b6cea-223">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-223">0</span></span>              |
| <span data-ttu-id="b6cea-224">magnetometerZ</span><span class="sxs-lookup"><span data-stu-id="b6cea-224">magnetometerZ</span></span>  | <span data-ttu-id="b6cea-225">mgauss</span><span class="sxs-lookup"><span data-stu-id="b6cea-225">mgauss</span></span> | <span data-ttu-id="b6cea-226">-1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-226">-1000</span></span>   | <span data-ttu-id="b6cea-227">1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-227">1000</span></span>    | <span data-ttu-id="b6cea-228">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-228">0</span></span>              |
| <span data-ttu-id="b6cea-229">accelerometerX</span><span class="sxs-lookup"><span data-stu-id="b6cea-229">accelerometerX</span></span> | <span data-ttu-id="b6cea-230">mg</span><span class="sxs-lookup"><span data-stu-id="b6cea-230">mg</span></span>     | <span data-ttu-id="b6cea-231">-2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-231">-2000</span></span>   | <span data-ttu-id="b6cea-232">2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-232">2000</span></span>    | <span data-ttu-id="b6cea-233">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-233">0</span></span>              |
| <span data-ttu-id="b6cea-234">accelerometerY</span><span class="sxs-lookup"><span data-stu-id="b6cea-234">accelerometerY</span></span> | <span data-ttu-id="b6cea-235">mg</span><span class="sxs-lookup"><span data-stu-id="b6cea-235">mg</span></span>     | <span data-ttu-id="b6cea-236">-2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-236">-2000</span></span>   | <span data-ttu-id="b6cea-237">2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-237">2000</span></span>    | <span data-ttu-id="b6cea-238">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-238">0</span></span>              |
| <span data-ttu-id="b6cea-239">accelerometerZ</span><span class="sxs-lookup"><span data-stu-id="b6cea-239">accelerometerZ</span></span> | <span data-ttu-id="b6cea-240">mg</span><span class="sxs-lookup"><span data-stu-id="b6cea-240">mg</span></span>     | <span data-ttu-id="b6cea-241">-2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-241">-2000</span></span>   | <span data-ttu-id="b6cea-242">2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-242">2000</span></span>    | <span data-ttu-id="b6cea-243">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-243">0</span></span>              |
| <span data-ttu-id="b6cea-244">gyroscopeX</span><span class="sxs-lookup"><span data-stu-id="b6cea-244">gyroscopeX</span></span>     | <span data-ttu-id="b6cea-245">mdps</span><span class="sxs-lookup"><span data-stu-id="b6cea-245">mdps</span></span>   | <span data-ttu-id="b6cea-246">-2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-246">-2000</span></span>   | <span data-ttu-id="b6cea-247">2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-247">2000</span></span>    | <span data-ttu-id="b6cea-248">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-248">0</span></span>              |
| <span data-ttu-id="b6cea-249">gyroscopeY</span><span class="sxs-lookup"><span data-stu-id="b6cea-249">gyroscopeY</span></span>     | <span data-ttu-id="b6cea-250">mdps</span><span class="sxs-lookup"><span data-stu-id="b6cea-250">mdps</span></span>   | <span data-ttu-id="b6cea-251">-2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-251">-2000</span></span>   | <span data-ttu-id="b6cea-252">2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-252">2000</span></span>    | <span data-ttu-id="b6cea-253">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-253">0</span></span>              |
| <span data-ttu-id="b6cea-254">gyroscopeZ</span><span class="sxs-lookup"><span data-stu-id="b6cea-254">gyroscopeZ</span></span>     | <span data-ttu-id="b6cea-255">mdps</span><span class="sxs-lookup"><span data-stu-id="b6cea-255">mdps</span></span>   | <span data-ttu-id="b6cea-256">-2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-256">-2000</span></span>   | <span data-ttu-id="b6cea-257">2000</span><span class="sxs-lookup"><span data-stu-id="b6cea-257">2000</span></span>    | <span data-ttu-id="b6cea-258">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-258">0</span></span>              |


#### <a name="states"></a><span data-ttu-id="b6cea-259">States</span><span class="sxs-lookup"><span data-stu-id="b6cea-259">States</span></span> 
| <span data-ttu-id="b6cea-260">Name</span><span class="sxs-lookup"><span data-stu-id="b6cea-260">Name</span></span>          | <span data-ttu-id="b6cea-261">Display name</span><span class="sxs-lookup"><span data-stu-id="b6cea-261">Display name</span></span>   | <span data-ttu-id="b6cea-262">NORMAL</span><span class="sxs-lookup"><span data-stu-id="b6cea-262">NORMAL</span></span> | <span data-ttu-id="b6cea-263">CAUTION</span><span class="sxs-lookup"><span data-stu-id="b6cea-263">CAUTION</span></span> | <span data-ttu-id="b6cea-264">DANGER</span><span class="sxs-lookup"><span data-stu-id="b6cea-264">DANGER</span></span> | 
| ------------- | -------------- | ------ | ------- | ------ | 
| <span data-ttu-id="b6cea-265">DeviceState</span><span class="sxs-lookup"><span data-stu-id="b6cea-265">DeviceState</span></span>   | <span data-ttu-id="b6cea-266">Device State</span><span class="sxs-lookup"><span data-stu-id="b6cea-266">Device State</span></span>   | <span data-ttu-id="b6cea-267">Green</span><span class="sxs-lookup"><span data-stu-id="b6cea-267">Green</span></span>  | <span data-ttu-id="b6cea-268">Orange</span><span class="sxs-lookup"><span data-stu-id="b6cea-268">Orange</span></span>  | <span data-ttu-id="b6cea-269">Red</span><span class="sxs-lookup"><span data-stu-id="b6cea-269">Red</span></span>    | 

#### <a name="events"></a><span data-ttu-id="b6cea-270">Events</span><span class="sxs-lookup"><span data-stu-id="b6cea-270">Events</span></span> 
| <span data-ttu-id="b6cea-271">Name</span><span class="sxs-lookup"><span data-stu-id="b6cea-271">Name</span></span>             | <span data-ttu-id="b6cea-272">Display name</span><span class="sxs-lookup"><span data-stu-id="b6cea-272">Display name</span></span>      | 
| ---------------- | ----------------- | 
| <span data-ttu-id="b6cea-273">ButtonBPressed</span><span class="sxs-lookup"><span data-stu-id="b6cea-273">ButtonBPressed</span></span>   | <span data-ttu-id="b6cea-274">Button B Pressed</span><span class="sxs-lookup"><span data-stu-id="b6cea-274">Button B Pressed</span></span>  | 

### <a name="settings"></a><span data-ttu-id="b6cea-275">Settings</span><span class="sxs-lookup"><span data-stu-id="b6cea-275">Settings</span></span>

<span data-ttu-id="b6cea-276">Numeric settings</span><span class="sxs-lookup"><span data-stu-id="b6cea-276">Numeric settings</span></span>

| <span data-ttu-id="b6cea-277">Display name</span><span class="sxs-lookup"><span data-stu-id="b6cea-277">Display name</span></span> | <span data-ttu-id="b6cea-278">Field name</span><span class="sxs-lookup"><span data-stu-id="b6cea-278">Field name</span></span> | <span data-ttu-id="b6cea-279">Units</span><span class="sxs-lookup"><span data-stu-id="b6cea-279">Units</span></span> | <span data-ttu-id="b6cea-280">Decimal places</span><span class="sxs-lookup"><span data-stu-id="b6cea-280">Decimal places</span></span> | <span data-ttu-id="b6cea-281">Minimum</span><span class="sxs-lookup"><span data-stu-id="b6cea-281">Minimum</span></span> | <span data-ttu-id="b6cea-282">Maximum</span><span class="sxs-lookup"><span data-stu-id="b6cea-282">Maximum</span></span> | <span data-ttu-id="b6cea-283">Initial</span><span class="sxs-lookup"><span data-stu-id="b6cea-283">Initial</span></span> |
| ------------ | ---------- | ----- | -------------- | ------- | ------- | ------- |
| <span data-ttu-id="b6cea-284">Voltage</span><span class="sxs-lookup"><span data-stu-id="b6cea-284">Voltage</span></span>      | <span data-ttu-id="b6cea-285">setVoltage</span><span class="sxs-lookup"><span data-stu-id="b6cea-285">setVoltage</span></span> | <span data-ttu-id="b6cea-286">Volts</span><span class="sxs-lookup"><span data-stu-id="b6cea-286">Volts</span></span> | <span data-ttu-id="b6cea-287">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-287">0</span></span>              | <span data-ttu-id="b6cea-288">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-288">0</span></span>       | <span data-ttu-id="b6cea-289">240</span><span class="sxs-lookup"><span data-stu-id="b6cea-289">240</span></span>     | <span data-ttu-id="b6cea-290">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-290">0</span></span>       |
| <span data-ttu-id="b6cea-291">Current</span><span class="sxs-lookup"><span data-stu-id="b6cea-291">Current</span></span>      | <span data-ttu-id="b6cea-292">setCurrent</span><span class="sxs-lookup"><span data-stu-id="b6cea-292">setCurrent</span></span> | <span data-ttu-id="b6cea-293">Amps</span><span class="sxs-lookup"><span data-stu-id="b6cea-293">Amps</span></span>  | <span data-ttu-id="b6cea-294">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-294">0</span></span>              | <span data-ttu-id="b6cea-295">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-295">0</span></span>       | <span data-ttu-id="b6cea-296">100</span><span class="sxs-lookup"><span data-stu-id="b6cea-296">100</span></span>     | <span data-ttu-id="b6cea-297">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-297">0</span></span>       |
| <span data-ttu-id="b6cea-298">Fan Speed</span><span class="sxs-lookup"><span data-stu-id="b6cea-298">Fan Speed</span></span>    | <span data-ttu-id="b6cea-299">fanSpeed</span><span class="sxs-lookup"><span data-stu-id="b6cea-299">fanSpeed</span></span>   | <span data-ttu-id="b6cea-300">RPM</span><span class="sxs-lookup"><span data-stu-id="b6cea-300">RPM</span></span>   | <span data-ttu-id="b6cea-301">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-301">0</span></span>              | <span data-ttu-id="b6cea-302">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-302">0</span></span>       | <span data-ttu-id="b6cea-303">1000</span><span class="sxs-lookup"><span data-stu-id="b6cea-303">1000</span></span>    | <span data-ttu-id="b6cea-304">0</span><span class="sxs-lookup"><span data-stu-id="b6cea-304">0</span></span>       |

<span data-ttu-id="b6cea-305">Toggle settings</span><span class="sxs-lookup"><span data-stu-id="b6cea-305">Toggle settings</span></span>

| <span data-ttu-id="b6cea-306">Display name</span><span class="sxs-lookup"><span data-stu-id="b6cea-306">Display name</span></span> | <span data-ttu-id="b6cea-307">Field name</span><span class="sxs-lookup"><span data-stu-id="b6cea-307">Field name</span></span> | <span data-ttu-id="b6cea-308">On text</span><span class="sxs-lookup"><span data-stu-id="b6cea-308">On text</span></span> | <span data-ttu-id="b6cea-309">Off text</span><span class="sxs-lookup"><span data-stu-id="b6cea-309">Off text</span></span> | <span data-ttu-id="b6cea-310">Initial</span><span class="sxs-lookup"><span data-stu-id="b6cea-310">Initial</span></span> |
| ------------ | ---------- | ------- | -------- | ------- |
| <span data-ttu-id="b6cea-311">IR</span><span class="sxs-lookup"><span data-stu-id="b6cea-311">IR</span></span>           | <span data-ttu-id="b6cea-312">activateIR</span><span class="sxs-lookup"><span data-stu-id="b6cea-312">activateIR</span></span> | <span data-ttu-id="b6cea-313">ON</span><span class="sxs-lookup"><span data-stu-id="b6cea-313">ON</span></span>      | <span data-ttu-id="b6cea-314">OFF</span><span class="sxs-lookup"><span data-stu-id="b6cea-314">OFF</span></span>      | <span data-ttu-id="b6cea-315">Off</span><span class="sxs-lookup"><span data-stu-id="b6cea-315">Off</span></span>     |

### <a name="properties"></a><span data-ttu-id="b6cea-316">Properties</span><span class="sxs-lookup"><span data-stu-id="b6cea-316">Properties</span></span>

| <span data-ttu-id="b6cea-317">Type</span><span class="sxs-lookup"><span data-stu-id="b6cea-317">Type</span></span>            | <span data-ttu-id="b6cea-318">Display name</span><span class="sxs-lookup"><span data-stu-id="b6cea-318">Display name</span></span> | <span data-ttu-id="b6cea-319">Field name</span><span class="sxs-lookup"><span data-stu-id="b6cea-319">Field name</span></span> | <span data-ttu-id="b6cea-320">Data type</span><span class="sxs-lookup"><span data-stu-id="b6cea-320">Data type</span></span> |
| --------------- | ------------ | ---------- | --------- |
| <span data-ttu-id="b6cea-321">Device property</span><span class="sxs-lookup"><span data-stu-id="b6cea-321">Device property</span></span> | <span data-ttu-id="b6cea-322">Die number</span><span class="sxs-lookup"><span data-stu-id="b6cea-322">Die number</span></span>   | <span data-ttu-id="b6cea-323">dieNumber</span><span class="sxs-lookup"><span data-stu-id="b6cea-323">dieNumber</span></span>  | <span data-ttu-id="b6cea-324">number</span><span class="sxs-lookup"><span data-stu-id="b6cea-324">number</span></span>    |
| <span data-ttu-id="b6cea-325">Device property</span><span class="sxs-lookup"><span data-stu-id="b6cea-325">Device property</span></span> | <span data-ttu-id="b6cea-326">Device Location</span><span class="sxs-lookup"><span data-stu-id="b6cea-326">Device Location</span></span>   | <span data-ttu-id="b6cea-327">location</span><span class="sxs-lookup"><span data-stu-id="b6cea-327">location</span></span>  | <span data-ttu-id="b6cea-328">location</span><span class="sxs-lookup"><span data-stu-id="b6cea-328">location</span></span>    |
| <span data-ttu-id="b6cea-329">Text</span><span class="sxs-lookup"><span data-stu-id="b6cea-329">Text</span></span>            | <span data-ttu-id="b6cea-330">Manufactured In</span><span class="sxs-lookup"><span data-stu-id="b6cea-330">Manufactured In</span></span>     | <span data-ttu-id="b6cea-331">manufacturedIn</span><span class="sxs-lookup"><span data-stu-id="b6cea-331">manufacturedIn</span></span>   | <span data-ttu-id="b6cea-332">N/A</span><span class="sxs-lookup"><span data-stu-id="b6cea-332">N/A</span></span>       |



## <a name="next-steps"></a><span data-ttu-id="b6cea-333">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6cea-333">Next steps</span></span>

<span data-ttu-id="b6cea-334">Now that you have learned how to connect a DevKit device to your Azure IoT Central application, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="b6cea-334">Now that you have learned how to connect a DevKit device to your Azure IoT Central application, here are the suggested next steps:</span></span>

* [<span data-ttu-id="b6cea-335">Prepare and connect a Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b6cea-335">Prepare and connect a Raspberry Pi</span></span>](howto-connect-raspberry-pi-python.md)
