---
title: Create a public Load Balancer Standard with zonal frontend using Azure CLI | Microsoft Docs
description: Learn how to create a public Load Balancer Standard with zonal frontend using Azure CLI
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
ms.openlocfilehash: ac950c0c8971f5ea8260a9e0285961ffa2f8e133
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868174"
---
#  <a name="create-a-public-load-balancer-standard-with-zonal-frontend-using-azure-cli"></a><span data-ttu-id="5b99c-103">Create a public Load Balancer Standard with zonal frontend using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5b99c-103">Create a public Load Balancer Standard with zonal frontend using Azure CLI</span></span>

<span data-ttu-id="5b99c-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend.</span><span class="sxs-lookup"><span data-stu-id="5b99c-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend.</span></span> <span data-ttu-id="5b99c-105">Having a zonal frontend means that any inbound or outbound flow is served by a single zone in a region.</span><span class="sxs-lookup"><span data-stu-id="5b99c-105">Having a zonal frontend means that any inbound or outbound flow is served by a single zone in a region.</span></span> <span data-ttu-id="5b99c-106">You can create a load balancer with a zonal frontend by using a zonal Standard Public IP address in its frontend configuration.</span><span class="sxs-lookup"><span data-stu-id="5b99c-106">You can create a load balancer with a zonal frontend by using a zonal Standard Public IP address in its frontend configuration.</span></span> <span data-ttu-id="5b99c-107">To understand how availability zones work with Standard Load Balancer, see [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="5b99c-107">To understand how availability zones work with Standard Load Balancer, see [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span> 

<span data-ttu-id="5b99c-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="5b99c-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5b99c-109">If you choose to install and use the CLI locally, make sure that you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) and are logged in to an Azure account with [az login](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest#az-login).</span><span class="sxs-lookup"><span data-stu-id="5b99c-109">If you choose to install and use the CLI locally, make sure that you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) and are logged in to an Azure account with [az login](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest#az-login).</span></span>

> [!NOTE]
> <span data-ttu-id="5b99c-110">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="5b99c-110">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="5b99c-111">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="5b99c-111">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="5b99c-112">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b99c-112">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="5b99c-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="5b99c-113">Create a resource group</span></span>

<span data-ttu-id="5b99c-114">Create a resource group using the following command:</span><span class="sxs-lookup"><span data-stu-id="5b99c-114">Create a resource group using the following command:</span></span>

```azurecli-interactive
az group create --name myResourceGroupZLB --location westeurope
```

## <a name="create-a-public-standard-ip-address"></a><span data-ttu-id="5b99c-115">Create a public Standard IP address</span><span class="sxs-lookup"><span data-stu-id="5b99c-115">Create a public Standard IP address</span></span>

<span data-ttu-id="5b99c-116">Create a zonal Standard Public IP address using the following command:</span><span class="sxs-lookup"><span data-stu-id="5b99c-116">Create a zonal Standard Public IP address using the following command:</span></span>

```azurecli-interactive
az network public-ip create --resource-group myResourceGroupZLB --name myPublicIPZonal --sku Standard --zone 1
```

## <a name="create-a-load-balancer"></a><span data-ttu-id="5b99c-117">Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="5b99c-117">Create a load balancer</span></span>

<span data-ttu-id="5b99c-118">Create a Public Load Balancer Standard with the Standard Public IP that you created in the preceding step using the following command:</span><span class="sxs-lookup"><span data-stu-id="5b99c-118">Create a Public Load Balancer Standard with the Standard Public IP that you created in the preceding step using the following command:</span></span>

```azurecli-interactive
az network lb create --resource-group myResourceGroupZLB --name myLoadBalancer --public-ip-address myPublicIPZonal --frontend-ip-name myFrontEnd --backend-pool-name myBackEndPool --sku Standard
```

## <a name="create-an-lb-probe-on-port-80"></a><span data-ttu-id="5b99c-119">Create an LB probe on port 80</span><span class="sxs-lookup"><span data-stu-id="5b99c-119">Create an LB probe on port 80</span></span>

<span data-ttu-id="5b99c-120">Create a load balancer health probe using the following command:</span><span class="sxs-lookup"><span data-stu-id="5b99c-120">Create a load balancer health probe using the following command:</span></span>

```azurecli-interactive
az network lb probe create --resource-group myResourceGroupZLB --lb-name myLoadBalancer \
  --name myHealthProbe --protocol tcp --port 80
```

## <a name="create-an-lb-rule-for-port-80"></a><span data-ttu-id="5b99c-121">Create an LB rule for port 80</span><span class="sxs-lookup"><span data-stu-id="5b99c-121">Create an LB rule for port 80</span></span>

<span data-ttu-id="5b99c-122">Create a load balancer rule using the following command:</span><span class="sxs-lookup"><span data-stu-id="5b99c-122">Create a load balancer rule using the following command:</span></span>

```azurecli-interactive
az network lb rule create --resource-group myResourceGroupZLB --lb-name myLoadBalancer --name myLoadBalancerRuleWeb \
  --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEnd \
  --backend-pool-name myBackEndPool --probe-name myHealthProbe
```

## <a name="next-steps"></a><span data-ttu-id="5b99c-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b99c-123">Next steps</span></span>
- <span data-ttu-id="5b99c-124">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="5b99c-124">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span>



