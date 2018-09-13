---
title: How to use Azure Table storage or Azure Cosmos DB Table API from Node.js | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: nodejs
ms.topic: sample
ms.date: 04/05/2018
ms.author: sngun
ms.openlocfilehash: 2b88bd3c86d520b10c27746319f807d2f6208bfa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857006"
---
# <a name="how-to-use-azure-table-storage-or-the-azure-cosmos-db-table-api-from-nodejs"></a><span data-ttu-id="377c9-103">How to use Azure Table storage or the Azure Cosmos DB Table API from Node.js</span><span class="sxs-lookup"><span data-stu-id="377c9-103">How to use Azure Table storage or the Azure Cosmos DB Table API from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

## <a name="overview"></a><span data-ttu-id="377c9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="377c9-104">Overview</span></span>
<span data-ttu-id="377c9-105">This article shows how to perform common scenarios using Azure Storage Table service or Azure Cosmos DB in a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="377c9-105">This article shows how to perform common scenarios using Azure Storage Table service or Azure Cosmos DB in a Node.js application.</span></span>

## <a name="create-an-azure-service-account"></a><span data-ttu-id="377c9-106">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="377c9-106">Create an Azure service account</span></span>

[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="377c9-107">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="377c9-107">Create an Azure storage account</span></span>

[!INCLUDE [cosmos-db-create-storage-account](../../includes/cosmos-db-create-storage-account.md)]

### <a name="create-an-azure-cosmos-db-table-api-account"></a><span data-ttu-id="377c9-108">Create an Azure Cosmos DB Table API account</span><span class="sxs-lookup"><span data-stu-id="377c9-108">Create an Azure Cosmos DB Table API account</span></span>

[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

## <a name="configure-your-application-to-access-azure-storage-or-the-azure-cosmos-db-table-api"></a><span data-ttu-id="377c9-109">Configure your application to access Azure Storage or the Azure Cosmos DB Table API</span><span class="sxs-lookup"><span data-stu-id="377c9-109">Configure your application to access Azure Storage or the Azure Cosmos DB Table API</span></span>
<span data-ttu-id="377c9-110">To use Azure Storage or Azure Cosmos DB, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the Storage REST services.</span><span class="sxs-lookup"><span data-stu-id="377c9-110">To use Azure Storage or Azure Cosmos DB, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="377c9-111">Use Node Package Manager (NPM) to install the package</span><span class="sxs-lookup"><span data-stu-id="377c9-111">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="377c9-112">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span><span class="sxs-lookup"><span data-stu-id="377c9-112">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="377c9-113">Type **npm install azure-storage** in the command window.</span><span class="sxs-lookup"><span data-stu-id="377c9-113">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="377c9-114">Output from the command is similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="377c9-114">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="377c9-115">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="377c9-115">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="377c9-116">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span><span class="sxs-lookup"><span data-stu-id="377c9-116">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="377c9-117">Import the package</span><span class="sxs-lookup"><span data-stu-id="377c9-117">Import the package</span></span>
<span data-ttu-id="377c9-118">Add the following code to the top of the **server.js** file in your application:</span><span class="sxs-lookup"><span data-stu-id="377c9-118">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="add-an-azure-storage-connection"></a><span data-ttu-id="377c9-119">Add an Azure Storage connection</span><span class="sxs-lookup"><span data-stu-id="377c9-119">Add an Azure Storage connection</span></span>
<span data-ttu-id="377c9-120">The Azure module reads the environment variables AZURE_STORAGE_ACCOUNT and AZURE_STORAGE_ACCESS_KEY, or AZURE_STORAGE_CONNECTION_STRING for information required to connect to your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="377c9-120">The Azure module reads the environment variables AZURE_STORAGE_ACCOUNT and AZURE_STORAGE_ACCESS_KEY, or AZURE_STORAGE_CONNECTION_STRING for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="377c9-121">If these environment variables are not set, you must specify the account information when calling **TableService**.</span><span class="sxs-lookup"><span data-stu-id="377c9-121">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span> <span data-ttu-id="377c9-122">For example, the following code creates a **TableService** object:</span><span class="sxs-lookup"><span data-stu-id="377c9-122">For example, the following code creates a **TableService** object:</span></span>

```nodejs
var tableSvc = azure.createTableService('myaccount', 'myaccesskey');
```

## <a name="add-an-azure-cosmos-db-connection"></a><span data-ttu-id="377c9-123">Add an Azure Cosmos DB connection</span><span class="sxs-lookup"><span data-stu-id="377c9-123">Add an Azure Cosmos DB connection</span></span>
<span data-ttu-id="377c9-124">To add an Azure Cosmos DB connection, create a **TableService** object and specify your account name, primary key, and endpoint.</span><span class="sxs-lookup"><span data-stu-id="377c9-124">To add an Azure Cosmos DB connection, create a **TableService** object and specify your account name, primary key, and endpoint.</span></span> <span data-ttu-id="377c9-125">You can copy these values from **Settings** > **Connection String** in the Azure portal for your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="377c9-125">You can copy these values from **Settings** > **Connection String** in the Azure portal for your Cosmos DB account.</span></span> <span data-ttu-id="377c9-126">For example:</span><span class="sxs-lookup"><span data-stu-id="377c9-126">For example:</span></span>

```nodejs
var tableSvc = azure.createTableService('myaccount', 'myprimarykey', 'myendpoint');
```  

## <a name="create-a-table"></a><span data-ttu-id="377c9-127">Create a table</span><span class="sxs-lookup"><span data-stu-id="377c9-127">Create a table</span></span>
<span data-ttu-id="377c9-128">The following code creates a **TableService** object and uses it to create a new table.</span><span class="sxs-lookup"><span data-stu-id="377c9-128">The following code creates a **TableService** object and uses it to create a new table.</span></span> 

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="377c9-129">The call to **createTableIfNotExists** creates a new table with the specified name if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="377c9-129">The call to **createTableIfNotExists** creates a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="377c9-130">The following example creates a new table named 'mytable' if it does not already exist:</span><span class="sxs-lookup"><span data-stu-id="377c9-130">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="377c9-131">The `result.created` is `true` if a new table is created, and `false` if the table already exists.</span><span class="sxs-lookup"><span data-stu-id="377c9-131">The `result.created` is `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="377c9-132">The `response` contains information about the request.</span><span class="sxs-lookup"><span data-stu-id="377c9-132">The `response` contains information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="377c9-133">Filters</span><span class="sxs-lookup"><span data-stu-id="377c9-133">Filters</span></span>
<span data-ttu-id="377c9-134">You can apply optional filtering to operations performed using **TableService**.</span><span class="sxs-lookup"><span data-stu-id="377c9-134">You can apply optional filtering to operations performed using **TableService**.</span></span> <span data-ttu-id="377c9-135">Filtering operations can include logging, automatic retries, etc. Filters are objects that implement a method with the signature:</span><span class="sxs-lookup"><span data-stu-id="377c9-135">Filtering operations can include logging, automatic retries, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="377c9-136">After doing its preprocessing on the request options, the method must call **next**, passing a callback with the following signature:</span><span class="sxs-lookup"><span data-stu-id="377c9-136">After doing its preprocessing on the request options, the method must call **next**, passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="377c9-137">In this callback, and after processing the **returnObject** (the response from the request to the server), the callback must either invoke **next** if it exists to continue processing other filters or simply invoke **finalCallback** otherwise to end the service invocation.</span><span class="sxs-lookup"><span data-stu-id="377c9-137">In this callback, and after processing the **returnObject** (the response from the request to the server), the callback must either invoke **next** if it exists to continue processing other filters or simply invoke **finalCallback** otherwise to end the service invocation.</span></span>

<span data-ttu-id="377c9-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="377c9-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="377c9-139">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="377c9-139">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="377c9-140">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="377c9-140">Add an entity to a table</span></span>
<span data-ttu-id="377c9-141">To add an entity, first create an object that defines your entity properties.</span><span class="sxs-lookup"><span data-stu-id="377c9-141">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="377c9-142">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-142">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="377c9-143">**PartitionKey** - Determines the partition in which the entity is stored.</span><span class="sxs-lookup"><span data-stu-id="377c9-143">**PartitionKey** - Determines the partition in which the entity is stored.</span></span>
* <span data-ttu-id="377c9-144">**RowKey** - Uniquely identifies the entity within the partition.</span><span class="sxs-lookup"><span data-stu-id="377c9-144">**RowKey** - Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="377c9-145">Both **PartitionKey** and **RowKey** must be string values.</span><span class="sxs-lookup"><span data-stu-id="377c9-145">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="377c9-146">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="377c9-146">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="377c9-147">The following is an example of defining an entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-147">The following is an example of defining an entity.</span></span> <span data-ttu-id="377c9-148">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="377c9-148">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="377c9-149">Specifying the type is optional, and types are inferred if not specified.</span><span class="sxs-lookup"><span data-stu-id="377c9-149">Specifying the type is optional, and types are inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="377c9-150">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span><span class="sxs-lookup"><span data-stu-id="377c9-150">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="377c9-151">You can also use the **entityGenerator** to create entities.</span><span class="sxs-lookup"><span data-stu-id="377c9-151">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="377c9-152">The following example creates the same task entity using the **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="377c9-152">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="377c9-153">To add an entity to your table, pass the entity object to the **insertEntity** method.</span><span class="sxs-lookup"><span data-stu-id="377c9-153">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="377c9-154">If the operation is successful, `result` contains the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` contains information about the operation.</span><span class="sxs-lookup"><span data-stu-id="377c9-154">If the operation is successful, `result` contains the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` contains information about the operation.</span></span>

<span data-ttu-id="377c9-155">Example response:</span><span class="sxs-lookup"><span data-stu-id="377c9-155">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="377c9-156">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span><span class="sxs-lookup"><span data-stu-id="377c9-156">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="377c9-157">If you plan on performing other operations on this entity, or want to cache the information, it can be useful to have it returned as part of the `result`.</span><span class="sxs-lookup"><span data-stu-id="377c9-157">If you plan on performing other operations on this entity, or want to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="377c9-158">You can do this by enabling **echoContent** as follows:</span><span class="sxs-lookup"><span data-stu-id="377c9-158">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="377c9-159">Update an entity</span><span class="sxs-lookup"><span data-stu-id="377c9-159">Update an entity</span></span>
<span data-ttu-id="377c9-160">There are multiple methods available to update an existing entity:</span><span class="sxs-lookup"><span data-stu-id="377c9-160">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="377c9-161">**replaceEntity** - Updates an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="377c9-161">**replaceEntity** - Updates an existing entity by replacing it.</span></span>
* <span data-ttu-id="377c9-162">**mergeEntity** - Updates an existing entity by merging new property values into the existing entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-162">**mergeEntity** - Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="377c9-163">**insertOrReplaceEntity** - Updates an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="377c9-163">**insertOrReplaceEntity** - Updates an existing entity by replacing it.</span></span> <span data-ttu-id="377c9-164">If no entity exists, a new one will be inserted.</span><span class="sxs-lookup"><span data-stu-id="377c9-164">If no entity exists, a new one will be inserted.</span></span>
* <span data-ttu-id="377c9-165">**insertOrMergeEntity** - Updates an existing entity by merging new property values into the existing.</span><span class="sxs-lookup"><span data-stu-id="377c9-165">**insertOrMergeEntity** - Updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="377c9-166">If no entity exists, a new one will be inserted.</span><span class="sxs-lookup"><span data-stu-id="377c9-166">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="377c9-167">The following example demonstrates updating an entity using **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="377c9-167">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="377c9-168">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span><span class="sxs-lookup"><span data-stu-id="377c9-168">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="377c9-169">To support concurrent updates:</span><span class="sxs-lookup"><span data-stu-id="377c9-169">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="377c9-170">Get the ETag of the object being updated.</span><span class="sxs-lookup"><span data-stu-id="377c9-170">Get the ETag of the object being updated.</span></span> <span data-ttu-id="377c9-171">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="377c9-171">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="377c9-172">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-172">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="377c9-173">For example:</span><span class="sxs-lookup"><span data-stu-id="377c9-173">For example:</span></span>
>
>       <span data-ttu-id="377c9-174">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="377c9-174">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="377c9-175">Perform the update operation.</span><span class="sxs-lookup"><span data-stu-id="377c9-175">Perform the update operation.</span></span> <span data-ttu-id="377c9-176">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` is returned stating that the update condition specified in the request was not satisfied.</span><span class="sxs-lookup"><span data-stu-id="377c9-176">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` is returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="377c9-177">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation fails; therefore, if you want to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="377c9-177">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation fails; therefore, if you want to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="377c9-178">The `result` for successful update operations contains the **Etag** of the updated entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-178">The `result` for successful update operations contains the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="377c9-179">Work with groups of entities</span><span class="sxs-lookup"><span data-stu-id="377c9-179">Work with groups of entities</span></span>
<span data-ttu-id="377c9-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span><span class="sxs-lookup"><span data-stu-id="377c9-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="377c9-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span><span class="sxs-lookup"><span data-stu-id="377c9-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="377c9-182">The following example demonstrates submitting two entities in a batch:</span><span class="sxs-lookup"><span data-stu-id="377c9-182">The following example demonstrates submitting two entities in a batch:</span></span>

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

<span data-ttu-id="377c9-183">For successful batch operations, `result` contains information for each operation in the batch.</span><span class="sxs-lookup"><span data-stu-id="377c9-183">For successful batch operations, `result` contains information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="377c9-184">Work with batched operations</span><span class="sxs-lookup"><span data-stu-id="377c9-184">Work with batched operations</span></span>
<span data-ttu-id="377c9-185">You can inspect operations added to a batch by viewing the `operations` property.</span><span class="sxs-lookup"><span data-stu-id="377c9-185">You can inspect operations added to a batch by viewing the `operations` property.</span></span> <span data-ttu-id="377c9-186">You can also use the following methods to work with operations:</span><span class="sxs-lookup"><span data-stu-id="377c9-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="377c9-187">**clear** - Clears all operations from a batch.</span><span class="sxs-lookup"><span data-stu-id="377c9-187">**clear** - Clears all operations from a batch.</span></span>
* <span data-ttu-id="377c9-188">**getOperations** - Gets an operation from the batch.</span><span class="sxs-lookup"><span data-stu-id="377c9-188">**getOperations** - Gets an operation from the batch.</span></span>
* <span data-ttu-id="377c9-189">**hasOperations** - Returns true if the batch contains operations.</span><span class="sxs-lookup"><span data-stu-id="377c9-189">**hasOperations** - Returns true if the batch contains operations.</span></span>
* <span data-ttu-id="377c9-190">**removeOperations** - Removes an operation.</span><span class="sxs-lookup"><span data-stu-id="377c9-190">**removeOperations** - Removes an operation.</span></span>
* <span data-ttu-id="377c9-191">**size** - Returns the number of operations in the batch.</span><span class="sxs-lookup"><span data-stu-id="377c9-191">**size** - Returns the number of operations in the batch.</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="377c9-192">Retrieve an entity by key</span><span class="sxs-lookup"><span data-stu-id="377c9-192">Retrieve an entity by key</span></span>
<span data-ttu-id="377c9-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span><span class="sxs-lookup"><span data-stu-id="377c9-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="377c9-194">After this operation is complete, `result` contains the entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-194">After this operation is complete, `result` contains the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="377c9-195">Query a set of entities</span><span class="sxs-lookup"><span data-stu-id="377c9-195">Query a set of entities</span></span>
<span data-ttu-id="377c9-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span><span class="sxs-lookup"><span data-stu-id="377c9-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="377c9-197">**select** - The fields to be returned from the query.</span><span class="sxs-lookup"><span data-stu-id="377c9-197">**select** - The fields to be returned from the query.</span></span>
* <span data-ttu-id="377c9-198">**where** - The where clause.</span><span class="sxs-lookup"><span data-stu-id="377c9-198">**where** - The where clause.</span></span>

  * <span data-ttu-id="377c9-199">**and** - An `and` where condition.</span><span class="sxs-lookup"><span data-stu-id="377c9-199">**and** - An `and` where condition.</span></span>
  * <span data-ttu-id="377c9-200">**or** - An `or` where condition.</span><span class="sxs-lookup"><span data-stu-id="377c9-200">**or** - An `or` where condition.</span></span>
* <span data-ttu-id="377c9-201">**top** - The number of items to fetch.</span><span class="sxs-lookup"><span data-stu-id="377c9-201">**top** - The number of items to fetch.</span></span>

<span data-ttu-id="377c9-202">The following example builds a query that returns the top five items with a PartitionKey of 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="377c9-202">The following example builds a query that returns the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="377c9-203">Because **select** is not used, all fields are returned.</span><span class="sxs-lookup"><span data-stu-id="377c9-203">Because **select** is not used, all fields are returned.</span></span> <span data-ttu-id="377c9-204">To perform the query against a table, use **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="377c9-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="377c9-205">The following example uses this query to return entities from 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="377c9-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="377c9-206">If successful, `result.entries` contains an array of entities that match the query.</span><span class="sxs-lookup"><span data-stu-id="377c9-206">If successful, `result.entries` contains an array of entities that match the query.</span></span> <span data-ttu-id="377c9-207">If the query was unable to return all entities, `result.continuationToken` is non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span><span class="sxs-lookup"><span data-stu-id="377c9-207">If the query was unable to return all entities, `result.continuationToken` is non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="377c9-208">For the initial query, use *null* for the third parameter.</span><span class="sxs-lookup"><span data-stu-id="377c9-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="377c9-209">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="377c9-209">Query a subset of entity properties</span></span>
<span data-ttu-id="377c9-210">A query to a table can retrieve just a few fields from an entity.</span><span class="sxs-lookup"><span data-stu-id="377c9-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="377c9-211">This reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="377c9-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="377c9-212">Use the **select** clause and pass the names of the fields to return.</span><span class="sxs-lookup"><span data-stu-id="377c9-212">Use the **select** clause and pass the names of the fields to return.</span></span> <span data-ttu-id="377c9-213">For example, the following query returns only the **description** and **dueDate** fields.</span><span class="sxs-lookup"><span data-stu-id="377c9-213">For example, the following query returns only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="377c9-214">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="377c9-214">Delete an entity</span></span>
<span data-ttu-id="377c9-215">You can delete an entity using its partition and row keys.</span><span class="sxs-lookup"><span data-stu-id="377c9-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="377c9-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to delete.</span><span class="sxs-lookup"><span data-stu-id="377c9-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to delete.</span></span> <span data-ttu-id="377c9-217">Then the object is passed to the **deleteEntity** method.</span><span class="sxs-lookup"><span data-stu-id="377c9-217">Then the object is passed to the **deleteEntity** method.</span></span>

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
> <span data-ttu-id="377c9-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span><span class="sxs-lookup"><span data-stu-id="377c9-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="377c9-219">See [Update an entity](#update-an-entity) for information on using ETags.</span><span class="sxs-lookup"><span data-stu-id="377c9-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="377c9-220">Delete a table</span><span class="sxs-lookup"><span data-stu-id="377c9-220">Delete a table</span></span>
<span data-ttu-id="377c9-221">The following code deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="377c9-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="377c9-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="377c9-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="377c9-223">Use continuation tokens</span><span class="sxs-lookup"><span data-stu-id="377c9-223">Use continuation tokens</span></span>
<span data-ttu-id="377c9-224">When you are querying tables for large amounts of results, look for continuation tokens.</span><span class="sxs-lookup"><span data-stu-id="377c9-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="377c9-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span><span class="sxs-lookup"><span data-stu-id="377c9-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="377c9-226">The **results** object returned during querying entities sets a `continuationToken` property when such a token is present.</span><span class="sxs-lookup"><span data-stu-id="377c9-226">The **results** object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="377c9-227">You can then use this when performing a query to continue to move across the partition and table entities.</span><span class="sxs-lookup"><span data-stu-id="377c9-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="377c9-228">When querying, you can provide a `continuationToken` parameter between the query object instance and the callback function:</span><span class="sxs-lookup"><span data-stu-id="377c9-228">When querying, you can provide a `continuationToken` parameter between the query object instance and the callback function:</span></span>

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

<span data-ttu-id="377c9-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span><span class="sxs-lookup"><span data-stu-id="377c9-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="377c9-230">Work with shared access signatures</span><span class="sxs-lookup"><span data-stu-id="377c9-230">Work with shared access signatures</span></span>
<span data-ttu-id="377c9-231">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your Storage account name or keys.</span><span class="sxs-lookup"><span data-stu-id="377c9-231">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your Storage account name or keys.</span></span> <span data-ttu-id="377c9-232">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span><span class="sxs-lookup"><span data-stu-id="377c9-232">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="377c9-233">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span><span class="sxs-lookup"><span data-stu-id="377c9-233">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="377c9-234">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span><span class="sxs-lookup"><span data-stu-id="377c9-234">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="377c9-235">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span><span class="sxs-lookup"><span data-stu-id="377c9-235">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="377c9-236">Note that you must also provide the host information, as it is required when the SAS holder attempts to access the table.</span><span class="sxs-lookup"><span data-stu-id="377c9-236">Note that you must also provide the host information, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="377c9-237">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span><span class="sxs-lookup"><span data-stu-id="377c9-237">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="377c9-238">The following example connects to the table and performs a query.</span><span class="sxs-lookup"><span data-stu-id="377c9-238">The following example connects to the table and performs a query.</span></span>

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

<span data-ttu-id="377c9-239">Because the SAS was generated with only query access, an error is returned if you attempt to insert, update, or delete entities.</span><span class="sxs-lookup"><span data-stu-id="377c9-239">Because the SAS was generated with only query access, an error is returned if you attempt to insert, update, or delete entities.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="377c9-240">Access Control Lists</span><span class="sxs-lookup"><span data-stu-id="377c9-240">Access Control Lists</span></span>
<span data-ttu-id="377c9-241">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span><span class="sxs-lookup"><span data-stu-id="377c9-241">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="377c9-242">This is useful if you want to allow multiple clients to access the table, but provide different access policies for each client.</span><span class="sxs-lookup"><span data-stu-id="377c9-242">This is useful if you want to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="377c9-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span><span class="sxs-lookup"><span data-stu-id="377c9-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="377c9-244">The following example defines two policies, one for 'user1' and one for 'user2':</span><span class="sxs-lookup"><span data-stu-id="377c9-244">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="377c9-245">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="377c9-245">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="377c9-246">This approach allows:</span><span class="sxs-lookup"><span data-stu-id="377c9-246">This approach allows:</span></span>

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

<span data-ttu-id="377c9-247">After the ACL has been set, you can then create a SAS based on the ID for a policy.</span><span class="sxs-lookup"><span data-stu-id="377c9-247">After the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="377c9-248">The following example creates a new SAS for 'user2':</span><span class="sxs-lookup"><span data-stu-id="377c9-248">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="377c9-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="377c9-249">Next steps</span></span>
<span data-ttu-id="377c9-250">For more information, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="377c9-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="377c9-251">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="377c9-251">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="377c9-252">[Azure Storage SDK for Node.js](https://github.com/Azure/azure-storage-node) repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="377c9-252">[Azure Storage SDK for Node.js](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="377c9-253">Azure for Node.js Developers</span><span class="sxs-lookup"><span data-stu-id="377c9-253">Azure for Node.js Developers</span></span>](https://docs.microsoft.com/javascript/azure/?view=azure-node-latest)
* [<span data-ttu-id="377c9-254">Create a Node.js web app in Azure</span><span class="sxs-lookup"><span data-stu-id="377c9-254">Create a Node.js web app in Azure</span></span>](../app-service/app-service-web-get-started-nodejs.md)
* <span data-ttu-id="377c9-255">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="377c9-255">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>
