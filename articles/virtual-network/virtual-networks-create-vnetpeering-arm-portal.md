---
title: Azure Virtual Network peering - Portal | Microsoft Docs
description: Learn how to create a virtual network peering using the Azure portal.
services: virtual-network
documentationcenter: ''
author: NarayanAnnamalai
manager: jefco
editor: ''
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: narayan;annahar
ms.openlocfilehash: 39b2827b29d2525374d2f92df34f61313474605f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551871"
---
# <a name="create-a-virtual-network-peering-using-the-azure-portal"></a><span data-ttu-id="7749a-103">Create a virtual network peering using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7749a-103">Create a virtual network peering using the Azure portal</span></span>
[!INCLUDE [virtual-networks-create-vnet-selectors-arm-include](../../includes/virtual-networks-create-vnetpeering-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnetpeering-intro-include.md)]

[!INCLUDE [virtual-networks-create-vnet-scenario-basic-include](../../includes/virtual-networks-create-vnetpeering-scenario-basic-include.md)]

<span data-ttu-id="7749a-104">To create a VNet peering based on the scenario by using the Azure portal, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="7749a-104">To create a VNet peering based on the scenario by using the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="7749a-105">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="7749a-105">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7749a-106">To establish a VNet peering, you need to create two links, one for each direction, between two VNets.</span><span class="sxs-lookup"><span data-stu-id="7749a-106">To establish a VNet peering, you need to create two links, one for each direction, between two VNets.</span></span> <span data-ttu-id="7749a-107">You can create VNet peering link for VNet1 to VNet2 first.</span><span class="sxs-lookup"><span data-stu-id="7749a-107">You can create VNet peering link for VNet1 to VNet2 first.</span></span> <span data-ttu-id="7749a-108">In the Azure portal, click **Browse** > **choose Virtual networks**</span><span class="sxs-lookup"><span data-stu-id="7749a-108">In the Azure portal, click **Browse** > **choose Virtual networks**</span></span>

    ![Create VNet peering in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure01.png)
3. <span data-ttu-id="7749a-110">In the **Virtual networks** blade, choose *VNET1*, click **Peerings**, then click **Add**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7749a-110">In the **Virtual networks** blade, choose *VNET1*, click **Peerings**, then click **Add**, as shown in the following picture:</span></span>

    ![Choose peering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure02.png)
4. <span data-ttu-id="7749a-112">In the **Add Peering** blade, enter *LinkToVnet2* for **Name**, choose a subscription, and the peer **Virtual network** *VNET2*, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7749a-112">In the **Add Peering** blade, enter *LinkToVnet2* for **Name**, choose a subscription, and the peer **Virtual network** *VNET2*, then click **OK**.</span></span>

    ![Link to VNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure03.png)
5. <span data-ttu-id="7749a-114">Once the VNet peering link is created, you'll see the link state, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7749a-114">Once the VNet peering link is created, you'll see the link state, as shown in the following picture:</span></span>

    ![Link State](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure04.png)
6. <span data-ttu-id="7749a-116">Create the VNet peering link for VNET2 to VNET1.</span><span class="sxs-lookup"><span data-stu-id="7749a-116">Create the VNet peering link for VNET2 to VNET1.</span></span> <span data-ttu-id="7749a-117">In the **Virtual Networks** blade, choose *VNET2*, click **Peerings**, then click **Add**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7749a-117">In the **Virtual Networks** blade, choose *VNET2*, click **Peerings**, then click **Add**, as shown in the following picture:</span></span>

    ![Peer from other VNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure05.png)
7. <span data-ttu-id="7749a-119">In the **Add peering** blade, enter *LinkToVnet1* for **Name**, choose the subscription, select *VNET1* for **Virtual network**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7749a-119">In the **Add peering** blade, enter *LinkToVnet1* for **Name**, choose the subscription, select *VNET1* for **Virtual network**, then click **OK**.</span></span>

    ![Creating virtual network tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure06.png)
8. <span data-ttu-id="7749a-121">Once the VNet peering link is created, you'll see the link state, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7749a-121">Once the VNet peering link is created, you'll see the link state, as shown in the following picture:</span></span>

    ![Final link state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure07.png)
