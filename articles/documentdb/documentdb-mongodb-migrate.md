---
title: Use mongoimport & mongorestore with Azure DocumentDB | Microsoft Docs
description: 'Learn how to use mongoimport and mongorestore to import data to a DocumentDB: API for MongoDB account'
keywords: mongoimport, mongorestore
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: anhoh
ms.openlocfilehash: bc73c7850e340372164ac168f4e57c02da1ed1c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553660"
---
# <a name="migrate-data-to-documentdb-by-using-mongoimport-and-mongorestore"></a><span data-ttu-id="8a63c-104">Migrate data to DocumentDB by using mongoimport and mongorestore</span><span class="sxs-lookup"><span data-stu-id="8a63c-104">Migrate data to DocumentDB by using mongoimport and mongorestore</span></span>
> [!div class="op_single_selector"]
> * [Import to DocumentDB](documentdb-import-data.md)
> * [Import to API for MongoDB](documentdb-mongodb-migrate.md)
>
>

<span data-ttu-id="8a63c-107">To migrate data to an Azure DocumentDB: API for MongoDB account, you must:</span><span class="sxs-lookup"><span data-stu-id="8a63c-107">To migrate data to an Azure DocumentDB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="8a63c-108">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="8a63c-108">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="8a63c-109">Get your [DocumentDB support for MongoDB connection string](documentdb-connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="8a63c-109">Get your [DocumentDB support for MongoDB connection string](documentdb-connect-mongodb-account.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a63c-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="8a63c-110">Before you begin</span></span>

* <span data-ttu-id="8a63c-111">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span><span class="sxs-lookup"><span data-stu-id="8a63c-111">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="8a63c-112">Be sure to increase the throughput for larger data migrations.</span><span class="sxs-lookup"><span data-stu-id="8a63c-112">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="8a63c-113">After you've completed the migration, decrease the throughput to save costs.</span><span class="sxs-lookup"><span data-stu-id="8a63c-113">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="8a63c-114">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in DocumentDB](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8a63c-114">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in DocumentDB](documentdb-performance-levels.md).</span></span>

* <span data-ttu-id="8a63c-115">Enable SSL: DocumentDB has strict security requirements and standards.</span><span class="sxs-lookup"><span data-stu-id="8a63c-115">Enable SSL: DocumentDB has strict security requirements and standards.</span></span> <span data-ttu-id="8a63c-116">Be sure to enable SSL when you interact with your account.</span><span class="sxs-lookup"><span data-stu-id="8a63c-116">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="8a63c-117">The procedures in the rest of the article include how to enable SSL for *mongoimport* and *mongorestore*.</span><span class="sxs-lookup"><span data-stu-id="8a63c-117">The procedures in the rest of the article include how to enable SSL for *mongoimport* and *mongorestore*.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="8a63c-118">Find your connection string information (host, port, username, and password)</span><span class="sxs-lookup"><span data-stu-id="8a63c-118">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="8a63c-119">In the [Azure portal](https://portal.azure.com), in the left pane, click the **NoSQL (DocumentDB)** entry.</span><span class="sxs-lookup"><span data-stu-id="8a63c-119">In the [Azure portal](https://portal.azure.com), in the left pane, click the **NoSQL (DocumentDB)** entry.</span></span>
2. <span data-ttu-id="8a63c-120">In the **Subscriptions** pane, select your account name.</span><span class="sxs-lookup"><span data-stu-id="8a63c-120">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="8a63c-121">In the **Connection String** blade, click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="8a63c-121">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="8a63c-122">The right pane contains all the information you need to successfully connect to your account.</span><span class="sxs-lookup"><span data-stu-id="8a63c-122">The right pane contains all the information you need to successfully connect to your account.</span></span>

    ![The "Connection String" blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-api-for-mongodb-with-mongoimport"></a><span data-ttu-id="8a63c-124">Import data to API for MongoDB with mongoimport</span><span class="sxs-lookup"><span data-stu-id="8a63c-124">Import data to API for MongoDB with mongoimport</span></span>

<span data-ttu-id="8a63c-125">To import data to your DocumentDB account, use the following template to execute the import.</span><span class="sxs-lookup"><span data-stu-id="8a63c-125">To import data to your DocumentDB account, use the following template to execute the import.</span></span> <span data-ttu-id="8a63c-126">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span><span class="sxs-lookup"><span data-stu-id="8a63c-126">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="8a63c-127">Template:</span><span class="sxs-lookup"><span data-stu-id="8a63c-127">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10250 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="8a63c-128">Example:</span><span class="sxs-lookup"><span data-stu-id="8a63c-128">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10250 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-api-for-mongodb-with-mongorestore"></a><span data-ttu-id="8a63c-129">Import data to API for MongoDB with mongorestore</span><span class="sxs-lookup"><span data-stu-id="8a63c-129">Import data to API for MongoDB with mongorestore</span></span>

<span data-ttu-id="8a63c-130">To restore data to your DocumentDB account, use the following template to execute the import.</span><span class="sxs-lookup"><span data-stu-id="8a63c-130">To restore data to your DocumentDB account, use the following template to execute the import.</span></span> <span data-ttu-id="8a63c-131">Fill in *host*, *username*, and *password* with the values specific to your account.</span><span class="sxs-lookup"><span data-stu-id="8a63c-131">Fill in *host*, *username*, and *password* with the values specific to your account.</span></span>

<span data-ttu-id="8a63c-132">Template:</span><span class="sxs-lookup"><span data-stu-id="8a63c-132">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10250 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="8a63c-133">Example:</span><span class="sxs-lookup"><span data-stu-id="8a63c-133">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10250 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07

## <a name="next-steps"></a><span data-ttu-id="8a63c-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a63c-134">Next steps</span></span>
* <span data-ttu-id="8a63c-135">For more information, explore [DocumentDB: API for MongoDB samples](documentdb-mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8a63c-135">For more information, explore [DocumentDB: API for MongoDB samples](documentdb-mongodb-samples.md).</span></span>

