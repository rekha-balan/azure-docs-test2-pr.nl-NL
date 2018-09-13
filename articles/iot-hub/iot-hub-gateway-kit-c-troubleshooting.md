---
title: SensorTag device & Azure IoT Gateway - Troubleshooting | Microsoft Docs
description: Troubleshooting page for Intel NUC gateway
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot issues, internet of things problems
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c91121bf3aa5732cd93b8a2d81e3c3627ae31e25
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661899"
---
# <a name="troubleshooting"></a><span data-ttu-id="56ff4-104">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="56ff4-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="56ff4-105">Hardware issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="56ff4-106">TI SensorTag cannot be connected</span><span class="sxs-lookup"><span data-stu-id="56ff4-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="56ff4-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="56ff4-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="56ff4-108">Have an issue with Intel NUC</span><span class="sxs-lookup"><span data-stu-id="56ff4-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="56ff4-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="56ff4-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="56ff4-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="56ff4-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="56ff4-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="56ff4-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="56ff4-112">Node.js package issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="56ff4-113">No response during gulp tasks</span><span class="sxs-lookup"><span data-stu-id="56ff4-113">No response during gulp tasks</span></span>

<span data-ttu-id="56ff4-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span><span class="sxs-lookup"><span data-stu-id="56ff4-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="56ff4-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span><span class="sxs-lookup"><span data-stu-id="56ff4-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="56ff4-116">You might see detailed error messages in your console output.</span><span class="sxs-lookup"><span data-stu-id="56ff4-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="56ff4-117">Device discovery issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-117">Device discovery issues</span></span>

<span data-ttu-id="56ff4-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="56ff4-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="56ff4-119">npm issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-119">npm issues</span></span>

<span data-ttu-id="56ff4-120">Try to update your npm package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="56ff4-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="56ff4-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="56ff4-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="56ff4-122">Remote Debugging</span><span class="sxs-lookup"><span data-stu-id="56ff4-122">Remote Debugging</span></span>
> <span data-ttu-id="56ff4-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="56ff4-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="56ff4-124">Run the sample application in debug mode</span><span class="sxs-lookup"><span data-stu-id="56ff4-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="56ff4-125">Run the sample application in debug mode by running the following command:</span><span class="sxs-lookup"><span data-stu-id="56ff4-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="56ff4-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span><span class="sxs-lookup"><span data-stu-id="56ff4-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="56ff4-127">Configure Visual Studio Code to connect to the remote device</span><span class="sxs-lookup"><span data-stu-id="56ff4-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="56ff4-128">Open the **Debug** panel on the left side.</span><span class="sxs-lookup"><span data-stu-id="56ff4-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="56ff4-129">Click the green **Start Debugging** (F5) button.</span><span class="sxs-lookup"><span data-stu-id="56ff4-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="56ff4-130">Visual Studio Code opens a `launch.json` file.</span><span class="sxs-lookup"><span data-stu-id="56ff4-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="56ff4-131">Update the `launch.json` file with the following content.</span><span class="sxs-lookup"><span data-stu-id="56ff4-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="56ff4-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span><span class="sxs-lookup"><span data-stu-id="56ff4-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Remote Debugging Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="56ff4-134">Attach to the remote application</span><span class="sxs-lookup"><span data-stu-id="56ff4-134">Attach to the remote application</span></span>

<span data-ttu-id="56ff4-135">Click the green **Start Debugging** (F5) button to start debugging.</span><span class="sxs-lookup"><span data-stu-id="56ff4-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="56ff4-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span><span class="sxs-lookup"><span data-stu-id="56ff4-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Debugging BLE Sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="56ff4-138">Azure CLI issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-138">Azure CLI issues</span></span>

<span data-ttu-id="56ff4-139">The Azure command-line interface (Azure CLI) is a preview build.</span><span class="sxs-lookup"><span data-stu-id="56ff4-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="56ff4-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="56ff4-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="56ff4-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="56ff4-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="56ff4-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="56ff4-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="56ff4-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span><span class="sxs-lookup"><span data-stu-id="56ff4-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="56ff4-144">Python installation issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="56ff4-145">Legacy installation issues (macOS)</span><span class="sxs-lookup"><span data-stu-id="56ff4-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="56ff4-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span><span class="sxs-lookup"><span data-stu-id="56ff4-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="56ff4-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span><span class="sxs-lookup"><span data-stu-id="56ff4-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="56ff4-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span><span class="sxs-lookup"><span data-stu-id="56ff4-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="56ff4-149">The solution is to remove those packages installed by root.</span><span class="sxs-lookup"><span data-stu-id="56ff4-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="56ff4-150">Use the following steps to complete this task:</span><span class="sxs-lookup"><span data-stu-id="56ff4-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="56ff4-151">Go to `/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="56ff4-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="56ff4-152">List packages created by root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="56ff4-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="56ff4-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="56ff4-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="56ff4-154">Reinstall Python.</span><span class="sxs-lookup"><span data-stu-id="56ff4-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="56ff4-155">Azure IoT Hub issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="56ff4-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span><span class="sxs-lookup"><span data-stu-id="56ff4-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="56ff4-157">Device Explorer</span><span class="sxs-lookup"><span data-stu-id="56ff4-157">Device Explorer</span></span>

<span data-ttu-id="56ff4-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="56ff4-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="56ff4-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="56ff4-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="56ff4-160">Device identity management to provision and manage devices registered with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56ff4-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="56ff4-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56ff4-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="56ff4-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56ff4-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="56ff4-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span><span class="sxs-lookup"><span data-stu-id="56ff4-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="56ff4-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="56ff4-164">iothub-explorer</span></span>

<span data-ttu-id="56ff4-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span><span class="sxs-lookup"><span data-stu-id="56ff4-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="56ff4-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span><span class="sxs-lookup"><span data-stu-id="56ff4-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="56ff4-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span><span class="sxs-lookup"><span data-stu-id="56ff4-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="56ff4-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span><span class="sxs-lookup"><span data-stu-id="56ff4-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="56ff4-169">The Azure portal</span><span class="sxs-lookup"><span data-stu-id="56ff4-169">The Azure portal</span></span>

<span data-ttu-id="56ff4-170">A full CLI experience helps you create and manage all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="56ff4-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="56ff4-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="56ff4-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="56ff4-172">Azure Storage issues</span><span class="sxs-lookup"><span data-stu-id="56ff4-172">Azure Storage issues</span></span>

<span data-ttu-id="56ff4-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="56ff4-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="56ff4-174">By using this tool, you can connect to your table and see the data in it.</span><span class="sxs-lookup"><span data-stu-id="56ff4-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="56ff4-175">You can use this tool to troubleshoot your Azure Storage issues.</span><span class="sxs-lookup"><span data-stu-id="56ff4-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>


