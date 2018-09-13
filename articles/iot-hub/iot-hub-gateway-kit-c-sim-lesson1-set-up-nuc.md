---
title: 'Simulated device & Azure IoT Gateway - Lesson 1: Set up NUC | Microsoft Docs'
description: Set up Intel NUC to work as an IoT gateway between a sensor and Azure IoT Hub to collect sensor information and send it to IoT Hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: yjianfeng
tags: ''
keywords: iot gateway, intel nuc, nuc computer, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a74b0129231499cc22d222fe09f99678a779cc4f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564521"
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="131f3-104">Set up Intel NUC as an IoT gateway</span><span class="sxs-lookup"><span data-stu-id="131f3-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="131f3-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="131f3-105">What you will do</span></span>

- <span data-ttu-id="131f3-106">Set up Intel NUC as an IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="131f3-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="131f3-107">Install the Azure IoT Gateway SDK package on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="131f3-107">Install the Azure IoT Gateway SDK package on Intel NUC.</span></span>
- <span data-ttu-id="131f3-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="131f3-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="131f3-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="131f3-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="131f3-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="131f3-110">What you will learn</span></span>

<span data-ttu-id="131f3-111">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="131f3-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="131f3-112">How to connect Intel NUC with peripherals.</span><span class="sxs-lookup"><span data-stu-id="131f3-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="131f3-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="131f3-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="131f3-114">How to run the "hello_world" sample application to verify the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="131f3-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="131f3-115">What you need</span><span class="sxs-lookup"><span data-stu-id="131f3-115">What you need</span></span>

- <span data-ttu-id="131f3-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux \*7.0.0.13) preinstalled.</span><span class="sxs-lookup"><span data-stu-id="131f3-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux \*7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="131f3-117">An Ethernet cable.</span><span class="sxs-lookup"><span data-stu-id="131f3-117">An Ethernet cable.</span></span>
- <span data-ttu-id="131f3-118">A keyboard.</span><span class="sxs-lookup"><span data-stu-id="131f3-118">A keyboard.</span></span>
- <span data-ttu-id="131f3-119">An HDMI or VGA cable.</span><span class="sxs-lookup"><span data-stu-id="131f3-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="131f3-120">A monitor with an HDMI or VGA port.</span><span class="sxs-lookup"><span data-stu-id="131f3-120">A monitor with an HDMI or VGA port.</span></span>

