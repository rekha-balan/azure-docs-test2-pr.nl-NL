---
title: How to use Azure table storage with the WebJobs SDK
description: Learn how to use Azure table storage with the WebJobs SDK. Create tables, add entities to tables, and read existing tables.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 41263de76392eb47f32e87eb38c93ce7efda7a63
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551138"
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="48631-104">How to use Azure table storage with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="48631-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="48631-105">Overview</span><span class="sxs-lookup"><span data-stu-id="48631-105">Overview</span></span>
<span data-ttu-id="48631-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="48631-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="48631-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="48631-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="48631-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span><span class="sxs-lookup"><span data-stu-id="48631-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <a id="ingress"></a> <span data-ttu-id="48631-109">How to add entities to a table</span><span class="sxs-lookup"><span data-stu-id="48631-109">How to add entities to a table</span></span>
<span data-ttu-id="48631-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span><span class="sxs-lookup"><span data-stu-id="48631-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="48631-111">The attribute constructor takes a string parameter that specifies the name of the table.</span><span class="sxs-lookup"><span data-stu-id="48631-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="48631-112">The following code sample adds `Person` entities to a table named *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="48631-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="48631-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span><span class="sxs-lookup"><span data-stu-id="48631-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="48631-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span><span class="sxs-lookup"><span data-stu-id="48631-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="48631-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span><span class="sxs-lookup"><span data-stu-id="48631-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <a id="monitor"></a> <span data-ttu-id="48631-116">Real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="48631-116">Real-time monitoring</span></span>
<span data-ttu-id="48631-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span><span class="sxs-lookup"><span data-stu-id="48631-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="48631-118">The **Invocation Log** section tells you if the function is still running.</span><span class="sxs-lookup"><span data-stu-id="48631-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Ingress function running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="48631-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span><span class="sxs-lookup"><span data-stu-id="48631-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Ingress function running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="48631-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span><span class="sxs-lookup"><span data-stu-id="48631-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Ingress function finished](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a> <span data-ttu-id="48631-124">How to read multiple entities from a table</span><span class="sxs-lookup"><span data-stu-id="48631-124">How to read multiple entities from a table</span></span>
<span data-ttu-id="48631-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="48631-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="48631-126">The following code sample reads and logs all rows from the `Ingress` table:</span><span class="sxs-lookup"><span data-stu-id="48631-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a id="readone"></a> <span data-ttu-id="48631-127">How to read a single entity from a table</span><span class="sxs-lookup"><span data-stu-id="48631-127">How to read a single entity from a table</span></span>
<span data-ttu-id="48631-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span><span class="sxs-lookup"><span data-stu-id="48631-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="48631-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span><span class="sxs-lookup"><span data-stu-id="48631-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="48631-130">The `Person` class in this example does not have to implement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="48631-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <a id="storageapi"></a> <span data-ttu-id="48631-131">How to use the .NET Storage API directly to work with a table</span><span class="sxs-lookup"><span data-stu-id="48631-131">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="48631-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span><span class="sxs-lookup"><span data-stu-id="48631-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="48631-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span><span class="sxs-lookup"><span data-stu-id="48631-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="48631-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="48631-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span> 

## <a id="queues"></a><span data-ttu-id="48631-135">Related topics covered by the queues how-to article</span><span class="sxs-lookup"><span data-stu-id="48631-135">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="48631-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="48631-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="48631-137">Topics covered in that article include the following:</span><span class="sxs-lookup"><span data-stu-id="48631-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="48631-138">Async functions</span><span class="sxs-lookup"><span data-stu-id="48631-138">Async functions</span></span>
* <span data-ttu-id="48631-139">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="48631-139">Multiple instances</span></span>
* <span data-ttu-id="48631-140">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="48631-140">Graceful shutdown</span></span>
* <span data-ttu-id="48631-141">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="48631-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="48631-142">Set the SDK connection strings in code</span><span class="sxs-lookup"><span data-stu-id="48631-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="48631-143">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="48631-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="48631-144">Trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="48631-144">Trigger a function manually</span></span>
* <span data-ttu-id="48631-145">Write logs</span><span class="sxs-lookup"><span data-stu-id="48631-145">Write logs</span></span>

## <a id="nextsteps"></a> <span data-ttu-id="48631-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="48631-146">Next steps</span></span>
<span data-ttu-id="48631-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span><span class="sxs-lookup"><span data-stu-id="48631-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="48631-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="48631-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>




