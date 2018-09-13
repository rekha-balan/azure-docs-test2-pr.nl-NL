---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 1: Get tools (macOS) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Pi on macOS.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot development, iot software, internet of things software, install git on mac, gulp run, install node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563620"
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="85362-104">Get the tools (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="85362-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="85362-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="85362-108">What you will do</span></span>
<span data-ttu-id="85362-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="85362-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="85362-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="85362-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.

## <a name="what-you-will-learn"></a><span data-ttu-id="85362-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="85362-112">What you will learn</span></span>
<span data-ttu-id="85362-113">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="85362-113">In this article, you will learn:</span></span>

* <span data-ttu-id="85362-114">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="85362-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="85362-115">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="85362-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="85362-116">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="85362-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="85362-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="85362-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="85362-118">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="85362-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="85362-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="85362-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="85362-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="85362-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="85362-121">What you need</span><span class="sxs-lookup"><span data-stu-id="85362-121">What you need</span></span>
<span data-ttu-id="85362-122">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="85362-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="85362-123">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="85362-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="85362-124">A Mac that is running macOS Yosemite (10.10) or later.</span><span class="sxs-lookup"><span data-stu-id="85362-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="85362-125">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="85362-125">Install Git and Node.js</span></span>
<span data-ttu-id="85362-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span><span class="sxs-lookup"><span data-stu-id="85362-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="85362-127">Install Homebrew.</span><span class="sxs-lookup"><span data-stu-id="85362-127">Install Homebrew.</span></span> <span data-ttu-id="85362-128">If you've already installed Homebrew, go to step 2.</span><span class="sxs-lookup"><span data-stu-id="85362-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="85362-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span><span class="sxs-lookup"><span data-stu-id="85362-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="85362-130">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="85362-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="85362-131">Install Git and Node.js by running the following command:</span><span class="sxs-lookup"><span data-stu-id="85362-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="85362-132">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="85362-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="85362-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span><span class="sxs-lookup"><span data-stu-id="85362-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="85362-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="85362-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="85362-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="85362-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="85362-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="85362-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="85362-137">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="85362-137">Install Visual Studio Code</span></span>
<span data-ttu-id="85362-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="85362-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="85362-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="85362-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="85362-140">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="85362-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="85362-141">Summary</span><span class="sxs-lookup"><span data-stu-id="85362-141">Summary</span></span>
<span data-ttu-id="85362-142">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="85362-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="85362-143">The next task is to create, deploy, and run the sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="85362-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85362-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="85362-144">Next steps</span></span>
[<span data-ttu-id="85362-145">Create and deploy the blink application</span><span class="sxs-lookup"><span data-stu-id="85362-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

