---
title: 'SensorTag device & Azure IoT Gateway - Lesson 2: Get tools (Windows) | Microsoft Docs'
description: Install the tools and the software on your host computer running Windows, create an IoT hub and register your device in the IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot development, iot software, iot cloud service, internet of things software, azure cli, install git on windows, gulp run, install node js windows, install npm on windows, install python on windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ae5fe8badd1a4875e959bf803d12d8b961eeb601
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550458"
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="200e9-104">Get the tools (Windows 7 and later)</span><span class="sxs-lookup"><span data-stu-id="200e9-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="200e9-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="200e9-108">What you will do</span></span>

- <span data-ttu-id="200e9-109">Install Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="200e9-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="200e9-110">Install the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="200e9-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="200e9-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="200e9-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="200e9-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="200e9-112">What you will learn</span></span>

<span data-ttu-id="200e9-113">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="200e9-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="200e9-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="200e9-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="200e9-115">Git is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="200e9-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="200e9-116">The sample application for this lesson is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="200e9-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="200e9-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="200e9-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="200e9-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="200e9-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="200e9-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="200e9-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="200e9-120">NPM is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="200e9-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="200e9-121">How to install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="200e9-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="200e9-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="200e9-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="200e9-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span><span class="sxs-lookup"><span data-stu-id="200e9-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="200e9-124">How to install Python.</span><span class="sxs-lookup"><span data-stu-id="200e9-124">How to install Python.</span></span>
  - <span data-ttu-id="200e9-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span><span class="sxs-lookup"><span data-stu-id="200e9-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="200e9-126">How to install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="200e9-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="200e9-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span><span class="sxs-lookup"><span data-stu-id="200e9-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="200e9-128">You work directly from a command line to provision and manage resources.</span><span class="sxs-lookup"><span data-stu-id="200e9-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="200e9-129">How to use the Azure CLI to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="200e9-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="200e9-130">What you need</span><span class="sxs-lookup"><span data-stu-id="200e9-130">What you need</span></span>

- <span data-ttu-id="200e9-131">An Internet connection to download the tools and software.</span><span class="sxs-lookup"><span data-stu-id="200e9-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="200e9-132">A Windows computer.</span><span class="sxs-lookup"><span data-stu-id="200e9-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="200e9-133">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="200e9-133">Install Git and Node.js</span></span>

<span data-ttu-id="200e9-134">Click the following links to download and install Git and Node.js LTS for Windows.</span><span class="sxs-lookup"><span data-stu-id="200e9-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="200e9-135">Get Git for Windows</span><span class="sxs-lookup"><span data-stu-id="200e9-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="200e9-136">Get Node.js LTS for Windows</span><span class="sxs-lookup"><span data-stu-id="200e9-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="200e9-137">Install Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="200e9-137">Install Node.js development tools</span></span>

<span data-ttu-id="200e9-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span><span class="sxs-lookup"><span data-stu-id="200e9-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="200e9-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="200e9-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="200e9-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="200e9-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> Node, NPM and Gulp are required to run automation scripts developed in Node.js.

## <a name="install-python"></a><span data-ttu-id="200e9-142">Install Python</span><span class="sxs-lookup"><span data-stu-id="200e9-142">Install Python</span></span>

<span data-ttu-id="200e9-143">You can choose from Python 2.7, 3.4 or 3.5.</span><span class="sxs-lookup"><span data-stu-id="200e9-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="200e9-144">In this tutorial, we use Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="200e9-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="200e9-145">If you've already installed python, go to the next section.</span><span class="sxs-lookup"><span data-stu-id="200e9-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="200e9-146">Get Python for Windows</span><span class="sxs-lookup"><span data-stu-id="200e9-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="200e9-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span><span class="sxs-lookup"><span data-stu-id="200e9-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="200e9-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="200e9-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="200e9-149">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="200e9-149">Install the Azure CLI</span></span>

<span data-ttu-id="200e9-150">To install the Azure CLI, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="200e9-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="200e9-151">Open a Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="200e9-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="200e9-152">Install the Azure CLI by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="200e9-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="200e9-153">The installation might take 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="200e9-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="200e9-154">Verify the installation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="200e9-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="200e9-155">You should see the following output if the installation is successful.</span><span class="sxs-lookup"><span data-stu-id="200e9-155">You should see the following output if the installation is successful.</span></span>

   ![Verify Azure CLI installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="200e9-157">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="200e9-157">Install Visual Studio Code</span></span>

<span data-ttu-id="200e9-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span><span class="sxs-lookup"><span data-stu-id="200e9-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="200e9-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="200e9-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="200e9-160">Summary</span><span class="sxs-lookup"><span data-stu-id="200e9-160">Summary</span></span>

<span data-ttu-id="200e9-161">You've installed all the required tools and software on your host computer.</span><span class="sxs-lookup"><span data-stu-id="200e9-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="200e9-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="200e9-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="200e9-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="200e9-163">Next steps</span></span>
[<span data-ttu-id="200e9-164">Create an IoT hub and register your device</span><span class="sxs-lookup"><span data-stu-id="200e9-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

