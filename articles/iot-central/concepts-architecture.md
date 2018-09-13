---
title: Architectural concepts in Azure IoT Central | Microsoft Docs
description: This article introduces key concepts relating the architecture of Azure IoT Central
author: dominicbetts
ms.author: dobett
ms.date: 11/30/2017
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: timlt
ms.openlocfilehash: 44408e7b6ad1a068f265bf7b78d973e6aae3001b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967074"
---
# <a name="azure-iot-central-architecture"></a>Azure IoT Central architecture

This article provides an overview of the Microsoft Azure IoT Central architecture.

![Top-level architecture](media/concepts-architecture/architecture.png)

## <a name="devices"></a>Devices

Devices exchange data with your Azure IoT Central application. A device can:

- Send measurements such as telemetry.
- Synchronize settings with your application.

In Azure IoT Central, the data that a device can exchange with your application is specified in a device template. For more information about device templates, see [Metadata management](#metadata-management).

To learn more about how devices connect to your Azure IoT Central application, see [Device connectivity](concepts-connectivity.md).

## <a name="cloud-gateway"></a>Cloud gateway

Azure IoT Central uses Azure IoT Hub as a cloud gateway that enables device connectivity. IoT Hub enables:

- Data ingestion at scale in the cloud.
- Device management.
- Secure device connectivity.

To learn more about IoT Hub, see [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/).

To learn more about device connectivity in Azure IoT Central, see [Device connectivity](concepts-connectivity.md).

## <a name="data-stores"></a>Data stores

Azure IoT Central stores application data in the cloud. Application data stored includes:

- Device templates.
- Device identities.
- Device metadata.
- User and role data.

Azure IoT Central uses a time series store for the measurement data sent from your devices. Time series data from devices used by the analytics service.

## <a name="analytics"></a>Analytics

The analytics service is responsible for generating the custom reporting data that the application displays. An operator can [customize the analytics](howto-create-analytics.md) displayed in the application. The analytics service is built on top of [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/) and processes the measurement data sent from your devices.

## <a name="rules-and-actions"></a>Rules and actions

[Rules and actions](howto-create-telemetry-rules.md) work closely together to automate tasks within the application. A builder can define rules based on device telemetry such as the temperature exceeding a defined threshold. Azure IoT Central uses a stream processor to determine when the rule conditions are met. When a rule condition is met, it triggers an action defined by the builder. For example, an action can send an email to notify an engineer that the temperature in a device is too high.

## <a name="metadata-management"></a>Metadata management

In an Azure IoT Central application, device templates define the behavior and capability of types of device. For example, a refrigerator device template specifies the telemetry a refrigerator sends to your application.

![Template architecture](media/concepts-architecture/template_architecture.png)

In a device template:

- **Measurements** specify the telemetry the device sends to the application.
- **Settings** specify the configurations that an operator can set.
- **Properties** specify metadata that an operator can set.
- **Rules** automate behavior in the application based on data sent from a device.
- **Dashboards** are customizable views of a device in the application.

An application can have one or more simulated and real devices based on each device template.

## <a name="rbac"></a>RBAC

An [administrator can define access rules](howto-administer.md) for an Azure IoT Central application using the predefined roles. An administrator can assign users to roles that determine what areas of the application the user has access to.

## <a name="security"></a>Security

Security features within Azure IoT Central include:

- Data is encrypted in transit and at rest.
- Authentication is provided either by Azure Active Directory or Microsoft Account. Two-factor authentication is supported.
- Full tenant isolation.
- Device level security.

## <a name="ui-shell"></a>UI shell

The UI shell is a modern, responsive, HTML5 browser-based application.

## <a name="next-steps"></a>Next steps

Now that you have learned about the architecture of Azure IoT Central, the suggested next step is to learn about [device connectivity](concepts-connectivity.md) in Azure IoT Central.