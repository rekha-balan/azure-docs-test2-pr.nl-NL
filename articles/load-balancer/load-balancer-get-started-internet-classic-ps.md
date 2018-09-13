---
title: Create an Internet-facing load balancer - Azure PowerShell classic | Microsoft Docs
description: Learn how to create an Internet facing load balancer in classic mode using PowerShell
services: load-balancer
documentationcenter: na
author: genlin
manager: cshepard
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: genli
ms.openlocfilehash: 07d3658ff86a46875a57cb3359a60661911e0c8b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825071"
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="af950-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span><span class="sxs-lookup"><span data-stu-id="af950-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic. Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource. You can view the documentation for different tools by clicking the tabs at the top of this article. This article covers the classic deployment model. You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="af950-112">Set up load balancer using PowerShell</span><span class="sxs-lookup"><span data-stu-id="af950-112">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="af950-113">To set up a load balancer using powershell, complete following steps:</span><span class="sxs-lookup"><span data-stu-id="af950-113">To set up a load balancer using powershell, complete following steps:</span></span>

1. <span data-ttu-id="af950-114">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="af950-114">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="af950-115">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="af950-115">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="af950-116">In the following example, you add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net), adding the endpoints for the load balancer to virtual machines named "web1" and "web2."</span><span class="sxs-lookup"><span data-stu-id="af950-116">In the following example, you add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net), adding the endpoints for the load balancer to virtual machines named "web1" and "web2."</span></span> <span data-ttu-id="af950-117">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span><span class="sxs-lookup"><span data-stu-id="af950-117">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="af950-118">Step 1</span><span class="sxs-lookup"><span data-stu-id="af950-118">Step 1</span></span>

<span data-ttu-id="af950-119">Create a load balanced endpoint for the first VM "web1"</span><span class="sxs-lookup"><span data-stu-id="af950-119">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="af950-120">Step 2</span><span class="sxs-lookup"><span data-stu-id="af950-120">Step 2</span></span>

<span data-ttu-id="af950-121">Create another endpoint for the second VM  "web2" using the same load balancer set name</span><span class="sxs-lookup"><span data-stu-id="af950-121">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="af950-122">Remove a virtual machine from a load balancer</span><span class="sxs-lookup"><span data-stu-id="af950-122">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="af950-123">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span><span class="sxs-lookup"><span data-stu-id="af950-123">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="af950-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="af950-124">Next steps</span></span>

<span data-ttu-id="af950-125">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span><span class="sxs-lookup"><span data-stu-id="af950-125">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="af950-126">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="af950-126">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="af950-127">It helps to learn about idle connection behavior when you are using Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="af950-127">It helps to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
