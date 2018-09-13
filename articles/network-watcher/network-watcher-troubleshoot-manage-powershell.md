---
title: Troubleshoot Azure Virtual Network Gateway and Connections - PowerShell | Microsoft Docs
description: This page explains how to use the Azure Network Watcher troubleshoot PowerShell cmdlet
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5c5f5603d6884c14dd796c2bc8014e8503cfd6bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662918"
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="05df7-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span><span class="sxs-lookup"><span data-stu-id="05df7-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="05df7-107">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="05df7-107">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="05df7-108">One of these capabilities is resource troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="05df7-108">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="05df7-109">Resource troubleshooting can be called by PowerShell, CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="05df7-109">Resource troubleshooting can be called by PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="05df7-110">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span><span class="sxs-lookup"><span data-stu-id="05df7-110">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="05df7-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="05df7-111">Before you begin</span></span>

<span data-ttu-id="05df7-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="05df7-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="overview"></a><span data-ttu-id="05df7-113">Overview</span><span class="sxs-lookup"><span data-stu-id="05df7-113">Overview</span></span>

<span data-ttu-id="05df7-114">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span><span class="sxs-lookup"><span data-stu-id="05df7-114">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="05df7-115">When a request is made to resource troubleshooting, logs are being queried and inspected.</span><span class="sxs-lookup"><span data-stu-id="05df7-115">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="05df7-116">When inspection is complete, the results are returned.</span><span class="sxs-lookup"><span data-stu-id="05df7-116">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="05df7-117">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span><span class="sxs-lookup"><span data-stu-id="05df7-117">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="05df7-118">The logs from troubleshooting are stored in a container on a storage account that is specified.</span><span class="sxs-lookup"><span data-stu-id="05df7-118">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="05df7-119">Retrieve Network Watcher</span><span class="sxs-lookup"><span data-stu-id="05df7-119">Retrieve Network Watcher</span></span>

<span data-ttu-id="05df7-120">The first step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="05df7-120">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="05df7-121">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span><span class="sxs-lookup"><span data-stu-id="05df7-121">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="05df7-122">Retrieve a Virtual Network Gateway Connection</span><span class="sxs-lookup"><span data-stu-id="05df7-122">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="05df7-123">In this example, resource troubleshooting is being ran on a Connection.</span><span class="sxs-lookup"><span data-stu-id="05df7-123">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="05df7-124">You can also pass it a Virtual Network Gateway.</span><span class="sxs-lookup"><span data-stu-id="05df7-124">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="05df7-125">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="05df7-125">Create a storage account</span></span>

<span data-ttu-id="05df7-126">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="05df7-126">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="05df7-127">In this step, we create a storage account, if an existing storage account exists you can use it.</span><span class="sxs-lookup"><span data-stu-id="05df7-127">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="05df7-128">Run Network Watcher resource troubleshooting</span><span class="sxs-lookup"><span data-stu-id="05df7-128">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="05df7-129">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05df7-129">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="05df7-130">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span><span class="sxs-lookup"><span data-stu-id="05df7-130">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="05df7-132">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span><span class="sxs-lookup"><span data-stu-id="05df7-132">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="05df7-133">It returns the results to the shell and stores logs of the results in the storage account specified.</span><span class="sxs-lookup"><span data-stu-id="05df7-133">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="05df7-134">Understanding the results</span><span class="sxs-lookup"><span data-stu-id="05df7-134">Understanding the results</span></span>

<span data-ttu-id="05df7-135">The action text provides general guidance on how to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="05df7-135">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="05df7-136">If an action can be taken for the issue, a link is provided with additional guidance.</span><span class="sxs-lookup"><span data-stu-id="05df7-136">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="05df7-137">In the case where there is no additional guidance, the response provides the url to open a support case.</span><span class="sxs-lookup"><span data-stu-id="05df7-137">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="05df7-138">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="05df7-138">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="05df7-139">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="05df7-139">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="05df7-140">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="05df7-140">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="05df7-141">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="05df7-141">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="05df7-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="05df7-142">Next steps</span></span>

<span data-ttu-id="05df7-143">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span><span class="sxs-lookup"><span data-stu-id="05df7-143">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
