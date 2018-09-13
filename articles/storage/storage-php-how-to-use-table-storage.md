---
title: How to use table storage from PHP | Microsoft Docs
description: Learn how to use the Table service from PHP to create and delete a table, and insert, delete, and query the table.
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e9fd8855cf0c51df5f3ec4f80a733e778996fb82
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670026"
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="e6789-103">How to use table storage from PHP</span><span class="sxs-lookup"><span data-stu-id="e6789-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="e6789-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e6789-104">Overview</span></span>
<span data-ttu-id="e6789-105">This guide shows you how to perform common scenarios using the Azure Table service.</span><span class="sxs-lookup"><span data-stu-id="e6789-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="e6789-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span><span class="sxs-lookup"><span data-stu-id="e6789-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="e6789-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span><span class="sxs-lookup"><span data-stu-id="e6789-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="e6789-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="e6789-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e6789-109">Create a PHP application</span><span class="sxs-lookup"><span data-stu-id="e6789-109">Create a PHP application</span></span>
<span data-ttu-id="e6789-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span><span class="sxs-lookup"><span data-stu-id="e6789-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="e6789-111">You can use any development tools to create your application, including Notepad.</span><span class="sxs-lookup"><span data-stu-id="e6789-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="e6789-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span><span class="sxs-lookup"><span data-stu-id="e6789-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="e6789-113">Get the Azure Client Libraries</span><span class="sxs-lookup"><span data-stu-id="e6789-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="e6789-114">Configure your application to access the Table service</span><span class="sxs-lookup"><span data-stu-id="e6789-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="e6789-115">To use the Azure Table service APIs, you need to:</span><span class="sxs-lookup"><span data-stu-id="e6789-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="e6789-116">Reference the autoloader file using the [require_once][require_once] statement, and</span><span class="sxs-lookup"><span data-stu-id="e6789-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="e6789-117">Reference any classes you might use.</span><span class="sxs-lookup"><span data-stu-id="e6789-117">Reference any classes you might use.</span></span>

<span data-ttu-id="e6789-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span><span class="sxs-lookup"><span data-stu-id="e6789-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="e6789-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="e6789-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e6789-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span><span class="sxs-lookup"><span data-stu-id="e6789-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="e6789-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span><span class="sxs-lookup"><span data-stu-id="e6789-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="e6789-122">Set up an Azure storage connection</span><span class="sxs-lookup"><span data-stu-id="e6789-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="e6789-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span><span class="sxs-lookup"><span data-stu-id="e6789-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="e6789-124">The format for the Table service connection string is:</span><span class="sxs-lookup"><span data-stu-id="e6789-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="e6789-125">For accessing a live service:</span><span class="sxs-lookup"><span data-stu-id="e6789-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="e6789-126">For accessing the emulator storage:</span><span class="sxs-lookup"><span data-stu-id="e6789-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="e6789-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span><span class="sxs-lookup"><span data-stu-id="e6789-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="e6789-128">You can:</span><span class="sxs-lookup"><span data-stu-id="e6789-128">You can:</span></span>

* <span data-ttu-id="e6789-129">pass the connection string directly to it or</span><span class="sxs-lookup"><span data-stu-id="e6789-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="e6789-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span><span class="sxs-lookup"><span data-stu-id="e6789-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="e6789-131">by default, it comes with support for one external source - environmental variables</span><span class="sxs-lookup"><span data-stu-id="e6789-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="e6789-132">you can add new sources by extending the **ConnectionStringSource** class</span><span class="sxs-lookup"><span data-stu-id="e6789-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="e6789-133">For the examples outlined here, the connection string will be passed directly.</span><span class="sxs-lookup"><span data-stu-id="e6789-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="e6789-134">Create a table</span><span class="sxs-lookup"><span data-stu-id="e6789-134">Create a table</span></span>
<span data-ttu-id="e6789-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="e6789-136">When creating a table, you can set the Table service timeout.</span><span class="sxs-lookup"><span data-stu-id="e6789-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="e6789-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="e6789-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

<span data-ttu-id="e6789-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="e6789-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e6789-139">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="e6789-139">Add an entity to a table</span></span>
<span data-ttu-id="e6789-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="e6789-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="e6789-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="e6789-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="e6789-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span><span class="sxs-lookup"><span data-stu-id="e6789-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="e6789-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span><span class="sxs-lookup"><span data-stu-id="e6789-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="e6789-144">Entities with the same `PartitionKey` are stored on the same node.</span><span class="sxs-lookup"><span data-stu-id="e6789-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="e6789-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span><span class="sxs-lookup"><span data-stu-id="e6789-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

