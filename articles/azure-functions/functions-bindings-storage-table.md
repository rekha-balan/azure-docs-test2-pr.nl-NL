---
title: Azure Table storage bindings for Azure Functions
description: Understand how to use Azure Table storage bindings in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
ms.date: 09/03/2018
ms.author: glenga
ms.openlocfilehash: 306e9d1f1990ea6b0f1449a876096a637ccda62a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791172"
---
# <a name="azure-table-storage-bindings-for-azure-functions"></a><span data-ttu-id="f9f84-104">Azure Table storage bindings for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f9f84-104">Azure Table storage bindings for Azure Functions</span></span>

<span data-ttu-id="f9f84-105">This article explains how to work with Azure Table storage bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f9f84-105">This article explains how to work with Azure Table storage bindings in Azure Functions.</span></span> <span data-ttu-id="f9f84-106">Azure Functions supports input and output bindings for Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="f9f84-106">Azure Functions supports input and output bindings for Azure Table storage.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="f9f84-107">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="f9f84-107">Packages - Functions 1.x</span></span>

<span data-ttu-id="f9f84-108">The Table storage bindings are provided in the [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) NuGet package, version 2.x.</span><span class="sxs-lookup"><span data-stu-id="f9f84-108">The Table storage bindings are provided in the [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) NuGet package, version 2.x.</span></span> <span data-ttu-id="f9f84-109">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/v2.x/src/Microsoft.Azure.WebJobs.Storage/Table) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="f9f84-109">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/v2.x/src/Microsoft.Azure.WebJobs.Storage/Table) GitHub repository.</span></span>

[!INCLUDE [functions-package-auto](../../includes/functions-package-auto.md)]

[!INCLUDE [functions-storage-sdk-version](../../includes/functions-storage-sdk-version.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="f9f84-110">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="f9f84-110">Packages - Functions 2.x</span></span>

<span data-ttu-id="f9f84-111">The Table storage bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="f9f84-111">The Table storage bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage) NuGet package, version 3.x.</span></span> <span data-ttu-id="f9f84-112">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/dev/src/Microsoft.Azure.WebJobs.Extensions.Storage/Tables) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="f9f84-112">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/dev/src/Microsoft.Azure.WebJobs.Extensions.Storage/Tables) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="input"></a><span data-ttu-id="f9f84-113">Input</span><span class="sxs-lookup"><span data-stu-id="f9f84-113">Input</span></span>

<span data-ttu-id="f9f84-114">Use the Azure Table storage input binding to read a table in an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f9f84-114">Use the Azure Table storage input binding to read a table in an Azure Storage account.</span></span>

## <a name="input---example"></a><span data-ttu-id="f9f84-115">Input - example</span><span class="sxs-lookup"><span data-stu-id="f9f84-115">Input - example</span></span>

<span data-ttu-id="f9f84-116">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="f9f84-116">See the language-specific example:</span></span>

