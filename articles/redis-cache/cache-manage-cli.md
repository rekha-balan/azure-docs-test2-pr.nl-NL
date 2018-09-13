---
title: Manage Azure Redis Cache using Azure CLI | Microsoft Docs
description: Learn how to install the Azure CLI on any platform, how to use it to connect to your Azure account, and how to create and manage a Redis cache from the Azure CLI.
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540841"
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="ca1d3-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="ca1d3-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure CLI](cache-manage-cli.md)
>
>

<span data-ttu-id="ca1d3-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="ca1d3-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> This article applies to a previous version of Azure CLI. For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ca1d3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ca1d3-110">Prerequisites</span></span>
<span data-ttu-id="ca1d3-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="ca1d3-112">You must have an Azure account.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-112">You must have an Azure account.</span></span> <span data-ttu-id="ca1d3-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="ca1d3-114">[Install the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d3-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="ca1d3-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="ca1d3-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d3-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="ca1d3-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="ca1d3-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d3-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="ca1d3-119">Redis Cache properties</span><span class="sxs-lookup"><span data-stu-id="ca1d3-119">Redis Cache properties</span></span>
<span data-ttu-id="ca1d3-120">The following properties are used when creating and updating Redis Cache instances.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="ca1d3-121">Property</span><span class="sxs-lookup"><span data-stu-id="ca1d3-121">Property</span></span> | <span data-ttu-id="ca1d3-122">Switch</span><span class="sxs-lookup"><span data-stu-id="ca1d3-122">Switch</span></span> | <span data-ttu-id="ca1d3-123">Description</span><span class="sxs-lookup"><span data-stu-id="ca1d3-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca1d3-124">name</span><span class="sxs-lookup"><span data-stu-id="ca1d3-124">name</span></span> |<span data-ttu-id="ca1d3-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="ca1d3-125">-n, --name</span></span> |<span data-ttu-id="ca1d3-126">Name of the Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="ca1d3-127">resource group</span><span class="sxs-lookup"><span data-stu-id="ca1d3-127">resource group</span></span> |<span data-ttu-id="ca1d3-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="ca1d3-128">-g, --resource-group</span></span> |<span data-ttu-id="ca1d3-129">Name of the Resource Group.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="ca1d3-130">location</span><span class="sxs-lookup"><span data-stu-id="ca1d3-130">location</span></span> |<span data-ttu-id="ca1d3-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="ca1d3-131">-l, --location</span></span> |<span data-ttu-id="ca1d3-132">Location to create cache.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-132">Location to create cache.</span></span> |
| <span data-ttu-id="ca1d3-133">size</span><span class="sxs-lookup"><span data-stu-id="ca1d3-133">size</span></span> |<span data-ttu-id="ca1d3-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="ca1d3-134">-z, --size</span></span> |<span data-ttu-id="ca1d3-135">Size of the Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-135">Size of the Redis Cache.</span></span> <span data-ttu-id="ca1d3-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="ca1d3-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="ca1d3-137">sku</span><span class="sxs-lookup"><span data-stu-id="ca1d3-137">sku</span></span> |<span data-ttu-id="ca1d3-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="ca1d3-138">-x, --sku</span></span> |<span data-ttu-id="ca1d3-139">Redis SKU.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-139">Redis SKU.</span></span> <span data-ttu-id="ca1d3-140">Should be one of : [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="ca1d3-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="ca1d3-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="ca1d3-141">EnableNonSslPort</span></span> |<span data-ttu-id="ca1d3-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="ca1d3-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="ca1d3-143">EnableNonSslPort property of the Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="ca1d3-144">Add this flag if you want to enable the Non SSL Port for your cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="ca1d3-145">Redis Configuration</span><span class="sxs-lookup"><span data-stu-id="ca1d3-145">Redis Configuration</span></span> |<span data-ttu-id="ca1d3-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="ca1d3-146">-c, --redis-configuration</span></span> |<span data-ttu-id="ca1d3-147">Redis Configuration.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-147">Redis Configuration.</span></span> <span data-ttu-id="ca1d3-148">Enter a JSON formatted string of configuration keys and values here.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="ca1d3-149">Format:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="ca1d3-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="ca1d3-150">Redis Configuration</span><span class="sxs-lookup"><span data-stu-id="ca1d3-150">Redis Configuration</span></span> |<span data-ttu-id="ca1d3-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="ca1d3-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="ca1d3-152">Redis Configuration.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-152">Redis Configuration.</span></span> <span data-ttu-id="ca1d3-153">Enter the path of a file containing configuration keys and values here.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="ca1d3-154">Format for the file entry: {"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="ca1d3-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="ca1d3-155">Shard Count</span><span class="sxs-lookup"><span data-stu-id="ca1d3-155">Shard Count</span></span> |<span data-ttu-id="ca1d3-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="ca1d3-156">-r, --shard-count</span></span> |<span data-ttu-id="ca1d3-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="ca1d3-158">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="ca1d3-158">Virtual Network</span></span> |<span data-ttu-id="ca1d3-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="ca1d3-159">-v, --virtual-network</span></span> |<span data-ttu-id="ca1d3-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="ca1d3-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="ca1d3-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="ca1d3-162">key type</span><span class="sxs-lookup"><span data-stu-id="ca1d3-162">key type</span></span> |<span data-ttu-id="ca1d3-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="ca1d3-163">-t, --key-type</span></span> |<span data-ttu-id="ca1d3-164">Type of key to renew.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-164">Type of key to renew.</span></span> <span data-ttu-id="ca1d3-165">Valid values: [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="ca1d3-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="ca1d3-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="ca1d3-166">StaticIP</span></span> |<span data-ttu-id="ca1d3-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="ca1d3-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="ca1d3-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="ca1d3-169">If not provided, one is chosen for you from the subnet.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="ca1d3-170">Subnet</span><span class="sxs-lookup"><span data-stu-id="ca1d3-170">Subnet</span></span> |<span data-ttu-id="ca1d3-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="ca1d3-171">t, --subnet <subnet></span></span> |<span data-ttu-id="ca1d3-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="ca1d3-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ca1d3-173">VirtualNetwork</span></span> |<span data-ttu-id="ca1d3-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="ca1d3-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="ca1d3-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="ca1d3-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="ca1d3-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="ca1d3-177">Subscription</span><span class="sxs-lookup"><span data-stu-id="ca1d3-177">Subscription</span></span> |<span data-ttu-id="ca1d3-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="ca1d3-178">-s, --subscription</span></span> |<span data-ttu-id="ca1d3-179">The subscription identifier.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="ca1d3-180">See all Redis Cache commands</span><span class="sxs-lookup"><span data-stu-id="ca1d3-180">See all Redis Cache commands</span></span>
<span data-ttu-id="ca1d3-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="ca1d3-182">Create a Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-182">Create a Redis Cache</span></span>
<span data-ttu-id="ca1d3-183">To create a Redis Cache, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="ca1d3-184">For more information about this command, run the `azure rediscache create -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="ca1d3-185">Delete an existing Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="ca1d3-186">To delete a Redis Cache, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="ca1d3-187">For more information about this command, run the `azure rediscache delete -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="ca1d3-188">List all Redis Caches within your Subscription or Resource Group</span><span class="sxs-lookup"><span data-stu-id="ca1d3-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="ca1d3-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="ca1d3-190">For more information about this command, run the `azure rediscache list -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="ca1d3-191">Show properties of an existing Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="ca1d3-192">To show properties of an existing Redis Cache, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="ca1d3-193">For more information about this command, run the `azure rediscache show -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="ca1d3-194">Change settings of an existing Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="ca1d3-195">To change settings of an existing Redis Cache, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="ca1d3-196">For more information about this command, run the `azure rediscache set -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="ca1d3-197">Renew the authentication key for an existing Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="ca1d3-198">To renew the authentication key for an existing Redis Cache, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="ca1d3-199">Specify `Primary` or `Secondary` for `key-type`.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="ca1d3-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="ca1d3-201">List Primary and Secondary keys of an existing Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ca1d3-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="ca1d3-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ca1d3-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="ca1d3-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span><span class="sxs-lookup"><span data-stu-id="ca1d3-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
