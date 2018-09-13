---
title: 'What is DocumentDB: API for MongoDB? | Microsoft Docs'
description: 'Learn about DocumentDB: API for MongoDB and how you can easily run existing MongoDB applications in the Azure cloud'
keywords: what is MongoDB
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: anhoh
ms.openlocfilehash: f173fa709f2a7a21042752ba4b5ac936d01fe300
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661235"
---
# <a name="what-is-documentdb-api-for-mongodb"></a><span data-ttu-id="5baca-105">What is DocumentDB: API for MongoDB?</span><span class="sxs-lookup"><span data-stu-id="5baca-105">What is DocumentDB: API for MongoDB?</span></span>

<span data-ttu-id="5baca-106">DocumentDB databases can now be used as the data store for apps written for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5baca-106">DocumentDB databases can now be used as the data store for apps written for MongoDB.</span></span> <span data-ttu-id="5baca-107">This means that by using existing [drivers](https://docs.mongodb.org/ecosystem/drivers/) for MongoDB databases, your application written for MongoDB can now communicate with DocumentDB and use DocumentDB databases instead of MongoDB databases.</span><span class="sxs-lookup"><span data-stu-id="5baca-107">This means that by using existing [drivers](https://docs.mongodb.org/ecosystem/drivers/) for MongoDB databases, your application written for MongoDB can now communicate with DocumentDB and use DocumentDB databases instead of MongoDB databases.</span></span> <span data-ttu-id="5baca-108">In many cases, you can switch from using MongoDB to DocumentDB by simply changing a connection string.</span><span class="sxs-lookup"><span data-stu-id="5baca-108">In many cases, you can switch from using MongoDB to DocumentDB by simply changing a connection string.</span></span> <span data-ttu-id="5baca-109">Using this functionality, customers can easily build and run MongoDB database applications in the Azure cloud - leveraging DocumentDB's fully managed and scalable NoSQL databases - while continuing to use familiar skills and tools for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5baca-109">Using this functionality, customers can easily build and run MongoDB database applications in the Azure cloud - leveraging DocumentDB's fully managed and scalable NoSQL databases - while continuing to use familiar skills and tools for MongoDB.</span></span>

