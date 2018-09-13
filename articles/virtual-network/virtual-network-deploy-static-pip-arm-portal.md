---
title: Create a VM with a static public IP address - Azure portal | Microsoft Docs
description: Learn how to create a VM with a static public IP address using the Azure portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a1161bff2d2db559f3a2a881fed4c5d0ecb487c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553133"
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="48a2d-103">Create a VM with a static public IP address using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="48a2d-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Template](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md). This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="48a2d-111">Create a VM with a static public IP</span><span class="sxs-lookup"><span data-stu-id="48a2d-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="48a2d-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="48a2d-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="48a2d-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="48a2d-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="48a2d-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="48a2d-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="48a2d-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - Basics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="48a2d-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure portal - Choose a size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="48a2d-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span><span class="sxs-lookup"><span data-stu-id="48a2d-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="48a2d-121">And then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-121">And then click **OK**.</span></span>
   
    ![Azure portal - Create public IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="48a2d-123">In the **Settings** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="48a2d-124">Review the **Summary** blade, as shown below, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="48a2d-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - Create public IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="48a2d-126">Notice the new tile in your dashboard.</span><span class="sxs-lookup"><span data-stu-id="48a2d-126">Notice the new tile in your dashboard.</span></span>
   
    ![Azure portal - Create public IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="48a2d-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span><span class="sxs-lookup"><span data-stu-id="48a2d-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure portal - Create public IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-static-pip-arm-portal/figure6.png)







