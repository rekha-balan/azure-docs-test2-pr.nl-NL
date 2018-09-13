---
title: Create a virtual network using the Azure CLI 1.0 | Microsoft Docs
description: Learn how to create a virtual network using the Azure CLI 1.0 | Resource Manager.
services: virtual-network
documentationcenter: ''
author: jimdial
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556026"
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="a2b76-103">Create a virtual network using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a2b76-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="a2b76-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="a2b76-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a2b76-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a2b76-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="a2b76-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="a2b76-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a2b76-107">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="a2b76-107">CLI versions to complete the task</span></span>
<span data-ttu-id="a2b76-108">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="a2b76-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a2b76-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="a2b76-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="a2b76-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="a2b76-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="a2b76-111">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="a2b76-111">Create a virtual network</span></span>

<span data-ttu-id="a2b76-112">To create a virtual network using the Azure CLI, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="a2b76-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="a2b76-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span><span class="sxs-lookup"><span data-stu-id="a2b76-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="a2b76-114">Create a VNet and a subnet:</span><span class="sxs-lookup"><span data-stu-id="a2b76-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="a2b76-115">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a2b76-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="a2b76-116">Parameters used:</span><span class="sxs-lookup"><span data-stu-id="a2b76-116">Parameters used:</span></span>

   * <span data-ttu-id="a2b76-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-117">**--vnet**.</span></span> <span data-ttu-id="a2b76-118">Name of the VNet to be created.</span><span class="sxs-lookup"><span data-stu-id="a2b76-118">Name of the VNet to be created.</span></span> <span data-ttu-id="a2b76-119">For our scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="a2b76-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="a2b76-120">**-e (or --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="a2b76-121">VNet address space.</span><span class="sxs-lookup"><span data-stu-id="a2b76-121">VNet address space.</span></span> <span data-ttu-id="a2b76-122">For our scenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="a2b76-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="a2b76-123">**-i (or -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="a2b76-124">Network mask in CIDR format.</span><span class="sxs-lookup"><span data-stu-id="a2b76-124">Network mask in CIDR format.</span></span> <span data-ttu-id="a2b76-125">For our scenario, *16*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="a2b76-126">**-n (or --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="a2b76-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="a2b76-127">Name of the first subnet.</span><span class="sxs-lookup"><span data-stu-id="a2b76-127">Name of the first subnet.</span></span> <span data-ttu-id="a2b76-128">For our scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="a2b76-129">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="a2b76-130">Starting IP address for subnet, or subnet address space.</span><span class="sxs-lookup"><span data-stu-id="a2b76-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="a2b76-131">For our scenario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="a2b76-132">**-r (or --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="a2b76-133">Network mask in CIDR format for subnet.</span><span class="sxs-lookup"><span data-stu-id="a2b76-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="a2b76-134">For our scenario, *24*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="a2b76-135">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-135">**-l (or --location)**.</span></span> <span data-ttu-id="a2b76-136">Azure region where the VNet is created.</span><span class="sxs-lookup"><span data-stu-id="a2b76-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="a2b76-137">For our scenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="a2b76-138">Create a subnet:</span><span class="sxs-lookup"><span data-stu-id="a2b76-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="a2b76-139">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a2b76-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="a2b76-140">Parameters used:</span><span class="sxs-lookup"><span data-stu-id="a2b76-140">Parameters used:</span></span>

   * <span data-ttu-id="a2b76-141">**-t (or --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="a2b76-142">Name of the VNet where the subnet will be created.</span><span class="sxs-lookup"><span data-stu-id="a2b76-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="a2b76-143">For our scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="a2b76-144">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-144">**-n (or --name)**.</span></span> <span data-ttu-id="a2b76-145">Name of the new subnet.</span><span class="sxs-lookup"><span data-stu-id="a2b76-145">Name of the new subnet.</span></span> <span data-ttu-id="a2b76-146">For our scenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="a2b76-147">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="a2b76-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="a2b76-148">Subnet CIDR block.</span><span class="sxs-lookup"><span data-stu-id="a2b76-148">Subnet CIDR block.</span></span> <span data-ttu-id="a2b76-149">Four our scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a2b76-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="a2b76-150">To view the properties of the new VNet:</span><span class="sxs-lookup"><span data-stu-id="a2b76-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="a2b76-151">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a2b76-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="a2b76-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2b76-152">Next steps</span></span>

<span data-ttu-id="a2b76-153">Learn how to connect:</span><span class="sxs-lookup"><span data-stu-id="a2b76-153">Learn how to connect:</span></span>

- <span data-ttu-id="a2b76-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span><span class="sxs-lookup"><span data-stu-id="a2b76-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="a2b76-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span><span class="sxs-lookup"><span data-stu-id="a2b76-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="a2b76-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="a2b76-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="a2b76-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="a2b76-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="a2b76-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a2b76-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>