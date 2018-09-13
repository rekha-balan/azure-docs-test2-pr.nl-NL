---
title: Create an Internet-facing load balancer - Azure PowerShell classic | Microsoft Docs
description: Learn how to create an Internet facing load balancer in classic mode using PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: b889208da300f301ee5c418bfa461a21cd8c07ee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660778"
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="e23aa-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span><span class="sxs-lookup"><span data-stu-id="e23aa-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure classic portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic. Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource. You can view the documentation for different tools by clicking the tabs at the top of this article. This article covers the classic deployment model. You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="e23aa-113">Set up load balancer using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e23aa-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="e23aa-114">To set up a load balancer using powershell, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="e23aa-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="e23aa-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="e23aa-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="e23aa-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="e23aa-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="e23aa-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span><span class="sxs-lookup"><span data-stu-id="e23aa-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="e23aa-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span><span class="sxs-lookup"><span data-stu-id="e23aa-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="e23aa-119">Step 1</span><span class="sxs-lookup"><span data-stu-id="e23aa-119">Step 1</span></span>

<span data-ttu-id="e23aa-120">Create a load balanced endpoint for the first VM "web1"</span><span class="sxs-lookup"><span data-stu-id="e23aa-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="e23aa-121">Step 2</span><span class="sxs-lookup"><span data-stu-id="e23aa-121">Step 2</span></span>

<span data-ttu-id="e23aa-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span><span class="sxs-lookup"><span data-stu-id="e23aa-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="e23aa-123">Remove a virtual machine from a load balancer</span><span class="sxs-lookup"><span data-stu-id="e23aa-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="e23aa-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span><span class="sxs-lookup"><span data-stu-id="e23aa-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="e23aa-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="e23aa-125">Next steps</span></span>

<span data-ttu-id="e23aa-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span><span class="sxs-lookup"><span data-stu-id="e23aa-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="e23aa-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="e23aa-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="e23aa-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e23aa-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
