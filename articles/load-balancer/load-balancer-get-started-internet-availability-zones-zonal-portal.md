---
title: Create a public Load Balancer Standard with zonal Public IP address frontend using Azure portal | Microsoft Docs
description: Learn how to create a public Load Balancer Standard with zonal Public IP address frontend with the Azure portal
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/26/2018
ms.author: kumud
ms.openlocfilehash: 533c48b3a004f85dfbd2970d73dcf7de21811dca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864538"
---
#  <a name="create-a-public-load-balancer-standard-with-zonal-public-ip-address-frontend-using-azure-portal"></a><span data-ttu-id="db6b9-103">Create a public Load Balancer Standard with zonal Public IP address frontend using Azure portal</span><span class="sxs-lookup"><span data-stu-id="db6b9-103">Create a public Load Balancer Standard with zonal Public IP address frontend using Azure portal</span></span>

<span data-ttu-id="db6b9-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend.</span><span class="sxs-lookup"><span data-stu-id="db6b9-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend.</span></span> <span data-ttu-id="db6b9-105">To understand how availability zones work with Standard Load Balancer, see [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="db6b9-105">To understand how availability zones work with Standard Load Balancer, see [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span> 

<span data-ttu-id="db6b9-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="db6b9-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!NOTE]
> <span data-ttu-id="db6b9-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="db6b9-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="db6b9-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="db6b9-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="db6b9-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db6b9-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="db6b9-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="db6b9-110">Log in to Azure</span></span> 

<span data-ttu-id="db6b9-111">Log in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="db6b9-111">Log in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-a-load-balancer-with-zonal-frontend-ip-address"></a><span data-ttu-id="db6b9-112">Create a load balancer with zonal frontend IP address</span><span class="sxs-lookup"><span data-stu-id="db6b9-112">Create a load balancer with zonal frontend IP address</span></span>

1. <span data-ttu-id="db6b9-113">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="db6b9-113">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="db6b9-114">On the top left-hand side of the screen, select **Create a resource** > **Networking** > **Load Balancer.**</span><span class="sxs-lookup"><span data-stu-id="db6b9-114">On the top left-hand side of the screen, select **Create a resource** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="db6b9-115">In the **Create load balancer** page, under **Name** type **myLoadBalancer**.</span><span class="sxs-lookup"><span data-stu-id="db6b9-115">In the **Create load balancer** page, under **Name** type **myLoadBalancer**.</span></span>
4. <span data-ttu-id="db6b9-116">Under **Type**, select **Public**.</span><span class="sxs-lookup"><span data-stu-id="db6b9-116">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="db6b9-117">Under SKU, select **Standard**.</span><span class="sxs-lookup"><span data-stu-id="db6b9-117">Under SKU, select **Standard**.</span></span>
6. <span data-ttu-id="db6b9-118">Click **Choose a Public IP address**, click **Create new**, and in **Create public IP address** page, under name, type **myPublicIPZonal**, for SKU, select **Standard**, for Availability zone, select **1**.</span><span class="sxs-lookup"><span data-stu-id="db6b9-118">Click **Choose a Public IP address**, click **Create new**, and in **Create public IP address** page, under name, type **myPublicIPZonal**, for SKU, select **Standard**, for Availability zone, select **1**.</span></span>
    
>[!NOTE] 
> <span data-ttu-id="db6b9-119">The public IP created in this step is of Standard SKU by default.</span><span class="sxs-lookup"><span data-stu-id="db6b9-119">The public IP created in this step is of Standard SKU by default.</span></span>

7. <span data-ttu-id="db6b9-120">For **Resource group**, click **Create new**, and then type **myResourceGroupZLB** as the name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="db6b9-120">For **Resource group**, click **Create new**, and then type **myResourceGroupZLB** as the name of the resource group.</span></span>
8. <span data-ttu-id="db6b9-121">For **Location**, select **West Europe**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="db6b9-121">For **Location**, select **West Europe**, and then click **OK**.</span></span> <span data-ttu-id="db6b9-122">The load balancer then starts to deploy and takes a few minutes to successfully complete deployment.</span><span class="sxs-lookup"><span data-stu-id="db6b9-122">The load balancer then starts to deploy and takes a few minutes to successfully complete deployment.</span></span>

    ![create zone-redundant Load Balancer Standard with the Azure portal](./media/load-balancer-get-started-internet-availability-zones-zonal-portal/load-balancer-zonal-frontend.png)


## <a name="next-steps"></a><span data-ttu-id="db6b9-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="db6b9-124">Next steps</span></span>
- <span data-ttu-id="db6b9-125">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="db6b9-125">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span>



