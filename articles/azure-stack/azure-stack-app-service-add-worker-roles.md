---
title: Scale out worker roles in App Services - Azure Stack  | Microsoft Docs
description: Detailed guidance for scaling Azure Stack App Services
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2018
ms.author: anwestg
ms.reviewer: brenduns
ms.openlocfilehash: abfc75e40e146b1cf7cb237f18a1ff08626e5be1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808280"
---
# <a name="app-service-on-azure-stack-add-more-infrastructure-or-worker-roles"></a><span data-ttu-id="9bbaf-103">App Service on Azure Stack: Add more infrastructure or worker roles</span><span class="sxs-lookup"><span data-stu-id="9bbaf-103">App Service on Azure Stack: Add more infrastructure or worker roles</span></span>

<span data-ttu-id="9bbaf-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="9bbaf-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>  

<span data-ttu-id="9bbaf-105">This document provides instructions about how to scale App Service on Azure Stack infrastructure and worker roles.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-105">This document provides instructions about how to scale App Service on Azure Stack infrastructure and worker roles.</span></span> <span data-ttu-id="9bbaf-106">It contains steps for creating additional worker roles to support applications of any size.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-106">It contains steps for creating additional worker roles to support applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="9bbaf-107">If your Azure Stack Environment does not have more than 96-GB RAM, you may have difficulties adding additional capacity.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-107">If your Azure Stack Environment does not have more than 96-GB RAM, you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="9bbaf-108">App Service on Azure Stack, by default, supports free and shared worker tiers.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-108">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="9bbaf-109">To add other worker tiers, you need to add more worker roles.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-109">To add other worker tiers, you need to add more worker roles.</span></span>

