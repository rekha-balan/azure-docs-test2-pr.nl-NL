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
# <a name="query-event-grid-subscriptions"></a><span data-ttu-id="24b86-103">Query Event Grid subscriptions</span><span class="sxs-lookup"><span data-stu-id="24b86-103">Query Event Grid subscriptions</span></span> 

<span data-ttu-id="24b86-104">This article describes how to list the Event Grid subscriptions in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="24b86-104">This article describes how to list the Event Grid subscriptions in your Azure subscription.</span></span> <span data-ttu-id="24b86-105">When querying your existing Event Grid subscriptions, it's important to understand the different types of subscriptions.</span><span class="sxs-lookup"><span data-stu-id="24b86-105">When querying your existing Event Grid subscriptions, it's important to understand the different types of subscriptions.</span></span> <span data-ttu-id="24b86-106">You provide different parameters based on the type of subscription you want to get.</span><span class="sxs-lookup"><span data-stu-id="24b86-106">You provide different parameters based on the type of subscription you want to get.</span></span>

## <a name="resource-groups-and-azure-subscriptions"></a><span data-ttu-id="24b86-107">Resource groups and Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="24b86-107">Resource groups and Azure subscriptions</span></span>

<span data-ttu-id="24b86-108">Azure subscriptions and resource groups aren't Azure resources.</span><span class="sxs-lookup"><span data-stu-id="24b86-108">Azure subscriptions and resource groups aren't Azure resources.</span></span> <span data-ttu-id="24b86-109">Therefore, event grid subscriptions to resource groups or Azure subscriptions do not have the same properties as event grid subscriptions to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="24b86-109">Therefore, event grid subscriptions to resource groups or Azure subscriptions do not have the same properties as event grid subscriptions to Azure resources.</span></span> <span data-ttu-id="24b86-110">Event grid subscriptions to resource groups or Azure subscriptions are considered global.</span><span class="sxs-lookup"><span data-stu-id="24b86-110">Event grid subscriptions to resource groups or Azure subscriptions are considered global.</span></span>

<span data-ttu-id="24b86-111">To get event grid subscriptions for an Azure subscription and its resource groups, you don't need to provide any parameters.</span><span class="sxs-lookup"><span data-stu-id="24b86-111">To get event grid subscriptions for an Azure subscription and its resource groups, you don't need to provide any parameters.</span></span> <span data-ttu-id="24b86-112">Make sure you've selected the Azure subscription you want to query.</span><span class="sxs-lookup"><span data-stu-id="24b86-112">Make sure you've selected the Azure subscription you want to query.</span></span> <span data-ttu-id="24b86-113">The following examples don't get event grid subscriptions for custom topics or Azure resources.</span><span class="sxs-lookup"><span data-stu-id="24b86-113">The following examples don't get event grid subscriptions for custom topics or Azure resources.</span></span>

<span data-ttu-id="24b86-114">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-114">For Azure CLI, use:</span></span>

```azurecli-interactive
az account set -s "My Azure Subscription"
az eventgrid event-subscription list
```

<span data-ttu-id="24b86-115">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-115">For PowerShell, use:</span></span>

```azurepowershell-interactive
Set-AzureRmContext -Subscription "My Azure Subscription"
Get-AzureRmEventGridSubscription
```

<span data-ttu-id="24b86-116">To get event grid subscriptions for an Azure subscription, provide the topic type of **Microsoft.Resources.Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="24b86-116">To get event grid subscriptions for an Azure subscription, provide the topic type of **Microsoft.Resources.Subscriptions**.</span></span>

<span data-ttu-id="24b86-117">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-117">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --topic-type-name "Microsoft.Resources.Subscriptions"
```

<span data-ttu-id="24b86-118">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-118">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.Resources.Subscriptions"
```

<span data-ttu-id="24b86-119">To get event grid subscriptions for all resource groups within an Azure subscription, provide the topic type of **Microsoft.Resources.ResourceGroups**.</span><span class="sxs-lookup"><span data-stu-id="24b86-119">To get event grid subscriptions for all resource groups within an Azure subscription, provide the topic type of **Microsoft.Resources.ResourceGroups**.</span></span>

<span data-ttu-id="24b86-120">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-120">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --topic-type-name "Microsoft.Resources.ResourceGroups"
```

<span data-ttu-id="24b86-121">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-121">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.Resources.ResourceGroups"
```

<span data-ttu-id="24b86-122">To get event grid subscriptions for a specified resource group, provide the name of the resource group as a parameter.</span><span class="sxs-lookup"><span data-stu-id="24b86-122">To get event grid subscriptions for a specified resource group, provide the name of the resource group as a parameter.</span></span>

<span data-ttu-id="24b86-123">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-123">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --resource-group myResourceGroup
```

<span data-ttu-id="24b86-124">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-124">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -ResourceGroupName myResourceGroup
```

