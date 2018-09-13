---
title: View relative latencies to Azure regions from specific locations | Microsoft Docs
description: Learn how to view relative latencies across Internet providers to Azure regions from specific locations.
services: network-watcher
documentationcenter: ''
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2017
ms.author: jdial
ms.custom: ''
ms.openlocfilehash: a6c2ffa619eeff8b455df8a8b2157525af12c640
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865275"
---
# <a name="view-relative-latency-to-azure-regions-from-specific-locations"></a><span data-ttu-id="a2658-103">View relative latency to Azure regions from specific locations</span><span class="sxs-lookup"><span data-stu-id="a2658-103">View relative latency to Azure regions from specific locations</span></span>

<span data-ttu-id="a2658-104">In this tutorial, learn how to use the Azure [Network Watcher](network-watcher-monitoring-overview.md) service to help you decide what Azure region to deploy your application or service in, based on your user demographic.</span><span class="sxs-lookup"><span data-stu-id="a2658-104">In this tutorial, learn how to use the Azure [Network Watcher](network-watcher-monitoring-overview.md) service to help you decide what Azure region to deploy your application or service in, based on your user demographic.</span></span> <span data-ttu-id="a2658-105">Additionally, you can use it to help evaluate service providers’ connections to Azure.</span><span class="sxs-lookup"><span data-stu-id="a2658-105">Additionally, you can use it to help evaluate service providers’ connections to Azure.</span></span>  
        
## <a name="create-a-network-watcher"></a><span data-ttu-id="a2658-106">Create a network watcher</span><span class="sxs-lookup"><span data-stu-id="a2658-106">Create a network watcher</span></span>

