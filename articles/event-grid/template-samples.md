---
title: Azure Resource Manager template samples - Event Grid | Microsoft Docs
description: Azure Resource Manager template samples for Event Grid
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.date: 03/27/2018
ms.author: tomfitz
ms.openlocfilehash: f4d6a663b4e0d2c2166028051e713668534b20bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967985"
---
# <a name="azure-resource-manager-templates-for-event-grid"></a>Azure Resource Manager templates for Event Grid

The following table includes links to Azure Resource Manager templates for Event Grid.

| | |
|-|-|
|**Event Grid subscriptions**||
| [Custom topic and subscription with WebHook endpoint](https://github.com/Azure/azure-quickstart-templates/tree/master/101-event-grid)| Deploys an Event Grid custom topic. Creates a subscription to that custom topic that uses a WebHook endpoint. |
| [Custom topic subscription with EventHub endpoint](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/subscribeCustomTopicToEventHub.json)| Creates an Event Grid subscription to a custom topic that already exists. The subscription uses an Event Hub for the endpoint. |
| [Resource group subscription](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/subscribeResourceGroupToWebHook.json)| Subscribes to events for a resource group. The resource group you specify as the target during deployment is the source of events. The subscription uses an Event Hub for the endpoint. |
| [Blob storage account and subscription](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/createBlobAndSubscribe.json)| Deploys an Azure Blob storage account and subscribes to events for that storage account. |
| | |
