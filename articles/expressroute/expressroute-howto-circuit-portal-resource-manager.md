---
title: 'Create and modify an ExpressRoute circuit: Azure portal | Microsoft Docs'
description: This article describes how to create, provision, verify, update, delete, and deprovision an ExpressRoute circuit.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 450fa0ec9198d2486a30e184848294d1931d6fb6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551671"
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="528c8-103">Create and modify an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-circuit-arm.md)
> * [Video - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> 
>

<span data-ttu-id="528c8-107">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="528c8-107">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="528c8-108">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span><span class="sxs-lookup"><span data-stu-id="528c8-108">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

<span data-ttu-id="528c8-109">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="528c8-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="528c8-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="528c8-110">Before you begin</span></span>
* <span data-ttu-id="528c8-111">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="528c8-111">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="528c8-112">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="528c8-112">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="528c8-113">Ensure that you have permissions to create new networking resources.</span><span class="sxs-lookup"><span data-stu-id="528c8-113">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="528c8-114">Contact your account administrator if you do not have the right permissions.</span><span class="sxs-lookup"><span data-stu-id="528c8-114">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="528c8-115">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span><span class="sxs-lookup"><span data-stu-id="528c8-115">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="528c8-116">Create and provision an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-116">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="528c8-117">1. Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="528c8-117">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="528c8-118">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="528c8-118">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="528c8-119">2. Create a new ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-119">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> Your ExpressRoute circuit will be billed from the moment a service key is issued. Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.
> 
> 

1. <span data-ttu-id="528c8-122">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span><span class="sxs-lookup"><span data-stu-id="528c8-122">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="528c8-123">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="528c8-123">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Create an ExpressRoute circuit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="528c8-125">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span><span class="sxs-lookup"><span data-stu-id="528c8-125">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="528c8-126">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span><span class="sxs-lookup"><span data-stu-id="528c8-126">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="528c8-127">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span><span class="sxs-lookup"><span data-stu-id="528c8-127">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="528c8-128">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="528c8-128">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="528c8-129">**Data metering** determines the billing type.</span><span class="sxs-lookup"><span data-stu-id="528c8-129">**Data metering** determines the billing type.</span></span> <span data-ttu-id="528c8-130">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span><span class="sxs-lookup"><span data-stu-id="528c8-130">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="528c8-131">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span><span class="sxs-lookup"><span data-stu-id="528c8-131">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Configure the SKU tier and data metering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft. This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located. While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit. 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="528c8-136">3. View the circuits and properties</span><span class="sxs-lookup"><span data-stu-id="528c8-136">3. View the circuits and properties</span></span>
<span data-ttu-id="528c8-137">**View all the circuits**</span><span class="sxs-lookup"><span data-stu-id="528c8-137">**View all the circuits**</span></span>

<span data-ttu-id="528c8-138">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span><span class="sxs-lookup"><span data-stu-id="528c8-138">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![View circuits](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="528c8-140">**View the properties**</span><span class="sxs-lookup"><span data-stu-id="528c8-140">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![View properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="528c8-142">4. Send the service key to your connectivity provider for provisioning</span><span class="sxs-lookup"><span data-stu-id="528c8-142">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="528c8-143">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span><span class="sxs-lookup"><span data-stu-id="528c8-143">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="528c8-144">**Circuit status** provides the state on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="528c8-144">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="528c8-145">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span><span class="sxs-lookup"><span data-stu-id="528c8-145">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="528c8-146">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span><span class="sxs-lookup"><span data-stu-id="528c8-146">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="528c8-147">Provider status: Not provisioned</span><span class="sxs-lookup"><span data-stu-id="528c8-147">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="528c8-148">Circuit status: Enabled</span><span class="sxs-lookup"><span data-stu-id="528c8-148">Circuit status: Enabled</span></span>

![Initiate provisioning process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="528c8-150">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span><span class="sxs-lookup"><span data-stu-id="528c8-150">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="528c8-151">Provider status: Provisioning</span><span class="sxs-lookup"><span data-stu-id="528c8-151">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="528c8-152">Circuit status: Enabled</span><span class="sxs-lookup"><span data-stu-id="528c8-152">Circuit status: Enabled</span></span>

<span data-ttu-id="528c8-153">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span><span class="sxs-lookup"><span data-stu-id="528c8-153">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="528c8-154">Provider status: Provisioned</span><span class="sxs-lookup"><span data-stu-id="528c8-154">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="528c8-155">Circuit status: Enabled</span><span class="sxs-lookup"><span data-stu-id="528c8-155">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="528c8-156">5. Periodically check the status and the state of the circuit key</span><span class="sxs-lookup"><span data-stu-id="528c8-156">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="528c8-157">You can view the properties of the circuit that you're interested in by selecting it.</span><span class="sxs-lookup"><span data-stu-id="528c8-157">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="528c8-158">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span><span class="sxs-lookup"><span data-stu-id="528c8-158">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Circuit and provider status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="528c8-160">6. Create your routing configuration</span><span class="sxs-lookup"><span data-stu-id="528c8-160">6. Create your routing configuration</span></span>
<span data-ttu-id="528c8-161">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span><span class="sxs-lookup"><span data-stu-id="528c8-161">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services. If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="528c8-164">7. Link a virtual network to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-164">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="528c8-165">Next, link a virtual network to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="528c8-165">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="528c8-166">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="528c8-166">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="528c8-167">Getting the status of an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-167">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="528c8-168">You can view the status of a circuit by selecting it.</span><span class="sxs-lookup"><span data-stu-id="528c8-168">You can view the status of a circuit by selecting it.</span></span> 

![Status of an ExpressRoute circuit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="528c8-170">Modifying an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-170">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="528c8-171">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span><span class="sxs-lookup"><span data-stu-id="528c8-171">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="528c8-172">You can do the following with no downtime:</span><span class="sxs-lookup"><span data-stu-id="528c8-172">You can do the following with no downtime:</span></span>

* <span data-ttu-id="528c8-173">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="528c8-173">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="528c8-174">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span><span class="sxs-lookup"><span data-stu-id="528c8-174">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="528c8-175">Note that downgrading the bandwidth of a circuit is not supported.</span><span class="sxs-lookup"><span data-stu-id="528c8-175">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="528c8-176">Change the metering plan from Metered Data to Unlimited Data.</span><span class="sxs-lookup"><span data-stu-id="528c8-176">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="528c8-177">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span><span class="sxs-lookup"><span data-stu-id="528c8-177">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="528c8-178">You can enable and disable *Allow Classic Operations*.</span><span class="sxs-lookup"><span data-stu-id="528c8-178">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="528c8-179">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="528c8-179">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="528c8-180">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="528c8-180">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Modify circuit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="528c8-182">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span><span class="sxs-lookup"><span data-stu-id="528c8-182">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port. You cannot upgrade the circuit if there is no additional capacity available at that location.
>
> You cannot reduce the bandwidth of an ExpressRoute circuit without disruption. Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.
> 
> Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="528c8-188">Deprovisioning and deleting an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-188">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="528c8-189">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span><span class="sxs-lookup"><span data-stu-id="528c8-189">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="528c8-190">Note the following:</span><span class="sxs-lookup"><span data-stu-id="528c8-190">Note the following:</span></span>

* <span data-ttu-id="528c8-191">You must unlink all virtual networks from the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="528c8-191">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="528c8-192">If this operation fails, check whether any virtual networks are linked to the circuit.</span><span class="sxs-lookup"><span data-stu-id="528c8-192">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="528c8-193">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span><span class="sxs-lookup"><span data-stu-id="528c8-193">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="528c8-194">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span><span class="sxs-lookup"><span data-stu-id="528c8-194">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="528c8-195">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="528c8-195">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="528c8-196">This will stop billing for the circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-196">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="528c8-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="528c8-197">Next steps</span></span>
<span data-ttu-id="528c8-198">After you create your circuit, make sure that you do the following:</span><span class="sxs-lookup"><span data-stu-id="528c8-198">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="528c8-199">Create and modify routing for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-199">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="528c8-200">Link your virtual network to your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="528c8-200">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)









