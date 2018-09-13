---
title: 'SensorTag Device & Azure IoT Gateway - Lesson 1: Set up Intel NUC | Microsoft Docs'
description: Set up Intel NUC to work as an IoT gateway between a sensor and Azure IoT Hub to collect sensor information and send it to IoT Hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: yjianfeng
tags: ''
keywords: iot gateway, intel nuc, nuc computer, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3f624315ccfdd55d989d038611d216bb8e0f123b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564511"
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="26adb-104">Set up Intel NUC as an IoT gateway</span><span class="sxs-lookup"><span data-stu-id="26adb-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="26adb-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="26adb-105">What you will do</span></span>

- <span data-ttu-id="26adb-106">Set up Intel NUC as an IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="26adb-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="26adb-107">Install the Azure IoT Gateway SDK package on the Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="26adb-107">Install the Azure IoT Gateway SDK package on the Intel NUC.</span></span>
- <span data-ttu-id="26adb-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="26adb-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span></span>

  > <span data-ttu-id="26adb-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="26adb-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="26adb-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="26adb-110">What you will learn</span></span>

<span data-ttu-id="26adb-111">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="26adb-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="26adb-112">How to connect Intel NUC with peripherals.</span><span class="sxs-lookup"><span data-stu-id="26adb-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="26adb-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="26adb-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="26adb-114">How to run the "hello_world" sample application to verify the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="26adb-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="26adb-115">What you need</span><span class="sxs-lookup"><span data-stu-id="26adb-115">What you need</span></span>

- <span data-ttu-id="26adb-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux \*7.0.0.13) preinstalled.</span><span class="sxs-lookup"><span data-stu-id="26adb-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux \*7.0.0.13) preinstalled.</span></span> <span data-ttu-id="26adb-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="26adb-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="26adb-118">An Ethernet cable.</span><span class="sxs-lookup"><span data-stu-id="26adb-118">An Ethernet cable.</span></span>
- <span data-ttu-id="26adb-119">A keyboard.</span><span class="sxs-lookup"><span data-stu-id="26adb-119">A keyboard.</span></span>
- <span data-ttu-id="26adb-120">An HDMI or VGA cable.</span><span class="sxs-lookup"><span data-stu-id="26adb-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="26adb-121">A monitor with an HDMI or VGA port.</span><span class="sxs-lookup"><span data-stu-id="26adb-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="26adb-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="26adb-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Gateway Kit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="26adb-124">Connect Intel NUC with the peripherals</span><span class="sxs-lookup"><span data-stu-id="26adb-124">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="26adb-125">The image below is an example of Intel NUC that is connected with various peripherals:</span><span class="sxs-lookup"><span data-stu-id="26adb-125">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="26adb-126">Connected to a keyboard.</span><span class="sxs-lookup"><span data-stu-id="26adb-126">Connected to a keyboard.</span></span>
2. <span data-ttu-id="26adb-127">Connected to a monitor with a VGA cable or HDMI cable.</span><span class="sxs-lookup"><span data-stu-id="26adb-127">Connected to a monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="26adb-128">Connected to a wired network with an Ethernet cable.</span><span class="sxs-lookup"><span data-stu-id="26adb-128">Connected to a wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="26adb-129">Connected to a power supply with a power cable.</span><span class="sxs-lookup"><span data-stu-id="26adb-129">Connected to a power supply with a power cable.</span></span>

