---
title: Azure Cosmos DB Automation - Management with Powershell | Microsoft Docs
description: Use Azure Powershell manage your Azure Cosmos DB accounts.
services: cosmos-db
author: dmakwana
manager: kfile
editor: ''
tags: azure-resource-manager
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 90de671d8e57244765f1da439649e57485814533
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969402"
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="74f35-103">Create an Azure Cosmos DB account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f35-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="74f35-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="74f35-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="74f35-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="74f35-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="74f35-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span><span class="sxs-lookup"><span data-stu-id="74f35-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="74f35-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-sql-api-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="74f35-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-sql-api-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="74f35-108">Getting Started</span><span class="sxs-lookup"><span data-stu-id="74f35-108">Getting Started</span></span>

<span data-ttu-id="74f35-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span><span class="sxs-lookup"><span data-stu-id="74f35-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="74f35-110">Notes</span><span class="sxs-lookup"><span data-stu-id="74f35-110">Notes</span></span>

* <span data-ttu-id="74f35-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span><span class="sxs-lookup"><span data-stu-id="74f35-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="74f35-112">All the following commands are synchronous.</span><span class="sxs-lookup"><span data-stu-id="74f35-112">All the following commands are synchronous.</span></span>

## <a id="create-documentdb-account-powershell"></a> <span data-ttu-id="74f35-113">Create an Azure Cosmos DB Account</span><span class="sxs-lookup"><span data-stu-id="74f35-113">Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="74f35-114">This command allows you to create an Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="74f35-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="74f35-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="74f35-116">`<write-region-location>` The location name of the write region of the database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="74f35-117">This location is required to have a failover priority value of 0.</span><span class="sxs-lookup"><span data-stu-id="74f35-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="74f35-118">There must be exactly one write region per database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="74f35-119">`<read-region-location>` The location name of the read region of the database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="74f35-120">This location is required to have a failover priority value of greater than 0.</span><span class="sxs-lookup"><span data-stu-id="74f35-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="74f35-121">There can be more than one read regions per database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="74f35-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="74f35-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="74f35-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="74f35-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="74f35-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="74f35-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="74f35-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="74f35-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="74f35-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="74f35-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span><span class="sxs-lookup"><span data-stu-id="74f35-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="74f35-128">Accepted range for this value is 1 - 100.</span><span class="sxs-lookup"><span data-stu-id="74f35-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="74f35-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span><span class="sxs-lookup"><span data-stu-id="74f35-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="74f35-130">Accepted range for this value is 1 – 2,147,483,647.</span><span class="sxs-lookup"><span data-stu-id="74f35-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="74f35-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span><span class="sxs-lookup"><span data-stu-id="74f35-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="74f35-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="74f35-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="74f35-135">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="74f35-136">Notes</span><span class="sxs-lookup"><span data-stu-id="74f35-136">Notes</span></span>
* <span data-ttu-id="74f35-137">The preceding example creates a database account with two regions.</span><span class="sxs-lookup"><span data-stu-id="74f35-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="74f35-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span><span class="sxs-lookup"><span data-stu-id="74f35-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="74f35-139">For more information, see [multi-region database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="74f35-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="74f35-140">The locations must be regions in which Azure Cosmos DB is generally available.</span><span class="sxs-lookup"><span data-stu-id="74f35-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="74f35-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="74f35-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <a id="update-documentdb-account-powershell"></a> <span data-ttu-id="74f35-142">Update an Azure Cosmos DB database account</span><span class="sxs-lookup"><span data-stu-id="74f35-142">Update an Azure Cosmos DB database account</span></span>

