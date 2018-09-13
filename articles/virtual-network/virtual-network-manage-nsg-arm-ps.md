---
title: Manage network security groups - Azure PowerShell | Microsoft Docs
description: Learn how to manage network security groups using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: edb23ae41e175061607d3a191c839e1194fa862b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551739"
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="345e0-103">Manage network security groups using PowerShell</span><span class="sxs-lookup"><span data-stu-id="345e0-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="345e0-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="345e0-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="345e0-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="345e0-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="345e0-106">Retrieve Information</span><span class="sxs-lookup"><span data-stu-id="345e0-106">Retrieve Information</span></span>
<span data-ttu-id="345e0-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span><span class="sxs-lookup"><span data-stu-id="345e0-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="345e0-108">View existing NSGs</span><span class="sxs-lookup"><span data-stu-id="345e0-108">View existing NSGs</span></span>
<span data-ttu-id="345e0-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="345e0-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="345e0-110">Expected result:</span><span class="sxs-lookup"><span data-stu-id="345e0-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="345e0-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="345e0-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="345e0-112">Expected output:</span><span class="sxs-lookup"><span data-stu-id="345e0-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="345e0-113">List all rules for an NSG</span><span class="sxs-lookup"><span data-stu-id="345e0-113">List all rules for an NSG</span></span>
<span data-ttu-id="345e0-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="345e0-115">Expected output:</span><span class="sxs-lookup"><span data-stu-id="345e0-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="345e0-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span><span class="sxs-lookup"><span data-stu-id="345e0-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="345e0-117">View NSGs associations</span><span class="sxs-lookup"><span data-stu-id="345e0-117">View NSGs associations</span></span>
<span data-ttu-id="345e0-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="345e0-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span><span class="sxs-lookup"><span data-stu-id="345e0-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="345e0-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="345e0-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="345e0-121">Manage rules</span><span class="sxs-lookup"><span data-stu-id="345e0-121">Manage rules</span></span>
<span data-ttu-id="345e0-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span><span class="sxs-lookup"><span data-stu-id="345e0-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="345e0-123">Add a rule</span><span class="sxs-lookup"><span data-stu-id="345e0-123">Add a rule</span></span>
<span data-ttu-id="345e0-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="345e0-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="345e0-125">Run the following command to retrieve the existing NSG and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="345e0-126">Run the following command to add a rule to the NSG:</span><span class="sxs-lookup"><span data-stu-id="345e0-126">Run the following command to add a rule to the NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="345e0-127">To save the changes made to the NSG, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="345e0-128">Expected output showing only the security rules:</span><span class="sxs-lookup"><span data-stu-id="345e0-128">Expected output showing only the security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="345e0-129">Change a rule</span><span class="sxs-lookup"><span data-stu-id="345e0-129">Change a rule</span></span>
<span data-ttu-id="345e0-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="345e0-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="345e0-131">Run the following command to retrieve the existing NSG and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="345e0-132">Run the following command with the new rule settings:</span><span class="sxs-lookup"><span data-stu-id="345e0-132">Run the following command with the new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange Internet `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="345e0-133">To save the changes made to the NSG, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="345e0-134">Expected output showing only the security rules:</span><span class="sxs-lookup"><span data-stu-id="345e0-134">Expected output showing only the security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="345e0-135">Delete a rule</span><span class="sxs-lookup"><span data-stu-id="345e0-135">Delete a rule</span></span>
1. <span data-ttu-id="345e0-136">Run the following command to retrieve the existing NSG and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="345e0-137">Run the following command to remove the rule from the NSG:</span><span class="sxs-lookup"><span data-stu-id="345e0-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="345e0-138">Save the changes made to the NSG, by running the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="345e0-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span><span class="sxs-lookup"><span data-stu-id="345e0-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="345e0-140">Manage associations</span><span class="sxs-lookup"><span data-stu-id="345e0-140">Manage associations</span></span>
<span data-ttu-id="345e0-141">You can associate an NSG to subnets and NICs.</span><span class="sxs-lookup"><span data-stu-id="345e0-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="345e0-142">You can also dissociate an NSG from any resource it's associated to.</span><span class="sxs-lookup"><span data-stu-id="345e0-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="345e0-143">Associate an NSG to a NIC</span><span class="sxs-lookup"><span data-stu-id="345e0-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="345e0-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="345e0-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="345e0-145">Run the following command to retrieve the existing NSG and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="345e0-146">Run the following command to retrieve the existing NIC and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="345e0-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="345e0-148">To save the changes made to the NIC, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="345e0-149">Expected output showing only the **NetworkSecurityGroup** property:</span><span class="sxs-lookup"><span data-stu-id="345e0-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="345e0-150">Dissociate an NSG from a NIC</span><span class="sxs-lookup"><span data-stu-id="345e0-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="345e0-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="345e0-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="345e0-152">Run the following command to retrieve the existing NIC and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="345e0-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="345e0-154">To save the changes made to the NIC, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="345e0-155">Expected output showing only the **NetworkSecurityGroup** property:</span><span class="sxs-lookup"><span data-stu-id="345e0-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="345e0-156">Dissociate an NSG from a subnet</span><span class="sxs-lookup"><span data-stu-id="345e0-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="345e0-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="345e0-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="345e0-158">Run the following command to retrieve the existing VNet and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="345e0-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="345e0-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="345e0-161">To save the changes made to the subnet, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="345e0-162">Expected output showing only the properties of the **FrontEnd** subnet.</span><span class="sxs-lookup"><span data-stu-id="345e0-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="345e0-163">Notice there isn't a property for **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="345e0-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="345e0-164">Associate an NSG to a subnet</span><span class="sxs-lookup"><span data-stu-id="345e0-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="345e0-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="345e0-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="345e0-166">Run the following command to retrieve the existing VNet and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="345e0-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="345e0-168">Run the following command to retrieve the existing NSG and store it in a variable:</span><span class="sxs-lookup"><span data-stu-id="345e0-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="345e0-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="345e0-170">To save the changes made to the subnet, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="345e0-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="345e0-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="345e0-172">Delete an NSG</span><span class="sxs-lookup"><span data-stu-id="345e0-172">Delete an NSG</span></span>
<span data-ttu-id="345e0-173">You can only delete an NSG if it's not associated to any resource.</span><span class="sxs-lookup"><span data-stu-id="345e0-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="345e0-174">To delete an NSG, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="345e0-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="345e0-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="345e0-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="345e0-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span><span class="sxs-lookup"><span data-stu-id="345e0-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="345e0-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span><span class="sxs-lookup"><span data-stu-id="345e0-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="345e0-178">To delete the NSG, run the following command:</span><span class="sxs-lookup"><span data-stu-id="345e0-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="345e0-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span><span class="sxs-lookup"><span data-stu-id="345e0-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="345e0-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="345e0-180">Next steps</span></span>
* <span data-ttu-id="345e0-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span><span class="sxs-lookup"><span data-stu-id="345e0-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

