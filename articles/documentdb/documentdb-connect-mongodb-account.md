---
title: MongoDB connection string for DocumentDB account | Microsoft Docs
description: Learn how to connect your MongoDB app to an Azure DocumentDB account using a MongoDB connection string.
keywords: mongodb connection string
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: anhoh
ms.openlocfilehash: 372d328eb6c5d370faf486b78873173c6b3b90b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553482"
---
# <a name="connect-an-application-to-documentdb-api-for-mongodb"></a><span data-ttu-id="9b39c-104">Connect an application to DocumentDB: API for MongoDB</span><span class="sxs-lookup"><span data-stu-id="9b39c-104">Connect an application to DocumentDB: API for MongoDB</span></span>
<span data-ttu-id="9b39c-105">Learn how to connect your MongoDB app to an Azure DocumentDB account using a MongoDB connection string.</span><span class="sxs-lookup"><span data-stu-id="9b39c-105">Learn how to connect your MongoDB app to an Azure DocumentDB account using a MongoDB connection string.</span></span> <span data-ttu-id="9b39c-106">By connecting your MongoDB app to an Azure DocumentDB database, you can use a DocumentDB database as the data store for your MongoDB app.</span><span class="sxs-lookup"><span data-stu-id="9b39c-106">By connecting your MongoDB app to an Azure DocumentDB database, you can use a DocumentDB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="9b39c-107">This tutorial provides two ways to retrieve connection string information:</span><span class="sxs-lookup"><span data-stu-id="9b39c-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="9b39c-108">[The Quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers.</span><span class="sxs-lookup"><span data-stu-id="9b39c-108">[The Quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers.</span></span>
- <span data-ttu-id="9b39c-109">[The custom connection string method](#GetCustomConnection), for use with other drivers.</span><span class="sxs-lookup"><span data-stu-id="9b39c-109">[The custom connection string method](#GetCustomConnection), for use with other drivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b39c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9b39c-110">Prerequisites</span></span>

- <span data-ttu-id="9b39c-111">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="9b39c-111">An Azure account.</span></span> <span data-ttu-id="9b39c-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span><span class="sxs-lookup"><span data-stu-id="9b39c-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="9b39c-113">A DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="9b39c-113">A DocumentDB account.</span></span> <span data-ttu-id="9b39c-114">For instructions, see [Create a DocumentDB account for use with MongoDB apps](documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="9b39c-114">For instructions, see [Create a DocumentDB account for use with MongoDB apps](documentdb-create-mongodb-account.md).</span></span>

## <a id="QuickstartConnection"></a><span data-ttu-id="9b39c-115">Get the MongoDB connection string using the Quick start</span><span class="sxs-lookup"><span data-stu-id="9b39c-115">Get the MongoDB connection string using the Quick start</span></span>
1. <span data-ttu-id="9b39c-116">In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b39c-116">In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b39c-117">In the **NoSQL (DocumentDB)** blade, select the DocumentDB: API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="9b39c-117">In the **NoSQL (DocumentDB)** blade, select the DocumentDB: API for MongoDB account.</span></span> 
3. <span data-ttu-id="9b39c-118">In the **Left Navigation** bar of the account blade, click **Quick start**.</span><span class="sxs-lookup"><span data-stu-id="9b39c-118">In the **Left Navigation** bar of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="9b39c-119">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span><span class="sxs-lookup"><span data-stu-id="9b39c-119">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="9b39c-120">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span><span class="sxs-lookup"><span data-stu-id="9b39c-120">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> <span data-ttu-id="9b39c-121">Please comment below on what you'd like to see and read [Get the account's connection string information](#GetCustomConnection) to learn how to craft your own connection.</span><span class="sxs-lookup"><span data-stu-id="9b39c-121">Please comment below on what you'd like to see and read [Get the account's connection string information](#GetCustomConnection) to learn how to craft your own connection.</span></span>
5. <span data-ttu-id="9b39c-122">Copy and paste the code snippet into your MongoDB app, and you are ready to go.</span><span class="sxs-lookup"><span data-stu-id="9b39c-122">Copy and paste the code snippet into your MongoDB app, and you are ready to go.</span></span>

    ![Screen shot of the quick start blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a> <span data-ttu-id="9b39c-124">Get the MongoDB connection string to customize</span><span class="sxs-lookup"><span data-stu-id="9b39c-124">Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="9b39c-125">In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b39c-125">In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b39c-126">In the **NoSQL (DocumentDB)** blade, select the DocumentDB: API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="9b39c-126">In the **NoSQL (DocumentDB)** blade, select the DocumentDB: API for MongoDB account.</span></span> 
3. <span data-ttu-id="9b39c-127">In the **Left Navigation** bar of the account blade, click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="9b39c-127">In the **Left Navigation** bar of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="9b39c-128">The **Connection String Information** blade opens and has all the information necessary to connect to the account using a driver for MongoDB, including a pre-constructed connection string.</span><span class="sxs-lookup"><span data-stu-id="9b39c-128">The **Connection String Information** blade opens and has all the information necessary to connect to the account using a driver for MongoDB, including a pre-constructed connection string.</span></span>

    ![Screen shot of the connection string blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="9b39c-130">Connection string requirements</span><span class="sxs-lookup"><span data-stu-id="9b39c-130">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="9b39c-131">DocumentDB has strict security requirements and standards.</span><span class="sxs-lookup"><span data-stu-id="9b39c-131">DocumentDB has strict security requirements and standards.</span></span> <span data-ttu-id="9b39c-132">DocumentDB accounts require authentication and secure communication via **SSL**.</span><span class="sxs-lookup"><span data-stu-id="9b39c-132">DocumentDB accounts require authentication and secure communication via **SSL**.</span></span>
>
>

<span data-ttu-id="9b39c-133">It is important to note that DocumentDB supports the standard MongoDB connection string URI format, with a couple of specific requirements: DocumentDB accounts require authentication and secure communication via SSL.</span><span class="sxs-lookup"><span data-stu-id="9b39c-133">It is important to note that DocumentDB supports the standard MongoDB connection string URI format, with a couple of specific requirements: DocumentDB accounts require authentication and secure communication via SSL.</span></span>  <span data-ttu-id="9b39c-134">Thus, the connection string format is:</span><span class="sxs-lookup"><span data-stu-id="9b39c-134">Thus, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="9b39c-135">Where the values of this string are available in the Connection String blade shown above.</span><span class="sxs-lookup"><span data-stu-id="9b39c-135">Where the values of this string are available in the Connection String blade shown above.</span></span>

* <span data-ttu-id="9b39c-136">Username (required)</span><span class="sxs-lookup"><span data-stu-id="9b39c-136">Username (required)</span></span>
  * <span data-ttu-id="9b39c-137">DocumentDB account name</span><span class="sxs-lookup"><span data-stu-id="9b39c-137">DocumentDB account name</span></span>
* <span data-ttu-id="9b39c-138">Password (required)</span><span class="sxs-lookup"><span data-stu-id="9b39c-138">Password (required)</span></span>
  * <span data-ttu-id="9b39c-139">DocumentDB account password</span><span class="sxs-lookup"><span data-stu-id="9b39c-139">DocumentDB account password</span></span>
* <span data-ttu-id="9b39c-140">Host (required)</span><span class="sxs-lookup"><span data-stu-id="9b39c-140">Host (required)</span></span>
  * <span data-ttu-id="9b39c-141">FQDN of DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="9b39c-141">FQDN of DocumentDB account</span></span>
* <span data-ttu-id="9b39c-142">Port (required)</span><span class="sxs-lookup"><span data-stu-id="9b39c-142">Port (required)</span></span>
  * <span data-ttu-id="9b39c-143">10250</span><span class="sxs-lookup"><span data-stu-id="9b39c-143">10250</span></span>
* <span data-ttu-id="9b39c-144">Database (optional)</span><span class="sxs-lookup"><span data-stu-id="9b39c-144">Database (optional)</span></span>
  * <span data-ttu-id="9b39c-145">The default database used by the connection (if no database is provided, the default database is "test")</span><span class="sxs-lookup"><span data-stu-id="9b39c-145">The default database used by the connection (if no database is provided, the default database is "test")</span></span>
* <span data-ttu-id="9b39c-146">ssl=true (required)</span><span class="sxs-lookup"><span data-stu-id="9b39c-146">ssl=true (required)</span></span>

<span data-ttu-id="9b39c-147">For example, consider the account shown in the Connection String Information above.</span><span class="sxs-lookup"><span data-stu-id="9b39c-147">For example, consider the account shown in the Connection String Information above.</span></span>  <span data-ttu-id="9b39c-148">A valid connection string is:</span><span class="sxs-lookup"><span data-stu-id="9b39c-148">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10250/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="9b39c-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b39c-149">Next steps</span></span>
* <span data-ttu-id="9b39c-150">Learn how to [use MongoChef](documentdb-mongodb-mongochef.md) with a DocumentDB: API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="9b39c-150">Learn how to [use MongoChef](documentdb-mongodb-mongochef.md) with a DocumentDB: API for MongoDB account.</span></span>
* <span data-ttu-id="9b39c-151">Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9b39c-151">Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).</span></span>


