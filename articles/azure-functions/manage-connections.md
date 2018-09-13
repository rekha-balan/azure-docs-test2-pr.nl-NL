---
title: How to manage connections in Azure Functions
description: Learn how to avoid performance problems in Azure Functions by using static connection clients.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.topic: conceptual
ms.date: 07/13/2018
ms.author: glenga
ms.openlocfilehash: 6a877bb7f21b129522b9ffeab22eb77d7a556d53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857961"
---
# <a name="how-to-manage-connections-in-azure-functions"></a><span data-ttu-id="065a3-103">How to manage connections in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="065a3-103">How to manage connections in Azure Functions</span></span>

<span data-ttu-id="065a3-104">Functions in a function app share resources, and among those shared resources are connections &mdash; HTTP connections, database connections, and connections to Azure services such as Storage.</span><span class="sxs-lookup"><span data-stu-id="065a3-104">Functions in a function app share resources, and among those shared resources are connections &mdash; HTTP connections, database connections, and connections to Azure services such as Storage.</span></span> <span data-ttu-id="065a3-105">When many functions are running concurrently, it's possible to run out of available connections.</span><span class="sxs-lookup"><span data-stu-id="065a3-105">When many functions are running concurrently, it's possible to run out of available connections.</span></span> <span data-ttu-id="065a3-106">This article explains how to code your functions to avoid using more connections than they actually need.</span><span class="sxs-lookup"><span data-stu-id="065a3-106">This article explains how to code your functions to avoid using more connections than they actually need.</span></span>

## <a name="connections-limit"></a><span data-ttu-id="065a3-107">Connections limit</span><span class="sxs-lookup"><span data-stu-id="065a3-107">Connections limit</span></span>

