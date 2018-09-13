---
title: Azure PowerShell script sample - Subscribe to resource group and filter by resource | Microsoft Docs
description: Azure PowerShell script sample - Subscribe to resource group and filter by resource
services: event-grid
documentationcenter: na
author: tfitzmac
ms.service: event-grid
ms.devlang: powershell
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2018
ms.author: tomfitz
ms.openlocfilehash: ed77e8f09af841a1414212d7df6b60655ac158cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856629"
---
# <a name="subscribe-to-events-for-a-resource-group-and-filter-for-a-resource-with-powershell"></a><span data-ttu-id="68a00-103">Subscribe to events for a resource group and filter for a resource with PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a00-103">Subscribe to events for a resource group and filter for a resource with PowerShell</span></span>

<span data-ttu-id="68a00-104">This script creates an Event Grid subscription to the events for a resource group.</span><span class="sxs-lookup"><span data-stu-id="68a00-104">This script creates an Event Grid subscription to the events for a resource group.</span></span> <span data-ttu-id="68a00-105">It uses a filter to get only events for a specified resource in the resource group.</span><span class="sxs-lookup"><span data-stu-id="68a00-105">It uses a filter to get only events for a specified resource in the resource group.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="68a00-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="68a00-106">Sample script</span></span>

```powershell
# Provide an endpoint for handling the events.
$myEndpoint = "<endpoint URL>"

# Select the Azure subscription that contains the resource group.
Set-AzureRmContext -Subscription "Contoso Subscription"

# Get the resource ID to filter events
$resourceId = (Get-AzureRmResource -ResourceName demoSecurityGroup -ResourceGroupName myResourceGroup).ResourceId

# Subscribe to the resource group. Provide the name of the resource group you want to subscribe to.
New-AzureRmEventGridSubscription `
  -Endpoint $myEndpoint `
  -EventSubscriptionName demoSubscriptionToResourceGroup `
  -ResourceGroupName myResourceGroup `
  -SubjectBeginsWith $resourceId
```

## <a name="script-explanation"></a><span data-ttu-id="68a00-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="68a00-107">Script explanation</span></span>

<span data-ttu-id="68a00-108">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="68a00-108">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="68a00-109">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="68a00-109">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="68a00-110">Command</span><span class="sxs-lookup"><span data-stu-id="68a00-110">Command</span></span> | <span data-ttu-id="68a00-111">Notes</span><span class="sxs-lookup"><span data-stu-id="68a00-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="68a00-112">New-AzureRmEventGridSubscription</span><span class="sxs-lookup"><span data-stu-id="68a00-112">New-AzureRmEventGridSubscription</span></span>](https://docs.microsoft.com/powershell/module/azurerm.eventgrid/new-azurermeventgridsubscription) | <span data-ttu-id="68a00-113">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="68a00-113">Create an Event Grid subscription.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68a00-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="68a00-114">Next steps</span></span>

* <span data-ttu-id="68a00-115">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="68a00-115">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span></span>
* <span data-ttu-id="68a00-116">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="68a00-116">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span></span>
