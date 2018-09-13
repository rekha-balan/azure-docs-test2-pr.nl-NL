---
title: Configure a virtual network in Azure DevTest Labs  | Microsoft Docs
description: Learn how to configure an existing virtual network and subnet, and use them in a VM with Azure DevTest Labs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: 0141ea8a88c0322e6f56cbea56d3a43c923769af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966577"
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="0fccd-103">Configure a virtual network in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0fccd-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="0fccd-104">As explained in the article [Add a VM to a lab](devtest-lab-add-vm.md), when you create a VM in a lab, you can specify a configured virtual network.</span><span class="sxs-lookup"><span data-stu-id="0fccd-104">As explained in the article [Add a VM to a lab](devtest-lab-add-vm.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="0fccd-105">For example, you might need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span><span class="sxs-lookup"><span data-stu-id="0fccd-105">For example, you might need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span>

<span data-ttu-id="0fccd-106">This article explains how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span><span class="sxs-lookup"><span data-stu-id="0fccd-106">This article explains how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="0fccd-107">Configure a virtual network for a lab using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0fccd-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="0fccd-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span><span class="sxs-lookup"><span data-stu-id="0fccd-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="0fccd-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="0fccd-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="0fccd-110">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="0fccd-110">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="0fccd-111">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="0fccd-111">From the list of labs, select the desired lab.</span></span> 
1. <span data-ttu-id="0fccd-112">On the lab's main pane, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-112">On the lab's main pane, select **Configuration and policies**.</span></span>

    ![Access the lab's configuration and policies](./media/devtest-lab-configure-vnet/policies-menu.png)
1. <span data-ttu-id="0fccd-114">In the **EXTERNAL RESOURCES** section, select **Virtual networks**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-114">In the **EXTERNAL RESOURCES** section, select **Virtual networks**.</span></span> <span data-ttu-id="0fccd-115">A list of virtual networks configured for the current lab is displayed as well as the default virtual network created for your lab.</span><span class="sxs-lookup"><span data-stu-id="0fccd-115">A list of virtual networks configured for the current lab is displayed as well as the default virtual network created for your lab.</span></span> 
1. <span data-ttu-id="0fccd-116">Select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-116">Select **+ Add**.</span></span>
   
    ![Add an existing virtual network to your lab](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
1. <span data-ttu-id="0fccd-118">On the **Virtual network** pane, select **[Select virtual network]**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-118">On the **Virtual network** pane, select **[Select virtual network]**.</span></span>
   
    ![Select an existing virtual network](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
1. <span data-ttu-id="0fccd-120">On the **Choose virtual network** pane, select the desired virtual network.</span><span class="sxs-lookup"><span data-stu-id="0fccd-120">On the **Choose virtual network** pane, select the desired virtual network.</span></span> <span data-ttu-id="0fccd-121">A list is displayed showing all of the virtual networks that are under the same region in the subscription as the lab.</span><span class="sxs-lookup"><span data-stu-id="0fccd-121">A list is displayed showing all of the virtual networks that are under the same region in the subscription as the lab.</span></span>
1. <span data-ttu-id="0fccd-122">After selecting a virtual network, you are returned to the **Virtual network** pane.</span><span class="sxs-lookup"><span data-stu-id="0fccd-122">After selecting a virtual network, you are returned to the **Virtual network** pane.</span></span> <span data-ttu-id="0fccd-123">Select the subnet in the list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0fccd-123">Select the subnet in the list at the bottom.</span></span>

    ![Subnet list](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="0fccd-125">The Lab Subnet pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="0fccd-125">The Lab Subnet pane is displayed.</span></span>

    ![Lab subnet pane](./media/devtest-lab-configure-vnet/lab-subnet.png)
     
   - <span data-ttu-id="0fccd-127">Specify a **Lab subnet name**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-127">Specify a **Lab subnet name**.</span></span>
   - <span data-ttu-id="0fccd-128">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-128">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
   - <span data-ttu-id="0fccd-129">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-129">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
   - <span data-ttu-id="0fccd-130">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span><span class="sxs-lookup"><span data-stu-id="0fccd-130">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
   - <span data-ttu-id="0fccd-131">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span><span class="sxs-lookup"><span data-stu-id="0fccd-131">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="0fccd-132">If you want an unrestricted number of VMs, leave this field blank.</span><span class="sxs-lookup"><span data-stu-id="0fccd-132">If you want an unrestricted number of VMs, leave this field blank.</span></span>
1. <span data-ttu-id="0fccd-133">Select **OK** to close the Lab Subnet pane.</span><span class="sxs-lookup"><span data-stu-id="0fccd-133">Select **OK** to close the Lab Subnet pane.</span></span>
1. <span data-ttu-id="0fccd-134">Select **Save** to close the Virtual network pane.</span><span class="sxs-lookup"><span data-stu-id="0fccd-134">Select **Save** to close the Virtual network pane.</span></span>

<span data-ttu-id="0fccd-135">Now that the virtual network is configured, it can be selected when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="0fccd-135">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> <span data-ttu-id="0fccd-136">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM to a lab](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0fccd-136">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM to a lab](devtest-lab-add-vm.md).</span></span> 

<span data-ttu-id="0fccd-137">Azure's [Virtual Network Documentation](https://docs.microsoft.com/azure/virtual-network) provides more information about how to use VNets, including how to set up and manage a VNet and connect it to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="0fccd-137">Azure's [Virtual Network Documentation](https://docs.microsoft.com/azure/virtual-network) provides more information about how to use VNets, including how to set up and manage a VNet and connect it to your on-premises network.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="0fccd-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fccd-138">Next steps</span></span>
<span data-ttu-id="0fccd-139">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0fccd-139">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm.md).</span></span>

