---
title: How to use Azure Storage Table service or the Azure Cosmos DB Table API from PHP | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: php
ms.topic: sample
ms.date: 04/05/2018
ms.author: sngun
ms.openlocfilehash: 7ca8e786a8284fd958948e313b79e34a6f502120
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864444"
---
# <a name="how-to-use-azure-storage-table-service-or-the-azure-cosmos-db-table-api-from-php"></a><span data-ttu-id="fd052-103">How to use Azure Storage Table service or the Azure Cosmos DB Table API from PHP</span><span class="sxs-lookup"><span data-stu-id="fd052-103">How to use Azure Storage Table service or the Azure Cosmos DB Table API from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

## <a name="overview"></a><span data-ttu-id="fd052-104">Overview</span><span class="sxs-lookup"><span data-stu-id="fd052-104">Overview</span></span>
<span data-ttu-id="fd052-105">This guide shows you how to perform common scenarios using the Azure Storage Table service and the Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="fd052-105">This guide shows you how to perform common scenarios using the Azure Storage Table service and the Azure Cosmos DB Table API.</span></span> <span data-ttu-id="fd052-106">The samples are written in PHP and use the [Azure Storage Table PHP Client Library][download].</span><span class="sxs-lookup"><span data-stu-id="fd052-106">The samples are written in PHP and use the [Azure Storage Table PHP Client Library][download].</span></span> <span data-ttu-id="fd052-107">The scenarios covered include **creating and deleting a table**, and **inserting, deleting, and querying entities in a table**.</span><span class="sxs-lookup"><span data-stu-id="fd052-107">The scenarios covered include **creating and deleting a table**, and **inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="fd052-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="fd052-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>


## <a name="create-an-azure-service-account"></a><span data-ttu-id="fd052-109">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="fd052-109">Create an Azure service account</span></span>

