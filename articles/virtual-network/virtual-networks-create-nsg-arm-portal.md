---
title: Manage network security groups - Azure portal | Microsoft Docs
description: Learn how to manage network security groups using the Azure portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd751ceca8ff57c2b26d6003f1c2c2c239877c50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554293"
---
# <a name="manage-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="5a960-103">Manage network security groups using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5a960-103">Manage network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5a960-104">This article covers the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="5a960-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="5a960-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5a960-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="5a960-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="5a960-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="5a960-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="5a960-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="5a960-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span><span class="sxs-lookup"><span data-stu-id="5a960-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="5a960-109">Create the NSG-FrontEnd NSG</span><span class="sxs-lookup"><span data-stu-id="5a960-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="5a960-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="5a960-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="5a960-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="5a960-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="5a960-112">Click **Browse >** > **Network Security Groups**.</span><span class="sxs-lookup"><span data-stu-id="5a960-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="5a960-114">In the **Network security groups** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="5a960-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="5a960-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5a960-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure portal - NSGs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="5a960-118">Create rules in an existing NSG</span><span class="sxs-lookup"><span data-stu-id="5a960-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="5a960-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="5a960-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="5a960-120">Click **Browse >** > **Network security groups**.</span><span class="sxs-lookup"><span data-stu-id="5a960-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="5a960-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span><span class="sxs-lookup"><span data-stu-id="5a960-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure portal - NSG-FrontEnd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="5a960-123">In the list of **Inbound security rules**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="5a960-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure portal - Add rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="5a960-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a960-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="5a960-126">Notice that most of these settings are default values already.</span><span class="sxs-lookup"><span data-stu-id="5a960-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure portal - Rule settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="5a960-128">After a few seconds you will see the new rule in the NSG.</span><span class="sxs-lookup"><span data-stu-id="5a960-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Azure portal - New rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="5a960-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span><span class="sxs-lookup"><span data-stu-id="5a960-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="5a960-131">Associate the NSG to the FrontEnd subnet</span><span class="sxs-lookup"><span data-stu-id="5a960-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="5a960-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="5a960-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="5a960-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="5a960-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure portal - TestVNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="5a960-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="5a960-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure portal - Subnet settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="5a960-137">In the **FrontEnd** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5a960-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure portal - Subnet settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="5a960-139">Create the NSG-BackEnd NSG</span><span class="sxs-lookup"><span data-stu-id="5a960-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="5a960-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="5a960-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="5a960-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="5a960-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="5a960-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span><span class="sxs-lookup"><span data-stu-id="5a960-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="5a960-143">Inbound rule</span><span class="sxs-lookup"><span data-stu-id="5a960-143">Inbound rule</span></span> | <span data-ttu-id="5a960-144">Outbound rule</span><span class="sxs-lookup"><span data-stu-id="5a960-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure portal - inbound rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure portal - outbound rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="5a960-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span><span class="sxs-lookup"><span data-stu-id="5a960-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a960-148">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5a960-148">Next Steps</span></span>
* <span data-ttu-id="5a960-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5a960-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="5a960-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span><span class="sxs-lookup"><span data-stu-id="5a960-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>













