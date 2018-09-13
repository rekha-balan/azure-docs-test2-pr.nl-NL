---
title: Connect a Raspberry Pi to Azure IoT Suite using Node.js with simulated telemetry | Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use Node.js to connect your Raspberry Pi to the remote monitoring solution, send simulated telemetry to the cloud, and respond to methods invoked from the solution dashboard.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 53297049fd36eae3839c6a8146afc336b8f5cd02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966580"
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="e8db0-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span><span class="sxs-lookup"><span data-stu-id="e8db0-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

<span data-ttu-id="e8db0-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span><span class="sxs-lookup"><span data-stu-id="e8db0-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="e8db0-106">The tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="e8db0-106">The tutorial uses:</span></span>

- <span data-ttu-id="e8db0-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span><span class="sxs-lookup"><span data-stu-id="e8db0-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="e8db0-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span><span class="sxs-lookup"><span data-stu-id="e8db0-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="e8db0-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e8db0-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="e8db0-110">The deployment reflects a real enterprise architecture.</span><span class="sxs-lookup"><span data-stu-id="e8db0-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="e8db0-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span><span class="sxs-lookup"><span data-stu-id="e8db0-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="e8db0-112">If you need the preconfigured solution again, you can easily recreate it.</span><span class="sxs-lookup"><span data-stu-id="e8db0-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="e8db0-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="e8db0-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="e8db0-114">Download and configure the sample</span><span class="sxs-lookup"><span data-stu-id="e8db0-114">Download and configure the sample</span></span>

<span data-ttu-id="e8db0-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e8db0-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="e8db0-116">Install Node.js</span><span class="sxs-lookup"><span data-stu-id="e8db0-116">Install Node.js</span></span>

<span data-ttu-id="e8db0-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e8db0-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="e8db0-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span><span class="sxs-lookup"><span data-stu-id="e8db0-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="e8db0-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="e8db0-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="e8db0-120">Use the following command to update your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="e8db0-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="e8db0-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="e8db0-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="e8db0-122">Use the following command to install the binaries:</span><span class="sxs-lookup"><span data-stu-id="e8db0-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="e8db0-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span><span class="sxs-lookup"><span data-stu-id="e8db0-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="e8db0-124">Clone the repositories</span><span class="sxs-lookup"><span data-stu-id="e8db0-124">Clone the repositories</span></span>

<span data-ttu-id="e8db0-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span><span class="sxs-lookup"><span data-stu-id="e8db0-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="e8db0-126">Update the device connection string</span><span class="sxs-lookup"><span data-stu-id="e8db0-126">Update the device connection string</span></span>

<span data-ttu-id="e8db0-127">Open the sample source file in the **nano** editor using the following command:</span><span class="sxs-lookup"><span data-stu-id="e8db0-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="e8db0-128">Find the line:</span><span class="sxs-lookup"><span data-stu-id="e8db0-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="e8db0-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e8db0-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="e8db0-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="e8db0-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="e8db0-131">Run the sample</span><span class="sxs-lookup"><span data-stu-id="e8db0-131">Run the sample</span></span>

<span data-ttu-id="e8db0-132">Run the following commands to install the prerequisite packages for the sample:</span><span class="sxs-lookup"><span data-stu-id="e8db0-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="e8db0-133">You can now run the sample program on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e8db0-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="e8db0-134">Enter the command:</span><span class="sxs-lookup"><span data-stu-id="e8db0-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="e8db0-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="e8db0-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output from Raspberry Pi app][img-raspberry-output]

<span data-ttu-id="e8db0-137">Press **Ctrl-C** to exit the program at any time.</span><span class="sxs-lookup"><span data-stu-id="e8db0-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="e8db0-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8db0-138">Next steps</span></span>

<span data-ttu-id="e8db0-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="e8db0-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
