---
title: Azure Functions External File bindings (Preview) | Microsoft Docs
description: Using External File bindings in Azure Functions
services: functions
documentationcenter: ''
author: alexkarcher-msft
manager: erikre
editor: ''
ms.assetid: ''
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 1ab9b7e306fda89235f4e9388fdbae4ea54307df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563774"
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="6b1c9-103">Azure Functions External File bindings (Preview)</span><span class="sxs-lookup"><span data-stu-id="6b1c9-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="6b1c9-104">This article explains how to configure and use external file bindings in Azure functions.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-104">This article explains how to configure and use external file bindings in Azure functions.</span></span> <span data-ttu-id="6b1c9-105">Azure functions supports trigger, input, and output bindings for external file.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="6b1c9-106">External file bindings allow functions to access files hosted outside of Azure.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-106">External file bindings allow functions to access files hosted outside of Azure.</span></span> <span data-ttu-id="6b1c9-107">This binding creates new API connections, or uses existing API connections from your Function App's resource group.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-107">This binding creates new API connections, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="6b1c9-108">Supported File connections</span><span class="sxs-lookup"><span data-stu-id="6b1c9-108">Supported File connections</span></span>

|<span data-ttu-id="6b1c9-109">Connector</span><span class="sxs-lookup"><span data-stu-id="6b1c9-109">Connector</span></span>|<span data-ttu-id="6b1c9-110">Trigger</span><span class="sxs-lookup"><span data-stu-id="6b1c9-110">Trigger</span></span>|<span data-ttu-id="6b1c9-111">Input</span><span class="sxs-lookup"><span data-stu-id="6b1c9-111">Input</span></span>|<span data-ttu-id="6b1c9-112">Output</span><span class="sxs-lookup"><span data-stu-id="6b1c9-112">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="6b1c9-113">Box</span><span class="sxs-lookup"><span data-stu-id="6b1c9-113">Box</span></span>](https://www.box.com)|<span data-ttu-id="6b1c9-114">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-114">x</span></span>|<span data-ttu-id="6b1c9-115">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-115">x</span></span>|<span data-ttu-id="6b1c9-116">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-116">x</span></span>
|[<span data-ttu-id="6b1c9-117">Dropbox</span><span class="sxs-lookup"><span data-stu-id="6b1c9-117">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="6b1c9-118">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-118">x</span></span>|<span data-ttu-id="6b1c9-119">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-119">x</span></span>|<span data-ttu-id="6b1c9-120">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-120">x</span></span>
|[<span data-ttu-id="6b1c9-121">File System</span><span class="sxs-lookup"><span data-stu-id="6b1c9-121">File System</span></span>](https://docs.microsoft.com/azure/logic-apps/logic-apps-using-file-connector)|<span data-ttu-id="6b1c9-122">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-122">x</span></span>|<span data-ttu-id="6b1c9-123">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-123">x</span></span>|<span data-ttu-id="6b1c9-124">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-124">x</span></span>
|[<span data-ttu-id="6b1c9-125">FTP</span><span class="sxs-lookup"><span data-stu-id="6b1c9-125">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="6b1c9-126">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-126">x</span></span>|<span data-ttu-id="6b1c9-127">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-127">x</span></span>|<span data-ttu-id="6b1c9-128">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-128">x</span></span>
|[<span data-ttu-id="6b1c9-129">OneDrive</span><span class="sxs-lookup"><span data-stu-id="6b1c9-129">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="6b1c9-130">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-130">x</span></span>|<span data-ttu-id="6b1c9-131">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-131">x</span></span>|<span data-ttu-id="6b1c9-132">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-132">x</span></span>
|[<span data-ttu-id="6b1c9-133">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="6b1c9-133">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="6b1c9-134">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-134">x</span></span>|<span data-ttu-id="6b1c9-135">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-135">x</span></span>|<span data-ttu-id="6b1c9-136">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-136">x</span></span>
|[<span data-ttu-id="6b1c9-137">SFTP</span><span class="sxs-lookup"><span data-stu-id="6b1c9-137">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="6b1c9-138">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-138">x</span></span>|<span data-ttu-id="6b1c9-139">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-139">x</span></span>|<span data-ttu-id="6b1c9-140">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-140">x</span></span>
|[<span data-ttu-id="6b1c9-141">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="6b1c9-141">Azure Blob Storage</span></span>](https://azure.microsoft.com/services/storage/blobs/)||<span data-ttu-id="6b1c9-142">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-142">x</span></span>|<span data-ttu-id="6b1c9-143">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-143">x</span></span>|
|[<span data-ttu-id="6b1c9-144">Google Drive</span><span class="sxs-lookup"><span data-stu-id="6b1c9-144">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="6b1c9-145">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-145">x</span></span>|<span data-ttu-id="6b1c9-146">x</span><span class="sxs-lookup"><span data-stu-id="6b1c9-146">x</span></span>|

> [!NOTE]
> <span data-ttu-id="6b1c9-147">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="6b1c9-147">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="6b1c9-148">External File trigger binding</span><span class="sxs-lookup"><span data-stu-id="6b1c9-148">External File trigger binding</span></span>

<span data-ttu-id="6b1c9-149">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-149">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="6b1c9-150">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span><span class="sxs-lookup"><span data-stu-id="6b1c9-150">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="6b1c9-151">Name patterns</span><span class="sxs-lookup"><span data-stu-id="6b1c9-151">Name patterns</span></span>
<span data-ttu-id="6b1c9-152">You can specify a file name pattern in the `path` property.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-152">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="6b1c9-153">For example:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-153">For example:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="6b1c9-154">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1`.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-154">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1`.</span></span>

<span data-ttu-id="6b1c9-155">Another example:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-155">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="6b1c9-156">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-156">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="6b1c9-157">You can restrict the file type of files by using a fixed value for the file extension.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-157">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="6b1c9-158">For example:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-158">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="6b1c9-159">In this case, only *.png* files in the *samples* folder trigger the function.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-159">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="6b1c9-160">Curly braces are special characters in name patterns.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-160">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="6b1c9-161">To specify file names that have curly braces in the name, double the curly braces.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-161">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="6b1c9-162">For example:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-162">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="6b1c9-163">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-163">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="6b1c9-164">Handling poison files</span><span class="sxs-lookup"><span data-stu-id="6b1c9-164">Handling poison files</span></span>
<span data-ttu-id="6b1c9-165">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-165">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="6b1c9-166">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-166">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="6b1c9-167">The queue message for poison files is a JSON object that contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-167">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="6b1c9-168">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span><span class="sxs-lookup"><span data-stu-id="6b1c9-168">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="6b1c9-169">FileType</span><span class="sxs-lookup"><span data-stu-id="6b1c9-169">FileType</span></span>
* <span data-ttu-id="6b1c9-170">FolderName</span><span class="sxs-lookup"><span data-stu-id="6b1c9-170">FolderName</span></span>
* <span data-ttu-id="6b1c9-171">FileName</span><span class="sxs-lookup"><span data-stu-id="6b1c9-171">FileName</span></span>
* <span data-ttu-id="6b1c9-172">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6b1c9-172">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="6b1c9-173">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="6b1c9-173">Trigger usage</span></span>
<span data-ttu-id="6b1c9-174">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-174">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6b1c9-175">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="6b1c9-175">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="6b1c9-176">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-176">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6b1c9-177">The file can be deserialized into any of the following types:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-177">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="6b1c9-178">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-178">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6b1c9-179">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-179">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="6b1c9-180">String - useful for text file data.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-180">String - useful for text file data.</span></span>

<span data-ttu-id="6b1c9-181">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-181">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="6b1c9-182">Other types deserialized by [ICloudBlobStreamBinder](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md#icbsb)</span><span class="sxs-lookup"><span data-stu-id="6b1c9-182">Other types deserialized by [ICloudBlobStreamBinder](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md#icbsb)</span></span>


## <a name="trigger-sample"></a><span data-ttu-id="6b1c9-183">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="6b1c9-183">Trigger sample</span></span>
<span data-ttu-id="6b1c9-184">Suppose you have the following function.json, that defines an external file trigger:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-184">Suppose you have the following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="6b1c9-185">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-185">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="6b1c9-186">C#</span><span class="sxs-lookup"><span data-stu-id="6b1c9-186">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="6b1c9-187">Node.js</span><span class="sxs-lookup"><span data-stu-id="6b1c9-187">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="6b1c9-188">Trigger usage in C#</span><span class="sxs-lookup"><span data-stu-id="6b1c9-188">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="6b1c9-189">Trigger usage in Node.js</span><span class="sxs-lookup"><span data-stu-id="6b1c9-189">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="6b1c9-190">External File input binding</span><span class="sxs-lookup"><span data-stu-id="6b1c9-190">External File input binding</span></span>
<span data-ttu-id="6b1c9-191">The Azure external file input binding enables you to use a file from an external folder in your function.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-191">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="6b1c9-192">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-192">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="6b1c9-193">Note the following:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-193">Note the following:</span></span>

* <span data-ttu-id="6b1c9-194">`path` must contain the folder name and the file name.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-194">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="6b1c9-195">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-195">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6b1c9-196">Input usage</span><span class="sxs-lookup"><span data-stu-id="6b1c9-196">Input usage</span></span>
<span data-ttu-id="6b1c9-197">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-197">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6b1c9-198">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span><span class="sxs-lookup"><span data-stu-id="6b1c9-198">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="6b1c9-199">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-199">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6b1c9-200">The file can be deserialized into any of the following types:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-200">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="6b1c9-201">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-201">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6b1c9-202">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-202">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="6b1c9-203">String - useful for text file data.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-203">String - useful for text file data.</span></span>

<span data-ttu-id="6b1c9-204">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-204">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="6b1c9-205">Input sample</span><span class="sxs-lookup"><span data-stu-id="6b1c9-205">Input sample</span></span>
<span data-ttu-id="6b1c9-206">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), n external file input, and an external file output:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-206">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), n external file input, and an external file output:</span></span>

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="6b1c9-207">See the language-specific sample that copies the input file to the output file.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-207">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="6b1c9-208">C#</span><span class="sxs-lookup"><span data-stu-id="6b1c9-208">C#</span></span>](#incsharp)
* [<span data-ttu-id="6b1c9-209">Node.js</span><span class="sxs-lookup"><span data-stu-id="6b1c9-209">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="input-usage-in-c"></a><span data-ttu-id="6b1c9-210">Input usage in C#</span><span class="sxs-lookup"><span data-stu-id="6b1c9-210">Input usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="input-usage-in-nodejs"></a><span data-ttu-id="6b1c9-211">Input usage in Node.js</span><span class="sxs-lookup"><span data-stu-id="6b1c9-211">Input usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="6b1c9-212">External File output binding</span><span class="sxs-lookup"><span data-stu-id="6b1c9-212">External File output binding</span></span>
<span data-ttu-id="6b1c9-213">The Azure external file output binding enables you to write files to an external folder in your function.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-213">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="6b1c9-214">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-214">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="6b1c9-215">Note the following:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-215">Note the following:</span></span>

* <span data-ttu-id="6b1c9-216">`path` must contain the folder name and the file name to write to.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-216">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="6b1c9-217">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-217">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6b1c9-218">Output usage</span><span class="sxs-lookup"><span data-stu-id="6b1c9-218">Output usage</span></span>
<span data-ttu-id="6b1c9-219">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span><span class="sxs-lookup"><span data-stu-id="6b1c9-219">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="6b1c9-220">In Node.js functions, you access the output file using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-220">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6b1c9-221">You can write to the output file using any of the following types:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-221">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="6b1c9-222">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-222">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="6b1c9-223">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-223">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="6b1c9-224">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-224">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="6b1c9-225">String - (`out string paramName`) useful for text file data.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-225">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="6b1c9-226">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span><span class="sxs-lookup"><span data-stu-id="6b1c9-226">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="6b1c9-227">In C# functions you can also output to any of the following types:</span><span class="sxs-lookup"><span data-stu-id="6b1c9-227">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="6b1c9-228">Output sample</span><span class="sxs-lookup"><span data-stu-id="6b1c9-228">Output sample</span></span>
<span data-ttu-id="6b1c9-229">See [input sample](#inputsample).</span><span class="sxs-lookup"><span data-stu-id="6b1c9-229">See [input sample](#inputsample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b1c9-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b1c9-230">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