<span data-ttu-id="e6789-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="e6789-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="e6789-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="e6789-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="e6789-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span><span class="sxs-lookup"><span data-stu-id="e6789-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="e6789-149">Each method will insert the entity if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="e6789-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="e6789-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span><span class="sxs-lookup"><span data-stu-id="e6789-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="e6789-151">The following example shows how to use **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="e6789-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="e6789-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span><span class="sxs-lookup"><span data-stu-id="e6789-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="e6789-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span><span class="sxs-lookup"><span data-stu-id="e6789-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="e6789-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span><span class="sxs-lookup"><span data-stu-id="e6789-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="e6789-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span><span class="sxs-lookup"><span data-stu-id="e6789-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

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
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="e6789-156">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="e6789-156">Retrieve a single entity</span></span>
<span data-ttu-id="e6789-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="e6789-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="e6789-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="e6789-159">Retrieve all entities in a partition</span><span class="sxs-lookup"><span data-stu-id="e6789-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="e6789-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span><span class="sxs-lookup"><span data-stu-id="e6789-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="e6789-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span><span class="sxs-lookup"><span data-stu-id="e6789-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="e6789-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="e6789-163">Retrieve a subset of entities in a partition</span><span class="sxs-lookup"><span data-stu-id="e6789-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="e6789-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span><span class="sxs-lookup"><span data-stu-id="e6789-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="e6789-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span><span class="sxs-lookup"><span data-stu-id="e6789-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="e6789-166">Retrieve a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="e6789-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="e6789-167">A query can retrieve a subset of entity properties.</span><span class="sxs-lookup"><span data-stu-id="e6789-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="e6789-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="e6789-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="e6789-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="e6789-170">You can call this method multiple times to add more properties.</span><span class="sxs-lookup"><span data-stu-id="e6789-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="e6789-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span><span class="sxs-lookup"><span data-stu-id="e6789-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="e6789-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span><span class="sxs-lookup"><span data-stu-id="e6789-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
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

## <a name="update-an-entity"></a><span data-ttu-id="e6789-173">Update an entity</span><span class="sxs-lookup"><span data-stu-id="e6789-173">Update an entity</span></span>
<span data-ttu-id="e6789-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="e6789-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="e6789-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span><span class="sxs-lookup"><span data-stu-id="e6789-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="e6789-176">Note that you can remove a property by setting its value to **null**.</span><span class="sxs-lookup"><span data-stu-id="e6789-176">Note that you can remove a property by setting its value to **null**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="e6789-177">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="e6789-177">Delete an entity</span></span>
<span data-ttu-id="e6789-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="e6789-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span><span class="sxs-lookup"><span data-stu-id="e6789-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="e6789-180">Batch table operations</span><span class="sxs-lookup"><span data-stu-id="e6789-180">Batch table operations</span></span>
<span data-ttu-id="e6789-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span><span class="sxs-lookup"><span data-stu-id="e6789-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="e6789-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="e6789-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span><span class="sxs-lookup"><span data-stu-id="e6789-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="e6789-184">**addInsertEntity** (adds an insertEntity operation)</span><span class="sxs-lookup"><span data-stu-id="e6789-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="e6789-185">**addUpdateEntity** (adds an updateEntity operation)</span><span class="sxs-lookup"><span data-stu-id="e6789-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="e6789-186">**addMergeEntity** (adds a mergeEntity operation)</span><span class="sxs-lookup"><span data-stu-id="e6789-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="e6789-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span><span class="sxs-lookup"><span data-stu-id="e6789-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="e6789-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span><span class="sxs-lookup"><span data-stu-id="e6789-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="e6789-189">**addDeleteEntity** (adds a deleteEntity operation)</span><span class="sxs-lookup"><span data-stu-id="e6789-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="e6789-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span><span class="sxs-lookup"><span data-stu-id="e6789-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

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
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="e6789-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="e6789-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="e6789-192">Delete a table</span><span class="sxs-lookup"><span data-stu-id="e6789-192">Delete a table</span></span>
<span data-ttu-id="e6789-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span><span class="sxs-lookup"><span data-stu-id="e6789-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="e6789-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6789-194">Next steps</span></span>
<span data-ttu-id="e6789-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span><span class="sxs-lookup"><span data-stu-id="e6789-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="e6789-196">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="e6789-196">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>

<span data-ttu-id="e6789-197">For more information, see also the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e6789-197">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
