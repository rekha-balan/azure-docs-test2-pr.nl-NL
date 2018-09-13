---
title: Azure CLI script sample - Subscribe to resource group | Microsoft Docs
description: Azure CLI Script Sample - Subscribe to resource group
services: event-grid
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2018
ms.author: tomfitz
ms.openlocfilehash: f13ba64825cb760412f8e4e73f1fc3a7daa8edd8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865699"
---
# <a name="subscribe-to-events-for-a-resource-group-with-azure-cli"></a><span data-ttu-id="c35d0-103">Subscribe to events for a resource group with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c35d0-103">Subscribe to events for a resource group with Azure CLI</span></span>

<span data-ttu-id="c35d0-104">This script creates an Event Grid subscription to the events for a resource group.</span><span class="sxs-lookup"><span data-stu-id="c35d0-104">This script creates an Event Grid subscription to the events for a resource group.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c35d0-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="c35d0-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-resource-group/subscribe-to-resource-group.sh "Subscribe to resource group")]

## <a name="script-explanation"></a><span data-ttu-id="c35d0-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c35d0-106">Script explanation</span></span>

<span data-ttu-id="c35d0-107">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="c35d0-107">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="c35d0-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c35d0-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c35d0-109">Command</span><span class="sxs-lookup"><span data-stu-id="c35d0-109">Command</span></span> | <span data-ttu-id="c35d0-110">Notes</span><span class="sxs-lookup"><span data-stu-id="c35d0-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c35d0-111">az eventgrid event-subscription create</span><span class="sxs-lookup"><span data-stu-id="c35d0-111">az eventgrid event-subscription create</span></span>](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | <span data-ttu-id="c35d0-112">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="c35d0-112">Create an Event Grid subscription.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c35d0-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="c35d0-113">Next steps</span></span>

* <span data-ttu-id="c35d0-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="c35d0-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span></span>
* <span data-ttu-id="c35d0-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c35d0-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