<span data-ttu-id="9bbaf-110">If you are not sure what was deployed with the default App Service on Azure Stack installation, you can review additional information in the [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bbaf-110">If you are not sure what was deployed with the default App Service on Azure Stack installation, you can review additional information in the [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="9bbaf-111">Azure App Service on Azure Stack deploys all roles using Virtual Machine Scale Sets and as such takes advantage of the scaling capabilities of this workload.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-111">Azure App Service on Azure Stack deploys all roles using Virtual Machine Scale Sets and as such takes advantage of the scaling capabilities of this workload.</span></span> <span data-ttu-id="9bbaf-112">Therefore, all scaling of the worker tiers is done via the App Service Admin.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-112">Therefore, all scaling of the worker tiers is done via the App Service Admin.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bbaf-113">Currently it is not possible to scale virtual machine scale sets in the portal as identified in the Azure Stack release notes,  therefore use the PowerShell example to scale out.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-113">Currently it is not possible to scale virtual machine scale sets in the portal as identified in the Azure Stack release notes,  therefore use the PowerShell example to scale out.</span></span>
>
>

## <a name="add-additional-workers-with-powershell"></a><span data-ttu-id="9bbaf-114">Add additional workers with PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bbaf-114">Add additional workers with PowerShell</span></span>

1. [<span data-ttu-id="9bbaf-115">Setup the Azure Stack Admin environment in PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bbaf-115">Setup the Azure Stack Admin environment in PowerShell</span></span>](azure-stack-powershell-configure-admin.md)

2. <span data-ttu-id="9bbaf-116">Use this example to scale out the scale set:</span><span class="sxs-lookup"><span data-stu-id="9bbaf-116">Use this example to scale out the scale set:</span></span>
   ```powershell
   
    ##### Scale out the AppService Role instances ######
   
    # Set context to AzureStack admin.
    Login-AzureRmAccount -EnvironmentName AzureStackAdmin
                                                 
    ## Name of the Resource group where AppService is deployed.
    $AppServiceResourceGroupName = "AppService.local"

    ## Name of the ScaleSet : e.g. FrontEndsScaleSet, ManagementServersScaleSet, PublishersScaleSet , LargeWorkerTierScaleSet,      MediumWorkerTierScaleSet, SmallWorkerTierScaleSet, SharedWorkerTierScaleSet
    $ScaleSetName = "SharedWorkerTierScaleSet"

    ## TotalCapacity is sum of the instances needed at the end of operation. 
    ## e.g. if your VMSS has 1 instance(s) currently and you need 1 more the TotalCapacity should be set to 2
    $TotalCapacity = 2  

    # Get current scale set
    $vmss = Get-AzureRmVmss -ResourceGroupName $AppServiceResourceGroupName -VMScaleSetName $ScaleSetName

    # Set and update the capacity
    $vmss.sku.capacity = $TotalCapacity
    Update-AzureRmVmss -ResourceGroupName $AppServiceResourceGroupName -Name $ScaleSetName -VirtualMachineScaleSet $vmss 
   ```    

   > [!NOTE]
   > <span data-ttu-id="9bbaf-117">This step can take a number of hours to complete depending on the type of role and the number of instances.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-117">This step can take a number of hours to complete depending on the type of role and the number of instances.</span></span>
   >
   >

3. <span data-ttu-id="9bbaf-118">Monitor the status of the new role instances in the App Service Administration, to check the status of an individual role instance click the role type in the list.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-118">Monitor the status of the new role instances in the App Service Administration, to check the status of an individual role instance click the role type in the list.</span></span>

## <a name="add-additional-workers-directly-within-the-app-service-resource-provider-admin"></a><span data-ttu-id="9bbaf-119">Add additional workers directly within the App Service Resource Provider Admin.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-119">Add additional workers directly within the App Service Resource Provider Admin.</span></span>

1. <span data-ttu-id="9bbaf-120">Sign in to the Azure Stack administration portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-120">Sign in to the Azure Stack administration portal as the service administrator.</span></span>

2. <span data-ttu-id="9bbaf-121">Browse to **App Services**.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-121">Browse to **App Services**.</span></span>

    ![](media/azure-stack-app-service-add-worker-roles/image01.png)

3. <span data-ttu-id="9bbaf-122">Click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-122">Click **Roles**.</span></span> <span data-ttu-id="9bbaf-123">Here you see the breakdown of all App Service roles deployed.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-123">Here you see the breakdown of all App Service roles deployed.</span></span>

4. <span data-ttu-id="9bbaf-124">Right click on the row of the type you want to scale and then click **ScaleSet**.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-124">Right click on the row of the type you want to scale and then click **ScaleSet**.</span></span>

    ![](media/azure-stack-app-service-add-worker-roles/image02.png)

5. <span data-ttu-id="9bbaf-125">Click **Scaling**, select the number of instances you want to scale to, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-125">Click **Scaling**, select the number of instances you want to scale to, and then click **Save**.</span></span>

    ![](media/azure-stack-app-service-add-worker-roles/image03.png)

6. <span data-ttu-id="9bbaf-126">App Service on Azure Stack will now add the additional VMs, configure them, install all the required software, and mark them as ready when this process is complete.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-126">App Service on Azure Stack will now add the additional VMs, configure them, install all the required software, and mark them as ready when this process is complete.</span></span> <span data-ttu-id="9bbaf-127">This process can take approximately 80 minutes.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-127">This process can take approximately 80 minutes.</span></span>

7. <span data-ttu-id="9bbaf-128">You can monitor the progress of the readiness of the new roles by viewing the workers in the **Roles** blade.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-128">You can monitor the progress of the readiness of the new roles by viewing the workers in the **Roles** blade.</span></span>

## <a name="result"></a><span data-ttu-id="9bbaf-129">Result</span><span class="sxs-lookup"><span data-stu-id="9bbaf-129">Result</span></span>

<span data-ttu-id="9bbaf-130">After they are fully deployed and ready, the workers become available for users to deploy their workload onto them.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-130">After they are fully deployed and ready, the workers become available for users to deploy their workload onto them.</span></span> <span data-ttu-id="9bbaf-131">The following shows an example of the multiple pricing tiers available by default.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-131">The following shows an example of the multiple pricing tiers available by default.</span></span> <span data-ttu-id="9bbaf-132">If there are no available workers for a particular worker tier, the option to choose the corresponding pricing tier is unavailable.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-132">If there are no available workers for a particular worker tier, the option to choose the corresponding pricing tier is unavailable.</span></span>

![](media/azure-stack-app-service-add-worker-roles/image04.png)

>[!NOTE]
> <span data-ttu-id="9bbaf-133">To scale out Management, Front End or Publisher roles add you must scale out the corresponding role type.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-133">To scale out Management, Front End or Publisher roles add you must scale out the corresponding role type.</span></span> 
>
>

<span data-ttu-id="9bbaf-134">To scale out Management, Front End, or Publisher roles, follow the same steps selecting the appropriate role type.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-134">To scale out Management, Front End, or Publisher roles, follow the same steps selecting the appropriate role type.</span></span> <span data-ttu-id="9bbaf-135">Controllers are not deployed as Scale Sets and therefore two should be deployed at Installation time for all production deployments.</span><span class="sxs-lookup"><span data-stu-id="9bbaf-135">Controllers are not deployed as Scale Sets and therefore two should be deployed at Installation time for all production deployments.</span></span>

### <a name="next-steps"></a><span data-ttu-id="9bbaf-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bbaf-136">Next steps</span></span>

[<span data-ttu-id="9bbaf-137">Configure deployment sources</span><span class="sxs-lookup"><span data-stu-id="9bbaf-137">Configure deployment sources</span></span>](azure-stack-app-service-configure-deployment-sources.md)
