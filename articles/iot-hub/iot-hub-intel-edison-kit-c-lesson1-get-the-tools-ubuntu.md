---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 1: Get tools (Ubuntu) | Microsoft Docs'
description: Download and install the necessary tools and software for the first sample application for Edison on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino development tools, iot development, iot software, internet of things software, install git on ubuntu, install node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 4c7b8e04-b892-459b-8b03-85bcaff2465c
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e929a1cb38f1bacca833e86878c13f20e02885ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540812"
---
# <a name="get-the-tools-ubuntu-1604"></a>Get the tools (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 or later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>What you will do
Download the development tools and the software for the first sample application for your Intel Edison. If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].

> [!NOTE]
> Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.

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
Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.

Install `gulp` by running the following command in the terminal:

```bash
sudo npm install -g gulp
```

If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.

## <a name="install-visual-studio-code"></a>Install Visual Studio Code
[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code. Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS. You use this editor later in the tutorial to edit the sample code.

## <a name="summary"></a>Summary
You've installed the required development tools and software for the first sample application. The next task is to create, deploy, and run the sample application on Edison.

## <a name="next-steps"></a>Next steps
[Create and deploy the blink sample application][create-and-deploy-the-blink-application]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
