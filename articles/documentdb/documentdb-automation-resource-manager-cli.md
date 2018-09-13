---
title: DocumentDB Automation - Azure CLI 2.0 | Microsoft Docs
description: Use Azure CLI 2.0 to manage DocumentDB database accounts. DocumentDB is a cloud-based NoSQL database for JSON data.
services: documentdb
author: dmakwana
manager: jhubbard
editor: ''
tags: azure-resource-manager
documentationcenter: ''
ms.assetid: 6158c27f-6b9a-404e-a234-b5d48c4a5b29
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/04/2017
ms.author: dimakwan
ms.openlocfilehash: 150e8f3e186683bce735d0952adb57544505d1e9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554305"
---
# <a name="automate-azure-documentdb-account-management-using-azure-cli-20"></a><span data-ttu-id="343a6-104">Automate Azure DocumentDB account management using Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="343a6-104">Automate Azure DocumentDB account management using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](documentdb-create-account.md)
> * [Azure CLI 1.0](documentdb-automation-resource-manager-cli-nodejs.md)
> * [Azure CLI 2.0](documentdb-automation-resource-manager-cli.md)
> * [Azure Powershell](documentdb-manage-account-with-powershell.md)

<span data-ttu-id="343a6-109">The following guide describes commands to automate management of your DocumentDB database accounts using the DocumentDB preview commands available in Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="343a6-109">The following guide describes commands to automate management of your DocumentDB database accounts using the DocumentDB preview commands available in Azure CLI 2.0.</span></span> <span data-ttu-id="343a6-110">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="343a6-110">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="343a6-111">Updating your database account enables you to modify consistency policies and add/remove regions.</span><span class="sxs-lookup"><span data-stu-id="343a6-111">Updating your database account enables you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="343a6-112">For cross-platform management of your DocumentDB database account, you can use either [Azure Powershell](documentdb-manage-account-with-powershell.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](documentdb-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="343a6-112">For cross-platform management of your DocumentDB database account, you can use either [Azure Powershell](documentdb-manage-account-with-powershell.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](documentdb-create-account.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="343a6-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="343a6-113">Getting started</span></span>

<span data-ttu-id="343a6-114">Follow the instructions in [How to install and configure Azure CLI 2.0][install-az-cli2] to set up your development environment with Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="343a6-114">Follow the instructions in [How to install and configure Azure CLI 2.0][install-az-cli2] to set up your development environment with Azure CLI 2.0.</span></span>

<span data-ttu-id="343a6-115">Log in to your Azure account by executing the following command and following the on-screen steps.</span><span class="sxs-lookup"><span data-stu-id="343a6-115">Log in to your Azure account by executing the following command and following the on-screen steps.</span></span>

    az login

<span data-ttu-id="343a6-116">If you do not already have an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), create one:</span><span class="sxs-lookup"><span data-stu-id="343a6-116">If you do not already have an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), create one:</span></span>

    az group create --name <resourcegroupname> --location <resourcegrouplocation>
    az group list

<span data-ttu-id="343a6-117">The `<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="343a6-117">The `<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="343a6-118">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="343a6-118">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

### <a name="notes"></a><span data-ttu-id="343a6-119">Notes</span><span class="sxs-lookup"><span data-stu-id="343a6-119">Notes</span></span>

* <span data-ttu-id="343a6-120">Execute 'az documentdb -h' to get a full list of available commands or visit the [reference page][az-documentdb-ref].</span><span class="sxs-lookup"><span data-stu-id="343a6-120">Execute 'az documentdb -h' to get a full list of available commands or visit the [reference page][az-documentdb-ref].</span></span>
* <span data-ttu-id="343a6-121">Execute 'az documentdb <command> -h' to get a list of details of the required and optional parameters per command.</span><span class="sxs-lookup"><span data-stu-id="343a6-121">Execute 'az documentdb <command> -h' to get a list of details of the required and optional parameters per command.</span></span>

## <a id="create-documentdb-account-cli"></a> <span data-ttu-id="343a6-122">Create a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="343a6-122">Create a DocumentDB database account</span></span>