9. <span data-ttu-id="7749a-123">Check the state for **LinkToVnet2** and it now changes to *Connected* as well.</span><span class="sxs-lookup"><span data-stu-id="7749a-123">Check the state for **LinkToVnet2** and it now changes to *Connected* as well.</span></span>  
    
    ![Final link state 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure08.png)

    > [!NOTE]
    > <span data-ttu-id="7749a-125">VNET peering is only established if both links are connected.</span><span class="sxs-lookup"><span data-stu-id="7749a-125">VNET peering is only established if both links are connected.</span></span>
    > 
    > 

<span data-ttu-id="7749a-126">There are a few configurable properties for each link:</span><span class="sxs-lookup"><span data-stu-id="7749a-126">There are a few configurable properties for each link:</span></span>

| <span data-ttu-id="7749a-127">Option</span><span class="sxs-lookup"><span data-stu-id="7749a-127">Option</span></span> | <span data-ttu-id="7749a-128">Description</span><span class="sxs-lookup"><span data-stu-id="7749a-128">Description</span></span> | <span data-ttu-id="7749a-129">Default</span><span class="sxs-lookup"><span data-stu-id="7749a-129">Default</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7749a-130">AllowVirtualNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="7749a-130">AllowVirtualNetworkAccess</span></span> |<span data-ttu-id="7749a-131">Whether address space of Peer VNet to be included as part of the Virtual_network Tag</span><span class="sxs-lookup"><span data-stu-id="7749a-131">Whether address space of Peer VNet to be included as part of the Virtual_network Tag</span></span> |<span data-ttu-id="7749a-132">Yes</span><span class="sxs-lookup"><span data-stu-id="7749a-132">Yes</span></span> |
| <span data-ttu-id="7749a-133">AllowForwardedTraffic</span><span class="sxs-lookup"><span data-stu-id="7749a-133">AllowForwardedTraffic</span></span> |<span data-ttu-id="7749a-134">Whether traffic not originating from a peered VNet is accepted or dropped</span><span class="sxs-lookup"><span data-stu-id="7749a-134">Whether traffic not originating from a peered VNet is accepted or dropped</span></span> |<span data-ttu-id="7749a-135">No</span><span class="sxs-lookup"><span data-stu-id="7749a-135">No</span></span> |
| <span data-ttu-id="7749a-136">AllowGatewayTransit</span><span class="sxs-lookup"><span data-stu-id="7749a-136">AllowGatewayTransit</span></span> |<span data-ttu-id="7749a-137">Allows the peer VNet to use your VNet gateway</span><span class="sxs-lookup"><span data-stu-id="7749a-137">Allows the peer VNet to use your VNet gateway</span></span> |<span data-ttu-id="7749a-138">No</span><span class="sxs-lookup"><span data-stu-id="7749a-138">No</span></span> |
| <span data-ttu-id="7749a-139">UseRemoteGateways</span><span class="sxs-lookup"><span data-stu-id="7749a-139">UseRemoteGateways</span></span> |<span data-ttu-id="7749a-140">Use your peer’s VNet gateway.</span><span class="sxs-lookup"><span data-stu-id="7749a-140">Use your peer’s VNet gateway.</span></span> <span data-ttu-id="7749a-141">The peer VNet must have a gateway configured with AllowGatewayTransit selected.</span><span class="sxs-lookup"><span data-stu-id="7749a-141">The peer VNet must have a gateway configured with AllowGatewayTransit selected.</span></span> <span data-ttu-id="7749a-142">You cannot use this option if you have a gateway configured.</span><span class="sxs-lookup"><span data-stu-id="7749a-142">You cannot use this option if you have a gateway configured.</span></span> |<span data-ttu-id="7749a-143">No</span><span class="sxs-lookup"><span data-stu-id="7749a-143">No</span></span> |

<span data-ttu-id="7749a-144">Each link in a VNet peering has the previous set of properties.</span><span class="sxs-lookup"><span data-stu-id="7749a-144">Each link in a VNet peering has the previous set of properties.</span></span> <span data-ttu-id="7749a-145">From the portal, you can click the **VNet Peering** link and change any available options, click **Save** to apply changes.</span><span class="sxs-lookup"><span data-stu-id="7749a-145">From the portal, you can click the **VNet Peering** link and change any available options, click **Save** to apply changes.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-crosssub-include](../../includes/virtual-networks-create-vnetpeering-scenario-crosssub-include.md)]

