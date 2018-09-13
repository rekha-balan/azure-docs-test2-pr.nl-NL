---
title: 'SensorTag device & Azure IoT Gateway - Lesson 4: Create function app | Microsoft Docs'
description: Save messages from Intel NUC to your IoT hub, write them to Azure Table storage and then read them from the cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: storing data in the cloud, data stored in cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bd35b289c0d0b1dd3e631823c86770f4b2cc1c94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552118"
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Create an Azure function app and storage account

Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud. An Azure function app hosts the execution of your functions in Azure. 

## <a name="what-you-will-do"></a>What you will do

- Use an Azure Resource Manager template to create an Azure function app and an Azure storage account. The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.

If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>What you will learn

In this lesson, you will learn:

- How to use Azure Resource Manager to deploy Azure resources.
- How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.

## <a name="what-you-need"></a>What you need

You must have successfully completed the previous lessons:

- [Lesson 1: Set up your Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [Lesson 2: Get your host computer and Azure IoT hub ready](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [Lesson 3: Receive messages from SensorTag and read messages from IoT hub](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Open a sample app

Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:

```bash
cd Lesson4
npm install
gulp init
code .
```

![repo structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.
- The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.
- The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configure Azure Resource Manager templates and create resources in Azure

Update the `arm-template-param.json` file in Visual Studio Code.

![arm template json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.

After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.

## <a name="summary"></a>Summary

You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages. You can now read messages that are sent by your gateway to your IoT hub.

## <a name="next-steps"></a>Next steps
[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).