<span data-ttu-id="343a6-123">This command enables you to create a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="343a6-123">This command enables you to create a DocumentDB database account.</span></span> <span data-ttu-id="343a6-124">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](documentdb-consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="343a6-124">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](documentdb-consistency-levels.md).</span></span> 

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
    --default-consistency-level   : Default consistency level of the DocumentDB database account.
                                    Allowed values: BoundedStaleness, Eventual, Session, Strong.
    --ip-range-filter             : Firewall support. Specifies the set of IP addresses or IP
                                    address ranges in CIDR form to be included as the allowed list
                                    of client IPs for a given database account. IP addresses/ranges
                                    must be comma separated and must not contain any spaces.
    --kind                        : The type of DocumentDB database account to create.  Allowed
                                    values: GlobalDocumentDB, MongoDB, Parse.  Default:
                                    GlobalDocumentDB.
    --locations                   : Space separated locations in 'regionName=failoverPriority'
                                    format. E.g "East US"=0 "West US"=1. Failover priority values
                                    are 0 for write regions and greater than 0 for read regions. A
                                    failover priority value must be unique and less than the total
                                    number of regions. Default: single region account in the
                                    location of the specified resource group.
    --max-interval                : When used with Bounded Staleness consistency, this value
                                    represents the time amount of staleness (in seconds) tolerated.
                                    Accepted range for this value is 1 - 100.  Default: 5.
    --max-staleness-prefix        : When used with Bounded Staleness consistency, this value
                                    represents the number of stale requests tolerated. Accepted
                                    range for this value is 1 - 2,147,483,647.  Default: 100.
```

<span data-ttu-id="343a6-125">Examples:</span><span class="sxs-lookup"><span data-stu-id="343a6-125">Examples:</span></span> 

    az documentdb create -g rg-test -n docdb-test
    az documentdb create -g rg-test -n docdb-test --kind MongoDB
    az documentdb create -g rg-test -n docdb-test --locations "East US"=0 "West US"=1 "South Central US"=2
    az documentdb create -g rg-test -n docdb-test --ip-range-filter "13.91.6.132,13.91.6.1/24"
    az documentdb create -g rg-test -n docdb-test --locations "East US"=0 "West US"=1 --default-consistency-level BoundedStaleness --max-interval 10 --max-staleness-prefix 200

### <a name="notes"></a><span data-ttu-id="343a6-126">Notes</span><span class="sxs-lookup"><span data-stu-id="343a6-126">Notes</span></span>
* <span data-ttu-id="343a6-127">The locations must be regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="343a6-127">The locations must be regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="343a6-128">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="343a6-128">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>
* <span data-ttu-id="343a6-129">To enable portal access, include the IP address for the Azure portal for your region in the ip-range-filter, as specified in [Configuring the IP access control policy](documentdb-firewall-support.md#configure-ip-policy).</span><span class="sxs-lookup"><span data-stu-id="343a6-129">To enable portal access, include the IP address for the Azure portal for your region in the ip-range-filter, as specified in [Configuring the IP access control policy](documentdb-firewall-support.md#configure-ip-policy).</span></span>

## <a id="update-documentdb-account-cli"></a> <span data-ttu-id="343a6-130">Update a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="343a6-130">Update a DocumentDB database account</span></span>

<span data-ttu-id="343a6-131">This command enables you to update your DocumentDB database account properties.</span><span class="sxs-lookup"><span data-stu-id="343a6-131">This command enables you to update your DocumentDB database account properties.</span></span> <span data-ttu-id="343a6-132">This includes the consistency policy and the locations which the database account exists in.</span><span class="sxs-lookup"><span data-stu-id="343a6-132">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> This command enables you to add and remove regions but does not allow you to modify failover priorities. To modify failover priorities, see [below](#modify-failover-priority-powershell).

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
    --default-consistency-level   : Default consistency level of the DocumentDB database account.
                                    Allowed values: BoundedStaleness, Eventual, Session, Strong.
    --ip-range-filter             : Firewall support. Specifies the set of IP addresses or IP address
                                    ranges in CIDR form to be included as the allowed list of client
                                    IPs for a given database account. IP addresses/ranges must be comma
                                    separated and must not contain any spaces.
    --locations                   : Space separated locations in 'regionName=failoverPriority' format.
                                    E.g "East US"=0. Failover priority values are 0 for write regions
                                    and greater than 0 for read regions. A failover priority value must
                                    be unique and less than the total number of regions.
    --max-interval                : When used with Bounded Staleness consistency, this value represents
                                    the time amount of staleness (in seconds) tolerated. Accepted range
                                    for this value is 1 - 100.
    --max-staleness-prefix        : When used with Bounded Staleness consistency, this value represents
                                    the number of stale requests tolerated. Accepted range for this
                                    value is 1 - 2,147,483,647.
```