## <a name="custom-topics-and-azure-resources"></a><span data-ttu-id="24b86-125">Custom topics and Azure resources</span><span class="sxs-lookup"><span data-stu-id="24b86-125">Custom topics and Azure resources</span></span>

<span data-ttu-id="24b86-126">Event grid custom topics are Azure resources.</span><span class="sxs-lookup"><span data-stu-id="24b86-126">Event grid custom topics are Azure resources.</span></span> <span data-ttu-id="24b86-127">Therefore, you query event grid subscriptions for custom topics and other resources, like Blob storage account, in the same way.</span><span class="sxs-lookup"><span data-stu-id="24b86-127">Therefore, you query event grid subscriptions for custom topics and other resources, like Blob storage account, in the same way.</span></span> <span data-ttu-id="24b86-128">To get event grid subscriptions for custom topics, you must provide parameters that identify the resource or identify the location of the resource.</span><span class="sxs-lookup"><span data-stu-id="24b86-128">To get event grid subscriptions for custom topics, you must provide parameters that identify the resource or identify the location of the resource.</span></span> <span data-ttu-id="24b86-129">It's not possible to broadly query event grid subscriptions for resources across your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="24b86-129">It's not possible to broadly query event grid subscriptions for resources across your Azure subscription.</span></span>

<span data-ttu-id="24b86-130">To get event grid subscriptions for custom topics and other resources in a location, provide the name of the location.</span><span class="sxs-lookup"><span data-stu-id="24b86-130">To get event grid subscriptions for custom topics and other resources in a location, provide the name of the location.</span></span>

<span data-ttu-id="24b86-131">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-131">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --location westus2
```

<span data-ttu-id="24b86-132">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-132">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -Location westus2
```

<span data-ttu-id="24b86-133">To get subscriptions to custom topics for a location, provide the location and the topic type of **Microsoft.EventGrid.Topics**.</span><span class="sxs-lookup"><span data-stu-id="24b86-133">To get subscriptions to custom topics for a location, provide the location and the topic type of **Microsoft.EventGrid.Topics**.</span></span>

<span data-ttu-id="24b86-134">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-134">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --topic-type-name "Microsoft.EventGrid.Topics" --location "westus2"
```

<span data-ttu-id="24b86-135">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-135">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.EventGrid.Topics" -Location westus2
```

<span data-ttu-id="24b86-136">To get subscriptions to storage accounts for a location, provide the location and the topic type of **Microsoft.Storage.StorageAccounts**.</span><span class="sxs-lookup"><span data-stu-id="24b86-136">To get subscriptions to storage accounts for a location, provide the location and the topic type of **Microsoft.Storage.StorageAccounts**.</span></span>

<span data-ttu-id="24b86-137">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-137">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --topic-type "Microsoft.Storage.StorageAccounts" --location westus2
```

<span data-ttu-id="24b86-138">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-138">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicTypeName "Microsoft.Storage.StorageAccounts" -Location westus2
```

<span data-ttu-id="24b86-139">To get event grid subscriptions for a custom topic, provide the name of the custom topic and the name of its resource group.</span><span class="sxs-lookup"><span data-stu-id="24b86-139">To get event grid subscriptions for a custom topic, provide the name of the custom topic and the name of its resource group.</span></span>

<span data-ttu-id="24b86-140">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-140">For Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid event-subscription list --topic-name myCustomTopic --resource-group myResourceGroup
```

<span data-ttu-id="24b86-141">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-141">For PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmEventGridSubscription -TopicName myCustomTopic -ResourceGroupName myResourceGroup
```

<span data-ttu-id="24b86-142">To get event grid subscriptions for a particular resource, provide the resource ID.</span><span class="sxs-lookup"><span data-stu-id="24b86-142">To get event grid subscriptions for a particular resource, provide the resource ID.</span></span>

<span data-ttu-id="24b86-143">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-143">For Azure CLI, use:</span></span>

```azurecli-interactive
resourceid=$(az resource show -n mystorage -g myResourceGroup --resource-type "Microsoft.Storage/storageaccounts" --query id --output tsv)
az eventgrid event-subscription list --resource-id $resourceid
```

<span data-ttu-id="24b86-144">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="24b86-144">For PowerShell, use:</span></span>

```azurepowershell-interactive
$resourceid = (Get-AzureRmResource -Name mystorage -ResourceGroupName myResourceGroup).ResourceId
Get-AzureRmEventGridSubscription -ResourceId $resourceid
```

## <a name="next-steps"></a><span data-ttu-id="24b86-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="24b86-145">Next steps</span></span>

* <span data-ttu-id="24b86-146">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span><span class="sxs-lookup"><span data-stu-id="24b86-146">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>
* <span data-ttu-id="24b86-147">For an introduction to Event Grid, see [About Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="24b86-147">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="24b86-148">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="24b86-148">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