<span data-ttu-id="74f35-143">This command allows you to update your Azure Cosmos DB database account properties.</span><span class="sxs-lookup"><span data-stu-id="74f35-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="74f35-144">This includes the consistency policy and the locations which the database account exists in.</span><span class="sxs-lookup"><span data-stu-id="74f35-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="74f35-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span><span class="sxs-lookup"><span data-stu-id="74f35-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="74f35-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="74f35-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="74f35-147">`<write-region-location>` The location name of the write region of the database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="74f35-148">This location is required to have a failover priority value of 0.</span><span class="sxs-lookup"><span data-stu-id="74f35-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="74f35-149">There must be exactly one write region per database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="74f35-150">`<read-region-location>` The location name of the read region of the database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="74f35-151">This location is required to have a failover priority value of greater than 0.</span><span class="sxs-lookup"><span data-stu-id="74f35-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="74f35-152">There can be more than one read regions per database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="74f35-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="74f35-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="74f35-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="74f35-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="74f35-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="74f35-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="74f35-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="74f35-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="74f35-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="74f35-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span><span class="sxs-lookup"><span data-stu-id="74f35-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="74f35-159">Accepted range for this value is 1 - 100.</span><span class="sxs-lookup"><span data-stu-id="74f35-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="74f35-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span><span class="sxs-lookup"><span data-stu-id="74f35-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="74f35-161">Accepted range for this value is 1 – 2,147,483,647.</span><span class="sxs-lookup"><span data-stu-id="74f35-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="74f35-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span><span class="sxs-lookup"><span data-stu-id="74f35-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="74f35-165">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> <span data-ttu-id="74f35-166">Delete an Azure Cosmos DB database account</span><span class="sxs-lookup"><span data-stu-id="74f35-166">Delete an Azure Cosmos DB database account</span></span>

<span data-ttu-id="74f35-167">This command allows you to delete an existing Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="74f35-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span><span class="sxs-lookup"><span data-stu-id="74f35-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="74f35-170">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> <span data-ttu-id="74f35-171">Get properties of an Azure Cosmos DB database account</span><span class="sxs-lookup"><span data-stu-id="74f35-171">Get properties of an Azure Cosmos DB database account</span></span>

<span data-ttu-id="74f35-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="74f35-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="74f35-175">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> <span data-ttu-id="74f35-176">Update Tags of an Azure Cosmos DB Database Account</span><span class="sxs-lookup"><span data-stu-id="74f35-176">Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="74f35-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="74f35-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span><span class="sxs-lookup"><span data-stu-id="74f35-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="74f35-179">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-179">Example:</span></span>

    $tags = @{"dept" = "Finance"; environment = "Production"}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDB/databaseAccounts"  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> <span data-ttu-id="74f35-180">List Account Keys</span><span class="sxs-lookup"><span data-stu-id="74f35-180">List Account Keys</span></span>

<span data-ttu-id="74f35-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span><span class="sxs-lookup"><span data-stu-id="74f35-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="74f35-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="74f35-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="74f35-183">Read-only keys for authenticating read-only operations are also available.</span><span class="sxs-lookup"><span data-stu-id="74f35-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="74f35-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="74f35-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="74f35-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="74f35-187">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> <span data-ttu-id="74f35-188">List Connection Strings</span><span class="sxs-lookup"><span data-stu-id="74f35-188">List Connection Strings</span></span>

<span data-ttu-id="74f35-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span><span class="sxs-lookup"><span data-stu-id="74f35-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="74f35-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="74f35-192">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> <span data-ttu-id="74f35-193">Regenerate Account Key</span><span class="sxs-lookup"><span data-stu-id="74f35-193">Regenerate Account Key</span></span>

<span data-ttu-id="74f35-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span><span class="sxs-lookup"><span data-stu-id="74f35-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="74f35-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span><span class="sxs-lookup"><span data-stu-id="74f35-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="74f35-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="74f35-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span><span class="sxs-lookup"><span data-stu-id="74f35-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="74f35-199">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> <span data-ttu-id="74f35-200">Modify Failover Priority of an Azure Cosmos DB Database Account</span><span class="sxs-lookup"><span data-stu-id="74f35-200">Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="74f35-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span><span class="sxs-lookup"><span data-stu-id="74f35-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="74f35-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="74f35-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="74f35-203">`<write-region-location>` The location name of the write region of the database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="74f35-204">This location is required to have a failover priority value of 0.</span><span class="sxs-lookup"><span data-stu-id="74f35-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="74f35-205">There must be exactly one write region per database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="74f35-206">`<read-region-location>` The location name of the read region of the database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="74f35-207">This location is required to have a failover priority value of greater than 0.</span><span class="sxs-lookup"><span data-stu-id="74f35-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="74f35-208">There can be more than one read regions per database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="74f35-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span><span class="sxs-lookup"><span data-stu-id="74f35-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="74f35-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="74f35-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="74f35-211">Example:</span><span class="sxs-lookup"><span data-stu-id="74f35-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="74f35-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="74f35-212">Next steps</span></span>

* <span data-ttu-id="74f35-213">To connect using .NET, see [Connect and query with .NET](create-sql-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="74f35-213">To connect using .NET, see [Connect and query with .NET](create-sql-api-dotnet.md).</span></span>
* <span data-ttu-id="74f35-214">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="74f35-214">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/
