---
title: Query Azure Event Grid subscriptions
description: Describes how to list Azure Event Grid subscriptions.
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: conceptual
ms.date: 04/04/2018
ms.author: tomfitz
ms.openlocfilehash: 2b46cde4a352e647ee97669f116a6c1926879fa0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871581"
---
# <a name="query-event-grid-subscriptions"></a>Query Event Grid subscriptions 

This article describes how to list the Event Grid subscriptions in your Azure subscription. When querying your existing Event Grid subscriptions, it's important to understand the different types of subscriptions. You provide different parameters based on the type of subscription you want to get.

## <a name="resource-groups-and-azure-subscriptions"></a>Resource groups and Azure subscriptions

Azure subscriptions and resource groups aren't Azure resources. Therefore, event grid subscriptions to resource groups or Azure subscriptions do not have the same properties as event grid subscriptions to Azure resources. Event grid subscriptions to resource groups or Azure subscriptions are considered global.

To get event grid subscriptions for an Azure subscription and its resource groups, you don't need to provide any parameters. Make sure you've selected the Azure subscription you want to query. The following examples don't get event grid subscriptions for custom topics or Azure resources.

For Azure CLI, use:

```azurecli-interactive
az account set -s "My Azure Subscription"
az eventgrid event-subscription list
```

For PowerShell, use:

```azurepowershell-interactive
Set-AzureRmContext -Subscription "My Azure Subscription"
Get-AzureRmEventGridSubscription
```

To get event grid subscriptions for an Azure subscription, provide the topic type of **Microsoft.Resources.Subscriptions**.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --topic-type-name "Microsoft.Resources.Subscriptions"
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.Resources.Subscriptions"
```

To get event grid subscriptions for all resource groups within an Azure subscription, provide the topic type of **Microsoft.Resources.ResourceGroups**.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --topic-type-name "Microsoft.Resources.ResourceGroups"
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.Resources.ResourceGroups"
```

To get event grid subscriptions for a specified resource group, provide the name of the resource group as a parameter.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --resource-group myResourceGroup
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -ResourceGroupName myResourceGroup
```

## <a name="custom-topics-and-azure-resources"></a>Custom topics and Azure resources

Event grid custom topics are Azure resources. Therefore, you query event grid subscriptions for custom topics and other resources, like Blob storage account, in the same way. To get event grid subscriptions for custom topics, you must provide parameters that identify the resource or identify the location of the resource. It's not possible to broadly query event grid subscriptions for resources across your Azure subscription.

To get event grid subscriptions for custom topics and other resources in a location, provide the name of the location.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --location westus2
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -Location westus2
```

To get subscriptions to custom topics for a location, provide the location and the topic type of **Microsoft.EventGrid.Topics**.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --topic-type-name "Microsoft.EventGrid.Topics" --location "westus2"
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.EventGrid.Topics" -Location westus2
```

To get subscriptions to storage accounts for a location, provide the location and the topic type of **Microsoft.Storage.StorageAccounts**.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --topic-type "Microsoft.Storage.StorageAccounts" --location westus2
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.Storage.StorageAccounts" -Location westus2
```

To get event grid subscriptions for a custom topic, provide the name of the custom topic and the name of its resource group.

For Azure CLI, use:

```azurecli-interactive
az eventgrid event-subscription list --topic-name myCustomTopic --resource-group myResourceGroup
```

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicName myCustomTopic -ResourceGroupName myResourceGroup
```

To get event grid subscriptions for a particular resource, provide the resource ID.

For Azure CLI, use:

```azurecli-interactive
resourceid=$(az resource show -n mystorage -g myResourceGroup --resource-type "Microsoft.Storage/storageaccounts" --query id --output tsv)
az eventgrid event-subscription list --resource-id $resourceid
```

For PowerShell, use:

```azurepowershell-interactive
$resourceid = (Get-AzureRmResource -Name mystorage -ResourceGroupName myResourceGroup).ResourceId
Get-AzureRmEventGridSubscription -ResourceId $resourceid
```

## <a name="next-steps"></a>Next steps

* For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).
* For an introduction to Event Grid, see [About Event Grid](overview.md).
* To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).
