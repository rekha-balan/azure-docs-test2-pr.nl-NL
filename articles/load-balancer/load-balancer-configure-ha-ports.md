---
title: Configure High Availability Ports for Azure Load Balancer| Microsoft Docs
description: Learn how to use High Availability Ports for load balancing internal traffic on all ports
services: load-balancer
documentationcenter: na
author: rdhillon
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2018
ms.author: kumud
ms.openlocfilehash: 117e73c35bb66578976ef990e61eea606e2e8e36
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869607"
---
# <a name="configure-high-availability-ports-for-an-internal-load-balancer"></a><span data-ttu-id="a9e68-103">Configure High Availability Ports for an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="a9e68-103">Configure High Availability Ports for an internal load balancer</span></span>

<span data-ttu-id="a9e68-104">This article provides an example deployment of High Availability Ports on an internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="a9e68-104">This article provides an example deployment of High Availability Ports on an internal load balancer.</span></span> <span data-ttu-id="a9e68-105">For more information on configurations specific to network virtual appliances (NVAs), see the corresponding provider websites.</span><span class="sxs-lookup"><span data-stu-id="a9e68-105">For more information on configurations specific to network virtual appliances (NVAs), see the corresponding provider websites.</span></span>

>[!NOTE]
><span data-ttu-id="a9e68-106">Azure Load Balancer supports two different types: Basic and Standard.</span><span class="sxs-lookup"><span data-stu-id="a9e68-106">Azure Load Balancer supports two different types: Basic and Standard.</span></span> <span data-ttu-id="a9e68-107">This article discusses Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="a9e68-107">This article discusses Standard Load Balancer.</span></span> <span data-ttu-id="a9e68-108">For more information about Basic Load Balancer, see [Load Balancer overview](load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9e68-108">For more information about Basic Load Balancer, see [Load Balancer overview](load-balancer-overview.md).</span></span>

<span data-ttu-id="a9e68-109">The illustration shows the following configuration of the deployment example described in this article:</span><span class="sxs-lookup"><span data-stu-id="a9e68-109">The illustration shows the following configuration of the deployment example described in this article:</span></span>

- <span data-ttu-id="a9e68-110">The NVAs are deployed in the back-end pool of an internal load balancer behind the High Availability Ports configuration.</span><span class="sxs-lookup"><span data-stu-id="a9e68-110">The NVAs are deployed in the back-end pool of an internal load balancer behind the High Availability Ports configuration.</span></span> 
- <span data-ttu-id="a9e68-111">The user-defined route (UDR) applied on the DMZ subnet routes all traffic to the NVAs by making the next hop as the internal load balancer virtual IP.</span><span class="sxs-lookup"><span data-stu-id="a9e68-111">The user-defined route (UDR) applied on the DMZ subnet routes all traffic to the NVAs by making the next hop as the internal load balancer virtual IP.</span></span> 
- <span data-ttu-id="a9e68-112">The internal load balancer distributes the traffic to one of the active NVAs according to the load balancer algorithm.</span><span class="sxs-lookup"><span data-stu-id="a9e68-112">The internal load balancer distributes the traffic to one of the active NVAs according to the load balancer algorithm.</span></span>
- <span data-ttu-id="a9e68-113">The NVA processes the traffic and forwards it to the original destination in the back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="a9e68-113">The NVA processes the traffic and forwards it to the original destination in the back-end subnet.</span></span>
- <span data-ttu-id="a9e68-114">The return path can take the same route if a corresponding UDR is configured in the back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="a9e68-114">The return path can take the same route if a corresponding UDR is configured in the back-end subnet.</span></span> 

![High Availability Ports example deployment](./media/load-balancer-configure-ha-ports/haports.png)



## <a name="configure-high-availability-ports"></a><span data-ttu-id="a9e68-116">Configure High Availability Ports</span><span class="sxs-lookup"><span data-stu-id="a9e68-116">Configure High Availability Ports</span></span>

<span data-ttu-id="a9e68-117">To configure High Availability Ports, set up an internal load balancer with the NVAs in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="a9e68-117">To configure High Availability Ports, set up an internal load balancer with the NVAs in the back-end pool.</span></span> <span data-ttu-id="a9e68-118">Set up a corresponding load balancer health probe configuration to detect NVA health and the load balancer rule with High Availability Ports.</span><span class="sxs-lookup"><span data-stu-id="a9e68-118">Set up a corresponding load balancer health probe configuration to detect NVA health and the load balancer rule with High Availability Ports.</span></span> <span data-ttu-id="a9e68-119">The general load balancer-related configuration is covered in [Get started](load-balancer-get-started-ilb-arm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a9e68-119">The general load balancer-related configuration is covered in [Get started](load-balancer-get-started-ilb-arm-portal.md).</span></span> <span data-ttu-id="a9e68-120">This article highlights the High Availability Ports configuration.</span><span class="sxs-lookup"><span data-stu-id="a9e68-120">This article highlights the High Availability Ports configuration.</span></span>

<span data-ttu-id="a9e68-121">The configuration essentially involves setting the front-end port and the back-end port value to **0**.</span><span class="sxs-lookup"><span data-stu-id="a9e68-121">The configuration essentially involves setting the front-end port and the back-end port value to **0**.</span></span> <span data-ttu-id="a9e68-122">Set the protocol value to **All**.</span><span class="sxs-lookup"><span data-stu-id="a9e68-122">Set the protocol value to **All**.</span></span> <span data-ttu-id="a9e68-123">This article describes how to configure High Availability Ports by using the Azure portal, PowerShell, and Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a9e68-123">This article describes how to configure High Availability Ports by using the Azure portal, PowerShell, and Azure CLI 2.0.</span></span>

### <a name="configure-a-high-availability-ports-load-balancer-rule-with-the-azure-portal"></a><span data-ttu-id="a9e68-124">Configure a High Availability Ports load balancer rule with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a9e68-124">Configure a High Availability Ports load balancer rule with the Azure portal</span></span>

<span data-ttu-id="a9e68-125">To configure High Availability Ports by using the Azure portal, select the **HA Ports** check box.</span><span class="sxs-lookup"><span data-stu-id="a9e68-125">To configure High Availability Ports by using the Azure portal, select the **HA Ports** check box.</span></span> <span data-ttu-id="a9e68-126">When selected, the related port and protocol configuration is automatically populated.</span><span class="sxs-lookup"><span data-stu-id="a9e68-126">When selected, the related port and protocol configuration is automatically populated.</span></span> 

![High Availability Ports configuration via the Azure portal](./media/load-balancer-configure-ha-ports/haports-portal.png)


### <a name="configure-a-high-availability-ports-load-balancing-rule-via-the-resource-manager-template"></a><span data-ttu-id="a9e68-128">Configure a High Availability Ports load-balancing rule via the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="a9e68-128">Configure a High Availability Ports load-balancing rule via the Resource Manager template</span></span>

<span data-ttu-id="a9e68-129">You can configure High Availability Ports by using the 2017-08-01 API version for Microsoft.Network/loadBalancers in the Load Balancer resource.</span><span class="sxs-lookup"><span data-stu-id="a9e68-129">You can configure High Availability Ports by using the 2017-08-01 API version for Microsoft.Network/loadBalancers in the Load Balancer resource.</span></span> <span data-ttu-id="a9e68-130">The following JSON snippet illustrates the changes in the load balancer configuration for High Availability Ports via the REST API:</span><span class="sxs-lookup"><span data-stu-id="a9e68-130">The following JSON snippet illustrates the changes in the load balancer configuration for High Availability Ports via the REST API:</span></span>

```json
    {
        "apiVersion": "2017-08-01",
        "type": "Microsoft.Network/loadBalancers",
        ...
        "sku":
        {
            "name": "Standard"
        },
        ...
        "properties": {
            "frontendIpConfigurations": [...],
            "backendAddressPools": [...],
            "probes": [...],
            "loadBalancingRules": [
             {
                "properties": {
                    ...
                    "protocol": "All",
                    "frontendPort": 0,
                    "backendPort": 0
                }
             }
            ],
       ...
       }
    }
```

### <a name="configure-a-high-availability-ports-load-balancer-rule-with-powershell"></a><span data-ttu-id="a9e68-131">Configure a High Availability Ports load balancer rule with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9e68-131">Configure a High Availability Ports load balancer rule with PowerShell</span></span>

<span data-ttu-id="a9e68-132">Use the following command to create the High Availability Ports load balancer rule while you create the internal load balancer with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a9e68-132">Use the following command to create the High Availability Ports load balancer rule while you create the internal load balancer with PowerShell:</span></span>

```powershell
lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HAPortsRule" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol "All" -FrontendPort 0 -BackendPort 0
```

### <a name="configure-a-high-availability-ports-load-balancer-rule-with-azure-cli-20"></a><span data-ttu-id="a9e68-133">Configure a High Availability Ports load balancer rule with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a9e68-133">Configure a High Availability Ports load balancer rule with Azure CLI 2.0</span></span>

<span data-ttu-id="a9e68-134">In step 4 of [Create an internal load balancer set](load-balancer-get-started-ilb-arm-cli.md), use the following command to create the High Availability Ports load balancer rule:</span><span class="sxs-lookup"><span data-stu-id="a9e68-134">In step 4 of [Create an internal load balancer set](load-balancer-get-started-ilb-arm-cli.md), use the following command to create the High Availability Ports load balancer rule:</span></span>

```azurecli
azure network lb rule create --resource-group contoso-rg --lb-name contoso-ilb --name haportsrule --protocol all --frontend-port 0 --backend-port 0 --frontend-ip-name feilb --backend-address-pool-name beilb
```

## <a name="next-steps"></a><span data-ttu-id="a9e68-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9e68-135">Next steps</span></span>

<span data-ttu-id="a9e68-136">Learn more about [High Availability Ports](load-balancer-ha-ports-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9e68-136">Learn more about [High Availability Ports](load-balancer-ha-ports-overview.md).</span></span>
