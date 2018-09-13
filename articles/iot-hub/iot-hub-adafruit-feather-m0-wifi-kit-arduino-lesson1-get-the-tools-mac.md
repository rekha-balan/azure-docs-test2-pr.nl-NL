---
title: 'Connect Arduino to Azure IoT - Lesson 1: Get tools (macOS) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Adafruit Feather M0 WiFi on macOS.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on mac, install node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a6dc2555367e5fe530b3acde1f1f04ac442fb638
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549987"
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="d4577-104">Get the tools (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="d4577-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="d4577-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="d4577-108">What you will do</span></span>

<span data-ttu-id="d4577-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span><span class="sxs-lookup"><span data-stu-id="d4577-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="d4577-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d4577-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.

## <a name="what-you-will-learn"></a><span data-ttu-id="d4577-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="d4577-112">What you will learn</span></span>
<span data-ttu-id="d4577-113">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="d4577-113">In this article, you will learn:</span></span>

* <span data-ttu-id="d4577-114">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="d4577-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="d4577-115">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="d4577-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="d4577-116">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="d4577-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="d4577-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="d4577-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="d4577-118">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="d4577-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="d4577-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="d4577-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="d4577-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="d4577-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d4577-121">What you need</span><span class="sxs-lookup"><span data-stu-id="d4577-121">What you need</span></span>
<span data-ttu-id="d4577-122">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="d4577-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="d4577-123">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="d4577-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="d4577-124">A Mac that is running macOS Yosemite (10.10) or later.</span><span class="sxs-lookup"><span data-stu-id="d4577-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="d4577-125">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="d4577-125">Install Git and Node.js</span></span>
<span data-ttu-id="d4577-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span><span class="sxs-lookup"><span data-stu-id="d4577-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="d4577-127">Install Homebrew.</span><span class="sxs-lookup"><span data-stu-id="d4577-127">Install Homebrew.</span></span> <span data-ttu-id="d4577-128">If you've already installed Homebrew, go to step 2.</span><span class="sxs-lookup"><span data-stu-id="d4577-128">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="d4577-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span><span class="sxs-lookup"><span data-stu-id="d4577-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="d4577-130">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="d4577-130">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="d4577-131">Install Git and Node.js by running the following command:</span><span class="sxs-lookup"><span data-stu-id="d4577-131">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="d4577-132">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="d4577-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="d4577-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="d4577-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="d4577-134">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="d4577-134">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="d4577-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="d4577-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="d4577-136">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d4577-136">Install Visual Studio Code</span></span>
<span data-ttu-id="d4577-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d4577-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="d4577-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="d4577-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="d4577-139">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="d4577-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="d4577-140">Summary</span><span class="sxs-lookup"><span data-stu-id="d4577-140">Summary</span></span>
<span data-ttu-id="d4577-141">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="d4577-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="d4577-142">The next task is to create, deploy, and run the sample application on your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="d4577-142">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4577-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4577-143">Next steps</span></span>
<span data-ttu-id="d4577-144">[Create and deploy the blink application][create-and-deploy-the-blink-application]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="d4577-144">[Create and deploy the blink application][create-and-deploy-the-blink-application]
<!-- Images and links --></span></span>

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md