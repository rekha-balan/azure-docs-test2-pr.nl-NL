---
title: Migrate Automation Account and Resources | Microsoft Docs
description: This article describes how to move an Automation Account in Azure Automation and associated resources from one subscription to another.
services: automation
documentationcenter: ''
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: b8402b82fee713be4405e71cbee0571b09649f3c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548952"
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="ba813-103">Migrate Automation Account and resources</span><span class="sxs-lookup"><span data-stu-id="ba813-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="ba813-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ba813-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="ba813-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span><span class="sxs-lookup"><span data-stu-id="ba813-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="ba813-106">The destination subscription/resource group must be in same region as the source.</span><span class="sxs-lookup"><span data-stu-id="ba813-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="ba813-107">Meaning, Automation accounts cannot be moved across regions.</span><span class="sxs-lookup"><span data-stu-id="ba813-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="ba813-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span><span class="sxs-lookup"><span data-stu-id="ba813-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="ba813-109">Write and delete operations are blocked on the groups until the move completes.</span><span class="sxs-lookup"><span data-stu-id="ba813-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="ba813-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span><span class="sxs-lookup"><span data-stu-id="ba813-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="ba813-111">This feature does not support moving Classic automation resources.</span><span class="sxs-lookup"><span data-stu-id="ba813-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="ba813-112">To move the Automation Account using the portal</span><span class="sxs-lookup"><span data-stu-id="ba813-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="ba813-113">From your Automation account, click **Move** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="ba813-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="ba813-114">![Move option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="ba813-114">![Move option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="ba813-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span><span class="sxs-lookup"><span data-stu-id="ba813-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="ba813-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span><span class="sxs-lookup"><span data-stu-id="ba813-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="ba813-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba813-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="ba813-118">![Move Resources Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="ba813-118">![Move Resources Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="ba813-119">This action will take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="ba813-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="ba813-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span><span class="sxs-lookup"><span data-stu-id="ba813-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="ba813-121">To move the Automation Account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba813-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="ba813-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span><span class="sxs-lookup"><span data-stu-id="ba813-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="ba813-123">The first example shows how to move an Automation account to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="ba813-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="ba813-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span><span class="sxs-lookup"><span data-stu-id="ba813-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="ba813-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span><span class="sxs-lookup"><span data-stu-id="ba813-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="ba813-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span><span class="sxs-lookup"><span data-stu-id="ba813-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="ba813-127">As with the previous example, you will be prompted to confirm the move.</span><span class="sxs-lookup"><span data-stu-id="ba813-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ba813-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba813-128">Next steps</span></span>
* <span data-ttu-id="ba813-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="ba813-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="ba813-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="ba813-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="ba813-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ba813-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="ba813-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba813-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>


