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
# <a name="subscribe-to-events-for-a-resource-group-and-filter-for-a-resource-with-azure-cli"></a><span data-ttu-id="c0b34-103">Subscribe to events for a resource group and filter for a resource with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c0b34-103">Subscribe to events for a resource group and filter for a resource with Azure CLI</span></span>

<span data-ttu-id="c0b34-104">This script creates an Event Grid subscription to the events for a resource group.</span><span class="sxs-lookup"><span data-stu-id="c0b34-104">This script creates an Event Grid subscription to the events for a resource group.</span></span> <span data-ttu-id="c0b34-105">It uses a filter to get only events for a specified resource in the resource group.</span><span class="sxs-lookup"><span data-stu-id="c0b34-105">It uses a filter to get only events for a specified resource in the resource group.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c0b34-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="c0b34-106">Sample script</span></span>

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

## <a name="script-explanation"></a><span data-ttu-id="c0b34-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c0b34-107">Script explanation</span></span>

<span data-ttu-id="c0b34-108">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="c0b34-108">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="c0b34-109">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c0b34-109">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c0b34-110">Command</span><span class="sxs-lookup"><span data-stu-id="c0b34-110">Command</span></span> | <span data-ttu-id="c0b34-111">Notes</span><span class="sxs-lookup"><span data-stu-id="c0b34-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c0b34-112">az eventgrid event-subscription create</span><span class="sxs-lookup"><span data-stu-id="c0b34-112">az eventgrid event-subscription create</span></span>](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | <span data-ttu-id="c0b34-113">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="c0b34-113">Create an Event Grid subscription.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c0b34-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0b34-114">Next steps</span></span>

* <span data-ttu-id="c0b34-115">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="c0b34-115">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span></span>
* <span data-ttu-id="c0b34-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c0b34-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
