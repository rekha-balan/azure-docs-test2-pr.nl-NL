---
title: Connect a Raspberry Pi to Azure IoT Suite using Node.js with real sensors | Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use Node.js to connect your Raspberry Pi to the remote monitoring solution, send telemetry from sensors to the cloud, and respond to methods invoked from the solution dashboard.
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
ms.openlocfilehash: 9bb4f62b1a3de68ce8796b60fe76cd97b9ab9ade
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966436"
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="82f41-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using Node.js</span><span class="sxs-lookup"><span data-stu-id="82f41-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

<span data-ttu-id="82f41-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span><span class="sxs-lookup"><span data-stu-id="82f41-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="82f41-106">The tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="82f41-106">The tutorial uses:</span></span>

- <span data-ttu-id="82f41-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span><span class="sxs-lookup"><span data-stu-id="82f41-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="82f41-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span><span class="sxs-lookup"><span data-stu-id="82f41-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="82f41-109">Overview</span><span class="sxs-lookup"><span data-stu-id="82f41-109">Overview</span></span>

<span data-ttu-id="82f41-110">In this tutorial, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="82f41-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="82f41-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="82f41-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="82f41-112">This step automatically deploys and configures multiple Azure services.</span><span class="sxs-lookup"><span data-stu-id="82f41-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="82f41-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="82f41-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="82f41-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="82f41-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prerequisites](../../includes/iot-suite-v1-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="82f41-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="82f41-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="82f41-116">The deployment reflects a real enterprise architecture.</span><span class="sxs-lookup"><span data-stu-id="82f41-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="82f41-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span><span class="sxs-lookup"><span data-stu-id="82f41-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="82f41-118">If you need the preconfigured solution again, you can easily recreate it.</span><span class="sxs-lookup"><span data-stu-id="82f41-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="82f41-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="82f41-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="82f41-120">Download and configure the sample</span><span class="sxs-lookup"><span data-stu-id="82f41-120">Download and configure the sample</span></span>

<span data-ttu-id="82f41-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="82f41-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="82f41-122">Install Node.js</span><span class="sxs-lookup"><span data-stu-id="82f41-122">Install Node.js</span></span>

<span data-ttu-id="82f41-123">Install Node.js on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="82f41-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="82f41-124">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span><span class="sxs-lookup"><span data-stu-id="82f41-124">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="82f41-125">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="82f41-125">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="82f41-126">Use the following command to update your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="82f41-126">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="82f41-127">Use the following command to download the Node.js binaries to your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="82f41-127">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="82f41-128">Use the following command to install the binaries:</span><span class="sxs-lookup"><span data-stu-id="82f41-128">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="82f41-129">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span><span class="sxs-lookup"><span data-stu-id="82f41-129">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="82f41-130">Clone the repositories</span><span class="sxs-lookup"><span data-stu-id="82f41-130">Clone the repositories</span></span>

<span data-ttu-id="82f41-131">If you haven't already done so, clone the required repositories by running the following commands on your Pi:</span><span class="sxs-lookup"><span data-stu-id="82f41-131">If you haven't already done so, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="82f41-132">Update the device connection string</span><span class="sxs-lookup"><span data-stu-id="82f41-132">Update the device connection string</span></span>

<span data-ttu-id="82f41-133">Open the sample source file in the **nano** editor using the following command:</span><span class="sxs-lookup"><span data-stu-id="82f41-133">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="82f41-134">Find the line:</span><span class="sxs-lookup"><span data-stu-id="82f41-134">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="82f41-135">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="82f41-135">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="82f41-136">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="82f41-136">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="82f41-137">Run the sample</span><span class="sxs-lookup"><span data-stu-id="82f41-137">Run the sample</span></span>

<span data-ttu-id="82f41-138">Run the following commands to install the prerequisite packages for the sample:</span><span class="sxs-lookup"><span data-stu-id="82f41-138">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="82f41-139">You can now run the sample program on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="82f41-139">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="82f41-140">Enter the command:</span><span class="sxs-lookup"><span data-stu-id="82f41-140">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="82f41-141">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="82f41-141">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output from Raspberry Pi app][img-raspberry-output]

<span data-ttu-id="82f41-143">Press **Ctrl-C** to exit the program at any time.</span><span class="sxs-lookup"><span data-stu-id="82f41-143">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="82f41-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="82f41-144">Next steps</span></span>

<span data-ttu-id="82f41-145">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="82f41-145">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
