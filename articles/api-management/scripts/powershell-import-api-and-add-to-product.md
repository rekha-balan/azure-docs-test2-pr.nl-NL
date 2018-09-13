---
title: Azure PowerShell Script Sample - Import an API | Microsoft Docs
description: Azure PowerShell Script Sample - Import an API
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
ms.openlocfilehash: c08a0a4892d1c0f5780f5b6ef9cc437078489971
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865980"
---
# <a name="import-an-api"></a><span data-ttu-id="889a0-103">Import an API</span><span class="sxs-lookup"><span data-stu-id="889a0-103">Import an API</span></span>

<span data-ttu-id="889a0-104">This sample script imports an API and adds it to an API Management product.</span><span class="sxs-lookup"><span data-stu-id="889a0-104">This sample script imports an API and adds it to an API Management product.</span></span> 

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="889a0-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="889a0-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="889a0-106">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="889a0-106">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="889a0-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="889a0-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="889a0-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="889a0-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="889a0-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="889a0-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/api-management/import-api-and-add-to-product/import_an_api_and_add_to_product.ps1 "Import an API")]

## <a name="clean-up-resources"></a><span data-ttu-id="889a0-110">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="889a0-110">Clean up resources</span></span>

<span data-ttu-id="889a0-111">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span><span class="sxs-lookup"><span data-stu-id="889a0-111">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="889a0-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="889a0-112">Next steps</span></span>

<span data-ttu-id="889a0-113">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="889a0-113">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="889a0-114">Additional Azure Powershell samples for Azure API Management can be found in the [PowerShell samples](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="889a0-114">Additional Azure Powershell samples for Azure API Management can be found in the [PowerShell samples](../powershell-samples.md).</span></span>
