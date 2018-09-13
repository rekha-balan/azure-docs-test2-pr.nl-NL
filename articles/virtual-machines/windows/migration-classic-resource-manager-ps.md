---
title: Migrate to Resource Manager with PowerShell | Microsoft Docs
description: This article walks through the platform-supported migration of IaaS resources such as virtual machines (VMs), virtual networks (VNETs), and storage accounts from classic to Azure Resource Manager (ARM) by using Azure PowerShell commands
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 6d3df144cce31e2043c9333862b0f00b7b1eb88a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564251"
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="4afa8-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4afa8-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="4afa8-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="4afa8-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> 

<span data-ttu-id="4afa8-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4afa8-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="4afa8-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4afa8-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span> 
* <span data-ttu-id="4afa8-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="4afa8-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="4afa8-108">Review most common migration errors</span><span class="sxs-lookup"><span data-stu-id="4afa8-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="4afa8-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span><span class="sxs-lookup"><span data-stu-id="4afa8-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="4afa8-111">Step 1: Plan for migration</span><span class="sxs-lookup"><span data-stu-id="4afa8-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="4afa8-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4afa8-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="4afa8-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4afa8-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="4afa8-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span><span class="sxs-lookup"><span data-stu-id="4afa8-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="4afa8-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="4afa8-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="4afa8-117">Alternatively, you can set up sample environments by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4afa8-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4afa8-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4afa8-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="4afa8-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span><span class="sxs-lookup"><span data-stu-id="4afa8-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="4afa8-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4afa8-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="4afa8-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span><span class="sxs-lookup"><span data-stu-id="4afa8-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="4afa8-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span><span class="sxs-lookup"><span data-stu-id="4afa8-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="4afa8-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="4afa8-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="4afa8-124">Step 2: Install the latest version of Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4afa8-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="4afa8-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="4afa8-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="4afa8-126">WebPI receives monthly updates.</span><span class="sxs-lookup"><span data-stu-id="4afa8-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="4afa8-127">PowerShell Gallery receives updates on a continuous basis.</span><span class="sxs-lookup"><span data-stu-id="4afa8-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="4afa8-128">This article is based on Azure PowerShell version 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="4afa8-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="4afa8-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="4afa8-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-co-administrator-for-the-subscription-in-azure-classic-portal"></a><span data-ttu-id="4afa8-130">Step 3: Ensure that you are co-administrator for the subscription in Azure Classic portal</span><span class="sxs-lookup"><span data-stu-id="4afa8-130">Step 3: Ensure that you are co-administrator for the subscription in Azure Classic portal</span></span>
<span data-ttu-id="4afa8-131">To perform this migration, you must be added as co-administrator for the subscription in the [Azure Classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="4afa8-131">To perform this migration, you must be added as co-administrator for the subscription in the [Azure Classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="4afa8-132">This is required even if you are already added as owner in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4afa8-132">This is required even if you are already added as owner in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4afa8-133">Try to [add a co-administrator for the subscription in Azure Classic portal](../../billing/billing-add-change-azure-subscription-administrator.md) to find out if you are co-administrator for the subscription.</span><span class="sxs-lookup"><span data-stu-id="4afa8-133">Try to [add a co-administrator for the subscription in Azure Classic portal](../../billing/billing-add-change-azure-subscription-administrator.md) to find out if you are co-administrator for the subscription.</span></span> <span data-ttu-id="4afa8-134">If you are not able to add a co-administrator then please contact a service administrator or co-administrator for the subscription to get yourself added.</span><span class="sxs-lookup"><span data-stu-id="4afa8-134">If you are not able to add a co-administrator then please contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="4afa8-135">Step 4: Set your subscription and sign up for migration</span><span class="sxs-lookup"><span data-stu-id="4afa8-135">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="4afa8-136">First, start a PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="4afa8-136">First, start a PowerShell prompt.</span></span> <span data-ttu-id="4afa8-137">For migration, you need to set up your environment for both classic and Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4afa8-137">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="4afa8-138">Sign in to your account for the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="4afa8-138">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="4afa8-139">Get the available subscriptions by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-139">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="4afa8-140">Set your Azure subscription for the current session.</span><span class="sxs-lookup"><span data-stu-id="4afa8-140">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="4afa8-141">This example sets the default subscription name to **My Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-141">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="4afa8-142">Replace the example subscription name with your own.</span><span class="sxs-lookup"><span data-stu-id="4afa8-142">Replace the example subscription name with your own.</span></span> 

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="4afa8-143">Registration is a one-time step, but you must do it once before attempting migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-143">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="4afa8-144">Without registering, you see the following error message:</span><span class="sxs-lookup"><span data-stu-id="4afa8-144">Without registering, you see the following error message:</span></span> 
> 
> <span data-ttu-id="4afa8-145">*BadRequest : Subscription is not registered for migration.*</span><span class="sxs-lookup"><span data-stu-id="4afa8-145">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="4afa8-146">Register with the migration resource provider by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-146">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="4afa8-147">Please wait five minutes for the registration to finish.</span><span class="sxs-lookup"><span data-stu-id="4afa8-147">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="4afa8-148">You can check the status of the approval by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-148">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="4afa8-149">Make sure that RegistrationState is `Registered` before you proceed.</span><span class="sxs-lookup"><span data-stu-id="4afa8-149">Make sure that RegistrationState is `Registered` before you proceed.</span></span> 

<span data-ttu-id="4afa8-150">Now sign in to your account for the classic model.</span><span class="sxs-lookup"><span data-stu-id="4afa8-150">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="4afa8-151">Get the available subscriptions by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-151">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="4afa8-152">Set your Azure subscription for the current session.</span><span class="sxs-lookup"><span data-stu-id="4afa8-152">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="4afa8-153">This example sets the default subscription to **My Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-153">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="4afa8-154">Replace the example subscription name with your own.</span><span class="sxs-lookup"><span data-stu-id="4afa8-154">Replace the example subscription name with your own.</span></span> 

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="4afa8-155">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span><span class="sxs-lookup"><span data-stu-id="4afa8-155">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="4afa8-156">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4afa8-156">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="4afa8-157">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="4afa8-157">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span> 

<span data-ttu-id="4afa8-158">This example checks the availability in the **West US** region.</span><span class="sxs-lookup"><span data-stu-id="4afa8-158">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="4afa8-159">Replace the example region name with your own.</span><span class="sxs-lookup"><span data-stu-id="4afa8-159">Replace the example region name with your own.</span></span> 

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="4afa8-160">Step 6: Run commands to migrate your IaaS resources</span><span class="sxs-lookup"><span data-stu-id="4afa8-160">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="4afa8-161">All the operations described here are idempotent.</span><span class="sxs-lookup"><span data-stu-id="4afa8-161">All the operations described here are idempotent.</span></span> <span data-ttu-id="4afa8-162">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span><span class="sxs-lookup"><span data-stu-id="4afa8-162">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="4afa8-163">The platform then tries the action again.</span><span class="sxs-lookup"><span data-stu-id="4afa8-163">The platform then tries the action again.</span></span>
> 
> 

## <a name="step-61-migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="4afa8-164">Step 6.1 Migrate virtual machines in a cloud service (not in a virtual network)</span><span class="sxs-lookup"><span data-stu-id="4afa8-164">Step 6.1 Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="4afa8-165">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="4afa8-165">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="4afa8-166">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span><span class="sxs-lookup"><span data-stu-id="4afa8-166">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="4afa8-167">Get the deployment name for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4afa8-167">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="4afa8-168">In this example, the service name is **My Service**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-168">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="4afa8-169">Replace the example service name with your own service name.</span><span class="sxs-lookup"><span data-stu-id="4afa8-169">Replace the example service name with your own service name.</span></span> 

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="4afa8-170">Prepare the virtual machines in the cloud service for migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-170">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="4afa8-171">You have two options to choose from.</span><span class="sxs-lookup"><span data-stu-id="4afa8-171">You have two options to choose from.</span></span>

* <span data-ttu-id="4afa8-172">**Option 1. Migrate the VMs to a platform-created virtual network**</span><span class="sxs-lookup"><span data-stu-id="4afa8-172">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>
  
    <span data-ttu-id="4afa8-173">First, validate if you can migrate the cloud service using the following commands:</span><span class="sxs-lookup"><span data-stu-id="4afa8-173">First, validate if you can migrate the cloud service using the following commands:</span></span>
  
    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```
  
    <span data-ttu-id="4afa8-174">The preceding command displays any warnings and errors that block migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-174">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="4afa8-175">If validation is successful, then you can move on to the **Prepare** step:</span><span class="sxs-lookup"><span data-stu-id="4afa8-175">If validation is successful, then you can move on to the **Prepare** step:</span></span>
  
    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="4afa8-176">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span><span class="sxs-lookup"><span data-stu-id="4afa8-176">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>
  
    <span data-ttu-id="4afa8-177">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-177">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="4afa8-178">Replace the names in the example with the names of your own resources.</span><span class="sxs-lookup"><span data-stu-id="4afa8-178">Replace the names in the example with the names of your own resources.</span></span>
  
    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```
  
    <span data-ttu-id="4afa8-179">First, validate if you can migrate the virtual network using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-179">First, validate if you can migrate the virtual network using the following command:</span></span>
  
    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```
  
    <span data-ttu-id="4afa8-180">The preceding command displays any warnings and errors that block migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-180">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="4afa8-181">If validation is successful, then you can proceed with the following Prepare step:</span><span class="sxs-lookup"><span data-stu-id="4afa8-181">If validation is successful, then you can proceed with the following Prepare step:</span></span>
  
    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="4afa8-182">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span><span class="sxs-lookup"><span data-stu-id="4afa8-182">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="4afa8-183">Ensure that they are in the `Prepared` state.</span><span class="sxs-lookup"><span data-stu-id="4afa8-183">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="4afa8-184">This example sets the VM name to **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-184">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="4afa8-185">Replace the example name with your own VM name.</span><span class="sxs-lookup"><span data-stu-id="4afa8-185">Replace the example name with your own VM name.</span></span>

    ```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
    ```

<span data-ttu-id="4afa8-186">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4afa8-186">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="4afa8-187">If you are not ready for migration and you want to go back to the old state, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-187">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="4afa8-188">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-188">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-62-migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="4afa8-189">Step 6.2 Migrate virtual machines in a virtual network</span><span class="sxs-lookup"><span data-stu-id="4afa8-189">Step 6.2 Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="4afa8-190">To migrate virtual machines in a virtual network, you migrate the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4afa8-190">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="4afa8-191">The virtual machines automatically migrate with the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4afa8-191">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="4afa8-192">Pick the virtual network that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="4afa8-192">Pick the virtual network that you want to migrate.</span></span> 
> [!NOTE]
> <span data-ttu-id="4afa8-193">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4afa8-193">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span> 

<span data-ttu-id="4afa8-194">This example sets the virtual network name to **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-194">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="4afa8-195">Replace the example virtual network name with your own.</span><span class="sxs-lookup"><span data-stu-id="4afa8-195">Replace the example virtual network name with your own.</span></span> 

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="4afa8-196">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span><span class="sxs-lookup"><span data-stu-id="4afa8-196">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
> 
> 

<span data-ttu-id="4afa8-197">First, validate if you can migrate the virtual network by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-197">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="4afa8-198">The preceding command displays any warnings and errors that block migration.</span><span class="sxs-lookup"><span data-stu-id="4afa8-198">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="4afa8-199">If validation is successful, then you can proceed with the following Prepare step:</span><span class="sxs-lookup"><span data-stu-id="4afa8-199">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="4afa8-200">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4afa8-200">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="4afa8-201">If you are not ready for migration and you want to go back to the old state, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-201">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="4afa8-202">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-202">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-63-migrate-a-storage-account"></a><span data-ttu-id="4afa8-203">Step 6.3 Migrate a storage account</span><span class="sxs-lookup"><span data-stu-id="4afa8-203">Step 6.3 Migrate a storage account</span></span>
<span data-ttu-id="4afa8-204">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span><span class="sxs-lookup"><span data-stu-id="4afa8-204">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="4afa8-205">Before you migrate the storage account, please perform preceding prerequisite checks:</span><span class="sxs-lookup"><span data-stu-id="4afa8-205">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="4afa8-206">**Migrate classic virtual machines whose disks are stored in the storage account**</span><span class="sxs-lookup"><span data-stu-id="4afa8-206">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="4afa8-207">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span><span class="sxs-lookup"><span data-stu-id="4afa8-207">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="4afa8-208">RoleName is the name of the virtual machine to which a disk is attached.</span><span class="sxs-lookup"><span data-stu-id="4afa8-208">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="4afa8-209">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span><span class="sxs-lookup"><span data-stu-id="4afa8-209">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName 

    ```
* <span data-ttu-id="4afa8-210">**Delete unattached classic VM disks stored in the storage account**</span><span class="sxs-lookup"><span data-stu-id="4afa8-210">**Delete unattached classic VM disks stored in the storage account**</span></span>
 
    <span data-ttu-id="4afa8-211">Find unattached classic VM disks in the storage account using following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-211">Find unattached classic VM disks in the storage account using following command:</span></span> 

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Format-List -Property DiskName  

    ```
    <span data-ttu-id="4afa8-212">If above command returns disks then delete these disks using following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-212">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="4afa8-213">**Delete VM images stored in the storage account**</span><span class="sxs-lookup"><span data-stu-id="4afa8-213">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="4afa8-214">Preceding command returns all the VM images with OS disk stored in the storage account.</span><span class="sxs-lookup"><span data-stu-id="4afa8-214">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="4afa8-215">Preceding command returns all the VM images with data disks stored in the storage account.</span><span class="sxs-lookup"><span data-stu-id="4afa8-215">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="4afa8-216">Delete all the VM images returned by above commands using preceding command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-216">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```
    
<span data-ttu-id="4afa8-217">Prepare each storage account for migration by using the following command.</span><span class="sxs-lookup"><span data-stu-id="4afa8-217">Prepare each storage account for migration by using the following command.</span></span> <span data-ttu-id="4afa8-218">In this example, the storage account name is **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="4afa8-218">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="4afa8-219">Replace the example name with the name of your own storage account.</span><span class="sxs-lookup"><span data-stu-id="4afa8-219">Replace the example name with the name of your own storage account.</span></span> 

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="4afa8-220">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4afa8-220">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="4afa8-221">If you are not ready for migration and you want to go back to the old state, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-221">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="4afa8-222">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4afa8-222">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="4afa8-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="4afa8-223">Next steps</span></span>
* [<span data-ttu-id="4afa8-224">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4afa8-224">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4afa8-225">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4afa8-225">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4afa8-226">Planning for migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4afa8-226">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4afa8-227">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4afa8-227">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4afa8-228">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4afa8-228">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4afa8-229">Review most common migration errors</span><span class="sxs-lookup"><span data-stu-id="4afa8-229">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4afa8-230">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4afa8-230">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

