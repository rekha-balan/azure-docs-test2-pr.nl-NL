---
title: 'App Service on Azure Stack: Fault Domain Update | Microsoft Docs'
description: How to redistribute Azure App Service on Azure Stack across fault domains
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: anwestg
ms.openlocfilehash: acadd1adec93d10d64712a2fbedb89e098998294
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864417"
---
# <a name="how-to-redistribute-azure-app-service-on-azure-stack-across-fault-domains"></a><span data-ttu-id="e97f4-103">How to redistribute Azure App Service on Azure Stack across fault domains</span><span class="sxs-lookup"><span data-stu-id="e97f4-103">How to redistribute Azure App Service on Azure Stack across fault domains</span></span>

<span data-ttu-id="e97f4-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="e97f4-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="e97f4-105">With the 1802 update, Azure Stack now supports the distribution of workloads across fault domains, a feature that's critical for high availability.</span><span class="sxs-lookup"><span data-stu-id="e97f4-105">With the 1802 update, Azure Stack now supports the distribution of workloads across fault domains, a feature that's critical for high availability.</span></span>

>[!IMPORTANT]
><span data-ttu-id="e97f4-106">To take advantage of fault domain support, you must update your Azure Stack integrated system to 1802.</span><span class="sxs-lookup"><span data-stu-id="e97f4-106">To take advantage of fault domain support, you must update your Azure Stack integrated system to 1802.</span></span> <span data-ttu-id="e97f4-107">This document only applies to App Service resource provider deployments that were finished before the 1802 update.</span><span class="sxs-lookup"><span data-stu-id="e97f4-107">This document only applies to App Service resource provider deployments that were finished before the 1802 update.</span></span> <span data-ttu-id="e97f4-108">If you deployed App Service on Azure Stack after the 1802 update was applied to Azure Stack, the resource provider is already distributed across fault domains.</span><span class="sxs-lookup"><span data-stu-id="e97f4-108">If you deployed App Service on Azure Stack after the 1802 update was applied to Azure Stack, the resource provider is already distributed across fault domains.</span></span>

## <a name="rebalance-an-app-service-resource-provider-across-fault-domains"></a><span data-ttu-id="e97f4-109">Rebalance an App Service resource provider across fault domains</span><span class="sxs-lookup"><span data-stu-id="e97f4-109">Rebalance an App Service resource provider across fault domains</span></span>

<span data-ttu-id="e97f4-110">To redistribute the scale sets deployed for the App Service resource provider, you must perform the steps in this article for each scale set.</span><span class="sxs-lookup"><span data-stu-id="e97f4-110">To redistribute the scale sets deployed for the App Service resource provider, you must perform the steps in this article for each scale set.</span></span> <span data-ttu-id="e97f4-111">By default, the scaleset names are:</span><span class="sxs-lookup"><span data-stu-id="e97f4-111">By default, the scaleset names are:</span></span>

* <span data-ttu-id="e97f4-112">ManagementServersScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-112">ManagementServersScaleSet</span></span>
* <span data-ttu-id="e97f4-113">FrontEndsScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-113">FrontEndsScaleSet</span></span>
* <span data-ttu-id="e97f4-114">PublishersScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-114">PublishersScaleSet</span></span>
* <span data-ttu-id="e97f4-115">SharedWorkerTierScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-115">SharedWorkerTierScaleSet</span></span>
* <span data-ttu-id="e97f4-116">SmallWorkerTierScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-116">SmallWorkerTierScaleSet</span></span>
* <span data-ttu-id="e97f4-117">MediumWorkerTierScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-117">MediumWorkerTierScaleSet</span></span>
* <span data-ttu-id="e97f4-118">LargeWorkerTierScaleSet</span><span class="sxs-lookup"><span data-stu-id="e97f4-118">LargeWorkerTierScaleSet</span></span>

>[!NOTE]
> <span data-ttu-id="e97f4-119">If you don't have instances deployed in some of the worker tier scale sets, you don't need to rebalance those scale sets.</span><span class="sxs-lookup"><span data-stu-id="e97f4-119">If you don't have instances deployed in some of the worker tier scale sets, you don't need to rebalance those scale sets.</span></span> <span data-ttu-id="e97f4-120">The scale sets will be balanced correctly when you scale them out in future.</span><span class="sxs-lookup"><span data-stu-id="e97f4-120">The scale sets will be balanced correctly when you scale them out in future.</span></span>

