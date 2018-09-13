---
title: Azure PowerShell Script Sample - Set up custom domain | Microsoft Docs
description: Azure PowerShell Script Sample - Set up custom domain
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.devlang: na
ms.topic: sample
ms.date: 12/14/2017
ms.author: apimpm
ms.custom: mvc
ms.openlocfilehash: b120f3d2731601652d46f71206637bacdda023cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864732"
---
# <a name="set-up-custom-domain"></a><span data-ttu-id="55fca-103">Set up custom domain</span><span class="sxs-lookup"><span data-stu-id="55fca-103">Set up custom domain</span></span>

<span data-ttu-id="55fca-104">This sample script sets up custom domain on proxy and portal endpoint of the API Management service.</span><span class="sxs-lookup"><span data-stu-id="55fca-104">This sample script sets up custom domain on proxy and portal endpoint of the API Management service.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="55fca-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="55fca-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="55fca-106">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="55fca-106">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="55fca-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="55fca-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="55fca-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="55fca-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="55fca-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="55fca-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/api-management/setup-custom-domain/setup_custom_domain.ps1 "Set up custom domain")]

## <a name="clean-up-resources"></a><span data-ttu-id="55fca-110">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="55fca-110">Clean up resources</span></span>

<span data-ttu-id="55fca-111">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span><span class="sxs-lookup"><span data-stu-id="55fca-111">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```

[!INCLUDE [api-management-custom-domain](../../../includes/api-management-custom-domain.md)]

## <a name="next-steps"></a><span data-ttu-id="55fca-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="55fca-112">Next steps</span></span>

<span data-ttu-id="55fca-113">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55fca-113">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="55fca-114">Additional Azure Powershell samples for Azure API Management can be found in the [PowerShell samples](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="55fca-114">Additional Azure Powershell samples for Azure API Management can be found in the [PowerShell samples](../powershell-samples.md).</span></span>