1. <span data-ttu-id="7749a-146">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="7749a-146">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7749a-147">In this example, UserA has administrative permissions to SubscriptionA, and UserB has administrative permissions to SubscriptionB.</span><span class="sxs-lookup"><span data-stu-id="7749a-147">In this example, UserA has administrative permissions to SubscriptionA, and UserB has administrative permissions to SubscriptionB.</span></span> <span data-ttu-id="7749a-148">Both subscriptions are associated to the same Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="7749a-148">Both subscriptions are associated to the same Azure Active Directory tenant.</span></span> <span data-ttu-id="7749a-149">You cannot create a peering between subscriptions associated to different Azure Active Directory tenants.</span><span class="sxs-lookup"><span data-stu-id="7749a-149">You cannot create a peering between subscriptions associated to different Azure Active Directory tenants.</span></span>
3. <span data-ttu-id="7749a-150">In the portal, click **Browse**, choose **Virtual networks**.</span><span class="sxs-lookup"><span data-stu-id="7749a-150">In the portal, click **Browse**, choose **Virtual networks**.</span></span> <span data-ttu-id="7749a-151">Click the VNet you want to setup peering for.</span><span class="sxs-lookup"><span data-stu-id="7749a-151">Click the VNet you want to setup peering for.</span></span>
4. <span data-ttu-id="7749a-152">In the blade for the VNet you selected, click **Access control**, then click **Add**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7749a-152">In the blade for the VNet you selected, click **Access control**, then click **Add**, as shown in the following picture:</span></span>

    ![Scenario 2 Browse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure09.png)
4. <span data-ttu-id="7749a-154">On the **Add access** blade, click a role and choose **Network Contributor**, click **Add users**, type the UserB sign in name, and click OK.</span><span class="sxs-lookup"><span data-stu-id="7749a-154">On the **Add access** blade, click a role and choose **Network Contributor**, click **Add users**, type the UserB sign in name, and click OK.</span></span>

    ![RBAC](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure10.png)

5. <span data-ttu-id="7749a-156">Login to the Azure portal as UserB, who is the privileged user for SubscriptionB.</span><span class="sxs-lookup"><span data-stu-id="7749a-156">Login to the Azure portal as UserB, who is the privileged user for SubscriptionB.</span></span> <span data-ttu-id="7749a-157">Follow the previous steps to add UserA to the Network Contributor role, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7749a-157">Follow the previous steps to add UserA to the Network Contributor role, as shown in the following picture:</span></span>

    ![RBAC2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure11.png)

    > [!NOTE]
    > <span data-ttu-id="7749a-159">You can log off and log on both user sessions in the browser to ensure the authorization is enabled successfully.</span><span class="sxs-lookup"><span data-stu-id="7749a-159">You can log off and log on both user sessions in the browser to ensure the authorization is enabled successfully.</span></span>
    >
    >

    > [!IMPORTANT]
    > <span data-ttu-id="7749a-160">If the peering you're creating is between two VNets created through the Azure Resource Manager deployment model, continue with the remaining steps in this section.</span><span class="sxs-lookup"><span data-stu-id="7749a-160">If the peering you're creating is between two VNets created through the Azure Resource Manager deployment model, continue with the remaining steps in this section.</span></span> <span data-ttu-id="7749a-161">If the two VNets were created through different deployment models, skip the remaining steps of this section and complete the steps in the [Peering virtual networks created through different deployment models](#x-model) section of this article.</span><span class="sxs-lookup"><span data-stu-id="7749a-161">If the two VNets were created through different deployment models, skip the remaining steps of this section and complete the steps in the [Peering virtual networks created through different deployment models](#x-model) section of this article.</span></span>

6. <span data-ttu-id="7749a-162">Login to the portal as UserA, navigate to the VNET3 blade, click **Peering**, check the **I Know my resource ID** checkbox and type the resource ID for VNET5 in the format shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7749a-162">Login to the portal as UserA, navigate to the VNET3 blade, click **Peering**, check the **I Know my resource ID** checkbox and type the resource ID for VNET5 in the format shown in the following example:</span></span>
   
    <span data-ttu-id="7749a-163">/subscriptions/{SubscriptionID}/resourceGroups/{ResourceGroupName}/providers/Microsoft.Network/virtualNetworks/{VNETname}</span><span class="sxs-lookup"><span data-stu-id="7749a-163">/subscriptions/{SubscriptionID}/resourceGroups/{ResourceGroupName}/providers/Microsoft.Network/virtualNetworks/{VNETname}</span></span>
   
    ![Resource ID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure12.png)
7. <span data-ttu-id="7749a-165">Login to the portal as UserB and follow the previous steps to create a peering link from VNET5 to VNet3.</span><span class="sxs-lookup"><span data-stu-id="7749a-165">Login to the portal as UserB and follow the previous steps to create a peering link from VNET5 to VNet3.</span></span>
   
    ![Resource ID 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure13.png)
8. <span data-ttu-id="7749a-167">Peering will be established.</span><span class="sxs-lookup"><span data-stu-id="7749a-167">Peering will be established.</span></span> <span data-ttu-id="7749a-168">Any VM connected to VNet3 should be able to communicate with any VM connected to VNet5.</span><span class="sxs-lookup"><span data-stu-id="7749a-168">Any VM connected to VNet3 should be able to communicate with any VM connected to VNet5.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-transit-include](../../includes/virtual-networks-create-vnetpeering-scenario-transit-include.md)]

