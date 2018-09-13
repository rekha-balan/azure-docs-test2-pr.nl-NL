---
title: 'PowerShell script: Set allowed VM sizes in Azure Lab Services | Microsoft Docs'
description: This PowerShell script sets allowed VM sizes in Azure Lab Services.
services: lab-services
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2018
ms.author: spelluru
ms.openlocfilehash: 559e74675a5d113584dca21979c20462c9cdf19c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871076"
---
# <a name="use-powershell-to-set-allowed-vm-sizes-in-azure-lab-services"></a>Use PowerShell to set allowed VM sizes in Azure Lab Services

This sample PowerShell script sets allowed virtual machine (VM) sizes in Azure Lab Services.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a>Prerequisites
* **A lab**. The script requires you to have an existing lab. 

## <a name="sample-script"></a>Sample script

[!code-powershell[main](../../../powershell_scripts/devtest-lab/set-allowed-vm-sizes-in-lab/set-allowed-vm-sizes-in-lab.ps1 "Add external user to a lab")]

## <a name="script-explanation"></a>Script explanation

This script uses the following commands: 

| Command | Notes |
|---|---|
| [Find-AzureRmResource](/powershell/module/azurerm.resources/find-azurermresource) | Searches for resources based on specified parameters. |
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Gets resources. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Modifies a resource. |
| [New-AzureRmResource](/powershell/module/azurerm.resources/new-azurermresource) | Create a resource. |

## <a name="next-steps"></a>Next steps

For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).

Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).
