---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 4: Troubleshooting | Microsoft Docs'
description: Troubleshooting page for Intel Edison Node.js experience
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino troubleshooting
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bfd4f2d5d4ca123851fa0deed647b87c2dd30c10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556411"
---
# <a name="troubleshooting"></a><span data-ttu-id="3089a-104">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="3089a-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="3089a-105">Hardware issues</span><span class="sxs-lookup"><span data-stu-id="3089a-105">Hardware issues</span></span>
<span data-ttu-id="3089a-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="3089a-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="3089a-107">Node.js package issues</span><span class="sxs-lookup"><span data-stu-id="3089a-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="3089a-108">No response during gulp tasks</span><span class="sxs-lookup"><span data-stu-id="3089a-108">No response during gulp tasks</span></span>
<span data-ttu-id="3089a-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span><span class="sxs-lookup"><span data-stu-id="3089a-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="3089a-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span><span class="sxs-lookup"><span data-stu-id="3089a-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="3089a-111">You might see detailed error messages in your console output.</span><span class="sxs-lookup"><span data-stu-id="3089a-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="3089a-112">NPM issues</span><span class="sxs-lookup"><span data-stu-id="3089a-112">NPM issues</span></span>
<span data-ttu-id="3089a-113">Try to update your NPM package with the following command:</span><span class="sxs-lookup"><span data-stu-id="3089a-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="3089a-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="3089a-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="3089a-115">Remote debugging</span><span class="sxs-lookup"><span data-stu-id="3089a-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="3089a-116">Run the sample application in debug mode</span><span class="sxs-lookup"><span data-stu-id="3089a-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="3089a-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span><span class="sxs-lookup"><span data-stu-id="3089a-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="3089a-118">Configure VS Code to connect to the remote device</span><span class="sxs-lookup"><span data-stu-id="3089a-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="3089a-119">Open the **Debug** panel from the left side.</span><span class="sxs-lookup"><span data-stu-id="3089a-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="3089a-120">Click the green **Start Debugging** (F5) button.</span><span class="sxs-lookup"><span data-stu-id="3089a-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="3089a-121">VS Code would open a **launch.json** file, which you need to update.</span><span class="sxs-lookup"><span data-stu-id="3089a-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="3089a-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span><span class="sxs-lookup"><span data-stu-id="3089a-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

![Remote debugging configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="3089a-124">Attach to the remote application</span><span class="sxs-lookup"><span data-stu-id="3089a-124">Attach to the remote application</span></span>

<span data-ttu-id="3089a-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span><span class="sxs-lookup"><span data-stu-id="3089a-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="3089a-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span><span class="sxs-lookup"><span data-stu-id="3089a-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Remote debugging interactive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="3089a-128">Azure-CLI issues</span><span class="sxs-lookup"><span data-stu-id="3089a-128">Azure-CLI issues</span></span>
<span data-ttu-id="3089a-129">The Azure command-line interface (Azure CLI) is a preview build.</span><span class="sxs-lookup"><span data-stu-id="3089a-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="3089a-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span><span class="sxs-lookup"><span data-stu-id="3089a-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="3089a-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span><span class="sxs-lookup"><span data-stu-id="3089a-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="3089a-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="3089a-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="3089a-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="3089a-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="3089a-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span><span class="sxs-lookup"><span data-stu-id="3089a-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="3089a-135">Python installation issues</span><span class="sxs-lookup"><span data-stu-id="3089a-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="3089a-136">Legacy installation issues (macOS)</span><span class="sxs-lookup"><span data-stu-id="3089a-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="3089a-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span><span class="sxs-lookup"><span data-stu-id="3089a-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="3089a-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span><span class="sxs-lookup"><span data-stu-id="3089a-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="3089a-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span><span class="sxs-lookup"><span data-stu-id="3089a-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="3089a-140">The solution is to remove those packages installed by root.</span><span class="sxs-lookup"><span data-stu-id="3089a-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="3089a-141">Use the following steps to complete this task:</span><span class="sxs-lookup"><span data-stu-id="3089a-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="3089a-142">Go to: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="3089a-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="3089a-143">List packages create by root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="3089a-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="3089a-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="3089a-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="3089a-145">Reinstall Python.</span><span class="sxs-lookup"><span data-stu-id="3089a-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="3089a-146">Azure IoT Hub issues</span><span class="sxs-lookup"><span data-stu-id="3089a-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="3089a-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span><span class="sxs-lookup"><span data-stu-id="3089a-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="3089a-148">Device Explorer</span><span class="sxs-lookup"><span data-stu-id="3089a-148">Device Explorer</span></span>
<span data-ttu-id="3089a-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="3089a-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="3089a-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="3089a-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="3089a-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3089a-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="3089a-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3089a-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="3089a-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3089a-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="3089a-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span><span class="sxs-lookup"><span data-stu-id="3089a-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="3089a-155">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="3089a-155">IoT hub Explorer</span></span>
<span data-ttu-id="3089a-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span><span class="sxs-lookup"><span data-stu-id="3089a-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="3089a-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span><span class="sxs-lookup"><span data-stu-id="3089a-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="3089a-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="3089a-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="3089a-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span><span class="sxs-lookup"><span data-stu-id="3089a-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="3089a-160">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3089a-160">Azure portal</span></span>
<span data-ttu-id="3089a-161">A full CLI experience helps you create and manage all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3089a-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="3089a-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3089a-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="3089a-163">Azure storage issues</span><span class="sxs-lookup"><span data-stu-id="3089a-163">Azure storage issues</span></span>
<span data-ttu-id="3089a-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="3089a-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="3089a-165">By using this tool, you can connect to your table and see the data in it.</span><span class="sxs-lookup"><span data-stu-id="3089a-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="3089a-166">You can use this tool to troubleshoot your Azure Storage issues.</span><span class="sxs-lookup"><span data-stu-id="3089a-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3089a-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="3089a-167">Next steps</span></span>
<span data-ttu-id="3089a-168">This page only includes the most common problems of Intel Edison kit.</span><span class="sxs-lookup"><span data-stu-id="3089a-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="3089a-169">You can also leave bottom comments to report issues for further troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="3089a-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="3089a-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3089a-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started

