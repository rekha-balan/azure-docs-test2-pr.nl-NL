---
title: 'Simulated device & Azure IoT Gateway - Lesson 2: Get tools (Ubuntu) | Microsoft Docs'
description: Install the tools and the software on your host computer running Ubuntu, create an IoT hub and register your device in the IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot development, iot software, iot cloud service, internet of things software, azure cli, install git on ubuntu, gulp run, install node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f9dc1ac8203262446b2321da91382b023adea79
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551098"
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="c8c71-104">Get the tools (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="c8c71-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="c8c71-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="c8c71-108">What you will do</span></span>

- <span data-ttu-id="c8c71-109">Install Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="c8c71-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="c8c71-110">Install the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="c8c71-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="c8c71-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c8c71-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="c8c71-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="c8c71-112">What you will learn</span></span>

<span data-ttu-id="c8c71-113">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="c8c71-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="c8c71-114">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="c8c71-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="c8c71-115">Git is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="c8c71-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="c8c71-116">The sample application for this lesson is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="c8c71-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="c8c71-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="c8c71-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="c8c71-118">How to use NPM to install Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="c8c71-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="c8c71-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="c8c71-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="c8c71-120">NPM is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="c8c71-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="c8c71-121">How to install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c8c71-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="c8c71-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="c8c71-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c8c71-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span><span class="sxs-lookup"><span data-stu-id="c8c71-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="c8c71-124">How to install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c8c71-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="c8c71-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c71-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="c8c71-126">You work directly from a command line to provision and manage resources.</span><span class="sxs-lookup"><span data-stu-id="c8c71-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="c8c71-127">How to use the Azure CLI to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c8c71-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c8c71-128">What you need</span><span class="sxs-lookup"><span data-stu-id="c8c71-128">What you need</span></span>

- <span data-ttu-id="c8c71-129">An Internet connection to download the tools and software.</span><span class="sxs-lookup"><span data-stu-id="c8c71-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="c8c71-130">A computer that is running Ubuntu 16.04 or later.</span><span class="sxs-lookup"><span data-stu-id="c8c71-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="c8c71-131">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="c8c71-131">Install Git and Node.js</span></span>

<span data-ttu-id="c8c71-132">To install Git and Node.js, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="c8c71-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="c8c71-133">Press `Ctrl + Alt + T` to open a terminal.</span><span class="sxs-lookup"><span data-stu-id="c8c71-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="c8c71-134">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="c8c71-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="c8c71-135">Install Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="c8c71-135">Install Node.js development tools</span></span>

<span data-ttu-id="c8c71-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span><span class="sxs-lookup"><span data-stu-id="c8c71-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="c8c71-137">To install gulp, run the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="c8c71-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="c8c71-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="c8c71-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> Node, NPM and Gulp are required to run automation scripts developed in Node.js.

## <a name="install-the-azure-cli"></a><span data-ttu-id="c8c71-140">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c8c71-140">Install the Azure CLI</span></span>

<span data-ttu-id="c8c71-141">To install the Azure CLI, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="c8c71-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="c8c71-142">Run the following commands in the terminal:</span><span class="sxs-lookup"><span data-stu-id="c8c71-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="c8c71-143">The installation might take 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="c8c71-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="c8c71-144">Verify the installation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="c8c71-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="c8c71-145">You should see the following output if the installation is successful.</span><span class="sxs-lookup"><span data-stu-id="c8c71-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="c8c71-146">![Verify Azure CLI installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="c8c71-146">![Verify Azure CLI installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="c8c71-147">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c8c71-147">Install Visual Studio Code</span></span>

<span data-ttu-id="c8c71-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span><span class="sxs-lookup"><span data-stu-id="c8c71-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="c8c71-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c8c71-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="c8c71-150">Summary</span><span class="sxs-lookup"><span data-stu-id="c8c71-150">Summary</span></span>

<span data-ttu-id="c8c71-151">You've installed all the required tools and software on your host computer.</span><span class="sxs-lookup"><span data-stu-id="c8c71-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="c8c71-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c8c71-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8c71-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8c71-153">Next steps</span></span>
[<span data-ttu-id="c8c71-154">Create an IoT hub and register your device</span><span class="sxs-lookup"><span data-stu-id="c8c71-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

