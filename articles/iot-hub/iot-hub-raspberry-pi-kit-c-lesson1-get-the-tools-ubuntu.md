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
# <a name="get-the-tools-ubuntu-1604"></a>Get the tools (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>What you will do
Download the development tools and the software for the first sample application for your Raspberry Pi 3. If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.

## <a name="what-you-will-learn"></a>What you will learn
In this article, you will learn:

* How to install Git and Node.js
  * [Git](https://git-scm.com) is an open source distributed version control system. The sample application for this article is stored on Git.
  * [Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.
* How to use NPM to install additional Node.js development tools.
  * The minimum required version of Node.js is 4.5 LTS.
  * [NPM](https://www.npmjs.com) is one of the package managers for Node.js.

## <a name="what-you-need"></a>What you need
To complete this operation, you will need:

* An Internet connection to download the development tools and the software.
* A computer that is running Ubuntu 16.04 or later.

## <a name="install-git-nodejs-and-npm"></a>Install Git, Node.js, and NPM
Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Install additional Node.js development tools
Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi. Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.

Install `gulp` and `device-discovery-cli` by running the following command in the terminal:

```bash
sudo npm install -g device-discovery-cli gulp
```

If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.

## <a name="install-visual-studio-code"></a>Install Visual Studio Code
[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code. Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS. You use this editor later in the tutorial to edit the sample code.

## <a name="summary"></a>Summary
You've installed the required development tools and software for the first sample application. The next task is to create, deploy, and run the sample application on Pi.

## <a name="next-steps"></a>Next steps
[Create and deploy the blink application](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

