---
title: How to use Blob storage from Node.js | Microsoft Docs
description: Store unstructured data in the cloud with Azure Blob storage (object storage).
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: b5ed7853c696d9e8477a31aba8a9cc9ab8558fa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563583"
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="d4957-103">How to use Blob storage from Node.js</span><span class="sxs-lookup"><span data-stu-id="d4957-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="d4957-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d4957-104">Overview</span></span>
<span data-ttu-id="d4957-105">This article shows you how to perform common scenarios using Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d4957-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="d4957-106">The samples are written via the Node.js API.</span><span class="sxs-lookup"><span data-stu-id="d4957-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="d4957-107">The scenarios covered include how to upload, list, download, and delete blobs.</span><span class="sxs-lookup"><span data-stu-id="d4957-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="d4957-108">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="d4957-108">Create a Node.js application</span></span>
<span data-ttu-id="d4957-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="d4957-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="d4957-110">Configure your application to access storage</span><span class="sxs-lookup"><span data-stu-id="d4957-110">Configure your application to access storage</span></span>
<span data-ttu-id="d4957-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="d4957-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="d4957-112">Use Node Package Manager (NPM) to obtain the package</span><span class="sxs-lookup"><span data-stu-id="d4957-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="d4957-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span><span class="sxs-lookup"><span data-stu-id="d4957-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="d4957-114">Type **npm install azure-storage** in the command window.</span><span class="sxs-lookup"><span data-stu-id="d4957-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="d4957-115">Output from the command is similar to the following code example.</span><span class="sxs-lookup"><span data-stu-id="d4957-115">Output from the command is similar to the following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="d4957-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="d4957-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="d4957-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span><span class="sxs-lookup"><span data-stu-id="d4957-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="d4957-118">Import the package</span><span class="sxs-lookup"><span data-stu-id="d4957-118">Import the package</span></span>
<span data-ttu-id="d4957-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span><span class="sxs-lookup"><span data-stu-id="d4957-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="d4957-120">Set up an Azure Storage connection</span><span class="sxs-lookup"><span data-stu-id="d4957-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="d4957-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="d4957-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="d4957-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="d4957-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="d4957-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service].</span><span class="sxs-lookup"><span data-stu-id="d4957-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="d4957-124">Create a container</span><span class="sxs-lookup"><span data-stu-id="d4957-124">Create a container</span></span>
<span data-ttu-id="d4957-125">The **BlobService** object lets you work with containers and blobs.</span><span class="sxs-lookup"><span data-stu-id="d4957-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="d4957-126">The following code creates a **BlobService** object.</span><span class="sxs-lookup"><span data-stu-id="d4957-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="d4957-127">Add the following near the top of **server.js**:</span><span class="sxs-lookup"><span data-stu-id="d4957-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="d4957-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span><span class="sxs-lookup"><span data-stu-id="d4957-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="d4957-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="d4957-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="d4957-130">To create a new container, use **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="d4957-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="d4957-131">The following code example creates a new container named 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="d4957-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="d4957-132">If the container is newly created, `result.created` is true.</span><span class="sxs-lookup"><span data-stu-id="d4957-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="d4957-133">If the container already exists, `result.created` is false.</span><span class="sxs-lookup"><span data-stu-id="d4957-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="d4957-134">`response` contains information about the operation, including the ETag information for the container.</span><span class="sxs-lookup"><span data-stu-id="d4957-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="d4957-135">Container security</span><span class="sxs-lookup"><span data-stu-id="d4957-135">Container security</span></span>
<span data-ttu-id="d4957-136">By default, new containers are private and cannot be accessed anonymously.</span><span class="sxs-lookup"><span data-stu-id="d4957-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="d4957-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span><span class="sxs-lookup"><span data-stu-id="d4957-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="d4957-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span><span class="sxs-lookup"><span data-stu-id="d4957-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="d4957-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span><span class="sxs-lookup"><span data-stu-id="d4957-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="d4957-140">The following code example demonstrates setting the access level to **blob**:</span><span class="sxs-lookup"><span data-stu-id="d4957-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="d4957-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span><span class="sxs-lookup"><span data-stu-id="d4957-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="d4957-142">The following code example changes the access level to container:</span><span class="sxs-lookup"><span data-stu-id="d4957-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="d4957-143">The result contains information about the operation, including the current **ETag** for the container.</span><span class="sxs-lookup"><span data-stu-id="d4957-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="d4957-144">Filters</span><span class="sxs-lookup"><span data-stu-id="d4957-144">Filters</span></span>
<span data-ttu-id="d4957-145">You can apply optional filtering operations to operations performed using **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="d4957-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="d4957-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span><span class="sxs-lookup"><span data-stu-id="d4957-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="d4957-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span><span class="sxs-lookup"><span data-stu-id="d4957-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="d4957-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span><span class="sxs-lookup"><span data-stu-id="d4957-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="d4957-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="d4957-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="d4957-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="d4957-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d4957-151">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="d4957-151">Upload a blob into a container</span></span>
<span data-ttu-id="d4957-152">There are three types of blobs: block blobs, page blobs and append blobs.</span><span class="sxs-lookup"><span data-stu-id="d4957-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="d4957-153">Block blobs allow you to more efficiently upload large data.</span><span class="sxs-lookup"><span data-stu-id="d4957-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="d4957-154">Append blobs are optimized for append operations.</span><span class="sxs-lookup"><span data-stu-id="d4957-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="d4957-155">Page blobs are optimized for read/write operations.</span><span class="sxs-lookup"><span data-stu-id="d4957-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="d4957-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4957-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="d4957-157">Block blobs</span><span class="sxs-lookup"><span data-stu-id="d4957-157">Block blobs</span></span>
<span data-ttu-id="d4957-158">To upload data to a block blob, use the following:</span><span class="sxs-lookup"><span data-stu-id="d4957-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="d4957-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span><span class="sxs-lookup"><span data-stu-id="d4957-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="d4957-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span><span class="sxs-lookup"><span data-stu-id="d4957-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="d4957-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span><span class="sxs-lookup"><span data-stu-id="d4957-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="d4957-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span><span class="sxs-lookup"><span data-stu-id="d4957-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="d4957-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="d4957-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span><span class="sxs-lookup"><span data-stu-id="d4957-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="d4957-165">Append blobs</span><span class="sxs-lookup"><span data-stu-id="d4957-165">Append blobs</span></span>
<span data-ttu-id="d4957-166">To upload data to a new append blob, use the following:</span><span class="sxs-lookup"><span data-stu-id="d4957-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="d4957-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span><span class="sxs-lookup"><span data-stu-id="d4957-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="d4957-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span><span class="sxs-lookup"><span data-stu-id="d4957-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="d4957-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span><span class="sxs-lookup"><span data-stu-id="d4957-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="d4957-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span><span class="sxs-lookup"><span data-stu-id="d4957-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="d4957-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="d4957-172">To append a block to an existing append blob, use the following:</span><span class="sxs-lookup"><span data-stu-id="d4957-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="d4957-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span><span class="sxs-lookup"><span data-stu-id="d4957-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="d4957-174">**appendFromStream** - append the contents of a stream to an existing append blob</span><span class="sxs-lookup"><span data-stu-id="d4957-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="d4957-175">**appendFromText** - append the contents of a string to an existing append blob</span><span class="sxs-lookup"><span data-stu-id="d4957-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="d4957-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span><span class="sxs-lookup"><span data-stu-id="d4957-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="d4957-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span><span class="sxs-lookup"><span data-stu-id="d4957-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="d4957-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span><span class="sxs-lookup"><span data-stu-id="d4957-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="d4957-179">appendBlockFromXXX won't.</span><span class="sxs-lookup"><span data-stu-id="d4957-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="d4957-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="d4957-181">Page blobs</span><span class="sxs-lookup"><span data-stu-id="d4957-181">Page blobs</span></span>
<span data-ttu-id="d4957-182">To upload data to a page blob, use the following:</span><span class="sxs-lookup"><span data-stu-id="d4957-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="d4957-183">**createPageBlob** - creates a new page blob of a specific length</span><span class="sxs-lookup"><span data-stu-id="d4957-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="d4957-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span><span class="sxs-lookup"><span data-stu-id="d4957-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="d4957-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span><span class="sxs-lookup"><span data-stu-id="d4957-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="d4957-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span><span class="sxs-lookup"><span data-stu-id="d4957-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="d4957-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span><span class="sxs-lookup"><span data-stu-id="d4957-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="d4957-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="d4957-189">Page blobs consist of 512-byte 'pages'.</span><span class="sxs-lookup"><span data-stu-id="d4957-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="d4957-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span><span class="sxs-lookup"><span data-stu-id="d4957-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d4957-191">List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="d4957-191">List the blobs in a container</span></span>
<span data-ttu-id="d4957-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span><span class="sxs-lookup"><span data-stu-id="d4957-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="d4957-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="d4957-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="d4957-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span><span class="sxs-lookup"><span data-stu-id="d4957-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="d4957-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span><span class="sxs-lookup"><span data-stu-id="d4957-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="d4957-196">Download blobs</span><span class="sxs-lookup"><span data-stu-id="d4957-196">Download blobs</span></span>
<span data-ttu-id="d4957-197">To download data from a blob, use the following:</span><span class="sxs-lookup"><span data-stu-id="d4957-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="d4957-198">**getBlobToLocalFile** - writes the blob contents to file</span><span class="sxs-lookup"><span data-stu-id="d4957-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="d4957-199">**getBlobToStream** - writes the blob contents to a stream</span><span class="sxs-lookup"><span data-stu-id="d4957-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="d4957-200">**getBlobToText** - writes the blob contents to a string</span><span class="sxs-lookup"><span data-stu-id="d4957-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="d4957-201">**createReadStream** - provides a stream to read from the blob</span><span class="sxs-lookup"><span data-stu-id="d4957-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="d4957-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span><span class="sxs-lookup"><span data-stu-id="d4957-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="d4957-203">The `result` contains information about the blob, including **ETag** information.</span><span class="sxs-lookup"><span data-stu-id="d4957-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="d4957-204">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="d4957-204">Delete a blob</span></span>
<span data-ttu-id="d4957-205">Finally, to delete a blob, call **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="d4957-206">The following code example deletes the blob named **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="d4957-207">Concurrent access</span><span class="sxs-lookup"><span data-stu-id="d4957-207">Concurrent access</span></span>
<span data-ttu-id="d4957-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span><span class="sxs-lookup"><span data-stu-id="d4957-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="d4957-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span><span class="sxs-lookup"><span data-stu-id="d4957-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="d4957-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span><span class="sxs-lookup"><span data-stu-id="d4957-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="d4957-211">ETag</span><span class="sxs-lookup"><span data-stu-id="d4957-211">ETag</span></span>
<span data-ttu-id="d4957-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span><span class="sxs-lookup"><span data-stu-id="d4957-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="d4957-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span><span class="sxs-lookup"><span data-stu-id="d4957-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="d4957-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span><span class="sxs-lookup"><span data-stu-id="d4957-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="d4957-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="d4957-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="d4957-216">When you're using ETags, the general pattern is:</span><span class="sxs-lookup"><span data-stu-id="d4957-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="d4957-217">Obtain the ETag as the result of a create, list, or get operation.</span><span class="sxs-lookup"><span data-stu-id="d4957-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="d4957-218">Perform an action, checking that the ETag value has not been modified.</span><span class="sxs-lookup"><span data-stu-id="d4957-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="d4957-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span><span class="sxs-lookup"><span data-stu-id="d4957-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="d4957-220">Lease</span><span class="sxs-lookup"><span data-stu-id="d4957-220">Lease</span></span>
<span data-ttu-id="d4957-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span><span class="sxs-lookup"><span data-stu-id="d4957-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="d4957-222">For example, the following code acquires a lease on **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="d4957-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span><span class="sxs-lookup"><span data-stu-id="d4957-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="d4957-224">The lease ID is returned as `result.id` from **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="d4957-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="d4957-225">By default, the lease duration is infinite.</span><span class="sxs-lookup"><span data-stu-id="d4957-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="d4957-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span><span class="sxs-lookup"><span data-stu-id="d4957-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="d4957-227">To remove a lease, use **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="d4957-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="d4957-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="d4957-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="d4957-229">Work with shared access signatures</span><span class="sxs-lookup"><span data-stu-id="d4957-229">Work with shared access signatures</span></span>
<span data-ttu-id="d4957-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span><span class="sxs-lookup"><span data-stu-id="d4957-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="d4957-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span><span class="sxs-lookup"><span data-stu-id="d4957-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="d4957-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span><span class="sxs-lookup"><span data-stu-id="d4957-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="d4957-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span><span class="sxs-lookup"><span data-stu-id="d4957-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="d4957-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span><span class="sxs-lookup"><span data-stu-id="d4957-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="d4957-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span><span class="sxs-lookup"><span data-stu-id="d4957-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="d4957-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span><span class="sxs-lookup"><span data-stu-id="d4957-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="d4957-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span><span class="sxs-lookup"><span data-stu-id="d4957-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="d4957-238">The following gets information about **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d4957-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="d4957-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span><span class="sxs-lookup"><span data-stu-id="d4957-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="d4957-240">Access control lists</span><span class="sxs-lookup"><span data-stu-id="d4957-240">Access control lists</span></span>
<span data-ttu-id="d4957-241">You can also use an access control list (ACL) to set the access policy for SAS.</span><span class="sxs-lookup"><span data-stu-id="d4957-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="d4957-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span><span class="sxs-lookup"><span data-stu-id="d4957-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="d4957-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span><span class="sxs-lookup"><span data-stu-id="d4957-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="d4957-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span><span class="sxs-lookup"><span data-stu-id="d4957-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="d4957-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="d4957-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="d4957-246">This approach allows:</span><span class="sxs-lookup"><span data-stu-id="d4957-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="d4957-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span><span class="sxs-lookup"><span data-stu-id="d4957-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="d4957-248">The following code example creates new shared access signatures for 'user2':</span><span class="sxs-lookup"><span data-stu-id="d4957-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="d4957-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4957-249">Next steps</span></span>
<span data-ttu-id="d4957-250">For more information, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="d4957-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="d4957-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="d4957-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="d4957-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="d4957-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="d4957-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="d4957-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="d4957-254">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="d4957-254">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="d4957-255">Transfer data with the AzCopy command-line utility</span><span class="sxs-lookup"><span data-stu-id="d4957-255">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
