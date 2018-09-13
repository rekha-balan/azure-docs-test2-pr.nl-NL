---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 1: Get tools (Ubuntu) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Pi on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: iot development, iot software, internet of things software, install git on ubuntu, gulp run, install node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de583be0cdce058c83091f421376812e8013d76e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554880"
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="337aa-104">Get the tools (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="337aa-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="337aa-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="337aa-108">What you will do</span></span>
<span data-ttu-id="337aa-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="337aa-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="337aa-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="337aa-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="337aa-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="337aa-111">What you will learn</span></span>
<span data-ttu-id="337aa-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="337aa-112">In this article, you will learn:</span></span>

* <span data-ttu-id="337aa-113">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="337aa-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="337aa-114">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="337aa-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="337aa-115">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="337aa-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="337aa-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="337aa-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="337aa-117">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="337aa-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="337aa-118">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="337aa-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="337aa-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="337aa-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="337aa-120">What do you need</span><span class="sxs-lookup"><span data-stu-id="337aa-120">What do you need</span></span>
<span data-ttu-id="337aa-121">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="337aa-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="337aa-122">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="337aa-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="337aa-123">A computer that is running Ubuntu 16.04 or later.</span><span class="sxs-lookup"><span data-stu-id="337aa-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="337aa-124">Install Git, Node.js, and NPM</span><span class="sxs-lookup"><span data-stu-id="337aa-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="337aa-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="337aa-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="337aa-126">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="337aa-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="337aa-127">You use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span><span class="sxs-lookup"><span data-stu-id="337aa-127">You use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="337aa-128">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="337aa-128">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="337aa-129">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="337aa-129">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="337aa-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="337aa-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="337aa-131">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="337aa-131">Install Visual Studio Code</span></span>
<span data-ttu-id="337aa-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="337aa-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="337aa-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="337aa-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="337aa-134">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="337aa-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="337aa-135">Summary</span><span class="sxs-lookup"><span data-stu-id="337aa-135">Summary</span></span>
<span data-ttu-id="337aa-136">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="337aa-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="337aa-137">The next task is to create, deploy, and run the sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="337aa-137">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="337aa-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="337aa-138">Next steps</span></span>
[<span data-ttu-id="337aa-139">Create and deploy the blink sample application</span><span class="sxs-lookup"><span data-stu-id="337aa-139">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

