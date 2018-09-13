---
title: Register a new Azure IoT Edge device (portal) | Microsoft Docs
description: Use the Azure portal to register a new IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/05/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: b61594469df33e11c23c9cbe0b9542da374fefa3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864585"
---
# <a name="register-a-new-azure-iot-edge-device-from-the-azure-portal"></a>Register a new Azure IoT Edge device from the Azure portal

Before you can use your IoT devices with Azure IoT Edge, you need to register them with your IoT hub. Once you register a device, you receive a connection string that can be used to set up your device for Edge workloads. 

This article shows how to register a new IoT Edge device using the Azure portal.

## <a name="prerequisites"></a>Prerequisites

* An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription. 

## <a name="create-a-device"></a>Create a device

In the Azure portal, IoT Edge devices are created and managed separately from devices that connect to your IoT hub but aren't edge-enabled. 

1. Sign in to the [Azure portal](https://portal.azure.com) and navigate to your IoT hub. 
2. Select **IoT Edge** from the menu.
3. Select **Add IoT Edge Device**. 
4. Provide a descriptive device ID. 
5. Select **Save**. 

## <a name="view-all-devices"></a>View all devices

All the edge-enabled devices that connect to your IoT hub are listed on the **IoT Edge** page. 

## <a name="retrieve-the-connection-string"></a>Retrieve the connection string

When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.

1. From the **IoT Edge** page in the portal, click on the device ID from the list of Edge devices. 
2. Copy the value of either **Connection string—primary key** or **Connection string—secondary key**. 

## <a name="next-steps"></a>Next steps

Learn how to [Deploy modules to a device with the Azure portal](how-to-deploy-modules-portal.md)