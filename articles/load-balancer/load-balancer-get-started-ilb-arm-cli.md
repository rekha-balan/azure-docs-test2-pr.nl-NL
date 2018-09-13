---
title: Create an Internal load balancer - Azure CLI | Microsoft Docs
description: Learn how to create an internal load balancer by using the Azure CLI in Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670662"
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="b036d-103">Create an internal load balancer by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b036d-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="b036d-110">Deploy the solution by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b036d-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="b036d-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span><span class="sxs-lookup"><span data-stu-id="b036d-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="b036d-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span><span class="sxs-lookup"><span data-stu-id="b036d-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="b036d-113">You need to create and configure the following objects to deploy a load balancer:</span><span class="sxs-lookup"><span data-stu-id="b036d-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="b036d-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span><span class="sxs-lookup"><span data-stu-id="b036d-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="b036d-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span><span class="sxs-lookup"><span data-stu-id="b036d-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="b036d-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span><span class="sxs-lookup"><span data-stu-id="b036d-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="b036d-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span><span class="sxs-lookup"><span data-stu-id="b036d-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="b036d-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span><span class="sxs-lookup"><span data-stu-id="b036d-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="b036d-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b036d-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="b036d-120">Set up CLI to use Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b036d-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="b036d-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b036d-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="b036d-122">Follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="b036d-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b036d-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span><span class="sxs-lookup"><span data-stu-id="b036d-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="b036d-124">Expected output:</span><span class="sxs-lookup"><span data-stu-id="b036d-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="b036d-125">Create an internal load balancer step by step</span><span class="sxs-lookup"><span data-stu-id="b036d-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="b036d-126">Sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="b036d-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="b036d-127">When prompted, enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="b036d-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="b036d-128">Change the command tools to Azure Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="b036d-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="b036d-129">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="b036d-129">Create a resource group</span></span>

<span data-ttu-id="b036d-130">All resources in Azure Resource Manager are associated with a resource group.</span><span class="sxs-lookup"><span data-stu-id="b036d-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="b036d-131">If you haven't done so yet, create a resource group.</span><span class="sxs-lookup"><span data-stu-id="b036d-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="b036d-132">Create an internal load balancer set</span><span class="sxs-lookup"><span data-stu-id="b036d-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="b036d-133">Create an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="b036d-133">Create an internal load balancer</span></span>

    <span data-ttu-id="b036d-134">In the following scenario, a resource group named nrprg is created in East US region.</span><span class="sxs-lookup"><span data-stu-id="b036d-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.

2. <span data-ttu-id="b036d-136">Create a front-end IP address for the internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="b036d-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="b036d-137">The IP address that you use must be within the subnet range of your virtual network.</span><span class="sxs-lookup"><span data-stu-id="b036d-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="b036d-138">Create the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="b036d-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="b036d-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span><span class="sxs-lookup"><span data-stu-id="b036d-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="b036d-140">Create a load balancer rule for the internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="b036d-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="b036d-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span><span class="sxs-lookup"><span data-stu-id="b036d-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="b036d-142">Create inbound NAT rules.</span><span class="sxs-lookup"><span data-stu-id="b036d-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="b036d-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span><span class="sxs-lookup"><span data-stu-id="b036d-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="b036d-144">The previous steps created two NAT rules  for remote desktop.</span><span class="sxs-lookup"><span data-stu-id="b036d-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="b036d-145">Create health probes for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b036d-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="b036d-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span><span class="sxs-lookup"><span data-stu-id="b036d-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="b036d-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span><span class="sxs-lookup"><span data-stu-id="b036d-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios. The IP address is 168.63.129.16. This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.
    > With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set. If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.

## <a name="create-nics"></a><span data-ttu-id="b036d-153">Create NICs</span><span class="sxs-lookup"><span data-stu-id="b036d-153">Create NICs</span></span>

<span data-ttu-id="b036d-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span><span class="sxs-lookup"><span data-stu-id="b036d-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="b036d-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="b036d-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="b036d-156">Expected output:</span><span class="sxs-lookup"><span data-stu-id="b036d-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="b036d-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="b036d-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="b036d-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="b036d-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="b036d-159">A storage account called *web1nrp* is created before the following command runs:</span><span class="sxs-lookup"><span data-stu-id="b036d-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > VMs in a load balancer need to be in the same availability set. Use `azure availset create` to create an availability set.

4. <span data-ttu-id="b036d-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="b036d-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="b036d-163">A storage account called *web1nrp* was created before running the following command.</span><span class="sxs-lookup"><span data-stu-id="b036d-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="b036d-164">Delete a load balancer</span><span class="sxs-lookup"><span data-stu-id="b036d-164">Delete a load balancer</span></span>

<span data-ttu-id="b036d-165">To remove a load balancer, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b036d-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="b036d-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="b036d-166">Next steps</span></span>

[<span data-ttu-id="b036d-167">Configure a load balancer distribution mode by using source IP affinity</span><span class="sxs-lookup"><span data-stu-id="b036d-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b036d-168">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="b036d-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

