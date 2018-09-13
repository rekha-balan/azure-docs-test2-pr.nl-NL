---
title: Connect a Raspberry Pi to Azure IoT Suite using C with simulated telemetry | Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use C to connect your Raspberry Pi to the remote monitoring solution, send simulated telemetry to the cloud, and respond to methods invoked from the solution dashboard.
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
ms.openlocfilehash: 19b16bff7874a03578b8766668c431553da0d875
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966948"
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="f9086-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C</span><span class="sxs-lookup"><span data-stu-id="f9086-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f9086-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span><span class="sxs-lookup"><span data-stu-id="f9086-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="f9086-106">The tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="f9086-106">The tutorial uses:</span></span>

- <span data-ttu-id="f9086-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span><span class="sxs-lookup"><span data-stu-id="f9086-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="f9086-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span><span class="sxs-lookup"><span data-stu-id="f9086-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f9086-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f9086-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f9086-110">The deployment reflects a real enterprise architecture.</span><span class="sxs-lookup"><span data-stu-id="f9086-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f9086-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span><span class="sxs-lookup"><span data-stu-id="f9086-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f9086-112">If you need the preconfigured solution again, you can easily recreate it.</span><span class="sxs-lookup"><span data-stu-id="f9086-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f9086-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f9086-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="f9086-114">Download and configure the sample</span><span class="sxs-lookup"><span data-stu-id="f9086-114">Download and configure the sample</span></span>

<span data-ttu-id="f9086-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f9086-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="f9086-116">Clone the repositories</span><span class="sxs-lookup"><span data-stu-id="f9086-116">Clone the repositories</span></span>

<span data-ttu-id="f9086-117">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span><span class="sxs-lookup"><span data-stu-id="f9086-117">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="f9086-118">Update the device connection string</span><span class="sxs-lookup"><span data-stu-id="f9086-118">Update the device connection string</span></span>

<span data-ttu-id="f9086-119">Open the sample source file in the **nano** editor using the following command:</span><span class="sxs-lookup"><span data-stu-id="f9086-119">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="f9086-120">Locate the following lines:</span><span class="sxs-lookup"><span data-stu-id="f9086-120">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="f9086-121">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f9086-121">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="f9086-122">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f9086-122">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="f9086-123">Build the sample</span><span class="sxs-lookup"><span data-stu-id="f9086-123">Build the sample</span></span>

<span data-ttu-id="f9086-124">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f9086-124">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="f9086-125">You can now build the updated sample solution on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f9086-125">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="f9086-126">You can now run the sample program on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f9086-126">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="f9086-127">Enter the command:</span><span class="sxs-lookup"><span data-stu-id="f9086-127">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="f9086-128">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f9086-128">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output from Raspberry Pi app][img-raspberry-output]

<span data-ttu-id="f9086-130">Press **Ctrl-C** to exit the program at any time.</span><span class="sxs-lookup"><span data-stu-id="f9086-130">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="f9086-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9086-131">Next steps</span></span>

<span data-ttu-id="f9086-132">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f9086-132">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
