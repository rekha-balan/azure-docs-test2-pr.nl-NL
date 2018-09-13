---
title: Azure Blob storage bindings for Azure Functions
description: Understand how to use Azure Blob storage triggers and bindings in Azure Functions.
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
ms.openlocfilehash: 9efe3c3d65dc1d809285eb760ca373c648ad66c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44829075"
---
# <a name="azure-blob-storage-bindings-for-azure-functions"></a><span data-ttu-id="83678-104">Azure Blob storage bindings for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="83678-104">Azure Blob storage bindings for Azure Functions</span></span>

<span data-ttu-id="83678-105">This article explains how to work with Azure Blob storage bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="83678-105">This article explains how to work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="83678-106">Azure Functions supports trigger, input, and output bindings for blobs.</span><span class="sxs-lookup"><span data-stu-id="83678-106">Azure Functions supports trigger, input, and output bindings for blobs.</span></span> <span data-ttu-id="83678-107">The article includes a section for each binding:</span><span class="sxs-lookup"><span data-stu-id="83678-107">The article includes a section for each binding:</span></span>

* [<span data-ttu-id="83678-108">Blob trigger</span><span class="sxs-lookup"><span data-stu-id="83678-108">Blob trigger</span></span>](#trigger)
* [<span data-ttu-id="83678-109">Blob input binding</span><span class="sxs-lookup"><span data-stu-id="83678-109">Blob input binding</span></span>](#input)
* [<span data-ttu-id="83678-110">Blob output binding</span><span class="sxs-lookup"><span data-stu-id="83678-110">Blob output binding</span></span>](#output)

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="83678-111">Use the Event Grid trigger instead of the Blob storage trigger for blob-only storage accounts, for high scale, or to avoid cold-start delays.</span><span class="sxs-lookup"><span data-stu-id="83678-111">Use the Event Grid trigger instead of the Blob storage trigger for blob-only storage accounts, for high scale, or to avoid cold-start delays.</span></span> <span data-ttu-id="83678-112">For more information, see the [Trigger](#trigger) section.</span><span class="sxs-lookup"><span data-stu-id="83678-112">For more information, see the [Trigger](#trigger) section.</span></span> 

## <a name="packages---functions-1x"></a><span data-ttu-id="83678-113">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="83678-113">Packages - Functions 1.x</span></span>

<span data-ttu-id="83678-114">The Blob storage bindings are provided in the [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) NuGet package, version 2.x.</span><span class="sxs-lookup"><span data-stu-id="83678-114">The Blob storage bindings are provided in the [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) NuGet package, version 2.x.</span></span> <span data-ttu-id="83678-115">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/v2.x/src/Microsoft.Azure.WebJobs.Storage/Blob) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="83678-115">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/v2.x/src/Microsoft.Azure.WebJobs.Storage/Blob) GitHub repository.</span></span>

[!INCLUDE [functions-package-auto](../../includes/functions-package-auto.md)]

[!INCLUDE [functions-storage-sdk-version](../../includes/functions-storage-sdk-version.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="83678-116">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="83678-116">Packages - Functions 2.x</span></span>

<span data-ttu-id="83678-117">The Blob storage bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="83678-117">The Blob storage bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage) NuGet package, version 3.x.</span></span> <span data-ttu-id="83678-118">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/dev/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="83678-118">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk/tree/dev/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="trigger"></a><span data-ttu-id="83678-119">Trigger</span><span class="sxs-lookup"><span data-stu-id="83678-119">Trigger</span></span>

<span data-ttu-id="83678-120">The Blob storage trigger starts a function when a new or updated blob is detected.</span><span class="sxs-lookup"><span data-stu-id="83678-120">The Blob storage trigger starts a function when a new or updated blob is detected.</span></span> <span data-ttu-id="83678-121">The blob contents are provided as input to the function.</span><span class="sxs-lookup"><span data-stu-id="83678-121">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="83678-122">The [Event Grid trigger](functions-bindings-event-grid.md) has built-in support for [blob events](../storage/blobs/storage-blob-event-overview.md) and can also be used to start a function when a new or updated blob is detected.</span><span class="sxs-lookup"><span data-stu-id="83678-122">The [Event Grid trigger](functions-bindings-event-grid.md) has built-in support for [blob events](../storage/blobs/storage-blob-event-overview.md) and can also be used to start a function when a new or updated blob is detected.</span></span> <span data-ttu-id="83678-123">For an example, see the [Image resize with Event Grid](../event-grid/resize-images-on-storage-blob-upload-event.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="83678-123">For an example, see the [Image resize with Event Grid](../event-grid/resize-images-on-storage-blob-upload-event.md) tutorial.</span></span>

<span data-ttu-id="83678-124">Use Event Grid instead of the Blob storage trigger for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="83678-124">Use Event Grid instead of the Blob storage trigger for the following scenarios:</span></span>

* <span data-ttu-id="83678-125">Blob-only storage accounts</span><span class="sxs-lookup"><span data-stu-id="83678-125">Blob-only storage accounts</span></span>
* <span data-ttu-id="83678-126">High scale</span><span class="sxs-lookup"><span data-stu-id="83678-126">High scale</span></span>
* <span data-ttu-id="83678-127">Minimizing cold-start delay</span><span class="sxs-lookup"><span data-stu-id="83678-127">Minimizing cold-start delay</span></span>

### <a name="blob-only-storage-accounts"></a><span data-ttu-id="83678-128">Blob-only storage accounts</span><span class="sxs-lookup"><span data-stu-id="83678-128">Blob-only storage accounts</span></span>

<span data-ttu-id="83678-129">[Blob-only storage accounts](../storage/common/storage-create-storage-account.md#blob-storage-accounts) are supported for blob input and output bindings but not for blob triggers.</span><span class="sxs-lookup"><span data-stu-id="83678-129">[Blob-only storage accounts](../storage/common/storage-create-storage-account.md#blob-storage-accounts) are supported for blob input and output bindings but not for blob triggers.</span></span> <span data-ttu-id="83678-130">Blob storage triggers require a general-purpose storage account.</span><span class="sxs-lookup"><span data-stu-id="83678-130">Blob storage triggers require a general-purpose storage account.</span></span>

### <a name="high-scale"></a><span data-ttu-id="83678-131">High scale</span><span class="sxs-lookup"><span data-stu-id="83678-131">High scale</span></span>

<span data-ttu-id="83678-132">High scale can be loosely defined as containers that have more than 100,000 blobs in them or storage accounts that have more than 100 blob updates per second.</span><span class="sxs-lookup"><span data-stu-id="83678-132">High scale can be loosely defined as containers that have more than 100,000 blobs in them or storage accounts that have more than 100 blob updates per second.</span></span>

### <a name="cold-start-delay"></a><span data-ttu-id="83678-133">Cold-start delay</span><span class="sxs-lookup"><span data-stu-id="83678-133">Cold-start delay</span></span>

<span data-ttu-id="83678-134">If your function app is on the Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle.</span><span class="sxs-lookup"><span data-stu-id="83678-134">If your function app is on the Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle.</span></span> <span data-ttu-id="83678-135">To avoid this cold-start delay, you can switch to an App Service plan with Always On enabled, or use a different trigger type.</span><span class="sxs-lookup"><span data-stu-id="83678-135">To avoid this cold-start delay, you can switch to an App Service plan with Always On enabled, or use a different trigger type.</span></span>

### <a name="queue-storage-trigger"></a><span data-ttu-id="83678-136">Queue storage trigger</span><span class="sxs-lookup"><span data-stu-id="83678-136">Queue storage trigger</span></span>

<span data-ttu-id="83678-137">Besides Event Grid, another alternative for processing blobs is the Queue storage trigger, but it has no built-in support for blob events.</span><span class="sxs-lookup"><span data-stu-id="83678-137">Besides Event Grid, another alternative for processing blobs is the Queue storage trigger, but it has no built-in support for blob events.</span></span> <span data-ttu-id="83678-138">You would have to create queue messages when creating or updating blobs.</span><span class="sxs-lookup"><span data-stu-id="83678-138">You would have to create queue messages when creating or updating blobs.</span></span> <span data-ttu-id="83678-139">For an example that assumes you've done that, see the [blob input binding example later in this article](#input---example).</span><span class="sxs-lookup"><span data-stu-id="83678-139">For an example that assumes you've done that, see the [blob input binding example later in this article](#input---example).</span></span>

## <a name="trigger---example"></a><span data-ttu-id="83678-140">Trigger - example</span><span class="sxs-lookup"><span data-stu-id="83678-140">Trigger - example</span></span>

<span data-ttu-id="83678-141">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="83678-141">See the language-specific example:</span></span>

* [<span data-ttu-id="83678-142">C#</span><span class="sxs-lookup"><span data-stu-id="83678-142">C#</span></span>](#trigger---c-example)
* [<span data-ttu-id="83678-143">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="83678-143">C# script (.csx)</span></span>](#trigger---c-script-example)
* [<span data-ttu-id="83678-144">JavaScript</span><span class="sxs-lookup"><span data-stu-id="83678-144">JavaScript</span></span>](#trigger---javascript-example)
* [<span data-ttu-id="83678-145">Java</span><span class="sxs-lookup"><span data-stu-id="83678-145">Java</span></span>](#trigger---javascript-example)

### <a name="trigger---c-example"></a><span data-ttu-id="83678-146">Trigger - C# example</span><span class="sxs-lookup"><span data-stu-id="83678-146">Trigger - C# example</span></span>

<span data-ttu-id="83678-147">The following example shows a [C# function](functions-dotnet-class-library.md) that writes a log when a blob is added or updated in the `samples-workitems` container.</span><span class="sxs-lookup"><span data-stu-id="83678-147">The following example shows a [C# function](functions-dotnet-class-library.md) that writes a log when a blob is added or updated in the `samples-workitems` container.</span></span>

```csharp
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="83678-148">The string `{name}` in the blob trigger path `samples-workitems/{name}` creates a [binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns) that you can use in function code to access the file name of the triggering blob.</span><span class="sxs-lookup"><span data-stu-id="83678-148">The string `{name}` in the blob trigger path `samples-workitems/{name}` creates a [binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns) that you can use in function code to access the file name of the triggering blob.</span></span> <span data-ttu-id="83678-149">For more information, see [Blob name patterns](#trigger---blob-name-patterns) later in this article.</span><span class="sxs-lookup"><span data-stu-id="83678-149">For more information, see [Blob name patterns](#trigger---blob-name-patterns) later in this article.</span></span>

<span data-ttu-id="83678-150">For more information about the `BlobTrigger` attribute, see [Trigger - attributes](#trigger---attributes).</span><span class="sxs-lookup"><span data-stu-id="83678-150">For more information about the `BlobTrigger` attribute, see [Trigger - attributes](#trigger---attributes).</span></span>

### <a name="trigger---c-script-example"></a><span data-ttu-id="83678-151">Trigger - C# script example</span><span class="sxs-lookup"><span data-stu-id="83678-151">Trigger - C# script example</span></span>

<span data-ttu-id="83678-152">The following example shows a blob trigger binding in a *function.json* file and [C# script (.csx)](functions-reference-csharp.md) code that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="83678-152">The following example shows a blob trigger binding in a *function.json* file and [C# script (.csx)](functions-reference-csharp.md) code that uses the binding.</span></span> <span data-ttu-id="83678-153">The function writes a log when a blob is added or updated in the `samples-workitems` container.</span><span class="sxs-lookup"><span data-stu-id="83678-153">The function writes a log when a blob is added or updated in the `samples-workitems` container.</span></span>

<span data-ttu-id="83678-154">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="83678-154">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems/{name}",
            "connection":"MyStorageAccountAppSetting"
        }
    ]
}
```

<span data-ttu-id="83678-155">The string `{name}` in the blob trigger path `samples-workitems/{name}` creates a [binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns) that you can use in function code to access the file name of the triggering blob.</span><span class="sxs-lookup"><span data-stu-id="83678-155">The string `{name}` in the blob trigger path `samples-workitems/{name}` creates a [binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns) that you can use in function code to access the file name of the triggering blob.</span></span> <span data-ttu-id="83678-156">For more information, see [Blob name patterns](#trigger---blob-name-patterns) later in this article.</span><span class="sxs-lookup"><span data-stu-id="83678-156">For more information, see [Blob name patterns](#trigger---blob-name-patterns) later in this article.</span></span>

<span data-ttu-id="83678-157">For more information about *function.json* file properties, see the [Configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="83678-157">For more information about *function.json* file properties, see the [Configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="83678-158">Here's C# script code that binds to a `Stream`:</span><span class="sxs-lookup"><span data-stu-id="83678-158">Here's C# script code that binds to a `Stream`:</span></span>

```cs
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="83678-159">Here's C# script code that binds to a `CloudBlockBlob`:</span><span class="sxs-lookup"><span data-stu-id="83678-159">Here's C# script code that binds to a `CloudBlockBlob`:</span></span>

```cs
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

### <a name="trigger---javascript-example"></a><span data-ttu-id="83678-160">Trigger - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="83678-160">Trigger - JavaScript example</span></span>

<span data-ttu-id="83678-161">The following example shows a blob trigger binding in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="83678-161">The following example shows a blob trigger binding in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="83678-162">The function writes a log when a blob is added or updated in the `samples-workitems` container.</span><span class="sxs-lookup"><span data-stu-id="83678-162">The function writes a log when a blob is added or updated in the `samples-workitems` container.</span></span>

<span data-ttu-id="83678-163">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="83678-163">Here's the *function.json* file:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems/{name}",
            "connection":"MyStorageAccountAppSetting"
        }
    ]
}
```

<span data-ttu-id="83678-164">The string `{name}` in the blob trigger path `samples-workitems/{name}` creates a [binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns) that you can use in function code to access the file name of the triggering blob.</span><span class="sxs-lookup"><span data-stu-id="83678-164">The string `{name}` in the blob trigger path `samples-workitems/{name}` creates a [binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns) that you can use in function code to access the file name of the triggering blob.</span></span> <span data-ttu-id="83678-165">For more information, see [Blob name patterns](#trigger---blob-name-patterns) later in this article.</span><span class="sxs-lookup"><span data-stu-id="83678-165">For more information, see [Blob name patterns](#trigger---blob-name-patterns) later in this article.</span></span>

<span data-ttu-id="83678-166">For more information about *function.json* file properties, see the [Configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="83678-166">For more information about *function.json* file properties, see the [Configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="83678-167">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="83678-167">Here's the JavaScript code:</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```

### <a name="trigger---java-example"></a><span data-ttu-id="83678-168">Trigger - Java example</span><span class="sxs-lookup"><span data-stu-id="83678-168">Trigger - Java example</span></span>

<span data-ttu-id="83678-169">The following example shows a blob trigger binding in a *function.json* file and [Java code](functions-reference-java.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="83678-169">The following example shows a blob trigger binding in a *function.json* file and [Java code](functions-reference-java.md) that uses the binding.</span></span> <span data-ttu-id="83678-170">The function writes a log when a blob is added or updated in the `myblob` container.</span><span class="sxs-lookup"><span data-stu-id="83678-170">The function writes a log when a blob is added or updated in the `myblob` container.</span></span>

<span data-ttu-id="83678-171">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="83678-171">Here's the *function.json* file:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "file",
            "type": "blobTrigger",
            "direction": "in",
            "path": "myblob/{name}",
            "connection":"MyStorageAccountAppSetting"
        }
    ]
}
```

<span data-ttu-id="83678-172">Here's the Java code:</span><span class="sxs-lookup"><span data-stu-id="83678-172">Here's the Java code:</span></span>

```java
 @FunctionName("blobprocessor")
 public void run(
    @BlobTrigger(name = "file",
                  dataType = "binary",
                  path = "myblob/filepath",
                  connection = "myconnvarname") byte[] content,
    @BindingName("name") String filename,
     final ExecutionContext context
 ) {
     context.getLogger().info("Name: " + name + " Size: " + content.length + " bytes");
 }

```


## <a name="trigger---attributes"></a><span data-ttu-id="83678-173">Trigger - attributes</span><span class="sxs-lookup"><span data-stu-id="83678-173">Trigger - attributes</span></span>

<span data-ttu-id="83678-174">In [C# class libraries](functions-dotnet-class-library.md), use the following attributes to configure a blob trigger:</span><span class="sxs-lookup"><span data-stu-id="83678-174">In [C# class libraries](functions-dotnet-class-library.md), use the following attributes to configure a blob trigger:</span></span>

* [<span data-ttu-id="83678-175">BlobTriggerAttribute</span><span class="sxs-lookup"><span data-stu-id="83678-175">BlobTriggerAttribute</span></span>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobTriggerAttribute.cs)

  <span data-ttu-id="83678-176">The attribute's constructor takes a path string that indicates the container to watch and optionally a [blob name pattern](#trigger---blob-name-patterns).</span><span class="sxs-lookup"><span data-stu-id="83678-176">The attribute's constructor takes a path string that indicates the container to watch and optionally a [blob name pattern](#trigger---blob-name-patterns).</span></span> <span data-ttu-id="83678-177">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="83678-177">Here's an example:</span></span>

  ```csharp
  [FunctionName("ResizeImage")]
  public static void Run(
      [BlobTrigger("sample-images/{name}")] Stream image, 
      [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageSmall)
  {
      ....
  }
  ```

  <span data-ttu-id="83678-178">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="83678-178">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span></span>

   ```csharp
  [FunctionName("ResizeImage")]
  public static void Run(
      [BlobTrigger("sample-images/{name}", Connection = "StorageConnectionAppSetting")] Stream image, 
      [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageSmall)
  {
      ....
  }
  ```

  <span data-ttu-id="83678-179">For a complete example, see [Trigger - C# example](#trigger---c-example).</span><span class="sxs-lookup"><span data-stu-id="83678-179">For a complete example, see [Trigger - C# example](#trigger---c-example).</span></span>

* [<span data-ttu-id="83678-180">StorageAccountAttribute</span><span class="sxs-lookup"><span data-stu-id="83678-180">StorageAccountAttribute</span></span>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)

  <span data-ttu-id="83678-181">Provides another way to specify the storage account to use.</span><span class="sxs-lookup"><span data-stu-id="83678-181">Provides another way to specify the storage account to use.</span></span> <span data-ttu-id="83678-182">The constructor takes the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="83678-182">The constructor takes the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="83678-183">The attribute can be applied at the parameter, method, or class level.</span><span class="sxs-lookup"><span data-stu-id="83678-183">The attribute can be applied at the parameter, method, or class level.</span></span> <span data-ttu-id="83678-184">The following example shows class level and method level:</span><span class="sxs-lookup"><span data-stu-id="83678-184">The following example shows class level and method level:</span></span>

  ```csharp
  [StorageAccount("ClassLevelStorageAppSetting")]
  public static class AzureFunctions
  {
      [FunctionName("BlobTrigger")]
      [StorageAccount("FunctionLevelStorageAppSetting")]
      public static void Run( //...
  {
      ....
  }
  ```

<span data-ttu-id="83678-185">The storage account to use is determined in the following order:</span><span class="sxs-lookup"><span data-stu-id="83678-185">The storage account to use is determined in the following order:</span></span>

* <span data-ttu-id="83678-186">The `BlobTrigger` attribute's `Connection` property.</span><span class="sxs-lookup"><span data-stu-id="83678-186">The `BlobTrigger` attribute's `Connection` property.</span></span>
* <span data-ttu-id="83678-187">The `StorageAccount` attribute applied to the same parameter as the `BlobTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="83678-187">The `StorageAccount` attribute applied to the same parameter as the `BlobTrigger` attribute.</span></span>
* <span data-ttu-id="83678-188">The `StorageAccount` attribute applied to the function.</span><span class="sxs-lookup"><span data-stu-id="83678-188">The `StorageAccount` attribute applied to the function.</span></span>
* <span data-ttu-id="83678-189">The `StorageAccount` attribute applied to the class.</span><span class="sxs-lookup"><span data-stu-id="83678-189">The `StorageAccount` attribute applied to the class.</span></span>
* <span data-ttu-id="83678-190">The default storage account for the function app ("AzureWebJobsStorage" app setting).</span><span class="sxs-lookup"><span data-stu-id="83678-190">The default storage account for the function app ("AzureWebJobsStorage" app setting).</span></span>

## <a name="trigger---configuration"></a><span data-ttu-id="83678-191">Trigger - configuration</span><span class="sxs-lookup"><span data-stu-id="83678-191">Trigger - configuration</span></span>

<span data-ttu-id="83678-192">The following table explains the binding configuration properties that you set in the *function.json* file and the `BlobTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="83678-192">The following table explains the binding configuration properties that you set in the *function.json* file and the `BlobTrigger` attribute.</span></span>

|<span data-ttu-id="83678-193">function.json property</span><span class="sxs-lookup"><span data-stu-id="83678-193">function.json property</span></span> | <span data-ttu-id="83678-194">Attribute property</span><span class="sxs-lookup"><span data-stu-id="83678-194">Attribute property</span></span> |<span data-ttu-id="83678-195">Description</span><span class="sxs-lookup"><span data-stu-id="83678-195">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="83678-196">**type**</span><span class="sxs-lookup"><span data-stu-id="83678-196">**type**</span></span> | <span data-ttu-id="83678-197">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-197">n/a</span></span> | <span data-ttu-id="83678-198">Must be set to `blobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="83678-198">Must be set to `blobTrigger`.</span></span> <span data-ttu-id="83678-199">This property is set automatically when you create the trigger in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="83678-199">This property is set automatically when you create the trigger in the Azure portal.</span></span>|
|<span data-ttu-id="83678-200">**direction**</span><span class="sxs-lookup"><span data-stu-id="83678-200">**direction**</span></span> | <span data-ttu-id="83678-201">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-201">n/a</span></span> | <span data-ttu-id="83678-202">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="83678-202">Must be set to `in`.</span></span> <span data-ttu-id="83678-203">This property is set automatically when you create the trigger in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="83678-203">This property is set automatically when you create the trigger in the Azure portal.</span></span> <span data-ttu-id="83678-204">Exceptions are noted in the [usage](#trigger---usage) section.</span><span class="sxs-lookup"><span data-stu-id="83678-204">Exceptions are noted in the [usage](#trigger---usage) section.</span></span> |
|<span data-ttu-id="83678-205">**name**</span><span class="sxs-lookup"><span data-stu-id="83678-205">**name**</span></span> | <span data-ttu-id="83678-206">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-206">n/a</span></span> | <span data-ttu-id="83678-207">The name of the variable that represents the blob in function code.</span><span class="sxs-lookup"><span data-stu-id="83678-207">The name of the variable that represents the blob in function code.</span></span> | 
|<span data-ttu-id="83678-208">**path**</span><span class="sxs-lookup"><span data-stu-id="83678-208">**path**</span></span> | <span data-ttu-id="83678-209">**BlobPath**</span><span class="sxs-lookup"><span data-stu-id="83678-209">**BlobPath**</span></span> |<span data-ttu-id="83678-210">The container to monitor.</span><span class="sxs-lookup"><span data-stu-id="83678-210">The container to monitor.</span></span>  <span data-ttu-id="83678-211">May be a [blob name pattern](#trigger-blob-name-patterns).</span><span class="sxs-lookup"><span data-stu-id="83678-211">May be a [blob name pattern](#trigger-blob-name-patterns).</span></span> | 
|<span data-ttu-id="83678-212">**connection**</span><span class="sxs-lookup"><span data-stu-id="83678-212">**connection**</span></span> | <span data-ttu-id="83678-213">**Connection**</span><span class="sxs-lookup"><span data-stu-id="83678-213">**Connection**</span></span> | <span data-ttu-id="83678-214">The name of an app setting that contains the Storage connection string to use for this binding.</span><span class="sxs-lookup"><span data-stu-id="83678-214">The name of an app setting that contains the Storage connection string to use for this binding.</span></span> <span data-ttu-id="83678-215">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span><span class="sxs-lookup"><span data-stu-id="83678-215">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span></span> <span data-ttu-id="83678-216">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span><span class="sxs-lookup"><span data-stu-id="83678-216">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span></span> <span data-ttu-id="83678-217">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="83678-217">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span></span><br><br><span data-ttu-id="83678-218">The connection string must be for a general-purpose storage account, not a [blob-only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="83678-218">The connection string must be for a general-purpose storage account, not a [blob-only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span></span>|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a><span data-ttu-id="83678-219">Trigger - usage</span><span class="sxs-lookup"><span data-stu-id="83678-219">Trigger - usage</span></span>

<span data-ttu-id="83678-220">In C# and C# script, you can use the following parameter types for the triggering blob:</span><span class="sxs-lookup"><span data-stu-id="83678-220">In C# and C# script, you can use the following parameter types for the triggering blob:</span></span>

* `Stream`
* `TextReader`
* `string`
* `Byte[]`
* <span data-ttu-id="83678-221">A POCO serializable as JSON</span><span class="sxs-lookup"><span data-stu-id="83678-221">A POCO serializable as JSON</span></span>
* <span data-ttu-id="83678-222">`ICloudBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-222">`ICloudBlob`<sup>1</sup></span></span>
* <span data-ttu-id="83678-223">`CloudBlockBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-223">`CloudBlockBlob`<sup>1</sup></span></span>
* <span data-ttu-id="83678-224">`CloudPageBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-224">`CloudPageBlob`<sup>1</sup></span></span>
* <span data-ttu-id="83678-225">`CloudAppendBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-225">`CloudAppendBlob`<sup>1</sup></span></span>

<span data-ttu-id="83678-226"><sup>1</sup> Requires "inout" binding `direction` in *function.json* or `FileAccess.ReadWrite` in a C# class library.</span><span class="sxs-lookup"><span data-stu-id="83678-226"><sup>1</sup> Requires "inout" binding `direction` in *function.json* or `FileAccess.ReadWrite` in a C# class library.</span></span>

<span data-ttu-id="83678-227">If you try to bind to one of the Storage SDK types and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="83678-227">If you try to bind to one of the Storage SDK types and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span>

<span data-ttu-id="83678-228">Binding to `string`, `Byte[]`, or POCO is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span><span class="sxs-lookup"><span data-stu-id="83678-228">Binding to `string`, `Byte[]`, or POCO is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="83678-229">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span><span class="sxs-lookup"><span data-stu-id="83678-229">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span> <span data-ttu-id="83678-230">For more information, see [Concurrency and memory usage](#trigger---concurrency-and-memory-usage) later in this article.</span><span class="sxs-lookup"><span data-stu-id="83678-230">For more information, see [Concurrency and memory usage](#trigger---concurrency-and-memory-usage) later in this article.</span></span>

<span data-ttu-id="83678-231">In JavaScript, access the input blob data using `context.bindings.<name from function.json>`.</span><span class="sxs-lookup"><span data-stu-id="83678-231">In JavaScript, access the input blob data using `context.bindings.<name from function.json>`.</span></span>

## <a name="trigger---blob-name-patterns"></a><span data-ttu-id="83678-232">Trigger - blob name patterns</span><span class="sxs-lookup"><span data-stu-id="83678-232">Trigger - blob name patterns</span></span>

<span data-ttu-id="83678-233">You can specify a blob name pattern in the `path` property in *function.json* or in the `BlobTrigger` attribute constructor.</span><span class="sxs-lookup"><span data-stu-id="83678-233">You can specify a blob name pattern in the `path` property in *function.json* or in the `BlobTrigger` attribute constructor.</span></span> <span data-ttu-id="83678-234">The name pattern can be a [filter or binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="83678-234">The name pattern can be a [filter or binding expression](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span> <span data-ttu-id="83678-235">The following sections provide examples.</span><span class="sxs-lookup"><span data-stu-id="83678-235">The following sections provide examples.</span></span>

### <a name="get-file-name-and-extension"></a><span data-ttu-id="83678-236">Get file name and extension</span><span class="sxs-lookup"><span data-stu-id="83678-236">Get file name and extension</span></span>

<span data-ttu-id="83678-237">The following example shows how to bind to the blob file name and extension separately:</span><span class="sxs-lookup"><span data-stu-id="83678-237">The following example shows how to bind to the blob file name and extension separately:</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```
<span data-ttu-id="83678-238">If the blob is named *original-Blob1.txt*, the values of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span><span class="sxs-lookup"><span data-stu-id="83678-238">If the blob is named *original-Blob1.txt*, the values of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

### <a name="filter-on-blob-name"></a><span data-ttu-id="83678-239">Filter on blob name</span><span class="sxs-lookup"><span data-stu-id="83678-239">Filter on blob name</span></span>

<span data-ttu-id="83678-240">The following example triggers only on blobs in the `input` container that start with the string "original-":</span><span class="sxs-lookup"><span data-stu-id="83678-240">The following example triggers only on blobs in the `input` container that start with the string "original-":</span></span>

```json
"path": "input/original-{name}",
```
 
<span data-ttu-id="83678-241">If the blob name is *original-Blob1.txt*, the value of the `name` variable in function code is `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="83678-241">If the blob name is *original-Blob1.txt*, the value of the `name` variable in function code is `Blob1`.</span></span>

### <a name="filter-on-file-type"></a><span data-ttu-id="83678-242">Filter on file type</span><span class="sxs-lookup"><span data-stu-id="83678-242">Filter on file type</span></span>

<span data-ttu-id="83678-243">The following example triggers only on *.png* files:</span><span class="sxs-lookup"><span data-stu-id="83678-243">The following example triggers only on *.png* files:</span></span>

```json
"path": "samples/{name}.png",
```

### <a name="filter-on-curly-braces-in-file-names"></a><span data-ttu-id="83678-244">Filter on curly braces in file names</span><span class="sxs-lookup"><span data-stu-id="83678-244">Filter on curly braces in file names</span></span>

<span data-ttu-id="83678-245">To look for curly braces in file names, escape the braces by using two braces.</span><span class="sxs-lookup"><span data-stu-id="83678-245">To look for curly braces in file names, escape the braces by using two braces.</span></span> <span data-ttu-id="83678-246">The following example filters for blobs that have curly braces in the name:</span><span class="sxs-lookup"><span data-stu-id="83678-246">The following example filters for blobs that have curly braces in the name:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="83678-247">If the blob is named *{20140101}-soundfile.mp3*, the `name` variable value in the function code is *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="83678-247">If the blob is named *{20140101}-soundfile.mp3*, the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

## <a name="trigger---metadata"></a><span data-ttu-id="83678-248">Trigger - metadata</span><span class="sxs-lookup"><span data-stu-id="83678-248">Trigger - metadata</span></span>

<span data-ttu-id="83678-249">The blob trigger provides several metadata properties.</span><span class="sxs-lookup"><span data-stu-id="83678-249">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="83678-250">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span><span class="sxs-lookup"><span data-stu-id="83678-250">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="83678-251">These values have the same semantics as the [CloudBlob](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet) type.</span><span class="sxs-lookup"><span data-stu-id="83678-251">These values have the same semantics as the [CloudBlob](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet) type.</span></span>

|<span data-ttu-id="83678-252">Property</span><span class="sxs-lookup"><span data-stu-id="83678-252">Property</span></span>  |<span data-ttu-id="83678-253">Type</span><span class="sxs-lookup"><span data-stu-id="83678-253">Type</span></span>  |<span data-ttu-id="83678-254">Description</span><span class="sxs-lookup"><span data-stu-id="83678-254">Description</span></span>  |
|---------|---------|---------|
|`BlobTrigger`|`string`|<span data-ttu-id="83678-255">The path to the triggering blob.</span><span class="sxs-lookup"><span data-stu-id="83678-255">The path to the triggering blob.</span></span>|
|`Uri`|`System.Uri`|<span data-ttu-id="83678-256">The blob's URI for the primary location.</span><span class="sxs-lookup"><span data-stu-id="83678-256">The blob's URI for the primary location.</span></span>|
|`Properties` |[<span data-ttu-id="83678-257">BlobProperties</span><span class="sxs-lookup"><span data-stu-id="83678-257">BlobProperties</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.blobproperties)|<span data-ttu-id="83678-258">The blob's system properties.</span><span class="sxs-lookup"><span data-stu-id="83678-258">The blob's system properties.</span></span> |
|`Metadata` |`IDictionary<string,string>`|<span data-ttu-id="83678-259">The user-defined metadata for the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-259">The user-defined metadata for the blob.</span></span>|

<span data-ttu-id="83678-260">For example, the following C# script and JavaScript examples log the path to the triggering blob, including the container:</span><span class="sxs-lookup"><span data-stu-id="83678-260">For example, the following C# script and JavaScript examples log the path to the triggering blob, including the container:</span></span>

```csharp
public static void Run(string myBlob, string blobTrigger, TraceWriter log)
{
    log.Info($"Full blob path: {blobTrigger}");
} 
```

```javascript
module.exports = function (context, myBlob) {
    context.log("Full blob path:", context.bindingData.blobTrigger);
    context.done();
};
```

## <a name="trigger---blob-receipts"></a><span data-ttu-id="83678-261">Trigger - blob receipts</span><span class="sxs-lookup"><span data-stu-id="83678-261">Trigger - blob receipts</span></span>

<span data-ttu-id="83678-262">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span><span class="sxs-lookup"><span data-stu-id="83678-262">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="83678-263">To determine if a given blob version has been processed, it maintains *blob receipts*.</span><span class="sxs-lookup"><span data-stu-id="83678-263">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="83678-264">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="83678-264">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="83678-265">A blob receipt has the following information:</span><span class="sxs-lookup"><span data-stu-id="83678-265">A blob receipt has the following information:</span></span>

* <span data-ttu-id="83678-266">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="83678-266">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="83678-267">The container name</span><span class="sxs-lookup"><span data-stu-id="83678-267">The container name</span></span>
* <span data-ttu-id="83678-268">The blob type ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="83678-268">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="83678-269">The blob name</span><span class="sxs-lookup"><span data-stu-id="83678-269">The blob name</span></span>
* <span data-ttu-id="83678-270">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="83678-270">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="83678-271">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span><span class="sxs-lookup"><span data-stu-id="83678-271">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

## <a name="trigger---poison-blobs"></a><span data-ttu-id="83678-272">Trigger - poison blobs</span><span class="sxs-lookup"><span data-stu-id="83678-272">Trigger - poison blobs</span></span>

<span data-ttu-id="83678-273">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span><span class="sxs-lookup"><span data-stu-id="83678-273">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="83678-274">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="83678-274">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="83678-275">The queue message for poison blobs is a JSON object that contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="83678-275">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="83678-276">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span><span class="sxs-lookup"><span data-stu-id="83678-276">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="83678-277">BlobType ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="83678-277">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="83678-278">ContainerName</span><span class="sxs-lookup"><span data-stu-id="83678-278">ContainerName</span></span>
* <span data-ttu-id="83678-279">BlobName</span><span class="sxs-lookup"><span data-stu-id="83678-279">BlobName</span></span>
* <span data-ttu-id="83678-280">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="83678-280">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

## <a name="trigger---concurrency-and-memory-usage"></a><span data-ttu-id="83678-281">Trigger - concurrency and memory usage</span><span class="sxs-lookup"><span data-stu-id="83678-281">Trigger - concurrency and memory usage</span></span>

<span data-ttu-id="83678-282">The blob trigger uses a queue internally, so the maximum number of concurrent function invocations is controlled by the [queues configuration in host.json](functions-host-json.md#queues).</span><span class="sxs-lookup"><span data-stu-id="83678-282">The blob trigger uses a queue internally, so the maximum number of concurrent function invocations is controlled by the [queues configuration in host.json](functions-host-json.md#queues).</span></span> <span data-ttu-id="83678-283">The default settings limit concurrency to 24 invocations.</span><span class="sxs-lookup"><span data-stu-id="83678-283">The default settings limit concurrency to 24 invocations.</span></span> <span data-ttu-id="83678-284">This limit applies separately to each function that uses a blob trigger.</span><span class="sxs-lookup"><span data-stu-id="83678-284">This limit applies separately to each function that uses a blob trigger.</span></span>

<span data-ttu-id="83678-285">[The consumption plan](functions-scale.md#how-the-consumption-plan-works) limits a function app on one virtual machine (VM) to 1.5 GB of memory.</span><span class="sxs-lookup"><span data-stu-id="83678-285">[The consumption plan](functions-scale.md#how-the-consumption-plan-works) limits a function app on one virtual machine (VM) to 1.5 GB of memory.</span></span> <span data-ttu-id="83678-286">Memory is used by each concurrently executing function instance and by the Functions runtime itself.</span><span class="sxs-lookup"><span data-stu-id="83678-286">Memory is used by each concurrently executing function instance and by the Functions runtime itself.</span></span> <span data-ttu-id="83678-287">If a blob-triggered function loads the entire blob into memory, the maximum memory used by that function just for blobs is 24 \* maximum blob size.</span><span class="sxs-lookup"><span data-stu-id="83678-287">If a blob-triggered function loads the entire blob into memory, the maximum memory used by that function just for blobs is 24 \* maximum blob size.</span></span> <span data-ttu-id="83678-288">For example, a function app with three blob-triggered functions and the default settings would have a maximum per-VM concurrency of 3\*24 = 72 function invocations.</span><span class="sxs-lookup"><span data-stu-id="83678-288">For example, a function app with three blob-triggered functions and the default settings would have a maximum per-VM concurrency of 3\*24 = 72 function invocations.</span></span>

<span data-ttu-id="83678-289">JavaScript functions load the entire blob into memory, and C# functions do that if you bind to `string`, `Byte[]`, or POCO.</span><span class="sxs-lookup"><span data-stu-id="83678-289">JavaScript functions load the entire blob into memory, and C# functions do that if you bind to `string`, `Byte[]`, or POCO.</span></span>

## <a name="trigger---polling"></a><span data-ttu-id="83678-290">Trigger - polling</span><span class="sxs-lookup"><span data-stu-id="83678-290">Trigger - polling</span></span>

<span data-ttu-id="83678-291">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span><span class="sxs-lookup"><span data-stu-id="83678-291">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="83678-292">This process can result in delays.</span><span class="sxs-lookup"><span data-stu-id="83678-292">This process can result in delays.</span></span> <span data-ttu-id="83678-293">A function might not get triggered until several minutes or longer after the blob is created.</span><span class="sxs-lookup"><span data-stu-id="83678-293">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="83678-294">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span><span class="sxs-lookup"><span data-stu-id="83678-294">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="83678-295">There's no guarantee that all events are captured.</span><span class="sxs-lookup"><span data-stu-id="83678-295">There's no guarantee that all events are captured.</span></span> <span data-ttu-id="83678-296">Under some conditions, logs may be missed.</span><span class="sxs-lookup"><span data-stu-id="83678-296">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="83678-297">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-297">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="83678-298">Then use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-298">Then use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span> <span data-ttu-id="83678-299">Another option is to use Event Grid; see the tutorial [Automate resizing uploaded images using Event Grid](../event-grid/resize-images-on-storage-blob-upload-event.md).</span><span class="sxs-lookup"><span data-stu-id="83678-299">Another option is to use Event Grid; see the tutorial [Automate resizing uploaded images using Event Grid](../event-grid/resize-images-on-storage-blob-upload-event.md).</span></span>

## <a name="input"></a><span data-ttu-id="83678-300">Input</span><span class="sxs-lookup"><span data-stu-id="83678-300">Input</span></span>

<span data-ttu-id="83678-301">Use a Blob storage input binding to read blobs.</span><span class="sxs-lookup"><span data-stu-id="83678-301">Use a Blob storage input binding to read blobs.</span></span>

## <a name="input---example"></a><span data-ttu-id="83678-302">Input - example</span><span class="sxs-lookup"><span data-stu-id="83678-302">Input - example</span></span>

<span data-ttu-id="83678-303">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="83678-303">See the language-specific example:</span></span>

* [<span data-ttu-id="83678-304">C#</span><span class="sxs-lookup"><span data-stu-id="83678-304">C#</span></span>](#input---c-example)
* [<span data-ttu-id="83678-305">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="83678-305">C# script (.csx)</span></span>](#input---c-script-example)
* [<span data-ttu-id="83678-306">JavaScript</span><span class="sxs-lookup"><span data-stu-id="83678-306">JavaScript</span></span>](#input---javascript-example)
* [<span data-ttu-id="83678-307">Java</span><span class="sxs-lookup"><span data-stu-id="83678-307">Java</span></span>](#input---java-example)

### <a name="input---c-example"></a><span data-ttu-id="83678-308">Input - C# example</span><span class="sxs-lookup"><span data-stu-id="83678-308">Input - C# example</span></span>

<span data-ttu-id="83678-309">The following example is a [C# function](functions-dotnet-class-library.md) that uses a queue trigger and an input blob binding.</span><span class="sxs-lookup"><span data-stu-id="83678-309">The following example is a [C# function](functions-dotnet-class-library.md) that uses a queue trigger and an input blob binding.</span></span> <span data-ttu-id="83678-310">The queue message contains the name of the blob, and the function logs the size of the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-310">The queue message contains the name of the blob, and the function logs the size of the blob.</span></span>

```csharp
[FunctionName("BlobInput")]
public static void Run(
    [QueueTrigger("myqueue-items")] string myQueueItem,
    [Blob("samples-workitems/{queueTrigger}", FileAccess.Read)] Stream myBlob,
    TraceWriter log)
{
    log.Info($"BlobInput processed blob\n Name:{myQueueItem} \n Size: {myBlob.Length} bytes");
}
```        

### <a name="input---c-script-example"></a><span data-ttu-id="83678-311">Input - C# script example</span><span class="sxs-lookup"><span data-stu-id="83678-311">Input - C# script example</span></span>

<!--Same example for input and output. -->

<span data-ttu-id="83678-312">The following example shows blob input and output bindings in a *function.json* file and [C# script (.csx)](functions-reference-csharp.md) code that uses the bindings.</span><span class="sxs-lookup"><span data-stu-id="83678-312">The following example shows blob input and output bindings in a *function.json* file and [C# script (.csx)](functions-reference-csharp.md) code that uses the bindings.</span></span> <span data-ttu-id="83678-313">The function makes a copy of a text blob.</span><span class="sxs-lookup"><span data-stu-id="83678-313">The function makes a copy of a text blob.</span></span> <span data-ttu-id="83678-314">The function is triggered by a queue message that contains the name of the blob to copy.</span><span class="sxs-lookup"><span data-stu-id="83678-314">The function is triggered by a queue message that contains the name of the blob to copy.</span></span> <span data-ttu-id="83678-315">The new blob is named *{originalblobname}-Copy*.</span><span class="sxs-lookup"><span data-stu-id="83678-315">The new blob is named *{originalblobname}-Copy*.</span></span>

<span data-ttu-id="83678-316">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span><span class="sxs-lookup"><span data-stu-id="83678-316">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span></span>

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="83678-317">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="83678-317">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="83678-318">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="83678-318">Here's the C# script code:</span></span>

```cs
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

### <a name="input---javascript-example"></a><span data-ttu-id="83678-319">Input - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="83678-319">Input - JavaScript example</span></span>

<!--Same example for input and output. -->

<span data-ttu-id="83678-320">The following example shows blob input and output bindings in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the bindings.</span><span class="sxs-lookup"><span data-stu-id="83678-320">The following example shows blob input and output bindings in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the bindings.</span></span> <span data-ttu-id="83678-321">The function makes a copy of a blob.</span><span class="sxs-lookup"><span data-stu-id="83678-321">The function makes a copy of a blob.</span></span> <span data-ttu-id="83678-322">The function is triggered by a queue message that contains the name of the blob to copy.</span><span class="sxs-lookup"><span data-stu-id="83678-322">The function is triggered by a queue message that contains the name of the blob to copy.</span></span> <span data-ttu-id="83678-323">The new blob is named *{originalblobname}-Copy*.</span><span class="sxs-lookup"><span data-stu-id="83678-323">The new blob is named *{originalblobname}-Copy*.</span></span>

<span data-ttu-id="83678-324">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span><span class="sxs-lookup"><span data-stu-id="83678-324">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span></span>

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="83678-325">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="83678-325">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="83678-326">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="83678-326">Here's the JavaScript code:</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

### <a name="input---java-example"></a><span data-ttu-id="83678-327">Input - Java example</span><span class="sxs-lookup"><span data-stu-id="83678-327">Input - Java example</span></span>

<span data-ttu-id="83678-328">The following example is a Java function that uses a queue trigger and an input blob binding.</span><span class="sxs-lookup"><span data-stu-id="83678-328">The following example is a Java function that uses a queue trigger and an input blob binding.</span></span> <span data-ttu-id="83678-329">The queue message contains the name of the blob, and the function logs the size of the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-329">The queue message contains the name of the blob, and the function logs the size of the blob.</span></span>

```java
@FunctionName("getBlobSize")
@StorageAccount("AzureWebJobsStorage")
public void blobSize(@QueueTrigger(name = "filename",  queueName = "myqueue-items") String filename,
                    @BlobInput(name = "file", dataType = "binary", path = "samples-workitems/{queueTrigger") byte[] content,
       final ExecutionContext context) {
      context.getLogger().info("The size of \"" + filename + "\" is: " + content.length + " bytes");
 }
 ```

  <span data-ttu-id="83678-330">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@BlobInput` annotation on parameters whose value would come from a blob.</span><span class="sxs-lookup"><span data-stu-id="83678-330">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@BlobInput` annotation on parameters whose value would come from a blob.</span></span>  <span data-ttu-id="83678-331">This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`.</span><span class="sxs-lookup"><span data-stu-id="83678-331">This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`.</span></span> 


## <a name="input---attributes"></a><span data-ttu-id="83678-332">Input - attributes</span><span class="sxs-lookup"><span data-stu-id="83678-332">Input - attributes</span></span>

<span data-ttu-id="83678-333">In [C# class libraries](functions-dotnet-class-library.md), use the [BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs).</span><span class="sxs-lookup"><span data-stu-id="83678-333">In [C# class libraries](functions-dotnet-class-library.md), use the [BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs).</span></span>

<span data-ttu-id="83678-334">The attribute's constructor takes the path to the blob and a `FileAccess` parameter indicating read or write, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="83678-334">The attribute's constructor takes the path to the blob and a `FileAccess` parameter indicating read or write, as shown in the following example:</span></span>

```csharp
[FunctionName("BlobInput")]
public static void Run(
    [QueueTrigger("myqueue-items")] string myQueueItem,
    [Blob("samples-workitems/{queueTrigger}", FileAccess.Read)] Stream myBlob,
    TraceWriter log)
{
    log.Info($"BlobInput processed blob\n Name:{myQueueItem} \n Size: {myBlob.Length} bytes");
}

```

<span data-ttu-id="83678-335">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="83678-335">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span></span>

```csharp
[FunctionName("BlobInput")]
public static void Run(
    [QueueTrigger("myqueue-items")] string myQueueItem,
    [Blob("samples-workitems/{queueTrigger}", FileAccess.Read, Connection = "StorageConnectionAppSetting")] Stream myBlob,
    TraceWriter log)
{
    log.Info($"BlobInput processed blob\n Name:{myQueueItem} \n Size: {myBlob.Length} bytes");
}
```

<span data-ttu-id="83678-336">You can use the `StorageAccount` attribute to specify the storage account at class, method, or parameter level.</span><span class="sxs-lookup"><span data-stu-id="83678-336">You can use the `StorageAccount` attribute to specify the storage account at class, method, or parameter level.</span></span> <span data-ttu-id="83678-337">For more information, see [Trigger - attributes](#trigger---attributes).</span><span class="sxs-lookup"><span data-stu-id="83678-337">For more information, see [Trigger - attributes](#trigger---attributes).</span></span>

## <a name="input---configuration"></a><span data-ttu-id="83678-338">Input - configuration</span><span class="sxs-lookup"><span data-stu-id="83678-338">Input - configuration</span></span>

<span data-ttu-id="83678-339">The following table explains the binding configuration properties that you set in the *function.json* file and the `Blob` attribute.</span><span class="sxs-lookup"><span data-stu-id="83678-339">The following table explains the binding configuration properties that you set in the *function.json* file and the `Blob` attribute.</span></span>

|<span data-ttu-id="83678-340">function.json property</span><span class="sxs-lookup"><span data-stu-id="83678-340">function.json property</span></span> | <span data-ttu-id="83678-341">Attribute property</span><span class="sxs-lookup"><span data-stu-id="83678-341">Attribute property</span></span> |<span data-ttu-id="83678-342">Description</span><span class="sxs-lookup"><span data-stu-id="83678-342">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="83678-343">**type**</span><span class="sxs-lookup"><span data-stu-id="83678-343">**type**</span></span> | <span data-ttu-id="83678-344">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-344">n/a</span></span> | <span data-ttu-id="83678-345">Must be set to `blob`.</span><span class="sxs-lookup"><span data-stu-id="83678-345">Must be set to `blob`.</span></span> |
|<span data-ttu-id="83678-346">**direction**</span><span class="sxs-lookup"><span data-stu-id="83678-346">**direction**</span></span> | <span data-ttu-id="83678-347">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-347">n/a</span></span> | <span data-ttu-id="83678-348">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="83678-348">Must be set to `in`.</span></span> <span data-ttu-id="83678-349">Exceptions are noted in the [usage](#input---usage) section.</span><span class="sxs-lookup"><span data-stu-id="83678-349">Exceptions are noted in the [usage](#input---usage) section.</span></span> |
|<span data-ttu-id="83678-350">**name**</span><span class="sxs-lookup"><span data-stu-id="83678-350">**name**</span></span> | <span data-ttu-id="83678-351">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-351">n/a</span></span> | <span data-ttu-id="83678-352">The name of the variable that represents the blob in function code.</span><span class="sxs-lookup"><span data-stu-id="83678-352">The name of the variable that represents the blob in function code.</span></span>|
|<span data-ttu-id="83678-353">**path**</span><span class="sxs-lookup"><span data-stu-id="83678-353">**path**</span></span> |<span data-ttu-id="83678-354">**BlobPath**</span><span class="sxs-lookup"><span data-stu-id="83678-354">**BlobPath**</span></span> | <span data-ttu-id="83678-355">The path to the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-355">The path to the blob.</span></span> | 
|<span data-ttu-id="83678-356">**connection**</span><span class="sxs-lookup"><span data-stu-id="83678-356">**connection**</span></span> |<span data-ttu-id="83678-357">**Connection**</span><span class="sxs-lookup"><span data-stu-id="83678-357">**Connection**</span></span>| <span data-ttu-id="83678-358">The name of an app setting that contains the Storage connection string to use for this binding.</span><span class="sxs-lookup"><span data-stu-id="83678-358">The name of an app setting that contains the Storage connection string to use for this binding.</span></span> <span data-ttu-id="83678-359">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span><span class="sxs-lookup"><span data-stu-id="83678-359">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span></span> <span data-ttu-id="83678-360">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span><span class="sxs-lookup"><span data-stu-id="83678-360">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span></span> <span data-ttu-id="83678-361">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="83678-361">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span></span><br><br><span data-ttu-id="83678-362">The connection string must be for a general-purpose storage account, not a [blob-only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="83678-362">The connection string must be for a general-purpose storage account, not a [blob-only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span></span>|
|<span data-ttu-id="83678-363">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-363">n/a</span></span> | <span data-ttu-id="83678-364">**Access**</span><span class="sxs-lookup"><span data-stu-id="83678-364">**Access**</span></span> | <span data-ttu-id="83678-365">Indicates whether you will be reading or writing.</span><span class="sxs-lookup"><span data-stu-id="83678-365">Indicates whether you will be reading or writing.</span></span> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="input---usage"></a><span data-ttu-id="83678-366">Input - usage</span><span class="sxs-lookup"><span data-stu-id="83678-366">Input - usage</span></span>

<span data-ttu-id="83678-367">In C# and C# script, you can use the following parameter types for the blob input binding:</span><span class="sxs-lookup"><span data-stu-id="83678-367">In C# and C# script, you can use the following parameter types for the blob input binding:</span></span>

* `Stream`
* `TextReader`
* `string`
* `Byte[]`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* <span data-ttu-id="83678-368">`ICloudBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-368">`ICloudBlob`<sup>1</sup></span></span>
* <span data-ttu-id="83678-369">`CloudBlockBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-369">`CloudBlockBlob`<sup>1</sup></span></span>
* <span data-ttu-id="83678-370">`CloudPageBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-370">`CloudPageBlob`<sup>1</sup></span></span>
* <span data-ttu-id="83678-371">`CloudAppendBlob`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-371">`CloudAppendBlob`<sup>1</sup></span></span>

<span data-ttu-id="83678-372"><sup>1</sup> Requires "inout" binding `direction` in *function.json* or `FileAccess.ReadWrite` in a C# class library.</span><span class="sxs-lookup"><span data-stu-id="83678-372"><sup>1</sup> Requires "inout" binding `direction` in *function.json* or `FileAccess.ReadWrite` in a C# class library.</span></span>

<span data-ttu-id="83678-373">If you try to bind to one of the Storage SDK types and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="83678-373">If you try to bind to one of the Storage SDK types and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span>

<span data-ttu-id="83678-374">Binding to `string` or `Byte[]` is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span><span class="sxs-lookup"><span data-stu-id="83678-374">Binding to `string` or `Byte[]` is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="83678-375">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span><span class="sxs-lookup"><span data-stu-id="83678-375">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span> <span data-ttu-id="83678-376">For more information, see [Concurrency and memory usage](#trigger---concurrency-and-memory-usage) earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="83678-376">For more information, see [Concurrency and memory usage](#trigger---concurrency-and-memory-usage) earlier in this article.</span></span>

<span data-ttu-id="83678-377">In JavaScript, access the blob data using `context.bindings.<name from function.json>`.</span><span class="sxs-lookup"><span data-stu-id="83678-377">In JavaScript, access the blob data using `context.bindings.<name from function.json>`.</span></span>

## <a name="output"></a><span data-ttu-id="83678-378">Output</span><span class="sxs-lookup"><span data-stu-id="83678-378">Output</span></span>

<span data-ttu-id="83678-379">Use Blob storage output bindings to write blobs.</span><span class="sxs-lookup"><span data-stu-id="83678-379">Use Blob storage output bindings to write blobs.</span></span>

## <a name="output---example"></a><span data-ttu-id="83678-380">Output - example</span><span class="sxs-lookup"><span data-stu-id="83678-380">Output - example</span></span>

<span data-ttu-id="83678-381">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="83678-381">See the language-specific example:</span></span>

* [<span data-ttu-id="83678-382">C#</span><span class="sxs-lookup"><span data-stu-id="83678-382">C#</span></span>](#output---c-example)
* [<span data-ttu-id="83678-383">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="83678-383">C# script (.csx)</span></span>](#output---c-script-example)
* [<span data-ttu-id="83678-384">JavaScript</span><span class="sxs-lookup"><span data-stu-id="83678-384">JavaScript</span></span>](#output---javascript-example)
* [<span data-ttu-id="83678-385">Java</span><span class="sxs-lookup"><span data-stu-id="83678-385">Java</span></span>](#output---java-example)

### <a name="output---c-example"></a><span data-ttu-id="83678-386">Output - C# example</span><span class="sxs-lookup"><span data-stu-id="83678-386">Output - C# example</span></span>

<span data-ttu-id="83678-387">The following example is a [C# function](functions-dotnet-class-library.md) that uses a blob trigger and two output blob bindings.</span><span class="sxs-lookup"><span data-stu-id="83678-387">The following example is a [C# function](functions-dotnet-class-library.md) that uses a blob trigger and two output blob bindings.</span></span> <span data-ttu-id="83678-388">The function is triggered by the creation of an image blob in the *sample-images* container.</span><span class="sxs-lookup"><span data-stu-id="83678-388">The function is triggered by the creation of an image blob in the *sample-images* container.</span></span> <span data-ttu-id="83678-389">It creates small and medium size copies of the image blob.</span><span class="sxs-lookup"><span data-stu-id="83678-389">It creates small and medium size copies of the image blob.</span></span> 

```csharp
[FunctionName("ResizeImage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

### <a name="output---c-script-example"></a><span data-ttu-id="83678-390">Output - C# script example</span><span class="sxs-lookup"><span data-stu-id="83678-390">Output - C# script example</span></span>

<!--Same example for input and output. -->

<span data-ttu-id="83678-391">The following example shows blob input and output bindings in a *function.json* file and [C# script (.csx)](functions-reference-csharp.md) code that uses the bindings.</span><span class="sxs-lookup"><span data-stu-id="83678-391">The following example shows blob input and output bindings in a *function.json* file and [C# script (.csx)](functions-reference-csharp.md) code that uses the bindings.</span></span> <span data-ttu-id="83678-392">The function makes a copy of a text blob.</span><span class="sxs-lookup"><span data-stu-id="83678-392">The function makes a copy of a text blob.</span></span> <span data-ttu-id="83678-393">The function is triggered by a queue message that contains the name of the blob to copy.</span><span class="sxs-lookup"><span data-stu-id="83678-393">The function is triggered by a queue message that contains the name of the blob to copy.</span></span> <span data-ttu-id="83678-394">The new blob is named *{originalblobname}-Copy*.</span><span class="sxs-lookup"><span data-stu-id="83678-394">The new blob is named *{originalblobname}-Copy*.</span></span>

<span data-ttu-id="83678-395">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span><span class="sxs-lookup"><span data-stu-id="83678-395">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span></span>

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="83678-396">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="83678-396">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="83678-397">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="83678-397">Here's the C# script code:</span></span>

```cs
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

### <a name="output---javascript-example"></a><span data-ttu-id="83678-398">Output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="83678-398">Output - JavaScript example</span></span>

<!--Same example for input and output. -->

<span data-ttu-id="83678-399">The following example shows blob input and output bindings in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the bindings.</span><span class="sxs-lookup"><span data-stu-id="83678-399">The following example shows blob input and output bindings in a *function.json* file and [JavaScript code](functions-reference-node.md) that uses the bindings.</span></span> <span data-ttu-id="83678-400">The function makes a copy of a blob.</span><span class="sxs-lookup"><span data-stu-id="83678-400">The function makes a copy of a blob.</span></span> <span data-ttu-id="83678-401">The function is triggered by a queue message that contains the name of the blob to copy.</span><span class="sxs-lookup"><span data-stu-id="83678-401">The function is triggered by a queue message that contains the name of the blob to copy.</span></span> <span data-ttu-id="83678-402">The new blob is named *{originalblobname}-Copy*.</span><span class="sxs-lookup"><span data-stu-id="83678-402">The new blob is named *{originalblobname}-Copy*.</span></span>

<span data-ttu-id="83678-403">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span><span class="sxs-lookup"><span data-stu-id="83678-403">In the *function.json* file, the `queueTrigger` metadata property is used to specify the blob name in the `path` properties:</span></span>

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnectionAppSetting",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="83678-404">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="83678-404">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="83678-405">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="83678-405">Here's the JavaScript code:</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

### <a name="output---java-example"></a><span data-ttu-id="83678-406">Output - Java example</span><span class="sxs-lookup"><span data-stu-id="83678-406">Output - Java example</span></span>

<span data-ttu-id="83678-407">The following example shows blob input and output bindings in a Java function.</span><span class="sxs-lookup"><span data-stu-id="83678-407">The following example shows blob input and output bindings in a Java function.</span></span> <span data-ttu-id="83678-408">The function makes a copy of a text blob.</span><span class="sxs-lookup"><span data-stu-id="83678-408">The function makes a copy of a text blob.</span></span> <span data-ttu-id="83678-409">The function is triggered by a queue message that contains the name of the blob to copy.</span><span class="sxs-lookup"><span data-stu-id="83678-409">The function is triggered by a queue message that contains the name of the blob to copy.</span></span> <span data-ttu-id="83678-410">The new blob is named {originalblobname}-Copy</span><span class="sxs-lookup"><span data-stu-id="83678-410">The new blob is named {originalblobname}-Copy</span></span>

```java
@FunctionName("copyTextBlob")
@StorageAccount("AzureWebJobsStorage")
@BlobOutput(name = "target", path = "samples-workitems/{queueTrigger}-Copy")
public String blobCopy(
    @QueueTrigger(name = "filename", queueName = "myqueue-items") String filename,
    @BlobInput(name = "source", path = "samples-workitems/{queueTrigger}") String content ) {
      return content;
 }
 ```

 <span data-ttu-id="83678-411">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@BlobOutput` annotation on function parameters whose value would be written to an object in blob storage.</span><span class="sxs-lookup"><span data-stu-id="83678-411">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@BlobOutput` annotation on function parameters whose value would be written to an object in blob storage.</span></span>  <span data-ttu-id="83678-412">The parameter type should be `OutputBinding<T>`, where T is any native Java type of a POJO.</span><span class="sxs-lookup"><span data-stu-id="83678-412">The parameter type should be `OutputBinding<T>`, where T is any native Java type of a POJO.</span></span>


## <a name="output---attributes"></a><span data-ttu-id="83678-413">Output - attributes</span><span class="sxs-lookup"><span data-stu-id="83678-413">Output - attributes</span></span>

<span data-ttu-id="83678-414">In [C# class libraries](functions-dotnet-class-library.md), use the [BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs).</span><span class="sxs-lookup"><span data-stu-id="83678-414">In [C# class libraries](functions-dotnet-class-library.md), use the [BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs).</span></span>

<span data-ttu-id="83678-415">The attribute's constructor takes the path to the blob and a `FileAccess` parameter indicating read or write, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="83678-415">The attribute's constructor takes the path to the blob and a `FileAccess` parameter indicating read or write, as shown in the following example:</span></span>

```csharp
[FunctionName("ResizeImage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageSmall)
{
    ...
}
```

<span data-ttu-id="83678-416">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="83678-416">You can set the `Connection` property to specify the storage account to use, as shown in the following example:</span></span>

```csharp
[FunctionName("ResizeImage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-md/{name}", FileAccess.Write, Connection = "StorageConnectionAppSetting")] Stream imageSmall)
{
    ...
}
```

<span data-ttu-id="83678-417">For a complete example, see [Output - C# example](#output---c-example).</span><span class="sxs-lookup"><span data-stu-id="83678-417">For a complete example, see [Output - C# example](#output---c-example).</span></span>

<span data-ttu-id="83678-418">You can use the `StorageAccount` attribute to specify the storage account at class, method, or parameter level.</span><span class="sxs-lookup"><span data-stu-id="83678-418">You can use the `StorageAccount` attribute to specify the storage account at class, method, or parameter level.</span></span> <span data-ttu-id="83678-419">For more information, see [Trigger - attributes](#trigger---attributes).</span><span class="sxs-lookup"><span data-stu-id="83678-419">For more information, see [Trigger - attributes](#trigger---attributes).</span></span>

## <a name="output---configuration"></a><span data-ttu-id="83678-420">Output - configuration</span><span class="sxs-lookup"><span data-stu-id="83678-420">Output - configuration</span></span>

<span data-ttu-id="83678-421">The following table explains the binding configuration properties that you set in the *function.json* file and the `Blob` attribute.</span><span class="sxs-lookup"><span data-stu-id="83678-421">The following table explains the binding configuration properties that you set in the *function.json* file and the `Blob` attribute.</span></span>

|<span data-ttu-id="83678-422">function.json property</span><span class="sxs-lookup"><span data-stu-id="83678-422">function.json property</span></span> | <span data-ttu-id="83678-423">Attribute property</span><span class="sxs-lookup"><span data-stu-id="83678-423">Attribute property</span></span> |<span data-ttu-id="83678-424">Description</span><span class="sxs-lookup"><span data-stu-id="83678-424">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="83678-425">**type**</span><span class="sxs-lookup"><span data-stu-id="83678-425">**type**</span></span> | <span data-ttu-id="83678-426">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-426">n/a</span></span> | <span data-ttu-id="83678-427">Must be set to `blob`.</span><span class="sxs-lookup"><span data-stu-id="83678-427">Must be set to `blob`.</span></span> |
|<span data-ttu-id="83678-428">**direction**</span><span class="sxs-lookup"><span data-stu-id="83678-428">**direction**</span></span> | <span data-ttu-id="83678-429">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-429">n/a</span></span> | <span data-ttu-id="83678-430">Must be set to `out` for an output binding.</span><span class="sxs-lookup"><span data-stu-id="83678-430">Must be set to `out` for an output binding.</span></span> <span data-ttu-id="83678-431">Exceptions are noted in the [usage](#output---usage) section.</span><span class="sxs-lookup"><span data-stu-id="83678-431">Exceptions are noted in the [usage](#output---usage) section.</span></span> |
|<span data-ttu-id="83678-432">**name**</span><span class="sxs-lookup"><span data-stu-id="83678-432">**name**</span></span> | <span data-ttu-id="83678-433">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-433">n/a</span></span> | <span data-ttu-id="83678-434">The name of the variable that represents the blob in function code.</span><span class="sxs-lookup"><span data-stu-id="83678-434">The name of the variable that represents the blob in function code.</span></span>  <span data-ttu-id="83678-435">Set to `$return` to reference the function return value.</span><span class="sxs-lookup"><span data-stu-id="83678-435">Set to `$return` to reference the function return value.</span></span>|
|<span data-ttu-id="83678-436">**path**</span><span class="sxs-lookup"><span data-stu-id="83678-436">**path**</span></span> |<span data-ttu-id="83678-437">**BlobPath**</span><span class="sxs-lookup"><span data-stu-id="83678-437">**BlobPath**</span></span> | <span data-ttu-id="83678-438">The path to the blob.</span><span class="sxs-lookup"><span data-stu-id="83678-438">The path to the blob.</span></span> | 
|<span data-ttu-id="83678-439">**connection**</span><span class="sxs-lookup"><span data-stu-id="83678-439">**connection**</span></span> |<span data-ttu-id="83678-440">**Connection**</span><span class="sxs-lookup"><span data-stu-id="83678-440">**Connection**</span></span>| <span data-ttu-id="83678-441">The name of an app setting that contains the Storage connection string to use for this binding.</span><span class="sxs-lookup"><span data-stu-id="83678-441">The name of an app setting that contains the Storage connection string to use for this binding.</span></span> <span data-ttu-id="83678-442">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span><span class="sxs-lookup"><span data-stu-id="83678-442">If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here.</span></span> <span data-ttu-id="83678-443">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span><span class="sxs-lookup"><span data-stu-id="83678-443">For example, if you set `connection` to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage."</span></span> <span data-ttu-id="83678-444">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="83678-444">If you leave `connection` empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`.</span></span><br><br><span data-ttu-id="83678-445">The connection string must be for a general-purpose storage account, not a [blob-only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="83678-445">The connection string must be for a general-purpose storage account, not a [blob-only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span></span>|
|<span data-ttu-id="83678-446">n/a</span><span class="sxs-lookup"><span data-stu-id="83678-446">n/a</span></span> | <span data-ttu-id="83678-447">**Access**</span><span class="sxs-lookup"><span data-stu-id="83678-447">**Access**</span></span> | <span data-ttu-id="83678-448">Indicates whether you will be reading or writing.</span><span class="sxs-lookup"><span data-stu-id="83678-448">Indicates whether you will be reading or writing.</span></span> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a><span data-ttu-id="83678-449">Output - usage</span><span class="sxs-lookup"><span data-stu-id="83678-449">Output - usage</span></span>

<span data-ttu-id="83678-450">In C# and C# script, you can bind to the following types to write blobs:</span><span class="sxs-lookup"><span data-stu-id="83678-450">In C# and C# script, you can bind to the following types to write blobs:</span></span>

* `TextWriter`
* `out string`
* `out Byte[]`
* `CloudBlobStream`
* `Stream`
* <span data-ttu-id="83678-451">`CloudBlobContainer`<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="83678-451">`CloudBlobContainer`<sup>1</sup></span></span>
* `CloudBlobDirectory`
* <span data-ttu-id="83678-452">`ICloudBlob`<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="83678-452">`ICloudBlob`<sup>2</sup></span></span>
* <span data-ttu-id="83678-453">`CloudBlockBlob`<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="83678-453">`CloudBlockBlob`<sup>2</sup></span></span>
* <span data-ttu-id="83678-454">`CloudPageBlob`<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="83678-454">`CloudPageBlob`<sup>2</sup></span></span>
* <span data-ttu-id="83678-455">`CloudAppendBlob`<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="83678-455">`CloudAppendBlob`<sup>2</sup></span></span>

<span data-ttu-id="83678-456"><sup>1</sup> Requires "in" binding `direction` in *function.json* or `FileAccess.Read` in a C# class library.</span><span class="sxs-lookup"><span data-stu-id="83678-456"><sup>1</sup> Requires "in" binding `direction` in *function.json* or `FileAccess.Read` in a C# class library.</span></span> <span data-ttu-id="83678-457">However, you can use the container object that the runtime provides to do write operations, such as uploading blobs to the container.</span><span class="sxs-lookup"><span data-stu-id="83678-457">However, you can use the container object that the runtime provides to do write operations, such as uploading blobs to the container.</span></span>

<span data-ttu-id="83678-458"><sup>2</sup> Requires "inout" binding `direction` in *function.json* or `FileAccess.ReadWrite` in a C# class library.</span><span class="sxs-lookup"><span data-stu-id="83678-458"><sup>2</sup> Requires "inout" binding `direction` in *function.json* or `FileAccess.ReadWrite` in a C# class library.</span></span>

<span data-ttu-id="83678-459">If you try to bind to one of the Storage SDK types and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span><span class="sxs-lookup"><span data-stu-id="83678-459">If you try to bind to one of the Storage SDK types and get an error message, make sure that you have a reference to [the correct Storage SDK version](#azure-storage-sdk-version-in-functions-1x).</span></span>

<span data-ttu-id="83678-460">In async functions, use the return value or `IAsyncCollector` instead of an `out` parameter.</span><span class="sxs-lookup"><span data-stu-id="83678-460">In async functions, use the return value or `IAsyncCollector` instead of an `out` parameter.</span></span>

<span data-ttu-id="83678-461">Binding to `string` or `Byte[]` is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span><span class="sxs-lookup"><span data-stu-id="83678-461">Binding to `string` or `Byte[]` is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="83678-462">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span><span class="sxs-lookup"><span data-stu-id="83678-462">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span> <span data-ttu-id="83678-463">For more information, see [Concurrency and memory usage](#trigger---concurrency-and-memory-usage) earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="83678-463">For more information, see [Concurrency and memory usage](#trigger---concurrency-and-memory-usage) earlier in this article.</span></span>


<span data-ttu-id="83678-464">In JavaScript, access the blob data using `context.bindings.<name from function.json>`.</span><span class="sxs-lookup"><span data-stu-id="83678-464">In JavaScript, access the blob data using `context.bindings.<name from function.json>`.</span></span>

## <a name="exceptions-and-return-codes"></a><span data-ttu-id="83678-465">Exceptions and return codes</span><span class="sxs-lookup"><span data-stu-id="83678-465">Exceptions and return codes</span></span>

| <span data-ttu-id="83678-466">Binding</span><span class="sxs-lookup"><span data-stu-id="83678-466">Binding</span></span> |  <span data-ttu-id="83678-467">Reference</span><span class="sxs-lookup"><span data-stu-id="83678-467">Reference</span></span> |
|---|---|
| <span data-ttu-id="83678-468">Blob</span><span class="sxs-lookup"><span data-stu-id="83678-468">Blob</span></span> | [<span data-ttu-id="83678-469">Blob Error Codes</span><span class="sxs-lookup"><span data-stu-id="83678-469">Blob Error Codes</span></span>](https://docs.microsoft.com/rest/api/storageservices/fileservices/blob-service-error-codes) |
| <span data-ttu-id="83678-470">Blob, Table, Queue</span><span class="sxs-lookup"><span data-stu-id="83678-470">Blob, Table, Queue</span></span> |  [<span data-ttu-id="83678-471">Storage Error Codes</span><span class="sxs-lookup"><span data-stu-id="83678-471">Storage Error Codes</span></span>](https://docs.microsoft.com/rest/api/storageservices/fileservices/common-rest-api-error-codes) |
| <span data-ttu-id="83678-472">Blob, Table, Queue</span><span class="sxs-lookup"><span data-stu-id="83678-472">Blob, Table, Queue</span></span> |  [<span data-ttu-id="83678-473">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="83678-473">Troubleshooting</span></span>](https://docs.microsoft.com/rest/api/storageservices/fileservices/troubleshooting-api-operations) |

## <a name="next-steps"></a><span data-ttu-id="83678-474">Next steps</span><span class="sxs-lookup"><span data-stu-id="83678-474">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="83678-475">Go to a quickstart that uses a Blob storage trigger</span><span class="sxs-lookup"><span data-stu-id="83678-475">Go to a quickstart that uses a Blob storage trigger</span></span>](functions-create-storage-blob-triggered-function.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="83678-476">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="83678-476">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
