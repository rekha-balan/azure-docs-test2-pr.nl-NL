---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 1: Get tools (Windows) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Edison on Windows 7 and later versions.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on windows, install node js windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552392"
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="90514-104">Get the tools (Windows 7 or later)</span><span class="sxs-lookup"><span data-stu-id="90514-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="90514-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="90514-108">What you will do</span></span>
<span data-ttu-id="90514-109">Download the development tools and the software for the first sample application for Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="90514-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="90514-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="90514-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="90514-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="90514-111">What you will learn</span></span>
<span data-ttu-id="90514-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="90514-112">In this article, you will learn:</span></span>

* <span data-ttu-id="90514-113">How to install Git and Node.js.</span><span class="sxs-lookup"><span data-stu-id="90514-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="90514-114">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="90514-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="90514-115">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="90514-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="90514-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="90514-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="90514-117">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="90514-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="90514-118">The minimum version requirement of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="90514-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="90514-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="90514-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="90514-120">What you need</span><span class="sxs-lookup"><span data-stu-id="90514-120">What you need</span></span>

<span data-ttu-id="90514-121">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="90514-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="90514-122">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="90514-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="90514-123">A computer that is running Windows.</span><span class="sxs-lookup"><span data-stu-id="90514-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="90514-124">Install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="90514-124">Install Git and Node.js</span></span>

<span data-ttu-id="90514-125">Click the links below to download and install Git and Node.js LTS for Windows.</span><span class="sxs-lookup"><span data-stu-id="90514-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="90514-126">Get Git for Windows</span><span class="sxs-lookup"><span data-stu-id="90514-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="90514-127">Get Node.js LTS for Windows</span><span class="sxs-lookup"><span data-stu-id="90514-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="90514-128">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="90514-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="90514-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span><span class="sxs-lookup"><span data-stu-id="90514-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="90514-130">Start a command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="90514-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="90514-131">Install `gulp` by running the following command:</span><span class="sxs-lookup"><span data-stu-id="90514-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="90514-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="90514-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="90514-133">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="90514-133">Install Visual Studio Code</span></span>

<span data-ttu-id="90514-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="90514-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="90514-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="90514-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="90514-136">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="90514-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="90514-137">Summary</span><span class="sxs-lookup"><span data-stu-id="90514-137">Summary</span></span>

<span data-ttu-id="90514-138">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="90514-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="90514-139">The next task is to create, deploy, and run the sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="90514-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90514-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="90514-140">Next steps</span></span>

<span data-ttu-id="90514-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="90514-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
