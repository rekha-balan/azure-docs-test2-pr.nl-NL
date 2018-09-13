---
title: Create an Azure virtual machine scale set | Microsoft Docs
description: Create and deploy a Linux or Windows Azure virtual machine scale set with Azure CLI, PowerShell, a template, or Visual Studio.
services: virtual-machine-scale-sets
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/30/2017
ms.author: adegeo
ms.openlocfilehash: 56a460fa8132d310352fbb7e085091c3ee7fa848
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663110"
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="d2e1a-103">Create and deploy a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="d2e1a-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="d2e1a-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="d2e1a-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="d2e1a-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="d2e1a-107">This tutorial shows you how to create a virtual machine scale set **without** using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-107">This tutorial shows you how to create a virtual machine scale set **without** using the Azure portal.</span></span> <span data-ttu-id="d2e1a-108">For information about how to use the Azure portal, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-108">For information about how to use the Azure portal, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="d2e1a-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="d2e1a-110">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="d2e1a-110">Sign in to Azure</span></span>

<span data-ttu-id="d2e1a-111">If you're using Azure CLI 2.0 or Azure PowerShell to create a scale set, you first need to sign in to your subscription.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-111">If you're using Azure CLI 2.0 or Azure PowerShell to create a scale set, you first need to sign in to your subscription.</span></span>

<span data-ttu-id="d2e1a-112">For more information about how to install, set up, and sign in to Azure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/resourcemanager/).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-112">For more information about how to install, set up, and sign in to Azure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/resourcemanager/).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d2e1a-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="d2e1a-113">Create a resource group</span></span>

<span data-ttu-id="d2e1a-114">You first need to create a resource group that the virtual machine scale set is associated with.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-114">You first need to create a resource group that the virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name vmss-test-1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name vmss-test-1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="d2e1a-115">Create from Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d2e1a-115">Create from Azure CLI</span></span>

<span data-ttu-id="d2e1a-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="d2e1a-117">If you omit default values, the are provided for you.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-117">If you omit default values, the are provided for you.</span></span> <span data-ttu-id="d2e1a-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="d2e1a-119">If you omit the following parts, they are created for you:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-119">If you omit the following parts, they are created for you:</span></span> 
- <span data-ttu-id="d2e1a-120">A load balancer</span><span class="sxs-lookup"><span data-stu-id="d2e1a-120">A load balancer</span></span>
- <span data-ttu-id="d2e1a-121">A virtual network</span><span class="sxs-lookup"><span data-stu-id="d2e1a-121">A virtual network</span></span>
- <span data-ttu-id="d2e1a-122">A public IP address</span><span class="sxs-lookup"><span data-stu-id="d2e1a-122">A public IP address</span></span>

