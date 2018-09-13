---
title: How to use Azure Table storage from Node.js | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage, a NoSQL data store.
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 70830309c33d4a94fc1eb5abb85cba26c8623f88
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553232"
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="a714e-103">How to use Azure Table storage from Node.js</span><span class="sxs-lookup"><span data-stu-id="a714e-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="a714e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a714e-104">Overview</span></span>
<span data-ttu-id="a714e-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="a714e-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="a714e-106">The code examples in this topic assume you already have a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="a714e-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="a714e-107">For information about how to create a Node.js application in Azure, see any of these topics:</span><span class="sxs-lookup"><span data-stu-id="a714e-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="a714e-108">Create a Node.js web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a714e-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="a714e-109">Build and deploy a Node.js web app to Azure using WebMatrix</span><span class="sxs-lookup"><span data-stu-id="a714e-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="a714e-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a714e-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="a714e-111">Configure your application to access Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a714e-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="a714e-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="a714e-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="a714e-113">Use Node Package Manager (NPM) to install the package</span><span class="sxs-lookup"><span data-stu-id="a714e-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="a714e-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span><span class="sxs-lookup"><span data-stu-id="a714e-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="a714e-115">Type **npm install azure-storage** in the command window.</span><span class="sxs-lookup"><span data-stu-id="a714e-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="a714e-116">Output from the command is similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="a714e-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="a714e-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="a714e-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a714e-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span><span class="sxs-lookup"><span data-stu-id="a714e-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="a714e-119">Import the package</span><span class="sxs-lookup"><span data-stu-id="a714e-119">Import the package</span></span>
<span data-ttu-id="a714e-120">Add the following code to the top of the **server.js** file in your application:</span><span class="sxs-lookup"><span data-stu-id="a714e-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="a714e-121">Set up an Azure Storage connection</span><span class="sxs-lookup"><span data-stu-id="a714e-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="a714e-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a714e-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="a714e-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span><span class="sxs-lookup"><span data-stu-id="a714e-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="a714e-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span><span class="sxs-lookup"><span data-stu-id="a714e-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="create-a-table"></a><span data-ttu-id="a714e-125">Create a table</span><span class="sxs-lookup"><span data-stu-id="a714e-125">Create a table</span></span>
<span data-ttu-id="a714e-126">The following code creates a **TableService** object and uses it to create a new table.</span><span class="sxs-lookup"><span data-stu-id="a714e-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="a714e-127">Add the following near the top of **server.js**.</span><span class="sxs-lookup"><span data-stu-id="a714e-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="a714e-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="a714e-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="a714e-129">The following example creates a new table named 'mytable' if it does not already exist:</span><span class="sxs-lookup"><span data-stu-id="a714e-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="a714e-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span><span class="sxs-lookup"><span data-stu-id="a714e-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="a714e-131">The `response` will contain information about the request.</span><span class="sxs-lookup"><span data-stu-id="a714e-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="a714e-132">Filters</span><span class="sxs-lookup"><span data-stu-id="a714e-132">Filters</span></span>
<span data-ttu-id="a714e-133">Optional filtering operations can be applied to operations performed using **TableService**.</span><span class="sxs-lookup"><span data-stu-id="a714e-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="a714e-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span><span class="sxs-lookup"><span data-stu-id="a714e-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="a714e-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span><span class="sxs-lookup"><span data-stu-id="a714e-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a714e-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span><span class="sxs-lookup"><span data-stu-id="a714e-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="a714e-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="a714e-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="a714e-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="a714e-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="a714e-139">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="a714e-139">Add an entity to a table</span></span>
<span data-ttu-id="a714e-140">To add an entity, first create an object that defines your entity properties.</span><span class="sxs-lookup"><span data-stu-id="a714e-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="a714e-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span><span class="sxs-lookup"><span data-stu-id="a714e-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="a714e-142">**PartitionKey** - determines the partition that the entity is stored in</span><span class="sxs-lookup"><span data-stu-id="a714e-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="a714e-143">**RowKey** - uniquely identifies the entity within the partition</span><span class="sxs-lookup"><span data-stu-id="a714e-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="a714e-144">Both **PartitionKey** and **RowKey** must be string values.</span><span class="sxs-lookup"><span data-stu-id="a714e-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="a714e-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="a714e-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="a714e-146">The following is an example of defining an entity.</span><span class="sxs-lookup"><span data-stu-id="a714e-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="a714e-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="a714e-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="a714e-148">Specifying the type is optional, and types will be inferred if not specified.</span><span class="sxs-lookup"><span data-stu-id="a714e-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="a714e-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span><span class="sxs-lookup"><span data-stu-id="a714e-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="a714e-150">You can also use the **entityGenerator** to create entities.</span><span class="sxs-lookup"><span data-stu-id="a714e-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="a714e-151">The following example creates the same task entity using the **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="a714e-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="a714e-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span><span class="sxs-lookup"><span data-stu-id="a714e-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="a714e-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span><span class="sxs-lookup"><span data-stu-id="a714e-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="a714e-154">Example response:</span><span class="sxs-lookup"><span data-stu-id="a714e-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="a714e-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span><span class="sxs-lookup"><span data-stu-id="a714e-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="a714e-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span><span class="sxs-lookup"><span data-stu-id="a714e-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="a714e-157">You can do this by enabling **echoContent** as follows:</span><span class="sxs-lookup"><span data-stu-id="a714e-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="a714e-158">Update an entity</span><span class="sxs-lookup"><span data-stu-id="a714e-158">Update an entity</span></span>
<span data-ttu-id="a714e-159">There are multiple methods available to update an existing entity:</span><span class="sxs-lookup"><span data-stu-id="a714e-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="a714e-160">**replaceEntity** - updates an existing entity by replacing it</span><span class="sxs-lookup"><span data-stu-id="a714e-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="a714e-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span><span class="sxs-lookup"><span data-stu-id="a714e-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="a714e-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="a714e-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="a714e-163">If no entity exists, a new one will be inserted</span><span class="sxs-lookup"><span data-stu-id="a714e-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="a714e-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span><span class="sxs-lookup"><span data-stu-id="a714e-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="a714e-165">If no entity exists, a new one will be inserted</span><span class="sxs-lookup"><span data-stu-id="a714e-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="a714e-166">The following example demonstrates updating an entity using **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="a714e-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="a714e-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span><span class="sxs-lookup"><span data-stu-id="a714e-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="a714e-168">To support concurrent updates:</span><span class="sxs-lookup"><span data-stu-id="a714e-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="a714e-169">Get the ETag of the object being updated.</span><span class="sxs-lookup"><span data-stu-id="a714e-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="a714e-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="a714e-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="a714e-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span><span class="sxs-lookup"><span data-stu-id="a714e-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="a714e-172">For example:</span><span class="sxs-lookup"><span data-stu-id="a714e-172">For example:</span></span>
>
>       <span data-ttu-id="a714e-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="a714e-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="a714e-174">Perform the update operation.</span><span class="sxs-lookup"><span data-stu-id="a714e-174">Perform the update operation.</span></span> <span data-ttu-id="a714e-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span><span class="sxs-lookup"><span data-stu-id="a714e-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="a714e-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span><span class="sxs-lookup"><span data-stu-id="a714e-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="a714e-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="a714e-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="a714e-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span><span class="sxs-lookup"><span data-stu-id="a714e-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="a714e-179">Work with groups of entities</span><span class="sxs-lookup"><span data-stu-id="a714e-179">Work with groups of entities</span></span>
<span data-ttu-id="a714e-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span><span class="sxs-lookup"><span data-stu-id="a714e-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="a714e-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span><span class="sxs-lookup"><span data-stu-id="a714e-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="a714e-182">The following example demonstrates submitting two entities in a batch:</span><span class="sxs-lookup"><span data-stu-id="a714e-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="a714e-183">For successful batch operations, `result` will contain information for each operation in the batch.</span><span class="sxs-lookup"><span data-stu-id="a714e-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="a714e-184">Work with batched operations</span><span class="sxs-lookup"><span data-stu-id="a714e-184">Work with batched operations</span></span>
<span data-ttu-id="a714e-185">Operations added to a batch can be inspected by viewing the `operations` property.</span><span class="sxs-lookup"><span data-stu-id="a714e-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="a714e-186">You can also use the following methods to work with operations:</span><span class="sxs-lookup"><span data-stu-id="a714e-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="a714e-187">**clear** - clears all operations from a batch</span><span class="sxs-lookup"><span data-stu-id="a714e-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="a714e-188">**getOperations** - gets an operation from the batch</span><span class="sxs-lookup"><span data-stu-id="a714e-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="a714e-189">**hasOperations** - returns true if the batch contains operations</span><span class="sxs-lookup"><span data-stu-id="a714e-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="a714e-190">**removeOperations** - removes an operation</span><span class="sxs-lookup"><span data-stu-id="a714e-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="a714e-191">**size** - returns the number of operations in the batch</span><span class="sxs-lookup"><span data-stu-id="a714e-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="a714e-192">Retrieve an entity by key</span><span class="sxs-lookup"><span data-stu-id="a714e-192">Retrieve an entity by key</span></span>
<span data-ttu-id="a714e-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span><span class="sxs-lookup"><span data-stu-id="a714e-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="a714e-194">Once this operation is complete, `result` will contain the entity.</span><span class="sxs-lookup"><span data-stu-id="a714e-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="a714e-195">Query a set of entities</span><span class="sxs-lookup"><span data-stu-id="a714e-195">Query a set of entities</span></span>
<span data-ttu-id="a714e-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span><span class="sxs-lookup"><span data-stu-id="a714e-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="a714e-197">**select** - the fields to be returned from the query</span><span class="sxs-lookup"><span data-stu-id="a714e-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="a714e-198">**where** - the where clause</span><span class="sxs-lookup"><span data-stu-id="a714e-198">**where** - the where clause</span></span>

  * <span data-ttu-id="a714e-199">**and** - an `and` where condition</span><span class="sxs-lookup"><span data-stu-id="a714e-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="a714e-200">**or** - an `or` where condition</span><span class="sxs-lookup"><span data-stu-id="a714e-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="a714e-201">**top** - the number of items to fetch</span><span class="sxs-lookup"><span data-stu-id="a714e-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="a714e-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="a714e-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="a714e-203">Since **select** is not used, all fields will be returned.</span><span class="sxs-lookup"><span data-stu-id="a714e-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="a714e-204">To perform the query against a table, use **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="a714e-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="a714e-205">The following example uses this query to return entities from 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="a714e-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="a714e-206">If successful, `result.entries` will contain an array of entities that match the query.</span><span class="sxs-lookup"><span data-stu-id="a714e-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="a714e-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span><span class="sxs-lookup"><span data-stu-id="a714e-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="a714e-208">For the initial query, use *null* for the third parameter.</span><span class="sxs-lookup"><span data-stu-id="a714e-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="a714e-209">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="a714e-209">Query a subset of entity properties</span></span>
