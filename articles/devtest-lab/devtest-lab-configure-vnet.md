---
title: Configure a virtual network in Azure DevTest Labs  | Microsoft Docs
description: Learn how to configure an existing virtual network and subnet, and use them in a VM with Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: b900901c0cd843f5dc4fe5a09b68d84543187aac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662534"
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="ae33c-103">Configure a virtual network in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ae33c-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="ae33c-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span><span class="sxs-lookup"><span data-stu-id="ae33c-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="ae33c-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span><span class="sxs-lookup"><span data-stu-id="ae33c-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="ae33c-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span><span class="sxs-lookup"><span data-stu-id="ae33c-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="ae33c-107">Configure a virtual network for a lab using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ae33c-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="ae33c-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span><span class="sxs-lookup"><span data-stu-id="ae33c-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="ae33c-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ae33c-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="ae33c-110">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="ae33c-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="ae33c-111">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="ae33c-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="ae33c-112">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="ae33c-113">On the lab's **Configuration** blade, select **Virtual networks**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="ae33c-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span><span class="sxs-lookup"><span data-stu-id="ae33c-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="ae33c-115">Select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-115">Select **+ Add**.</span></span>
   
    ![Add an existing virtual network to your lab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="ae33c-117">On the **Virtual network** blade, select **[Select virtual network]**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Select an existing virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="ae33c-119">On the **Choose virtual network** blade, select the desired virtual network.</span><span class="sxs-lookup"><span data-stu-id="ae33c-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="ae33c-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span><span class="sxs-lookup"><span data-stu-id="ae33c-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="ae33c-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="ae33c-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Subnet list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="ae33c-123">The Lab Subnet blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="ae33c-123">The Lab Subnet blade is displayed.</span></span>

    ![Lab subnet blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="ae33c-125">Specify a **Lab subnet name**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="ae33c-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="ae33c-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="ae33c-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span><span class="sxs-lookup"><span data-stu-id="ae33c-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="ae33c-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span><span class="sxs-lookup"><span data-stu-id="ae33c-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="ae33c-130">If you want an unrestricted number of VMs, leave this field blank.</span><span class="sxs-lookup"><span data-stu-id="ae33c-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="ae33c-131">Select **OK** to close the Lab Subnet blade.</span><span class="sxs-lookup"><span data-stu-id="ae33c-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="ae33c-132">Select **Save** to close the Virtual network blade.</span><span class="sxs-lookup"><span data-stu-id="ae33c-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="ae33c-133">Now that the virtual network is configured, it can be selected when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="ae33c-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="ae33c-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="ae33c-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="ae33c-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae33c-135">Next steps</span></span>
<span data-ttu-id="ae33c-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="ae33c-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>





