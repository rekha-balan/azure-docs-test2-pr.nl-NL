---
title: Create a public Load Balancer Standard with zone-redundant Public IP address frontend using PowerShell | Microsoft Docs
description: Learn how to create public Load Balancer Standard with a zone-redundant Public IP address frontend using PowerShell
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2018
ms.author: kumud
ms.openlocfilehash: ba76037f36d3f4f8a06103105d65b3f2ddc88c96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867255"
---
#  <a name="create-a-public-load-balancer-standard-with-zone-redundant-public-ip-address-frontend-using-powershell"></a><span data-ttu-id="d123d-103">Create a public Load Balancer Standard with zone-redundant Public IP address frontend using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d123d-103">Create a public Load Balancer Standard with zone-redundant Public IP address frontend using PowerShell</span></span>

<span data-ttu-id="d123d-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend using a Public IP Standard address.</span><span class="sxs-lookup"><span data-stu-id="d123d-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend using a Public IP Standard address.</span></span>

<span data-ttu-id="d123d-105">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="d123d-105">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!NOTE]
 <span data-ttu-id="d123d-106">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="d123d-106">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="d123d-107">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="d123d-107">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="d123d-108">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d123d-108">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="d123d-109">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="d123d-109">Log in to Azure</span></span>

<span data-ttu-id="d123d-110">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="d123d-110">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="d123d-111">Create resource group</span><span class="sxs-lookup"><span data-stu-id="d123d-111">Create resource group</span></span>

<span data-ttu-id="d123d-112">Create a Resource Group using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-112">Create a Resource Group using the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location westeurope
```

## <a name="create-a-public-ip-standard"></a><span data-ttu-id="d123d-113">Create a public IP Standard</span><span class="sxs-lookup"><span data-stu-id="d123d-113">Create a public IP Standard</span></span> 
<span data-ttu-id="d123d-114">Create a Public IP Standard using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-114">Create a Public IP Standard using the following command:</span></span>

```powershell
$publicIp = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Name 'myPublicIP' `
  -Location westeurope -AllocationMethod Static -Sku Standard 
```

## <a name="create-a-front-end-ip-configuration-for-the-website"></a><span data-ttu-id="d123d-115">Create a front-end IP configuration for the website</span><span class="sxs-lookup"><span data-stu-id="d123d-115">Create a front-end IP configuration for the website</span></span>

<span data-ttu-id="d123d-116">Create a frontend IP configuration using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-116">Create a frontend IP configuration using the following command:</span></span>

```powershell
$feip = New-AzureRmLoadBalancerFrontendIpConfig -Name 'myFrontEndPool' -PublicIpAddress $publicIp
```

## <a name="create-the-back-end-address-pool"></a><span data-ttu-id="d123d-117">Create the back-end address pool</span><span class="sxs-lookup"><span data-stu-id="d123d-117">Create the back-end address pool</span></span>

<span data-ttu-id="d123d-118">Create a backend address pool using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-118">Create a backend address pool using the following command:</span></span>

```powershell
$bepool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name 'myBackEndPool'
```

## <a name="create-a-load-balancer-probe-on-port-80"></a><span data-ttu-id="d123d-119">Create a load balancer probe on port 80</span><span class="sxs-lookup"><span data-stu-id="d123d-119">Create a load balancer probe on port 80</span></span>

<span data-ttu-id="d123d-120">Create a health probe on port 80 for the load balancer using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-120">Create a health probe on port 80 for the load balancer using the following command:</span></span>

```powershell
$probe = New-AzureRmLoadBalancerProbeConfig -Name 'myHealthProbe' -Protocol Http -Port 80 `
  -RequestPath / -IntervalInSeconds 360 -ProbeCount 5
```

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="d123d-121">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="d123d-121">Create a load balancer rule</span></span>
 <span data-ttu-id="d123d-122">Create a load balancer rule using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-122">Create a load balancer rule using the following command:</span></span>

```powershell
   $rule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $feip -BackendAddressPool  $bepool -Probe $probe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

## <a name="create-a-load-balancer"></a><span data-ttu-id="d123d-123">Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="d123d-123">Create a load balancer</span></span>
<span data-ttu-id="d123d-124">Create a Load Balancer Standard using the following command:</span><span class="sxs-lookup"><span data-stu-id="d123d-124">Create a Load Balancer Standard using the following command:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer -ResourceGroupName myResourceGroup -Name 'MyLoadBalancer' -Location westeurope `
  -FrontendIpConfiguration $feip -BackendAddressPool $bepool `
  -Probe $probe -LoadBalancingRule $rule -Sku Standard
```

## <a name="next-steps"></a><span data-ttu-id="d123d-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="d123d-125">Next steps</span></span>
- <span data-ttu-id="d123d-126">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="d123d-126">Learn more about [Standard Load Balancer and Availability zones](load-balancer-standard-availability-zones.md).</span></span>



