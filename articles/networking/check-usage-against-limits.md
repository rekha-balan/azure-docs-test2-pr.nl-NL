---
title: Check Azure resource usage against limits | Microsoft Docs
description: Learn how to check your Azure resource usage against Azure subscription limits.
services: networking
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: networking
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2018
ms.author: jdial
ms.openlocfilehash: 30b0c1bdd23858b5cc6224deb2698b5f180359eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871643"
---
# <a name="check-resource-usage-against-limits"></a><span data-ttu-id="0e4e4-103">Check resource usage against limits</span><span class="sxs-lookup"><span data-stu-id="0e4e4-103">Check resource usage against limits</span></span>

<span data-ttu-id="0e4e4-104">In this article, you learn how to see the number of each network resource type that you've deployed in your subscription and what your [subscription limits](../azure-subscription-service-limits.md?toc=%2fazure%2fnetworking%2ftoc.json#networking-limits) are.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-104">In this article, you learn how to see the number of each network resource type that you've deployed in your subscription and what your [subscription limits](../azure-subscription-service-limits.md?toc=%2fazure%2fnetworking%2ftoc.json#networking-limits) are.</span></span> <span data-ttu-id="0e4e4-105">The ability to view resource usage against limits is helpful to track current usage, and plan for future use.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-105">The ability to view resource usage against limits is helpful to track current usage, and plan for future use.</span></span> <span data-ttu-id="0e4e4-106">You can use the [Azure Portal](#azure-portal), [PowerShell](#powershell), or the [Azure CLI](#azure-cli) to track usage.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-106">You can use the [Azure Portal](#azure-portal), [PowerShell](#powershell), or the [Azure CLI](#azure-cli) to track usage.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="0e4e4-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0e4e4-107">Azure Portal</span></span>

1. <span data-ttu-id="0e4e4-108">Log into the Azure [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-108">Log into the Azure [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0e4e4-109">At the top, left corner of the Azure portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-109">At the top, left corner of the Azure portal, select **All services**.</span></span>
3. <span data-ttu-id="0e4e4-110">Enter *Subscriptions* in the **Filter** box.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-110">Enter *Subscriptions* in the **Filter** box.</span></span> <span data-ttu-id="0e4e4-111">When **Subscriptions** appears in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-111">When **Subscriptions** appears in the search results, select it.</span></span>
4. <span data-ttu-id="0e4e4-112">Select the name of the subscription you want to view usage information for.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-112">Select the name of the subscription you want to view usage information for.</span></span>
5. <span data-ttu-id="0e4e4-113">Under **SETTINGS**, select **Usage + quota**.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-113">Under **SETTINGS**, select **Usage + quota**.</span></span>
6. <span data-ttu-id="0e4e4-114">You can select the following options:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-114">You can select the following options:</span></span>
    - <span data-ttu-id="0e4e4-115">**Resource types**: You can select all resource types, or select the specific types of resources you want to view.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-115">**Resource types**: You can select all resource types, or select the specific types of resources you want to view.</span></span>
    - <span data-ttu-id="0e4e4-116">**Providers**: You can select all resource providers, or select **Compute**, **Network**, or **Storage**.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-116">**Providers**: You can select all resource providers, or select **Compute**, **Network**, or **Storage**.</span></span>
    - <span data-ttu-id="0e4e4-117">**Locations**: You can select all Azure locations, or select specific locations.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-117">**Locations**: You can select all Azure locations, or select specific locations.</span></span>
    - <span data-ttu-id="0e4e4-118">You can select to show all resources, or only the resources where at least one is deployed.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-118">You can select to show all resources, or only the resources where at least one is deployed.</span></span>

    <span data-ttu-id="0e4e4-119">The example in the following picture shows all of the network resources with at least one resource deployed in the East US:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-119">The example in the following picture shows all of the network resources with at least one resource deployed in the East US:</span></span>

        ![View usage data](./media/check-usage-against-limits/view-usage.png)

    <span data-ttu-id="0e4e4-120">You can sort the columns by selecting the column heading.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-120">You can sort the columns by selecting the column heading.</span></span> <span data-ttu-id="0e4e4-121">The limits shown are the limits for your subscription.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-121">The limits shown are the limits for your subscription.</span></span> <span data-ttu-id="0e4e4-122">If you need to increase a default limit, select **Request Increase**, then complete and submit the support request.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-122">If you need to increase a default limit, select **Request Increase**, then complete and submit the support request.</span></span> <span data-ttu-id="0e4e4-123">All resources have a maximum limit listed in Azure [limits](../azure-subscription-service-limits.md?toc=%2fazure%2fnetworking%2ftoc.json#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-123">All resources have a maximum limit listed in Azure [limits](../azure-subscription-service-limits.md?toc=%2fazure%2fnetworking%2ftoc.json#networking-limits).</span></span> <span data-ttu-id="0e4e4-124">If your current limit is already at the maximum number, the limit can't be increased.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-124">If your current limit is already at the maximum number, the limit can't be increased.</span></span>

## <a name="powershell"></a><span data-ttu-id="0e4e4-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e4e4-125">PowerShell</span></span>

<span data-ttu-id="0e4e4-126">You can run the commands that follow in the [Azure Cloud Shell](https://shell.azure.com/powershell), or by running PowerShell from your computer.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-126">You can run the commands that follow in the [Azure Cloud Shell](https://shell.azure.com/powershell), or by running PowerShell from your computer.</span></span> <span data-ttu-id="0e4e4-127">The Azure Cloud Shell is a free interactive shell.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-127">The Azure Cloud Shell is a free interactive shell.</span></span> <span data-ttu-id="0e4e4-128">It has common Azure tools preinstalled and configured to use with your account.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-128">It has common Azure tools preinstalled and configured to use with your account.</span></span> <span data-ttu-id="0e4e4-129">If you run PowerShell from your computer, you need the *AzureRM* PowerShell module, version 6.0.1 or later.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-129">If you run PowerShell from your computer, you need the *AzureRM* PowerShell module, version 6.0.1 or later.</span></span> <span data-ttu-id="0e4e4-130">Run `Get-Module -ListAvailable AzureRM` on your computer, to find the installed version.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-130">Run `Get-Module -ListAvailable AzureRM` on your computer, to find the installed version.</span></span> <span data-ttu-id="0e4e4-131">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-131">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="0e4e4-132">If you're running PowerShell locally, you also need to run `Login-AzureRmAccount` to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-132">If you're running PowerShell locally, you also need to run `Login-AzureRmAccount` to log in to Azure.</span></span>

<span data-ttu-id="0e4e4-133">View your usage against limits with [Get-AzureRmNetworkUsage](https://docs.microsoft.com/en-us/powershell/module/azurerm.network/get-azurermnetworkusage?view=azurermps-6.8.0).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-133">View your usage against limits with [Get-AzureRmNetworkUsage](https://docs.microsoft.com/en-us/powershell/module/azurerm.network/get-azurermnetworkusage?view=azurermps-6.8.0).</span></span> <span data-ttu-id="0e4e4-134">The following example gets the usage for resources where at least one resource is deployed in the East US location:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-134">The following example gets the usage for resources where at least one resource is deployed in the East US location:</span></span>

```azurepowershell-interactive
Get-AzureRmNetworkUsage `
  -Location eastus `
  | Where-Object {$_.CurrentValue -gt 0} `
  | Format-Table ResourceType, CurrentValue, Limit
```

<span data-ttu-id="0e4e4-135">You receive output formatted the same as the following example output:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-135">You receive output formatted the same as the following example output:</span></span>

```powershell
ResourceType            CurrentValue Limit
------------            ------------ -----
Virtual Networks                   1    50
Network Security Groups            2   100
Public IP Addresses                1    60
Network Interfaces                 1 24000
Network Watchers                   1     1
```

## <a name="azure-cli"></a><span data-ttu-id="0e4e4-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0e4e4-136">Azure CLI</span></span>

<span data-ttu-id="0e4e4-137">If using Azure Command-line interface (CLI) commands to complete tasks in this article, either run the commands in the [Azure Cloud Shell](https://shell.azure.com/bash), or by running the CLI from your computer.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-137">If using Azure Command-line interface (CLI) commands to complete tasks in this article, either run the commands in the [Azure Cloud Shell](https://shell.azure.com/bash), or by running the CLI from your computer.</span></span> <span data-ttu-id="0e4e4-138">This article requires the Azure CLI version 2.0.32 or later.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-138">This article requires the Azure CLI version 2.0.32 or later.</span></span> <span data-ttu-id="0e4e4-139">Run `az --version` to find the installed version.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-139">Run `az --version` to find the installed version.</span></span> <span data-ttu-id="0e4e4-140">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-140">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="0e4e4-141">If you're running the Azure CLI locally, you also need to run `az login` to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-141">If you're running the Azure CLI locally, you also need to run `az login` to log in to Azure.</span></span>

<span data-ttu-id="0e4e4-142">View your usage against limits with [az network list-usages](/cli/azure/network?view=azure-cli-latest#az-network-list-usages).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-142">View your usage against limits with [az network list-usages](/cli/azure/network?view=azure-cli-latest#az-network-list-usages).</span></span> <span data-ttu-id="0e4e4-143">The following example gets the usage for resources in the East US location:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-143">The following example gets the usage for resources in the East US location:</span></span>

```azurecli-interactive
az network list-usages \
  --location eastus \
  --out table
```

<span data-ttu-id="0e4e4-144">You receive output formatted the same as the following example output:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-144">You receive output formatted the same as the following example output:</span></span>

```azurecli
Name                    CurrentValue Limit
------------            ------------ -----
Virtual Networks                   1    50
Network Security Groups            2   100
Public IP Addresses                1    60
Network Interfaces                 1 24000
Network Watchers                   1     1
Load Balancers                     0   100
Application Gateways               0    50
```
