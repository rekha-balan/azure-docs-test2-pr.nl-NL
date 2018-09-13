---
title: Create a public Load Balancer Standard with zone-redundant Public IP address frontend using Azure portal | Microsoft Docs
description: Learn how to create a public Load Balancer Standard with zone-redundant Public IP address frontend with the Azure portal
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
ms.date: 03/22/2018
ms.author: kumud
ms.openlocfilehash: 9a51638ea6d85178e6631ac278c116e4c7e05d61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866674"
---
#  <a name="create-a-public-load-balancer-standard-with-zone-redundant-public-ip-address-frontend-using-azure-portal"></a><span data-ttu-id="9d2ba-103">Create a public Load Balancer Standard with zone-redundant Public IP address frontend using Azure portal</span><span class="sxs-lookup"><span data-stu-id="9d2ba-103">Create a public Load Balancer Standard with zone-redundant Public IP address frontend using Azure portal</span></span>

<span data-ttu-id="9d2ba-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend using a Public IP Standard address.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend using a Public IP Standard address.</span></span> <span data-ttu-id="9d2ba-105">A single frontend IP address on a Standard Load Balancer is zone-redundant by default.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-105">A single frontend IP address on a Standard Load Balancer is zone-redundant by default.</span></span>

<span data-ttu-id="9d2ba-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!NOTE]
 <span data-ttu-id="9d2ba-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="9d2ba-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="9d2ba-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="9d2ba-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d2ba-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="9d2ba-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="9d2ba-110">Log in to Azure</span></span> 

<span data-ttu-id="9d2ba-111">Log in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-111">Log in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-a-zone-redundant-load-balancer"></a><span data-ttu-id="9d2ba-112">Create a zone redundant load balancer</span><span class="sxs-lookup"><span data-stu-id="9d2ba-112">Create a zone redundant load balancer</span></span>

1. <span data-ttu-id="9d2ba-113">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-113">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="9d2ba-114">On the top left-hand side of the screen, select **Create a resource** > **Networking** > **Load Balancer.**</span><span class="sxs-lookup"><span data-stu-id="9d2ba-114">On the top left-hand side of the screen, select **Create a resource** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="9d2ba-115">In the **Create load balancer** page, under **Name** type **myLoadBalancer**.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-115">In the **Create load balancer** page, under **Name** type **myLoadBalancer**.</span></span>
4. <span data-ttu-id="9d2ba-116">Under **Type**, select **Public**.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-116">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="9d2ba-117">Under SKU, select **Standard**.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-117">Under SKU, select **Standard**.</span></span>
6. <span data-ttu-id="9d2ba-118">Click **Public IP address**, click **Create new**, and in **Create public IP address** page, under name, type **myPublicIPStandard**.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-118">Click **Public IP address**, click **Create new**, and in **Create public IP address** page, under name, type **myPublicIPStandard**.</span></span>
    >[!NOTE] 
    > <span data-ttu-id="9d2ba-119">The public IP created in this step is of Standard SKU and is zone-redundant by default.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-119">The public IP created in this step is of Standard SKU and is zone-redundant by default.</span></span> 
8. <span data-ttu-id="9d2ba-120">Under **Location**, select **East US2**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-120">Under **Location**, select **East US2**, and then click **OK**.</span></span> <span data-ttu-id="9d2ba-121">The load balancer then starts to deploy and takes a few minutes to successfully complete deployment.</span><span class="sxs-lookup"><span data-stu-id="9d2ba-121">The load balancer then starts to deploy and takes a few minutes to successfully complete deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d2ba-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d2ba-122">Next steps</span></span>
- <span data-ttu-id="9d2ba-123">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="9d2ba-123">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span>



