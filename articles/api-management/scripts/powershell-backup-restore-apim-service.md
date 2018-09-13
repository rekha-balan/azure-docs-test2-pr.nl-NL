---
title: Azure PowerShell Script Sample - Backup and restore service | Microsoft Docs
description: Azure PowerShell Script Sample - Backup and restore service
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.devlang: na
ms.topic: sample
ms.date: 11/16/2017
ms.author: apimpm
ms.custom: mvc
ms.openlocfilehash: f8283a5720b457b74c26852b01ad30a423bd450d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868484"
---
# <a name="backup-and-restore-service"></a><span data-ttu-id="40ff7-103">Backup and restore service</span><span class="sxs-lookup"><span data-stu-id="40ff7-103">Backup and restore service</span></span>

<span data-ttu-id="40ff7-104">This sample shown in this article shows how to backup and restore the API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="40ff7-104">This sample shown in this article shows how to backup and restore the API Management service instance.</span></span> 

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="40ff7-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="40ff7-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="40ff7-106">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="40ff7-106">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="40ff7-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="40ff7-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="40ff7-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="40ff7-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="40ff7-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="40ff7-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/api-management/backup-restore-apim-service/backup_restore_apim_service.ps1 "Backup and restore the APIM service instance")]

## <a name="clean-up-resources"></a><span data-ttu-id="40ff7-110">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="40ff7-110">Clean up resources</span></span>

<span data-ttu-id="40ff7-111">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span><span class="sxs-lookup"><span data-stu-id="40ff7-111">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="40ff7-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="40ff7-112">Next steps</span></span>

<span data-ttu-id="40ff7-113">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="40ff7-113">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="40ff7-114">Additional Azure Powershell samples for Azure API Management can be found in the [PowerShell samples](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="40ff7-114">Additional Azure Powershell samples for Azure API Management can be found in the [PowerShell samples](../powershell-samples.md).</span></span>
