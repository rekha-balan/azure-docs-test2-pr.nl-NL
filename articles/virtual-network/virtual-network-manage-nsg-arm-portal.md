---
title: Manage NSGs using the Azure portal | Microsoft Docs
description: Learn how to manage existing NSGs using the Azure portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: 3ee09f1eaaec2d913c58f2c4f33bd567e5d56393
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661758"
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="efa32-103">Manage NSGs using the portal</span><span class="sxs-lookup"><span data-stu-id="efa32-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Azure CLI](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md). This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="efa32-109">Retrieve Information</span><span class="sxs-lookup"><span data-stu-id="efa32-109">Retrieve Information</span></span>
<span data-ttu-id="efa32-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span><span class="sxs-lookup"><span data-stu-id="efa32-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="efa32-111">View existing NSGs</span><span class="sxs-lookup"><span data-stu-id="efa32-111">View existing NSGs</span></span>

<span data-ttu-id="efa32-112">To view all existing NSGs in a subscription, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="efa32-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="efa32-114">Click **Browse >** > **Network security groups**.</span><span class="sxs-lookup"><span data-stu-id="efa32-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="efa32-116">Check the list of NSGs in the **Network security groups** blade.</span><span class="sxs-lookup"><span data-stu-id="efa32-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="efa32-118">View NSGs in a resource group</span><span class="sxs-lookup"><span data-stu-id="efa32-118">View NSGs in a resource group</span></span>

<span data-ttu-id="efa32-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-120">Click **Resource groups >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="efa32-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="efa32-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span><span class="sxs-lookup"><span data-stu-id="efa32-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="efa32-124">List all rules for an NSG</span><span class="sxs-lookup"><span data-stu-id="efa32-124">List all rules for an NSG</span></span>

<span data-ttu-id="efa32-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="efa32-127">In the **Settings** tab, click **Inbound security rules**.</span><span class="sxs-lookup"><span data-stu-id="efa32-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="efa32-129">The **Inbound security rules** blade is displayed as shown below.</span><span class="sxs-lookup"><span data-stu-id="efa32-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="efa32-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span><span class="sxs-lookup"><span data-stu-id="efa32-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="efa32-133">View NSGs associations</span><span class="sxs-lookup"><span data-stu-id="efa32-133">View NSGs associations</span></span>

<span data-ttu-id="efa32-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="efa32-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span><span class="sxs-lookup"><span data-stu-id="efa32-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="efa32-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span><span class="sxs-lookup"><span data-stu-id="efa32-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="efa32-139">Manage rules</span><span class="sxs-lookup"><span data-stu-id="efa32-139">Manage rules</span></span>
<span data-ttu-id="efa32-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span><span class="sxs-lookup"><span data-stu-id="efa32-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="efa32-141">Add a rule</span><span class="sxs-lookup"><span data-stu-id="efa32-141">Add a rule</span></span>
<span data-ttu-id="efa32-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="efa32-144">In the **Settings** tab, click **Inbound security rules**.</span><span class="sxs-lookup"><span data-stu-id="efa32-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="efa32-145">In the **Inbound security rules** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="efa32-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="efa32-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="efa32-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="efa32-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span><span class="sxs-lookup"><span data-stu-id="efa32-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="efa32-150">Change a rule</span><span class="sxs-lookup"><span data-stu-id="efa32-150">Change a rule</span></span>
<span data-ttu-id="efa32-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="efa32-153">In the **Settings** tab, click the rule created above.</span><span class="sxs-lookup"><span data-stu-id="efa32-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="efa32-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="efa32-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="efa32-156">Delete a rule</span><span class="sxs-lookup"><span data-stu-id="efa32-156">Delete a rule</span></span>

<span data-ttu-id="efa32-157">To delete the rule created above, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="efa32-159">In the **Settings** tab, click the rule created above.</span><span class="sxs-lookup"><span data-stu-id="efa32-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="efa32-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="efa32-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="efa32-162">Manage associations</span><span class="sxs-lookup"><span data-stu-id="efa32-162">Manage associations</span></span>
<span data-ttu-id="efa32-163">You can associate an NSG to subnets and NICs.</span><span class="sxs-lookup"><span data-stu-id="efa32-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="efa32-164">You can also dissociate an NSG from any resource it's associated to.</span><span class="sxs-lookup"><span data-stu-id="efa32-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="efa32-165">Associate an NSG to a NIC</span><span class="sxs-lookup"><span data-stu-id="efa32-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="efa32-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="efa32-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="efa32-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="efa32-170">Dissociate an NSG from a NIC</span><span class="sxs-lookup"><span data-stu-id="efa32-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="efa32-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="efa32-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="efa32-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span><span class="sxs-lookup"><span data-stu-id="efa32-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> You can also use this blade to associate the NIC to any existing NSG.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="efa32-176">Dissociate an NSG from a subnet</span><span class="sxs-lookup"><span data-stu-id="efa32-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="efa32-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="efa32-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="efa32-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span><span class="sxs-lookup"><span data-stu-id="efa32-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="efa32-181">In the **FrontEnd** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="efa32-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="efa32-183">Associate an NSG to a subnet</span><span class="sxs-lookup"><span data-stu-id="efa32-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="efa32-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="efa32-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="efa32-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="efa32-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="efa32-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="efa32-187">In the **FrontEnd** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="efa32-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> You can also associate an NSG to a subnet from thh NSG's **Settings** blade.
>

## <a name="delete-an-nsg"></a><span data-ttu-id="efa32-189">Delete an NSG</span><span class="sxs-lookup"><span data-stu-id="efa32-189">Delete an NSG</span></span>
<span data-ttu-id="efa32-190">You can only delete an NSG if it's not associated to any resource.</span><span class="sxs-lookup"><span data-stu-id="efa32-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="efa32-191">To delete an NSG, complete the following steps:.</span><span class="sxs-lookup"><span data-stu-id="efa32-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="efa32-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="efa32-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="efa32-193">In the **Settings** blade, click **Network interfaces**.</span><span class="sxs-lookup"><span data-stu-id="efa32-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="efa32-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="efa32-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="efa32-195">Repeat step 3 for each NIC.</span><span class="sxs-lookup"><span data-stu-id="efa32-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="efa32-196">In the **Settings** blade, click **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="efa32-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="efa32-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="efa32-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="efa32-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span><span class="sxs-lookup"><span data-stu-id="efa32-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="efa32-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="efa32-200">Next steps</span></span>
* <span data-ttu-id="efa32-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span><span class="sxs-lookup"><span data-stu-id="efa32-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
