<span data-ttu-id="d2e1a-123">When choosing the virtual machine image that you want to use on the virtual machine scale set, you have a few choices:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-123">When choosing the virtual machine image that you want to use on the virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="d2e1a-124">URN</span><span class="sxs-lookup"><span data-stu-id="d2e1a-124">URN</span></span>  
<span data-ttu-id="d2e1a-125">The identifier of a resource:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-125">The identifier of a resource:</span></span>  
<span data-ttu-id="d2e1a-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="d2e1a-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="d2e1a-127">URN alias</span><span class="sxs-lookup"><span data-stu-id="d2e1a-127">URN alias</span></span>  
<span data-ttu-id="d2e1a-128">The friendly name of a URN:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-128">The friendly name of a URN:</span></span>  
<span data-ttu-id="d2e1a-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="d2e1a-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="d2e1a-130">Custom resource id</span><span class="sxs-lookup"><span data-stu-id="d2e1a-130">Custom resource id</span></span>  
<span data-ttu-id="d2e1a-131">The path to an Azure resource:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-131">The path to an Azure resource:</span></span>  
<span data-ttu-id="d2e1a-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="d2e1a-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="d2e1a-133">Web resource</span><span class="sxs-lookup"><span data-stu-id="d2e1a-133">Web resource</span></span>  
<span data-ttu-id="d2e1a-134">The path to an HTTP URI:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-134">The path to an HTTP URI:</span></span>  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
><span data-ttu-id="d2e1a-135">You can get a list of available images with `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-135">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="d2e1a-136">To create a virtual machine scale set, you must specify the following:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-136">To create a virtual machine scale set, you must specify the following:</span></span>

- <span data-ttu-id="d2e1a-137">Resource group</span><span class="sxs-lookup"><span data-stu-id="d2e1a-137">Resource group</span></span> 
- <span data-ttu-id="d2e1a-138">Name</span><span class="sxs-lookup"><span data-stu-id="d2e1a-138">Name</span></span>
- <span data-ttu-id="d2e1a-139">Operating system image</span><span class="sxs-lookup"><span data-stu-id="d2e1a-139">Operating system image</span></span>
- <span data-ttu-id="d2e1a-140">Authentication information</span><span class="sxs-lookup"><span data-stu-id="d2e1a-140">Authentication information</span></span> 
 
<span data-ttu-id="d2e1a-141">The following example creates a basic virtual machine scale set (this step might take a few minutes).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-141">The following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group vmss-test-1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="d2e1a-142">Once the command finishes you will now have your virtual machine scale set created.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-142">Once the command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="d2e1a-143">You may need to get the IP address of the virtual machine so that you can connect to it.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-143">You may need to get the IP address of the virtual machine so that you can connect to it.</span></span> <span data-ttu-id="d2e1a-144">You can get a lot of different information about the virtual machine (including the IP address) with the following command.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-144">You can get a lot of different information about the virtual machine (including the IP address) with the following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group vmss-test-1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="d2e1a-145">Create from PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2e1a-145">Create from PowerShell</span></span>

<span data-ttu-id="d2e1a-146">PowerShell is more complicated to use than Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-146">PowerShell is more complicated to use than Azure CLI.</span></span> <span data-ttu-id="d2e1a-147">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-147">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="d2e1a-148">Referencing an image with PowerShell is a slightly more complicated too.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-148">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="d2e1a-149">You can get images with the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-149">You can get images with the following cmdlets:</span></span>

1. <span data-ttu-id="d2e1a-150">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="d2e1a-150">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="d2e1a-151">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="d2e1a-151">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="d2e1a-152">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="d2e1a-152">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="d2e1a-153">The cmdlets work can be piped in sequence.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-153">The cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="d2e1a-154">Here is an example of how to get all images for the **West US 2** region with a publisher that has the name **microsoft** in it.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-154">Here is an example of how to get all images for the **West US 2** region with a publisher that has the name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="d2e1a-155">The workflow for creating a virtual machine scale set is as follows:</span><span class="sxs-lookup"><span data-stu-id="d2e1a-155">The workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="d2e1a-156">Create a config object that holds information about the scale set.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-156">Create a config object that holds information about the scale set.</span></span>
2. <span data-ttu-id="d2e1a-157">Reference the base OS image.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-157">Reference the base OS image.</span></span>
3. <span data-ttu-id="d2e1a-158">Configure the operating system settings: authentication, VM name prefix, and user/pass.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-158">Configure the operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="d2e1a-159">Configure networking.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-159">Configure networking.</span></span>
5. <span data-ttu-id="d2e1a-160">Create the scale set.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-160">Create the scale set.</span></span>

<span data-ttu-id="d2e1a-161">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-161">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location WestUS2 -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create the virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName "vmss-test-1" -Location "westus2" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ip-address" -LoadBalancerBackendAddressPoolsId $null -SubnetId $vnet.Subnets[0].Id

# Attach the virtual network to the config object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName vmss-test-1 -Name my-scale-set -VirtualMachineScaleSet $vmssConfig
```

## <a name="create-from-a-template"></a><span data-ttu-id="d2e1a-162">Create from a template</span><span class="sxs-lookup"><span data-stu-id="d2e1a-162">Create from a template</span></span>

<span data-ttu-id="d2e1a-163">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-163">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="d2e1a-164">You can create your own template or use one from the [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-164">You can create your own template or use one from the [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="d2e1a-165">These templates can be deployed directly to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-165">These templates can be deployed directly to your Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="d2e1a-166">To create your own template, you create a JSON text file.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-166">To create your own template, you create a JSON text file.</span></span> <span data-ttu-id="d2e1a-167">For general information about how to create and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-167">For general information about how to create and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d2e1a-168">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-168">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="d2e1a-169">For more information about how to create and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-169">For more information about how to create and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="d2e1a-170">Create from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2e1a-170">Create from Visual Studio</span></span>

<span data-ttu-id="d2e1a-171">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template to it.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-171">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template to it.</span></span> <span data-ttu-id="d2e1a-172">You can choose whether you want to import it from GitHub or the Azure Web Application Gallery.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-172">You can choose whether you want to import it from GitHub or the Azure Web Application Gallery.</span></span> <span data-ttu-id="d2e1a-173">A deployment PowerShell script is also generated for you.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-173">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="d2e1a-174">For more information, see [How to create a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-174">For more information, see [How to create a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-the-azure-portal"></a><span data-ttu-id="d2e1a-175">Create from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d2e1a-175">Create from the Azure portal</span></span>

<span data-ttu-id="d2e1a-176">The Azure portal provides a convenient way to quickly create a scale set.</span><span class="sxs-lookup"><span data-stu-id="d2e1a-176">The Azure portal provides a convenient way to quickly create a scale set.</span></span> <span data-ttu-id="d2e1a-177">For more information, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-177">For more information, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2e1a-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2e1a-178">Next steps</span></span>

<span data-ttu-id="d2e1a-179">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-179">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="d2e1a-180">Learn how to [manage your apps](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="d2e1a-180">Learn how to [manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>