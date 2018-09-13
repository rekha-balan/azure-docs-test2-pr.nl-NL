---
title: Azure CLI script sample - Subscribe to Azure subscription | Microsoft Docs
description: Azure CLI Script Sample - Subscribe to Azure subscription
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
ms.openlocfilehash: ac02c5515f598daf4aa91879af78341969718163
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868281"
---
# <a name="subscribe-to-events-for-an-azure-subscription-with-azure-cli"></a><span data-ttu-id="b769a-103">Subscribe to events for an Azure subscription with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b769a-103">Subscribe to events for an Azure subscription with Azure CLI</span></span>

<span data-ttu-id="b769a-104">This script creates an Event Grid subscription to the events for an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b769a-104">This script creates an Event Grid subscription to the events for an Azure subscription.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b769a-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="b769a-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-azure-subscription/subscribe-to-azure-subscription.sh "Subscribe to Azure subscription")]

## <a name="script-explanation"></a><span data-ttu-id="b769a-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b769a-106">Script explanation</span></span>

<span data-ttu-id="b769a-107">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="b769a-107">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="b769a-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="b769a-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="b769a-109">Command</span><span class="sxs-lookup"><span data-stu-id="b769a-109">Command</span></span> | <span data-ttu-id="b769a-110">Notes</span><span class="sxs-lookup"><span data-stu-id="b769a-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b769a-111">az eventgrid event-subscription create</span><span class="sxs-lookup"><span data-stu-id="b769a-111">az eventgrid event-subscription create</span></span>](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | <span data-ttu-id="b769a-112">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="b769a-112">Create an Event Grid subscription.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b769a-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="b769a-113">Next steps</span></span>

* <span data-ttu-id="b769a-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="b769a-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span></span>
* <span data-ttu-id="b769a-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="b769a-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
