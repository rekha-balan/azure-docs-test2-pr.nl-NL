---
title: Using the Mongoose framework with Azure Cosmos DB | Microsoft Docs
description: Learn how to connect a Node.js Mongoose app to Azure Cosmos DB
services: cosmos-db
author: slyons
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 01/08/2018
ms.author: sclyon
ms.openlocfilehash: aa178a24f0c36a1c5fb56b342141b066c150c7c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857120"
---
# <a name="azure-cosmos-db-using-the-mongoose-framework-with-azure-cosmos-db"></a><span data-ttu-id="d8dbb-103">Azure Cosmos DB: Using the Mongoose framework with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d8dbb-103">Azure Cosmos DB: Using the Mongoose framework with Azure Cosmos DB</span></span>

<span data-ttu-id="d8dbb-104">This tutorial demonstrates how to use the [Mongoose Framework](http://mongoosejs.com/) when storing data in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-104">This tutorial demonstrates how to use the [Mongoose Framework](http://mongoosejs.com/) when storing data in Azure Cosmos DB.</span></span> <span data-ttu-id="d8dbb-105">We use the MongoDB API for Azure Cosmos DB for this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-105">We use the MongoDB API for Azure Cosmos DB for this walkthrough.</span></span> <span data-ttu-id="d8dbb-106">For those of you unfamiliar, Mongoose is an object modeling framework for MongoDB in Node.js and provides a straight-forward, schema-based solution to model your application data.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-106">For those of you unfamiliar, Mongoose is an object modeling framework for MongoDB in Node.js and provides a straight-forward, schema-based solution to model your application data.</span></span>

<span data-ttu-id="d8dbb-107">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-107">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="d8dbb-108">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-108">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8dbb-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8dbb-109">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

<span data-ttu-id="d8dbb-110">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-110">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="d8dbb-111">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="d8dbb-111">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="d8dbb-112">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-112">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="d8dbb-113">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="d8dbb-113">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="d8dbb-114">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="d8dbb-114">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="set-up-your-nodejs-application"></a><span data-ttu-id="d8dbb-115">Set up your Node.js application</span><span class="sxs-lookup"><span data-stu-id="d8dbb-115">Set up your Node.js application</span></span>

>[!Note]
> <span data-ttu-id="d8dbb-116">If you'd like to just walkthrough the sample code instead of setup the application itself, clone the [sample](https://github.com/Azure-Samples/Mongoose_CosmosDB) used for this tutorial and build your Node.js Mongoose application on Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-116">If you'd like to just walkthrough the sample code instead of setup the application itself, clone the [sample](https://github.com/Azure-Samples/Mongoose_CosmosDB) used for this tutorial and build your Node.js Mongoose application on Azure Cosmos DB.</span></span>

1. <span data-ttu-id="d8dbb-117">To create a Node.js application in the folder of your choice, run the following command in a node command prompt.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-117">To create a Node.js application in the folder of your choice, run the following command in a node command prompt.</span></span>

    ```npm init```

    <span data-ttu-id="d8dbb-118">Answer the questions and your project will be ready to go.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-118">Answer the questions and your project will be ready to go.</span></span>

1. <span data-ttu-id="d8dbb-119">Add a new file to the folder and name it ```index.js```.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-119">Add a new file to the folder and name it ```index.js```.</span></span>
1. <span data-ttu-id="d8dbb-120">Install the necessary packages using one of the ```npm install``` options:</span><span class="sxs-lookup"><span data-stu-id="d8dbb-120">Install the necessary packages using one of the ```npm install``` options:</span></span>
    * <span data-ttu-id="d8dbb-121">Mongoose: ```npm install mongoose --save```</span><span class="sxs-lookup"><span data-stu-id="d8dbb-121">Mongoose: ```npm install mongoose --save```</span></span>
    * <span data-ttu-id="d8dbb-122">Dotenv (if you'd like to load your secrets from an .env file): ```npm install dotenv --save```</span><span class="sxs-lookup"><span data-stu-id="d8dbb-122">Dotenv (if you'd like to load your secrets from an .env file): ```npm install dotenv --save```</span></span>

    >[!Note]
    > <span data-ttu-id="d8dbb-123">The ```--save``` flag adds the dependency to the package.json file.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-123">The ```--save``` flag adds the dependency to the package.json file.</span></span>

1. <span data-ttu-id="d8dbb-124">Import the dependencies in your index.js file.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-124">Import the dependencies in your index.js file.</span></span>
    ```JavaScript
    var mongoose = require('mongoose');
    var env = require('dotenv').load();    //Use the .env file to load the variables
    ```

1. <span data-ttu-id="d8dbb-125">Add your Cosmos DB connection string and Cosmos DB Name to the ```.env``` file.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-125">Add your Cosmos DB connection string and Cosmos DB Name to the ```.env``` file.</span></span>

    ```JavaScript
    COSMOSDB_CONNSTR={Your MongoDB Connection String Here}
    COSMOSDB_DBNAME={Your DB Name Here}
    ```

1. <span data-ttu-id="d8dbb-126">Connect to Azure Cosmos DB using the Mongoose framework by adding the following code to the end of index.js.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-126">Connect to Azure Cosmos DB using the Mongoose framework by adding the following code to the end of index.js.</span></span>
    ```JavaScript
    mongoose.connect(process.env.COSMOSDB_CONNSTR+process.env.COSMOSDB_DBNAME+"?ssl=true&replicaSet=globaldb"); //Creates a new DB, if it doesn't already exist

    var db = mongoose.connection;
    db.on('error', console.error.bind(console, 'connection error:'));
    db.once('open', function() {
    console.log("Connected to DB");
    });
    ```
    >[!Note]
    > <span data-ttu-id="d8dbb-127">Here, the environment variables are loaded using process.env.{variableName} using the 'dotenv' npm package.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-127">Here, the environment variables are loaded using process.env.{variableName} using the 'dotenv' npm package.</span></span>

    <span data-ttu-id="d8dbb-128">Once you are connected to Azure Cosmos DB, you can now start setting up object models in Mongoose.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-128">Once you are connected to Azure Cosmos DB, you can now start setting up object models in Mongoose.</span></span>

## <a name="caveats-to-using-mongoose-with-azure-cosmos-db"></a><span data-ttu-id="d8dbb-129">Caveats to using Mongoose with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d8dbb-129">Caveats to using Mongoose with Azure Cosmos DB</span></span>

<span data-ttu-id="d8dbb-130">For every model you create, Mongoose creates a new MongoDB collection underneath the covers.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-130">For every model you create, Mongoose creates a new MongoDB collection underneath the covers.</span></span> <span data-ttu-id="d8dbb-131">However, given the per-collection billing model of Azure Cosmos DB, it might not be the most cost-efficient way to go, if you've got multiple object models that are sparsely populated.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-131">However, given the per-collection billing model of Azure Cosmos DB, it might not be the most cost-efficient way to go, if you've got multiple object models that are sparsely populated.</span></span>

<span data-ttu-id="d8dbb-132">This walkthrough covers both models.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-132">This walkthrough covers both models.</span></span> <span data-ttu-id="d8dbb-133">We'll first cover the walkthrough on storing one type of data per collection.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-133">We'll first cover the walkthrough on storing one type of data per collection.</span></span> <span data-ttu-id="d8dbb-134">This is the defacto behavior for Mongoose.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-134">This is the defacto behavior for Mongoose.</span></span>

<span data-ttu-id="d8dbb-135">Mongoose also has a concept called [Discriminators](http://mongoosejs.com/docs/discriminators.html).</span><span class="sxs-lookup"><span data-stu-id="d8dbb-135">Mongoose also has a concept called [Discriminators](http://mongoosejs.com/docs/discriminators.html).</span></span> <span data-ttu-id="d8dbb-136">Discriminators are a schema inheritance mechanism.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-136">Discriminators are a schema inheritance mechanism.</span></span> <span data-ttu-id="d8dbb-137">They enable you to have multiple models with overlapping schemas on top of the same underlying MongoDB collection.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-137">They enable you to have multiple models with overlapping schemas on top of the same underlying MongoDB collection.</span></span>

<span data-ttu-id="d8dbb-138">You can store the various data models in the same collection and then use a filter clause at query time to pull down only the data needed.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-138">You can store the various data models in the same collection and then use a filter clause at query time to pull down only the data needed.</span></span>

### <a name="one-collection-per-object-model"></a><span data-ttu-id="d8dbb-139">One collection per object model</span><span class="sxs-lookup"><span data-stu-id="d8dbb-139">One collection per object model</span></span>

<span data-ttu-id="d8dbb-140">The default Mongoose behavior is to create a MongoDB collection every time you create an Object model.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-140">The default Mongoose behavior is to create a MongoDB collection every time you create an Object model.</span></span> <span data-ttu-id="d8dbb-141">This section explores how to achieve this with MongoDB for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-141">This section explores how to achieve this with MongoDB for Azure Cosmos DB.</span></span> <span data-ttu-id="d8dbb-142">This method is recommended with Azure Cosmos DB when you have object models with large amounts of data.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-142">This method is recommended with Azure Cosmos DB when you have object models with large amounts of data.</span></span> <span data-ttu-id="d8dbb-143">This is the default operating model for Mongoose, so, you might be familiar with this, if you're familiar with Mongoose.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-143">This is the default operating model for Mongoose, so, you might be familiar with this, if you're familiar with Mongoose.</span></span>

1. <span data-ttu-id="d8dbb-144">Open your ```index.js``` again.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-144">Open your ```index.js``` again.</span></span>

1. <span data-ttu-id="d8dbb-145">Create the schema definition for 'Family'.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-145">Create the schema definition for 'Family'.</span></span>

    ```JavaScript
    const Family = mongoose.model('Family', new mongoose.Schema({
        lastName: String,
        parents: [{
            familyName: String,
            firstName: String,
            gender: String
        }],
        children: [{
            familyName: String,
            firstName: String,
            gender: String,
            grade: Number
        }],
        pets:[{
            givenName: String
        }],
        address: {
            country: String,
            state: String,
            city: String
        }
    }));
    ```

1. <span data-ttu-id="d8dbb-146">Create an object for 'Family'.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-146">Create an object for 'Family'.</span></span>

    ```JavaScript
    const family = new Family({
        lastName: "Volum",
        parents: [
            { firstName: "Thomas" },
            { firstName: "Mary Kay" }
        ],
        children: [
            { firstName: "Ryan", gender: "male", grade: 8 },
            { firstName: "Patrick", gender: "male", grade: 7 }
        ],
        pets: [
            { givenName: "Blackie" }
        ],
        address: { country: "USA", state: "WA", city: "Seattle" }
    });
    ```

1. <span data-ttu-id="d8dbb-147">Finally, let's save the object to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-147">Finally, let's save the object to Azure Cosmos DB.</span></span> <span data-ttu-id="d8dbb-148">This creates a collection underneath the covers.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-148">This creates a collection underneath the covers.</span></span>

    ```JavaScript
    family.save((err, saveFamily) => {
        console.log(JSON.stringify(saveFamily));
    });
    ```

1. <span data-ttu-id="d8dbb-149">Now, let's create another schema and object.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-149">Now, let's create another schema and object.</span></span> <span data-ttu-id="d8dbb-150">This time, let's create one for 'Vacation Destinations' that the families might be interested in.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-150">This time, let's create one for 'Vacation Destinations' that the families might be interested in.</span></span>
    1. <span data-ttu-id="d8dbb-151">Just like last time, let's create the scheme</span><span class="sxs-lookup"><span data-stu-id="d8dbb-151">Just like last time, let's create the scheme</span></span>
    ```JavaScript
    const VacationDestinations = mongoose.model('VacationDestinations', new mongoose.Schema({
        name: String,
        country: String
    }));
    ```

    1. <span data-ttu-id="d8dbb-152">Create a sample object (You can add multiple objects to this schema) and save it.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-152">Create a sample object (You can add multiple objects to this schema) and save it.</span></span>
    ```JavaScript
    const vacaySpot = new VacationDestinations({
        name: "Honolulu",
        country: "USA"
    });

    vacaySpot.save((err, saveVacay) => {
        console.log(JSON.stringify(saveVacay));
    });
    ```

1. <span data-ttu-id="d8dbb-153">Now, going into the Azure portal, you notice two collections created in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-153">Now, going into the Azure portal, you notice two collections created in Azure Cosmos DB.</span></span>

    ![Node.js tutorial - Screen shot of the Azure portal, showing an Azure Cosmos DB account, with multiple collection names highlighted - Node database][mutiple-coll]

1. <span data-ttu-id="d8dbb-155">Finally, let's read the data from Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-155">Finally, let's read the data from Azure Cosmos DB.</span></span> <span data-ttu-id="d8dbb-156">Since we're using the default Mongoose operating model, the reads are the same as any other reads with Mongoose.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-156">Since we're using the default Mongoose operating model, the reads are the same as any other reads with Mongoose.</span></span>

    ```JavaScript
    Family.find({ 'children.gender' : "male"}, function(err, foundFamily){
        foundFamily.forEach(fam => console.log("Found Family: " + JSON.stringify(fam)));
    });
    ```

### <a name="using-mongoose-discriminators-to-store-data-in-a-single-collection"></a><span data-ttu-id="d8dbb-157">Using Mongoose discriminators to store data in a single collection</span><span class="sxs-lookup"><span data-stu-id="d8dbb-157">Using Mongoose discriminators to store data in a single collection</span></span>

<span data-ttu-id="d8dbb-158">In this method, we use [Mongoose Discriminators](http://mongoosejs.com/docs/discriminators.html) to help optimize for the costs of each Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-158">In this method, we use [Mongoose Discriminators](http://mongoosejs.com/docs/discriminators.html) to help optimize for the costs of each Azure Cosmos DB collection.</span></span> <span data-ttu-id="d8dbb-159">Discriminators allow you to define a differentiating 'Key', which allows you to store, differentiate and filter on different object models.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-159">Discriminators allow you to define a differentiating 'Key', which allows you to store, differentiate and filter on different object models.</span></span>

<span data-ttu-id="d8dbb-160">Here, we create a base object model, define a differentiating key and add 'Family' and 'VacationDestinations' as an extension to the base model.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-160">Here, we create a base object model, define a differentiating key and add 'Family' and 'VacationDestinations' as an extension to the base model.</span></span>

1. <span data-ttu-id="d8dbb-161">Let's set up the base config and define the discriminator key.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-161">Let's set up the base config and define the discriminator key.</span></span>

    ```JavaScript
    const baseConfig = {
        discriminatorKey: "_type", //If you've got a lot of different data types, you could also consider setting up a secondary index here.
        collection: "alldata"   //Name of the Common Collection
    };
    ```

1. <span data-ttu-id="d8dbb-162">Next, let's define the common object model</span><span class="sxs-lookup"><span data-stu-id="d8dbb-162">Next, let's define the common object model</span></span>

    ```JavaScript
    const commonModel = mongoose.model('Common', new mongoose.Schema({}, baseConfig));
    ```

1. <span data-ttu-id="d8dbb-163">We now define the 'Family' model.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-163">We now define the 'Family' model.</span></span> <span data-ttu-id="d8dbb-164">Notice here that we're using ```commonModel.discriminator``` instead of ```mongoose.model```.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-164">Notice here that we're using ```commonModel.discriminator``` instead of ```mongoose.model```.</span></span> <span data-ttu-id="d8dbb-165">Additionally, we're also adding the base config to the mongoose schema.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-165">Additionally, we're also adding the base config to the mongoose schema.</span></span> <span data-ttu-id="d8dbb-166">So, here, the discriminatorKey is ```FamilyType```.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-166">So, here, the discriminatorKey is ```FamilyType```.</span></span>

    ```JavaScript
    const Family_common = commonModel.discriminator('FamilyType', new     mongoose.Schema({
        lastName: String,
        parents: [{
            familyName: String,
            firstName: String,
            gender: String
        }],
        children: [{
            familyName: String,
            firstName: String,
           gender: String,
            grade: Number
        }],
        pets:[{
            givenName: String
        }],
        address: {
            country: String,
            state: String,
            city: String
        }
    }, baseConfig));
    ```

1. <span data-ttu-id="d8dbb-167">Similarly, let's add another schema, this time for the 'VacationDestinations'.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-167">Similarly, let's add another schema, this time for the 'VacationDestinations'.</span></span> <span data-ttu-id="d8dbb-168">Here, the DiscriminatorKey is ```VacationDestinationsType```.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-168">Here, the DiscriminatorKey is ```VacationDestinationsType```.</span></span>

    ```JavaScript
    const Vacation_common = commonModel.discriminator('VacationDestinationsType', new mongoose.Schema({
        name: String,
        country: String
    }, baseConfig));
    ```

1. <span data-ttu-id="d8dbb-169">Finally, let's create objects for the model and save it.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-169">Finally, let's create objects for the model and save it.</span></span>
    1. <span data-ttu-id="d8dbb-170">Let's add object(s) to the 'Family' model.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-170">Let's add object(s) to the 'Family' model.</span></span>
    ```JavaScript
    const family_common = new Family_common({
        lastName: "Volum",
        parents: [
            { firstName: "Thomas" },
            { firstName: "Mary Kay" }
        ],
        children: [
            { firstName: "Ryan", gender: "male", grade: 8 },
            { firstName: "Patrick", gender: "male", grade: 7 }
        ],
        pets: [
            { givenName: "Blackie" }
        ],
        address: { country: "USA", state: "WA", city: "Seattle" }
    });

    family_common.save((err, saveFamily) => {
        console.log("Saved: " + JSON.stringify(saveFamily));
    });
    ```

    1. <span data-ttu-id="d8dbb-171">Next, let's add object(s) to the 'VacationDestinations' model and save it.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-171">Next, let's add object(s) to the 'VacationDestinations' model and save it.</span></span>
    ```JavaScript
    const vacay_common = new Vacation_common({
        name: "Honolulu",
        country: "USA"
    });

    vacay_common.save((err, saveVacay) => {
        console.log("Saved: " + JSON.stringify(saveVacay));
    });
    ```

1. <span data-ttu-id="d8dbb-172">Now, if you go back to the Azure portal, you notice that you have only one collection called ```alldata``` with both 'Family' and 'VacationDestinations' data.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-172">Now, if you go back to the Azure portal, you notice that you have only one collection called ```alldata``` with both 'Family' and 'VacationDestinations' data.</span></span>

    ![Node.js tutorial - Screen shot of the Azure portal, showing an Azure Cosmos DB account, with the collection name highlighted - Node database][alldata]

1. <span data-ttu-id="d8dbb-174">Also, notice that each object has another attribute called as ```__type```, which help you differentiate between the two different object models.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-174">Also, notice that each object has another attribute called as ```__type```, which help you differentiate between the two different object models.</span></span>

1. <span data-ttu-id="d8dbb-175">Finally, let's read the data that is stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-175">Finally, let's read the data that is stored in Azure Cosmos DB.</span></span> <span data-ttu-id="d8dbb-176">Mongoose takes care of filtering data based on the model.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-176">Mongoose takes care of filtering data based on the model.</span></span> <span data-ttu-id="d8dbb-177">So, you have to do nothing different when reading data.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-177">So, you have to do nothing different when reading data.</span></span> <span data-ttu-id="d8dbb-178">Just specify your model (in this case, ```Family_common```) and Mongoose handles filtering on the 'DiscriminatorKey'.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-178">Just specify your model (in this case, ```Family_common```) and Mongoose handles filtering on the 'DiscriminatorKey'.</span></span>

    ```JavaScript
    Family_common.find({ 'children.gender' : "male"}, function(err, foundFamily){
        foundFamily.forEach(fam => console.log("Found Family (using discriminator): " + JSON.stringify(fam)));
    });
    ```

<span data-ttu-id="d8dbb-179">As you can see, it is easy to work with Mongoose discriminators.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-179">As you can see, it is easy to work with Mongoose discriminators.</span></span> <span data-ttu-id="d8dbb-180">So, if you have an app that uses the Mongoose framework, this tutorial is a way for you to get your application up and running on the MongoDB API on Azure Cosmos DB without requiring too many changes.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-180">So, if you have an app that uses the Mongoose framework, this tutorial is a way for you to get your application up and running on the MongoDB API on Azure Cosmos DB without requiring too many changes.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d8dbb-181">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d8dbb-181">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="d8dbb-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8dbb-182">Next steps</span></span>

<span data-ttu-id="d8dbb-183">Learn more about the MongoDB operations, operators, stages, commands and options supported by the Azure Cosmos DB MongoDB API in [MongoDB API support for MongoDB features and syntax](mongodb-feature-support.md).</span><span class="sxs-lookup"><span data-stu-id="d8dbb-183">Learn more about the MongoDB operations, operators, stages, commands and options supported by the Azure Cosmos DB MongoDB API in [MongoDB API support for MongoDB features and syntax](mongodb-feature-support.md).</span></span>

[alldata]: ./media/mongodb-mongoose/mongo-collections-alldata.png
[mutiple-coll]: ./media/mongodb-mongoose/mongo-mutliple-collections.png