![Intel NUC connected to peripherals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="26adb-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="26adb-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="26adb-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span><span class="sxs-lookup"><span data-stu-id="26adb-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span></span> <span data-ttu-id="26adb-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span><span class="sxs-lookup"><span data-stu-id="26adb-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span></span>

1. <span data-ttu-id="26adb-134">Turn on the Intel NUC by pressing the power button and then log in.</span><span class="sxs-lookup"><span data-stu-id="26adb-134">Turn on the Intel NUC by pressing the power button and then log in.</span></span>

   <span data-ttu-id="26adb-135">The default user name and password are both `root`.</span><span class="sxs-lookup"><span data-stu-id="26adb-135">The default user name and password are both `root`.</span></span>

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="26adb-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span><span class="sxs-lookup"><span data-stu-id="26adb-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span></span>

   <span data-ttu-id="26adb-137">Here is an example of the command output.</span><span class="sxs-lookup"><span data-stu-id="26adb-137">Here is an example of the command output.</span></span>

   ![ifconfig output showing Intel NUC IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="26adb-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span><span class="sxs-lookup"><span data-stu-id="26adb-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="26adb-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="26adb-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>

    - <span data-ttu-id="26adb-141">[PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="26adb-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="26adb-142">The built-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="26adb-142">The built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="26adb-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span><span class="sxs-lookup"><span data-stu-id="26adb-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span></span> <span data-ttu-id="26adb-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span><span class="sxs-lookup"><span data-stu-id="26adb-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span></span> <span data-ttu-id="26adb-145">Here is an example that uses an SSH client on macOS.</span><span class="sxs-lookup"><span data-stu-id="26adb-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="26adb-146">![SSH client running on macOS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="26adb-146">![SSH client running on macOS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-gateway-sdk-package"></a><span data-ttu-id="26adb-147">Install the Azure IoT Gateway SDK package</span><span class="sxs-lookup"><span data-stu-id="26adb-147">Install the Azure IoT Gateway SDK package</span></span>

<span data-ttu-id="26adb-148">The Azure IoT Gateway SDK package contains the pre-compiled binaries of the SDK and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="26adb-148">The Azure IoT Gateway SDK package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="26adb-149">These binaries are the Azure IoT Gateway SDK, the Azure IoT SDK and the corresponding tools.</span><span class="sxs-lookup"><span data-stu-id="26adb-149">These binaries are the Azure IoT Gateway SDK, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="26adb-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="26adb-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span></span> <span data-ttu-id="26adb-151">The SDK is the core part of the gateway.</span><span class="sxs-lookup"><span data-stu-id="26adb-151">The SDK is the core part of the gateway.</span></span> 

<span data-ttu-id="26adb-152">Follow these steps to install the package.</span><span class="sxs-lookup"><span data-stu-id="26adb-152">Follow these steps to install the package.</span></span>

1. <span data-ttu-id="26adb-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span><span class="sxs-lookup"><span data-stu-id="26adb-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="26adb-154">Enter 'y', when it prompts you to 'Include this channel?'</span><span class="sxs-lookup"><span data-stu-id="26adb-154">Enter 'y', when it prompts you to 'Include this channel?'</span></span>

   <span data-ttu-id="26adb-155">The `rpm` command imports the rpm key.</span><span class="sxs-lookup"><span data-stu-id="26adb-155">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="26adb-156">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="26adb-156">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="26adb-157">Before you run the `smart update` command, you will see an output like below.</span><span class="sxs-lookup"><span data-stu-id="26adb-157">Before you run the `smart update` command, you will see an output like below.</span></span>

   ![rpm and smart channel commands output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="26adb-159">Execute the smart update command:</span><span class="sxs-lookup"><span data-stu-id="26adb-159">Execute the smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="26adb-160">Install the Azure IoT Gateway package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="26adb-160">Install the Azure IoT Gateway package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="26adb-161">`packagegroup-cloud-azure` is the name of the package.</span><span class="sxs-lookup"><span data-stu-id="26adb-161">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="26adb-162">The `smart install` command is used to install the package.</span><span class="sxs-lookup"><span data-stu-id="26adb-162">The `smart install` command is used to install the package.</span></span>

    > <span data-ttu-id="26adb-163">Run the following command if you see this error: 'public key not available'</span><span class="sxs-lookup"><span data-stu-id="26adb-163">Run the following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="26adb-164">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span><span class="sxs-lookup"><span data-stu-id="26adb-164">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="26adb-165">After the package is installed, Intel NUC is ready to function as a gateway.</span><span class="sxs-lookup"><span data-stu-id="26adb-165">After the package is installed, Intel NUC is ready to function as a gateway.</span></span>

## <a name="run-the-azure-iot-gateway-sdk-helloworld-sample-application"></a><span data-ttu-id="26adb-166">Run the Azure IoT Gateway SDK "hello_world" sample application</span><span class="sxs-lookup"><span data-stu-id="26adb-166">Run the Azure IoT Gateway SDK "hello_world" sample application</span></span>

<span data-ttu-id="26adb-167">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of the Azure IoT Gateway SDK architecture to log a hello world message to a file (log.txt) every 5 seconds.</span><span class="sxs-lookup"><span data-stu-id="26adb-167">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of the Azure IoT Gateway SDK architecture to log a hello world message to a file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="26adb-168">You can run the Hello World sample by executing the following commands:</span><span class="sxs-lookup"><span data-stu-id="26adb-168">You can run the Hello World sample by executing the following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="26adb-169">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span><span class="sxs-lookup"><span data-stu-id="26adb-169">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span></span>
<span data-ttu-id="26adb-170">![application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="26adb-170">![application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="26adb-171">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span><span class="sxs-lookup"><span data-stu-id="26adb-171">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="26adb-172">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="26adb-172">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="26adb-173">Open log.txt using the following command:</span><span class="sxs-lookup"><span data-stu-id="26adb-173">Open log.txt using the following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="26adb-174">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span><span class="sxs-lookup"><span data-stu-id="26adb-174">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span></span>
<span data-ttu-id="26adb-175">![log.txt directory view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="26adb-175">![log.txt directory view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="26adb-176">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="26adb-176">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="26adb-177">Summary</span><span class="sxs-lookup"><span data-stu-id="26adb-177">Summary</span></span>

<span data-ttu-id="26adb-178">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="26adb-178">Congratulations!</span></span> <span data-ttu-id="26adb-179">You've finished setting up Intel NUC as a gateway.</span><span class="sxs-lookup"><span data-stu-id="26adb-179">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="26adb-180">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span><span class="sxs-lookup"><span data-stu-id="26adb-180">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26adb-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="26adb-181">Next steps</span></span>
[<span data-ttu-id="26adb-182">Use an IoT gateway to connect a device to Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="26adb-182">Use an IoT gateway to connect a device to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)









