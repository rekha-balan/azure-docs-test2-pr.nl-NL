---
title: Configure node endpoints in Azure Batch pool | Microsoft Docs
description: How to configure or disable access to SSH or RDP ports on compute nodes in an Azure Batch pool.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.topic: article
ms.date: 02/13/2018
ms.author: danlep
ms.openlocfilehash: 5898206761e5029f94b6d1f1b48223481ae2ca13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871611"
---
# <a name="configure-or-disable-remote-access-to-compute-nodes-in-an-azure-batch-pool"></a><span data-ttu-id="a7573-103">Configure or disable remote access to compute nodes in an Azure Batch pool</span><span class="sxs-lookup"><span data-stu-id="a7573-103">Configure or disable remote access to compute nodes in an Azure Batch pool</span></span>

<span data-ttu-id="a7573-104">By default, Batch allows a [node user](/rest/api/batchservice/computenode/adduser) with network connectivity to connect externally to a compute node in a Batch pool.</span><span class="sxs-lookup"><span data-stu-id="a7573-104">By default, Batch allows a [node user](/rest/api/batchservice/computenode/adduser) with network connectivity to connect externally to a compute node in a Batch pool.</span></span> <span data-ttu-id="a7573-105">For example, a user can connect by Remote Desktop (RDP) on port 3389 to a compute node in a Windows pool.</span><span class="sxs-lookup"><span data-stu-id="a7573-105">For example, a user can connect by Remote Desktop (RDP) on port 3389 to a compute node in a Windows pool.</span></span> <span data-ttu-id="a7573-106">Similarly, by default, a user can connect by Secure Shell (SSH) on port 22 to a compute node in a Linux pool.</span><span class="sxs-lookup"><span data-stu-id="a7573-106">Similarly, by default, a user can connect by Secure Shell (SSH) on port 22 to a compute node in a Linux pool.</span></span> 