![Gateway Kit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="131f3-122">Connect Intel NUC with the peripherals</span><span class="sxs-lookup"><span data-stu-id="131f3-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="131f3-123">The image below is an example of Intel NUC that is connected with various peripherals:</span><span class="sxs-lookup"><span data-stu-id="131f3-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="131f3-124">Connected to a keyboard.</span><span class="sxs-lookup"><span data-stu-id="131f3-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="131f3-125">Connected to the monitor by a VGA cable or HDMI cable.</span><span class="sxs-lookup"><span data-stu-id="131f3-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="131f3-126">Connected to a wired network by an Ethernet cable.</span><span class="sxs-lookup"><span data-stu-id="131f3-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="131f3-127">Connected to the power supply with a power cable.</span><span class="sxs-lookup"><span data-stu-id="131f3-127">Connected to the power supply with a power cable.</span></span>

![Intel NUC connected to peripherals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="131f3-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="131f3-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="131f3-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span><span class="sxs-lookup"><span data-stu-id="131f3-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="131f3-131">If you already know the IP address, you can skip to step 3 in this section.</span><span class="sxs-lookup"><span data-stu-id="131f3-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="131f3-132">Turn on Intel NUC by pressing the Power button and log in the system.</span><span class="sxs-lookup"><span data-stu-id="131f3-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="131f3-133">The default user name and password are both `root`.</span><span class="sxs-lookup"><span data-stu-id="131f3-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="131f3-134">Get the IP address of NUC by running the `ifconfig` command.</span><span class="sxs-lookup"><span data-stu-id="131f3-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="131f3-135">This step is done on the NUC device.</span><span class="sxs-lookup"><span data-stu-id="131f3-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="131f3-136">Here is an example of the command output.</span><span class="sxs-lookup"><span data-stu-id="131f3-136">Here is an example of the command output.</span></span>

   ![ifconfig output showing NUC IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="131f3-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="131f3-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="131f3-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="131f3-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="131f3-140">[PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="131f3-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="131f3-141">The build-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="131f3-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="131f3-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span><span class="sxs-lookup"><span data-stu-id="131f3-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="131f3-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span><span class="sxs-lookup"><span data-stu-id="131f3-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="131f3-144">Here is the example use SSH client on macOS.</span><span class="sxs-lookup"><span data-stu-id="131f3-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="131f3-145">![SSH client running on macOS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="131f3-145">![SSH client running on macOS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-gateway-sdk-package"></a><span data-ttu-id="131f3-146">Install the Azure IoT Gateway SDK package</span><span class="sxs-lookup"><span data-stu-id="131f3-146">Install the Azure IoT Gateway SDK package</span></span>

<span data-ttu-id="131f3-147">The Azure IoT Gateway SDK package contains the pre-compiled binaries of the SDK and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="131f3-147">The Azure IoT Gateway SDK package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="131f3-148">These binaries are the Azure IoT Gateway SDK, the Azure IoT SDK and the corresponding tools.</span><span class="sxs-lookup"><span data-stu-id="131f3-148">These binaries are the Azure IoT Gateway SDK, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="131f3-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="131f3-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="131f3-150">The SDK is the core part of the gateway.</span><span class="sxs-lookup"><span data-stu-id="131f3-150">The SDK is the core part of the gateway.</span></span> <span data-ttu-id="131f3-151">To install the package, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="131f3-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="131f3-152">Add the IoT cloud repository by running the following commands in a terminal window:</span><span class="sxs-lookup"><span data-stu-id="131f3-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="131f3-153">The `rpm` command imports the rpm key.</span><span class="sxs-lookup"><span data-stu-id="131f3-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="131f3-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="131f3-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="131f3-155">Before you run the `smart update` command, you see an output like below.</span><span class="sxs-lookup"><span data-stu-id="131f3-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![rpm and smart channel commands output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="131f3-157">Install the package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="131f3-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="131f3-158">`packagegroup-cloud-azure` is the name of the package.</span><span class="sxs-lookup"><span data-stu-id="131f3-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="131f3-159">The `smart install` command is used to install the package.</span><span class="sxs-lookup"><span data-stu-id="131f3-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="131f3-160">After the package is installed, Intel NUC is expected to work as a gateway.</span><span class="sxs-lookup"><span data-stu-id="131f3-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-gateway-sdk-helloworld-sample-application"></a><span data-ttu-id="131f3-161">Run the Azure IoT Gateway SDK "hello_world" sample application</span><span class="sxs-lookup"><span data-stu-id="131f3-161">Run the Azure IoT Gateway SDK "hello_world" sample application</span></span>

<span data-ttu-id="131f3-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span><span class="sxs-lookup"><span data-stu-id="131f3-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="131f3-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Gateway SDK architecture to log a hello world message to a file every 5 seconds.</span><span class="sxs-lookup"><span data-stu-id="131f3-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Gateway SDK architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="131f3-164">You can run the sample "hello_world" sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="131f3-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="131f3-165">The sample application produces the following output if the gateway functionality is working correctly:</span><span class="sxs-lookup"><span data-stu-id="131f3-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="131f3-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="131f3-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="131f3-168">Summary</span><span class="sxs-lookup"><span data-stu-id="131f3-168">Summary</span></span>

<span data-ttu-id="131f3-169">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="131f3-169">Congratulations!</span></span> <span data-ttu-id="131f3-170">You've finished setting up Intel NUC as a gateway.</span><span class="sxs-lookup"><span data-stu-id="131f3-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="131f3-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span><span class="sxs-lookup"><span data-stu-id="131f3-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="131f3-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="131f3-172">Next steps</span></span>
[<span data-ttu-id="131f3-173">Get your host computer and Azure IoT hub ready</span><span class="sxs-lookup"><span data-stu-id="131f3-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)