<span data-ttu-id="343a6-135">Examples:</span><span class="sxs-lookup"><span data-stu-id="343a6-135">Examples:</span></span> 

    az documentdb update -g rg-test -n docdb-test --locations "East US"=0 "West US"=1 "South Central US"=2
    az documentdb update -g rg-test -n docdb-test --ip-range-filter "13.91.6.132,13.91.6.1/24"
    az documentdb update -g rg-test -n docdb-test --default-consistency-level BoundedStaleness --max-interval 10 --max-staleness-prefix 200

## <a id="add-remove-region-documentdb-account-cli"></a> <span data-ttu-id="343a6-136">Add/remove region from a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="343a6-136">Add/remove region from a DocumentDB database account</span></span>

<span data-ttu-id="343a6-137">To add or remove region(s) from your existing DocumentDB database account, use the [update](#update-documentdb-account-cli) command with the `--locations` flag.</span><span class="sxs-lookup"><span data-stu-id="343a6-137">To add or remove region(s) from your existing DocumentDB database account, use the [update](#update-documentdb-account-cli) command with the `--locations` flag.</span></span> <span data-ttu-id="343a6-138">The example below shows how to create a new account and subsequently add and remove regions from that account.</span><span class="sxs-lookup"><span data-stu-id="343a6-138">The example below shows how to create a new account and subsequently add and remove regions from that account.</span></span>

<span data-ttu-id="343a6-139">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-139">Example:</span></span>

    az documentdb create -g rg-test -n docdb-test --locations "East US"=0 "West US"=1
    az documentdb update -g rg-test -n docdb-test --locations "East US"=0 "North Europe"=1 "South Central US"=2


## <a id="delete-documentdb-account-cli"></a> <span data-ttu-id="343a6-140">Delete a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="343a6-140">Delete a DocumentDB database account</span></span>

<span data-ttu-id="343a6-141">This command enables you to delete an existing DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="343a6-141">This command enables you to delete an existing DocumentDB database account.</span></span>

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
```

<span data-ttu-id="343a6-142">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-142">Example:</span></span>

    az documentdb delete -g rg-test -n docdb-test

## <a id="get-documentdb-properties-cli"></a> <span data-ttu-id="343a6-143">Get properties of a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="343a6-143">Get properties of a DocumentDB database account</span></span>

<span data-ttu-id="343a6-144">This command enables you to get the properties of an existing DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="343a6-144">This command enables you to get the properties of an existing DocumentDB database account.</span></span>

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
```

<span data-ttu-id="343a6-145">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-145">Example:</span></span>

    az documentdb show -g rg-test -n docdb-test

## <a id="list-account-keys-cli"></a> <span data-ttu-id="343a6-146">List account keys</span><span class="sxs-lookup"><span data-stu-id="343a6-146">List account keys</span></span>

<span data-ttu-id="343a6-147">When you create a DocumentDB account, the service generates two master access keys that can be used for authentication when the DocumentDB account is accessed.</span><span class="sxs-lookup"><span data-stu-id="343a6-147">When you create a DocumentDB account, the service generates two master access keys that can be used for authentication when the DocumentDB account is accessed.</span></span> <span data-ttu-id="343a6-148">By providing two access keys, DocumentDB enables you to regenerate the keys with no interruption to your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="343a6-148">By providing two access keys, DocumentDB enables you to regenerate the keys with no interruption to your DocumentDB account.</span></span> <span data-ttu-id="343a6-149">Read-only keys for authenticating read-only operations are also available.</span><span class="sxs-lookup"><span data-stu-id="343a6-149">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="343a6-150">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="343a6-150">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
```

<span data-ttu-id="343a6-151">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-151">Example:</span></span>

    az documentdb list-keys -g rg-test -n docdb-test

## <a id="list-connection-strings-cli"></a> <span data-ttu-id="343a6-152">List connection strings</span><span class="sxs-lookup"><span data-stu-id="343a6-152">List connection strings</span></span>

<span data-ttu-id="343a6-153">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span><span class="sxs-lookup"><span data-stu-id="343a6-153">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
```

<span data-ttu-id="343a6-154">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-154">Example:</span></span>

    az documentdb list-connection-strings -g rg-test -n docdb-test

## <a id="regenerate-account-key-cli"></a> <span data-ttu-id="343a6-155">Regenerate account key</span><span class="sxs-lookup"><span data-stu-id="343a6-155">Regenerate account key</span></span>

<span data-ttu-id="343a6-156">You should change the access keys to your DocumentDB account periodically to help keep your connections more secure.</span><span class="sxs-lookup"><span data-stu-id="343a6-156">You should change the access keys to your DocumentDB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="343a6-157">Two access keys are assigned to enable you to maintain connections to the DocumentDB account using one access key while you regenerate the other access key.</span><span class="sxs-lookup"><span data-stu-id="343a6-157">Two access keys are assigned to enable you to maintain connections to the DocumentDB account using one access key while you regenerate the other access key.</span></span>

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
    --key-kind          [Required]: The access key to regenerate.  Allowed values: primary, primaryReadonly,
                                    secondary, secondaryReadonly.
```

<span data-ttu-id="343a6-158">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-158">Example:</span></span>

    az documentdb regenerate-key -g rg-test -n docdb-test --key-kind secondary

## <a id="modify-failover-priority-cli"></a> <span data-ttu-id="343a6-159">Modify failover priority of a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="343a6-159">Modify failover priority of a DocumentDB database account</span></span>

<span data-ttu-id="343a6-160">For multi-region database accounts, you can change the failover priority of the various regions which the DocumentDB database account exists in.</span><span class="sxs-lookup"><span data-stu-id="343a6-160">For multi-region database accounts, you can change the failover priority of the various regions which the DocumentDB database account exists in.</span></span> <span data-ttu-id="343a6-161">For more information on failover in your DocumentDB database account, see [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="343a6-161">For more information on failover in your DocumentDB database account, see [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md).</span></span>

```
Arguments
    --name -n           [Required]: Name of the DocumentDB database account.
    --resource-group -g [Required]: Name of the resource group.
    --failover-policies [Required]: Space separated failover policies in 'regionName=failoverPriority' format.
                                    E.g "East US"=0 "West US"=1.
```

<span data-ttu-id="343a6-162">Example:</span><span class="sxs-lookup"><span data-stu-id="343a6-162">Example:</span></span>

    az documentdb failover-priority-change "East US"=1 "West US"=0 "South Central US"=2

## <a name="next-steps"></a><span data-ttu-id="343a6-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="343a6-163">Next steps</span></span>
<span data-ttu-id="343a6-164">Now that you have a DocumentDB account, the next step is to create a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="343a6-164">Now that you have a DocumentDB account, the next step is to create a DocumentDB database.</span></span> <span data-ttu-id="343a6-165">You can create a database by using one of the following:</span><span class="sxs-lookup"><span data-stu-id="343a6-165">You can create a database by using one of the following:</span></span>

* <span data-ttu-id="343a6-166">The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="343a6-166">The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).</span></span>
* <span data-ttu-id="343a6-167">The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="343a6-167">The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.</span></span>
* <span data-ttu-id="343a6-168">The [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="343a6-168">The [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="343a6-169">DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs.</span><span class="sxs-lookup"><span data-stu-id="343a6-169">DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs.</span></span>

<span data-ttu-id="343a6-170">After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections.</span><span class="sxs-lookup"><span data-stu-id="343a6-170">After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections.</span></span>


<span data-ttu-id="343a6-171">After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span><span class="sxs-lookup"><span data-stu-id="343a6-171">After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span></span>

<span data-ttu-id="343a6-172">To learn more about DocumentDB, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="343a6-172">To learn more about DocumentDB, explore these resources:</span></span>

* [<span data-ttu-id="343a6-173">Learning path for DocumentDB</span><span class="sxs-lookup"><span data-stu-id="343a6-173">Learning path for DocumentDB</span></span>](https://azure.microsoft.com/documentation/learning-paths/documentdb/)
* [<span data-ttu-id="343a6-174">DocumentDB resource model and concepts</span><span class="sxs-lookup"><span data-stu-id="343a6-174">DocumentDB resource model and concepts</span></span>](documentdb-resources.md)


<!--Reference style links - using these makes the source content way more readable than using inline links-->
[scaling-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally/#scaling-across-the-planet
[install-az-cli2]: https://docs.microsoft.com/en-us/cli/azure/install-az-cli2
[az-documentdb-ref]: https://docs.microsoft.com/en-us/cli/azure/documentdb
[az-documentdb-create-ref]: https://docs.microsoft.com/en-us/cli/azure/documentdb#create
[rp-rest-api]: https://docs.microsoft.com/en-us/rest/api/documentdbresourceprovider/
