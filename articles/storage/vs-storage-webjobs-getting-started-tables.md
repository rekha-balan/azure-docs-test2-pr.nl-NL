---
title: Getting Started with Azure storage and Visual Studio connected services (WebJob projects)
description: How to get started using Azure Table storage in an Azure WebJobs project in Visual Studio after connecting to a storage account using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 9a3f511c38e1b723d1e4997dea8fd896260af1bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551007"
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="a2ab9-103">Getting Started with Azure Storage (Azure WebJob Projects)</span><span class="sxs-lookup"><span data-stu-id="a2ab9-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="a2ab9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a2ab9-104">Overview</span></span>
<span data-ttu-id="a2ab9-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="a2ab9-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="a2ab9-107">The Azure Table storage service enables you to store large amounts of structured data.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="a2ab9-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="a2ab9-109">Azure tables are ideal for storing structured, non-relational data.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="a2ab9-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="a2ab9-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="a2ab9-112">How to add entities to a table</span><span class="sxs-lookup"><span data-stu-id="a2ab9-112">How to add entities to a table</span></span>
<span data-ttu-id="a2ab9-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="a2ab9-114">The attribute constructor takes a string parameter that specifies the name of the table.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="a2ab9-115">The following code sample adds **Person** entities to a table named *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="a2ab9-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="a2ab9-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="a2ab9-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="a2ab9-119">Real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="a2ab9-119">Real-time monitoring</span></span>
<span data-ttu-id="a2ab9-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="a2ab9-121">The **Invocation Log** section tells you if the function is still running.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Ingress function running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="a2ab9-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Ingress function running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="a2ab9-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Ingress function finished](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="a2ab9-127">How to read multiple entities from a table</span><span class="sxs-lookup"><span data-stu-id="a2ab9-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="a2ab9-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="a2ab9-129">The following code sample reads and logs all rows from the **Ingress** table:</span><span class="sxs-lookup"><span data-stu-id="a2ab9-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="a2ab9-130">How to read a single entity from a table</span><span class="sxs-lookup"><span data-stu-id="a2ab9-130">How to read a single entity from a table</span></span>
<span data-ttu-id="a2ab9-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="a2ab9-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span><span class="sxs-lookup"><span data-stu-id="a2ab9-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="a2ab9-133">The **Person** class in this example does not have to implement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="a2ab9-134">How to use the .NET Storage API directly to work with a table</span><span class="sxs-lookup"><span data-stu-id="a2ab9-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="a2ab9-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="a2ab9-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="a2ab9-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="a2ab9-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="a2ab9-138">Related topics covered by the queues how-to article</span><span class="sxs-lookup"><span data-stu-id="a2ab9-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="a2ab9-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="a2ab9-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2ab9-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2ab9-140">Next steps</span></span>
<span data-ttu-id="a2ab9-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span><span class="sxs-lookup"><span data-stu-id="a2ab9-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="a2ab9-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="a2ab9-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>




