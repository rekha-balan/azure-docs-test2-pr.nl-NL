---
title: Azure DocumentDB Automation - Management with Powershell | Microsoft Docs
description: Use Azure Powershell manage your DocumentDB database accounts. DocumentDB is a cloud-based NoSQL database for JSON data.
services: documentdb
author: dmakwana
manager: jhubbard
editor: ''
tags: azure-resource-manager
documentationcenter: ''
ms.assetid: ''
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: dimakwan
ms.openlocfilehash: 1d7691fd5248691f42ad31224f2fff9f7f0d4b9e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564506"
---
# <a name="automate-azure-documentdb-account-management-using-azure-powershell"></a><span data-ttu-id="03851-104">Automate Azure DocumentDB account management using Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="03851-104">Automate Azure DocumentDB account management using Azure Powershell</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](documentdb-create-account.md)
> * [Azure CLI 1.0](documentdb-automation-resource-manager-cli-nodejs.md)
> * [Azure CLI 2.0](documentdb-automation-resource-manager-cli.md)
> * [Azure PowerShell](documentdb-manage-account-with-powershell.md)

<span data-ttu-id="03851-109">The following guide describes commands to automate management of your DocumentDB database accounts using Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="03851-109">The following guide describes commands to automate management of your DocumentDB database accounts using Azure Powershell.</span></span> <span data-ttu-id="03851-110">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="03851-110">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="03851-111">Updating your database account allows you to modify consistency policies and add/remove regions.</span><span class="sxs-lookup"><span data-stu-id="03851-111">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="03851-112">For cross-platform management of your DocumentDB database account, you can use either [Azure CLI](documentdb-automation-resource-manager-cli.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](documentdb-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="03851-112">For cross-platform management of your DocumentDB database account, you can use either [Azure CLI](documentdb-automation-resource-manager-cli.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](documentdb-create-account.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="03851-113">Getting Started</span><span class="sxs-lookup"><span data-stu-id="03851-113">Getting Started</span></span>

<span data-ttu-id="03851-114">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and login to your Azure Resource Manager account in Powershell.</span><span class="sxs-lookup"><span data-stu-id="03851-114">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and login to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="03851-115">Notes</span><span class="sxs-lookup"><span data-stu-id="03851-115">Notes</span></span>

* <span data-ttu-id="03851-116">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span><span class="sxs-lookup"><span data-stu-id="03851-116">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="03851-117">All the following commands are synchronous.</span><span class="sxs-lookup"><span data-stu-id="03851-117">All the following commands are synchronous.</span></span>

## <a id="create-documentdb-account-powershell"></a> <span data-ttu-id="03851-118">Create a DocumentDB Database Account</span><span class="sxs-lookup"><span data-stu-id="03851-118">Create a DocumentDB Database Account</span></span>

<span data-ttu-id="03851-119">This command allows you to create a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-119">This command allows you to create a DocumentDB database account.</span></span> <span data-ttu-id="03851-120">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](documentdb-consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="03851-120">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](documentdb-consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $DocumentDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -PropertyObject $DocumentDBProperties
    
* <span data-ttu-id="03851-121">`<write-region-location>` The location name of the write region of the database account.</span><span class="sxs-lookup"><span data-stu-id="03851-121">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="03851-122">This location is required to have a failover priority value of 0.</span><span class="sxs-lookup"><span data-stu-id="03851-122">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="03851-123">There must be exactly one write region per database account.</span><span class="sxs-lookup"><span data-stu-id="03851-123">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="03851-124">`<read-region-location>` The location name of the read region of the database account.</span><span class="sxs-lookup"><span data-stu-id="03851-124">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="03851-125">This location is required to have a failover priority value of greater than 0.</span><span class="sxs-lookup"><span data-stu-id="03851-125">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="03851-126">There can be more than one read regions per database account.</span><span class="sxs-lookup"><span data-stu-id="03851-126">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="03851-127">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="03851-127">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="03851-128">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="03851-128">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="03851-129">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="03851-129">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span></span>
* <span data-ttu-id="03851-130">`<default-consistency-level>` The default consistency level of the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="03851-130">`<default-consistency-level>` The default consistency level of the DocumentDB account.</span></span> <span data-ttu-id="03851-131">For more information, see [Consistency Levels in DocumentDB](documentdb-consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="03851-131">For more information, see [Consistency Levels in DocumentDB](documentdb-consistency-levels.md).</span></span>
* <span data-ttu-id="03851-132">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span><span class="sxs-lookup"><span data-stu-id="03851-132">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="03851-133">Accepted range for this value is 1 - 100.</span><span class="sxs-lookup"><span data-stu-id="03851-133">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="03851-134">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span><span class="sxs-lookup"><span data-stu-id="03851-134">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="03851-135">Accepted range for this value is 1 – 2,147,483,647.</span><span class="sxs-lookup"><span data-stu-id="03851-135">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="03851-136">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-136">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-137">`<resource-group-location>` The location of the Azure Resource Group to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-137">`<resource-group-location>` The location of the Azure Resource Group to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-138">`<database-account-name>` The name of the DocumentDB database account to be created.</span><span class="sxs-lookup"><span data-stu-id="03851-138">`<database-account-name>` The name of the DocumentDB database account to be created.</span></span> <span data-ttu-id="03851-139">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="03851-139">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="03851-140">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-140">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $DocumentDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -PropertyObject $DocumentDBProperties

### <a name="notes"></a><span data-ttu-id="03851-141">Notes</span><span class="sxs-lookup"><span data-stu-id="03851-141">Notes</span></span>
* <span data-ttu-id="03851-142">The preceding example creates a database account with two regions.</span><span class="sxs-lookup"><span data-stu-id="03851-142">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="03851-143">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span><span class="sxs-lookup"><span data-stu-id="03851-143">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="03851-144">For more information, see [multi-region database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="03851-144">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="03851-145">The locations must be regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="03851-145">The locations must be regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="03851-146">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="03851-146">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <a id="update-documentdb-account-powershell"></a> <span data-ttu-id="03851-147">Update a DocumentDB Database Account</span><span class="sxs-lookup"><span data-stu-id="03851-147">Update a DocumentDB Database Account</span></span>

<span data-ttu-id="03851-148">This command allows you to update your DocumentDB database account properties.</span><span class="sxs-lookup"><span data-stu-id="03851-148">This command allows you to update your DocumentDB database account properties.</span></span> <span data-ttu-id="03851-149">This includes the consistency policy and the locations which the database account exists in.</span><span class="sxs-lookup"><span data-stu-id="03851-149">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> This command allows you to add and remove regions but does not allow you to modify failover priorities. To modify failover priorities, see [below](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $DocumentDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -PropertyObject $DocumentDBProperties
    
* <span data-ttu-id="03851-152">`<write-region-location>` The location name of the write region of the database account.</span><span class="sxs-lookup"><span data-stu-id="03851-152">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="03851-153">This location is required to have a failover priority value of 0.</span><span class="sxs-lookup"><span data-stu-id="03851-153">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="03851-154">There must be exactly one write region per database account.</span><span class="sxs-lookup"><span data-stu-id="03851-154">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="03851-155">`<read-region-location>` The location name of the read region of the database account.</span><span class="sxs-lookup"><span data-stu-id="03851-155">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="03851-156">This location is required to have a failover priority value of greater than 0.</span><span class="sxs-lookup"><span data-stu-id="03851-156">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="03851-157">There can be more than one read regions per database account.</span><span class="sxs-lookup"><span data-stu-id="03851-157">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="03851-158">`<default-consistency-level>` The default consistency level of the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="03851-158">`<default-consistency-level>` The default consistency level of the DocumentDB account.</span></span> <span data-ttu-id="03851-159">For more information, see [Consistency Levels in DocumentDB](documentdb-consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="03851-159">For more information, see [Consistency Levels in DocumentDB](documentdb-consistency-levels.md).</span></span>
* <span data-ttu-id="03851-160">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="03851-160">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="03851-161">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="03851-161">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="03851-162">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="03851-162">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span></span>
* <span data-ttu-id="03851-163">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span><span class="sxs-lookup"><span data-stu-id="03851-163">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="03851-164">Accepted range for this value is 1 - 100.</span><span class="sxs-lookup"><span data-stu-id="03851-164">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="03851-165">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span><span class="sxs-lookup"><span data-stu-id="03851-165">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="03851-166">Accepted range for this value is 1 – 2,147,483,647.</span><span class="sxs-lookup"><span data-stu-id="03851-166">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="03851-167">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-167">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-168">`<resource-group-location>` The location of the Azure Resource Group to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-168">`<resource-group-location>` The location of the Azure Resource Group to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-169">`<database-account-name>` The name of the DocumentDB database account to be updated.</span><span class="sxs-lookup"><span data-stu-id="03851-169">`<database-account-name>` The name of the DocumentDB database account to be updated.</span></span>

<span data-ttu-id="03851-170">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-170">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $DocumentDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -PropertyObject $DocumentDBProperties

## <a id="delete-documentdb-account-powershell"></a> <span data-ttu-id="03851-171">Delete a DocumentDB Database Account</span><span class="sxs-lookup"><span data-stu-id="03851-171">Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="03851-172">This command allows you to delete an existing DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-172">This command allows you to delete an existing DocumentDB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="03851-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-174">`<database-account-name>` The name of the DocumentDB database account to be deleted.</span><span class="sxs-lookup"><span data-stu-id="03851-174">`<database-account-name>` The name of the DocumentDB database account to be deleted.</span></span>

<span data-ttu-id="03851-175">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-175">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> <span data-ttu-id="03851-176">Get Properties of a DocumentDB Database Account</span><span class="sxs-lookup"><span data-stu-id="03851-176">Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="03851-177">This command allows you to get the properties of an existing DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-177">This command allows you to get the properties of an existing DocumentDB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="03851-178">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-178">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-179">`<database-account-name>` The name of the DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-179">`<database-account-name>` The name of the DocumentDB database account.</span></span>

<span data-ttu-id="03851-180">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-180">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> <span data-ttu-id="03851-181">Update Tags of a DocumentDB Database Account</span><span class="sxs-lookup"><span data-stu-id="03851-181">Update Tags of a DocumentDB Database Account</span></span>

<span data-ttu-id="03851-182">The following example describes how to set [Azure resource tags][azure-resource-tags] for your DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-182">The following example describes how to set [Azure resource tags][azure-resource-tags] for your DocumentDB database account.</span></span>

> [!NOTE]
> This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.

<span data-ttu-id="03851-184">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-184">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> <span data-ttu-id="03851-185">List Account Keys</span><span class="sxs-lookup"><span data-stu-id="03851-185">List Account Keys</span></span>

<span data-ttu-id="03851-186">When you create a DocumentDB account, the service generates two master access keys that can be used for authentication when the DocumentDB account is accessed.</span><span class="sxs-lookup"><span data-stu-id="03851-186">When you create a DocumentDB account, the service generates two master access keys that can be used for authentication when the DocumentDB account is accessed.</span></span> <span data-ttu-id="03851-187">By providing two access keys, DocumentDB enables you to regenerate the keys with no interruption to your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="03851-187">By providing two access keys, DocumentDB enables you to regenerate the keys with no interruption to your DocumentDB account.</span></span> <span data-ttu-id="03851-188">Read-only keys for authenticating read-only operations are also available.</span><span class="sxs-lookup"><span data-stu-id="03851-188">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="03851-189">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="03851-189">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="03851-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-191">`<database-account-name>` The name of the DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-191">`<database-account-name>` The name of the DocumentDB database account.</span></span>

<span data-ttu-id="03851-192">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> <span data-ttu-id="03851-193">List Connection Strings</span><span class="sxs-lookup"><span data-stu-id="03851-193">List Connection Strings</span></span>

<span data-ttu-id="03851-194">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span><span class="sxs-lookup"><span data-stu-id="03851-194">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="03851-195">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-195">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-196">`<database-account-name>` The name of the DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-196">`<database-account-name>` The name of the DocumentDB database account.</span></span>

<span data-ttu-id="03851-197">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-197">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> <span data-ttu-id="03851-198">Regenerate Account Key</span><span class="sxs-lookup"><span data-stu-id="03851-198">Regenerate Account Key</span></span>

<span data-ttu-id="03851-199">You should change the access keys to your DocumentDB account periodically to help keep your connections more secure.</span><span class="sxs-lookup"><span data-stu-id="03851-199">You should change the access keys to your DocumentDB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="03851-200">Two access keys are assigned to enable you to maintain connections to the DocumentDB account using one access key while you regenerate the other access key.</span><span class="sxs-lookup"><span data-stu-id="03851-200">Two access keys are assigned to enable you to maintain connections to the DocumentDB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="03851-201">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-201">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-202">`<database-account-name>` The name of the DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-202">`<database-account-name>` The name of the DocumentDB database account.</span></span>
* <span data-ttu-id="03851-203">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span><span class="sxs-lookup"><span data-stu-id="03851-203">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="03851-204">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-204">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> <span data-ttu-id="03851-205">Modify Failover Priority of a DocumentDB Database Account</span><span class="sxs-lookup"><span data-stu-id="03851-205">Modify Failover Priority of a DocumentDB Database Account</span></span>

<span data-ttu-id="03851-206">For multi-region database accounts, you can change the failover priority of the various regions which the DocumentDB database account exists in.</span><span class="sxs-lookup"><span data-stu-id="03851-206">For multi-region database accounts, you can change the failover priority of the various regions which the DocumentDB database account exists in.</span></span> <span data-ttu-id="03851-207">For more information on failover in your DocumentDB database account, see [Distribute data globally with DocumentDB][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="03851-207">For more information on failover in your DocumentDB database account, see [Distribute data globally with DocumentDB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="03851-208">`<write-region-location>` The location name of the write region of the database account.</span><span class="sxs-lookup"><span data-stu-id="03851-208">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="03851-209">This location is required to have a failover priority value of 0.</span><span class="sxs-lookup"><span data-stu-id="03851-209">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="03851-210">There must be exactly one write region per database account.</span><span class="sxs-lookup"><span data-stu-id="03851-210">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="03851-211">`<read-region-location>` The location name of the read region of the database account.</span><span class="sxs-lookup"><span data-stu-id="03851-211">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="03851-212">This location is required to have a failover priority value of greater than 0.</span><span class="sxs-lookup"><span data-stu-id="03851-212">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="03851-213">There can be more than one read regions per database account.</span><span class="sxs-lookup"><span data-stu-id="03851-213">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="03851-214">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="03851-214">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new DocumentDB database account belongs to.</span></span>
* <span data-ttu-id="03851-215">`<database-account-name>` The name of the DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="03851-215">`<database-account-name>` The name of the DocumentDB database account.</span></span>

<span data-ttu-id="03851-216">Example:</span><span class="sxs-lookup"><span data-stu-id="03851-216">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/en-us/azure/powershell-install-configure
[scaling-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally/#scaling-across-the-planet
[distribute-data-globally]: https://docs.microsoft.com/en-us/azure/documentdb/documentdb-distribute-data-globally
[azure-resource-groups]: https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/en-us/rest/api/documentdbresourceprovider/