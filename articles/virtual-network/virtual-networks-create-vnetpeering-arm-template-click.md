---
title: Azure Virtual Network peering - Template | Microsoft Docs
description: Learn how to create a virtual network peering using an Azure Resource Manager template.
services: virtual-network
documentationcenter: ''
author: narayanannamalai
manager: jefco
editor: ''
tags: azure-resource-manager
ms.assetid: 75f8d10e-23e8-44bd-9972-aab74048cf38
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: narayan;annahar
ms.openlocfilehash: 7b4fda3ffb269c6a9de407bbd9af32d90768504f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661759"
---
# <a name="create-a-virtual-network-peering-using-an-azure-resource-manager-template"></a><span data-ttu-id="197fb-103">Create a virtual network peering using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="197fb-103">Create a virtual network peering using an Azure Resource Manager template</span></span>
[!INCLUDE [virtual-networks-create-vnet-selectors-arm-include](../../includes/virtual-networks-create-vnetpeering-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnetpeering-intro-include.md)]

[!INCLUDE [virtual-networks-create-vnet-scenario-basic-include](../../includes/virtual-networks-create-vnetpeering-scenario-basic-include.md)]

<span data-ttu-id="197fb-104">To create a VNet peering by using Resource Manager templates, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="197fb-104">To create a VNet peering by using Resource Manager templates, complete the following steps:</span></span>

