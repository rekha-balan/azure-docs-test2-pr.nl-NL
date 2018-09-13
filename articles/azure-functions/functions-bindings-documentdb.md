---
title: Azure Functions DocumentDB bindings | Microsoft Docs
description: Understand how to use Azure DocumentDB bindings in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/10/2016
ms.author: chrande; glenga
ms.openlocfilehash: 2ac78606f851068fa0fb7dcab3bac1c629b9cdb3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552105"
---
# <a name="azure-functions-documentdb-bindings"></a><span data-ttu-id="94cc9-104">Azure Functions DocumentDB bindings</span><span class="sxs-lookup"><span data-stu-id="94cc9-104">Azure Functions DocumentDB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="94cc9-105">This article explains how to configure and code Azure DocumentDB bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="94cc9-105">This article explains how to configure and code Azure DocumentDB bindings in Azure Functions.</span></span> <span data-ttu-id="94cc9-106">Azure Functions supports input and output bindings for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="94cc9-106">Azure Functions supports input and output bindings for DocumentDB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="94cc9-107">For more information on DocumentDB, see [Introduction to DocumentDB](../documentdb/documentdb-introduction.md) and [Build a DocumentDB console application](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="94cc9-107">For more information on DocumentDB, see [Introduction to DocumentDB](../documentdb/documentdb-introduction.md) and [Build a DocumentDB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-input-binding"></a><span data-ttu-id="94cc9-108">DocumentDB input binding</span><span class="sxs-lookup"><span data-stu-id="94cc9-108">DocumentDB input binding</span></span>
<span data-ttu-id="94cc9-109">The DocumentDB input binding retrieves a DocumentDB document and passes it to the named input parameter of the function.</span><span class="sxs-lookup"><span data-stu-id="94cc9-109">The DocumentDB input binding retrieves a DocumentDB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="94cc9-110">The document ID can be determined based on the trigger that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="94cc9-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="94cc9-111">The DocumentDB input to a function uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="94cc9-111">The DocumentDB input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "documentDB",
  "databaseName": "<Name of the DocumentDB database>",
  "collectionName": "<Name of the DocumentDB collection>",
  "id": "<Id of the DocumentDB document - see below>",
  "connection": "<Name of app setting with connection string - see below>",
  "direction": "in"
},
```

<span data-ttu-id="94cc9-112">Note the following:</span><span class="sxs-lookup"><span data-stu-id="94cc9-112">Note the following:</span></span>

* <span data-ttu-id="94cc9-113">`id` supports bindings similar to `{queueTrigger}`, which uses the string value of the queue message as the document Id.</span><span class="sxs-lookup"><span data-stu-id="94cc9-113">`id` supports bindings similar to `{queueTrigger}`, which uses the string value of the queue message as the document Id.</span></span>
* <span data-ttu-id="94cc9-114">`connection` must be the name of an app setting that points to the endpoint for your DocumentDB account (with the value `AccountEndpoint=<Endpoint for your account>;AccountKey=<Your primary access key>`).</span><span class="sxs-lookup"><span data-stu-id="94cc9-114">`connection` must be the name of an app setting that points to the endpoint for your DocumentDB account (with the value `AccountEndpoint=<Endpoint for your account>;AccountKey=<Your primary access key>`).</span></span> <span data-ttu-id="94cc9-115">If you create a DocumentDB account through the Functions portal UI, the account creation process creates an app setting for you.</span><span class="sxs-lookup"><span data-stu-id="94cc9-115">If you create a DocumentDB account through the Functions portal UI, the account creation process creates an app setting for you.</span></span> <span data-ttu-id="94cc9-116">To use an existing DocumentDB account, you need to [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="94cc9-116">To use an existing DocumentDB account, you need to [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span></span> 
* <span data-ttu-id="94cc9-117">If the specified document is not found, the named input parameter to the function is set to `null`.</span><span class="sxs-lookup"><span data-stu-id="94cc9-117">If the specified document is not found, the named input parameter to the function is set to `null`.</span></span> 

## <a name="input-usage"></a><span data-ttu-id="94cc9-118">Input usage</span><span class="sxs-lookup"><span data-stu-id="94cc9-118">Input usage</span></span>
<span data-ttu-id="94cc9-119">This section shows you how to use your DocumentDB input binding in your function code.</span><span class="sxs-lookup"><span data-stu-id="94cc9-119">This section shows you how to use your DocumentDB input binding in your function code.</span></span>

<span data-ttu-id="94cc9-120">In C# and F# functions, any changes made to the input document (named input parameter) is automatically sent back to the collection when the function exits successfully.</span><span class="sxs-lookup"><span data-stu-id="94cc9-120">In C# and F# functions, any changes made to the input document (named input parameter) is automatically sent back to the collection when the function exits successfully.</span></span> <span data-ttu-id="94cc9-121">In Node.js functions, updates to the document in the input binding are not sent back to the collection.</span><span class="sxs-lookup"><span data-stu-id="94cc9-121">In Node.js functions, updates to the document in the input binding are not sent back to the collection.</span></span> <span data-ttu-id="94cc9-122">However, you can use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates to input documents.</span><span class="sxs-lookup"><span data-stu-id="94cc9-122">However, you can use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates to input documents.</span></span> <span data-ttu-id="94cc9-123">See how it is done in the [Node.js sample](#innodejs).</span><span class="sxs-lookup"><span data-stu-id="94cc9-123">See how it is done in the [Node.js sample](#innodejs).</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="94cc9-124">Input sample</span><span class="sxs-lookup"><span data-stu-id="94cc9-124">Input sample</span></span>
<span data-ttu-id="94cc9-125">Suppose you have the following DocumentDB input binding in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="94cc9-125">Suppose you have the following DocumentDB input binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_DOCUMENTDB",     
  "direction": "in"
}
```

