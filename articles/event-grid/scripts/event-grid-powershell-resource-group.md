---
title: Azure PowerShell script sample - Subscribe to resource group | Microsoft Docs
description: Azure PowerShell script sample - Subscribe to resource group
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
ms.openlocfilehash: 1a3a32003c76c0132ee0503af996e3f323a08577
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856467"
---
# <a name="subscribe-to-events-for-a-resource-group-with-powershell"></a>Subscribe to events for a resource group with PowerShell

This script creates an Event Grid subscription to the events for a resource group.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-powershell[main](../../../powershell_scripts/event-grid/subscribe-to-resource-group/subscribe-to-resource-group.ps1 "Subscribe to resource group")]

## <a name="script-explanation"></a>Script explanation

This script uses the following command to create the event subscription. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [New-AzureRmEventGridSubscription](https://docs.microsoft.com/powershell/module/azurerm.eventgrid/new-azurermeventgridsubscription) | Create an Event Grid subscription. |

## <a name="next-steps"></a>Next steps

* For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).
* For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).
