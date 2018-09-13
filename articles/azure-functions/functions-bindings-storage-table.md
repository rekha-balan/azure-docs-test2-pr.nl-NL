---
title: Azure Functions Storage Table bindings | Microsoft Docs
description: Understand how to use Azure Storage bindings in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 67c308f8216ebd291ae483c9b18d43528687e9a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550486"
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="5e4b2-104">Azure Functions Storage table bindings</span><span class="sxs-lookup"><span data-stu-id="5e4b2-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="5e4b2-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="5e4b2-106">Azure Functions supports input and output bindings for Azure Storage tables.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="5e4b2-107">The Storage table binding supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="5e4b2-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="5e4b2-109">The `filter` and `take` properties are not used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="5e4b2-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="5e4b2-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="5e4b2-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="5e4b2-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="5e4b2-114">Don't set `partitionKey` or `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="5e4b2-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="5e4b2-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="5e4b2-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="5e4b2-118">Storage table input binding</span><span class="sxs-lookup"><span data-stu-id="5e4b2-118">Storage table input binding</span></span>
<span data-ttu-id="5e4b2-119">The Azure Storage table input binding enables you to use a storage table in your function.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="5e4b2-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="5e4b2-121">Note the following:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-121">Note the following:</span></span> 

* <span data-ttu-id="5e4b2-122">Use `partitionKey` and `rowKey` together to read a single entity.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="5e4b2-123">These properties are optional.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-123">These properties are optional.</span></span> 
* <span data-ttu-id="5e4b2-124">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="5e4b2-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="5e4b2-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#application-settings).</span><span class="sxs-lookup"><span data-stu-id="5e4b2-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#application-settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="5e4b2-127">Input usage</span><span class="sxs-lookup"><span data-stu-id="5e4b2-127">Input usage</span></span>
<span data-ttu-id="5e4b2-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="5e4b2-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span><span class="sxs-lookup"><span data-stu-id="5e4b2-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="5e4b2-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="5e4b2-131">The input data can be deserialized in Node.js or C# functions.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="5e4b2-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="5e4b2-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="5e4b2-134">Any type that implements `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="5e4b2-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="5e4b2-135">Input sample</span><span class="sxs-lookup"><span data-stu-id="5e4b2-135">Input sample</span></span>
<span data-ttu-id="5e4b2-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="5e4b2-137">The JSON specifies `PartitionKey` 
`RowKey`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="5e4b2-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
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
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="5e4b2-139">See the language-specific sample that reads a single table entity.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="5e4b2-140">C#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="5e4b2-141">F#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="5e4b2-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="5e4b2-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="5e4b2-143">Input sample in C#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-143">Input sample in C#</span></span> #
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

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="5e4b2-144">Input sample in F#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-144">Input sample in F#</span></span> #
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

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="5e4b2-145">Input sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="5e4b2-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="5e4b2-146">Storage table output binding</span><span class="sxs-lookup"><span data-stu-id="5e4b2-146">Storage table output binding</span></span>
<span data-ttu-id="5e4b2-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="5e4b2-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="5e4b2-149">Note the following:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-149">Note the following:</span></span> 

* <span data-ttu-id="5e4b2-150">Use `partitionKey` and `rowKey` together to write a single entity.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="5e4b2-151">These properties are optional.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-151">These properties are optional.</span></span> <span data-ttu-id="5e4b2-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="5e4b2-153">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="5e4b2-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="5e4b2-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#application-settings).</span><span class="sxs-lookup"><span data-stu-id="5e4b2-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#application-settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="5e4b2-156">Output usage</span><span class="sxs-lookup"><span data-stu-id="5e4b2-156">Output usage</span></span>
<span data-ttu-id="5e4b2-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span><span class="sxs-lookup"><span data-stu-id="5e4b2-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="5e4b2-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="5e4b2-159">You can serialize objects in Node.js or C# functions.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="5e4b2-160">In C# functions, you can also bind to the following types:</span><span class="sxs-lookup"><span data-stu-id="5e4b2-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="5e4b2-161">Any type that implements `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="5e4b2-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="5e4b2-162">`ICollector<T>` (to output multiple entities.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="5e4b2-163">See [sample](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="5e4b2-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="5e4b2-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="5e4b2-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="5e4b2-165">`CloudTable` (using the Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="5e4b2-166">See [sample](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="5e4b2-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="5e4b2-167">Output sample</span><span class="sxs-lookup"><span data-stu-id="5e4b2-167">Output sample</span></span>
<span data-ttu-id="5e4b2-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

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
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="5e4b2-169">See the language-specific sample that creates multiple table entities.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="5e4b2-170">C#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="5e4b2-171">F#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="5e4b2-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="5e4b2-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="5e4b2-173">Output sample in C#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-173">Output sample in C#</span></span> #
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
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="5e4b2-174">Output sample in F#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-174">Output sample in F#</span></span> #
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

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="5e4b2-175">Output sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="5e4b2-175">Output sample in Node.js</span></span>
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

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="5e4b2-176">Sample: Read multiple table entities in C#</span><span class="sxs-lookup"><span data-stu-id="5e4b2-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="5e4b2-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="5e4b2-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="5e4b2-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5e4b2-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e4b2-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

