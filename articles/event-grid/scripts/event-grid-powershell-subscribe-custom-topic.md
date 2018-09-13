---
title: Azure PowerShell script sample - Subscribe to custom topic | Microsoft Docs
description: Azure PowerShell script sample - Subscribe to custom topic
services: event-grid
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.devlang: powershell
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2018
ms.author: tomfitz
ms.openlocfilehash: 9c779e1f214369de9390e2c0f1037042c161c8aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865669"
---
# <a name="subscribe-to-events-for-a-custom-topic-with-powershell"></a><span data-ttu-id="a5af0-103">Subscribe to events for a custom topic with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5af0-103">Subscribe to events for a custom topic with PowerShell</span></span>

<span data-ttu-id="a5af0-104">This script creates an Event Grid subscription to the events for a custom topic.</span><span class="sxs-lookup"><span data-stu-id="a5af0-104">This script creates an Event Grid subscription to the events for a custom topic.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a5af0-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="a5af0-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/event-grid/subscribe-to-custom-topic/subscribe-to-custom-topic.ps1 "Subscribe to custom topic")]

## <a name="script-explanation"></a><span data-ttu-id="a5af0-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a5af0-106">Script explanation</span></span>

<span data-ttu-id="a5af0-107">This script uses the following command to create the event subscription.</span><span class="sxs-lookup"><span data-stu-id="a5af0-107">This script uses the following command to create the event subscription.</span></span> <span data-ttu-id="a5af0-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a5af0-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="a5af0-109">Command</span><span class="sxs-lookup"><span data-stu-id="a5af0-109">Command</span></span> | <span data-ttu-id="a5af0-110">Notes</span><span class="sxs-lookup"><span data-stu-id="a5af0-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a5af0-111">New-AzureRmEventGridSubscription</span><span class="sxs-lookup"><span data-stu-id="a5af0-111">New-AzureRmEventGridSubscription</span></span>](https://docs.microsoft.com/powershell/module/azurerm.eventgrid/new-azurermeventgridsubscription) | <span data-ttu-id="a5af0-112">Create an Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="a5af0-112">Create an Event Grid subscription.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a5af0-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5af0-113">Next steps</span></span>

* <span data-ttu-id="a5af0-114">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5af0-114">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span></span>
* <span data-ttu-id="a5af0-115">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a5af0-115">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span></span>
