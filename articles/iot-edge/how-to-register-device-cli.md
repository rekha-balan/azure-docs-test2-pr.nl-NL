---
title: Register a new Azure IoT Edge device (CLI) | Microsoft Docs
description: Use the IoT extension for Azure CLI 2.0 to register a new IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/27/2018
ms.topic: conceptual
ms.reviewer: menchi
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 451f4df31cd1c520b14227829923f72fe80c38c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965504"
---
# <a name="register-a-new-azure-iot-edge-device-with-azure-cli-20"></a>Register a new Azure IoT Edge device with Azure CLI 2.0

Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub. Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads. 

[Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge. It enables you to manage Azure IoT Hub resources, device provisioning service instances, and linked-hubs out of the box. The new IoT extension enriches Azure CLI 2.0 with features such as device management and full IoT Edge capability.

This article shows how to register a new IoT Edge device using Azure CLI 2.0.

## <a name="prerequisites"></a>Prerequisites

* An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription. 
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment. At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above. Use `az –-version` to validate. This version supports az extension commands and introduces the Knack command framework. 
* The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).

## <a name="create-a-device"></a>Create a device

Use the following command to create a new device identity in your IoT hub: 

   ```cli
   az iot hub device-identity create --device-id [device id] --hub-name [hub name] --edge-enabled
   ```

This command includes three parameters:
* **device-id**: Provide a descriptive name that's unique to your IoT hub.
* **hub-name**: Provide the name of your IoT hub.
* **edge-enabled**: This parameter declares that the device is for use with IoT Edge.

   ![Create IoT Edge device](./media/how-to-register-device-cli/Create-edge-device.png)

## <a name="view-all-devices"></a>View all devices

Use the following command to view all devices in your IoT hub:

   ```cli
   az iot hub device-identity list --hub-name [hub name]
   ```

Any device that is registered as an IoT Edge device will have the property **capabilities.iotEdge** set to **true**. 

## <a name="retrieve-the-connection-string"></a>Retrieve the connection string

When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub. Use the following command to return the connection string for a single device:

   ```cli
   az iot hub device-identity show-connection-string --device-id [device id] --hub-name [hub name] 
   ```

The device id parameter is case-sensitive. Don't copy the quotation marks around the connection string. 

## <a name="next-steps"></a>Next steps

Learn how to [Deploy modules to a device with Azure CLI 2.0](how-to-deploy-modules-cli.md)