---
title: NoSQL Python examples for DocumentDB | Microsoft Docs
description: Find NoSQL Python examples on github for common tasks in DocumentDB, including CRUD operations for JSON documents in NoSQL databases.
keywords: python examples
services: documentdb
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2016
ms.author: moderakh
ms.openlocfilehash: 7b555732bad08c86c33ee78344ae9c4e6af7c7b8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553195"
---
# <a name="documentdb-python-examples"></a><span data-ttu-id="bd4a8-104">DocumentDB Python examples</span><span class="sxs-lookup"><span data-stu-id="bd4a8-104">DocumentDB Python examples</span></span>
> [!div class="op_single_selector"]
> * [.NET Examples](documentdb-dotnet-samples.md)
> * [Node.js Examples](documentdb-nodejs-samples.md)
> * [Python Examples](documentdb-python-samples.md)
> * [Azure Code Sample Gallery](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

<span data-ttu-id="bd4a8-109">Sample solutions that perform CRUD operations and other common operations on Azure DocumentDB resources are included in the [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-109">Sample solutions that perform CRUD operations and other common operations on Azure DocumentDB resources are included in the [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span></span> <span data-ttu-id="bd4a8-110">This article provides:</span><span class="sxs-lookup"><span data-stu-id="bd4a8-110">This article provides:</span></span>

* <span data-ttu-id="bd4a8-111">Links to the tasks in each of the Python example project files.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-111">Links to the tasks in each of the Python example project files.</span></span> 
* <span data-ttu-id="bd4a8-112">Links to the related API reference content.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-112">Links to the related API reference content.</span></span>

<span data-ttu-id="bd4a8-113">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="bd4a8-113">**Prerequisites**</span></span>

1. <span data-ttu-id="bd4a8-114">You need an Azure account to use these Python examples:</span><span class="sxs-lookup"><span data-stu-id="bd4a8-114">You need an Azure account to use these Python examples:</span></span>
   * <span data-ttu-id="bd4a8-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="bd4a8-116">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-116">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
     * <span data-ttu-id="bd4a8-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
2. <span data-ttu-id="bd4a8-118">You also need the [Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="bd4a8-118">You also need the [Python SDK](documentdb-sdk-python.md).</span></span> 
   
   > [!NOTE]
   > Each sample is self-contained, it sets itself up and cleans up after itself. As such, the samples issue multiple calls to [document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Each time this is done your subscription will be billed for 1 hour of usage per the performance tier of the collection being created. 
   > 
   > 

## <a name="database-examples"></a><span data-ttu-id="bd4a8-122">Database examples</span><span class="sxs-lookup"><span data-stu-id="bd4a8-122">Database examples</span></span>
<span data-ttu-id="bd4a8-123">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of the [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how to perform the following tasks.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-123">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of the [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how to perform the following tasks.</span></span>

| <span data-ttu-id="bd4a8-124">Task</span><span class="sxs-lookup"><span data-stu-id="bd4a8-124">Task</span></span> | <span data-ttu-id="bd4a8-125">API reference</span><span class="sxs-lookup"><span data-stu-id="bd4a8-125">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="bd4a8-126">Create a database</span><span class="sxs-lookup"><span data-stu-id="bd4a8-126">Create a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[<span data-ttu-id="bd4a8-127">document_client.CreateDatabase</span><span class="sxs-lookup"><span data-stu-id="bd4a8-127">document_client.CreateDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="bd4a8-128">Query an account for a database</span><span class="sxs-lookup"><span data-stu-id="bd4a8-128">Query an account for a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[<span data-ttu-id="bd4a8-129">document_client.QueryDatabases</span><span class="sxs-lookup"><span data-stu-id="bd4a8-129">document_client.QueryDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="bd4a8-130">Read a database by Id</span><span class="sxs-lookup"><span data-stu-id="bd4a8-130">Read a database by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[<span data-ttu-id="bd4a8-131">document_client.ReadDatabase</span><span class="sxs-lookup"><span data-stu-id="bd4a8-131">document_client.ReadDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="bd4a8-132">List databases for an account</span><span class="sxs-lookup"><span data-stu-id="bd4a8-132">List databases for an account</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[<span data-ttu-id="bd4a8-133">document_client.ReadDatabases</span><span class="sxs-lookup"><span data-stu-id="bd4a8-133">document_client.ReadDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="bd4a8-134">Delete a database</span><span class="sxs-lookup"><span data-stu-id="bd4a8-134">Delete a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[<span data-ttu-id="bd4a8-135">document_client.DeleteDatabase</span><span class="sxs-lookup"><span data-stu-id="bd4a8-135">document_client.DeleteDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a><span data-ttu-id="bd4a8-136">Collection examples</span><span class="sxs-lookup"><span data-stu-id="bd4a8-136">Collection examples</span></span>
<span data-ttu-id="bd4a8-137">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of the [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how to perform the following tasks.</span><span class="sxs-lookup"><span data-stu-id="bd4a8-137">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of the [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how to perform the following tasks.</span></span>

| <span data-ttu-id="bd4a8-138">Task</span><span class="sxs-lookup"><span data-stu-id="bd4a8-138">Task</span></span> | <span data-ttu-id="bd4a8-139">API reference</span><span class="sxs-lookup"><span data-stu-id="bd4a8-139">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="bd4a8-140">Create a collection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-140">Create a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[<span data-ttu-id="bd4a8-141">document_client.CreateCollection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-141">document_client.CreateCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="bd4a8-142">Read a list of all collections in a database</span><span class="sxs-lookup"><span data-stu-id="bd4a8-142">Read a list of all collections in a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[<span data-ttu-id="bd4a8-143">document_client.ListCollections</span><span class="sxs-lookup"><span data-stu-id="bd4a8-143">document_client.ListCollections</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="bd4a8-144">Get a collection by Id</span><span class="sxs-lookup"><span data-stu-id="bd4a8-144">Get a collection by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[<span data-ttu-id="bd4a8-145">document_client.ReadCollection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-145">document_client.ReadCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="bd4a8-146">Get performance tier of a collection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-146">Get performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[<span data-ttu-id="bd4a8-147">DocumentQueryable.QueryOffers</span><span class="sxs-lookup"><span data-stu-id="bd4a8-147">DocumentQueryable.QueryOffers</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="bd4a8-148">Change performance tier of a collection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-148">Change performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[<span data-ttu-id="bd4a8-149">document_client.ReplaceOffer</span><span class="sxs-lookup"><span data-stu-id="bd4a8-149">document_client.ReplaceOffer</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="bd4a8-150">Delete a collection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-150">Delete a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[<span data-ttu-id="bd4a8-151">document_client.DeleteCollection</span><span class="sxs-lookup"><span data-stu-id="bd4a8-151">document_client.DeleteCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

