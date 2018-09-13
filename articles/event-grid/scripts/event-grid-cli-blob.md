---
title: Azure CLI script sample - Subscribe to Blob storage account | Microsoft Docs
description: Azure CLI Script Sample - Subscribe to Blob storage account
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
ms.openlocfilehash: 434d94b9ba2c06c85c84c17be68d8493e8344d2b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856488"
---
# <a name="subscribe-to-events-for-a-blob-storage-account-with-azure-cli"></a><span data-ttu-id="39fc4-103">Subscribe to events for a Blob storage account with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39fc4-103">Subscribe to events for a Blob storage account with Azure CLI</span></span>

<span data-ttu-id="39fc4-104">This script creates an Event Grid subscription to the events for a Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="39fc4-104">This script creates an Event Grid subscription to the events for a Blob storage account.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="39fc4-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="39fc4-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-blob-storage/subscribe-to-blob-storage.sh "Subscribe to Blob storage")]

## <a name="script-explanation"></a><span data-ttu-id="39fc4-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="39fc4-106">Script explanation</span></span>

<span data-ttu-id="39fc4-107">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="39fc4-107">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="39fc4-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="39fc4-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="39fc4-109">Command</span><span class="sxs-lookup"><span data-stu-id="39fc4-109">Command</span></span> | <span data-ttu-id="39fc4-110">Notes</span><span class="sxs-lookup"><span data-stu-id="39fc4-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39fc4-111">az eventgrid event-subscription create</span><span class="sxs-lookup"><span data-stu-id="39fc4-111">az eventgrid event-subscription create</span></span>](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | <span data-ttu-id="39fc4-112">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="39fc4-112">Create an Event Grid subscription.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="39fc4-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="39fc4-113">Next steps</span></span>

* <span data-ttu-id="39fc4-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="39fc4-114">For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).</span></span>
* <span data-ttu-id="39fc4-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="39fc4-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
