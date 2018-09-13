---
title: Use MongoChef for MongoDB with Azure DocumentDB | Microsoft Docs
description: 'Learn how to use MongoChef with a DocumentDB: API for MongoDB account'
keywords: mongochef
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
ms.openlocfilehash: 08ecc06eade15561dd285ee76593d094a10c73ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563313"
---
# <a name="use-mongochef-with-a-documentdb-api-for-mongodb-account"></a><span data-ttu-id="ea7db-104">Use MongoChef with a DocumentDB: API for MongoDB account</span><span class="sxs-lookup"><span data-stu-id="ea7db-104">Use MongoChef with a DocumentDB: API for MongoDB account</span></span>

<span data-ttu-id="ea7db-105">To connect to an Azure DocumentDB: API for MongoDB account, you must:</span><span class="sxs-lookup"><span data-stu-id="ea7db-105">To connect to an Azure DocumentDB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="ea7db-106">Download and install [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="ea7db-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="ea7db-107">Have your DocumentDB: API for MongoDB account [connection string](documentdb-connect-mongodb-account.md) information</span><span class="sxs-lookup"><span data-stu-id="ea7db-107">Have your DocumentDB: API for MongoDB account [connection string](documentdb-connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="ea7db-108">Create the connection in MongoChef</span><span class="sxs-lookup"><span data-stu-id="ea7db-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="ea7db-109">To add your DocumentDB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="ea7db-109">To add your DocumentDB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="ea7db-110">Retrieve your DocumentDB: API for MongoDB connection information using the instructions [here](documentdb-connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="ea7db-110">Retrieve your DocumentDB: API for MongoDB connection information using the instructions [here](documentdb-connect-mongodb-account.md).</span></span>

    ![Screen shot of the connection string blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="ea7db-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span><span class="sxs-lookup"><span data-stu-id="ea7db-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Screen shot of the MongoChef connection manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="ea7db-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the DocumentDB: API for MongoDB account and the PORT.</span><span class="sxs-lookup"><span data-stu-id="ea7db-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the DocumentDB: API for MongoDB account and the PORT.</span></span>

    ![Screen shot of the MongoChef connection manager server tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="ea7db-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span><span class="sxs-lookup"><span data-stu-id="ea7db-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="ea7db-117">Accept the default authentication db (admin) or provide your own value.</span><span class="sxs-lookup"><span data-stu-id="ea7db-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Screen shot of the MongoChef connection manager authentication tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="ea7db-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span><span class="sxs-lookup"><span data-stu-id="ea7db-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Screen shot of the MongoChef connection manager SSL tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="ea7db-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Screen shot of the MongoChef test connection window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="ea7db-123">Use MongoChef to create a database, collection, and documents</span><span class="sxs-lookup"><span data-stu-id="ea7db-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="ea7db-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="ea7db-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="ea7db-125">In **Connection Manager**, highlight the connection and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Screen shot of the MongoChef connection manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="ea7db-127">Right click the host and choose **Add Database**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="ea7db-128">Provide a database name and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-128">Provide a database name and click **OK**.</span></span>

    ![Screen shot of the MongoChef Add Database option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="ea7db-130">Right click the database and choose **Add Collection**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="ea7db-131">Provide a collection name and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-131">Provide a collection name and click **Create**.</span></span>

    ![Screen shot of the MongoChef Add Collection option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="ea7db-133">Click the **Collection** menu item, then click **Add Document**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Screen shot of the MongoChef Add Document menu item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="ea7db-135">In the Add Document dialog, paste the following and then click **Add Document**.</span><span class="sxs-lookup"><span data-stu-id="ea7db-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="ea7db-136">Add another document, this time with the following content.</span><span class="sxs-lookup"><span data-stu-id="ea7db-136">Add another document, this time with the following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="ea7db-137">Execute a sample query.</span><span class="sxs-lookup"><span data-stu-id="ea7db-137">Execute a sample query.</span></span> <span data-ttu-id="ea7db-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span><span class="sxs-lookup"><span data-stu-id="ea7db-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Screen shot of Mongo Chef query results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="ea7db-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea7db-140">Next steps</span></span>
* <span data-ttu-id="ea7db-141">Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ea7db-141">Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).</span></span>