1. <span data-ttu-id="7749a-169">As a first step, VNET peering links from HubVnet to VNET1.</span><span class="sxs-lookup"><span data-stu-id="7749a-169">As a first step, VNET peering links from HubVnet to VNET1.</span></span> <span data-ttu-id="7749a-170">Note that Allow Forwarded Traffic option is not selected for the link.</span><span class="sxs-lookup"><span data-stu-id="7749a-170">Note that Allow Forwarded Traffic option is not selected for the link.</span></span>
   
    ![Basic Peering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure14.png)
2. <span data-ttu-id="7749a-172">As a next step, peering links from VNET1 to HubVnet can be created.</span><span class="sxs-lookup"><span data-stu-id="7749a-172">As a next step, peering links from VNET1 to HubVnet can be created.</span></span> <span data-ttu-id="7749a-173">Note that Allow forwarded traffic option is selected.</span><span class="sxs-lookup"><span data-stu-id="7749a-173">Note that Allow forwarded traffic option is selected.</span></span>
   
    ![Basic Peering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure15a.png)
3. <span data-ttu-id="7749a-175">After peering is established, you can refer to this [article](virtual-network-create-udr-arm-ps.md) and define User Defined Route(UDR) to redirect VNet1 traffic through a virtual appliance to use its capabilities.</span><span class="sxs-lookup"><span data-stu-id="7749a-175">After peering is established, you can refer to this [article](virtual-network-create-udr-arm-ps.md) and define User Defined Route(UDR) to redirect VNet1 traffic through a virtual appliance to use its capabilities.</span></span> <span data-ttu-id="7749a-176">When you specify the Next Hop address in route, you can set it to the IP address of virtual appliance in peer VNet HubVNet</span><span class="sxs-lookup"><span data-stu-id="7749a-176">When you specify the Next Hop address in route, you can set it to the IP address of virtual appliance in peer VNet HubVNet</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-asmtoarm-include](../../includes/virtual-networks-create-vnetpeering-scenario-asmtoarm-include.md)]

