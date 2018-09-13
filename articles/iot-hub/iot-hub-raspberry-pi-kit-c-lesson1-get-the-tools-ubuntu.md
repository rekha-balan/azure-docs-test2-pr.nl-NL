---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 1: Get tools (Ubuntu) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Pi on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot development, iot software, internet of things software, install git on ubuntu, gulp run, install node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556586"
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="63c7a-104">Get the tools (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="63c7a-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="63c7a-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="63c7a-108">What you will do</span></span>
<span data-ttu-id="63c7a-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="63c7a-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="63c7a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="63c7a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.

## <a name="what-you-will-learn"></a><span data-ttu-id="63c7a-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="63c7a-112">What you will learn</span></span>
<span data-ttu-id="63c7a-113">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="63c7a-113">In this article, you will learn:</span></span>

* <span data-ttu-id="63c7a-114">How to install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="63c7a-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="63c7a-115">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="63c7a-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="63c7a-116">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="63c7a-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="63c7a-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="63c7a-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="63c7a-118">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="63c7a-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="63c7a-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="63c7a-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="63c7a-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="63c7a-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="63c7a-121">What you need</span><span class="sxs-lookup"><span data-stu-id="63c7a-121">What you need</span></span>
<span data-ttu-id="63c7a-122">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="63c7a-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="63c7a-123">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="63c7a-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="63c7a-124">A computer that is running Ubuntu 16.04 or later.</span><span class="sxs-lookup"><span data-stu-id="63c7a-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="63c7a-125">Install Git, Node.js, and NPM</span><span class="sxs-lookup"><span data-stu-id="63c7a-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="63c7a-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="63c7a-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="63c7a-127">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="63c7a-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="63c7a-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span><span class="sxs-lookup"><span data-stu-id="63c7a-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="63c7a-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="63c7a-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="63c7a-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="63c7a-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="63c7a-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="63c7a-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="63c7a-132">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="63c7a-132">Install Visual Studio Code</span></span>
<span data-ttu-id="63c7a-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="63c7a-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="63c7a-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="63c7a-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="63c7a-135">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="63c7a-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="63c7a-136">Summary</span><span class="sxs-lookup"><span data-stu-id="63c7a-136">Summary</span></span>
<span data-ttu-id="63c7a-137">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="63c7a-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="63c7a-138">The next task is to create, deploy, and run the sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="63c7a-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63c7a-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="63c7a-139">Next steps</span></span>
[<span data-ttu-id="63c7a-140">Create and deploy the blink application</span><span class="sxs-lookup"><span data-stu-id="63c7a-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

