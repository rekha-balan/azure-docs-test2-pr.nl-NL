---
title: include file
description: include file
services: iot-edge
author: kgremban
ms.service: iot-edge
ms.topic: include
ms.date: 06/25/2018
ms.author: kgremban
ms.custom: include file
ms.openlocfilehash: bacafdc8f7fd8e206335f3be0a086df1c54f1081
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45073881"
---
Create a device identity for your simulated device so that it can communicate with your IoT hub. Since IoT Edge devices behave and can be managed differently than typical IoT devices, you declare this to be an IoT Edge device from the beginning. 

1. In the Azure portal, navigate to your IoT hub.
1. Select **IoT Edge** then select **Add IoT Edge Device**.

   ![Add IoT Edge Device](./media/iot-edge-register-device/add-device.png)

1. Give your simulated device a unique device ID.
1. Select **Save** to add your device.
1. Select your new device from the list of devices.
1. Copy the value for **Connection string—primary key** and save it. You'll use this value to configure the IoT Edge runtime in the next section. 

