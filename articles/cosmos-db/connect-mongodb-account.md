---
title: MongoDB connection string for an Azure Cosmos DB account | Microsoft Docs
description: Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.
keywords: mongodb connection string
services: cosmos-db
author: slyons
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: conceptual
ms.date: 12/19/2017
ms.author: sclyon
ms.openlocfilehash: ad8d6fe36c289c4c9e37689e1c7d755dc3bf9048
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966605"
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="dc00e-104">Connect a MongoDB application to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="dc00e-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="dc00e-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span><span class="sxs-lookup"><span data-stu-id="dc00e-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="dc00e-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span><span class="sxs-lookup"><span data-stu-id="dc00e-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="dc00e-107">This tutorial provides two ways to retrieve connection string information:</span><span class="sxs-lookup"><span data-stu-id="dc00e-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="dc00e-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span><span class="sxs-lookup"><span data-stu-id="dc00e-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="dc00e-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span><span class="sxs-lookup"><span data-stu-id="dc00e-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc00e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dc00e-110">Prerequisites</span></span>

- <span data-ttu-id="dc00e-111">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="dc00e-111">An Azure account.</span></span> <span data-ttu-id="dc00e-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span><span class="sxs-lookup"><span data-stu-id="dc00e-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="dc00e-113">An Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="dc00e-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="dc00e-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dc00e-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <a id="QuickstartConnection"></a><span data-ttu-id="dc00e-115">Get the MongoDB connection string by using the quick start</span><span class="sxs-lookup"><span data-stu-id="dc00e-115">Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="dc00e-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc00e-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc00e-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="dc00e-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="dc00e-118">In the left pane of the account blade, click **Quick start**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="dc00e-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="dc00e-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="dc00e-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span><span class="sxs-lookup"><span data-stu-id="dc00e-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="dc00e-121">Please comment below on what you'd like to see.</span><span class="sxs-lookup"><span data-stu-id="dc00e-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="dc00e-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="dc00e-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="dc00e-123">Copy and paste the code snippet into your MongoDB app.</span><span class="sxs-lookup"><span data-stu-id="dc00e-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Quick start blade](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a> <span data-ttu-id="dc00e-125">Get the MongoDB connection string to customize</span><span class="sxs-lookup"><span data-stu-id="dc00e-125">Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="dc00e-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc00e-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc00e-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="dc00e-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="dc00e-128">In the left pane of the account blade, click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="dc00e-129">The **Connection String** blade opens.</span><span class="sxs-lookup"><span data-stu-id="dc00e-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="dc00e-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span><span class="sxs-lookup"><span data-stu-id="dc00e-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Connection String blade](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="dc00e-132">Connection string requirements</span><span class="sxs-lookup"><span data-stu-id="dc00e-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="dc00e-133">Azure Cosmos DB has strict security requirements and standards.</span><span class="sxs-lookup"><span data-stu-id="dc00e-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="dc00e-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span><span class="sxs-lookup"><span data-stu-id="dc00e-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="dc00e-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span><span class="sxs-lookup"><span data-stu-id="dc00e-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="dc00e-136">So, the connection string format is:</span><span class="sxs-lookup"><span data-stu-id="dc00e-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="dc00e-137">The values of this string are available in the **Connection String** blade shown earlier:</span><span class="sxs-lookup"><span data-stu-id="dc00e-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="dc00e-138">Username (required): Azure Cosmos DB account name.</span><span class="sxs-lookup"><span data-stu-id="dc00e-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="dc00e-139">Password (required): Azure Cosmos DB account password.</span><span class="sxs-lookup"><span data-stu-id="dc00e-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="dc00e-140">Host (required): FQDN of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="dc00e-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="dc00e-141">Port (required): 10255.</span><span class="sxs-lookup"><span data-stu-id="dc00e-141">Port (required): 10255.</span></span>
* <span data-ttu-id="dc00e-142">Database (optional): The database that the connection uses.</span><span class="sxs-lookup"><span data-stu-id="dc00e-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="dc00e-143">If no database is provided, the default database is "test."</span><span class="sxs-lookup"><span data-stu-id="dc00e-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="dc00e-144">ssl=true (required)</span><span class="sxs-lookup"><span data-stu-id="dc00e-144">ssl=true (required)</span></span>

<span data-ttu-id="dc00e-145">For example, consider the account shown in the **Connection String** blade.</span><span class="sxs-lookup"><span data-stu-id="dc00e-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="dc00e-146">A valid connection string is:</span><span class="sxs-lookup"><span data-stu-id="dc00e-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@contoso123.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="dc00e-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc00e-147">Next steps</span></span>
* <span data-ttu-id="dc00e-148">Learn how to [use Studio 3T (MongoChef)](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="dc00e-148">Learn how to [use Studio 3T (MongoChef)](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="dc00e-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc00e-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
