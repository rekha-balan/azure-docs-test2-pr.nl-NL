---
title: Developing with multiple regions in DocumentDB | Microsoft Docs
description: Learn how to access your data in multiple regions from Azure DocumentDB, a fully managed NoSQL database service.
services: documentdb
documentationcenter: ''
author: mimig1
manager: jhubbard
editor: ''
ms.assetid: d4579378-0b3a-44a5-9f5b-630f1fa4c66d
ms.service: documentdb
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/09/2017
ms.author: mimig
ms.openlocfilehash: 0322e6881066d33856c3a65fa37d7d01e271e6d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563610"
---
# <a name="developing-with-multi-region-documentdb-accounts"></a><span data-ttu-id="6eee9-103">Developing with multi-region DocumentDB accounts</span><span class="sxs-lookup"><span data-stu-id="6eee9-103">Developing with multi-region DocumentDB accounts</span></span>

<span data-ttu-id="6eee9-104">Learn about multi-region DocumentDB accounts in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span><span class="sxs-lookup"><span data-stu-id="6eee9-104">Learn about multi-region DocumentDB accounts in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a name="introduction"></a><span data-ttu-id="6eee9-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="6eee9-105">Introduction</span></span>

<span data-ttu-id="6eee9-106">In order to take advantage of [global distribution](documentdb-distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span><span class="sxs-lookup"><span data-stu-id="6eee9-106">In order to take advantage of [global distribution](documentdb-distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="6eee9-107">This can be done by setting the connection policy.</span><span class="sxs-lookup"><span data-stu-id="6eee9-107">This can be done by setting the connection policy.</span></span> <span data-ttu-id="6eee9-108">Based on the Azure DocumentDB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span><span class="sxs-lookup"><span data-stu-id="6eee9-108">Based on the Azure DocumentDB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span></span>

<span data-ttu-id="6eee9-109">This preference list is specified when initializing a connection using the DocumentDB client SDKs.</span><span class="sxs-lookup"><span data-stu-id="6eee9-109">This preference list is specified when initializing a connection using the DocumentDB client SDKs.</span></span> <span data-ttu-id="6eee9-110">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span><span class="sxs-lookup"><span data-stu-id="6eee9-110">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="6eee9-111">The SDK will automatically send all writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="6eee9-111">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="6eee9-112">All reads will be sent to the first available region in the PreferredLocations list.</span><span class="sxs-lookup"><span data-stu-id="6eee9-112">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="6eee9-113">If the request fails, the client will fail down the list to the next region, and so on.</span><span class="sxs-lookup"><span data-stu-id="6eee9-113">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="6eee9-114">The client SDKs will only attempt to read from the regions specified in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="6eee9-114">The client SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="6eee9-115">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span><span class="sxs-lookup"><span data-stu-id="6eee9-115">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="6eee9-116">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span><span class="sxs-lookup"><span data-stu-id="6eee9-116">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="6eee9-117">If the PreferredLocations property is not set, all requests will be served from the current write region.</span><span class="sxs-lookup"><span data-stu-id="6eee9-117">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="6eee9-118">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="6eee9-118">.NET SDK</span></span>
<span data-ttu-id="6eee9-119">The SDK can be used without any code changes.</span><span class="sxs-lookup"><span data-stu-id="6eee9-119">The SDK can be used without any code changes.</span></span> <span data-ttu-id="6eee9-120">In this case, the SDK automatically directs both reads and writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="6eee9-120">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="6eee9-121">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="6eee9-121">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="6eee9-122">This property is of type Collection `<string>` and should contain a list of region names.</span><span class="sxs-lookup"><span data-stu-id="6eee9-122">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="6eee9-123">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span><span class="sxs-lookup"><span data-stu-id="6eee9-123">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="6eee9-124">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span><span class="sxs-lookup"><span data-stu-id="6eee9-124">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="6eee9-125">The URLs for the endpoints should not be considered as long-lived constants.</span><span class="sxs-lookup"><span data-stu-id="6eee9-125">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="6eee9-126">The service may update these at any point.</span><span class="sxs-lookup"><span data-stu-id="6eee9-126">The service may update these at any point.</span></span> <span data-ttu-id="6eee9-127">The SDK handles this change automatically.</span><span class="sxs-lookup"><span data-stu-id="6eee9-127">The SDK handles this change automatically.</span></span>
>
>

    // Getting endpoints from application settings or other configuration location
    Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
    string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
    
    ConnectionPolicy connectionPolicy = new ConnectionPolicy();

    //Setting read region selection preference
    connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
    connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
    connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

    // initialize connection
    DocumentClient docClient = new DocumentClient(
        accountEndPoint,
        accountKey,
        connectionPolicy);

    // connect to DocDB
    await docClient.OpenAsync().ConfigureAwait(false);


## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="6eee9-128">NodeJS, JavaScript, and Python SDKs</span><span class="sxs-lookup"><span data-stu-id="6eee9-128">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="6eee9-129">The SDK can be used without any code changes.</span><span class="sxs-lookup"><span data-stu-id="6eee9-129">The SDK can be used without any code changes.</span></span> <span data-ttu-id="6eee9-130">In this case, the SDK will automatically direct both reads and writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="6eee9-130">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="6eee9-131">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="6eee9-131">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="6eee9-132">This is parameter is an array of strings that takes a list of region names.</span><span class="sxs-lookup"><span data-stu-id="6eee9-132">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="6eee9-133">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span><span class="sxs-lookup"><span data-stu-id="6eee9-133">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="6eee9-134">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="6eee9-134">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="6eee9-135">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span><span class="sxs-lookup"><span data-stu-id="6eee9-135">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="6eee9-136">The URLs for the endpoints should not be considered as long-lived constants.</span><span class="sxs-lookup"><span data-stu-id="6eee9-136">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="6eee9-137">The service may update these at any point.</span><span class="sxs-lookup"><span data-stu-id="6eee9-137">The service may update these at any point.</span></span> <span data-ttu-id="6eee9-138">The SDK will handle this change automatically.</span><span class="sxs-lookup"><span data-stu-id="6eee9-138">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="6eee9-139">Below is a code example for NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="6eee9-139">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="6eee9-140">Python and Java will follow the same pattern.</span><span class="sxs-lookup"><span data-stu-id="6eee9-140">Python and Java will follow the same pattern.</span></span>

    // Creating a ConnectionPolicy object
    var connectionPolicy = new DocumentBase.ConnectionPolicy();

    // Setting read region selection preference, in the following order -
    // 1 - West US
    // 2 - East US
    // 3 - North Europe
    connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

    // initialize the connection
    var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);


## <a name="rest"></a><span data-ttu-id="6eee9-141">REST</span><span class="sxs-lookup"><span data-stu-id="6eee9-141">REST</span></span>
<span data-ttu-id="6eee9-142">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span><span class="sxs-lookup"><span data-stu-id="6eee9-142">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="6eee9-143">The service will return a list of regions and their corresponding DocumentDB endpoint URIs for the replicas.</span><span class="sxs-lookup"><span data-stu-id="6eee9-143">The service will return a list of regions and their corresponding DocumentDB endpoint URIs for the replicas.</span></span> <span data-ttu-id="6eee9-144">The current write region will be indicated in the response.</span><span class="sxs-lookup"><span data-stu-id="6eee9-144">The current write region will be indicated in the response.</span></span> <span data-ttu-id="6eee9-145">The client can then select the appropriate endpoint for all further REST API requests as follows.</span><span class="sxs-lookup"><span data-stu-id="6eee9-145">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="6eee9-146">Example response</span><span class="sxs-lookup"><span data-stu-id="6eee9-146">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="6eee9-147">All PUT, POST and DELETE requests must go to the indicated write URI</span><span class="sxs-lookup"><span data-stu-id="6eee9-147">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="6eee9-148">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span><span class="sxs-lookup"><span data-stu-id="6eee9-148">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="6eee9-149">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span><span class="sxs-lookup"><span data-stu-id="6eee9-149">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="6eee9-150">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span><span class="sxs-lookup"><span data-stu-id="6eee9-150">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="6eee9-151">The client should then GET the list of regions again to get the updated write region.</span><span class="sxs-lookup"><span data-stu-id="6eee9-151">The client should then GET the list of regions again to get the updated write region.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eee9-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="6eee9-152">Next steps</span></span>
<span data-ttu-id="6eee9-153">Learn more about the distributing data globally with DocumentDB in the following articles:</span><span class="sxs-lookup"><span data-stu-id="6eee9-153">Learn more about the distributing data globally with DocumentDB in the following articles:</span></span>

* [<span data-ttu-id="6eee9-154">Distribute data globally with DocumentDB</span><span class="sxs-lookup"><span data-stu-id="6eee9-154">Distribute data globally with DocumentDB</span></span>](documentdb-distribute-data-globally.md)
* [<span data-ttu-id="6eee9-155">Consistency levels</span><span class="sxs-lookup"><span data-stu-id="6eee9-155">Consistency levels</span></span>](documentdb-consistency-levels.md)
* [<span data-ttu-id="6eee9-156">Add regions using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6eee9-156">Add regions using the Azure portal</span></span>](documentdb-portal-global-replication.md)

[regions]: https://azure.microsoft.com/regions/
