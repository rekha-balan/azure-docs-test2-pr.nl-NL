---
title: Delete an Azure cluster and its resources | Microsoft Docs
description: Learn how to completely delete a Service Fabric cluster either deleting the resource group containing the cluster or by selectively deleting resources.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: ''
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: chackdan
ms.openlocfilehash: 51c1d98c5e8f7208b051d2adcef2cb3b37ef431f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551517"
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="e8b0a-103">Delete a Service Fabric cluster on Azure and the resources it uses</span><span class="sxs-lookup"><span data-stu-id="e8b0a-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="e8b0a-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="e8b0a-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="e8b0a-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span><span class="sxs-lookup"><span data-stu-id="e8b0a-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="e8b0a-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="e8b0a-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span><span class="sxs-lookup"><span data-stu-id="e8b0a-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="e8b0a-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="e8b0a-110">You can delete the resource group using PowerShell or through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="e8b0a-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="e8b0a-112">Delete the resource group using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8b0a-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="e8b0a-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e8b0a-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="e8b0a-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azureps-cmdlets-docs)</span><span class="sxs-lookup"><span data-stu-id="e8b0a-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azureps-cmdlets-docs)</span></span>

<span data-ttu-id="e8b0a-116">Open a PowerShell window and run the following PS cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e8b0a-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="e8b0a-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="e8b0a-118">On confirmation the RG and all the resources it contains are deleted.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="e8b0a-119">Delete a resource group in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e8b0a-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="e8b0a-120">Login to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8b0a-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e8b0a-121">Navigate to the Service Fabric cluster you want to delete.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="e8b0a-122">Click on the Resource Group name on the cluster essentials page.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="e8b0a-123">This brings up the **Resource Group Essentials** page.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="e8b0a-124">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-124">Click **Delete**.</span></span>
6. <span data-ttu-id="e8b0a-125">Follow the instructions on that page to complete the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Resource Group Delete][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="e8b0a-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span><span class="sxs-lookup"><span data-stu-id="e8b0a-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="e8b0a-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="e8b0a-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="e8b0a-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="e8b0a-131">You can use them to decide which resources you want to delete.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="e8b0a-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span><span class="sxs-lookup"><span data-stu-id="e8b0a-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="e8b0a-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="e8b0a-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="e8b0a-134">Delete specific resources in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e8b0a-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="e8b0a-135">Login to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8b0a-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e8b0a-136">Navigate to the Service Fabric cluster you want to delete.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="e8b0a-137">Go to **All settings** on the essentials blade.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="e8b0a-138">Click on **Tags** under **Resource Management** in the settings blade.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="e8b0a-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Resource Tags][ResourceTags]
6. <span data-ttu-id="e8b0a-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Tagged Resources][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="e8b0a-143">Delete the resources using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8b0a-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="e8b0a-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e8b0a-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="e8b0a-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="e8b0a-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azureps-cmdlets-docs)</span><span class="sxs-lookup"><span data-stu-id="e8b0a-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azureps-cmdlets-docs)</span></span>

<span data-ttu-id="e8b0a-147">Open a PowerShell window and run the following PS cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e8b0a-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="e8b0a-148">For each of the resources you want to delete, run the following:</span><span class="sxs-lookup"><span data-stu-id="e8b0a-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="e8b0a-149">To delete the cluster resource, run the following:</span><span class="sxs-lookup"><span data-stu-id="e8b0a-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="e8b0a-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8b0a-150">Next steps</span></span>
<span data-ttu-id="e8b0a-151">Read the following to also learn about upgrading a cluster and partitioning services:</span><span class="sxs-lookup"><span data-stu-id="e8b0a-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="e8b0a-152">Learn about cluster upgrades</span><span class="sxs-lookup"><span data-stu-id="e8b0a-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="e8b0a-153">Learn about partitioning stateful services for maximum scale</span><span class="sxs-lookup"><span data-stu-id="e8b0a-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-delete/TaggedResources.PNG



