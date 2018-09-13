---
title: Connect a Raspberry Pi to Azure IoT Suite using C with real sensors| Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use C to connect your Raspberry Pi to the remote monitoring solution, send telemetry from sensors to the cloud, and respond to methods invoked from the solution dashboard.
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
ms.openlocfilehash: 635eb9d4e85eaf43dc83f2bd5a0d0f7c32620d98
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871405"
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="f5560-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using C</span><span class="sxs-lookup"><span data-stu-id="f5560-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f5560-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span><span class="sxs-lookup"><span data-stu-id="f5560-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="f5560-106">The tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="f5560-106">The tutorial uses:</span></span>

- <span data-ttu-id="f5560-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span><span class="sxs-lookup"><span data-stu-id="f5560-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="f5560-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span><span class="sxs-lookup"><span data-stu-id="f5560-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="f5560-109">Overview</span><span class="sxs-lookup"><span data-stu-id="f5560-109">Overview</span></span>

<span data-ttu-id="f5560-110">In this tutorial, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5560-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="f5560-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f5560-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="f5560-112">This step automatically deploys and configures multiple Azure services.</span><span class="sxs-lookup"><span data-stu-id="f5560-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f5560-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="f5560-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="f5560-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="f5560-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prerequisites](../../includes/iot-suite-v1-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f5560-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f5560-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f5560-116">The deployment reflects a real enterprise architecture.</span><span class="sxs-lookup"><span data-stu-id="f5560-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f5560-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span><span class="sxs-lookup"><span data-stu-id="f5560-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f5560-118">If you need the preconfigured solution again, you can easily recreate it.</span><span class="sxs-lookup"><span data-stu-id="f5560-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f5560-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f5560-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="f5560-120">Download and configure the sample</span><span class="sxs-lookup"><span data-stu-id="f5560-120">Download and configure the sample</span></span>

<span data-ttu-id="f5560-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f5560-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="f5560-122">Clone the repositories</span><span class="sxs-lookup"><span data-stu-id="f5560-122">Clone the repositories</span></span>

<span data-ttu-id="f5560-123">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span><span class="sxs-lookup"><span data-stu-id="f5560-123">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="f5560-124">Update the device connection string</span><span class="sxs-lookup"><span data-stu-id="f5560-124">Update the device connection string</span></span>

<span data-ttu-id="f5560-125">Open the sample source file in the **nano** editor using the following command:</span><span class="sxs-lookup"><span data-stu-id="f5560-125">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="f5560-126">Locate the following lines:</span><span class="sxs-lookup"><span data-stu-id="f5560-126">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="f5560-127">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5560-127">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="f5560-128">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f5560-128">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="f5560-129">Build the sample</span><span class="sxs-lookup"><span data-stu-id="f5560-129">Build the sample</span></span>

<span data-ttu-id="f5560-130">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f5560-130">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="f5560-131">You can now build the updated sample solution on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f5560-131">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="f5560-132">You can now run the sample program on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f5560-132">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="f5560-133">Enter the command:</span><span class="sxs-lookup"><span data-stu-id="f5560-133">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="f5560-134">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f5560-134">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output from Raspberry Pi app][img-raspberry-output]

<span data-ttu-id="f5560-136">Press **Ctrl-C** to exit the program at any time.</span><span class="sxs-lookup"><span data-stu-id="f5560-136">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="f5560-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5560-137">Next steps</span></span>

<span data-ttu-id="f5560-138">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f5560-138">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