## <a name="what-is-the-benefit-of-using-documentdb-api-for-mongodb"></a><span data-ttu-id="5baca-110">What is the benefit of using DocumentDB: API for MongoDB?</span><span class="sxs-lookup"><span data-stu-id="5baca-110">What is the benefit of using DocumentDB: API for MongoDB?</span></span>
<span data-ttu-id="5baca-111">**No Server Management** - DocumentDB is a fully managed service, which means you do not have to manage any infrastructure or Virtual Machines yourself.</span><span class="sxs-lookup"><span data-stu-id="5baca-111">**No Server Management** - DocumentDB is a fully managed service, which means you do not have to manage any infrastructure or Virtual Machines yourself.</span></span> <span data-ttu-id="5baca-112">DocumentDB is available in 30+ [Azure Regions](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="5baca-112">DocumentDB is available in 30+ [Azure Regions](https://azure.microsoft.com/regions/services/).</span></span>

<span data-ttu-id="5baca-113">**Limitless Scale** - You can scale throughput and storage independently and elastically.</span><span class="sxs-lookup"><span data-stu-id="5baca-113">**Limitless Scale** - You can scale throughput and storage independently and elastically.</span></span> <span data-ttu-id="5baca-114">You can add capacity to serve millions of requests per second with ease.</span><span class="sxs-lookup"><span data-stu-id="5baca-114">You can add capacity to serve millions of requests per second with ease.</span></span>

<span data-ttu-id="5baca-115">**Enterprise grade** - DocumentDB supports multiple local replicas to deliver 99.99% availability and data protection in the face of local and regional failures.</span><span class="sxs-lookup"><span data-stu-id="5baca-115">**Enterprise grade** - DocumentDB supports multiple local replicas to deliver 99.99% availability and data protection in the face of local and regional failures.</span></span> <span data-ttu-id="5baca-116">DocumentDB has enterprise grade [compliance certifications](https://www.microsoft.com/trustcenter) and security features.</span><span class="sxs-lookup"><span data-stu-id="5baca-116">DocumentDB has enterprise grade [compliance certifications](https://www.microsoft.com/trustcenter) and security features.</span></span> 

<span data-ttu-id="5baca-117">**MongoDB compatibility** - DocumentDB: API for MongoDB is designed for compatability with MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5baca-117">**MongoDB compatibility** - DocumentDB: API for MongoDB is designed for compatability with MongoDB.</span></span> <span data-ttu-id="5baca-118">You can use your existing code, applications, drivers, and tools to work with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="5baca-118">You can use your existing code, applications, drivers, and tools to work with DocumentDB.</span></span> 

<span data-ttu-id="5baca-119">Learn more in this Azure Friday video with Scott Hanselman and DocumentDB Principal Engineering Manager, Kirill Gavrylyuk.</span><span class="sxs-lookup"><span data-stu-id="5baca-119">Learn more in this Azure Friday video with Scott Hanselman and DocumentDB Principal Engineering Manager, Kirill Gavrylyuk.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/DocumentDB-Database-as-a-Service-for-MongoDB-Developers/player]
> 


## <a name="how-to-get-started"></a><span data-ttu-id="5baca-120">How to get started?</span><span class="sxs-lookup"><span data-stu-id="5baca-120">How to get started?</span></span>
<span data-ttu-id="5baca-121">Create a DocumentDB: API for MongoDB account in the [Azure Portal](https://portal.azure.com) and swap the connection to your new account.</span><span class="sxs-lookup"><span data-stu-id="5baca-121">Create a DocumentDB: API for MongoDB account in the [Azure Portal](https://portal.azure.com) and swap the connection to your new account.</span></span> 

<span data-ttu-id="5baca-122">*And, that's it!*</span><span class="sxs-lookup"><span data-stu-id="5baca-122">*And, that's it!*</span></span>

<span data-ttu-id="5baca-123">For more detailed instructions, follow [create account](documentdb-create-mongodb-account.md) and [connect to your account](documentdb-connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="5baca-123">For more detailed instructions, follow [create account](documentdb-create-mongodb-account.md) and [connect to your account](documentdb-connect-mongodb-account.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5baca-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="5baca-124">Next steps</span></span>

<span data-ttu-id="5baca-125">Information about DocumentDB: API for MongoDB is integrated into the overall DocumentDB documentation, but here are a few pointers to get you started:</span><span class="sxs-lookup"><span data-stu-id="5baca-125">Information about DocumentDB: API for MongoDB is integrated into the overall DocumentDB documentation, but here are a few pointers to get you started:</span></span>
* <span data-ttu-id="5baca-126">Follow the [Connect to a MongoDB account](documentdb-connect-mongodb-account.md) tutorial to learn how to get your account connection string information.</span><span class="sxs-lookup"><span data-stu-id="5baca-126">Follow the [Connect to a MongoDB account](documentdb-connect-mongodb-account.md) tutorial to learn how to get your account connection string information.</span></span>
* <span data-ttu-id="5baca-127">Follow the [Use MongoChef with DocumentDB](documentdb-mongodb-mongochef.md) tutorial to learn how to create a connection between your DocumentDB database and MongoDB app in MongoChef.</span><span class="sxs-lookup"><span data-stu-id="5baca-127">Follow the [Use MongoChef with DocumentDB](documentdb-mongodb-mongochef.md) tutorial to learn how to create a connection between your DocumentDB database and MongoDB app in MongoChef.</span></span>
* <span data-ttu-id="5baca-128">Follow the [Migrate data to DocumentDB with protocol support for MongoDB](documentdb-mongodb-migrate.md) tutorial to import your data to an API for MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="5baca-128">Follow the [Migrate data to DocumentDB with protocol support for MongoDB](documentdb-mongodb-migrate.md) tutorial to import your data to an API for MongoDB database.</span></span>
* <span data-ttu-id="5baca-129">Build your first API for MongoDB app using [Node.js](documentdb-mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5baca-129">Build your first API for MongoDB app using [Node.js](documentdb-mongodb-samples.md).</span></span>
* <span data-ttu-id="5baca-130">Build your first API for MongoDB web app using .[NET](documentdb-mongodb-application.md).</span><span class="sxs-lookup"><span data-stu-id="5baca-130">Build your first API for MongoDB web app using .[NET](documentdb-mongodb-application.md).</span></span>
* <span data-ttu-id="5baca-131">Connect to an API for MongoDB account using [Robomongo](documentdb-mongodb-robomongo.md).</span><span class="sxs-lookup"><span data-stu-id="5baca-131">Connect to an API for MongoDB account using [Robomongo](documentdb-mongodb-robomongo.md).</span></span>
* <span data-ttu-id="5baca-132">Learn how many RUs your operations are using with the [GetLastRequestStatistics command and the Azure portal metrics](documentdb-request-units.md#GetLastRequestStatistics).</span><span class="sxs-lookup"><span data-stu-id="5baca-132">Learn how many RUs your operations are using with the [GetLastRequestStatistics command and the Azure portal metrics](documentdb-request-units.md#GetLastRequestStatistics).</span></span>
* <span data-ttu-id="5baca-133">Learn how to [configure read preferences for globally distributed apps](documentdb-distribute-data-globally.md#ReadPreferencesAPIforMongoDB).</span><span class="sxs-lookup"><span data-stu-id="5baca-133">Learn how to [configure read preferences for globally distributed apps](documentdb-distribute-data-globally.md#ReadPreferencesAPIforMongoDB).</span></span>

