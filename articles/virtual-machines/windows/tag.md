---
title: How to tag a Windows VM resource in Azure | Microsoft Docs
description: Learn about tagging a Windows virtual machine created in Azure using the Resource Manager deployment model
services: virtual-machines-windows
documentationcenter: ''
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 8b3bc5d23ac862239cf9171a7726e832c1420945
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555554"
---
# <a name="how-to-tag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="77463-103">How to tag a Windows virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="77463-103">How to tag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="77463-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="77463-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="77463-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span><span class="sxs-lookup"><span data-stu-id="77463-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="77463-106">Azure currently supports up to 15 tags per resource and resource group.</span><span class="sxs-lookup"><span data-stu-id="77463-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="77463-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span><span class="sxs-lookup"><span data-stu-id="77463-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="77463-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span><span class="sxs-lookup"><span data-stu-id="77463-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span></span> <span data-ttu-id="77463-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="77463-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="77463-110">Tagging with PowerShell</span><span class="sxs-lookup"><span data-stu-id="77463-110">Tagging with PowerShell</span></span>
<span data-ttu-id="77463-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="77463-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="77463-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77463-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span></span> <span data-ttu-id="77463-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="77463-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="77463-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77463-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="77463-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span><span class="sxs-lookup"><span data-stu-id="77463-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="77463-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span><span class="sxs-lookup"><span data-stu-id="77463-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span></span> <span data-ttu-id="77463-117">Note when updating tags through PowerShell, tags are updated as a whole.</span><span class="sxs-lookup"><span data-stu-id="77463-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="77463-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span><span class="sxs-lookup"><span data-stu-id="77463-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span></span> <span data-ttu-id="77463-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="77463-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="77463-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span><span class="sxs-lookup"><span data-stu-id="77463-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="77463-121">The second command displays the tags for the given variable.</span><span class="sxs-lookup"><span data-stu-id="77463-121">The second command displays the tags for the given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="77463-122">The third command adds an additional tag to the *$tags* variable.</span><span class="sxs-lookup"><span data-stu-id="77463-122">The third command adds an additional tag to the *$tags* variable.</span></span> <span data-ttu-id="77463-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span><span class="sxs-lookup"><span data-stu-id="77463-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="77463-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span><span class="sxs-lookup"><span data-stu-id="77463-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span></span> <span data-ttu-id="77463-125">In this case, it is MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="77463-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="77463-126">The fifth command displays all of the tags on the resource.</span><span class="sxs-lookup"><span data-stu-id="77463-126">The fifth command displays all of the tags on the resource.</span></span> <span data-ttu-id="77463-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span><span class="sxs-lookup"><span data-stu-id="77463-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="77463-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="77463-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="77463-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="77463-129">Next steps</span></span>
* <span data-ttu-id="77463-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="77463-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="77463-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="77463-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
