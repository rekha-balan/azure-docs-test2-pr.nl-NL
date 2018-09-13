---
title: 'Connect Arduino to Azure IoT - Lesson 1: Get tools (Ubuntu) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Adafruit Feather M0 WiFi on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on ubuntu, install node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90b1c12659c33517142e2048d8f5f629f6d6b4c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548891"
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="e6bd6-104">Get the tools (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="e6bd6-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="e6bd6-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="e6bd6-108">What you will do</span></span>

<span data-ttu-id="e6bd6-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="e6bd6-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e6bd6-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.

## <a name="what-you-will-learn"></a><span data-ttu-id="e6bd6-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="e6bd6-112">What you will learn</span></span>
<span data-ttu-id="e6bd6-113">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="e6bd6-113">In this article, you will learn:</span></span>

* <span data-ttu-id="e6bd6-114">How to install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="e6bd6-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="e6bd6-115">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e6bd6-116">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e6bd6-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e6bd6-118">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="e6bd6-119">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e6bd6-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e6bd6-121">What you need</span><span class="sxs-lookup"><span data-stu-id="e6bd6-121">What you need</span></span>
<span data-ttu-id="e6bd6-122">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="e6bd6-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="e6bd6-123">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="e6bd6-124">A computer that is running Ubuntu 16.04 or later.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="e6bd6-125">Install Git, Node.js, and NPM</span><span class="sxs-lookup"><span data-stu-id="e6bd6-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="e6bd6-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="e6bd6-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e6bd6-127">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="e6bd6-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="e6bd6-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="e6bd6-129">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="e6bd6-129">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="e6bd6-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e6bd6-131">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e6bd6-131">Install Visual Studio Code</span></span>
<span data-ttu-id="e6bd6-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="e6bd6-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e6bd6-134">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e6bd6-135">Summary</span><span class="sxs-lookup"><span data-stu-id="e6bd6-135">Summary</span></span>
<span data-ttu-id="e6bd6-136">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="e6bd6-137">The next task is to create, deploy, and run the sample application on your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="e6bd6-137">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6bd6-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6bd6-138">Next steps</span></span>
<span data-ttu-id="e6bd6-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="e6bd6-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md