---
title: Migrate VMs to Resource Manager using Azure CLI | Microsoft Docs
description: This article walks through the platform-supported migration of resources from classic to Azure Resource Manager by using Azure CLI
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 9aec1c2aa4a5f410fb3942e373942f71a8470218
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553139"
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="2d0b8-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2d0b8-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="2d0b8-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2d0b8-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2d0b8-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2d0b8-106">All the operations described here are idempotent.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="2d0b8-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="2d0b8-108">The platform will then try the action again.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="2d0b8-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span><span class="sxs-lookup"><span data-stu-id="2d0b8-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="2d0b8-111">Step 1: Prepare for migration</span><span class="sxs-lookup"><span data-stu-id="2d0b8-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="2d0b8-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2d0b8-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="2d0b8-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d0b8-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="2d0b8-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="2d0b8-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="2d0b8-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="2d0b8-117">Alternatively, you can set up sample environments by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d0b8-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="2d0b8-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="2d0b8-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="2d0b8-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="2d0b8-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="2d0b8-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="2d0b8-124">Step 2: Set your subscription and register the provider</span><span class="sxs-lookup"><span data-stu-id="2d0b8-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="2d0b8-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="2d0b8-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2d0b8-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="2d0b8-127">Sign-in to your account.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="2d0b8-128">Select the Azure subscription by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="2d0b8-129">Registration is a one time step but it needs to be done once before attempting migration.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="2d0b8-130">Without registering you'll see the following error message</span><span class="sxs-lookup"><span data-stu-id="2d0b8-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="2d0b8-131">*BadRequest : Subscription is not registered for migration.*</span><span class="sxs-lookup"><span data-stu-id="2d0b8-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="2d0b8-132">Register with the migration resource provider by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="2d0b8-133">Note that in some cases, this command times out. However, the registration will be successful.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-133">Note that in some cases, this command times out. However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="2d0b8-134">Please wait five minutes for the registration to finish.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-134">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="2d0b8-135">You can check the status of the approval by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-135">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="2d0b8-136">Make sure that RegistrationState is `Registered` before you proceed.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="2d0b8-137">Now switch CLI to the `asm` mode.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-137">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="2d0b8-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span><span class="sxs-lookup"><span data-stu-id="2d0b8-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="2d0b8-139">For this step you'll need to switch to `arm` mode.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-139">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="2d0b8-140">Do this with the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-140">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="2d0b8-141">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-141">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="2d0b8-142">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="2d0b8-142">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="2d0b8-143">Once you're done verifying this step, you can switch back to `asm` mode.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-143">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="2d0b8-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span><span class="sxs-lookup"><span data-stu-id="2d0b8-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="2d0b8-145">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-145">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="2d0b8-146">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-146">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="2d0b8-147">Run the following command to get the deployment name for the cloud service from the verbose output.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-147">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="2d0b8-148">In most cases, the deployment name is the same as the cloud service name.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-148">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="2d0b8-149">First, validate if you can migrate the cloud service using the following commands:</span><span class="sxs-lookup"><span data-stu-id="2d0b8-149">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="2d0b8-150">Prepare the virtual machines in the cloud service for migration.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-150">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="2d0b8-151">You have two options to choose from.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-151">You have two options to choose from.</span></span>

<span data-ttu-id="2d0b8-152">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-152">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="2d0b8-153">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-153">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="2d0b8-154">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-154">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="2d0b8-155">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-155">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="2d0b8-156">If you are not ready for migration and you want to go back to the old state, use the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-156">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="2d0b8-157">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-157">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="2d0b8-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span><span class="sxs-lookup"><span data-stu-id="2d0b8-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="2d0b8-159">Pick the virtual network that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-159">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="2d0b8-160">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-160">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="2d0b8-161">Get all the virtual networks in the subscription by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-161">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="2d0b8-162">The output will look something like this:</span><span class="sxs-lookup"><span data-stu-id="2d0b8-162">The output will look something like this:</span></span>

![Screenshot of the command line with the entire virtual network name highlighted.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="2d0b8-164">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-164">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="2d0b8-165">First, validate if you can migrate the virtual network using the following command:</span><span class="sxs-lookup"><span data-stu-id="2d0b8-165">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="2d0b8-166">Prepare the virtual network of your choice for migration by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-166">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="2d0b8-167">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-167">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="2d0b8-168">If you are not ready for migration and you want to go back to the old state, use the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-168">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="2d0b8-169">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-169">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="2d0b8-170">Step 5: Migrate a storage account</span><span class="sxs-lookup"><span data-stu-id="2d0b8-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="2d0b8-171">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-171">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="2d0b8-172">Prepare the storage account for migration by using the following command</span><span class="sxs-lookup"><span data-stu-id="2d0b8-172">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="2d0b8-173">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-173">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="2d0b8-174">If you are not ready for migration and you want to go back to the old state, use the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-174">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="2d0b8-175">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span><span class="sxs-lookup"><span data-stu-id="2d0b8-175">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="2d0b8-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d0b8-176">Next steps</span></span>

* [<span data-ttu-id="2d0b8-177">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d0b8-177">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d0b8-178">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d0b8-178">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d0b8-179">Planning for migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d0b8-179">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d0b8-180">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d0b8-180">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2d0b8-181">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d0b8-181">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2d0b8-182">Review most common migration errors</span><span class="sxs-lookup"><span data-stu-id="2d0b8-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d0b8-183">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d0b8-183">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


