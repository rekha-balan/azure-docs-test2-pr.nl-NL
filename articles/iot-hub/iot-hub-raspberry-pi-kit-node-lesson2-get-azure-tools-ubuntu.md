---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 2: Get tools (Ubuntu) | Microsoft Docs'
description: Install Python and the Azure command-line interface (Azure CLI) on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: iot cloud service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c3db1fdf1c510c68cc68fa73b333c7265262cdb0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552102"
---
# <a name="get-azure-tools-ubuntu-1604"></a>Get Azure tools (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 and later](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>What you will do
Install the Azure command-line interface (Azure CLI). If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn
In this article, you will learn:
* How to install the Azure CLI.
* How to add an IoT subgroup of the Azure CLI.

## <a name="what-you-need"></a>What you need
* An Ubuntu computer with an Internet connection.
* An active Azure subscription. If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.

## <a name="install-the-azure-cli"></a>Install the Azure CLI
The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command-line to provision and manage resources.

To install the latest Azure CLI, follow these steps:

1. Run the following commands in a terminal window. It might take five minutes to install the Azure CLI.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Verify the installation by running the following command:

   ```bash
   az iot -h
   ```

You should see the following output if the installation is successful.

![Output that indicates success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Summary
You've installed the Azure CLI. Your next task is to create your Azure IoT hub and device identity using the Azure CLI.

## <a name="next-steps"></a>Next steps
[Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)


