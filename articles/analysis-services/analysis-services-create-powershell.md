---
title: Quickstart - Create an Azure Analysis Services server by using PowerShell | Microsoft Docs
description: Learn how to create an Azure Analysis Services server by using PowerShell
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: quickstart
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 9149f15d0503b9a39ac67d9c3f6fc1ddde7e03bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967816"
---
# <a name="quickstart-create-a-server---powershell"></a><span data-ttu-id="67a5a-103">Quickstart: Create a server - PowerShell</span><span class="sxs-lookup"><span data-stu-id="67a5a-103">Quickstart: Create a server - PowerShell</span></span>

<span data-ttu-id="67a5a-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="67a5a-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in your Azure subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67a5a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="67a5a-105">Prerequisites</span></span>

- <span data-ttu-id="67a5a-106">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span><span class="sxs-lookup"><span data-stu-id="67a5a-106">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
- <span data-ttu-id="67a5a-107">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span><span class="sxs-lookup"><span data-stu-id="67a5a-107">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="67a5a-108">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="67a5a-108">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
- <span data-ttu-id="67a5a-109">**Azure PowerShell module version 4.0 or later**.</span><span class="sxs-lookup"><span data-stu-id="67a5a-109">**Azure PowerShell module version 4.0 or later**.</span></span> <span data-ttu-id="67a5a-110">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="67a5a-110">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="67a5a-111">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="67a5a-111">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="67a5a-112">Import AzureRm.AnalysisServices module</span><span class="sxs-lookup"><span data-stu-id="67a5a-112">Import AzureRm.AnalysisServices module</span></span>

<span data-ttu-id="67a5a-113">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span><span class="sxs-lookup"><span data-stu-id="67a5a-113">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="67a5a-114">Load the AzureRm.AnalysisServices module into your PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="67a5a-114">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="log-in-to-azure"></a><span data-ttu-id="67a5a-115">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="67a5a-115">Log in to Azure</span></span>

<span data-ttu-id="67a5a-116">Log in to your Azure subscription by using the [Connect-AzureRmAccount](/powershell/module/azurerm.profile/connect-azurermaccount) command.</span><span class="sxs-lookup"><span data-stu-id="67a5a-116">Log in to your Azure subscription by using the [Connect-AzureRmAccount](/powershell/module/azurerm.profile/connect-azurermaccount) command.</span></span> <span data-ttu-id="67a5a-117">Follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="67a5a-117">Follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="67a5a-118">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="67a5a-118">Create a resource group</span></span>

<span data-ttu-id="67a5a-119">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="67a5a-119">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="67a5a-120">When you create your server, you must specify a resource group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="67a5a-120">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="67a5a-121">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="67a5a-121">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="67a5a-122">The following example creates a resource group named `myResourceGroup` in the West US region.</span><span class="sxs-lookup"><span data-stu-id="67a5a-122">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "WestUS"
```

## <a name="create-a-server"></a><span data-ttu-id="67a5a-123">Create a server</span><span class="sxs-lookup"><span data-stu-id="67a5a-123">Create a server</span></span>

<span data-ttu-id="67a5a-124">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span><span class="sxs-lookup"><span data-stu-id="67a5a-124">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="67a5a-125">The following example creates a server named myServer in myResourceGroup, in the WestUS region, at the D1 (free) tier, and specifies philipc@adventureworks.com as a server administrator.</span><span class="sxs-lookup"><span data-stu-id="67a5a-125">The following example creates a server named myServer in myResourceGroup, in the WestUS region, at the D1 (free) tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myserver" -Location WestUS -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="67a5a-126">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="67a5a-126">Clean up resources</span></span>

<span data-ttu-id="67a5a-127">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span><span class="sxs-lookup"><span data-stu-id="67a5a-127">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="67a5a-128">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span><span class="sxs-lookup"><span data-stu-id="67a5a-128">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="67a5a-129">The following example removes the server created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="67a5a-129">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myserver" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="67a5a-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="67a5a-130">Next steps</span></span>

<span data-ttu-id="67a5a-131">In this quickstart, you learned how to create a server in your Azure subscription by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67a5a-131">In this quickstart, you learned how to create a server in your Azure subscription by using PowerShell.</span></span> <span data-ttu-id="67a5a-132">Now that you have server, you can help secure it by configuring an (optional) server firewall.</span><span class="sxs-lookup"><span data-stu-id="67a5a-132">Now that you have server, you can help secure it by configuring an (optional) server firewall.</span></span> <span data-ttu-id="67a5a-133">You can also add a basic sample data model to your server right from the portal.</span><span class="sxs-lookup"><span data-stu-id="67a5a-133">You can also add a basic sample data model to your server right from the portal.</span></span> <span data-ttu-id="67a5a-134">Having a sample model is helpful when learning about configuring model database roles and testing client connections.</span><span class="sxs-lookup"><span data-stu-id="67a5a-134">Having a sample model is helpful when learning about configuring model database roles and testing client connections.</span></span> <span data-ttu-id="67a5a-135">To learn more, continue to the tutorial for adding a sample model.</span><span class="sxs-lookup"><span data-stu-id="67a5a-135">To learn more, continue to the tutorial for adding a sample model.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="67a5a-136">[Quickstart: Configure server firewall - Portal](analysis-services-qs-firewall.md)    </span><span class="sxs-lookup"><span data-stu-id="67a5a-136">[Quickstart: Configure server firewall - Portal](analysis-services-qs-firewall.md)    </span></span>  
> [!div class="nextstepaction"]
> [<span data-ttu-id="67a5a-137">Tutorial: Add a sample model to your server</span><span class="sxs-lookup"><span data-stu-id="67a5a-137">Tutorial: Add a sample model to your server</span></span>](analysis-services-create-sample-model.md)