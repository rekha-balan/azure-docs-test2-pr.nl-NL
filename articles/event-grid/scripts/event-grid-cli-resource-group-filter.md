---
title: Azure CLI script sample - Subscribe to resource group and filter by resource | Microsoft Docs
description: Azure CLI Script Sample - Subscribe to resource group and filter by resource
services: event-grid
documentationcenter: na
author: tfitzmac
ms.service: event-grid
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2018
ms.author: tomfitz
ms.openlocfilehash: 4c3ac2eed6d7304be136fb20e7d9b8322658159a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870311"
---
# <a name="subscribe-to-events-for-a-resource-group-and-filter-for-a-resource-with-azure-cli"></a>Subscribe to events for a resource group and filter for a resource with Azure CLI

This script creates an Event Grid subscription to the events for a resource group. It uses a filter to get only events for a specified resource in the resource group.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

```azurecli
#!/bin/bash

# Provide an endpoint for handling the events.
myEndpoint="<endpoint URL>"

# Select the Azure subscription that contains the resource group.
az account set --subscription "Contoso Subscription"

# Get the resource ID to filter events
resourceId=$(az resource show --name demoSecurityGroup --resource-group myResourceGroup --resource-type Microsoft.Network/networkSecurityGroups --query id --output tsv)

# Subscribe to the resource group. Provide the name of the resource group you want to subscribe to.
az eventgrid event-subscription create \
  --name demoSubscriptionToResourceGroup \
  --resource-group myResourceGroup \
  --endpoint $myEndpoint \
  --subject-begins-with $resourceId
```

## <a name="script-explanation"></a>Script explanation

This script uses the following command to create the event subscription. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az eventgrid event-subscription create](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | Create an Event Grid subscription. |


## <a name="next-steps"></a>Next steps

* For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).
* For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).
