---
title: Connect Raspberry Pi (C) to Azure IoT - Troubleshoot | Microsoft Docs
description: Troubleshooting page for Raspberry Pi Node.js experience
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot issues, internet of things problems
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4c03618a94bb9dfbc35a63bd6458b36bc66be098
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556588"
---
# <a name="troubleshooting"></a><span data-ttu-id="141dd-104">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="141dd-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="141dd-105">Hardware issues</span><span class="sxs-lookup"><span data-stu-id="141dd-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="141dd-106">The application runs well but the LED is not blinking</span><span class="sxs-lookup"><span data-stu-id="141dd-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="141dd-107">This issue is always related to the hardware circuit connectivity.</span><span class="sxs-lookup"><span data-stu-id="141dd-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="141dd-108">Use the following steps to identify problems.</span><span class="sxs-lookup"><span data-stu-id="141dd-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="141dd-109">Check that you chose the correct **GPIO** on your board.</span><span class="sxs-lookup"><span data-stu-id="141dd-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="141dd-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="141dd-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="141dd-111">Check that the polarity of your LED is correct.</span><span class="sxs-lookup"><span data-stu-id="141dd-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="141dd-112">The longer leg should indicate the **positive**, anode pin.</span><span class="sxs-lookup"><span data-stu-id="141dd-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="141dd-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="141dd-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="141dd-114">Treat Pi as the DC power.</span><span class="sxs-lookup"><span data-stu-id="141dd-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="141dd-115">Check that the LED works fine.</span><span class="sxs-lookup"><span data-stu-id="141dd-115">Check that the LED works fine.</span></span>

![LED specification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="141dd-117">Other hardware issues</span><span class="sxs-lookup"><span data-stu-id="141dd-117">Other hardware issues</span></span>
<span data-ttu-id="141dd-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="141dd-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="141dd-119">Node.js package issues</span><span class="sxs-lookup"><span data-stu-id="141dd-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="141dd-120">No response during gulp tasks</span><span class="sxs-lookup"><span data-stu-id="141dd-120">No response during gulp tasks</span></span>
<span data-ttu-id="141dd-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span><span class="sxs-lookup"><span data-stu-id="141dd-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="141dd-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span><span class="sxs-lookup"><span data-stu-id="141dd-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="141dd-123">You might see detailed error messages in your console output.</span><span class="sxs-lookup"><span data-stu-id="141dd-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="141dd-124">Device discovery issues</span><span class="sxs-lookup"><span data-stu-id="141dd-124">Device discovery issues</span></span>
<span data-ttu-id="141dd-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="141dd-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="141dd-126">NPM issues</span><span class="sxs-lookup"><span data-stu-id="141dd-126">NPM issues</span></span>
<span data-ttu-id="141dd-127">Try to update your NPM package with the following command:</span><span class="sxs-lookup"><span data-stu-id="141dd-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="141dd-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="141dd-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="141dd-129">Remote debugging</span><span class="sxs-lookup"><span data-stu-id="141dd-129">Remote debugging</span></span>

<span data-ttu-id="141dd-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span><span class="sxs-lookup"><span data-stu-id="141dd-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="141dd-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span><span class="sxs-lookup"><span data-stu-id="141dd-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="141dd-132">Azure-CLI issues</span><span class="sxs-lookup"><span data-stu-id="141dd-132">Azure-CLI issues</span></span>
<span data-ttu-id="141dd-133">The Azure command-line interface (Azure CLI) is a preview build.</span><span class="sxs-lookup"><span data-stu-id="141dd-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="141dd-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span><span class="sxs-lookup"><span data-stu-id="141dd-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="141dd-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span><span class="sxs-lookup"><span data-stu-id="141dd-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="141dd-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="141dd-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="141dd-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="141dd-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="141dd-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span><span class="sxs-lookup"><span data-stu-id="141dd-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="141dd-139">Python installation issues</span><span class="sxs-lookup"><span data-stu-id="141dd-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="141dd-140">Legacy installation issues (macOS)</span><span class="sxs-lookup"><span data-stu-id="141dd-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="141dd-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span><span class="sxs-lookup"><span data-stu-id="141dd-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="141dd-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span><span class="sxs-lookup"><span data-stu-id="141dd-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="141dd-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span><span class="sxs-lookup"><span data-stu-id="141dd-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="141dd-144">The solution is to remove those packages installed by root.</span><span class="sxs-lookup"><span data-stu-id="141dd-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="141dd-145">Use the following steps to complete this task:</span><span class="sxs-lookup"><span data-stu-id="141dd-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="141dd-146">Go to: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="141dd-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="141dd-147">List packages create by root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="141dd-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="141dd-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="141dd-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="141dd-149">Reinstall Python.</span><span class="sxs-lookup"><span data-stu-id="141dd-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="141dd-150">Azure IoT Hub issues</span><span class="sxs-lookup"><span data-stu-id="141dd-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="141dd-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span><span class="sxs-lookup"><span data-stu-id="141dd-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="141dd-152">Device Explorer</span><span class="sxs-lookup"><span data-stu-id="141dd-152">Device Explorer</span></span>
<span data-ttu-id="141dd-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="141dd-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="141dd-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="141dd-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="141dd-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="141dd-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="141dd-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="141dd-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="141dd-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="141dd-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="141dd-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span><span class="sxs-lookup"><span data-stu-id="141dd-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="141dd-159">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="141dd-159">IoT hub Explorer</span></span>
<span data-ttu-id="141dd-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span><span class="sxs-lookup"><span data-stu-id="141dd-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="141dd-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span><span class="sxs-lookup"><span data-stu-id="141dd-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="141dd-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="141dd-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="141dd-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span><span class="sxs-lookup"><span data-stu-id="141dd-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="141dd-164">Azure portal</span><span class="sxs-lookup"><span data-stu-id="141dd-164">Azure portal</span></span>
<span data-ttu-id="141dd-165">A full CLI experience helps you create and manage all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="141dd-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="141dd-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="141dd-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="141dd-167">Azure storage issues</span><span class="sxs-lookup"><span data-stu-id="141dd-167">Azure storage issues</span></span>
<span data-ttu-id="141dd-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="141dd-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="141dd-169">By using this tool, you can connect to your table and see the data in it.</span><span class="sxs-lookup"><span data-stu-id="141dd-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="141dd-170">You can use this tool to troubleshoot your Azure Storage issues.</span><span class="sxs-lookup"><span data-stu-id="141dd-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

