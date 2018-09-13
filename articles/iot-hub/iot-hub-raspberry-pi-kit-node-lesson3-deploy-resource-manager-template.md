---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 3: Template deployment | Microsoft Docs'
description: The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: storing data in the cloud, data stored in cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f8d5d4d0fdf7d54501c7f89135ade0427f5f4b6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554586"
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Create an Azure function app and Azure storage account
[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud. An Azure function app hosts the execution of your functions in Azure.

## <a name="what-you-will-do"></a>What you will do
Use an Azure Resource Manager template to create an Azure function app and an Azure storage account. The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage. If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn
In this article, you will learn:

* How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.
* How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.

## <a name="what-you-need"></a>What you need
You must have successfully completed:
* [Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)
* [Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a>Open the sample app
Open the sample project in Visual Studio Code by running the following commands:

```bash
cd Lesson3
code .
```

![Repo structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* The `app.js` file in the `app` subfolder is the key source file. This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.
* The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.
* The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.
* The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configure Azure Resource Manager templates and create resources in Azure
Update the `arm-template-param.json` file in Visual Studio Code.

![Azure Resource Manager template parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Replace **[prefix string for new resources]** with any prefix you want. The prefix ensures that the resource name is globally unique to avoid conflict. Do not use a dash or number initial in the prefix.

After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

It takes about five minutes to create these resources. While the resource creation is in progress, you can move on to the next article.

## <a name="summary"></a>Summary
You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages. You can now deploy and run the sample to send device-to-cloud messages on Pi.

## <a name="next-steps"></a>Next steps
[Run a sample application to send device-to-cloud messages on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)



