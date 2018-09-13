---
title: Azure Event Grid SDKs
description: Describes the SDKs for Azure Event Grid. These SDKs provide management, publishing and consumption.
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 06/29/2018
ms.author: tomfitz
ms.openlocfilehash: 3c085074863aa166a5766116b6c63b7dc341ad96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870758"
---
# <a name="event-grid-sdks-for-management-and-publishing"></a>Event Grid SDKs for management and publishing

Event Grid provides SDKs that enable you to programmatically manage your resources and post events.

## <a name="management-sdks"></a>Management SDKs

The management SDKs enable you to create, update, and delete event grid topics and subscriptions. Currently, the following SDKs are available:

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.Management.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://search.maven.org/#search%7Cga%7C1%7Cazure-mgmt-eventgrid)
* [Node](https://www.npmjs.com/package/azure-arm-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-mgmt-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_mgmt_event_grid)

## <a name="data-plane-sdks"></a>Data plane SDKs

The data plane SDKs enable you to post events to topics by taking care of authenticating, forming the event, and asynchronously posting to the specified endpoint. They also enable you to consume first party events. Currently, the following SDKs are available:

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventgrid)
* [Node](https://www.npmjs.com/package/azure-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_event_grid)

## <a name="next-steps"></a>Next steps

* For example applications, see [Event Grid code samples](https://azure.microsoft.com/resources/samples/?sort=0&service=event-grid).
* For an introduction to Event Grid, see [What is Event Grid?](overview.md)
* For Event Grid commands in Azure CLI, see [Azure CLI](/cli/azure/eventgrid).
* For Event Grid commands in PowerShell, see [PowerShell](/powershell/module/azurerm.eventgrid).