<span data-ttu-id="065a3-108">The number of available connections is limited partly because a function app runs in the [Azure App Service sandbox](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox).</span><span class="sxs-lookup"><span data-stu-id="065a3-108">The number of available connections is limited partly because a function app runs in the [Azure App Service sandbox](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox).</span></span> <span data-ttu-id="065a3-109">One of the restrictions that the sandbox imposes on your code is a [cap on the number of connections, currently 300](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#numerical-sandbox-limits).</span><span class="sxs-lookup"><span data-stu-id="065a3-109">One of the restrictions that the sandbox imposes on your code is a [cap on the number of connections, currently 300](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#numerical-sandbox-limits).</span></span> <span data-ttu-id="065a3-110">When you reach this limit, the functions runtime creates a log with the following message: `Host thresholds exceeded: Connections`.</span><span class="sxs-lookup"><span data-stu-id="065a3-110">When you reach this limit, the functions runtime creates a log with the following message: `Host thresholds exceeded: Connections`.</span></span>

<span data-ttu-id="065a3-111">The likelihood of exceeding the limit goes up when the [scale controller adds function app instances](functions-scale.md#how-the-consumption-plan-works) to handle more requests.</span><span class="sxs-lookup"><span data-stu-id="065a3-111">The likelihood of exceeding the limit goes up when the [scale controller adds function app instances](functions-scale.md#how-the-consumption-plan-works) to handle more requests.</span></span> <span data-ttu-id="065a3-112">Each function app instance can be running many functions at once, all of which are using connections that count toward the 300 limit.</span><span class="sxs-lookup"><span data-stu-id="065a3-112">Each function app instance can be running many functions at once, all of which are using connections that count toward the 300 limit.</span></span>

## <a name="use-static-clients"></a><span data-ttu-id="065a3-113">Use static clients</span><span class="sxs-lookup"><span data-stu-id="065a3-113">Use static clients</span></span>

<span data-ttu-id="065a3-114">To avoid holding more connections than necessary, reuse client instances rather than creating new ones with each function invocation.</span><span class="sxs-lookup"><span data-stu-id="065a3-114">To avoid holding more connections than necessary, reuse client instances rather than creating new ones with each function invocation.</span></span> <span data-ttu-id="065a3-115">.NET clients like the [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx), [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient
), and Azure Storage clients can manage connections if you use a single, static client.</span><span class="sxs-lookup"><span data-stu-id="065a3-115">.NET clients like the [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx), [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient
), and Azure Storage clients can manage connections if you use a single, static client.</span></span>

<span data-ttu-id="065a3-116">Here are some guidelines to follow when using a service-specific client in an Azure Functions application:</span><span class="sxs-lookup"><span data-stu-id="065a3-116">Here are some guidelines to follow when using a service-specific client in an Azure Functions application:</span></span>

- <span data-ttu-id="065a3-117">**DO NOT** create a new client with every function invocation.</span><span class="sxs-lookup"><span data-stu-id="065a3-117">**DO NOT** create a new client with every function invocation.</span></span>
- <span data-ttu-id="065a3-118">**DO** create a single, static client that can be used by every function invocation.</span><span class="sxs-lookup"><span data-stu-id="065a3-118">**DO** create a single, static client that can be used by every function invocation.</span></span>
- <span data-ttu-id="065a3-119">**CONSIDER** creating a single, static client in a shared helper class if different functions use the same service.</span><span class="sxs-lookup"><span data-stu-id="065a3-119">**CONSIDER** creating a single, static client in a shared helper class if different functions use the same service.</span></span>

## <a name="httpclient-code-example"></a><span data-ttu-id="065a3-120">HttpClient code example</span><span class="sxs-lookup"><span data-stu-id="065a3-120">HttpClient code example</span></span>

<span data-ttu-id="065a3-121">Here's an example of function code that creates a static [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx):</span><span class="sxs-lookup"><span data-stu-id="065a3-121">Here's an example of function code that creates a static [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx):</span></span>

```cs
// Create a single, static HttpClient
private static HttpClient httpClient = new HttpClient();

public static async Task Run(string input)
{
    var response = await httpClient.GetAsync("http://example.com");
    // Rest of function
}
```

<span data-ttu-id="065a3-122">A common question about the .NET [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) is "Should I be disposing my client?"</span><span class="sxs-lookup"><span data-stu-id="065a3-122">A common question about the .NET [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) is "Should I be disposing my client?"</span></span> <span data-ttu-id="065a3-123">In general, you dispose objects that implement `IDisposable` when you're done using them.</span><span class="sxs-lookup"><span data-stu-id="065a3-123">In general, you dispose objects that implement `IDisposable` when you're done using them.</span></span> <span data-ttu-id="065a3-124">But you don't dispose a static client because you aren't done using it when the function ends.</span><span class="sxs-lookup"><span data-stu-id="065a3-124">But you don't dispose a static client because you aren't done using it when the function ends.</span></span> <span data-ttu-id="065a3-125">You want the static client to live for the duration of your application.</span><span class="sxs-lookup"><span data-stu-id="065a3-125">You want the static client to live for the duration of your application.</span></span>

## <a name="documentclient-code-example"></a><span data-ttu-id="065a3-126">DocumentClient code example</span><span class="sxs-lookup"><span data-stu-id="065a3-126">DocumentClient code example</span></span>

<span data-ttu-id="065a3-127">[DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient
) connects to an Azure Cosmos DB instance.</span><span class="sxs-lookup"><span data-stu-id="065a3-127">[DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient
) connects to an Azure Cosmos DB instance.</span></span> <span data-ttu-id="065a3-128">The Azure Cosmos DB documentation recommends that you [use a singleton Azure Cosmos DB client for the lifetime of your application](https://docs.microsoft.com/azure/cosmos-db/performance-tips#sdk-usage).</span><span class="sxs-lookup"><span data-stu-id="065a3-128">The Azure Cosmos DB documentation recommends that you [use a singleton Azure Cosmos DB client for the lifetime of your application](https://docs.microsoft.com/azure/cosmos-db/performance-tips#sdk-usage).</span></span> <span data-ttu-id="065a3-129">The following example shows one pattern for doing that in a function:</span><span class="sxs-lookup"><span data-stu-id="065a3-129">The following example shows one pattern for doing that in a function:</span></span>

```cs
#r "Microsoft.Azure.Documents.Client"
using Microsoft.Azure.Documents.Client;

private static Lazy<DocumentClient> lazyClient = new Lazy<DocumentClient>(InitializeDocumentClient);
private static DocumentClient documentClient => lazyClient.Value;

private static DocumentClient InitializeDocumentClient()
{
    // Perform any initialization here
    var uri = new Uri("example");
    var authKey = "authKey";
    
    return new DocumentClient(uri, authKey);
}

public static async Task Run(string input)
{
    Uri collectionUri = UriFactory.CreateDocumentCollectionUri("database", "collection");
    object document = new { Data = "example" };
    await documentClient.UpsertDocumentAsync(collectionUri, document);
    
    // Rest of function
}
```

## <a name="sqlclient-connections"></a><span data-ttu-id="065a3-130">SqlClient connections</span><span class="sxs-lookup"><span data-stu-id="065a3-130">SqlClient connections</span></span>

<span data-ttu-id="065a3-131">Your function code may use the .NET Framework Data Provider for SQL Server ([SqlClient](https://msdn.microsoft.com/library/system.data.sqlclient(v=vs.110).aspx)) to make connections to a SQL relational database.</span><span class="sxs-lookup"><span data-stu-id="065a3-131">Your function code may use the .NET Framework Data Provider for SQL Server ([SqlClient](https://msdn.microsoft.com/library/system.data.sqlclient(v=vs.110).aspx)) to make connections to a SQL relational database.</span></span> <span data-ttu-id="065a3-132">This is also the underlying provider for data frameworks that rely on ADO.NET, such as Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="065a3-132">This is also the underlying provider for data frameworks that rely on ADO.NET, such as Entity Framework.</span></span> <span data-ttu-id="065a3-133">Unlike [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) and [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient
) connections, ADO.NET implements connection pooling by default.</span><span class="sxs-lookup"><span data-stu-id="065a3-133">Unlike [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) and [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient
) connections, ADO.NET implements connection pooling by default.</span></span> <span data-ttu-id="065a3-134">However, because you can still run out of connections, you should optimize connections to the database.</span><span class="sxs-lookup"><span data-stu-id="065a3-134">However, because you can still run out of connections, you should optimize connections to the database.</span></span> <span data-ttu-id="065a3-135">For more information, see [SQL Server Connection Pooling (ADO.NET)](https://docs.microsoft.com/dotnet/framework/data/adonet/sql-server-connection-pooling).</span><span class="sxs-lookup"><span data-stu-id="065a3-135">For more information, see [SQL Server Connection Pooling (ADO.NET)](https://docs.microsoft.com/dotnet/framework/data/adonet/sql-server-connection-pooling).</span></span>

> [!TIP]
> <span data-ttu-id="065a3-136">Some data frameworks, such as [Entity Framework](https://msdn.microsoft.com/library/aa937723(v=vs.113).aspx), typically get connection strings from the **ConnectionStrings** section of a configuration file.</span><span class="sxs-lookup"><span data-stu-id="065a3-136">Some data frameworks, such as [Entity Framework](https://msdn.microsoft.com/library/aa937723(v=vs.113).aspx), typically get connection strings from the **ConnectionStrings** section of a configuration file.</span></span> <span data-ttu-id="065a3-137">In this case, you must explicitly add SQL database connection strings to the **Connection strings** collection of your function app settings and in the [local.settings.json file](functions-run-local.md#local-settings-file) in your local project.</span><span class="sxs-lookup"><span data-stu-id="065a3-137">In this case, you must explicitly add SQL database connection strings to the **Connection strings** collection of your function app settings and in the [local.settings.json file](functions-run-local.md#local-settings-file) in your local project.</span></span> <span data-ttu-id="065a3-138">If you are creating a [SqlConnection](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(v=vs.110).aspx) in your function code, you should store the connection string value in **Application settings** with your other connections.</span><span class="sxs-lookup"><span data-stu-id="065a3-138">If you are creating a [SqlConnection](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(v=vs.110).aspx) in your function code, you should store the connection string value in **Application settings** with your other connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="065a3-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="065a3-139">Next steps</span></span>

<span data-ttu-id="065a3-140">For more information about why static clients are recommended, see [Improper instantiation antipattern](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/).</span><span class="sxs-lookup"><span data-stu-id="065a3-140">For more information about why static clients are recommended, see [Improper instantiation antipattern](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/).</span></span>

<span data-ttu-id="065a3-141">For more Azure Functions performance tips, see [Optimize the performance and reliability of Azure Functions](functions-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="065a3-141">For more Azure Functions performance tips, see [Optimize the performance and reliability of Azure Functions](functions-best-practices.md).</span></span>
