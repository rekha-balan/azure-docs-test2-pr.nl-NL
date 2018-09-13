---
title: Use MongoDB APIs to build a DocumentDB app | Microsoft Docs
description: A NoSQL tutorial that creates an online database using the DocumentDB APIs for MongoDB.
keywords: mongodb examples
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: anhoh
ms.openlocfilehash: 867ec5d0b27e790f3b00c94a4e5d14e4b2b17f73
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662130"
---
# <a name="build-a-documentdb-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="4b0af-104">Build a DocumentDB: API for MongoDB app using Node.js</span><span class="sxs-lookup"><span data-stu-id="4b0af-104">Build a DocumentDB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="4b0af-111">This example shows you how to build a DocumentDB: API for MongoDB console app using Node.js.</span><span class="sxs-lookup"><span data-stu-id="4b0af-111">This example shows you how to build a DocumentDB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="4b0af-112">To use this example, you must:</span><span class="sxs-lookup"><span data-stu-id="4b0af-112">To use this example, you must:</span></span>

* <span data-ttu-id="4b0af-113">[Create](documentdb-create-mongodb-account.md) an Azure DocumentDB: API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="4b0af-113">[Create](documentdb-create-mongodb-account.md) an Azure DocumentDB: API for MongoDB account.</span></span>
* <span data-ttu-id="4b0af-114">Retrieve your MongoDB [connection string](documentdb-connect-mongodb-account.md) information.</span><span class="sxs-lookup"><span data-stu-id="4b0af-114">Retrieve your MongoDB [connection string](documentdb-connect-mongodb-account.md) information.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="4b0af-115">Create the app</span><span class="sxs-lookup"><span data-stu-id="4b0af-115">Create the app</span></span>

1. <span data-ttu-id="4b0af-116">Create a *app.js* file and copy & paste the code below.</span><span class="sxs-lookup"><span data-stu-id="4b0af-116">Create a *app.js* file and copy & paste the code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10250/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into the families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="4b0af-117">Modify the following variables in the *app.js* file per your account settings (Learn how to find your [connection string](documentdb-connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="4b0af-117">Modify the following variables in the *app.js* file per your account settings (Learn how to find your [connection string](documentdb-connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10250/?ssl=true';
    ```
     
3. <span data-ttu-id="4b0af-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span><span class="sxs-lookup"><span data-stu-id="4b0af-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b0af-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b0af-119">Next steps</span></span>
* <span data-ttu-id="4b0af-120">Learn how to [use MongoChef](documentdb-mongodb-mongochef.md) with your DocumentDB: API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="4b0af-120">Learn how to [use MongoChef](documentdb-mongodb-mongochef.md) with your DocumentDB: API for MongoDB account.</span></span>
