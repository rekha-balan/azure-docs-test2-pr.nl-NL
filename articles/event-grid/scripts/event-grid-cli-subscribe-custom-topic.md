---
title: Azure CLI script sample - Subscribe to custom topic | Microsoft Docs
description: Azure CLI Script Sample - Subscribe to custom topic
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
ms.openlocfilehash: 0c0b4c77815efc4ae3c80a8602222122254f7d88
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864575"
---
# <a name="subscribe-to-events-for-a-custom-topic-with-azure-cli"></a><span data-ttu-id="b5860-103">Subscribe to events for a custom topic with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b5860-103">Subscribe to events for a custom topic with Azure CLI</span></span>

<span data-ttu-id="b5860-104">This script creates an Event Grid subscription to the events for a custom topic.</span><span class="sxs-lookup"><span data-stu-id="b5860-104">This script creates an Event Grid subscription to the events for a custom topic.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b5860-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="b5860-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-custom-topic/subscribe-to-custom-topic.sh "Subscribe to custom topic")]

## <a name="script-explanation"></a><span data-ttu-id="b5860-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b5860-106">Script explanation</span></span>

<span data-ttu-id="b5860-107">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="b5860-107">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="b5860-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="b5860-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="b5860-109">Command</span><span class="sxs-lookup"><span data-stu-id="b5860-109">Command</span></span> | <span data-ttu-id="b5860-110">Notes</span><span class="sxs-lookup"><span data-stu-id="b5860-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b5860-111">az eventgrid event-subscription create</span><span class="sxs-lookup"><span data-stu-id="b5860-111">az eventgrid event-subscription create</span></span>](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | <span data-ttu-id="b5860-112">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="b5860-112">Create an Event Grid subscription.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b5860-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5860-113">Next steps</span></span>

* <span data-ttu-id="b5860-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="b5860-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span></span>
* <span data-ttu-id="b5860-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="b5860-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
