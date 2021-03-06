---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 1: Get tools (Windows) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Pi on Windows 7 and later versions.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: iot development, iot software, internet of things software, install git on windows, gulp run, install node js windows, install npm on windows, install python on windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 24c58e006bbef9bbc1fcd626a0f8f6bcac063f05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553569"
---
# <a name="get-the-tools-windows-7-or-later"></a>Get the tools (Windows 7 or later)

> [!div class="op_single_selector"]
> * [Windows 7 or later](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>What you will do
Download the development tools and the software for the first sample application for Raspberry Pi 3. If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn
In this article, you will learn:

* How to install Git and Node.js.
  * [Git](https://git-scm.com) is an open source distributed version control system. The sample application for this article is stored on Git.
  * [Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.
* How to use NPM to install additional Node.js development tools.
  * The minimum version requirement of Node.js is 4.5 LTS.
  * [NPM](https://www.npmjs.com) is one of the package managers for Node.js.

## <a name="what-you-need"></a>What you need
To complete this operation, you will need:

* An Internet connection to download the development tools and the software.
* A computer that is running Windows.

## <a name="install-git-and-nodejs"></a>Install Git and Node.js
Click the following links to download and install Git and Node.js LTS for Windows.

* [Get Git for Windows](https://git-scm.com/download/win/)
* [Get Node.js LTS for Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Install additional Node.js development tools
Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi. You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.

Start a command prompt as an administrator. Install `gulp` and `device-discovery-cli` by running the following command:

```bash
npm install -g device-discovery-cli gulp
```

If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.

## <a name="install-visual-studio-code"></a>Install Visual Studio Code
[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code. Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS. You use this editor later in the tutorial to edit the sample code.

## <a name="summary"></a>Summary
You've installed the required development tools and software for the first sample application. The next task is to create, deploy, and run the sample application on Pi.

## <a name="next-steps"></a>Next steps
[Create and deploy the blink sample application](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

