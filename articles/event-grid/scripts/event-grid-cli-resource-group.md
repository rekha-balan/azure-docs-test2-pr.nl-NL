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
# <a name="subscribe-to-events-for-a-resource-group-with-azure-cli"></a>Subscribe to events for a resource group with Azure CLI

This script creates an Event Grid subscription to the events for a resource group. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-resource-group/subscribe-to-resource-group.sh "Subscribe to resource group")]

## <a name="script-explanation"></a>Script explanation

This script uses the following command to create the event subscription. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az eventgrid event-subscription create](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | Create an Event Grid subscription. |


## <a name="next-steps"></a>Next steps

* For information about querying subscriptions, see [Query Event Grid subscriptions](../query-event-subscriptions.md).
* For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).
