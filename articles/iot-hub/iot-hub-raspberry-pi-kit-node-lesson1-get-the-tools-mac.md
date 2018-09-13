---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 1: Get tools (macOS) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Pi on macOS.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: iot development, iot software, internet of things software, install python mac, install git on mac, gulp run, install node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551329"
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="06703-104">Get the tools (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="06703-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="06703-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="06703-108">What you will do</span></span>
<span data-ttu-id="06703-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="06703-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="06703-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="06703-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="06703-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="06703-111">What you will learn</span></span>
<span data-ttu-id="06703-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="06703-112">In this article, you will learn:</span></span>

* <span data-ttu-id="06703-113">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="06703-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="06703-114">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="06703-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="06703-115">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="06703-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="06703-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="06703-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="06703-117">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="06703-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="06703-118">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="06703-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="06703-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="06703-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="06703-120">What you need</span><span class="sxs-lookup"><span data-stu-id="06703-120">What you need</span></span>
<span data-ttu-id="06703-121">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="06703-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="06703-122">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="06703-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="06703-123">A Mac that is running macOS Yosemite (10.10) or later.</span><span class="sxs-lookup"><span data-stu-id="06703-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="06703-124">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="06703-124">Install Git and Node.js</span></span>
<span data-ttu-id="06703-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span><span class="sxs-lookup"><span data-stu-id="06703-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="06703-126">Install Homebrew.</span><span class="sxs-lookup"><span data-stu-id="06703-126">Install Homebrew.</span></span> <span data-ttu-id="06703-127">If you've already installed Homebrew, go to step 2.</span><span class="sxs-lookup"><span data-stu-id="06703-127">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="06703-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span><span class="sxs-lookup"><span data-stu-id="06703-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="06703-129">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="06703-129">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="06703-130">Install Git and Node.js by running the following command:</span><span class="sxs-lookup"><span data-stu-id="06703-130">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="06703-131">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="06703-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="06703-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span><span class="sxs-lookup"><span data-stu-id="06703-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="06703-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="06703-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="06703-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="06703-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="06703-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="06703-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="06703-136">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="06703-136">Install Visual Studio Code</span></span>
<span data-ttu-id="06703-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="06703-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="06703-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="06703-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="06703-139">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="06703-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="06703-140">Summary</span><span class="sxs-lookup"><span data-stu-id="06703-140">Summary</span></span>
<span data-ttu-id="06703-141">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="06703-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="06703-142">The next task is to create, deploy, and run the sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="06703-142">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06703-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="06703-143">Next steps</span></span>
[<span data-ttu-id="06703-144">Create and deploy the blink sample application</span><span class="sxs-lookup"><span data-stu-id="06703-144">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