<span data-ttu-id="a7573-107">In your environment, you might need to restrict or disable these default external access settings.</span><span class="sxs-lookup"><span data-stu-id="a7573-107">In your environment, you might need to restrict or disable these default external access settings.</span></span> <span data-ttu-id="a7573-108">You can modify these settings by using the Batch APIs to set the [PoolEndpointConfiguration](/rest/api/batchservice/pool/add#poolendpointconfiguration) property.</span><span class="sxs-lookup"><span data-stu-id="a7573-108">You can modify these settings by using the Batch APIs to set the [PoolEndpointConfiguration](/rest/api/batchservice/pool/add#poolendpointconfiguration) property.</span></span> 

## <a name="about-the-pool-endpoint-configuration"></a><span data-ttu-id="a7573-109">About the pool endpoint configuration</span><span class="sxs-lookup"><span data-stu-id="a7573-109">About the pool endpoint configuration</span></span>
<span data-ttu-id="a7573-110">The endpoint configuration consists of one or more [network address translation (NAT) pools](/rest/api/batchservice/pool/add#inboundnatpool) of frontend ports.</span><span class="sxs-lookup"><span data-stu-id="a7573-110">The endpoint configuration consists of one or more [network address translation (NAT) pools](/rest/api/batchservice/pool/add#inboundnatpool) of frontend ports.</span></span> <span data-ttu-id="a7573-111">(Do not confuse a NAT pool with the Batch pool of compute nodes.) You set up each NAT pool to override the default connection settings on the pool's compute nodes.</span><span class="sxs-lookup"><span data-stu-id="a7573-111">(Do not confuse a NAT pool with the Batch pool of compute nodes.) You set up each NAT pool to override the default connection settings on the pool's compute nodes.</span></span> 

<span data-ttu-id="a7573-112">Each NAT pool configuration includes one or more [network security group (NSG) rules](/rest/api/batchservice/pool/add#networksecuritygrouprule).</span><span class="sxs-lookup"><span data-stu-id="a7573-112">Each NAT pool configuration includes one or more [network security group (NSG) rules](/rest/api/batchservice/pool/add#networksecuritygrouprule).</span></span> <span data-ttu-id="a7573-113">Each NSG rule allows or denies certain network traffic to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="a7573-113">Each NSG rule allows or denies certain network traffic to the endpoint.</span></span> <span data-ttu-id="a7573-114">You can choose to allow or deny all traffic, traffic identified by a [service tag](../virtual-network/security-overview.md#service-tags) (such as "Internet"), or traffic from specific IP addresses or subnets.</span><span class="sxs-lookup"><span data-stu-id="a7573-114">You can choose to allow or deny all traffic, traffic identified by a [service tag](../virtual-network/security-overview.md#service-tags) (such as "Internet"), or traffic from specific IP addresses or subnets.</span></span>

### <a name="considerations"></a><span data-ttu-id="a7573-115">Considerations</span><span class="sxs-lookup"><span data-stu-id="a7573-115">Considerations</span></span>
* <span data-ttu-id="a7573-116">The pool endpoint configuration is part of the pool's [network configuration](/rest/api/batchservice/pool/add#NetworkConfiguration).</span><span class="sxs-lookup"><span data-stu-id="a7573-116">The pool endpoint configuration is part of the pool's [network configuration](/rest/api/batchservice/pool/add#NetworkConfiguration).</span></span> <span data-ttu-id="a7573-117">The network configuration can optionally include settings to join the pool to an [Azure virtual network](batch-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="a7573-117">The network configuration can optionally include settings to join the pool to an [Azure virtual network](batch-virtual-network.md).</span></span> <span data-ttu-id="a7573-118">If you set up the pool in a virtual network, you can create NSG rules that use address settings in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a7573-118">If you set up the pool in a virtual network, you can create NSG rules that use address settings in the virtual network.</span></span>
* <span data-ttu-id="a7573-119">You can configure multiple NSG rules when you configure a NAT pool.</span><span class="sxs-lookup"><span data-stu-id="a7573-119">You can configure multiple NSG rules when you configure a NAT pool.</span></span> <span data-ttu-id="a7573-120">The rules are checked in the order of priority.</span><span class="sxs-lookup"><span data-stu-id="a7573-120">The rules are checked in the order of priority.</span></span> <span data-ttu-id="a7573-121">Once a rule applies, no more rules are tested for matching.</span><span class="sxs-lookup"><span data-stu-id="a7573-121">Once a rule applies, no more rules are tested for matching.</span></span>


## <a name="example-deny-all-rdp-traffic"></a><span data-ttu-id="a7573-122">Example: Deny all RDP traffic</span><span class="sxs-lookup"><span data-stu-id="a7573-122">Example: Deny all RDP traffic</span></span>

<span data-ttu-id="a7573-123">The following C# snippet shows how to configure the RDP endpoint on compute nodes in a Windows pool to deny all network traffic.</span><span class="sxs-lookup"><span data-stu-id="a7573-123">The following C# snippet shows how to configure the RDP endpoint on compute nodes in a Windows pool to deny all network traffic.</span></span> <span data-ttu-id="a7573-124">The endpoint uses a frontend pool of ports in the range *60000 - 60099*.</span><span class="sxs-lookup"><span data-stu-id="a7573-124">The endpoint uses a frontend pool of ports in the range *60000 - 60099*.</span></span> 

```csharp
pool.NetworkConfiguration = new NetworkConfiguration
{
    EndpointConfiguration = new PoolEndpointConfiguration(new InboundNatPool[]
    {
      new InboundNatPool("RDP", InboundEndpointProtocol.Tcp, 3389, 60000, 60099, new NetworkSecurityGroupRule[]
        {
            new NetworkSecurityGroupRule(162, NetworkSecurityGroupRuleAccess.Deny, "*"),
        })
    })    
};
```

## <a name="example-deny-all-ssh-traffic-from-the-internet"></a><span data-ttu-id="a7573-125">Example: Deny all SSH traffic from the internet</span><span class="sxs-lookup"><span data-stu-id="a7573-125">Example: Deny all SSH traffic from the internet</span></span>

<span data-ttu-id="a7573-126">The following Python snippet shows how to configure the SSH endpoint on compute nodes in a Linux pool to deny all internet traffic.</span><span class="sxs-lookup"><span data-stu-id="a7573-126">The following Python snippet shows how to configure the SSH endpoint on compute nodes in a Linux pool to deny all internet traffic.</span></span> <span data-ttu-id="a7573-127">The endpoint uses a frontend pool of ports in the range *4000 - 4100*.</span><span class="sxs-lookup"><span data-stu-id="a7573-127">The endpoint uses a frontend pool of ports in the range *4000 - 4100*.</span></span> 

```python
pool.network_configuration=batchmodels.NetworkConfiguration(
    endpoint_configuration=batchmodels.PoolEndpointConfiguration(
        inbound_nat_pools=[batchmodels.InboundNATPool(
            name='SSH',
            protocol='tcp',
            backend_port=22,
            frontend_port_range_start=4000,
            frontend_port_range_end=4100,
            network_security_group_rules=[
                batchmodels.NetworkSecurityGroupRule(
                priority=170,
                access=batchmodels.NetworkSecurityGroupRuleAccess.deny,
                source_address_prefix='Internet'
                )
            ]
        )
        ]
    ) 
)
```

## <a name="example-allow-rdp-traffic-from-a-specific-ip-address"></a><span data-ttu-id="a7573-128">Example: Allow RDP traffic from a specific IP address</span><span class="sxs-lookup"><span data-stu-id="a7573-128">Example: Allow RDP traffic from a specific IP address</span></span>

<span data-ttu-id="a7573-129">The following C# snippet shows how to configure the RDP endpoint on compute nodes in a Windows pool to allow RDP access only from IP address *198.51.100.7*.</span><span class="sxs-lookup"><span data-stu-id="a7573-129">The following C# snippet shows how to configure the RDP endpoint on compute nodes in a Windows pool to allow RDP access only from IP address *198.51.100.7*.</span></span> <span data-ttu-id="a7573-130">The second NSG rule denies traffic that does not match the IP address.</span><span class="sxs-lookup"><span data-stu-id="a7573-130">The second NSG rule denies traffic that does not match the IP address.</span></span>

```csharp
pool.NetworkConfiguration = new NetworkConfiguration
{
    EndpointConfiguration = new PoolEndpointConfiguration(new InboundNatPool[]
    {
        new InboundNatPool("RDP", InboundEndpointProtocol.Tcp, 3389, 7500, 8000, new NetworkSecurityGroupRule[]
        {   
            new NetworkSecurityGroupRule(179,NetworkSecurityGroupRuleAccess.Allow, "198.51.100.7"),
            new NetworkSecurityGroupRule(180,NetworkSecurityGroupRuleAccess.Deny, "*")
        })
    })    
};
```

## <a name="example-allow-ssh-traffic-from-a-specific-subnet"></a><span data-ttu-id="a7573-131">Example: Allow SSH traffic from a specific subnet</span><span class="sxs-lookup"><span data-stu-id="a7573-131">Example: Allow SSH traffic from a specific subnet</span></span>

<span data-ttu-id="a7573-132">The following Python snippet shows how to configure the SSH endpoint on compute nodes in a Linux pool to allow access only from the subnet *192.168.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a7573-132">The following Python snippet shows how to configure the SSH endpoint on compute nodes in a Linux pool to allow access only from the subnet *192.168.1.0/24*.</span></span> <span data-ttu-id="a7573-133">The second NSG rule denies traffic that does not match the subnet.</span><span class="sxs-lookup"><span data-stu-id="a7573-133">The second NSG rule denies traffic that does not match the subnet.</span></span>

```python
pool.network_configuration=batchmodels.NetworkConfiguration(
    endpoint_configuration=batchmodels.PoolEndpointConfiguration(
        inbound_nat_pools=[batchmodels.InboundNATPool(
            name='SSH',
            protocol='tcp',
            backend_port=22,
            frontend_port_range_start=4000,
            frontend_port_range_end=4100,
            network_security_group_rules=[
                batchmodels.NetworkSecurityGroupRule(
                priority=170,
                access='allow',
                source_address_prefix='192.168.1.0/24'
                ),
                batchmodels.NetworkSecurityGroupRule(
                priority=175,
                access='deny',
                source_address_prefix='*'
                )
            ]
        )
        ]
    )
)
```

## <a name="next-steps"></a><span data-ttu-id="a7573-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7573-134">Next steps</span></span>

- <span data-ttu-id="a7573-135">For more information about NSG rules in Azure, see [Filter network traffic with network security groups](../virtual-network/security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7573-135">For more information about NSG rules in Azure, see [Filter network traffic with network security groups](../virtual-network/security-overview.md).</span></span>

- <span data-ttu-id="a7573-136">For an in-depth overview of Batch, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="a7573-136">For an in-depth overview of Batch, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>

