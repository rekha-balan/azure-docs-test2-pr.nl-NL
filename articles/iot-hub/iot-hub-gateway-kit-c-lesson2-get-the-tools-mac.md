---
title: 'SensorTag device & Azure IoT Gateway - Lesson 2: Get tools (macOS) | Microsoft Docs'
description: Install tools on your Mac computer, create an IoT hub and register your device in the IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot development, iot software, iot cloud service, internet of things software, azure cli, install python mac, install git on mac, gulp run, install node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: daa384a30b870506184fa30a817b748d8b121fa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564150"
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="34f66-104">Get the tools (MacOS)</span><span class="sxs-lookup"><span data-stu-id="34f66-104">Get the tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="34f66-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="34f66-108">What you will do</span></span>

- <span data-ttu-id="34f66-109">Install Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="34f66-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="34f66-110">Install the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="34f66-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="34f66-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="34f66-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="34f66-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="34f66-112">What you will learn</span></span>

<span data-ttu-id="34f66-113">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="34f66-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="34f66-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="34f66-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="34f66-115">Git is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="34f66-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="34f66-116">The sample application for this lesson is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="34f66-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="34f66-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="34f66-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="34f66-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="34f66-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="34f66-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="34f66-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="34f66-120">NPM is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="34f66-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="34f66-121">How to install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="34f66-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="34f66-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="34f66-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="34f66-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span><span class="sxs-lookup"><span data-stu-id="34f66-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="34f66-124">How to install Python.</span><span class="sxs-lookup"><span data-stu-id="34f66-124">How to install Python.</span></span>
  - <span data-ttu-id="34f66-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span><span class="sxs-lookup"><span data-stu-id="34f66-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="34f66-126">How to install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="34f66-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="34f66-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span><span class="sxs-lookup"><span data-stu-id="34f66-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="34f66-128">You work directly from a command line to provision and manage resources.</span><span class="sxs-lookup"><span data-stu-id="34f66-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="34f66-129">How to use the Azure CLI to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="34f66-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="34f66-130">What you need</span><span class="sxs-lookup"><span data-stu-id="34f66-130">What you need</span></span>

- <span data-ttu-id="34f66-131">An Internet connection to download the tools and software.</span><span class="sxs-lookup"><span data-stu-id="34f66-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="34f66-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span><span class="sxs-lookup"><span data-stu-id="34f66-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="34f66-133">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="34f66-133">Install Git and Node.js</span></span>

<span data-ttu-id="34f66-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span><span class="sxs-lookup"><span data-stu-id="34f66-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="34f66-135">[Download](http://brew.sh/) and install Homebrew.</span><span class="sxs-lookup"><span data-stu-id="34f66-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="34f66-136">If you’ve already installed Homebrew, go to step 2.</span><span class="sxs-lookup"><span data-stu-id="34f66-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="34f66-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span><span class="sxs-lookup"><span data-stu-id="34f66-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="34f66-138">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="34f66-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="34f66-139">Install Git and Node.js by running the following command:</span><span class="sxs-lookup"><span data-stu-id="34f66-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="34f66-140">Install Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="34f66-140">Install Node.js development tools</span></span>

<span data-ttu-id="34f66-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span><span class="sxs-lookup"><span data-stu-id="34f66-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="34f66-142">To install gulp, run the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="34f66-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="34f66-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="34f66-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> Node, NPM and Gulp are required to run automation scripts developed in Node.js.

## <a name="install-python"></a><span data-ttu-id="34f66-145">Install Python</span><span class="sxs-lookup"><span data-stu-id="34f66-145">Install Python</span></span>

<span data-ttu-id="34f66-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span><span class="sxs-lookup"><span data-stu-id="34f66-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="34f66-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="34f66-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="34f66-148">Install Python and pip by running the following command:</span><span class="sxs-lookup"><span data-stu-id="34f66-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="34f66-149">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34f66-149">Install the Azure CLI</span></span>

<span data-ttu-id="34f66-150">To install the Azure CLI, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="34f66-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="34f66-151">Run the following commands in the terminal:</span><span class="sxs-lookup"><span data-stu-id="34f66-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="34f66-152">The installation might take 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="34f66-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="34f66-153">Verify the installation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="34f66-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="34f66-154">You should see the following output if the installation is successful.</span><span class="sxs-lookup"><span data-stu-id="34f66-154">You should see the following output if the installation is successful.</span></span>

   ![Verify Azure CLI installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="34f66-156">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="34f66-156">Install Visual Studio Code</span></span>

<span data-ttu-id="34f66-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span><span class="sxs-lookup"><span data-stu-id="34f66-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="34f66-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="34f66-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="34f66-159">Summary</span><span class="sxs-lookup"><span data-stu-id="34f66-159">Summary</span></span>

<span data-ttu-id="34f66-160">You’ve installed all the required tools and software on your Mac computer.</span><span class="sxs-lookup"><span data-stu-id="34f66-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="34f66-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="34f66-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34f66-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="34f66-162">Next steps</span></span>
[<span data-ttu-id="34f66-163">Create an IoT hub and register Device</span><span class="sxs-lookup"><span data-stu-id="34f66-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