<span data-ttu-id="e97f4-121">To scale out the scale sets, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="e97f4-121">To scale out the scale sets, follow these steps:</span></span>

1. <span data-ttu-id="e97f4-122">Sign in to the Azure Stack Administrator Portal.</span><span class="sxs-lookup"><span data-stu-id="e97f4-122">Sign in to the Azure Stack Administrator Portal.</span></span>
1. <span data-ttu-id="e97f4-123">Select **All services**.</span><span class="sxs-lookup"><span data-stu-id="e97f4-123">Select **All services**.</span></span>
2. <span data-ttu-id="e97f4-124">In the **COMPUTE** category, select **Virtual machine scale sets**.</span><span class="sxs-lookup"><span data-stu-id="e97f4-124">In the **COMPUTE** category, select **Virtual machine scale sets**.</span></span> <span data-ttu-id="e97f4-125">Existing scale sets deployed as part of the App Service deployment will be listed with instance count information.</span><span class="sxs-lookup"><span data-stu-id="e97f4-125">Existing scale sets deployed as part of the App Service deployment will be listed with instance count information.</span></span> <span data-ttu-id="e97f4-126">The following screen capture shows an example of scale sets.</span><span class="sxs-lookup"><span data-stu-id="e97f4-126">The following screen capture shows an example of scale sets.</span></span>

      ![Azure App Service Scale Sets listed in Virtual Machine Scale Sets UX][1]

1. <span data-ttu-id="e97f4-128">Scale out each set.</span><span class="sxs-lookup"><span data-stu-id="e97f4-128">Scale out each set.</span></span> <span data-ttu-id="e97f4-129">For example, if you have three existing instances in the scale set you must scale out to 6 so the three new instances are deployed across fault domains.</span><span class="sxs-lookup"><span data-stu-id="e97f4-129">For example, if you have three existing instances in the scale set you must scale out to 6 so the three new instances are deployed across fault domains.</span></span> <span data-ttu-id="e97f4-130">The following PowerShell example shows out to scale out the scale set.</span><span class="sxs-lookup"><span data-stu-id="e97f4-130">The following PowerShell example shows out to scale out the scale set.</span></span>

   ```powershell
   Add-AzureRmAccount -EnvironmentName AzureStackAdmin 

   # Get current scale set
   $vmss = Get-AzureRmVmss -ResourceGroupName "AppService.local" -VMScaleSetName "SmallWorkerTierScaleSet"

   # Set and update the capacity of your scale set
   $vmss.sku.capacity = 6
   Update-AzureRmVmss -ResourceGroupName AppService.local" -Name "SmallWorkerTierScaleSet" -VirtualMachineScaleSet $vmss
   ```

   >[!NOTE]
   ><span data-ttu-id="e97f4-131">This step can take several of hours to finish, depending on the type of role and the number of instances.</span><span class="sxs-lookup"><span data-stu-id="e97f4-131">This step can take several of hours to finish, depending on the type of role and the number of instances.</span></span>

1. <span data-ttu-id="e97f4-132">In **App Service Administration Roles**, monitor the status of the new role instances.</span><span class="sxs-lookup"><span data-stu-id="e97f4-132">In **App Service Administration Roles**, monitor the status of the new role instances.</span></span> <span data-ttu-id="e97f4-133">To check the status of a role instance, select the role type in the list</span><span class="sxs-lookup"><span data-stu-id="e97f4-133">To check the status of a role instance, select the role type in the list</span></span>

    ![Azure App Service on Azure Stack Roles][2]

1. <span data-ttu-id="e97f4-135">When the status of the new role instances is **Ready**, go back to **Virtual Machine Scale Set** and **delete** the old role instances.</span><span class="sxs-lookup"><span data-stu-id="e97f4-135">When the status of the new role instances is **Ready**, go back to **Virtual Machine Scale Set** and **delete** the old role instances.</span></span>

1. <span data-ttu-id="e97f4-136">Repeat these steps for **each** virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="e97f4-136">Repeat these steps for **each** virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e97f4-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="e97f4-137">Next steps</span></span>

<span data-ttu-id="e97f4-138">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span><span class="sxs-lookup"><span data-stu-id="e97f4-138">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

* [<span data-ttu-id="e97f4-139">SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="e97f4-139">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
* [<span data-ttu-id="e97f4-140">MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="e97f4-140">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-fault-domain-update/app-service-scale-sets.png
[2]: ./media/azure-stack-app-service-fault-domain-update/app-service-roles.png
