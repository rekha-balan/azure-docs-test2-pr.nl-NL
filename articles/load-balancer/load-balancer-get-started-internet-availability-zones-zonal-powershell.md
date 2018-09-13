---
title: Create a public Load Balancer Standard with zonal Public IP address frontend using Azure PowerShell | Microsoft Docs
description: Learn how to create public Load Balancer Standard with a zonal Public IP address frontend using Azure PowerShell
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
ms.openlocfilehash: dbb4176ac61cf707b28cddc98db80a1188be3cc8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865945"
---
#  <a name="create-a-public-load-balancer-standard-with-zonal-frontend-using-azure-powershell"></a><span data-ttu-id="18126-103">Create a public Load Balancer Standard with zonal frontend using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="18126-103">Create a public Load Balancer Standard with zonal frontend using Azure PowerShell</span></span>

<span data-ttu-id="18126-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend using a Public IP Standard address.</span><span class="sxs-lookup"><span data-stu-id="18126-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend using a Public IP Standard address.</span></span> <span data-ttu-id="18126-105">To understand how availability zones work with Standard Load Balancer, see [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="18126-105">To understand how availability zones work with Standard Load Balancer, see [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span> 

<span data-ttu-id="18126-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="18126-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!NOTE]
> <span data-ttu-id="18126-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="18126-107">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="18126-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="18126-108">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="18126-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18126-109">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="18126-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="18126-110">Log in to Azure</span></span>

<span data-ttu-id="18126-111">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="18126-111">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="18126-112">Create resource group</span><span class="sxs-lookup"><span data-stu-id="18126-112">Create resource group</span></span>

<span data-ttu-id="18126-113">Create a Resource Group using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-113">Create a Resource Group using the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupZLB -Location westeurope
```

## <a name="create-a-public-ip-standard"></a><span data-ttu-id="18126-114">Create a public IP Standard</span><span class="sxs-lookup"><span data-stu-id="18126-114">Create a public IP Standard</span></span> 
<span data-ttu-id="18126-115">Create a Public IP Standard using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-115">Create a Public IP Standard using the following command:</span></span>

```powershell
$publicIp = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupZLB -Name 'myPublicIPZonal' `
  -Location westeurope -AllocationMethod Static -Sku Standard -zone 1
```

## <a name="create-a-front-end-ip-configuration-for-the-website"></a><span data-ttu-id="18126-116">Create a front-end IP configuration for the website</span><span class="sxs-lookup"><span data-stu-id="18126-116">Create a front-end IP configuration for the website</span></span>

<span data-ttu-id="18126-117">Create a frontend IP configuration using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-117">Create a frontend IP configuration using the following command:</span></span>

```powershell
$feip = New-AzureRmLoadBalancerFrontendIpConfig -Name 'myFrontEnd' -PublicIpAddress $publicIp
```

## <a name="create-the-back-end-address-pool"></a><span data-ttu-id="18126-118">Create the back-end address pool</span><span class="sxs-lookup"><span data-stu-id="18126-118">Create the back-end address pool</span></span>

<span data-ttu-id="18126-119">Create a backend address pool using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-119">Create a backend address pool using the following command:</span></span>

```powershell
$bepool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name 'myBackEndPool'
```

## <a name="create-a-load-balancer-probe-on-port-80"></a><span data-ttu-id="18126-120">Create a load balancer probe on port 80</span><span class="sxs-lookup"><span data-stu-id="18126-120">Create a load balancer probe on port 80</span></span>

<span data-ttu-id="18126-121">Create a health probe on port 80 for the load balancer using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-121">Create a health probe on port 80 for the load balancer using the following command:</span></span>

```powershell
$probe = New-AzureRmLoadBalancerProbeConfig -Name 'myHealthProbe' -Protocol Http -Port 80 `
  -RequestPath / -IntervalInSeconds 360 -ProbeCount 5
```

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="18126-122">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="18126-122">Create a load balancer rule</span></span>
 <span data-ttu-id="18126-123">Create a load balancer rule using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-123">Create a load balancer rule using the following command:</span></span>

```powershell
   $rule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $feip -BackendAddressPool  $bepool -Probe $probe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

## <a name="create-a-load-balancer"></a><span data-ttu-id="18126-124">Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="18126-124">Create a load balancer</span></span>
<span data-ttu-id="18126-125">Create a Load Balancer Standard using the following command:</span><span class="sxs-lookup"><span data-stu-id="18126-125">Create a Load Balancer Standard using the following command:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer -ResourceGroupName myResourceGroupZLB -Name 'MyLoadBalancer' -Location westeurope `
  -FrontendIpConfiguration $feip -BackendAddressPool $bepool `
  -Probe $probe -LoadBalancingRule $rule -Sku Standard
```

## <a name="next-steps"></a><span data-ttu-id="18126-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="18126-126">Next steps</span></span>
- <span data-ttu-id="18126-127">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="18126-127">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span>



