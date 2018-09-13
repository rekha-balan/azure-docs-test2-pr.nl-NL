---
title: Azure Government Connect with PowerShell | Microsoft Docs
description: Information on connecting your subscription in Azure Government with PowerShell
services: azure-government
cloud: gov
documentationcenter: ''
author: zakramer
manager: liki
ms.assetid: 47e5e535-baa0-457e-8c41-f9fd65478b38
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 02/13/2017
ms.author: zakramer
ms.openlocfilehash: de36ddf8e270f12c886877d7c78237106aabc38c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562873"
---
# <a name="connect-to-azure-government-with-powershell"></a>Connect to Azure Government with PowerShell
To use Azure PowerShell with Azure Government, you need to connect to Azure Government instead of Azure Public. Azure PowerShell can be used to manage a large subscription through script or to access features that are not currently available in the Azure portal. If you have used PowerShell in Azure Public, it is mostly the same.  The differences in Azure Government are:

* Connecting your account
* Region names

> [!NOTE]
> If you have not used PowerShell yet, check out the [Introduction to Azure PowerShell](/powershell/azureps-cmdlets-docs).
> 
> 

When you start PowerShell, you have to tell Azure PowerShell to connect to Azure Government by specifying an environment parameter.  The parameter ensures that PowerShell is connecting to the correct endpoints.  The collection of endpoints is determined when you connect log in to your account.  Different APIs require different versions of the environment switch:

| Connection type | Command |
| --- | --- |
| [Azure (Classic deployment model)](https://msdn.microsoft.com/library/dn708504.aspx) commands |`Add-AzureAccount -Environment AzureUSGovernment` |
| [Azure (Resource Manager deployment model)](https://msdn.microsoft.com/library/mt125356.aspx) commands |`Login-AzureRmAccount -EnvironmentName AzureUSGovernment` |
| [Azure Active Directory (Classic deployment model)](https://msdn.microsoft.com/library/azure/jj151815.aspx) commands |`Connect-MsolService -AzureEnvironment UsGovernment` |
| [Azure Active Directory (Resource Manager deployment model)](https://msdn.microsoft.com/library/azure/mt757189.aspx) commands |`Connect-AzureAD -AzureEnvironmentName AzureUSGovernment` |

You may also use the `Environment` switch when connecting to a storage account using `New-AzureStorageContext` and specify `AzureUSGovernment`.

### <a name="determining-region"></a>Determining region
Once you are connected, there is one additional difference – The regions used to target a service.  Every Azure cloud has different regions.  You can see them listed on the service availability page.  You normally use the region in the `Location` parameter for a command.

There is one catch.  The Azure Government region display names have different formatting than their common names:

| Common Name | Display Name | Location Name |
| --- | --- | --- |
| US Gov Virginia |`USGov Virginia` | `usgovvirginia` |
| US Gov Iowa |`USGov Iowa` | `usgoviowa` |
| US DoD East |`USDoD East` | `usdodeast` |
| US DoD Central |`USDoD Central` | `usdodcentral` |

> [!NOTE]
> There is no space between `US` and `Gov` or `US` and `DoD` when using the `Location` parameter.
> 
> 

> [!NOTE]
> As is true with PowerShell for Azure Public, you can use either the Display Name or the Location Name for the `Location` parameter.
>
>

If you ever want to validate the available regions in Azure Government, you can run the following commands and print the current list:

    Get-AzureLocation

If you are curious about the available environments across Azure, you can run:

    Get-AzureEnvironment
