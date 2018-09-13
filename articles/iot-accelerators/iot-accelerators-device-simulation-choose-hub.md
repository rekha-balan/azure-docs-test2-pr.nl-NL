---
title: Use an existing IoT hub with the Device Simulation solution - Azure | Microsoft Docs
description: This article describes how to configure the Device Simulation solution accelerator to use an existing IoT Hub.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 07/06/2018
ms.topic: conceptual
ms.openlocfilehash: ee96173ca5f36dee0f08c38e4b6e29da6fee804e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856705"
---
# <a name="use-an-existing-iot-hub-with-the-device-simulation-solution-accelerator"></a>Use an existing IoT hub with the Device Simulation solution accelerator

When you provision the Device Simulation solution accelerator, you can choose to deploy an IoT hub in the solution accelerator's resource group to use in your simulation.

If you don't choose to deploy the optional IoT Hub, you must use your own hub for any simulations you run. If you do choose to deploy the optional IoT Hub, you can choose to use this optional hub or your own hub.

If you don't have an IoT hub, you can always create a new one from the [Azure portal](https://portal.azure.com).

To use a pre-existing IoT hub, you need a connection string for the **iothubowner** shared access policy. You can get this connection string from the [Azure portal](https://portal.azure.com):

1. On the hub's configuration page in the portal, click **Shared access policies**.
1. Click **iothubowner**.
1. Copy either the primary or secondary connection string.

[![Get connection string](./media/iot-accelerators-device-simulation-choose-hub/connectionstring-inline.png)](./media/iot-accelerators-device-simulation-choose-hub/connectionstring-expanded.png#lightbox)

USe the connection string you copied when you configure the simulation:

[![Configure simulation](./media/iot-accelerators-device-simulation-choose-hub/configuresimulation-inline.png)](./media/iot-accelerators-device-simulation-choose-hub/configuresimulation-expanded.png#lightbox)

## <a name="next-steps"></a>Next steps

In this how-to guide, you've learned how to use an existing IoT hub in a simulation. Next, you may want to learn how to [Configure a custom device model](iot-accelerators-device-simulation-custom-model.md) for a simulation.