<span data-ttu-id="a2658-107">If you already have a network watcher in at least one Azure [region](https://azure.microsoft.com/regions), you can skip the tasks in this section.</span><span class="sxs-lookup"><span data-stu-id="a2658-107">If you already have a network watcher in at least one Azure [region](https://azure.microsoft.com/regions), you can skip the tasks in this section.</span></span> <span data-ttu-id="a2658-108">Create a resource group for the network watcher.</span><span class="sxs-lookup"><span data-stu-id="a2658-108">Create a resource group for the network watcher.</span></span> <span data-ttu-id="a2658-109">In this example, the resource group is created in the East US region, but you can create the resource group in any Azure region.</span><span class="sxs-lookup"><span data-stu-id="a2658-109">In this example, the resource group is created in the East US region, but you can create the resource group in any Azure region.</span></span>

```powershell
New-AzureRmResourceGroup -Name NetworkWatcherRG -Location eastus
```

<span data-ttu-id="a2658-110">Create a network watcher.</span><span class="sxs-lookup"><span data-stu-id="a2658-110">Create a network watcher.</span></span> <span data-ttu-id="a2658-111">You must have a network watcher created in at least one Azure region.</span><span class="sxs-lookup"><span data-stu-id="a2658-111">You must have a network watcher created in at least one Azure region.</span></span> <span data-ttu-id="a2658-112">In this example, a network watcher is created in the East US Azure region.</span><span class="sxs-lookup"><span data-stu-id="a2658-112">In this example, a network watcher is created in the East US Azure region.</span></span>

```powershell
New-AzureRmNetworkWatcher -Name NetworkWatcher_eastus -ResourceGroupName NetworkWatcherRG -Location eastus
```

## <a name="compare-relative-network-latencies-to-a-single-azure-region-from-a-specific-location"></a><span data-ttu-id="a2658-113">Compare relative network latencies to a single Azure region from a specific location</span><span class="sxs-lookup"><span data-stu-id="a2658-113">Compare relative network latencies to a single Azure region from a specific location</span></span>

<span data-ttu-id="a2658-114">Evaluate service providers, or troubleshoot a user reporting an issue such as “the site was slow,” from a specific location to the azure region where a service is deployed.</span><span class="sxs-lookup"><span data-stu-id="a2658-114">Evaluate service providers, or troubleshoot a user reporting an issue such as “the site was slow,” from a specific location to the azure region where a service is deployed.</span></span> <span data-ttu-id="a2658-115">For example, the following command returns the average relative Internet service provider latencies between the state of Washington in the United States and the West US 2 Azure region between December 13-15, 2017:</span><span class="sxs-lookup"><span data-stu-id="a2658-115">For example, the following command returns the average relative Internet service provider latencies between the state of Washington in the United States and the West US 2 Azure region between December 13-15, 2017:</span></span>

```powershell
Get-AzureRmNetworkWatcherReachabilityReport `
  -NetworkWatcherName NetworkWatcher_eastus `
  -ResourceGroupName NetworkWatcherRG `
  -Location "West US 2" `
  -Country "United States" `
  -State "washington" `
  -StartTime "2017-12-13" `
  -EndTime "2017-12-15"
```

> [!NOTE]
> <span data-ttu-id="a2658-116">The region you specify in the previous command doesn't need to be the same as the region you specified when you retrieved the network watcher.</span><span class="sxs-lookup"><span data-stu-id="a2658-116">The region you specify in the previous command doesn't need to be the same as the region you specified when you retrieved the network watcher.</span></span> <span data-ttu-id="a2658-117">The previous command simply requires that you specify an existing network watcher.</span><span class="sxs-lookup"><span data-stu-id="a2658-117">The previous command simply requires that you specify an existing network watcher.</span></span> <span data-ttu-id="a2658-118">The network watcher can be in any region.</span><span class="sxs-lookup"><span data-stu-id="a2658-118">The network watcher can be in any region.</span></span> <span data-ttu-id="a2658-119">If you specify values for `-Country` and `-State`, they must be valid.</span><span class="sxs-lookup"><span data-stu-id="a2658-119">If you specify values for `-Country` and `-State`, they must be valid.</span></span> <span data-ttu-id="a2658-120">The values are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="a2658-120">The values are case-sensitive.</span></span> <span data-ttu-id="a2658-121">Data is available for a limited number of countries, states, and cities.</span><span class="sxs-lookup"><span data-stu-id="a2658-121">Data is available for a limited number of countries, states, and cities.</span></span> <span data-ttu-id="a2658-122">Run the commands in [View available countries, states, cities, and providers](#view-available) to view a list of available countries, cities, and states to use with the previous command.</span><span class="sxs-lookup"><span data-stu-id="a2658-122">Run the commands in [View available countries, states, cities, and providers](#view-available) to view a list of available countries, cities, and states to use with the previous command.</span></span> 

> [!WARNING]
> <span data-ttu-id="a2658-123">You must specify a date after November 14, 2017 for `-StartTime` and `-EndTime`.</span><span class="sxs-lookup"><span data-stu-id="a2658-123">You must specify a date after November 14, 2017 for `-StartTime` and `-EndTime`.</span></span> <span data-ttu-id="a2658-124">Specifying a date prior to November 14, 2017 returns no data.</span><span class="sxs-lookup"><span data-stu-id="a2658-124">Specifying a date prior to November 14, 2017 returns no data.</span></span> 

<span data-ttu-id="a2658-125">The output from the previous command follows:</span><span class="sxs-lookup"><span data-stu-id="a2658-125">The output from the previous command follows:</span></span>

```powershell
AggregationLevel   : State
ProviderLocation   : {
                       "Country": "United States",
                       "State": "washington"
                     }
ReachabilityReport : [
                       {
                         "Provider": "Qwest Communications Company, LLC - ASN 209",
                         "AzureLocation": "West US 2",
                         "Latencies": [
                           {
                             "TimeStamp": "2017-12-14T00:00:00Z",
                             "Score": 92
                           },
                           {
                             "TimeStamp": "2017-12-13T00:00:00Z",
                             "Score": 92
                           }
                         ]
                       },
                       {
                         "Provider": "Comcast Cable Communications, LLC - ASN 7922",
                         "AzureLocation": "West US 2",
                         "Latencies": [
                           {
                             "TimeStamp": "2017-12-14T00:00:00Z",
                             "Score": 96
                           },
                           {
                             "TimeStamp": "2017-12-13T00:00:00Z",
                             "Score": 96
                           }
                         ]
                       }
                     ]
```

<span data-ttu-id="a2658-126">In the returned output, the value for **Score** is the relative latency across regions and providers.</span><span class="sxs-lookup"><span data-stu-id="a2658-126">In the returned output, the value for **Score** is the relative latency across regions and providers.</span></span> <span data-ttu-id="a2658-127">A score of 1 is the worst (highest) latency, whereas 100 is the lowest latency.</span><span class="sxs-lookup"><span data-stu-id="a2658-127">A score of 1 is the worst (highest) latency, whereas 100 is the lowest latency.</span></span> <span data-ttu-id="a2658-128">The relative latencies are averaged for the day.</span><span class="sxs-lookup"><span data-stu-id="a2658-128">The relative latencies are averaged for the day.</span></span> <span data-ttu-id="a2658-129">In the previous example, while it's clear that the latencies were the same both days and that there is a small difference between the latency of the two providers, it's also clear that the latencies for both providers are low on the 1-100 scale.</span><span class="sxs-lookup"><span data-stu-id="a2658-129">In the previous example, while it's clear that the latencies were the same both days and that there is a small difference between the latency of the two providers, it's also clear that the latencies for both providers are low on the 1-100 scale.</span></span> <span data-ttu-id="a2658-130">While this is expected, since the state of Washington in the United States is physically close to the West US 2 Azure region, sometimes results aren't as expected.</span><span class="sxs-lookup"><span data-stu-id="a2658-130">While this is expected, since the state of Washington in the United States is physically close to the West US 2 Azure region, sometimes results aren't as expected.</span></span> <span data-ttu-id="a2658-131">The larger the date range you specify, the more you can average latency over time.</span><span class="sxs-lookup"><span data-stu-id="a2658-131">The larger the date range you specify, the more you can average latency over time.</span></span>

## <a name="compare-relative-network-latencies-across-azure-regions-from-a-specific-location"></a><span data-ttu-id="a2658-132">Compare relative network latencies across Azure regions from a specific location</span><span class="sxs-lookup"><span data-stu-id="a2658-132">Compare relative network latencies across Azure regions from a specific location</span></span>

<span data-ttu-id="a2658-133">If, instead of specifying the relative latencies between a specific location and a specific Azure region using `-Location`, you wanted to determine the relative latencies to all Azure regions from a specific physical location, you can do that too.</span><span class="sxs-lookup"><span data-stu-id="a2658-133">If, instead of specifying the relative latencies between a specific location and a specific Azure region using `-Location`, you wanted to determine the relative latencies to all Azure regions from a specific physical location, you can do that too.</span></span> <span data-ttu-id="a2658-134">For example, the following command helps you evaluate what azure region to deploy a service in if your primary users are Comcast users located in Washington state:</span><span class="sxs-lookup"><span data-stu-id="a2658-134">For example, the following command helps you evaluate what azure region to deploy a service in if your primary users are Comcast users located in Washington state:</span></span>

```powershell
Get-AzureRmNetworkWatcherReachabilityReport `
  -NetworkWatcherName NetworkWatcher_eastus `
  -ResourceGroupName NetworkWatcherRG `
  -Provider "Comcast Cable Communications, LLC - ASN 7922" `
  -Country "United States" `
  -State "washington" `
  -StartTime "2017-12-13" `
  -EndTime "2017-12-15"
```

>[!NOTE]
<span data-ttu-id="a2658-135">Unlike when you specify a single location, if you don't specify a location, or specify multiple locations, such as "West US2", "West US", you must specify an Internet service provider when running the command.</span><span class="sxs-lookup"><span data-stu-id="a2658-135">Unlike when you specify a single location, if you don't specify a location, or specify multiple locations, such as "West US2", "West US", you must specify an Internet service provider when running the command.</span></span> 

## <a name="view-available"></a><span data-ttu-id="a2658-136">View available countries, states, cities, and providers</span><span class="sxs-lookup"><span data-stu-id="a2658-136">View available countries, states, cities, and providers</span></span>

<span data-ttu-id="a2658-137">Data is available for specific Internet service providers, countries, states, and cities.</span><span class="sxs-lookup"><span data-stu-id="a2658-137">Data is available for specific Internet service providers, countries, states, and cities.</span></span> <span data-ttu-id="a2658-138">To view a list of all available Internet service providers, countries, states, and cities, that you can view data for, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="a2658-138">To view a list of all available Internet service providers, countries, states, and cities, that you can view data for, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkWatcherReachabilityProvidersList -NetworkWatcherName NetworkWatcher_eastus -ResourceGroupName NetworkWatcherRG
```

<span data-ttu-id="a2658-139">Data is only available for the countries, states, and cities returned by the previous command.</span><span class="sxs-lookup"><span data-stu-id="a2658-139">Data is only available for the countries, states, and cities returned by the previous command.</span></span> <span data-ttu-id="a2658-140">The previous command requires you to specify an existing network watcher.</span><span class="sxs-lookup"><span data-stu-id="a2658-140">The previous command requires you to specify an existing network watcher.</span></span> <span data-ttu-id="a2658-141">The example specified the *NetworkWatcher_eastus* network watcher in a resource group named *NetworkWatcherRG*, but you can specify any existing network watcher.</span><span class="sxs-lookup"><span data-stu-id="a2658-141">The example specified the *NetworkWatcher_eastus* network watcher in a resource group named *NetworkWatcherRG*, but you can specify any existing network watcher.</span></span> <span data-ttu-id="a2658-142">If you don't have an existing network watcher, create one by completing the tasks in [Create a network watcher](#create-a-network-watcher).</span><span class="sxs-lookup"><span data-stu-id="a2658-142">If you don't have an existing network watcher, create one by completing the tasks in [Create a network watcher](#create-a-network-watcher).</span></span> 

<span data-ttu-id="a2658-143">After running the previous command, you can filter the output returned by specifying valid values for **Country**, **State**, and **City**, if desired.</span><span class="sxs-lookup"><span data-stu-id="a2658-143">After running the previous command, you can filter the output returned by specifying valid values for **Country**, **State**, and **City**, if desired.</span></span>  <span data-ttu-id="a2658-144">For example, to view the list of Internet service providers available in Seattle, Washington, in the United States, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="a2658-144">For example, to view the list of Internet service providers available in Seattle, Washington, in the United States, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkWatcherReachabilityProvidersList `
  -NetworkWatcherName NetworkWatcher_eastus `
  -ResourceGroupName NetworkWatcherRG `
  -City seattle `
  -Country "United States" `
  -State washington
```

> [!WARNING]
> <span data-ttu-id="a2658-145">The value specified for **Country** must be upper and lowercase.</span><span class="sxs-lookup"><span data-stu-id="a2658-145">The value specified for **Country** must be upper and lowercase.</span></span> <span data-ttu-id="a2658-146">The values specified for **State** and **City** must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="a2658-146">The values specified for **State** and **City** must be lowercase.</span></span> <span data-ttu-id="a2658-147">The values must be listed in the output returned after running the command with no values for **Country**, **State**, and **City**.</span><span class="sxs-lookup"><span data-stu-id="a2658-147">The values must be listed in the output returned after running the command with no values for **Country**, **State**, and **City**.</span></span> <span data-ttu-id="a2658-148">If you specify the incorrect case, or specify a value for **Country**, **State**, or **City** that is not in the output returned after running the command with no values for these properties, the returned output is empty.</span><span class="sxs-lookup"><span data-stu-id="a2658-148">If you specify the incorrect case, or specify a value for **Country**, **State**, or **City** that is not in the output returned after running the command with no values for these properties, the returned output is empty.</span></span>
