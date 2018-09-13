---
title: Connect Raspberry Pi (C) to Azure IoT - Troubleshoot | Microsoft Docs
description: Troubleshooting page for the Raspberry Pi Node.js experience
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: iot issues, internet of things problems
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b69d2780be3f96d3e491a7735239d60b50a1e0f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563219"
---
# <a name="troubleshooting"></a><span data-ttu-id="e1ddb-104">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="e1ddb-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="e1ddb-105">Hardware issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="e1ddb-106">The application runs well but the LED is not blinking</span><span class="sxs-lookup"><span data-stu-id="e1ddb-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="e1ddb-107">This issue is always related to hardware circuit connectivity.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="e1ddb-108">Use the following steps to identify problems:</span><span class="sxs-lookup"><span data-stu-id="e1ddb-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="e1ddb-109">Check that you chose the correct **GPIO** on your board.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="e1ddb-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="e1ddb-111">Check that the polarity of your LED is correct.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="e1ddb-112">The longer leg should indicate the **positive**, anode pin.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="e1ddb-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="e1ddb-114">Treat Pi as the DC power.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="e1ddb-115">Check that the LED works fine.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-115">Check that the LED works fine.</span></span>

![LED specification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="e1ddb-117">Other hardware issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-117">Other hardware issues</span></span>
<span data-ttu-id="e1ddb-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="e1ddb-119">Node.js package issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="e1ddb-120">No response during gulp tasks</span><span class="sxs-lookup"><span data-stu-id="e1ddb-120">No response during gulp tasks</span></span>
<span data-ttu-id="e1ddb-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="e1ddb-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="e1ddb-123">You might see detailed error messages in your console output.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="e1ddb-124">Device discovery issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-124">Device discovery issues</span></span>
<span data-ttu-id="e1ddb-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="e1ddb-126">npm issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-126">npm issues</span></span>
<span data-ttu-id="e1ddb-127">Try to update your npm package by using the following command:</span><span class="sxs-lookup"><span data-stu-id="e1ddb-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="e1ddb-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="e1ddb-129">Remote debugging</span><span class="sxs-lookup"><span data-stu-id="e1ddb-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="e1ddb-130">Run the sample application in debug mode</span><span class="sxs-lookup"><span data-stu-id="e1ddb-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="e1ddb-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="e1ddb-132">Configure Visual Studio Code to connect to the remote device</span><span class="sxs-lookup"><span data-stu-id="e1ddb-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="e1ddb-133">Open the **Debug** panel on the left side.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="e1ddb-134">Click the green **Start Debugging** (F5) button.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="e1ddb-135">Visual Studio Code opens a launch.json file.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="e1ddb-136">Update the launch.json file with the following content.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="e1ddb-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ddb-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Remote debugging configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="e1ddb-140">Attach to the remote application</span><span class="sxs-lookup"><span data-stu-id="e1ddb-140">Attach to the remote application</span></span>
<span data-ttu-id="e1ddb-141">Click the green **Start Debugging** (F5) button to start debugging.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="e1ddb-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Remote debugging interactive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="e1ddb-144">Azure CLI issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-144">Azure CLI issues</span></span>
<span data-ttu-id="e1ddb-145">The Azure command-line interface (Azure CLI) is a preview build.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="e1ddb-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="e1ddb-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="e1ddb-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="e1ddb-149">Python installation issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="e1ddb-150">Legacy installation issues (macOS)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="e1ddb-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="e1ddb-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="e1ddb-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="e1ddb-154">The solution is to remove those packages installed by root.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="e1ddb-155">Use the following steps to complete this task:</span><span class="sxs-lookup"><span data-stu-id="e1ddb-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="e1ddb-156">Go to: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="e1ddb-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="e1ddb-157">List packages created by root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="e1ddb-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="e1ddb-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="e1ddb-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="e1ddb-159">Reinstall Python.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="e1ddb-160">Azure IoT Hub issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="e1ddb-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="e1ddb-162">Device explorer</span><span class="sxs-lookup"><span data-stu-id="e1ddb-162">Device explorer</span></span>
<span data-ttu-id="e1ddb-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="e1ddb-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="e1ddb-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="e1ddb-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="e1ddb-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="e1ddb-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="e1ddb-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="e1ddb-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="e1ddb-169">iothub-explorer</span></span>
<span data-ttu-id="e1ddb-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="e1ddb-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="e1ddb-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="e1ddb-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="e1ddb-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span><span class="sxs-lookup"><span data-stu-id="e1ddb-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="e1ddb-174">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e1ddb-174">Azure portal</span></span>
<span data-ttu-id="e1ddb-175">A full CLI experience helps you create and manage all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="e1ddb-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="e1ddb-177">Azure Storage issues</span><span class="sxs-lookup"><span data-stu-id="e1ddb-177">Azure Storage issues</span></span>
<span data-ttu-id="e1ddb-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="e1ddb-179">By using this tool, you can connect to your table and see the data in it.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="e1ddb-180">You can use this tool to troubleshoot your Azure Storage issues.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>




