---
title: Azure Cosmos DB global distribution tutorial for the SQL API | Microsoft Docs
description: Learn how to set up Azure Cosmos DB global distribution using the SQL API.
services: cosmos-db
keywords: global distribution
author: rafats
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.date: 05/10/2017
ms.author: rafats
ms.custom: mvc
ms.openlocfilehash: 624c5e78287fac57b06f6b5112d2523e31256ae0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857686"
---
# <a name="set-up-azure-cosmos-db-global-distribution-using-the-sql-api"></a><span data-ttu-id="1e5a4-104">Set up Azure Cosmos DB global distribution using the SQL API</span><span class="sxs-lookup"><span data-stu-id="1e5a4-104">Set up Azure Cosmos DB global distribution using the SQL API</span></span>

<span data-ttu-id="1e5a4-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the SQL API.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the SQL API.</span></span>

<span data-ttu-id="1e5a4-106">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="1e5a4-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="1e5a4-107">Configure global distribution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1e5a4-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="1e5a4-108">Configure global distribution using the [SQL APIs](sql-api-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1e5a4-108">Configure global distribution using the [SQL APIs](sql-api-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-sql-api"></a><span data-ttu-id="1e5a4-109">Connecting to a preferred region using the SQL API</span><span class="sxs-lookup"><span data-stu-id="1e5a4-109">Connecting to a preferred region using the SQL API</span></span>

<span data-ttu-id="1e5a4-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="1e5a4-111">This can be done by setting the connection policy.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="1e5a4-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SQL SDK to perform write and read operations.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SQL SDK to perform write and read operations.</span></span>

<span data-ttu-id="1e5a4-113">This preference list is specified when initializing a connection using the SQL SDKs.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-113">This preference list is specified when initializing a connection using the SQL SDKs.</span></span> <span data-ttu-id="1e5a4-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="1e5a4-115">The SDK will automatically send all writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="1e5a4-116">All reads will be sent to the first available region in the PreferredLocations list.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="1e5a4-117">If the request fails, the client will fail down the list to the next region, and so on.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="1e5a4-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="1e5a4-119">So, for example, if the Database Account is available in four regions, but the client only specifies two read(non-write) regions for PreferredLocations, then no reads will be served out of the read region that is not specified in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-119">So, for example, if the Database Account is available in four regions, but the client only specifies two read(non-write) regions for PreferredLocations, then no reads will be served out of the read region that is not specified in PreferredLocations.</span></span> <span data-ttu-id="1e5a4-120">If the read regions specified in the PreferredLocations are not available,  reads will be served out of write region.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-120">If the read regions specified in the PreferredLocations are not available,  reads will be served out of write region.</span></span>

<span data-ttu-id="1e5a4-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="1e5a4-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="1e5a4-123">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1e5a4-123">.NET SDK</span></span>
<span data-ttu-id="1e5a4-124">The SDK can be used without any code changes.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-124">The SDK can be used without any code changes.</span></span> <span data-ttu-id="1e5a4-125">In this case, the SDK automatically directs both reads and writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-125">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="1e5a4-126">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-126">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="1e5a4-127">This property is of type Collection `<string>` and should contain a list of region names.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-127">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="1e5a4-128">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-128">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="1e5a4-129">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-129">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="1e5a4-130">The URLs for the endpoints should not be considered as long-lived constants.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-130">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="1e5a4-131">The service may update these at any point.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-131">The service may update these at any point.</span></span> <span data-ttu-id="1e5a4-132">The SDK handles this change automatically.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-132">The SDK handles this change automatically.</span></span>
>
>

```csharp
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
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="1e5a4-133">NodeJS, JavaScript, and Python SDKs</span><span class="sxs-lookup"><span data-stu-id="1e5a4-133">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="1e5a4-134">The SDK can be used without any code changes.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-134">The SDK can be used without any code changes.</span></span> <span data-ttu-id="1e5a4-135">In this case, the SDK will automatically direct both reads and writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-135">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="1e5a4-136">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-136">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="1e5a4-137">This is parameter is an array of strings that takes a list of region names.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-137">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="1e5a4-138">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-138">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="1e5a4-139">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="1e5a4-139">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="1e5a4-140">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-140">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="1e5a4-141">The URLs for the endpoints should not be considered as long-lived constants.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-141">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="1e5a4-142">The service may update these at any point.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-142">The service may update these at any point.</span></span> <span data-ttu-id="1e5a4-143">The SDK will handle this change automatically.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-143">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="1e5a4-144">Below is a code example for NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-144">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="1e5a4-145">Python and Java will follow the same pattern.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-145">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="1e5a4-146">REST</span><span class="sxs-lookup"><span data-stu-id="1e5a4-146">REST</span></span>
<span data-ttu-id="1e5a4-147">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-147">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="1e5a4-148">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-148">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="1e5a4-149">The current write region will be indicated in the response.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-149">The current write region will be indicated in the response.</span></span> <span data-ttu-id="1e5a4-150">The client can then select the appropriate endpoint for all further REST API requests as follows.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-150">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="1e5a4-151">Example response</span><span class="sxs-lookup"><span data-stu-id="1e5a4-151">Example response</span></span>

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


* <span data-ttu-id="1e5a4-152">All PUT, POST and DELETE requests must go to the indicated write URI</span><span class="sxs-lookup"><span data-stu-id="1e5a4-152">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="1e5a4-153">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span><span class="sxs-lookup"><span data-stu-id="1e5a4-153">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="1e5a4-154">Write requests to read-only regions will fail with HTTP error code 403 ("Forbidden").</span><span class="sxs-lookup"><span data-stu-id="1e5a4-154">Write requests to read-only regions will fail with HTTP error code 403 ("Forbidden").</span></span>

<span data-ttu-id="1e5a4-155">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 ("Forbidden").</span><span class="sxs-lookup"><span data-stu-id="1e5a4-155">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 ("Forbidden").</span></span> <span data-ttu-id="1e5a4-156">The client should then GET the list of regions again to get the updated write region.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-156">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="1e5a4-157">That's it, that completes this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-157">That's it, that completes this tutorial.</span></span> <span data-ttu-id="1e5a4-158">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="1e5a4-158">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="1e5a4-159">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="1e5a4-159">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e5a4-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e5a4-160">Next steps</span></span>

<span data-ttu-id="1e5a4-161">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="1e5a4-161">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e5a4-162">Configure global distribution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1e5a4-162">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="1e5a4-163">Configure global distribution using the SQL APIs</span><span class="sxs-lookup"><span data-stu-id="1e5a4-163">Configure global distribution using the SQL APIs</span></span>

<span data-ttu-id="1e5a4-164">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span><span class="sxs-lookup"><span data-stu-id="1e5a4-164">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e5a4-165">Develop locally with the emulator</span><span class="sxs-lookup"><span data-stu-id="1e5a4-165">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

