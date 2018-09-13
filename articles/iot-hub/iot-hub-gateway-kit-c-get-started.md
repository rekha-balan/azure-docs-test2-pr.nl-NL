---
title: SensorTag device & Azure IoT Gateway - Get started | Microsoft Docs
description: Get started with IoT Gateway Starter Kit, create your Azure IoT hub, and connect SensorTag and Gateway to the IoT hub
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot hub, iot gateway, getting started with the internet of things, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7f186167509769fbdc1f4aa2ae06657ff0b1424c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661807"
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Get started with IoT Gateway Starter Kit with a SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Simulated Device](iot-hub-gateway-kit-c-sim-get-started.md)

In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.

***
**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit). **Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>Lesson 1: Configure your NUC
![Lesson1 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Gateway SDK package on NUC, and run a sample app to verify the gateway functionality.

*Estimated time to complete: 15 minutes*

Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lesson 2: Create your IoT Hub
![Lesson2 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

In this lesson, you install the tools and software on your host computer. Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.

Complete Lesson 1 before you start this lesson.

### <a name="get-the-tools"></a>Get the tools
Install the tools and software on your host computer.

*Estimated time to complete: 20 minutes*

Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Create an IoT hub and register your device
Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.

*Estimated time to complete: 10 minutes*

Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Lesson 3: Receive messages from SensorTag and read messages from your IoT hub
In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway. Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks. Modules communicate with one another via a message broker. The sample application has a BLE module and an IoT hub module. The BLE module receives data from BLE SensorTag. The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in the Azure IoT Gateway SDK.

![Lesson 3 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a>Configure and run the BLE sample app
Set up the connectivity between SensorTag and your gateway. Then finish the configuration and run the BLE sample application.

*Estimated time to complete: 15 minutes*

Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Read messages from your IoT hub
Run sample code on your host computer to read messages from your IoT hub.

*Estimated time to complete: 15 minutes*

Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-to-azure-table-storage"></a>Lesson 4: Save messages to Azure Table storage
Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.

![Lesson 4 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Create an Azure function app and Azure Storage account
Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.

*Estimated time to complete: 10 minutes*

Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Read messages persisted in Azure Table storage
Monitor the gateway-to-cloud messages as they are written to Azure Table storage.

*Estimated time to complete: 5 minutes*

Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Troubleshooting
If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.

## <a name="explore-more"></a>Explore more
Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.



