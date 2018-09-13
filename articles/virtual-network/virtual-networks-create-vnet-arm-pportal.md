---
title: Create a virtual network - Azure portal | Microsoft Docs
description: Learn how to create a virtual network using the Azure portal.
services: virtual-network
documentationcenter: ''
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/8/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c13e02bf51226bf87efc1abf1165368620fcf40a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554470"
---
# <a name="create-a-virtual-network-using-the-azure-portal"></a><span data-ttu-id="8f3c1-103">Create a virtual network using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8f3c1-103">Create a virtual network using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="8f3c1-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="8f3c1-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="8f3c1-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="8f3c1-107">This article explains how to create a VNet through the Resource Manager deployment model using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-107">This article explains how to create a VNet through the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="8f3c1-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Template](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (Classic)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Classic)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Classic)](virtual-networks-create-vnet-classic-cli.md)


[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="8f3c1-116">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="8f3c1-116">Create a virtual network</span></span>

<span data-ttu-id="8f3c1-117">To create a virtual network using the Azure portal, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-117">To create a virtual network using the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="8f3c1-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="8f3c1-119">Click **New** > **Networking** > **Virtual network**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-119">Click **New** > **Networking** > **Virtual network**, as shown in the following picture:</span></span>

    ![New Virtual Network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-create-vnet-arm-pportal/1.png)

3. <span data-ttu-id="8f3c1-121">In the **Virtual network** blade that appears, ensure that *Resource Manager* is selected and click **Create**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-121">In the **Virtual network** blade that appears, ensure that *Resource Manager* is selected and click **Create**, as shown in the following picture:</span></span>

    ![Virtual Network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-create-vnet-arm-pportal/2.png)
    
4. <span data-ttu-id="8f3c1-123">In the **Create virtual network** blade that appeared, enter *TestVNet* for **Name**, *192.168.0.0/16* for **Address space**, *FrontEnd* for **Subnet name** *192.168.1.0/24* for **Subnet address range**, *TestRG* for **Resource group**, select your **Subscription**, a **Location** and click the **Create** button, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-123">In the **Create virtual network** blade that appeared, enter *TestVNet* for **Name**, *192.168.0.0/16* for **Address space**, *FrontEnd* for **Subnet name** *192.168.1.0/24* for **Subnet address range**, *TestRG* for **Resource group**, select your **Subscription**, a **Location** and click the **Create** button, as shown in the following picture:</span></span>

    ![Create virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-create-vnet-arm-pportal/3.png)

    <span data-ttu-id="8f3c1-125">Alternatively, you can select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-125">Alternatively, you can select an existing resource group.</span></span> <span data-ttu-id="8f3c1-126">To learn more about resource groups, read the [Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups) article.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-126">To learn more about resource groups, read the [Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups) article.</span></span> <span data-ttu-id="8f3c1-127">You can also select a different location.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-127">You can also select a different location.</span></span> <span data-ttu-id="8f3c1-128">To learn more about Azure locations and regions, read the [Azure regions](https://azure.microsoft.com/regions) article.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-128">To learn more about Azure locations and regions, read the [Azure regions](https://azure.microsoft.com/regions) article.</span></span>

5. <span data-ttu-id="8f3c1-129">The portal only enables you to create one subnet when creating a VNet.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-129">The portal only enables you to create one subnet when creating a VNet.</span></span> <span data-ttu-id="8f3c1-130">For this scenario, a second subnet must be created after the VNet is created.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-130">For this scenario, a second subnet must be created after the VNet is created.</span></span> <span data-ttu-id="8f3c1-131">To create the second subnet, click **All resources**, then click **TestVNet** in the **All resources** blade, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-131">To create the second subnet, click **All resources**, then click **TestVNet** in the **All resources** blade, as shown in the following picture:</span></span>

    ![Created VNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-create-vnet-arm-pportal/4.png)

6. <span data-ttu-id="8f3c1-133">In the **TestVNet** blade that appears, click **Subnet**, then click **+Subnet**, enter *BackEnd* for **Name**, *192.168.2.0/24* for **Address range** in the **Add subnet** blade, then click **OK**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-133">In the **TestVNet** blade that appears, click **Subnet**, then click **+Subnet**, enter *BackEnd* for **Name**, *192.168.2.0/24* for **Address range** in the **Add subnet** blade, then click **OK**, as shown in the following picture:</span></span>

    ![Add subnet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-create-vnet-arm-pportal/5.png)

7. <span data-ttu-id="8f3c1-135">The two subnets are listed, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-135">The two subnets are listed, as shown in the following picture:</span></span>
    
    ![List of subnets in VNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-create-vnet-arm-pportal/6.png)

<span data-ttu-id="8f3c1-137">This article explained how to create a virtual network with two subnets for testing.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-137">This article explained how to create a virtual network with two subnets for testing.</span></span> <span data-ttu-id="8f3c1-138">Before creating a virtual network for production use, we recommend reading the [Virtual network overview](virtual-networks-overview.md) and [Virtual network plan and design](virtual-network-vnet-plan-design-arm.md) articles to fully understand virtual networks and all settings.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-138">Before creating a virtual network for production use, we recommend reading the [Virtual network overview](virtual-networks-overview.md) and [Virtual network plan and design](virtual-network-vnet-plan-design-arm.md) articles to fully understand virtual networks and all settings.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8f3c1-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f3c1-139">Next steps</span></span>

<span data-ttu-id="8f3c1-140">Learn how to connect:</span><span class="sxs-lookup"><span data-stu-id="8f3c1-140">Learn how to connect:</span></span>

- <span data-ttu-id="8f3c1-141">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-141">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="8f3c1-142">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-142">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="8f3c1-143">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-143">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="8f3c1-144">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-144">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="8f3c1-145">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md) articles.</span><span class="sxs-lookup"><span data-stu-id="8f3c1-145">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md) articles.</span></span>