1. <span data-ttu-id="7749a-177">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="7749a-177">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7749a-178">If you are creating a peering between VNets deployed through different deployment models in the *same* subscription, skip to step 3.</span><span class="sxs-lookup"><span data-stu-id="7749a-178">If you are creating a peering between VNets deployed through different deployment models in the *same* subscription, skip to step 3.</span></span> <span data-ttu-id="7749a-179">The ability to create a VNet peering between VNets deployed through different deployment models in *different* subscriptions is in **preview** release.</span><span class="sxs-lookup"><span data-stu-id="7749a-179">The ability to create a VNet peering between VNets deployed through different deployment models in *different* subscriptions is in **preview** release.</span></span> <span data-ttu-id="7749a-180">Capabilities in preview release do not have the same level of reliability and service level agreement as general release capabilities.</span><span class="sxs-lookup"><span data-stu-id="7749a-180">Capabilities in preview release do not have the same level of reliability and service level agreement as general release capabilities.</span></span> <span data-ttu-id="7749a-181">If you are creating a peering between VNets deployed through different deployment models in different subscriptions you must first complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="7749a-181">If you are creating a peering between VNets deployed through different deployment models in different subscriptions you must first complete the following tasks:</span></span>
    - <span data-ttu-id="7749a-182">Register the preview capability in your Azure subscription by entering the following commands from PowerShell: `Register-AzureRmProviderFeature -FeatureName AllowClassicCrossSubscriptionPeering -ProviderNamespace Microsoft.Network` and `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network` This step cannot be completed in the portal.</span><span class="sxs-lookup"><span data-stu-id="7749a-182">Register the preview capability in your Azure subscription by entering the following commands from PowerShell: `Register-AzureRmProviderFeature -FeatureName AllowClassicCrossSubscriptionPeering -ProviderNamespace Microsoft.Network` and `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network` This step cannot be completed in the portal.</span></span>
    - <span data-ttu-id="7749a-183">Complete steps 1-6 in the [Peering across subscriptions](#x-sub) section of this article.</span><span class="sxs-lookup"><span data-stu-id="7749a-183">Complete steps 1-6 in the [Peering across subscriptions](#x-sub) section of this article.</span></span>
3. <span data-ttu-id="7749a-184">To establish VNET peering in this scenario, you need to create only one link, from the virtual network in Azure resource manager to the one in classic.</span><span class="sxs-lookup"><span data-stu-id="7749a-184">To establish VNET peering in this scenario, you need to create only one link, from the virtual network in Azure resource manager to the one in classic.</span></span> <span data-ttu-id="7749a-185">That is, from **VNET1** to **VNET2**.</span><span class="sxs-lookup"><span data-stu-id="7749a-185">That is, from **VNET1** to **VNET2**.</span></span> <span data-ttu-id="7749a-186">On the portal, Click **Browse** > choose **Virtual Networks**</span><span class="sxs-lookup"><span data-stu-id="7749a-186">On the portal, Click **Browse** > choose **Virtual Networks**</span></span>
4. <span data-ttu-id="7749a-187">In the Virtual networks blade, choose **VNET1**.</span><span class="sxs-lookup"><span data-stu-id="7749a-187">In the Virtual networks blade, choose **VNET1**.</span></span> <span data-ttu-id="7749a-188">Click **Peerings**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7749a-188">Click **Peerings**, then click **Add**.</span></span>
5. <span data-ttu-id="7749a-189">In the **Add Peering** blade, name your link.</span><span class="sxs-lookup"><span data-stu-id="7749a-189">In the **Add Peering** blade, name your link.</span></span> <span data-ttu-id="7749a-190">Here it is called **LinkToVNet2**.</span><span class="sxs-lookup"><span data-stu-id="7749a-190">Here it is called **LinkToVNet2**.</span></span> <span data-ttu-id="7749a-191">Under Peer details, select **Classic**.</span><span class="sxs-lookup"><span data-stu-id="7749a-191">Under Peer details, select **Classic**.</span></span>
6. <span data-ttu-id="7749a-192">Choose the subscription and the peer Virtual Network **VNET2**.</span><span class="sxs-lookup"><span data-stu-id="7749a-192">Choose the subscription and the peer Virtual Network **VNET2**.</span></span> <span data-ttu-id="7749a-193">Then click OK.</span><span class="sxs-lookup"><span data-stu-id="7749a-193">Then click OK.</span></span>

    ![Linking Vnet1 to Vnet 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure18.png)
7. <span data-ttu-id="7749a-195">Once this VNet peering link is created, the two virtual networks are peered and you will be able to see the following:</span><span class="sxs-lookup"><span data-stu-id="7749a-195">Once this VNet peering link is created, the two virtual networks are peered and you will be able to see the following:</span></span>

    ![Checking peering connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure19.png)

## <a name="remove-vnet-peering"></a><span data-ttu-id="7749a-197">Remove VNet Peering</span><span class="sxs-lookup"><span data-stu-id="7749a-197">Remove VNet Peering</span></span>
1. <span data-ttu-id="7749a-198">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="7749a-198">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7749a-199">Go to virtual network blade, click Peerings, click the Link you want to remove, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7749a-199">Go to virtual network blade, click Peerings, click the Link you want to remove, then click **Delete**.</span></span>

    ![Delete1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure15.png)
3. <span data-ttu-id="7749a-201">Once you remove one link in VNET peering, the  peer link state will go to disconnected.</span><span class="sxs-lookup"><span data-stu-id="7749a-201">Once you remove one link in VNET peering, the  peer link state will go to disconnected.</span></span>

    ![Delete2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnetpeering-arm-portal/figure16.png)
4. <span data-ttu-id="7749a-203">In this state, you cannot re-create the link until the peer link state changes to Initiated.</span><span class="sxs-lookup"><span data-stu-id="7749a-203">In this state, you cannot re-create the link until the peer link state changes to Initiated.</span></span> <span data-ttu-id="7749a-204">We recommend you remove the both links before you re-create the VNET peering.</span><span class="sxs-lookup"><span data-stu-id="7749a-204">We recommend you remove the both links before you re-create the VNET peering.</span></span>




















