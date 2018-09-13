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
# <a name="azure-functions-documentdb-bindings"></a>Azure Functions DocumentDB bindings
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

This article explains how to configure and code Azure DocumentDB bindings in Azure Functions. Azure Functions supports input and output bindings for DocumentDB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

For more information on DocumentDB, see [Introduction to DocumentDB](../documentdb/documentdb-introduction.md) and [Build a DocumentDB console application](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-input-binding"></a>DocumentDB input binding
The DocumentDB input binding retrieves a DocumentDB document and passes it to the named input parameter of the function. The document ID can be determined based on the trigger that invokes the function. 

The DocumentDB input to a function uses the following JSON object in the `bindings` array of function.json:

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

Note the following:

* `id` supports bindings similar to `{queueTrigger}`, which uses the string value of the queue message as the document Id.
* `connection` must be the name of an app setting that points to the endpoint for your DocumentDB account (with the value `AccountEndpoint=<Endpoint for your account>;AccountKey=<Your primary access key>`). If you create a DocumentDB account through the Functions portal UI, the account creation process creates an app setting for you. To use an existing DocumentDB account, you need to [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md). 
* If the specified document is not found, the named input parameter to the function is set to `null`. 

## <a name="input-usage"></a>Input usage
This section shows you how to use your DocumentDB input binding in your function code.

In C# and F# functions, any changes made to the input document (named input parameter) is automatically sent back to the collection when the function exits successfully. In Node.js functions, updates to the document in the input binding are not sent back to the collection. However, you can use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates to input documents. See how it is done in the [Node.js sample](#innodejs).

<a name="inputsample"></a>

## <a name="input-sample"></a>Input sample
Suppose you have the following DocumentDB input binding in the `bindings` array of function.json:

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

See the language-specific sample that uses this input binding to update the document's text value.

* [C#](#incsharp)
* [F#](#infsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Input sample in C# #

```cs
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Input sample in F# #

```fsharp
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

You need to add a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:

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

To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).

<a name="innodejs"></a>

### <a name="input-sample-in-nodejs"></a>Input sample in Node.js

```javascript
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a id="docdboutput"></a>DocumentDB output binding
The DocumentDB output binding lets you write a new document to an Azure DocumentDB database. 

The output binding uses the following JSON object in the `bindings` array of function.json: 

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

Note the following:

* Set `createIfNotExists` to `true` to create the database and collection if it doesn't exist. The default value is `false`. New collections are created with reserved throughput, which has pricing implications. For more information, see [DocumentDB pricing](https://azure.microsoft.com/pricing/details/documentdb/).
* `connection` must be the name of an app setting that points to the endpoint for your DocumentDB account (with the value `AccountEndpoint=<Endpoint for your account>;AccountKey=<Your primary access key>`). If you create a DocumentDB account through the Functions portal UI, the account creation process creates a new app setting for you. To use an existing DocumentDB account, you need to [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md). 

## <a name="output-usage"></a>Output usage
This section shows you how to use your DocumentDB output binding in your function code.

When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID. You can specify the document ID of output document by specifying the `id` JSON property in the output parameter. 

>[!Note]  
>When you specify the ID of an existing document, it gets overwritten by the new output document. 

You can write to the output using any of the following types:

* Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.
  If you declare a custom output type (e.g. `out FooType paramName`), Azure Functions attempts to serialize object into JSON. If the output parameter is null when the function exits, the Functions runtime creates a blob as a null object.
* String - (`out string paramName`) useful for text blob data. the Functions runtime creates a blob only if the string parameter is non-null when the function exits.

In C# functions you can also output to any of the following types:

* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.


<a name="outputsample"></a>

## <a name="output-sample"></a>Output sample
Suppose you have the following DocumentDB output binding in the `bindings` array of function.json:

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

And you have a queue input binding for a queue that receives JSON in the following format:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

And you want to create DocumentDB documents in the following format for each record:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

See the language-specific sample that uses this output binding to add documents to your database.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Output sample in C# #

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

### <a name="output-sample-in-f"></a>Output sample in F# #

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

You need to add a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:

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

To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Output sample in Node.js

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
