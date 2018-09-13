---
title: Connect a Raspberry Pi to Azure IoT Suite using C to support firmware updates | Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use C to connect your Raspberry Pi to the remote monitoring solution, send telemetry from sensors to the cloud, and perform a remote firmware update.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 8160752b0116c3ef3e6b6ab7920bb35e471f180b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856156"
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="f1685-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span><span class="sxs-lookup"><span data-stu-id="f1685-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f1685-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span><span class="sxs-lookup"><span data-stu-id="f1685-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="f1685-106">Develop a temperature and humidity reader that can communicate with the cloud.</span><span class="sxs-lookup"><span data-stu-id="f1685-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="f1685-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f1685-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="f1685-108">The tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="f1685-108">The tutorial uses:</span></span>

* <span data-ttu-id="f1685-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span><span class="sxs-lookup"><span data-stu-id="f1685-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
* <span data-ttu-id="f1685-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span><span class="sxs-lookup"><span data-stu-id="f1685-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="f1685-111">Overview</span><span class="sxs-lookup"><span data-stu-id="f1685-111">Overview</span></span>

<span data-ttu-id="f1685-112">In this tutorial, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1685-112">In this tutorial, you complete the following steps:</span></span>

* <span data-ttu-id="f1685-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f1685-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="f1685-114">This step automatically deploys and configures multiple Azure services.</span><span class="sxs-lookup"><span data-stu-id="f1685-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="f1685-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="f1685-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
* <span data-ttu-id="f1685-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="f1685-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
* <span data-ttu-id="f1685-117">Use the sample device code to update the client application.</span><span class="sxs-lookup"><span data-stu-id="f1685-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prerequisites](../../includes/iot-suite-v1-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f1685-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f1685-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f1685-119">The deployment reflects a real enterprise architecture.</span><span class="sxs-lookup"><span data-stu-id="f1685-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f1685-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span><span class="sxs-lookup"><span data-stu-id="f1685-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f1685-121">If you need the preconfigured solution again, you can easily recreate it.</span><span class="sxs-lookup"><span data-stu-id="f1685-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f1685-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f1685-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="f1685-123">Download and configure the sample</span><span class="sxs-lookup"><span data-stu-id="f1685-123">Download and configure the sample</span></span>

<span data-ttu-id="f1685-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f1685-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="f1685-125">Clone the repositories</span><span class="sxs-lookup"><span data-stu-id="f1685-125">Clone the repositories</span></span>

<span data-ttu-id="f1685-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span><span class="sxs-lookup"><span data-stu-id="f1685-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="f1685-127">Update the device connection string</span><span class="sxs-lookup"><span data-stu-id="f1685-127">Update the device connection string</span></span>

<span data-ttu-id="f1685-128">Open the sample configuration file in the **nano** editor using the following command:</span><span class="sxs-lookup"><span data-stu-id="f1685-128">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="f1685-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f1685-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="f1685-130">When you are done, the contents of the deviceinfo file should look like the following example:</span><span class="sxs-lookup"><span data-stu-id="f1685-130">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="f1685-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f1685-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="f1685-132">Build the sample</span><span class="sxs-lookup"><span data-stu-id="f1685-132">Build the sample</span></span>

<span data-ttu-id="f1685-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f1685-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="f1685-134">You can now build the sample solution on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f1685-134">You can now build the sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="f1685-135">You can now run the sample program on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f1685-135">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="f1685-136">Enter the command:</span><span class="sxs-lookup"><span data-stu-id="f1685-136">Enter the command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="f1685-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f1685-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output from Raspberry Pi app][img-raspberry-output]

<span data-ttu-id="f1685-139">Press **Ctrl-C** to exit the program at any time.</span><span class="sxs-lookup"><span data-stu-id="f1685-139">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="f1685-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span><span class="sxs-lookup"><span data-stu-id="f1685-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="f1685-141">Select your Raspberry Pi in the **Device List**.</span><span class="sxs-lookup"><span data-stu-id="f1685-141">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="f1685-142">Then choose **Methods**:</span><span class="sxs-lookup"><span data-stu-id="f1685-142">Then choose **Methods**:</span></span>

    ![List devices in dashboard][img-list-devices]

1. <span data-ttu-id="f1685-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span><span class="sxs-lookup"><span data-stu-id="f1685-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="f1685-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="f1685-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="f1685-146">This archive file contains the implementation of version 2.0 of the firmware.</span><span class="sxs-lookup"><span data-stu-id="f1685-146">This archive file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="f1685-147">Choose **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="f1685-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="f1685-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="f1685-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="f1685-149">It then starts the firmware update process by downloading the new version of the firmware:</span><span class="sxs-lookup"><span data-stu-id="f1685-149">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Show method history][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="f1685-151">Observe the firmware update process</span><span class="sxs-lookup"><span data-stu-id="f1685-151">Observe the firmware update process</span></span>

<span data-ttu-id="f1685-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span><span class="sxs-lookup"><span data-stu-id="f1685-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="f1685-153">You can view the progress in of the update process on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f1685-153">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Show update progress][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="f1685-155">The remote monitoring app restarts silently when the update completes.</span><span class="sxs-lookup"><span data-stu-id="f1685-155">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="f1685-156">Use the command `ps -ef` to verify it is running.</span><span class="sxs-lookup"><span data-stu-id="f1685-156">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="f1685-157">If you want to terminate the process, use the `kill` command with the process id.</span><span class="sxs-lookup"><span data-stu-id="f1685-157">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="f1685-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="f1685-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="f1685-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span><span class="sxs-lookup"><span data-stu-id="f1685-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Show job status][img-job-status]

    <span data-ttu-id="f1685-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span><span class="sxs-lookup"><span data-stu-id="f1685-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="f1685-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span><span class="sxs-lookup"><span data-stu-id="f1685-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="f1685-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f1685-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="f1685-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span><span class="sxs-lookup"><span data-stu-id="f1685-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1685-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1685-165">Next steps</span></span>

<span data-ttu-id="f1685-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f1685-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md