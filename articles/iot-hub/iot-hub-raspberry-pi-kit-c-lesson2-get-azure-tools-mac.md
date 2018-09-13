---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 2: Azure tools (macOS) | Microsoft Docs'
description: Install Python and Azure command-line interface (Azure CLI) on macOS.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot cloud service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 179c54348e02c030f2cd93a8a348c5bd5f442b27
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563509"
---
# <a name="get-azure-tools-macos-1010"></a>Get Azure tools (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 and later](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>What you will do
Install the Azure command-line interface (Azure CLI). If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn
In this article, you will learn:
* How to install Azure CLI.
* How to add an IoT subgroup of the Azure CLI.

## <a name="what-you-need"></a>What you need
* A Mac with an Internet connection.
* An active Azure subscription. If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.

## <a name="install-python"></a>Install Python
Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew. See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Install Python and pip by running the following command:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Install the Azure CLI
The Azure CLI provides a multiplatform command-line experience for Azure. You work directly from your command line to provision and manage resources. 

To install the latest Azure CLI, follow these steps:

1. Run the following commands in a terminal window. It might take five minutes to install the Azure CLI.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Verify the installation by running the following command:

   ```bash
   az iot -h
   ```

You should see the following output if the installation is successful.

![Output that indicates success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Summary
You've installed the Azure CLI. Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.

## <a name="next-steps"></a>Next steps
[Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)


