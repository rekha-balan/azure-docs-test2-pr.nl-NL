---
title: Connected Factory solution features - Azure | Microsoft Docs
description: An overview of the features of the Connected Factory preconfigured solution.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: dobett
ms.openlocfilehash: 3478217771418ab31772d6a42a7ed8d8a2e8069a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871668"
---
# <a name="what-is-connected-factory-iot-solution-accelerator"></a>What is Connected Factory IoT solution accelerator?

Connected Factory is an implementation of Microsoft's Azure Industrial IoT reference architecture, packaged as on open-source solution. You can use it as a starting point for a commercial product. You can deploy a pre-built version of the Connected Factory solution into your Azure subscription from [Azure IoT solution accelerators](https://www.azureiotsolutions.com/#solutions/types/CF).

![Connected Factory solution dashboard](./media/iot-accelerators-connected-factory-features/dashboard.png)

Connected Factory includes the following features:

## <a name="industrial-device-interoperability"></a>Industrial device interoperability

- Connect to industrial assets with an OPC UA interface.
- Use the simulated production lines (running OPC UA servers in Docker containers) to see live telemetry from them.
- Browse the OPC UA information model of the OPC UA servers from a cloud dashboard.

## <a name="remote-management"></a>Remote management

- Configure your OPC UA assets from the cloud dashboard (call methods, read, and write data).
- Publish and unpublish telemetry data from your OPC UA assets from a cloud dashboard.

## <a name="cloud-dashboard"></a>Cloud dashboard

- View telemetry previews directly in a cloud dashboard.
- View trends in telemetry data and create correlations using the Time Series Insights Explorer dashboard.
- See calculated Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) from a cloud dashboard.
- View industrial asset hierarchies in a tree topology as well as on an interactive map.
- View, acknowledge, and close alerts from a cloud dashboard.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

- [Azure Time Series Insights](../time-series-insights/time-series-insights-overview.md) is built for storing, visualizing, and querying large amounts of time-series data. Connected Factory leverages this service.
- Connected Factory integrates with this service enabling you perform deep, real-time analysis of your device data.

## <a name="rules-and-alerts"></a>Rules and alerts

[Configure threshold-based rules for alerts](iot-accelerators-connected-factory-configure.md).

## <a name="end-to-end-security"></a>End-to-end security

- Configure security permissions for users using Role-Based Access Control (RBAC).
- End-to-end encryption is implemented using OPC UA authentication (using X.509 certificates) as well as security tokens.

## <a name="customizability"></a>Customizability

- Customize the solution to meet specific business requirements.
- Full solution source-code available on GitHub. See the [Connected Factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory) repository.

## <a name="next-steps"></a>Next steps

Learn more about the Connected Factory preconfigured solution by reading the following articles:

* [Connected Factory preconfigured solution walkthrough](iot-accelerators-connected-factory-sample-walkthrough.md)
* [Deploy a gateway for Connected Factory]( iot-accelerators-connected-factory-gateway-deployment.md)
