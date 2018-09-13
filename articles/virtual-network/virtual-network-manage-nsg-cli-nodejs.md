---
title: Manage network security groups - Azure CLI 1.0 | Microsoft Docs
description: Learn how to manage network security groups using the Azure command-line interface (CLI) 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e53c3ff2ffbef95d6b72ca6afb3b4de377f0389
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661771"
---
# <a name="manage-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="2c2e8-103">Manage network security groups using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2c2e8-103">Manage network security groups using the Azure CLI 1.0</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="2c2e8-104">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="2c2e8-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="2c2e8-105">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="2c2e8-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for the classic and resource management deployment models</span><span class="sxs-lookup"><span data-stu-id="2c2e8-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="2c2e8-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for the resource management deployment model (this article)</span><span class="sxs-lookup"><span data-stu-id="2c2e8-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="2c2e8-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2c2e8-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2c2e8-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="2c2e8-110">Retrieve Information</span><span class="sxs-lookup"><span data-stu-id="2c2e8-110">Retrieve Information</span></span>
<span data-ttu-id="2c2e8-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="2c2e8-112">View existing NSGs</span><span class="sxs-lookup"><span data-stu-id="2c2e8-112">View existing NSGs</span></span>
<span data-ttu-id="2c2e8-113">To view the list of NSGs in a specific resource group, run the `azure network nsg list` command as shown below.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-113">To view the list of NSGs in a specific resource group, run the `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="2c2e8-114">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting the network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="2c2e8-115">List all rules for an NSG</span><span class="sxs-lookup"><span data-stu-id="2c2e8-115">List all rules for an NSG</span></span>
<span data-ttu-id="2c2e8-116">To view the rules of an NSG named **NSG-FrontEnd**, run the `azure network nsg show` command as shown below.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-116">To view the rules of an NSG named **NSG-FrontEnd**, run the `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="2c2e8-117">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="2c2e8-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` to list the rules from the **NSG-FrontEnd** NSG.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` to list the rules from the **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="2c2e8-119">View NSG associations</span><span class="sxs-lookup"><span data-stu-id="2c2e8-119">View NSG associations</span></span>

<span data-ttu-id="2c2e8-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `azure network nsg show` command as shown below.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="2c2e8-121">Notice that the only difference is the use of the **--json** parameter.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-121">Notice that the only difference is the use of the **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="2c2e8-122">Look for the **networkInterfaces** and **subnets** properties as shown below:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-122">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="2c2e8-123">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-123">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="2c2e8-124">Manage rules</span><span class="sxs-lookup"><span data-stu-id="2c2e8-124">Manage rules</span></span>
<span data-ttu-id="2c2e8-125">You can add rules to an existing NSG, edit existing rules, and remove rules.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-125">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="2c2e8-126">Add a rule</span><span class="sxs-lookup"><span data-stu-id="2c2e8-126">Add a rule</span></span>
<span data-ttu-id="2c2e8-127">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-127">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access to port 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="2c2e8-128">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up the network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="2c2e8-129">Change a rule</span><span class="sxs-lookup"><span data-stu-id="2c2e8-129">Change a rule</span></span>
<span data-ttu-id="2c2e8-130">To change the rule created above to allow inbound traffic from the **Internet** only, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-130">To change the rule created above to allow inbound traffic from the **Internet** only, run the following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="2c2e8-131">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up the network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="2c2e8-132">Delete a rule</span><span class="sxs-lookup"><span data-stu-id="2c2e8-132">Delete a rule</span></span>
<span data-ttu-id="2c2e8-133">To delete the rule created above, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-133">To delete the rule created above, run the following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="2c2e8-134">The `--quiet` parameter ensures you don't need to confirm the deletion.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-134">The `--quiet` parameter ensures you don't need to confirm the deletion.</span></span>
>

<span data-ttu-id="2c2e8-135">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up the network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="2c2e8-136">Manage associations</span><span class="sxs-lookup"><span data-stu-id="2c2e8-136">Manage associations</span></span>
<span data-ttu-id="2c2e8-137">You can associate an NSG to subnets and NICs.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-137">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="2c2e8-138">You can also dissociate an NSG from any resource it's associated to.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="2c2e8-139">Associate an NSG to a NIC</span><span class="sxs-lookup"><span data-stu-id="2c2e8-139">Associate an NSG to a NIC</span></span>
<span data-ttu-id="2c2e8-140">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-140">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="2c2e8-141">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Looking up the network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="2c2e8-142">Dissociate an NSG from a NIC</span><span class="sxs-lookup"><span data-stu-id="2c2e8-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="2c2e8-143">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-143">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="2c2e8-144">Notice the "" (empty) value for the `network-security-group-id` parameter.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-144">Notice the "" (empty) value for the `network-security-group-id` parameter.</span></span> <span data-ttu-id="2c2e8-145">That is how you remove an association to an NSG.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-145">That is how you remove an association to an NSG.</span></span> <span data-ttu-id="2c2e8-146">You can't do the same with the `network-security-group-name` parameter.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-146">You can't do the same with the `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="2c2e8-147">Expected result:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="2c2e8-148">Dissociate an NSG from a subnet</span><span class="sxs-lookup"><span data-stu-id="2c2e8-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="2c2e8-149">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-149">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="2c2e8-150">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up the subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up the subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="2c2e8-151">Associate an NSG to a subnet</span><span class="sxs-lookup"><span data-stu-id="2c2e8-151">Associate an NSG to a subnet</span></span>
<span data-ttu-id="2c2e8-152">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-152">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="2c2e8-153">The command above only works because the **NSG-FrontEnd** NSG is in the same resource group as the virtual network **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-153">The command above only works because the **NSG-FrontEnd** NSG is in the same resource group as the virtual network **TestVNet**.</span></span> <span data-ttu-id="2c2e8-154">If the NSG is in a different resource group, you need to use the `--network-security-group-id` parameter instead, and provide the full id for the NSG.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-154">If the NSG is in a different resource group, you need to use the `--network-security-group-id` parameter instead, and provide the full id for the NSG.</span></span> <span data-ttu-id="2c2e8-155">You can retrieve the id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for the **id** property.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-155">You can retrieve the id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for the **id** property.</span></span> 
> 

<span data-ttu-id="2c2e8-156">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up the subnet "FrontEnd"
        + Looking up the network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="2c2e8-157">Delete an NSG</span><span class="sxs-lookup"><span data-stu-id="2c2e8-157">Delete an NSG</span></span>
<span data-ttu-id="2c2e8-158">You can only delete an NSG if it's not associated to any resource.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-158">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="2c2e8-159">To delete an NSG, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-159">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="2c2e8-160">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="2c2e8-160">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="2c2e8-161">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-161">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="2c2e8-162">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-162">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="2c2e8-163">To delete the NSG, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-163">To delete the NSG, run the following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="2c2e8-164">Expected output:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up the network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="2c2e8-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c2e8-165">Next steps</span></span>
* <span data-ttu-id="2c2e8-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