<span data-ttu-id="a714e-210">A query to a table can retrieve just a few fields from an entity.</span><span class="sxs-lookup"><span data-stu-id="a714e-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="a714e-211">This reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="a714e-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="a714e-212">Use the **select** clause and pass the names of the fields to be returned.</span><span class="sxs-lookup"><span data-stu-id="a714e-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="a714e-213">For example, the following query will return only the **description** and **dueDate** fields.</span><span class="sxs-lookup"><span data-stu-id="a714e-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="a714e-214">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="a714e-214">Delete an entity</span></span>
<span data-ttu-id="a714e-215">You can delete an entity using its partition and row keys.</span><span class="sxs-lookup"><span data-stu-id="a714e-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="a714e-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span><span class="sxs-lookup"><span data-stu-id="a714e-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="a714e-217">Then the object is passed to the **deleteEntity** method.</span><span class="sxs-lookup"><span data-stu-id="a714e-217">Then the object is passed to the **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="a714e-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span><span class="sxs-lookup"><span data-stu-id="a714e-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="a714e-219">See [Update an entity](#update-an-entity) for information on using ETags.</span><span class="sxs-lookup"><span data-stu-id="a714e-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="a714e-220">Delete a table</span><span class="sxs-lookup"><span data-stu-id="a714e-220">Delete a table</span></span>
<span data-ttu-id="a714e-221">The following code deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="a714e-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="a714e-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="a714e-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="a714e-223">Use continuation tokens</span><span class="sxs-lookup"><span data-stu-id="a714e-223">Use continuation tokens</span></span>
<span data-ttu-id="a714e-224">When you are querying tables for large amounts of results, look for continuation tokens.</span><span class="sxs-lookup"><span data-stu-id="a714e-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="a714e-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span><span class="sxs-lookup"><span data-stu-id="a714e-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="a714e-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span><span class="sxs-lookup"><span data-stu-id="a714e-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="a714e-227">You can then use this when performing a query to continue to move across the partition and table entities.</span><span class="sxs-lookup"><span data-stu-id="a714e-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="a714e-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span><span class="sxs-lookup"><span data-stu-id="a714e-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="a714e-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span><span class="sxs-lookup"><span data-stu-id="a714e-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="a714e-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span><span class="sxs-lookup"><span data-stu-id="a714e-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="a714e-231">Look for `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="a714e-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="a714e-232">Work with shared access signatures</span><span class="sxs-lookup"><span data-stu-id="a714e-232">Work with shared access signatures</span></span>
<span data-ttu-id="a714e-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span><span class="sxs-lookup"><span data-stu-id="a714e-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="a714e-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span><span class="sxs-lookup"><span data-stu-id="a714e-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="a714e-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span><span class="sxs-lookup"><span data-stu-id="a714e-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="a714e-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span><span class="sxs-lookup"><span data-stu-id="a714e-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="a714e-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span><span class="sxs-lookup"><span data-stu-id="a714e-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="a714e-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span><span class="sxs-lookup"><span data-stu-id="a714e-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="a714e-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span><span class="sxs-lookup"><span data-stu-id="a714e-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="a714e-240">The following example connects to the table and performs a query.</span><span class="sxs-lookup"><span data-stu-id="a714e-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="a714e-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span><span class="sxs-lookup"><span data-stu-id="a714e-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="a714e-242">Access Control Lists</span><span class="sxs-lookup"><span data-stu-id="a714e-242">Access Control Lists</span></span>
<span data-ttu-id="a714e-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span><span class="sxs-lookup"><span data-stu-id="a714e-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="a714e-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span><span class="sxs-lookup"><span data-stu-id="a714e-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="a714e-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span><span class="sxs-lookup"><span data-stu-id="a714e-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="a714e-246">The following example defines two policies, one for 'user1' and one for 'user2':</span><span class="sxs-lookup"><span data-stu-id="a714e-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="a714e-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="a714e-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="a714e-248">This approach allows:</span><span class="sxs-lookup"><span data-stu-id="a714e-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="a714e-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span><span class="sxs-lookup"><span data-stu-id="a714e-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="a714e-250">The following example creates a new SAS for 'user2':</span><span class="sxs-lookup"><span data-stu-id="a714e-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="a714e-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="a714e-251">Next steps</span></span>
<span data-ttu-id="a714e-252">For more information, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="a714e-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="a714e-253">[Azure Storage Team Blog][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="a714e-253">[Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="a714e-254">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="a714e-254">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>
* [<span data-ttu-id="a714e-255">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="a714e-255">Node.js Developer Center</span></span>](/develop/nodejs/)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[OData.org]: http://www.odata.org/
[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx

[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[Create and deploy a Node.js application to an Azure website]: ../app-service-web/app-service-web-get-started-nodejs.md
