---
title: Create an Azure API Management instance using PowerShell | Microsoft Docs
description: Follow the steps of this tutorial to create a new Azure API Management instance.
services: api-management
documentationcenter: ''
author: vladvino
manager: cflower
editor: ''
ms.service: api-management
ms.workload: integration
ms.topic: quickstart
ms.custom: mvc
ms.date: 11/15/2017
ms.author: apimpm
ms.openlocfilehash: 8ed6df3a0aee500192e401f1089925bf6e2d84d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968098"
---
# <a name="create-a-new-azure-api-management-service-instance"></a><span data-ttu-id="6b274-103">Create a new Azure API Management service instance</span><span class="sxs-lookup"><span data-stu-id="6b274-103">Create a new Azure API Management service instance</span></span>

<span data-ttu-id="6b274-104">Azure API Management (APIM) helps organizations publish APIs to external, partner, and internal developers to unlock the potential of their data and services.</span><span class="sxs-lookup"><span data-stu-id="6b274-104">Azure API Management (APIM) helps organizations publish APIs to external, partner, and internal developers to unlock the potential of their data and services.</span></span> <span data-ttu-id="6b274-105">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security, and protection.</span><span class="sxs-lookup"><span data-stu-id="6b274-105">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security, and protection.</span></span> <span data-ttu-id="6b274-106">APIM  enables you to create and manage modern API gateways for existing backend services hosted anywhere.</span><span class="sxs-lookup"><span data-stu-id="6b274-106">APIM  enables you to create and manage modern API gateways for existing backend services hosted anywhere.</span></span> <span data-ttu-id="6b274-107">For more information, see the [Overview](api-management-key-concepts.md) topic.</span><span class="sxs-lookup"><span data-stu-id="6b274-107">For more information, see the [Overview](api-management-key-concepts.md) topic.</span></span>

<span data-ttu-id="6b274-108">This quickstart describes the steps for creating a new API Management instance using the PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="6b274-108">This quickstart describes the steps for creating a new API Management instance using the PowerShell scripts.</span></span> <span data-ttu-id="6b274-109">The quickstart shows you how to use the **Azure Cloud Shell** that you can run from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6b274-109">The quickstart shows you how to use the **Azure Cloud Shell** that you can run from Azure portal.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="6b274-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="6b274-110">Log in to Azure</span></span>

<span data-ttu-id="6b274-111">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6b274-111">Log in to the Azure portal at http://portal.azure.com.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="6b274-112">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="6b274-112">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="6b274-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="6b274-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="6b274-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6b274-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="6b274-115">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="6b274-115">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="6b274-116">Create resource group</span><span class="sxs-lookup"><span data-stu-id="6b274-116">Create resource group</span></span>

<span data-ttu-id="6b274-117">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="6b274-117">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="6b274-118">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="6b274-118">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroup -Location WestUS
```

## <a name="create-an-api-management-service"></a><span data-ttu-id="6b274-119">Create an API Management service</span><span class="sxs-lookup"><span data-stu-id="6b274-119">Create an API Management service</span></span>

<span data-ttu-id="6b274-120">This is long running operation and could take up to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="6b274-120">This is long running operation and could take up to 15 minutes.</span></span>

```azurepowershell-interactive
New-AzureRmApiManagement -ResourceGroupName "myResourceGroup" -Location "West US" -Name "apim-name" -Organization "myOrganization" -AdminEmail "myEmail" -Sku "Developer"
```

## <a name="clean-up-resources"></a><span data-ttu-id="6b274-121">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6b274-121">Clean up resources</span></span>

<span data-ttu-id="6b274-122">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6b274-122">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6b274-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b274-123">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b274-124">Import and publish your first API</span><span class="sxs-lookup"><span data-stu-id="6b274-124">Import and publish your first API</span></span>](import-and-publish.md)
