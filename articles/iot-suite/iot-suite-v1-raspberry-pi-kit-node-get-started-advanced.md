---
title: Connect a Raspberry Pi to Azure IoT Suite using Node.js to support firmware updates | Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use Node.js to connect your Raspberry Pi to the remote monitoring solution, send telemetry from sensors to the cloud, and perform a remote firmware update.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 31bbeff8049c6005671b991f965fae7316e3adf6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868896"
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="46171-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span><span class="sxs-lookup"><span data-stu-id="46171-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

<span data-ttu-id="46171-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span><span class="sxs-lookup"><span data-stu-id="46171-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="46171-106">Develop a temperature and humidity reader that can communicate with the cloud.</span><span class="sxs-lookup"><span data-stu-id="46171-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="46171-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="46171-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="46171-108">The tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="46171-108">The tutorial uses:</span></span>

- <span data-ttu-id="46171-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span><span class="sxs-lookup"><span data-stu-id="46171-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="46171-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span><span class="sxs-lookup"><span data-stu-id="46171-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="46171-111">Overview</span><span class="sxs-lookup"><span data-stu-id="46171-111">Overview</span></span>

<span data-ttu-id="46171-112">In this tutorial, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="46171-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="46171-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="46171-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="46171-114">This step automatically deploys and configures multiple Azure services.</span><span class="sxs-lookup"><span data-stu-id="46171-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="46171-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="46171-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="46171-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="46171-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="46171-117">Use the sample device code to update the client application.</span><span class="sxs-lookup"><span data-stu-id="46171-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prerequisites](../../includes/iot-suite-v1-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="46171-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="46171-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="46171-119">The deployment reflects a real enterprise architecture.</span><span class="sxs-lookup"><span data-stu-id="46171-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="46171-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span><span class="sxs-lookup"><span data-stu-id="46171-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="46171-121">If you need the preconfigured solution again, you can easily recreate it.</span><span class="sxs-lookup"><span data-stu-id="46171-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="46171-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="46171-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="46171-123">Download and configure the sample</span><span class="sxs-lookup"><span data-stu-id="46171-123">Download and configure the sample</span></span>

<span data-ttu-id="46171-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="46171-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="46171-125">Install Node.js</span><span class="sxs-lookup"><span data-stu-id="46171-125">Install Node.js</span></span>

<span data-ttu-id="46171-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="46171-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="46171-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span><span class="sxs-lookup"><span data-stu-id="46171-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="46171-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="46171-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="46171-129">Use the following command to update your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="46171-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="46171-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="46171-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="46171-131">Use the following command to install the binaries:</span><span class="sxs-lookup"><span data-stu-id="46171-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="46171-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span><span class="sxs-lookup"><span data-stu-id="46171-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="46171-133">Clone the repositories</span><span class="sxs-lookup"><span data-stu-id="46171-133">Clone the repositories</span></span>

<span data-ttu-id="46171-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span><span class="sxs-lookup"><span data-stu-id="46171-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="46171-135">Update the device connection string</span><span class="sxs-lookup"><span data-stu-id="46171-135">Update the device connection string</span></span>

<span data-ttu-id="46171-136">Open the sample configuration file in the **nano** editor using the following command:</span><span class="sxs-lookup"><span data-stu-id="46171-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="46171-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="46171-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="46171-138">When you are done, the contents of the deviceinfo file should look like the following example:</span><span class="sxs-lookup"><span data-stu-id="46171-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="46171-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="46171-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="46171-140">Run the sample</span><span class="sxs-lookup"><span data-stu-id="46171-140">Run the sample</span></span>

<span data-ttu-id="46171-141">Run the following commands to install the prerequisite packages for the sample:</span><span class="sxs-lookup"><span data-stu-id="46171-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="46171-142">You can now run the sample program on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="46171-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="46171-143">Enter the command:</span><span class="sxs-lookup"><span data-stu-id="46171-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="46171-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="46171-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output from Raspberry Pi app][img-raspberry-output]

<span data-ttu-id="46171-146">Press **Ctrl-C** to exit the program at any time.</span><span class="sxs-lookup"><span data-stu-id="46171-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="46171-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span><span class="sxs-lookup"><span data-stu-id="46171-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="46171-148">Select your Raspberry Pi in the **Device List**.</span><span class="sxs-lookup"><span data-stu-id="46171-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="46171-149">Then choose **Methods**:</span><span class="sxs-lookup"><span data-stu-id="46171-149">Then choose **Methods**:</span></span>

    ![List devices in dashboard][img-list-devices]

1. <span data-ttu-id="46171-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span><span class="sxs-lookup"><span data-stu-id="46171-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="46171-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="46171-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="46171-153">This file contains the implementation of version 2.0 of the firmware.</span><span class="sxs-lookup"><span data-stu-id="46171-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="46171-154">Choose **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="46171-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="46171-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="46171-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="46171-156">It then starts the firmware update process by downloading the new version of the firmware:</span><span class="sxs-lookup"><span data-stu-id="46171-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Show method history][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="46171-158">Observe the firmware update process</span><span class="sxs-lookup"><span data-stu-id="46171-158">Observe the firmware update process</span></span>

<span data-ttu-id="46171-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span><span class="sxs-lookup"><span data-stu-id="46171-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="46171-160">You can view the progress in of the update process on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="46171-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Show update progress][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="46171-162">The remote monitoring app restarts silently when the update completes.</span><span class="sxs-lookup"><span data-stu-id="46171-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="46171-163">Use the command `ps -ef` to verify it is running.</span><span class="sxs-lookup"><span data-stu-id="46171-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="46171-164">If you want to terminate the process, use the `kill` command with the process id.</span><span class="sxs-lookup"><span data-stu-id="46171-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="46171-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="46171-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="46171-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span><span class="sxs-lookup"><span data-stu-id="46171-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Show job status][img-job-status]

    <span data-ttu-id="46171-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span><span class="sxs-lookup"><span data-stu-id="46171-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="46171-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span><span class="sxs-lookup"><span data-stu-id="46171-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="46171-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="46171-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="46171-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span><span class="sxs-lookup"><span data-stu-id="46171-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46171-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="46171-172">Next steps</span></span>

<span data-ttu-id="46171-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="46171-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
