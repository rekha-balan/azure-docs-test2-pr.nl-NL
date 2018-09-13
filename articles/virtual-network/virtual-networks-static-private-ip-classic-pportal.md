---
title: Configure private IP addresses for VMs (Classic) - Azure portal | Microsoft Docs
description: Learn how to configure private IP addresses for virtual machines (Classic) using the Azure portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d45c444e6af2f86c84ee1716fc9decbe0e67e5b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540678"
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="dc083-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dc083-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="dc083-104">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="dc083-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="dc083-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="dc083-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="dc083-106">The sample steps below expect a simple environment already created.</span><span class="sxs-lookup"><span data-stu-id="dc083-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="dc083-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="dc083-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="dc083-108">How to specify a static private IP address when creating a VM</span><span class="sxs-lookup"><span data-stu-id="dc083-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="dc083-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="dc083-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="dc083-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="dc083-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="dc083-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc083-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="dc083-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span><span class="sxs-lookup"><span data-stu-id="dc083-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="dc083-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="dc083-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="dc083-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span><span class="sxs-lookup"><span data-stu-id="dc083-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="dc083-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span><span class="sxs-lookup"><span data-stu-id="dc083-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="dc083-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span><span class="sxs-lookup"><span data-stu-id="dc083-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="dc083-121">In the **Create VM** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc083-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="dc083-122">Notice the tile below displayed in your dashboard.</span><span class="sxs-lookup"><span data-stu-id="dc083-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="dc083-124">How to retrieve static private IP address information for a VM</span><span class="sxs-lookup"><span data-stu-id="dc083-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="dc083-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span><span class="sxs-lookup"><span data-stu-id="dc083-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="dc083-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span><span class="sxs-lookup"><span data-stu-id="dc083-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="dc083-128">How to remove a static private IP address from a VM</span><span class="sxs-lookup"><span data-stu-id="dc083-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="dc083-129">To remove the static private IP address from the VM created above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="dc083-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="dc083-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="dc083-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="dc083-132">How to add a static private IP address to an existing VM</span><span class="sxs-lookup"><span data-stu-id="dc083-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="dc083-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="dc083-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="dc083-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span><span class="sxs-lookup"><span data-stu-id="dc083-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="dc083-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="dc083-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc083-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc083-136">Next steps</span></span>
* <span data-ttu-id="dc083-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="dc083-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="dc083-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="dc083-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="dc083-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc083-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>








