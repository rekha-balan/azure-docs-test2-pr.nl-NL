---
title: Azure PowerShell Script Sample -  Create a Log Analytics workspace| Microsoft Docs
description: Azure PowerShell Script Sample -  Create a Log Analytics workspace to
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: log-analytics
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/07/2017
ms.author: magoedte
ms.openlocfilehash: 30d036ae56acc3a798d2776f292243f65cbea43d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865775"
---
# <a name="create-a-log-analytics-workspace-with-powershell"></a>Create a Log Analytics workspace with PowerShell

This script gets you up and running quickly with an Azure Log Analytics workspace, which is required if you want to start collecting, analyzing, and taking action on data.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-powershell[main](../../../powershell_scripts/log-analytics/log-analytics-create-new-resource/log-analytics-create-new-resource.ps1 "Create new Log Analytics workspace")]

## <a name="script-explanation"></a>Script explanation

This script uses following commands to create a new Log Analytics workspace in your  subscription. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [Get-AzureRmOperationalInsightsWorkspace](/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightsworkspace) | Gets information about an existing workspace. |
| [New-AzureRmOperationalInsightsWorkspace](/powershell/module/azurerm.operationalinsights/new-azurermoperationalinsightsworkspace) | Creates a workspace in the specified resource group and location. |


## <a name="next-steps"></a>Next steps

For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).