<span data-ttu-id="94cc9-126">See the language-specific sample that uses this input binding to update the document's text value.</span><span class="sxs-lookup"><span data-stu-id="94cc9-126">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="94cc9-127">C#</span><span class="sxs-lookup"><span data-stu-id="94cc9-127">C#</span></span>](#incsharp)
* [<span data-ttu-id="94cc9-128">F#</span><span class="sxs-lookup"><span data-stu-id="94cc9-128">F#</span></span>](#infsharp)
* [<span data-ttu-id="94cc9-129">Node.js</span><span class="sxs-lookup"><span data-stu-id="94cc9-129">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="94cc9-130">Input sample in C#</span><span class="sxs-lookup"><span data-stu-id="94cc9-130">Input sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="94cc9-131">Input sample in F#</span><span class="sxs-lookup"><span data-stu-id="94cc9-131">Input sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="94cc9-132">You need to add a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span><span class="sxs-lookup"><span data-stu-id="94cc9-132">You need to add a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="94cc9-133">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="94cc9-133">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="innodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="94cc9-134">Input sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="94cc9-134">Input sample in Node.js</span></span>

```javascript
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a id="docdboutput"></a><span data-ttu-id="94cc9-135">DocumentDB output binding</span><span class="sxs-lookup"><span data-stu-id="94cc9-135">DocumentDB output binding</span></span>
<span data-ttu-id="94cc9-136">The DocumentDB output binding lets you write a new document to an Azure DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="94cc9-136">The DocumentDB output binding lets you write a new document to an Azure DocumentDB database.</span></span> 

<span data-ttu-id="94cc9-137">The output binding uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="94cc9-137">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span> 

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "documentDB",
  "databaseName": "<Name of the DocumentDB database>",
  "collectionName": "<Name of the DocumentDB collection>",
  "createIfNotExists": <true or false - see below>,
  "connection": "<Value of AccountEndpoint in Application Setting - see below>",
  "direction": "out"
}
```

<span data-ttu-id="94cc9-138">Note the following:</span><span class="sxs-lookup"><span data-stu-id="94cc9-138">Note the following:</span></span>

* <span data-ttu-id="94cc9-139">Set `createIfNotExists` to `true` to create the database and collection if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="94cc9-139">Set `createIfNotExists` to `true` to create the database and collection if it doesn't exist.</span></span> <span data-ttu-id="94cc9-140">The default value is `false`.</span><span class="sxs-lookup"><span data-stu-id="94cc9-140">The default value is `false`.</span></span> <span data-ttu-id="94cc9-141">New collections are created with reserved throughput, which has pricing implications.</span><span class="sxs-lookup"><span data-stu-id="94cc9-141">New collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="94cc9-142">For more information, see [DocumentDB pricing](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="94cc9-142">For more information, see [DocumentDB pricing](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
* <span data-ttu-id="94cc9-143">`connection` must be the name of an app setting that points to the endpoint for your DocumentDB account (with the value `AccountEndpoint=<Endpoint for your account>;AccountKey=<Your primary access key>`).</span><span class="sxs-lookup"><span data-stu-id="94cc9-143">`connection` must be the name of an app setting that points to the endpoint for your DocumentDB account (with the value `AccountEndpoint=<Endpoint for your account>;AccountKey=<Your primary access key>`).</span></span> <span data-ttu-id="94cc9-144">If you create a DocumentDB account through the Functions portal UI, the account creation process creates a new app setting for you.</span><span class="sxs-lookup"><span data-stu-id="94cc9-144">If you create a DocumentDB account through the Functions portal UI, the account creation process creates a new app setting for you.</span></span> <span data-ttu-id="94cc9-145">To use an existing DocumentDB account, you need to [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="94cc9-145">To use an existing DocumentDB account, you need to [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span></span> 

## <a name="output-usage"></a><span data-ttu-id="94cc9-146">Output usage</span><span class="sxs-lookup"><span data-stu-id="94cc9-146">Output usage</span></span>
<span data-ttu-id="94cc9-147">This section shows you how to use your DocumentDB output binding in your function code.</span><span class="sxs-lookup"><span data-stu-id="94cc9-147">This section shows you how to use your DocumentDB output binding in your function code.</span></span>

<span data-ttu-id="94cc9-148">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span><span class="sxs-lookup"><span data-stu-id="94cc9-148">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="94cc9-149">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span><span class="sxs-lookup"><span data-stu-id="94cc9-149">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="94cc9-150">When you specify the ID of an existing document, it gets overwritten by the new output document.</span><span class="sxs-lookup"><span data-stu-id="94cc9-150">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="94cc9-151">You can write to the output using any of the following types:</span><span class="sxs-lookup"><span data-stu-id="94cc9-151">You can write to the output using any of the following types:</span></span>

* <span data-ttu-id="94cc9-152">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span><span class="sxs-lookup"><span data-stu-id="94cc9-152">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="94cc9-153">If you declare a custom output type (e.g. `out FooType paramName`), Azure Functions attempts to serialize object into JSON.</span><span class="sxs-lookup"><span data-stu-id="94cc9-153">If you declare a custom output type (e.g. `out FooType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="94cc9-154">If the output parameter is null when the function exits, the Functions runtime creates a blob as a null object.</span><span class="sxs-lookup"><span data-stu-id="94cc9-154">If the output parameter is null when the function exits, the Functions runtime creates a blob as a null object.</span></span>
* <span data-ttu-id="94cc9-155">String - (`out string paramName`) useful for text blob data.</span><span class="sxs-lookup"><span data-stu-id="94cc9-155">String - (`out string paramName`) useful for text blob data.</span></span> <span data-ttu-id="94cc9-156">the Functions runtime creates a blob only if the string parameter is non-null when the function exits.</span><span class="sxs-lookup"><span data-stu-id="94cc9-156">the Functions runtime creates a blob only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="94cc9-157">In C# functions you can also output to any of the following types:</span><span class="sxs-lookup"><span data-stu-id="94cc9-157">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<span data-ttu-id="94cc9-158">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span><span class="sxs-lookup"><span data-stu-id="94cc9-158">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>


<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="94cc9-159">Output sample</span><span class="sxs-lookup"><span data-stu-id="94cc9-159">Output sample</span></span>
<span data-ttu-id="94cc9-160">Suppose you have the following DocumentDB output binding in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="94cc9-160">Suppose you have the following DocumentDB output binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_DOCUMENTDB",     
  "direction": "out"
}
```

<span data-ttu-id="94cc9-161">And you have a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="94cc9-161">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="94cc9-162">And you want to create DocumentDB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="94cc9-162">And you want to create DocumentDB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="94cc9-163">See the language-specific sample that uses this output binding to add documents to your database.</span><span class="sxs-lookup"><span data-stu-id="94cc9-163">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="94cc9-164">C#</span><span class="sxs-lookup"><span data-stu-id="94cc9-164">C#</span></span>](#outcsharp)
* [<span data-ttu-id="94cc9-165">F#</span><span class="sxs-lookup"><span data-stu-id="94cc9-165">F#</span></span>](#outfsharp)
* [<span data-ttu-id="94cc9-166">Node.js</span><span class="sxs-lookup"><span data-stu-id="94cc9-166">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="94cc9-167">Output sample in C#</span><span class="sxs-lookup"><span data-stu-id="94cc9-167">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="94cc9-168">Output sample in F#</span><span class="sxs-lookup"><span data-stu-id="94cc9-168">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="94cc9-169">You need to add a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span><span class="sxs-lookup"><span data-stu-id="94cc9-169">You need to add a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="94cc9-170">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="94cc9-170">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="94cc9-171">Output sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="94cc9-171">Output sample in Node.js</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