1. <span data-ttu-id="197fb-105">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="197fb-105">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>

   > [!NOTE]
   > <span data-ttu-id="197fb-106">The PowerShell cmdlet for managing VNet peering is shipped with [Azure PowerShell 1.6.](http://www.powershellgallery.com/packages/Azure/1.6.0)</span><span class="sxs-lookup"><span data-stu-id="197fb-106">The PowerShell cmdlet for managing VNet peering is shipped with [Azure PowerShell 1.6.](http://www.powershellgallery.com/packages/Azure/1.6.0)</span></span>
   > 
   > 
2. <span data-ttu-id="197fb-107">The text below shows the definition of a VNet peering link for VNet1 to VNet2, based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="197fb-107">The text below shows the definition of a VNet peering link for VNet1 to VNet2, based on the scenario above.</span></span> <span data-ttu-id="197fb-108">Copy the content below and save it to a file named VNetPeeringVNet1.json.</span><span class="sxs-lookup"><span data-stu-id="197fb-108">Copy the content below and save it to a file named VNetPeeringVNet1.json.</span></span>

    ```json
        {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [
            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "VNet1/LinkToVNet2",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": false,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks', 'vnet2')]"       
        }
            }
            }
        ]
        }
    ```
3. <span data-ttu-id="197fb-109">The section below shows the definition of a VNet peering link for VNet2 to VNet1, based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="197fb-109">The section below shows the definition of a VNet peering link for VNet2 to VNet1, based on the scenario above.</span></span>  <span data-ttu-id="197fb-110">Copy the content below and save it to a file named VNetPeeringVNet2.json.</span><span class="sxs-lookup"><span data-stu-id="197fb-110">Copy the content below and save it to a file named VNetPeeringVNet2.json.</span></span>

    ```json
        {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [
            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "VNet2/LinkToVNet1",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": false,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks', 'vnet1')]"       
                }
            }
            }
        ]
        }
    ```
    <span data-ttu-id="197fb-111">As seen in the template above, there are a few configurable properties for VNet peering:</span><span class="sxs-lookup"><span data-stu-id="197fb-111">As seen in the template above, there are a few configurable properties for VNet peering:</span></span>
   
   | <span data-ttu-id="197fb-112">Option</span><span class="sxs-lookup"><span data-stu-id="197fb-112">Option</span></span> | <span data-ttu-id="197fb-113">Description</span><span class="sxs-lookup"><span data-stu-id="197fb-113">Description</span></span> | <span data-ttu-id="197fb-114">Default</span><span class="sxs-lookup"><span data-stu-id="197fb-114">Default</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="197fb-115">AllowVirtualNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="197fb-115">AllowVirtualNetworkAccess</span></span> |<span data-ttu-id="197fb-116">Whether or not the address space of a peer VNet is included as part of the virtual_network tag.</span><span class="sxs-lookup"><span data-stu-id="197fb-116">Whether or not the address space of a peer VNet is included as part of the virtual_network tag.</span></span> |<span data-ttu-id="197fb-117">Yes</span><span class="sxs-lookup"><span data-stu-id="197fb-117">Yes</span></span> |
   | <span data-ttu-id="197fb-118">AllowForwardedTraffic</span><span class="sxs-lookup"><span data-stu-id="197fb-118">AllowForwardedTraffic</span></span> |<span data-ttu-id="197fb-119">Whether traffic not originating from a peered VNet is accepted or dropped.</span><span class="sxs-lookup"><span data-stu-id="197fb-119">Whether traffic not originating from a peered VNet is accepted or dropped.</span></span> |<span data-ttu-id="197fb-120">No</span><span class="sxs-lookup"><span data-stu-id="197fb-120">No</span></span> |
   | <span data-ttu-id="197fb-121">AllowGatewayTransit</span><span class="sxs-lookup"><span data-stu-id="197fb-121">AllowGatewayTransit</span></span> |<span data-ttu-id="197fb-122">Allows the peer VNet to use your VNet gateway.</span><span class="sxs-lookup"><span data-stu-id="197fb-122">Allows the peer VNet to use your VNet gateway.</span></span> |<span data-ttu-id="197fb-123">No</span><span class="sxs-lookup"><span data-stu-id="197fb-123">No</span></span> |
   | <span data-ttu-id="197fb-124">UseRemoteGateways</span><span class="sxs-lookup"><span data-stu-id="197fb-124">UseRemoteGateways</span></span> |<span data-ttu-id="197fb-125">Use your peer’s VNet gateway.</span><span class="sxs-lookup"><span data-stu-id="197fb-125">Use your peer’s VNet gateway.</span></span> <span data-ttu-id="197fb-126">The peer VNet must have a gateway configured and AllowGatewayTransit selected.</span><span class="sxs-lookup"><span data-stu-id="197fb-126">The peer VNet must have a gateway configured and AllowGatewayTransit selected.</span></span> <span data-ttu-id="197fb-127">You cannot use this option if you have a gateway configured.</span><span class="sxs-lookup"><span data-stu-id="197fb-127">You cannot use this option if you have a gateway configured.</span></span> |<span data-ttu-id="197fb-128">No</span><span class="sxs-lookup"><span data-stu-id="197fb-128">No</span></span> |
   
    <span data-ttu-id="197fb-129">Each link in VNet peering has the set of properties above.</span><span class="sxs-lookup"><span data-stu-id="197fb-129">Each link in VNet peering has the set of properties above.</span></span> <span data-ttu-id="197fb-130">For example, you can set AllowVirtualNetworkAccess to True for VNet peering link VNet1 to VNet2 and set it to False for the VNet peering link in the other direction.</span><span class="sxs-lookup"><span data-stu-id="197fb-130">For example, you can set AllowVirtualNetworkAccess to True for VNet peering link VNet1 to VNet2 and set it to False for the VNet peering link in the other direction.</span></span>
4. <span data-ttu-id="197fb-131">To deploy the template file, you can run the `New-AzureRmResourceGroupDeployment` to create or update the deployment.</span><span class="sxs-lookup"><span data-stu-id="197fb-131">To deploy the template file, you can run the `New-AzureRmResourceGroupDeployment` to create or update the deployment.</span></span> <span data-ttu-id="197fb-132">For more information about using Resource Manager templates, please refer to this [article](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="197fb-132">For more information about using Resource Manager templates, please refer to this [article](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName <resource group name> -TemplateFile <template file path> -DeploymentDebugLogLevel all
    ```

   > [!NOTE]
   > <span data-ttu-id="197fb-133">Replace the resource group name and template file, as appropriate.</span><span class="sxs-lookup"><span data-stu-id="197fb-133">Replace the resource group name and template file, as appropriate.</span></span>
   > 
   > 
   
    <span data-ttu-id="197fb-134">The following is an example based on the previous scenario:</span><span class="sxs-lookup"><span data-stu-id="197fb-134">The following is an example based on the previous scenario:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName VNet101 -TemplateFile .\VNetPeeringVNet1.json -DeploymentDebugLogLevel all
    ```

    <span data-ttu-id="197fb-135">Returned output:</span><span class="sxs-lookup"><span data-stu-id="197fb-135">Returned output:</span></span>
   
        DeploymentName        : VNetPeeringVNet1
        ResourceGroupName    : VNet101
        ProvisioningState        : Succeeded
        Timestamp            : MM/DD/YEAR 9:05:03 AM
        Mode            : Incremental
        TemplateLink        :
        Parameters            :
        Outputs            :
        DeploymentDebugLogLevel : RequestContent, ResponseContent
   
    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName VNet101 -TemplateFile .\VNetPeeringVNet2.json -DeploymentDebugLogLevel all
    ```

    <span data-ttu-id="197fb-136">Returned output:</span><span class="sxs-lookup"><span data-stu-id="197fb-136">Returned output:</span></span>
   
        DeploymentName        : VNetPeeringVNet2
        ResourceGroupName    : VNet101
        ProvisioningState        : Succeeded
        Timestamp            : MM/DD/YEAR 9:07:22 AM
        Mode            : Incremental
        TemplateLink        :
        Parameters            :
        Outputs            :
        DeploymentDebugLogLevel : RequestContent, ResponseContent
5. <span data-ttu-id="197fb-137">After the deployment is finished, run the following cmdlet to view the peering state:</span><span class="sxs-lookup"><span data-stu-id="197fb-137">After the deployment is finished, run the following cmdlet to view the peering state:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering -VirtualNetworkName VNet1 -ResourceGroupName VNet101 -Name linktoVNet2
    ```

    <span data-ttu-id="197fb-138">Returned output:</span><span class="sxs-lookup"><span data-stu-id="197fb-138">Returned output:</span></span>
   
        Name            : LinkToVNet2
        Id                : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VNet101/providers/Microsoft.Network/virtualNetworks/VNet1/virtualNetworkPeerings/LinkToVNet2
        Etag            : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ResourceGroupName    : VNet101
        VirtualNetworkName    : VNet1
        ProvisioningState        : Succeeded
        RemoteVirtualNetwork    : {
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VNet101/providers/Microsoft.Network/virtualNetworks/VNet2"
                                        }
        AllowVirtualNetworkAccess    : True
        AllowForwardedTraffic            : False
        AllowGatewayTransit              : False
        UseRemoteGateways                : False
        RemoteGateways                   : null
        RemoteVirtualNetworkAddressSpace : null
   
    <span data-ttu-id="197fb-139">After the peering is established in this scenario, you should be able to initiate the connections from any VM to any VM across both VNets.</span><span class="sxs-lookup"><span data-stu-id="197fb-139">After the peering is established in this scenario, you should be able to initiate the connections from any VM to any VM across both VNets.</span></span> <span data-ttu-id="197fb-140">By default, `AllowVirtualNetworkAccess` is *True* and VNet peering will provision the proper ACLs to allow the communication between VNets.</span><span class="sxs-lookup"><span data-stu-id="197fb-140">By default, `AllowVirtualNetworkAccess` is *True* and VNet peering will provision the proper ACLs to allow the communication between VNets.</span></span> <span data-ttu-id="197fb-141">You can still apply network security group (NSG) rules to block connectivity between specific subnets or virtual machines to gain fine-grain control of access between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="197fb-141">You can still apply network security group (NSG) rules to block connectivity between specific subnets or virtual machines to gain fine-grain control of access between two virtual networks.</span></span> <span data-ttu-id="197fb-142">Read the [Network security groups](virtual-networks-create-nsg-arm-ps.md) article to learn more about NSGs.</span><span class="sxs-lookup"><span data-stu-id="197fb-142">Read the [Network security groups](virtual-networks-create-nsg-arm-ps.md) article to learn more about NSGs.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-crosssub-include](../../includes/virtual-networks-create-vnetpeering-scenario-crosssub-include.md)]

<span data-ttu-id="197fb-143">To create a VNet peering across subscriptions, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="197fb-143">To create a VNet peering across subscriptions, complete the following steps:</span></span>

1. <span data-ttu-id="197fb-144">Sign in to Azure with privileged User-A's account in Subscription-A and run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="197fb-144">Sign in to Azure with privileged User-A's account in Subscription-A and run the following cmdlet:</span></span>

    ```powershell
    New-AzureRmRoleAssignment -SignInName <UserB ID> -RoleDefinitionName "Network Contributor" -Scope /subscriptions/<Subscription-A-ID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Network/VirtualNetwork/VNet5
    ```

    <span data-ttu-id="197fb-145">This is not a requirement.</span><span class="sxs-lookup"><span data-stu-id="197fb-145">This is not a requirement.</span></span> <span data-ttu-id="197fb-146">Peering can be established even if users individually raise peering requests for their respective Vnets as long as the requests match.</span><span class="sxs-lookup"><span data-stu-id="197fb-146">Peering can be established even if users individually raise peering requests for their respective Vnets as long as the requests match.</span></span> <span data-ttu-id="197fb-147">Adding a privileged user of the other VNet as users in the local VNet makes it easier to do the setup.</span><span class="sxs-lookup"><span data-stu-id="197fb-147">Adding a privileged user of the other VNet as users in the local VNet makes it easier to do the setup.</span></span>
2. <span data-ttu-id="197fb-148">Sign in to Azure with privileged User-B's account for Subscription-B and run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="197fb-148">Sign in to Azure with privileged User-B's account for Subscription-B and run the following cmdlet:</span></span>

    ```powershell
    New-AzureRmRoleAssignment -SignInName <UserA ID> -RoleDefinitionName "Network Contributor" -Scope /subscriptions/<Subscription-B-ID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Network/VirtualNetwork/VNet3
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="197fb-149">If the peering you're creating is between two VNets created through the Azure Resource Manager deployment model, continue with the remaining steps in this section.</span><span class="sxs-lookup"><span data-stu-id="197fb-149">If the peering you're creating is between two VNets created through the Azure Resource Manager deployment model, continue with the remaining steps in this section.</span></span> <span data-ttu-id="197fb-150">If the two VNets were created through different deployment models, skip the remaining steps of this section and complete the steps in the [Peering virtual networks created through different deployment models](#x-model) section of this article.</span><span class="sxs-lookup"><span data-stu-id="197fb-150">If the two VNets were created through different deployment models, skip the remaining steps of this section and complete the steps in the [Peering virtual networks created through different deployment models](#x-model) section of this article.</span></span>

3. <span data-ttu-id="197fb-151">In User-A’s login session, run this cmdlet:</span><span class="sxs-lookup"><span data-stu-id="197fb-151">In User-A’s login session, run this cmdlet:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName VNet101 -TemplateFile .\VNetPeeringVNet3.json -DeploymentDebugLogLevel all
    ```
   
    <span data-ttu-id="197fb-152">The json is as follows:</span><span class="sxs-lookup"><span data-stu-id="197fb-152">The json is as follows:</span></span>

    ```json
        {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [
            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "VNet3/LinkToVNet5",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": false,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "/subscriptions/<Subscription-B-ID>/resourceGroups/<resource group name>/providers/Microsoft.Network/virtualNetworks/VNet5"
                }
            }
            }
        ]
        }
    ```
4. <span data-ttu-id="197fb-153">In User-B’s login session, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="197fb-153">In User-B’s login session, run the following cmdlet:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName VNet101 -TemplateFile .\VNetPeeringVNet5.json -DeploymentDebugLogLevel all
    ```

    <span data-ttu-id="197fb-154">The JSON is as follows:</span><span class="sxs-lookup"><span data-stu-id="197fb-154">The JSON is as follows:</span></span>

    ```json
        {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [
            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "VNet5/LinkToVNet3",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": false,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "/subscriptions/Subscription-A-ID /resourceGroups/<resource group name>/providers/Microsoft.Network/virtualNetworks/VNet3"
                }
            }
            }
        ]
        }
    ```

    <span data-ttu-id="197fb-155">After peering is established in this scenario, you should be able to initiate the connections from any virtual machine to any virtual machine of both VNets across different subscriptions.</span><span class="sxs-lookup"><span data-stu-id="197fb-155">After peering is established in this scenario, you should be able to initiate the connections from any virtual machine to any virtual machine of both VNets across different subscriptions.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-transit-include](../../includes/virtual-networks-create-vnetpeering-scenario-transit-include.md)]

1. <span data-ttu-id="197fb-156">In this scenario, you can deploy the following sample template to establish the VNet peering.</span><span class="sxs-lookup"><span data-stu-id="197fb-156">In this scenario, you can deploy the following sample template to establish the VNet peering.</span></span> <span data-ttu-id="197fb-157">You'll need to set the `AllowForwardedTraffic` property to *True*, which allows the network virtual appliance in the peered VNet to send and receive traffic.</span><span class="sxs-lookup"><span data-stu-id="197fb-157">You'll need to set the `AllowForwardedTraffic` property to *True*, which allows the network virtual appliance in the peered VNet to send and receive traffic.</span></span>

    <span data-ttu-id="197fb-158">The following JSON is the content of a template for creating a VNet peering from HubVNet to VNet1.</span><span class="sxs-lookup"><span data-stu-id="197fb-158">The following JSON is the content of a template for creating a VNet peering from HubVNet to VNet1.</span></span> <span data-ttu-id="197fb-159">Note that AllowForwardedTraffic is set to false.</span><span class="sxs-lookup"><span data-stu-id="197fb-159">Note that AllowForwardedTraffic is set to false.</span></span>

    ```json
        {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [
            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "HubVNet/LinkToVNet1",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": false,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks', 'vnet1')]"       
                }
            }
            }
        ]
        }
    ```
2. <span data-ttu-id="197fb-160">The following JSON is the content of a template for creating a VNet peering from VNet1 to HubVnet.</span><span class="sxs-lookup"><span data-stu-id="197fb-160">The following JSON is the content of a template for creating a VNet peering from VNet1 to HubVnet.</span></span> <span data-ttu-id="197fb-161">Note that AllowForwardedTraffic is set to true.</span><span class="sxs-lookup"><span data-stu-id="197fb-161">Note that AllowForwardedTraffic is set to true.</span></span>

    ```json
        {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [
            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "VNet1/LinkToHubVNet",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": true,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks', 'HubVnet')]"       
                }
            }
            }
        ]
        }
    ```
3. <span data-ttu-id="197fb-162">After peering is established, you can refer to this [article](virtual-network-create-udr-arm-ps.md) to define user-defined routes (UDR) to redirect VNet1 traffic through a virtual appliance to use its capabilities.</span><span class="sxs-lookup"><span data-stu-id="197fb-162">After peering is established, you can refer to this [article](virtual-network-create-udr-arm-ps.md) to define user-defined routes (UDR) to redirect VNet1 traffic through a virtual appliance to use its capabilities.</span></span> <span data-ttu-id="197fb-163">When you specify the next hop address in route, you can set it to the IP address of the virtual appliance in the peer VNet HubVNet.</span><span class="sxs-lookup"><span data-stu-id="197fb-163">When you specify the next hop address in route, you can set it to the IP address of the virtual appliance in the peer VNet HubVNet.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-asmtoarm-include](../../includes/virtual-networks-create-vnetpeering-scenario-asmtoarm-include.md)]

<span data-ttu-id="197fb-164">To create a peering between virtual networks from different deployment models, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="197fb-164">To create a peering between virtual networks from different deployment models, complete the following steps:</span></span>

1. <span data-ttu-id="197fb-165">If you are creating a peering between VNets deployed through different deployment models in the *same* subscription, skip to step 2.</span><span class="sxs-lookup"><span data-stu-id="197fb-165">If you are creating a peering between VNets deployed through different deployment models in the *same* subscription, skip to step 2.</span></span> <span data-ttu-id="197fb-166">The ability to create a VNet peering between VNets deployed through different deployment models in *different* subscriptions is in **preview** release.</span><span class="sxs-lookup"><span data-stu-id="197fb-166">The ability to create a VNet peering between VNets deployed through different deployment models in *different* subscriptions is in **preview** release.</span></span> <span data-ttu-id="197fb-167">Capabilities in preview release do not have the same level of reliability and service level agreement as general release capabilities.</span><span class="sxs-lookup"><span data-stu-id="197fb-167">Capabilities in preview release do not have the same level of reliability and service level agreement as general release capabilities.</span></span> <span data-ttu-id="197fb-168">If you are creating a peering between VNets deployed through different deployment models in different subscriptions you must first complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="197fb-168">If you are creating a peering between VNets deployed through different deployment models in different subscriptions you must first complete the following tasks:</span></span>
    - <span data-ttu-id="197fb-169">Register the preview capability in your Azure subscription by entering the following commands from PowerShell: `Register-AzureRmProviderFeature -FeatureName AllowClassicCrossSubscriptionPeering -ProviderNamespace Microsoft.Network`  and `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network`</span><span class="sxs-lookup"><span data-stu-id="197fb-169">Register the preview capability in your Azure subscription by entering the following commands from PowerShell: `Register-AzureRmProviderFeature -FeatureName AllowClassicCrossSubscriptionPeering -ProviderNamespace Microsoft.Network`  and `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network`</span></span>
    - <span data-ttu-id="197fb-170">Complete steps 1-2 in the [Peering across subscriptions](#x-sub) section of this article.</span><span class="sxs-lookup"><span data-stu-id="197fb-170">Complete steps 1-2 in the [Peering across subscriptions](#x-sub) section of this article.</span></span>
2. <span data-ttu-id="197fb-171">The text below shows the definition of a VNet peering link for VNET1 to VNET2 in this scenario.</span><span class="sxs-lookup"><span data-stu-id="197fb-171">The text below shows the definition of a VNet peering link for VNET1 to VNET2 in this scenario.</span></span> <span data-ttu-id="197fb-172">Only one link is required to peer a classic virtual network to a Azure resource manager virtual network.</span><span class="sxs-lookup"><span data-stu-id="197fb-172">Only one link is required to peer a classic virtual network to a Azure resource manager virtual network.</span></span>

    <span data-ttu-id="197fb-173">Be sure to put in your subscription ID for where the classic virtual network or VNET2 is located and change MyResouceGroup to the appropriate resource group name.</span><span class="sxs-lookup"><span data-stu-id="197fb-173">Be sure to put in your subscription ID for where the classic virtual network or VNET2 is located and change MyResouceGroup to the appropriate resource group name.</span></span>

    ```json
       {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
        },
        "variables": {
        },
        "resources": [

            {
            "apiVersion": "2016-06-01",
            "type": "Microsoft.Network/virtualNetworks/virtualNetworkPeerings",
            "name": "VNET1/LinkToVNET2",
            "location": "[resourceGroup().location]",
            "properties": {
            "allowVirtualNetworkAccess": true,
            "allowForwardedTraffic": false,
            "allowGatewayTransit": false,
            "useRemoteGateways": false,
                "remoteVirtualNetwork": {
                "id": "[resourceId('Microsoft.ClassicNetwork/virtualNetworks', 'VNET2')]"
        }

            }
            }
        ]
        }
    ```
3. <span data-ttu-id="197fb-174">To deploy the template file, run the following cmdlet to create or update the deployment:</span><span class="sxs-lookup"><span data-stu-id="197fb-174">To deploy the template file, run the following cmdlet to create or update the deployment:</span></span>

    ```powershell
        New-AzureRmResourceGroupDeployment -ResourceGroupName MyResourceGroup -TemplateFile .\VnetPeering.json -DeploymentDebugLogLevel all
    ```

    <span data-ttu-id="197fb-175">Returned output:</span><span class="sxs-lookup"><span data-stu-id="197fb-175">Returned output:</span></span>
   
        DeploymentName          : VnetPeering
        ResourceGroupName       : MyResourceGroup
        ProvisioningState       : Succeeded
        Timestamp               : XX/XX/YYYY 5:42:33 PM
        Mode                    : Incremental
        TemplateLink            :
        Parameters              :
        Outputs                 :
        DeploymentDebugLogLevel : RequestContent, ResponseContent
4. <span data-ttu-id="197fb-176">After the deployment succeeds, you can run the following cmdlet to view the peering state:</span><span class="sxs-lookup"><span data-stu-id="197fb-176">After the deployment succeeds, you can run the following cmdlet to view the peering state:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering -VirtualNetworkName VNET1 -ResourceGroupName MyResourceGroup -Name LinkToVNET2
    ```

    <span data-ttu-id="197fb-177">Returned output:</span><span class="sxs-lookup"><span data-stu-id="197fb-177">Returned output:</span></span>
   
        Name                             : LinkToVNET2
        Id                               : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResource
                                   Group/providers/Microsoft.Network/virtualNetworks/VNET1/virtualNetworkPeering
                                   s/LinkToVNET2
        Etag                             : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ResourceGroupName                : MyResourceGroup
        VirtualNetworkName               : VNET1
        PeeringState                     : Connected
        ProvisioningState                : Succeeded
        RemoteVirtualNetwork             : {
                                     "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/M
                                   yResourceGroup/providers/Microsoft.ClassicNetwork/virtualNetworks/VNET2"
                                   }
        AllowVirtualNetworkAccess        : True
        AllowForwardedTraffic            : False
        AllowGatewayTransit              : False
        UseRemoteGateways                : False
        RemoteGateways                   : null
        RemoteVirtualNetworkAddressSpace : null

    <span data-ttu-id="197fb-178">After peering is established between a classic VNet and a resource manager VNet, you should be able to initiate connections from any virtual machine in VNET1 to any virtual machine in VNET2 and vice versa.</span><span class="sxs-lookup"><span data-stu-id="197fb-178">After peering is established between a classic VNet and a resource manager VNet, you should be able to initiate connections from any virtual machine in VNET1 to any virtual machine in VNET2 and vice versa.</span></span>

