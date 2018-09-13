---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 1: Get tools (macOS) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Edison on macOS.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on mac, install node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661610"
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="56b04-104">Get the tools (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="56b04-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="56b04-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="56b04-108">What you will do</span></span>
<span data-ttu-id="56b04-109">Download the development tools and the software for the first sample application for your Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="56b04-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="56b04-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="56b04-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="56b04-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="56b04-111">What you will learn</span></span>
<span data-ttu-id="56b04-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="56b04-112">In this article, you will learn:</span></span>

* <span data-ttu-id="56b04-113">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="56b04-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="56b04-114">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="56b04-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="56b04-115">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="56b04-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="56b04-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="56b04-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="56b04-117">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="56b04-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="56b04-118">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="56b04-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="56b04-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="56b04-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="56b04-120">What you need</span><span class="sxs-lookup"><span data-stu-id="56b04-120">What you need</span></span>
<span data-ttu-id="56b04-121">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="56b04-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="56b04-122">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="56b04-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="56b04-123">A Mac that is running macOS Yosemite (10.10) or later.</span><span class="sxs-lookup"><span data-stu-id="56b04-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="56b04-124">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="56b04-124">Install Git and Node.js</span></span>
<span data-ttu-id="56b04-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span><span class="sxs-lookup"><span data-stu-id="56b04-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="56b04-126">Install Homebrew.</span><span class="sxs-lookup"><span data-stu-id="56b04-126">Install Homebrew.</span></span> <span data-ttu-id="56b04-127">If you've already installed Homebrew, go to step 2.</span><span class="sxs-lookup"><span data-stu-id="56b04-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="56b04-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span><span class="sxs-lookup"><span data-stu-id="56b04-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="56b04-129">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="56b04-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="56b04-130">Install Git and Node.js by running the following command:</span><span class="sxs-lookup"><span data-stu-id="56b04-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="56b04-131">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="56b04-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="56b04-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span><span class="sxs-lookup"><span data-stu-id="56b04-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="56b04-133">Install `gulp` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="56b04-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="56b04-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="56b04-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="56b04-135">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="56b04-135">Install Visual Studio Code</span></span>
<span data-ttu-id="56b04-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="56b04-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="56b04-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="56b04-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="56b04-138">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="56b04-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="56b04-139">Summary</span><span class="sxs-lookup"><span data-stu-id="56b04-139">Summary</span></span>
<span data-ttu-id="56b04-140">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="56b04-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="56b04-141">The next task is to create, deploy, and run the sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="56b04-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56b04-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="56b04-142">Next steps</span></span>
<span data-ttu-id="56b04-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="56b04-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
