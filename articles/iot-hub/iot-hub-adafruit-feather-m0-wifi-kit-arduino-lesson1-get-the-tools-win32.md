---
title: 'Connect Arduino to Azure IoT - Lesson 1: Get tools (Windows) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Adafruit Feather M0 WiFi on Windows 7 and later versions.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on windows, install node js windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d27c016c4a74e31455e676b3c3070a8e262b21f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661134"
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="7826d-104">Get the tools (Windows 7 or later)</span><span class="sxs-lookup"><span data-stu-id="7826d-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="7826d-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="7826d-108">What you will do</span></span>

<span data-ttu-id="7826d-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span><span class="sxs-lookup"><span data-stu-id="7826d-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="7826d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="7826d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.

## <a name="what-you-will-learn"></a><span data-ttu-id="7826d-112">What you will learn</span><span class="sxs-lookup"><span data-stu-id="7826d-112">What you will learn</span></span>
<span data-ttu-id="7826d-113">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="7826d-113">In this article, you will learn:</span></span>

* <span data-ttu-id="7826d-114">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="7826d-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="7826d-115">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="7826d-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="7826d-116">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="7826d-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="7826d-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="7826d-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="7826d-118">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="7826d-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="7826d-119">The minimum version requirement of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7826d-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="7826d-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="7826d-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7826d-121">What you need</span><span class="sxs-lookup"><span data-stu-id="7826d-121">What you need</span></span>

<span data-ttu-id="7826d-122">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="7826d-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="7826d-123">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="7826d-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="7826d-124">A computer that is running Windows.</span><span class="sxs-lookup"><span data-stu-id="7826d-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7826d-125">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="7826d-125">Install Git and Node.js</span></span>

<span data-ttu-id="7826d-126">Click the links below to download and install Git and Node.js LTS for Windows.</span><span class="sxs-lookup"><span data-stu-id="7826d-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="7826d-127">Get Git for Windows</span><span class="sxs-lookup"><span data-stu-id="7826d-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="7826d-128">Get Node.js LTS for Windows</span><span class="sxs-lookup"><span data-stu-id="7826d-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="7826d-129">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="7826d-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="7826d-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="7826d-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="7826d-131">Start a command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7826d-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="7826d-132">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="7826d-132">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="7826d-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="7826d-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="7826d-134">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7826d-134">Install Visual Studio Code</span></span>

<span data-ttu-id="7826d-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7826d-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="7826d-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="7826d-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7826d-137">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="7826d-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="7826d-138">Summary</span><span class="sxs-lookup"><span data-stu-id="7826d-138">Summary</span></span>

<span data-ttu-id="7826d-139">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="7826d-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="7826d-140">The next task is to create, deploy, and run the sample application on your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="7826d-140">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7826d-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="7826d-141">Next steps</span></span>

<span data-ttu-id="7826d-142">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="7826d-142">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]
<!-- Images and links --></span></span>

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md