* [<span data-ttu-id="f9f84-117">C# read one entity</span><span class="sxs-lookup"><span data-stu-id="f9f84-117">C# read one entity</span></span>](#input---c-example---one-entity)
* [<span data-ttu-id="f9f84-118">C# bind to IQueryable</span><span class="sxs-lookup"><span data-stu-id="f9f84-118">C# bind to IQueryable</span></span>](#input---c-example---iqueryable)
* [<span data-ttu-id="f9f84-119">C# bind to CloudTable</span><span class="sxs-lookup"><span data-stu-id="f9f84-119">C# bind to CloudTable</span></span>](#input---c-example---cloudtable)
* [<span data-ttu-id="f9f84-120">C# script read one entity</span><span class="sxs-lookup"><span data-stu-id="f9f84-120">C# script read one entity</span></span>](#input---c-script-example---one-entity)
* [<span data-ttu-id="f9f84-121">C# script bind to IQueryable</span><span class="sxs-lookup"><span data-stu-id="f9f84-121">C# script bind to IQueryable</span></span>](#input---c-script-example---iqueryable)
* [<span data-ttu-id="f9f84-122">C# script bind to CloudTable</span><span class="sxs-lookup"><span data-stu-id="f9f84-122">C# script bind to CloudTable</span></span>](#input---c-script-example---cloudtable)
* [<span data-ttu-id="f9f84-123">F#</span><span class="sxs-lookup"><span data-stu-id="f9f84-123">F#</span></span>](#input---f-example)
* [<span data-ttu-id="f9f84-124">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f9f84-124">JavaScript</span></span>](#input---javascript-example)
* [<span data-ttu-id="f9f84-125">Java</span><span class="sxs-lookup"><span data-stu-id="f9f84-125">Java</span></span>](#input---java-example)

### <a name="input---c-example---one-entity"></a><span data-ttu-id="f9f84-126">Input - C# example - one entity</span><span class="sxs-lookup"><span data-stu-id="f9f84-126">Input - C# example - one entity</span></span>

<span data-ttu-id="f9f84-127">The following example shows a [C# function](functions-dotnet-class-library.md) that reads a single table row.</span><span class="sxs-lookup"><span data-stu-id="f9f84-127">The following example shows a [C# function](functions-dotnet-class-library.md) that reads a single table row.</span></span> 

<span data-ttu-id="f9f84-128">The row key value "{queueTrigger}" indicates that the row key comes from the queue message string.</span><span class="sxs-lookup"><span data-stu-id="f9f84-128">The row key value "{queueTrigger}" indicates that the row key comes from the queue message string.</span></span>

```csharp
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableInput")]
    public static void TableInput(
        [QueueTrigger("table-items")] string input, 
        [Table("MyTable", "MyPartition", "{queueTrigger}")] MyPoco poco, 
        TraceWriter log)
    {
        log.Info($"PK={poco.PartitionKey}, RK={poco.RowKey}, Text={poco.Text}");
    }
}
```

### <a name="input---c-example---iqueryable"></a><span data-ttu-id="f9f84-129">Input - C# example - IQueryable</span><span class="sxs-lookup"><span data-stu-id="f9f84-129">Input - C# example - IQueryable</span></span>

<span data-ttu-id="f9f84-130">The following example shows a [C# function](functions-dotnet-class-library.md) that reads multiple table rows.</span><span class="sxs-lookup"><span data-stu-id="f9f84-130">The following example shows a [C# function](functions-dotnet-class-library.md) that reads multiple table rows.</span></span> <span data-ttu-id="f9f84-131">Note that the `MyPoco` class derives from `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-131">Note that the `MyPoco` class derives from `TableEntity`.</span></span>

```csharp
public class TableStorage
{
    public class MyPoco : TableEntity
    {
        public string Text { get; set; }
    }

    [FunctionName("TableInput")]
    public static void TableInput(
        [QueueTrigger("table-items")] string input, 
        [Table("MyTable", "MyPartition")] IQueryable<MyPoco> pocos, 
        TraceWriter log)
    {
        foreach (MyPoco poco in pocos)
        {
            log.Info($"PK={poco.PartitionKey}, RK={poco.RowKey}, Text={poco.Text}");
        }
    }
}
```

### <a name="input---c-example---cloudtable"></a><span data-ttu-id="f9f84-132">Input - C# example - CloudTable</span><span class="sxs-lookup"><span data-stu-id="f9f84-132">Input - C# example - CloudTable</span></span>

<span data-ttu-id="f9f84-133">`IQueryable` isn't supported in the [Functions v2 runtime](functions-versions.md).</span><span class="sxs-lookup"><span data-stu-id="f9f84-133">`IQueryable` isn't supported in the [Functions v2 runtime](functions-versions.md).</span></span> <span data-ttu-id="f9f84-134">An alternative is to use a `CloudTable` method parameter to read the table by using the Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="f9f84-134">An alternative is to use a `CloudTable` method parameter to read the table by using the Azure Storage SDK.</span></span> <span data-ttu-id="f9f84-135">Here's an example of a 2.x function that queries an Azure Functions log table:</span><span class="sxs-lookup"><span data-stu-id="f9f84-135">Here's an example of a 2.x function that queries an Azure Functions log table:</span></span>

```csharp
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using Microsoft.WindowsAzure.Storage.Table;
using System;
using System.Threading.Tasks;

namespace FunctionAppCloudTable2
{
    public class LogEntity : TableEntity
    {
        public string OriginalName { get; set; }
    }
    public static class CloudTableDemo
    {
        [FunctionName("CloudTableDemo")]
        public static async Task Run(
            [TimerTrigger("0 */1 * * * *")] TimerInfo myTimer, 
            [Table("AzureWebJobsHostLogscommon")] CloudTable cloudTable,
            TraceWriter log)
        {
            log.Info($"C# Timer trigger function executed at: {DateTime.Now}");

            TableQuery<LogEntity> rangeQuery = new TableQuery<LogEntity>().Where(
                TableQuery.CombineFilters(
                    TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, 
                        "FD2"),
                    TableOperators.And,
                    TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.GreaterThan, 
                        "t")));

            // Execute the query and loop through the results
            foreach (LogEntity entity in 
                await cloudTable.ExecuteQuerySegmentedAsync(rangeQuery, null))
            {
                log.Info(
                    $"{entity.PartitionKey}\t{entity.RowKey}\t{entity.Timestamp}\t{entity.OriginalName}");
            }
        }
    }
}
```

<span data-ttu-id="f9f84-136">For more information about how to use CloudTable, see [Get started with Azure Table storage](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f9f84-136">For more information about how to use CloudTable, see [Get started with Azure Table storage](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="f9f84-137">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="f9f84-137">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span>

### <a name="input---c-script-example---one-entity"></a><span data-ttu-id="f9f84-138">Input - C# script example - one entity</span><span class="sxs-lookup"><span data-stu-id="f9f84-138">Input - C# script example - one entity</span></span>

<span data-ttu-id="f9f84-139">The following example shows a table input binding in a *function.json* file and [C# script](functions-reference-csharp.md) code that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-139">The following example shows a table input binding in a *function.json* file and [C# script](functions-reference-csharp.md) code that uses the binding.</span></span> <span data-ttu-id="f9f84-140">The function uses a queue trigger to read a single table row.</span><span class="sxs-lookup"><span data-stu-id="f9f84-140">The function uses a queue trigger to read a single table row.</span></span> 

<span data-ttu-id="f9f84-141">The *function.json* file specifies a `partitionKey` and a `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-141">The *function.json* file specifies a `partitionKey` and a `rowKey`.</span></span> <span data-ttu-id="f9f84-142">The `rowKey` value "{queueTrigger}" indicates that the row key comes from the queue message string.</span><span class="sxs-lookup"><span data-stu-id="f9f84-142">The `rowKey` value "{queueTrigger}" indicates that the row key comes from the queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnectionAppSetting",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-143">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-143">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-144">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="f9f84-144">Here's the C# script code:</span></span>

```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

### <a name="input---c-script-example---iqueryable"></a><span data-ttu-id="f9f84-145">Input - C# script example - IQueryable</span><span class="sxs-lookup"><span data-stu-id="f9f84-145">Input - C# script example - IQueryable</span></span>

<span data-ttu-id="f9f84-146">The following example shows a table input binding in a *function.json* file and [C# script](functions-reference-csharp.md) code that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-146">The following example shows a table input binding in a *function.json* file and [C# script](functions-reference-csharp.md) code that uses the binding.</span></span> <span data-ttu-id="f9f84-147">The function reads entities for a partition key that is specified in a queue message.</span><span class="sxs-lookup"><span data-stu-id="f9f84-147">The function reads entities for a partition key that is specified in a queue message.</span></span>

<span data-ttu-id="f9f84-148">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="f9f84-148">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnectionAppSetting",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnectionAppSetting",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-149">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-149">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-150">The C# script code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`:</span><span class="sxs-lookup"><span data-stu-id="f9f84-150">The C# script code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`:</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

### <a name="input---c-script-example---cloudtable"></a><span data-ttu-id="f9f84-151">Input - C# script example - CloudTable</span><span class="sxs-lookup"><span data-stu-id="f9f84-151">Input - C# script example - CloudTable</span></span>

<span data-ttu-id="f9f84-152">`IQueryable` isn't supported in the [Functions v2 runtime](functions-versions.md).</span><span class="sxs-lookup"><span data-stu-id="f9f84-152">`IQueryable` isn't supported in the [Functions v2 runtime](functions-versions.md).</span></span> <span data-ttu-id="f9f84-153">An alternative is to use a `CloudTable` method parameter to read the table by using the Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="f9f84-153">An alternative is to use a `CloudTable` method parameter to read the table by using the Azure Storage SDK.</span></span> <span data-ttu-id="f9f84-154">Here's an example of a 2.x function that queries an Azure Functions log table:</span><span class="sxs-lookup"><span data-stu-id="f9f84-154">Here's an example of a 2.x function that queries an Azure Functions log table:</span></span>

```json
{
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "0 */1 * * * *"
    },
    {
      "name": "cloudTable",
      "type": "table",
      "connection": "AzureWebJobsStorage",
      "tableName": "AzureWebJobsHostLogscommon",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;
using System;
using System.Threading.Tasks;

public static async Task Run(TimerInfo myTimer, CloudTable cloudTable, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");

    TableQuery<LogEntity> rangeQuery = new TableQuery<LogEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, 
            "FD2"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.GreaterThan, 
            "a")));

    // Execute the query and loop through the results
    foreach (LogEntity entity in 
    await cloudTable.ExecuteQuerySegmentedAsync(rangeQuery, null))
    {
        log.Info(
            $"{entity.PartitionKey}\t{entity.RowKey}\t{entity.Timestamp}\t{entity.OriginalName}");
    }
}

public class LogEntity : TableEntity
{
    public string OriginalName { get; set; }
}
```

<span data-ttu-id="f9f84-155">For more information about how to use CloudTable, see [Get started with Azure Table storage](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f9f84-155">For more information about how to use CloudTable, see [Get started with Azure Table storage](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="f9f84-156">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="f9f84-156">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span>

### <a name="input---f-example"></a><span data-ttu-id="f9f84-157">Input - F# example</span><span class="sxs-lookup"><span data-stu-id="f9f84-157">Input - F# example</span></span>

<span data-ttu-id="f9f84-158">The following example shows a table input binding in a *function.json* file and [F# script](functions-reference-fsharp.md) code that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-158">The following example shows a table input binding in a *function.json* file and [F# script](functions-reference-fsharp.md) code that uses the binding.</span></span> <span data-ttu-id="f9f84-159">The function uses a queue trigger to read a single table row.</span><span class="sxs-lookup"><span data-stu-id="f9f84-159">The function uses a queue trigger to read a single table row.</span></span> 

<span data-ttu-id="f9f84-160">The *function.json* file specifies a `partitionKey` and a `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-160">The *function.json* file specifies a `partitionKey` and a `rowKey`.</span></span> <span data-ttu-id="f9f84-161">The `rowKey` value "{queueTrigger}" indicates that the row key comes from the queue message string.</span><span class="sxs-lookup"><span data-stu-id="f9f84-161">The `rowKey` value "{queueTrigger}" indicates that the row key comes from the queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnectionAppSetting",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-162">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-162">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-163">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="f9f84-163">Here's the F# code:</span></span>

```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

### <a name="input---javascript-example"></a><span data-ttu-id="f9f84-164">Input - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="f9f84-164">Input - JavaScript example</span></span>

<span data-ttu-id="f9f84-165">The following example shows a  table input binding in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-165">The following example shows a  table input binding in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="f9f84-166">The function uses a queue trigger to read a single table row.</span><span class="sxs-lookup"><span data-stu-id="f9f84-166">The function uses a queue trigger to read a single table row.</span></span> 

<span data-ttu-id="f9f84-167">The *function.json* file specifies a `partitionKey` and a `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-167">The *function.json* file specifies a `partitionKey` and a `rowKey`.</span></span> <span data-ttu-id="f9f84-168">The `rowKey` value "{queueTrigger}" indicates that the row key comes from the queue message string.</span><span class="sxs-lookup"><span data-stu-id="f9f84-168">The `rowKey` value "{queueTrigger}" indicates that the row key comes from the queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnectionAppSetting",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-169">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-169">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-170">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="f9f84-170">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

### <a name="input---java-example"></a><span data-ttu-id="f9f84-171">Input - Java example</span><span class="sxs-lookup"><span data-stu-id="f9f84-171">Input - Java example</span></span>

<span data-ttu-id="f9f84-172">The following example shows an HTTP triggered function which returns the total count of the items in a specified partition in Table storage.</span><span class="sxs-lookup"><span data-stu-id="f9f84-172">The following example shows an HTTP triggered function which returns the total count of the items in a specified partition in Table storage.</span></span>

```java
@FunctionName("getallcount")
public int run(
   @HttpTrigger(name = "req",
                 methods = {"get"},
                 authLevel = AuthorizationLevel.ANONYMOUS) Object dummyShouldNotBeUsed,
   @TableInput(name = "items",
                tableName = "mytablename",  partitionKey = "myparkey",
                connection = "myconnvarname") MyItem[] items
) {
    return items.length;
}
```


## <a name="input---attributes"></a><span data-ttu-id="f9f84-173">Input - attributes</span><span class="sxs-lookup"><span data-stu-id="f9f84-173">Input - attributes</span></span>
 
<span data-ttu-id="f9f84-174">In [C# class libraries](functions-dotnet-class-library.md), use the following attributes to configure a table input binding:</span><span class="sxs-lookup"><span data-stu-id="f9f84-174">In [C# class libraries](functions-dotnet-class-library.md), use the following attributes to configure a table input binding:</span></span>

* [<span data-ttu-id="f9f84-175">TableAttribute</span><span class="sxs-lookup"><span data-stu-id="f9f84-175">TableAttribute</span></span>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs)

  <span data-ttu-id="f9f84-176">The attribute's constructor takes the table name, partition key, and row key.</span><span class="sxs-lookup"><span data-stu-id="f9f84-176">The attribute's constructor takes the table name, partition key, and row key.</span></span> <span data-ttu-id="f9f84-177">It can be used on an out parameter or on the return value of the function, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f9f84-177">It can be used on an out parameter or on the return value of the function, as shown in the following example:</span></span>

  ```csharp
  [FunctionName("TableInput")]
  public static void Run(
      [QueueTrigger("table-items")] string input, 
      [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, 
      TraceWriter log)
  {
      ...
  }
  ```

  <span data-ttu-id="f9f84-178">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f9f84-178">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span></span>

  ```csharp
  [FunctionName("TableInput")]
  public static void Run(
      [QueueTrigger("table-items")] string input, 
      [Table("MyTable", "Http", "{queueTrigger}", Connection = "StorageConnectionAppSetting")] MyPoco poco, 
      TraceWriter log)
  {
      ...
  }
  ```

  <span data-ttu-id="f9f84-179">For a complete example, see [Input - C# example](#input---c-example).</span><span class="sxs-lookup"><span data-stu-id="f9f84-179">For a complete example, see [Input - C# example](#input---c-example).</span></span>

* [<span data-ttu-id="f9f84-180">StorageAccountAttribute</span><span class="sxs-lookup"><span data-stu-id="f9f84-180">StorageAccountAttribute</span></span>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)

  <span data-ttu-id="f9f84-181">Provides another way to specify the storage account to use.</span><span class="sxs-lookup"><span data-stu-id="f9f84-181">Provides another way to specify the storage account to use.</span></span> <span data-ttu-id="f9f84-182">The constructor takes the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="f9f84-182">The constructor takes the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="f9f84-183">The attribute can be applied at the parameter, method, or class level.</span><span class="sxs-lookup"><span data-stu-id="f9f84-183">The attribute can be applied at the parameter, method, or class level.</span></span> <span data-ttu-id="f9f84-184">The following example shows class level and method level:</span><span class="sxs-lookup"><span data-stu-id="f9f84-184">The following example shows class level and method level:</span></span>

  ```csharp
  [StorageAccount("ClassLevelStorageAppSetting")]
  public static class AzureFunctions
  {
      [FunctionName("TableInput")]
      [StorageAccount("FunctionLevelStorageAppSetting")]
      public static void Run( //...
  {
      ...
  }
  ```

<span data-ttu-id="f9f84-185">The storage account to use is determined in the following order:</span><span class="sxs-lookup"><span data-stu-id="f9f84-185">The storage account to use is determined in the following order:</span></span>

* <span data-ttu-id="f9f84-186">The `Table` attribute's `Connection` property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-186">The `Table` attribute's `Connection` property.</span></span>
* <span data-ttu-id="f9f84-187">The `StorageAccount` attribute applied to the same parameter as the `Table` attribute.</span><span class="sxs-lookup"><span data-stu-id="f9f84-187">The `StorageAccount` attribute applied to the same parameter as the `Table` attribute.</span></span>
* <span data-ttu-id="f9f84-188">The `StorageAccount` attribute applied to the function.</span><span class="sxs-lookup"><span data-stu-id="f9f84-188">The `StorageAccount` attribute applied to the function.</span></span>
* <span data-ttu-id="f9f84-189">The `StorageAccount` attribute applied to the class.</span><span class="sxs-lookup"><span data-stu-id="f9f84-189">The `StorageAccount` attribute applied to the class.</span></span>
* <span data-ttu-id="f9f84-190">The default storage account for the function app ("AzureWebJobsStorage" app setting).</span><span class="sxs-lookup"><span data-stu-id="f9f84-190">The default storage account for the function app ("AzureWebJobsStorage" app setting).</span></span>

## <a name="input---java-annotations"></a><span data-ttu-id="f9f84-191">Input - Java annotations</span><span class="sxs-lookup"><span data-stu-id="f9f84-191">Input - Java annotations</span></span>

<span data-ttu-id="f9f84-192">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@TableInput` annotation on parameters whose value would come from Table storage.</span><span class="sxs-lookup"><span data-stu-id="f9f84-192">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@TableInput` annotation on parameters whose value would come from Table storage.</span></span>  <span data-ttu-id="f9f84-193">This annotation can be used with native Java types, POJOs, or nullable values using Optional<T>.</span><span class="sxs-lookup"><span data-stu-id="f9f84-193">This annotation can be used with native Java types, POJOs, or nullable values using Optional<T>.</span></span> 

## <a name="input---configuration"></a><span data-ttu-id="f9f84-194">Input - configuration</span><span class="sxs-lookup"><span data-stu-id="f9f84-194">Input - configuration</span></span>

<span data-ttu-id="f9f84-195">The following table explains the binding configuration properties that you set in the *function.json* file and the `Table` attribute.</span><span class="sxs-lookup"><span data-stu-id="f9f84-195">The following table explains the binding configuration properties that you set in the *function.json* file and the `Table` attribute.</span></span>

|<span data-ttu-id="f9f84-196">function.json property</span><span class="sxs-lookup"><span data-stu-id="f9f84-196">function.json property</span></span> | <span data-ttu-id="f9f84-197">Attribute property</span><span class="sxs-lookup"><span data-stu-id="f9f84-197">Attribute property</span></span> |<span data-ttu-id="f9f84-198">Description</span><span class="sxs-lookup"><span data-stu-id="f9f84-198">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="f9f84-199">**type**</span><span class="sxs-lookup"><span data-stu-id="f9f84-199">**type**</span></span> | <span data-ttu-id="f9f84-200">n/a</span><span class="sxs-lookup"><span data-stu-id="f9f84-200">n/a</span></span> | <span data-ttu-id="f9f84-201">Must be set to `table`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-201">Must be set to `table`.</span></span> <span data-ttu-id="f9f84-202">This property is set automatically when you create the binding in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f9f84-202">This property is set automatically when you create the binding in the Azure portal.</span></span>|
|<span data-ttu-id="f9f84-203">**direction**</span><span class="sxs-lookup"><span data-stu-id="f9f84-203">**direction**</span></span> | <span data-ttu-id="f9f84-204">n/a</span><span class="sxs-lookup"><span data-stu-id="f9f84-204">n/a</span></span> | <span data-ttu-id="f9f84-205">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-205">Must be set to `in`.</span></span> <span data-ttu-id="f9f84-206">This property is set automatically when you create the binding in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f9f84-206">This property is set automatically when you create the binding in the Azure portal.</span></span> |
|<span data-ttu-id="f9f84-207">**name**</span><span class="sxs-lookup"><span data-stu-id="f9f84-207">**name**</span></span> | <span data-ttu-id="f9f84-208">n/a</span><span class="sxs-lookup"><span data-stu-id="f9f84-208">n/a</span></span> | <span data-ttu-id="f9f84-209">The name of the variable that represents the table or entity in function code.</span><span class="sxs-lookup"><span data-stu-id="f9f84-209">The name of the variable that represents the table or entity in function code.</span></span> | 
|<span data-ttu-id="f9f84-210">**tableName**</span><span class="sxs-lookup"><span data-stu-id="f9f84-210">**tableName**</span></span> | <span data-ttu-id="f9f84-211">**TableName**</span><span class="sxs-lookup"><span data-stu-id="f9f84-211">**TableName**</span></span> | <span data-ttu-id="f9f84-212">The name of the table.</span><span class="sxs-lookup"><span data-stu-id="f9f84-212">The name of the table.</span></span>| 
|<span data-ttu-id="f9f84-213">**partitionKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-213">**partitionKey**</span></span> | <span data-ttu-id="f9f84-214">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-214">**PartitionKey**</span></span> |<span data-ttu-id="f9f84-215">Optional.</span><span class="sxs-lookup"><span data-stu-id="f9f84-215">Optional.</span></span> <span data-ttu-id="f9f84-216">The partition key of the table entity to read.</span><span class="sxs-lookup"><span data-stu-id="f9f84-216">The partition key of the table entity to read.</span></span> <span data-ttu-id="f9f84-217">See the [usage](#input---usage) section for guidance on how to use this property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-217">See the [usage](#input---usage) section for guidance on how to use this property.</span></span>| 
|<span data-ttu-id="f9f84-218">**rowKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-218">**rowKey**</span></span> |<span data-ttu-id="f9f84-219">**RowKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-219">**RowKey**</span></span> | <span data-ttu-id="f9f84-220">Optional.</span><span class="sxs-lookup"><span data-stu-id="f9f84-220">Optional.</span></span> <span data-ttu-id="f9f84-221">The row key of the table entity to read.</span><span class="sxs-lookup"><span data-stu-id="f9f84-221">The row key of the table entity to read.</span></span> <span data-ttu-id="f9f84-222">See the [usage](#input---usage) section for guidance on how to use this property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-222">See the [usage](#input---usage) section for guidance on how to use this property.</span></span>| 
|<span data-ttu-id="f9f84-223">**take**</span><span class="sxs-lookup"><span data-stu-id="f9f84-223">**take**</span></span> |<span data-ttu-id="f9f84-224">**Take**</span><span class="sxs-lookup"><span data-stu-id="f9f84-224">**Take**</span></span> | <span data-ttu-id="f9f84-225">Optional.</span><span class="sxs-lookup"><span data-stu-id="f9f84-225">Optional.</span></span> <span data-ttu-id="f9f84-226">The maximum number of entities to read in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f9f84-226">The maximum number of entities to read in JavaScript.</span></span> <span data-ttu-id="f9f84-227">See the [usage](#input---usage) section for guidance on how to use this property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-227">See the [usage](#input---usage) section for guidance on how to use this property.</span></span>| 
|<span data-ttu-id="f9f84-228">**filter**</span><span class="sxs-lookup"><span data-stu-id="f9f84-228">**filter**</span></span> |<span data-ttu-id="f9f84-229">**Filter**</span><span class="sxs-lookup"><span data-stu-id="f9f84-229">**Filter**</span></span> | <span data-ttu-id="f9f84-230">Optional.</span><span class="sxs-lookup"><span data-stu-id="f9f84-230">Optional.</span></span> <span data-ttu-id="f9f84-231">An OData filter expression for table input in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f9f84-231">An OData filter expression for table input in JavaScript.</span></span> <span data-ttu-id="f9f84-232">See the [usage](#input---usage) section for guidance on how to use this property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-232">See the [usage](#input---usage) section for guidance on how to use this property.</span></span>| 
|<span data-ttu-id="f9f84-233">**connection**</span><span class="sxs-lookup"><span data-stu-id="f9f84-233">**connection**</span></span> |<span data-ttu-id="f9f84-234">**Connection**</span><span class="sxs-lookup"><span data-stu-id="f9f84-234">**Connection**</span></span> | <span data-ttu-id="f9f84-235">The name of an app setting that contains the Storage connection string to use for this binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-235">The name of an app setting that contains the Storage connection string to use for this binding.</span></span> <span data-ttu-id="f9f84-236">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span><span class="sxs-lookup"><span data-stu-id="f9f84-236">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span></span> <span data-ttu-id="f9f84-237">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span><span class="sxs-lookup"><span data-stu-id="f9f84-237">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span></span> <span data-ttu-id="f9f84-238">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-238">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span></span>|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="input---usage"></a><span data-ttu-id="f9f84-239">Input - usage</span><span class="sxs-lookup"><span data-stu-id="f9f84-239">Input - usage</span></span>

<span data-ttu-id="f9f84-240">The Table storage input binding supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="f9f84-240">The Table storage input binding supports the following scenarios:</span></span>

* <span data-ttu-id="f9f84-241">**Read one row in C# or C# script**</span><span class="sxs-lookup"><span data-stu-id="f9f84-241">**Read one row in C# or C# script**</span></span>

  <span data-ttu-id="f9f84-242">Set `partitionKey` and `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-242">Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="f9f84-243">Access the table data by using a method parameter `T <paramName>`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-243">Access the table data by using a method parameter `T <paramName>`.</span></span> <span data-ttu-id="f9f84-244">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f9f84-244">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span></span> <span data-ttu-id="f9f84-245">`T` is typically a type that implements `ITableEntity` or derives from `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-245">`T` is typically a type that implements `ITableEntity` or derives from `TableEntity`.</span></span> <span data-ttu-id="f9f84-246">The `filter` and `take` properties are not used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="f9f84-246">The `filter` and `take` properties are not used in this scenario.</span></span> 

* <span data-ttu-id="f9f84-247">**Read one or more rows in C# or C# script**</span><span class="sxs-lookup"><span data-stu-id="f9f84-247">**Read one or more rows in C# or C# script**</span></span>

  <span data-ttu-id="f9f84-248">Access the table data by using a method parameter `IQueryable<T> <paramName>`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-248">Access the table data by using a method parameter `IQueryable<T> <paramName>`.</span></span> <span data-ttu-id="f9f84-249">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f9f84-249">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span></span> <span data-ttu-id="f9f84-250">`T` must be a type that implements `ITableEntity` or derives from `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-250">`T` must be a type that implements `ITableEntity` or derives from `TableEntity`.</span></span> <span data-ttu-id="f9f84-251">You can use `IQueryable` methods to do any filtering required.</span><span class="sxs-lookup"><span data-stu-id="f9f84-251">You can use `IQueryable` methods to do any filtering required.</span></span> <span data-ttu-id="f9f84-252">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="f9f84-252">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>  

  > [!NOTE]
  > <span data-ttu-id="f9f84-253">`IQueryable` isn't supported in the [Functions v2 runtime](functions-versions.md).</span><span class="sxs-lookup"><span data-stu-id="f9f84-253">`IQueryable` isn't supported in the [Functions v2 runtime](functions-versions.md).</span></span> <span data-ttu-id="f9f84-254">An alternative is to [use a CloudTable paramName method parameter](https://stackoverflow.com/questions/48922485/binding-to-table-storage-in-v2-azure-functions-using-cloudtable) to read the table by using the Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="f9f84-254">An alternative is to [use a CloudTable paramName method parameter](https://stackoverflow.com/questions/48922485/binding-to-table-storage-in-v2-azure-functions-using-cloudtable) to read the table by using the Azure Storage SDK.</span></span> <span data-ttu-id="f9f84-255">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="f9f84-255">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span>

* <span data-ttu-id="f9f84-256">**Read one or more rows in JavaScript**</span><span class="sxs-lookup"><span data-stu-id="f9f84-256">**Read one or more rows in JavaScript**</span></span>

  <span data-ttu-id="f9f84-257">Set the `filter` and `take` properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-257">Set the `filter` and `take` properties.</span></span> <span data-ttu-id="f9f84-258">Don't set `partitionKey` or `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-258">Don't set `partitionKey` or `rowKey`.</span></span> <span data-ttu-id="f9f84-259">Access the input table entity (or entities) using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-259">Access the input table entity (or entities) using `context.bindings.<name>`.</span></span> <span data-ttu-id="f9f84-260">The deserialized objects have `RowKey` and `PartitionKey` properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-260">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

## <a name="output"></a><span data-ttu-id="f9f84-261">Output</span><span class="sxs-lookup"><span data-stu-id="f9f84-261">Output</span></span>

<span data-ttu-id="f9f84-262">Use an Azure Table storage output binding to write entities to a table in an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f9f84-262">Use an Azure Table storage output binding to write entities to a table in an Azure Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="f9f84-263">This output binding does not support updating existing entities.</span><span class="sxs-lookup"><span data-stu-id="f9f84-263">This output binding does not support updating existing entities.</span></span> <span data-ttu-id="f9f84-264">Use the `TableOperation.Replace` operation [from the Azure Storage SDK](https://docs.microsoft.com/azure/cosmos-db/table-storage-how-to-use-dotnet#replace-an-entity) to update an existing entity.</span><span class="sxs-lookup"><span data-stu-id="f9f84-264">Use the `TableOperation.Replace` operation [from the Azure Storage SDK](https://docs.microsoft.com/azure/cosmos-db/table-storage-how-to-use-dotnet#replace-an-entity) to update an existing entity.</span></span>   

## <a name="output---example"></a><span data-ttu-id="f9f84-265">Output - example</span><span class="sxs-lookup"><span data-stu-id="f9f84-265">Output - example</span></span>

<span data-ttu-id="f9f84-266">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="f9f84-266">See the language-specific example:</span></span>

* [<span data-ttu-id="f9f84-267">C#</span><span class="sxs-lookup"><span data-stu-id="f9f84-267">C#</span></span>](#output---c-example)
* [<span data-ttu-id="f9f84-268">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="f9f84-268">C# script (.csx)</span></span>](#output---c-script-example)
* [<span data-ttu-id="f9f84-269">F#</span><span class="sxs-lookup"><span data-stu-id="f9f84-269">F#</span></span>](#output---f-example)
* [<span data-ttu-id="f9f84-270">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f9f84-270">JavaScript</span></span>](#output---javascript-example)

### <a name="output---c-example"></a><span data-ttu-id="f9f84-271">Output - C# example</span><span class="sxs-lookup"><span data-stu-id="f9f84-271">Output - C# example</span></span>

<span data-ttu-id="f9f84-272">The following example shows a [C# function](functions-dotnet-class-library.md) that uses an HTTP trigger to write a single table row.</span><span class="sxs-lookup"><span data-stu-id="f9f84-272">The following example shows a [C# function](functions-dotnet-class-library.md) that uses an HTTP trigger to write a single table row.</span></span> 

```csharp
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }
}
```

### <a name="output---c-script-example"></a><span data-ttu-id="f9f84-273">Output - C# script example</span><span class="sxs-lookup"><span data-stu-id="f9f84-273">Output - C# script example</span></span>

<span data-ttu-id="f9f84-274">The following example shows a table output binding in a *function.json* file and [C# script](functions-reference-csharp.md) code that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-274">The following example shows a table output binding in a *function.json* file and [C# script](functions-reference-csharp.md) code that uses the binding.</span></span> <span data-ttu-id="f9f84-275">The function writes multiple table entities.</span><span class="sxs-lookup"><span data-stu-id="f9f84-275">The function writes multiple table entities.</span></span>

<span data-ttu-id="f9f84-276">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="f9f84-276">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnectionAppSetting",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-277">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-277">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-278">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="f9f84-278">Here's the C# script code:</span></span>

```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```

### <a name="output---f-example"></a><span data-ttu-id="f9f84-279">Output - F# example</span><span class="sxs-lookup"><span data-stu-id="f9f84-279">Output - F# example</span></span>

<span data-ttu-id="f9f84-280">The following example shows a table output binding in a *function.json* file and [F# script](functions-reference-fsharp.md) code that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-280">The following example shows a table output binding in a *function.json* file and [F# script](functions-reference-fsharp.md) code that uses the binding.</span></span> <span data-ttu-id="f9f84-281">The function writes multiple table entities.</span><span class="sxs-lookup"><span data-stu-id="f9f84-281">The function writes multiple table entities.</span></span>

<span data-ttu-id="f9f84-282">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="f9f84-282">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnectionAppSetting",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-283">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-283">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-284">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="f9f84-284">Here's the F# code:</span></span>

```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

### <a name="output---javascript-example"></a><span data-ttu-id="f9f84-285">Output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="f9f84-285">Output - JavaScript example</span></span>

<span data-ttu-id="f9f84-286">The following example shows a  table output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-286">The following example shows a  table output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="f9f84-287">The function writes multiple table entities.</span><span class="sxs-lookup"><span data-stu-id="f9f84-287">The function writes multiple table entities.</span></span>

<span data-ttu-id="f9f84-288">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="f9f84-288">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnectionAppSetting",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f9f84-289">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-289">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="f9f84-290">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="f9f84-290">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

## <a name="output---attributes"></a><span data-ttu-id="f9f84-291">Output - attributes</span><span class="sxs-lookup"><span data-stu-id="f9f84-291">Output - attributes</span></span>

<span data-ttu-id="f9f84-292">In [C# class libraries](functions-dotnet-class-library.md), use the [TableAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs).</span><span class="sxs-lookup"><span data-stu-id="f9f84-292">In [C# class libraries](functions-dotnet-class-library.md), use the [TableAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs).</span></span>

<span data-ttu-id="f9f84-293">The attribute's constructor takes the table name.</span><span class="sxs-lookup"><span data-stu-id="f9f84-293">The attribute's constructor takes the table name.</span></span> <span data-ttu-id="f9f84-294">It can be used on an `out` parameter or on the return value of the function, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f9f84-294">It can be used on an `out` parameter or on the return value of the function, as shown in the following example:</span></span>

```csharp
[FunctionName("TableOutput")]
[return: Table("MyTable")]
public static MyPoco TableOutput(
    [HttpTrigger] dynamic input, 
    TraceWriter log)
{
    ...
}
```

<span data-ttu-id="f9f84-295">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f9f84-295">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span></span>

```csharp
[FunctionName("TableOutput")]
[return: Table("MyTable", Connection = "StorageConnectionAppSetting")]
public static MyPoco TableOutput(
    [HttpTrigger] dynamic input, 
    TraceWriter log)
{
    ...
}
```

<span data-ttu-id="f9f84-296">For a complete example, see [Output - C# example](#output---c-example).</span><span class="sxs-lookup"><span data-stu-id="f9f84-296">For a complete example, see [Output - C# example](#output---c-example).</span></span>

<span data-ttu-id="f9f84-297">You can use the `StorageAccount` attribute to specify the storage account at class, method, or parameter level.</span><span class="sxs-lookup"><span data-stu-id="f9f84-297">You can use the `StorageAccount` attribute to specify the storage account at class, method, or parameter level.</span></span> <span data-ttu-id="f9f84-298">For more information, see [Input - attributes](#input---attributes).</span><span class="sxs-lookup"><span data-stu-id="f9f84-298">For more information, see [Input - attributes](#input---attributes).</span></span>

## <a name="output---configuration"></a><span data-ttu-id="f9f84-299">Output - configuration</span><span class="sxs-lookup"><span data-stu-id="f9f84-299">Output - configuration</span></span>

<span data-ttu-id="f9f84-300">The following table explains the binding configuration properties that you set in the *function.json* file and the `Table` attribute.</span><span class="sxs-lookup"><span data-stu-id="f9f84-300">The following table explains the binding configuration properties that you set in the *function.json* file and the `Table` attribute.</span></span>

|<span data-ttu-id="f9f84-301">function.json property</span><span class="sxs-lookup"><span data-stu-id="f9f84-301">function.json property</span></span> | <span data-ttu-id="f9f84-302">Attribute property</span><span class="sxs-lookup"><span data-stu-id="f9f84-302">Attribute property</span></span> |<span data-ttu-id="f9f84-303">Description</span><span class="sxs-lookup"><span data-stu-id="f9f84-303">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="f9f84-304">**type**</span><span class="sxs-lookup"><span data-stu-id="f9f84-304">**type**</span></span> | <span data-ttu-id="f9f84-305">n/a</span><span class="sxs-lookup"><span data-stu-id="f9f84-305">n/a</span></span> | <span data-ttu-id="f9f84-306">Must be set to `table`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-306">Must be set to `table`.</span></span> <span data-ttu-id="f9f84-307">This property is set automatically when you create the binding in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f9f84-307">This property is set automatically when you create the binding in the Azure portal.</span></span>|
|<span data-ttu-id="f9f84-308">**direction**</span><span class="sxs-lookup"><span data-stu-id="f9f84-308">**direction**</span></span> | <span data-ttu-id="f9f84-309">n/a</span><span class="sxs-lookup"><span data-stu-id="f9f84-309">n/a</span></span> | <span data-ttu-id="f9f84-310">Must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-310">Must be set to `out`.</span></span> <span data-ttu-id="f9f84-311">This property is set automatically when you create the binding in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f9f84-311">This property is set automatically when you create the binding in the Azure portal.</span></span> |
|<span data-ttu-id="f9f84-312">**name**</span><span class="sxs-lookup"><span data-stu-id="f9f84-312">**name**</span></span> | <span data-ttu-id="f9f84-313">n/a</span><span class="sxs-lookup"><span data-stu-id="f9f84-313">n/a</span></span> | <span data-ttu-id="f9f84-314">The variable name used in function code that represents the table or entity.</span><span class="sxs-lookup"><span data-stu-id="f9f84-314">The variable name used in function code that represents the table or entity.</span></span> <span data-ttu-id="f9f84-315">Set to `$return` to reference the function return value.</span><span class="sxs-lookup"><span data-stu-id="f9f84-315">Set to `$return` to reference the function return value.</span></span>| 
|<span data-ttu-id="f9f84-316">**tableName**</span><span class="sxs-lookup"><span data-stu-id="f9f84-316">**tableName**</span></span> |<span data-ttu-id="f9f84-317">**TableName**</span><span class="sxs-lookup"><span data-stu-id="f9f84-317">**TableName**</span></span> | <span data-ttu-id="f9f84-318">The name of the table.</span><span class="sxs-lookup"><span data-stu-id="f9f84-318">The name of the table.</span></span>| 
|<span data-ttu-id="f9f84-319">**partitionKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-319">**partitionKey**</span></span> |<span data-ttu-id="f9f84-320">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-320">**PartitionKey**</span></span> | <span data-ttu-id="f9f84-321">The partition key of the table entity to write.</span><span class="sxs-lookup"><span data-stu-id="f9f84-321">The partition key of the table entity to write.</span></span> <span data-ttu-id="f9f84-322">See the [usage section](#output---usage) for guidance on how to use this property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-322">See the [usage section](#output---usage) for guidance on how to use this property.</span></span>| 
|<span data-ttu-id="f9f84-323">**rowKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-323">**rowKey**</span></span> |<span data-ttu-id="f9f84-324">**RowKey**</span><span class="sxs-lookup"><span data-stu-id="f9f84-324">**RowKey**</span></span> | <span data-ttu-id="f9f84-325">The row key of the table entity to write.</span><span class="sxs-lookup"><span data-stu-id="f9f84-325">The row key of the table entity to write.</span></span> <span data-ttu-id="f9f84-326">See the [usage section](#output---usage) for guidance on how to use this property.</span><span class="sxs-lookup"><span data-stu-id="f9f84-326">See the [usage section](#output---usage) for guidance on how to use this property.</span></span>| 
|<span data-ttu-id="f9f84-327">**connection**</span><span class="sxs-lookup"><span data-stu-id="f9f84-327">**connection**</span></span> |<span data-ttu-id="f9f84-328">**Connection**</span><span class="sxs-lookup"><span data-stu-id="f9f84-328">**Connection**</span></span> | <span data-ttu-id="f9f84-329">The name of an app setting that contains the Storage connection string to use for this binding.</span><span class="sxs-lookup"><span data-stu-id="f9f84-329">The name of an app setting that contains the Storage connection string to use for this binding.</span></span> <span data-ttu-id="f9f84-330">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span><span class="sxs-lookup"><span data-stu-id="f9f84-330">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span></span> <span data-ttu-id="f9f84-331">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span><span class="sxs-lookup"><span data-stu-id="f9f84-331">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span></span> <span data-ttu-id="f9f84-332">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-332">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span></span>|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a><span data-ttu-id="f9f84-333">Output - usage</span><span class="sxs-lookup"><span data-stu-id="f9f84-333">Output - usage</span></span>

<span data-ttu-id="f9f84-334">The Table storage output binding supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="f9f84-334">The Table storage output binding supports the following scenarios:</span></span>

* <span data-ttu-id="f9f84-335">**Write one row in any language**</span><span class="sxs-lookup"><span data-stu-id="f9f84-335">**Write one row in any language**</span></span>

  <span data-ttu-id="f9f84-336">In C# and C# script, access the output table entity by using a method parameter such as `out T paramName` or the function return value.</span><span class="sxs-lookup"><span data-stu-id="f9f84-336">In C# and C# script, access the output table entity by using a method parameter such as `out T paramName` or the function return value.</span></span> <span data-ttu-id="f9f84-337">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f9f84-337">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span></span> <span data-ttu-id="f9f84-338">`T` can be any serializable type if the partition key and row key are provided by the *function.json* file or the `Table` attribute.</span><span class="sxs-lookup"><span data-stu-id="f9f84-338">`T` can be any serializable type if the partition key and row key are provided by the *function.json* file or the `Table` attribute.</span></span> <span data-ttu-id="f9f84-339">Otherwise, `T` must be a type that includes `PartitionKey` and `RowKey` properties.</span><span class="sxs-lookup"><span data-stu-id="f9f84-339">Otherwise, `T` must be a type that includes `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="f9f84-340">In this scenario, `T` typically implements `ITableEntity` or derives from `TableEntity`, but it doesn't have to.</span><span class="sxs-lookup"><span data-stu-id="f9f84-340">In this scenario, `T` typically implements `ITableEntity` or derives from `TableEntity`, but it doesn't have to.</span></span>

* <span data-ttu-id="f9f84-341">**Write one or more rows in C# or C#**</span><span class="sxs-lookup"><span data-stu-id="f9f84-341">**Write one or more rows in C# or C#**</span></span>

  <span data-ttu-id="f9f84-342">In C# and C# script, access the output table entity by using a method parameter `ICollector<T> paramName` or `IAsyncCollector<T> paramName`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-342">In C# and C# script, access the output table entity by using a method parameter `ICollector<T> paramName` or `IAsyncCollector<T> paramName`.</span></span> <span data-ttu-id="f9f84-343">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f9f84-343">In C# script, `paramName` is the value specified in the `name` property of *function.json*.</span></span> <span data-ttu-id="f9f84-344">`T` specifies the schema of the entities you want to add.</span><span class="sxs-lookup"><span data-stu-id="f9f84-344">`T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="f9f84-345">Typically, `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span><span class="sxs-lookup"><span data-stu-id="f9f84-345">Typically, `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="f9f84-346">The partition key and row key values in *function.json* or the `Table` attribute constructor are not used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="f9f84-346">The partition key and row key values in *function.json* or the `Table` attribute constructor are not used in this scenario.</span></span>

  <span data-ttu-id="f9f84-347">An alternative is to use a `CloudTable` method parameter to write to the table by using the Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="f9f84-347">An alternative is to use a `CloudTable` method parameter to write to the table by using the Azure Storage SDK.</span></span> <span data-ttu-id="f9f84-348">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="f9f84-348">If you try to bind to `CloudTable` and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span> <span data-ttu-id="f9f84-349">For an example of code that binds to `CloudTable`, see the input binding examples for [C#](#input---c-example---cloudtable) or [C# script](#input---c-script-example---cloudtable) earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="f9f84-349">For an example of code that binds to `CloudTable`, see the input binding examples for [C#](#input---c-example---cloudtable) or [C# script](#input---c-script-example---cloudtable) earlier in this article.</span></span>

* <span data-ttu-id="f9f84-350">**Write one or more rows in JavaScript**</span><span class="sxs-lookup"><span data-stu-id="f9f84-350">**Write one or more rows in JavaScript**</span></span>

  <span data-ttu-id="f9f84-351">In JavaScript functions, access the table output using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f9f84-351">In JavaScript functions, access the table output using `context.bindings.<name>`.</span></span>

## <a name="exceptions-and-return-codes"></a><span data-ttu-id="f9f84-352">Exceptions and return codes</span><span class="sxs-lookup"><span data-stu-id="f9f84-352">Exceptions and return codes</span></span>

| <span data-ttu-id="f9f84-353">Binding</span><span class="sxs-lookup"><span data-stu-id="f9f84-353">Binding</span></span> | <span data-ttu-id="f9f84-354">Reference</span><span class="sxs-lookup"><span data-stu-id="f9f84-354">Reference</span></span> |
|---|---|
| <span data-ttu-id="f9f84-355">Table</span><span class="sxs-lookup"><span data-stu-id="f9f84-355">Table</span></span> | [<span data-ttu-id="f9f84-356">Table Error Codes</span><span class="sxs-lookup"><span data-stu-id="f9f84-356">Table Error Codes</span></span>](https://docs.microsoft.com/rest/api/storageservices/fileservices/table-service-error-codes) |
| <span data-ttu-id="f9f84-357">Blob, Table, Queue</span><span class="sxs-lookup"><span data-stu-id="f9f84-357">Blob, Table, Queue</span></span> | [<span data-ttu-id="f9f84-358">Storage Error Codes</span><span class="sxs-lookup"><span data-stu-id="f9f84-358">Storage Error Codes</span></span>](https://docs.microsoft.com/rest/api/storageservices/fileservices/common-rest-api-error-codes) |
| <span data-ttu-id="f9f84-359">Blob, Table, Queue</span><span class="sxs-lookup"><span data-stu-id="f9f84-359">Blob, Table, Queue</span></span> | [<span data-ttu-id="f9f84-360">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f9f84-360">Troubleshooting</span></span>](https://docs.microsoft.com/rest/api/storageservices/fileservices/troubleshooting-api-operations) |

## <a name="next-steps"></a><span data-ttu-id="f9f84-361">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9f84-361">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9f84-362">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="f9f84-362">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
