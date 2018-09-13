---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 1: Get tools (Ubuntu) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Edison on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on ubuntu, install node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 74c5f06c2b12d140814bfb75125d60b83addf70c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564141"
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="c160d-104">Get the tools (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="c160d-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="c160d-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="c160d-108">What you will do</span></span>
<span data-ttu-id="c160d-109">Download the development tools and the software for the first sample application for your Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="c160d-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="c160d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c160d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c160d-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="c160d-111">What you will learn</span></span>
<span data-ttu-id="c160d-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="c160d-112">In this article, you will learn:</span></span>

* <span data-ttu-id="c160d-113">How to install Git and Node.js</span><span class="sxs-lookup"><span data-stu-id="c160d-113">How to install Git and Node.js</span></span>
  * <span data-ttu-id="c160d-114">[Git](https://git-scm.com) is an open source distributed version control system.</span><span class="sxs-lookup"><span data-stu-id="c160d-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="c160d-115">The sample application for this article is stored on Git.</span><span class="sxs-lookup"><span data-stu-id="c160d-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="c160d-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span><span class="sxs-lookup"><span data-stu-id="c160d-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="c160d-117">How to use NPM to install additional Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="c160d-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="c160d-118">The minimum required version of Node.js is 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="c160d-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="c160d-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span><span class="sxs-lookup"><span data-stu-id="c160d-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c160d-120">What you need</span><span class="sxs-lookup"><span data-stu-id="c160d-120">What you need</span></span>
<span data-ttu-id="c160d-121">To complete this operation, you will need:</span><span class="sxs-lookup"><span data-stu-id="c160d-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="c160d-122">An Internet connection to download the development tools and the software.</span><span class="sxs-lookup"><span data-stu-id="c160d-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="c160d-123">A computer that is running Ubuntu 16.04 or later.</span><span class="sxs-lookup"><span data-stu-id="c160d-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="c160d-124">Install Git, Node.js, and NPM</span><span class="sxs-lookup"><span data-stu-id="c160d-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="c160d-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="c160d-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="c160d-126">Install additional Node.js development tools</span><span class="sxs-lookup"><span data-stu-id="c160d-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="c160d-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span><span class="sxs-lookup"><span data-stu-id="c160d-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="c160d-128">Install `gulp` by running the following command in the terminal:</span><span class="sxs-lookup"><span data-stu-id="c160d-128">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="c160d-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="c160d-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="c160d-130">Install Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c160d-130">Install Visual Studio Code</span></span>
<span data-ttu-id="c160d-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c160d-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="c160d-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="c160d-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c160d-133">You use this editor later in the tutorial to edit the sample code.</span><span class="sxs-lookup"><span data-stu-id="c160d-133">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="c160d-134">Summary</span><span class="sxs-lookup"><span data-stu-id="c160d-134">Summary</span></span>
<span data-ttu-id="c160d-135">You've installed the required development tools and software for the first sample application.</span><span class="sxs-lookup"><span data-stu-id="c160d-135">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="c160d-136">The next task is to create, deploy, and run the sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="c160d-136">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c160d-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="c160d-137">Next steps</span></span>
<span data-ttu-id="c160d-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="c160d-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
