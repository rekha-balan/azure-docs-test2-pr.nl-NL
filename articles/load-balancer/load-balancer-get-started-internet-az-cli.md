---
title: Create a public Load Balancer Standard with zone-redundant Public IP address frontend using Azure CLI | Microsoft Docs
description: Learn how to create a public Load Balancer Standard with zone-redundant Public IP address frontend using Azure CLI
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
ms.openlocfilehash: 785041b41395af385dcbbdc30df30e9d83db9e73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864801"
---
#  <a name="create-a-public-load-balancer-standard-with-zone-redundant-frontend-using-azure-cli"></a><span data-ttu-id="560f2-103">Create a public Load Balancer Standard with zone-redundant frontend using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="560f2-103">Create a public Load Balancer Standard with zone-redundant frontend using Azure CLI</span></span>

<span data-ttu-id="560f2-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend using a Public IP Standard address.</span><span class="sxs-lookup"><span data-stu-id="560f2-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend using a Public IP Standard address.</span></span>

<span data-ttu-id="560f2-105">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="560f2-105">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="560f2-106">If you choose to install and use the CLI locally, make sure that you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) and are logged in to an Azure account with [az login](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest#az-login).</span><span class="sxs-lookup"><span data-stu-id="560f2-106">If you choose to install and use the CLI locally, make sure that you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) and are logged in to an Azure account with [az login](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest#az-login).</span></span>

> [!NOTE]
 <span data-ttu-id="560f2-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="560f2-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="560f2-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="560f2-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="560f2-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="560f2-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="560f2-110">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="560f2-110">Create a resource group</span></span>

<span data-ttu-id="560f2-111">Create a resource group using the following command:</span><span class="sxs-lookup"><span data-stu-id="560f2-111">Create a resource group using the following command:</span></span>

```azurecli-interactive
az group create --name myResourceGroupSLB --location westeurope
```

## <a name="create-a-public-ip-standard"></a><span data-ttu-id="560f2-112">Create a public IP Standard</span><span class="sxs-lookup"><span data-stu-id="560f2-112">Create a public IP Standard</span></span>

<span data-ttu-id="560f2-113">Create a Public IP Standard using the following command:</span><span class="sxs-lookup"><span data-stu-id="560f2-113">Create a Public IP Standard using the following command:</span></span>

```azurecli-interactive
az network public-ip create --resource-group myResourceGroupSLB --name myPublicIP --sku Standard
```

## <a name="create-a-load-balancer"></a><span data-ttu-id="560f2-114">Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="560f2-114">Create a load balancer</span></span>

<span data-ttu-id="560f2-115">Create a Public Load Balancer Standard with the Standard Public IP that you created in the preceding step using the following command:</span><span class="sxs-lookup"><span data-stu-id="560f2-115">Create a Public Load Balancer Standard with the Standard Public IP that you created in the preceding step using the following command:</span></span>

```azurecli-interactive
az network lb create --resource-group myResourceGroupSLB --name myLoadBalancer --public-ip-address myPublicIP --frontend-ip-name myFrontEnd --backend-pool-name myBackEndPool --sku Standard
```

## <a name="create-an-lb-probe-on-port-80"></a><span data-ttu-id="560f2-116">Create an LB probe on port 80</span><span class="sxs-lookup"><span data-stu-id="560f2-116">Create an LB probe on port 80</span></span>

<span data-ttu-id="560f2-117">Create a load balancer health probe using the following command:</span><span class="sxs-lookup"><span data-stu-id="560f2-117">Create a load balancer health probe using the following command:</span></span>

```azurecli-interactive
az network lb probe create --resource-group myResourceGroupSLB --lb-name myLoadBalancer \
  --name myHealthProbe --protocol tcp --port 80
```

## <a name="create-an-lb-rule-for-port-80"></a><span data-ttu-id="560f2-118">Create an LB rule for port 80</span><span class="sxs-lookup"><span data-stu-id="560f2-118">Create an LB rule for port 80</span></span>

<span data-ttu-id="560f2-119">Create a load balancer rule using the following command:</span><span class="sxs-lookup"><span data-stu-id="560f2-119">Create a load balancer rule using the following command:</span></span>

```azurecli-interactive
az network lb rule create --resource-group myResourceGroup --lb-name myLoadBalancer --name myLoadBalancerRuleWeb \
  --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEnd \
  --backend-pool-name myBackEndPool --probe-name myHealthProbe
```

## <a name="next-steps"></a><span data-ttu-id="560f2-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="560f2-120">Next steps</span></span>
- <span data-ttu-id="560f2-121">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="560f2-121">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span>



