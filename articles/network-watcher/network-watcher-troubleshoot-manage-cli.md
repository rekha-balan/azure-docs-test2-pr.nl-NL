---
title: Troubleshoot Azure Virtual Network Gateway and Connections - Azure CLI | Microsoft Docs
description: This page explains how to use the Azure Network Watcher troubleshoot Azure CLI
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a213c146a9ea1bb6c23bbcbfb6353372f2e4cbfc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549830"
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli"></a><span data-ttu-id="cff76-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cff76-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="cff76-107">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="cff76-107">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="cff76-108">One of these capabilities is resource troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="cff76-108">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="cff76-109">Resource troubleshooting can be called by PowerShell, CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="cff76-109">Resource troubleshooting can be called by PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="cff76-110">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span><span class="sxs-lookup"><span data-stu-id="cff76-110">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="cff76-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="cff76-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="cff76-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="cff76-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cff76-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="cff76-113">Before you begin</span></span>

<span data-ttu-id="cff76-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="cff76-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="overview"></a><span data-ttu-id="cff76-115">Overview</span><span class="sxs-lookup"><span data-stu-id="cff76-115">Overview</span></span>

<span data-ttu-id="cff76-116">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span><span class="sxs-lookup"><span data-stu-id="cff76-116">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="cff76-117">When a request is made to resource troubleshooting, logs are being queried and inspected.</span><span class="sxs-lookup"><span data-stu-id="cff76-117">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="cff76-118">When inspection is complete, the results are returned.</span><span class="sxs-lookup"><span data-stu-id="cff76-118">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="cff76-119">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span><span class="sxs-lookup"><span data-stu-id="cff76-119">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="cff76-120">The logs from troubleshooting are stored in a container on a storage account that is specified.</span><span class="sxs-lookup"><span data-stu-id="cff76-120">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="cff76-121">Retrieve a Virtual Network Gateway Connection</span><span class="sxs-lookup"><span data-stu-id="cff76-121">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="cff76-122">In this example, resource troubleshooting is being ran on a Connection.</span><span class="sxs-lookup"><span data-stu-id="cff76-122">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="cff76-123">You can also pass it a Virtual Network Gateway.</span><span class="sxs-lookup"><span data-stu-id="cff76-123">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="cff76-124">The following cmdlet lists the vpn-connections in a resource group.</span><span class="sxs-lookup"><span data-stu-id="cff76-124">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="cff76-125">You can also run the command to see the connections in a subscription.</span><span class="sxs-lookup"><span data-stu-id="cff76-125">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="cff76-126">Once you have the name of the connection, you can run this command to get its resource Id:</span><span class="sxs-lookup"><span data-stu-id="cff76-126">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="cff76-127">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="cff76-127">Create a storage account</span></span>

<span data-ttu-id="cff76-128">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="cff76-128">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="cff76-129">In this step, we create a storage account, if an existing storage account exists you can use it.</span><span class="sxs-lookup"><span data-stu-id="cff76-129">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="cff76-130">Create the storage account</span><span class="sxs-lookup"><span data-stu-id="cff76-130">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="cff76-131">Get the storage account keys</span><span class="sxs-lookup"><span data-stu-id="cff76-131">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="cff76-132">Create the container</span><span class="sxs-lookup"><span data-stu-id="cff76-132">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --acount-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="cff76-133">Run Network Watcher resource troubleshooting</span><span class="sxs-lookup"><span data-stu-id="cff76-133">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="cff76-134">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cff76-134">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="cff76-135">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span><span class="sxs-lookup"><span data-stu-id="cff76-135">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="cff76-136">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span><span class="sxs-lookup"><span data-stu-id="cff76-136">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="cff76-137">It returns the results to the shell and stores logs of the results in the storage account specified.</span><span class="sxs-lookup"><span data-stu-id="cff76-137">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="cff76-138">Understanding the results</span><span class="sxs-lookup"><span data-stu-id="cff76-138">Understanding the results</span></span>

<span data-ttu-id="cff76-139">The action text provides general guidance on how to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="cff76-139">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="cff76-140">If an action can be taken for the issue, a link is provided with additional guidance.</span><span class="sxs-lookup"><span data-stu-id="cff76-140">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="cff76-141">In the case where there is no additional guidance, the response provides the url to open a support case.</span><span class="sxs-lookup"><span data-stu-id="cff76-141">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="cff76-142">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cff76-142">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="cff76-143">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="cff76-143">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="cff76-144">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="cff76-144">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="cff76-145">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="cff76-145">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cff76-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="cff76-146">Next steps</span></span>

<span data-ttu-id="cff76-147">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span><span class="sxs-lookup"><span data-stu-id="cff76-147">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