[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="fd052-110">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="fd052-110">Create an Azure storage account</span></span>

[!INCLUDE [cosmos-db-create-storage-account](../../includes/cosmos-db-create-storage-account.md)]

### <a name="create-an-azure-cosmos-db-table-api-account"></a><span data-ttu-id="fd052-111">Create an Azure Cosmos DB Table API account</span><span class="sxs-lookup"><span data-stu-id="fd052-111">Create an Azure Cosmos DB Table API account</span></span>

[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="fd052-112">Create a PHP application</span><span class="sxs-lookup"><span data-stu-id="fd052-112">Create a PHP application</span></span>

<span data-ttu-id="fd052-113">The only requirement to create a PHP application to access the Storage Table service or Azure Cosmos DB Table API is to reference classes in the azure-storage-table SDK for PHP from within your code.</span><span class="sxs-lookup"><span data-stu-id="fd052-113">The only requirement to create a PHP application to access the Storage Table service or Azure Cosmos DB Table API is to reference classes in the azure-storage-table SDK for PHP from within your code.</span></span> <span data-ttu-id="fd052-114">You can use any development tools to create your application, including Notepad.</span><span class="sxs-lookup"><span data-stu-id="fd052-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="fd052-115">In this guide, you use Storage Table service or Azure Cosmos DB features that can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span><span class="sxs-lookup"><span data-stu-id="fd052-115">In this guide, you use Storage Table service or Azure Cosmos DB features that can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-client-library"></a><span data-ttu-id="fd052-116">Get the client library</span><span class="sxs-lookup"><span data-stu-id="fd052-116">Get the client library</span></span>

1. <span data-ttu-id="fd052-117">Create a file named composer.json in the root of your project and add the following code to it:</span><span class="sxs-lookup"><span data-stu-id="fd052-117">Create a file named composer.json in the root of your project and add the following code to it:</span></span>
```json
{
  "require": {
    "microsoft/azure-storage-table": "*"
  }
}
```
2. <span data-ttu-id="fd052-118">Download [composer.phar](http://getcomposer.org/composer.phar) in your root.</span><span class="sxs-lookup"><span data-stu-id="fd052-118">Download [composer.phar](http://getcomposer.org/composer.phar) in your root.</span></span> 
3. <span data-ttu-id="fd052-119">Open a command prompt and execute the following command in your project root:</span><span class="sxs-lookup"><span data-stu-id="fd052-119">Open a command prompt and execute the following command in your project root:</span></span>
```
php composer.phar install
```
<span data-ttu-id="fd052-120">Alternatively, go to the [Azure Storage Table PHP Client Library](https://github.com/Azure/azure-storage-php/tree/master/azure-storage-table) on GitHub to clone the source code.</span><span class="sxs-lookup"><span data-stu-id="fd052-120">Alternatively, go to the [Azure Storage Table PHP Client Library](https://github.com/Azure/azure-storage-php/tree/master/azure-storage-table) on GitHub to clone the source code.</span></span>


## <a name="add-required-references"></a><span data-ttu-id="fd052-121">Add required references</span><span class="sxs-lookup"><span data-stu-id="fd052-121">Add required references</span></span>
<span data-ttu-id="fd052-122">To use the Storage Table service or Azure Cosmos DB APIs, you must:</span><span class="sxs-lookup"><span data-stu-id="fd052-122">To use the Storage Table service or Azure Cosmos DB APIs, you must:</span></span>

* <span data-ttu-id="fd052-123">Reference the autoloader file using the [require_once][require_once] statement, and</span><span class="sxs-lookup"><span data-stu-id="fd052-123">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
* <span data-ttu-id="fd052-124">Reference any classes you use.</span><span class="sxs-lookup"><span data-stu-id="fd052-124">Reference any classes you use.</span></span>

<span data-ttu-id="fd052-125">The following example shows how to include the autoloader file and reference the **TableRestProxy** class.</span><span class="sxs-lookup"><span data-stu-id="fd052-125">The following example shows how to include the autoloader file and reference the **TableRestProxy** class.</span></span>

```php
require_once 'vendor/autoload.php';
use MicrosoftAzure\Storage\Table\TableRestProxy;
```

<span data-ttu-id="fd052-126">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span><span class="sxs-lookup"><span data-stu-id="fd052-126">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="add-a-storage-table-service-connection"></a><span data-ttu-id="fd052-127">Add a Storage Table service connection</span><span class="sxs-lookup"><span data-stu-id="fd052-127">Add a Storage Table service connection</span></span>
<span data-ttu-id="fd052-128">To instantiate a Storage Table service client, you must first have a valid connection string.</span><span class="sxs-lookup"><span data-stu-id="fd052-128">To instantiate a Storage Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="fd052-129">The format for the Storage Table service connection string is:</span><span class="sxs-lookup"><span data-stu-id="fd052-129">The format for the Storage Table service connection string is:</span></span>

```php
$connectionString = "DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]"
```

## <a name="add-an-azure-cosmos-db-connection"></a><span data-ttu-id="fd052-130">Add an Azure Cosmos DB connection</span><span class="sxs-lookup"><span data-stu-id="fd052-130">Add an Azure Cosmos DB connection</span></span>
<span data-ttu-id="fd052-131">To instantiate an Azure Cosmos DB Table client, you must first have a valid connection string.</span><span class="sxs-lookup"><span data-stu-id="fd052-131">To instantiate an Azure Cosmos DB Table client, you must first have a valid connection string.</span></span> <span data-ttu-id="fd052-132">The format for the Azure Cosmos DB connection string is:</span><span class="sxs-lookup"><span data-stu-id="fd052-132">The format for the Azure Cosmos DB connection string is:</span></span>

```php
$connectionString = "DefaultEndpointsProtocol=[https];AccountName=[myaccount];AccountKey=[myaccountkey];TableEndpoint=[https://myendpoint/]";
```

## <a name="add-a-storage-emulator-connection"></a><span data-ttu-id="fd052-133">Add a Storage emulator connection</span><span class="sxs-lookup"><span data-stu-id="fd052-133">Add a Storage emulator connection</span></span>
<span data-ttu-id="fd052-134">To access the emulator storage:</span><span class="sxs-lookup"><span data-stu-id="fd052-134">To access the emulator storage:</span></span>

```php
UseDevelopmentStorage = true
```

<span data-ttu-id="fd052-135">To create an Azure Table service client or Azure Cosmos DB client, you need to use the **TableRestProxy** class.</span><span class="sxs-lookup"><span data-stu-id="fd052-135">To create an Azure Table service client or Azure Cosmos DB client, you need to use the **TableRestProxy** class.</span></span> <span data-ttu-id="fd052-136">You can:</span><span class="sxs-lookup"><span data-stu-id="fd052-136">You can:</span></span>

* <span data-ttu-id="fd052-137">Pass the connection string directly to it or</span><span class="sxs-lookup"><span data-stu-id="fd052-137">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="fd052-138">Use the **CloudConfigurationManager  (CCM)** to check multiple external sources for the connection string:</span><span class="sxs-lookup"><span data-stu-id="fd052-138">Use the **CloudConfigurationManager  (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="fd052-139">By default, it comes with support for one external source - environmental variables.</span><span class="sxs-lookup"><span data-stu-id="fd052-139">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="fd052-140">You can add new sources by extending the `ConnectionStringSource` class.</span><span class="sxs-lookup"><span data-stu-id="fd052-140">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="fd052-141">For the examples outlined here, the connection string is passed directly.</span><span class="sxs-lookup"><span data-stu-id="fd052-141">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;

$tableClient = TableRestProxy::createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="fd052-142">Create a table</span><span class="sxs-lookup"><span data-stu-id="fd052-142">Create a table</span></span>
<span data-ttu-id="fd052-143">A **TableRestProxy** object lets you create a table with the **createTable** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-143">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="fd052-144">When creating a table, you can set the Table service timeout.</span><span class="sxs-lookup"><span data-stu-id="fd052-144">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="fd052-145">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="fd052-145">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

```php
require_once 'vendor\autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;

// Create Table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

try    {
    // Create table.
    $tableClient->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
}
```

<span data-ttu-id="fd052-146">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="fd052-146">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="fd052-147">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="fd052-147">Add an entity to a table</span></span>
<span data-ttu-id="fd052-148">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd052-148">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="fd052-149">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="fd052-149">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="fd052-150">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span><span class="sxs-lookup"><span data-stu-id="fd052-150">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="fd052-151">The system uses `PartitionKey` to automatically distribute the table's entities over many Storage nodes.</span><span class="sxs-lookup"><span data-stu-id="fd052-151">The system uses `PartitionKey` to automatically distribute the table's entities over many Storage nodes.</span></span> <span data-ttu-id="fd052-152">Entities with the same `PartitionKey` are stored on the same node.</span><span class="sxs-lookup"><span data-stu-id="fd052-152">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="fd052-153">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span><span class="sxs-lookup"><span data-stu-id="fd052-153">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableClient->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

<span data-ttu-id="fd052-154">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="fd052-154">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="fd052-155">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd052-155">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="fd052-156">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span><span class="sxs-lookup"><span data-stu-id="fd052-156">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="fd052-157">Each method will insert the entity if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="fd052-157">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="fd052-158">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span><span class="sxs-lookup"><span data-stu-id="fd052-158">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="fd052-159">The following example shows how to use **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd052-159">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="fd052-160">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span><span class="sxs-lookup"><span data-stu-id="fd052-160">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="fd052-161">However, if it has previously been inserted (as shown in the example above), the `DueDate` property is updated, and the `Status` property is added.</span><span class="sxs-lookup"><span data-stu-id="fd052-161">However, if it has previously been inserted (as shown in the example above), the `DueDate` property is updated, and the `Status` property is added.</span></span> <span data-ttu-id="fd052-162">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span><span class="sxs-lookup"><span data-stu-id="fd052-162">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="fd052-163">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span><span class="sxs-lookup"><span data-stu-id="fd052-163">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableClient->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="fd052-164">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="fd052-164">Retrieve a single entity</span></span>
<span data-ttu-id="fd052-165">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="fd052-165">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="fd052-166">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-166">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

try    {
    $result = $tableClient->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="fd052-167">Retrieve all entities in a partition</span><span class="sxs-lookup"><span data-stu-id="fd052-167">Retrieve all entities in a partition</span></span>
<span data-ttu-id="fd052-168">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span><span class="sxs-lookup"><span data-stu-id="fd052-168">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="fd052-169">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span><span class="sxs-lookup"><span data-stu-id="fd052-169">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="fd052-170">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-170">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableClient->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="fd052-171">Retrieve a subset of entities in a partition</span><span class="sxs-lookup"><span data-stu-id="fd052-171">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="fd052-172">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span><span class="sxs-lookup"><span data-stu-id="fd052-172">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="fd052-173">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span><span class="sxs-lookup"><span data-stu-id="fd052-173">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableClient->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="fd052-174">Retrieve a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="fd052-174">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="fd052-175">A query can retrieve a subset of entity properties.</span><span class="sxs-lookup"><span data-stu-id="fd052-175">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="fd052-176">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="fd052-176">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="fd052-177">To specify a property to retrieve, pass the name of the property to the **Query->addSelectField** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-177">To specify a property to retrieve, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="fd052-178">You can call this method multiple times to add more properties.</span><span class="sxs-lookup"><span data-stu-id="fd052-178">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="fd052-179">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span><span class="sxs-lookup"><span data-stu-id="fd052-179">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="fd052-180">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span><span class="sxs-lookup"><span data-stu-id="fd052-180">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableClient->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="fd052-181">Update an entity</span><span class="sxs-lookup"><span data-stu-id="fd052-181">Update an entity</span></span>
<span data-ttu-id="fd052-182">You can update an existing entity by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd052-182">You can update an existing entity by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="fd052-183">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span><span class="sxs-lookup"><span data-stu-id="fd052-183">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="fd052-184">Note that you can remove a property by setting its value to **null**.</span><span class="sxs-lookup"><span data-stu-id="fd052-184">Note that you can remove a property by setting its value to **null**.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

$result = $tableClient->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();
$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.
$entity->setPropertyValue("Location", null); //Removed Location.
$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableClient->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="fd052-185">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="fd052-185">Delete an entity</span></span>
<span data-ttu-id="fd052-186">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-186">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

try    {
    // Delete entity.
    $tableClient->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="fd052-187">For concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span><span class="sxs-lookup"><span data-stu-id="fd052-187">For concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="fd052-188">Batch table operations</span><span class="sxs-lookup"><span data-stu-id="fd052-188">Batch table operations</span></span>
<span data-ttu-id="fd052-189">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span><span class="sxs-lookup"><span data-stu-id="fd052-189">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="fd052-190">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-190">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="fd052-191">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span><span class="sxs-lookup"><span data-stu-id="fd052-191">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="fd052-192">**addInsertEntity** (adds an insertEntity operation)</span><span class="sxs-lookup"><span data-stu-id="fd052-192">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="fd052-193">**addUpdateEntity** (adds an updateEntity operation)</span><span class="sxs-lookup"><span data-stu-id="fd052-193">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="fd052-194">**addMergeEntity** (adds a mergeEntity operation)</span><span class="sxs-lookup"><span data-stu-id="fd052-194">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="fd052-195">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span><span class="sxs-lookup"><span data-stu-id="fd052-195">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="fd052-196">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span><span class="sxs-lookup"><span data-stu-id="fd052-196">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="fd052-197">**addDeleteEntity** (adds a deleteEntity operation)</span><span class="sxs-lookup"><span data-stu-id="fd052-197">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="fd052-198">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request.</span><span class="sxs-lookup"><span data-stu-id="fd052-198">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request.</span></span> 

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

// Configure a connection string for Storage Table service.
$connectionString = "DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]"

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableClient->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="fd052-199">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="fd052-199">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="fd052-200">Delete a table</span><span class="sxs-lookup"><span data-stu-id="fd052-200">Delete a table</span></span>
<span data-ttu-id="fd052-201">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span><span class="sxs-lookup"><span data-stu-id="fd052-201">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

```php
require_once 'vendor/autoload.php';

use MicrosoftAzure\Storage\Table\TableRestProxy;
use MicrosoftAzure\Storage\Common\Exceptions\ServiceException;

// Create table REST proxy.
$tableClient = TableRestProxy::createTableService($connectionString);

try    {
    // Delete table.
    $tableClient->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Table-Service-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="fd052-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd052-202">Next steps</span></span>
<span data-ttu-id="fd052-203">Now that you've learned the basics of the Azure Table service and Azure Cosmos DB, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="fd052-203">Now that you've learned the basics of the Azure Table service and Azure Cosmos DB, follow these links to learn more.</span></span>

* <span data-ttu-id="fd052-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="fd052-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="fd052-205">[PHP Developer Center](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="fd052-205">[PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[download]: https://packagist.org/packages/microsoft/azure-storage-table
[require_once]: http://php.net/require_once
[table-service-timeouts]: https://docs.microsoft.com/rest/api/storageservices/setting-timeouts-for-table-service-operations

[table-data-model]: https://docs.microsoft.com/rest/api/storageservices/Understanding-the-Table-Service-Data-Model
[filters]: https://docs.microsoft.com/rest/api/storageservices/Querying-Tables-and-Entities
[entity-group-transactions]: https://docs.microsoft.com/rest/api/storageservices/Performing-Entity-Group-Transactions
