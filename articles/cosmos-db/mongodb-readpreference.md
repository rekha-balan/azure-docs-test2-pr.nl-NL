---
title: Using MongoDB Read Preference with the Azure Cosmos DB MongoDB API  | Microsoft Docs
description: Learn how to use MongoDB Read Preference with the Azure Cosmos DB MongoDB API
services: cosmos-db
author: vidhoonv
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: ''
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 02/26/2018
ms.author: sclyon
ms.openlocfilehash: 90c8d73e32f4c99c6871ce9cdb7839cd1d380b9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969002"
---
# <a name="how-to-globally-distribute-reads-using-read-preference-with-the-azure-cosmos-db-mongodb-api"></a><span data-ttu-id="8d4cf-103">How to globally distribute reads using Read Preference with the Azure Cosmos DB MongoDB API</span><span class="sxs-lookup"><span data-stu-id="8d4cf-103">How to globally distribute reads using Read Preference with the Azure Cosmos DB MongoDB API</span></span> 

<span data-ttu-id="8d4cf-104">This article shows how to globally distribute read operations using [MongoDB Read Preference](https://docs.mongodb.com/manual/core/read-preference/) settings with Azure Cosmos DB's MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-104">This article shows how to globally distribute read operations using [MongoDB Read Preference](https://docs.mongodb.com/manual/core/read-preference/) settings with Azure Cosmos DB's MongoDB API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8d4cf-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d4cf-105">Prerequisites</span></span> 
<span data-ttu-id="8d4cf-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 
[!INCLUDE [cosmos-db-emulator-mongodb](../../includes/cosmos-db-emulator-mongodb.md)]

<span data-ttu-id="8d4cf-107">Refer to this [Quickstart](tutorial-global-distribution-mongodb.md) article for instructions on using the Azure portal to set up Azure Cosmos DB account with global distribution and then connect using MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-107">Refer to this [Quickstart](tutorial-global-distribution-mongodb.md) article for instructions on using the Azure portal to set up Azure Cosmos DB account with global distribution and then connect using MongoDB API.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="8d4cf-108">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-108">Clone the sample application</span></span>

<span data-ttu-id="8d4cf-109">Open a git terminal window, such as git bash, and `cd` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-109">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

<span data-ttu-id="8d4cf-110">Run the following commands to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-110">Run the following commands to clone the sample repository.</span></span> <span data-ttu-id="8d4cf-111">Based on your platform of interest, use one of the following sample repositories:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-111">Based on your platform of interest, use one of the following sample repositories:</span></span>

1. [<span data-ttu-id="8d4cf-112">.NET sample application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-112">.NET sample application</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-geo-readpreference)
2. [<span data-ttu-id="8d4cf-113">NodeJS sample application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-113">NodeJS sample application</span></span>]( https://github.com/Azure-Samples/azure-cosmos-db-mongodb-node-geo-readpreference)
3. [<span data-ttu-id="8d4cf-114">Mongoose sample application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-114">Mongoose sample application</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-mongoose-geo-readpreference)
4. [<span data-ttu-id="8d4cf-115">Java sample application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-115">Java sample application</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-geo-readpreference)
5. [<span data-ttu-id="8d4cf-116">SpringBoot sample application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-116">SpringBoot sample application</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-spring)


```bash
git clone <sample repo url>
```

## <a name="run-the-application"></a><span data-ttu-id="8d4cf-117">Run the application</span><span class="sxs-lookup"><span data-stu-id="8d4cf-117">Run the application</span></span>

<span data-ttu-id="8d4cf-118">Depending on the platform used, install the required packages and start the application.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-118">Depending on the platform used, install the required packages and start the application.</span></span> <span data-ttu-id="8d4cf-119">To install dependencies, follow the README included in the sample application repository.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-119">To install dependencies, follow the README included in the sample application repository.</span></span> <span data-ttu-id="8d4cf-120">For instance, in the NodeJS sample application, use the following commands to install the required packages and start the application.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-120">For instance, in the NodeJS sample application, use the following commands to install the required packages and start the application.</span></span>

```bash
cd mean
npm install
node index.js
```
<span data-ttu-id="8d4cf-121">The application tries to connect to a MongoDB source and fails because the connection string is invalid.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-121">The application tries to connect to a MongoDB source and fails because the connection string is invalid.</span></span> <span data-ttu-id="8d4cf-122">Follow the steps in the README to update the connection string `url`.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-122">Follow the steps in the README to update the connection string `url`.</span></span> <span data-ttu-id="8d4cf-123">Also, update the `readFromRegion` to a read region in your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-123">Also, update the `readFromRegion` to a read region in your Azure Cosmos DB account.</span></span> <span data-ttu-id="8d4cf-124">The following instructions are from the NodeJS sample:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-124">The following instructions are from the NodeJS sample:</span></span>

```
* Next, substitute the `url`, `readFromRegion` in App.Config with your Cosmos DB account's values. 
```

<span data-ttu-id="8d4cf-125">After following these steps, the sample application runs and produces the following output:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-125">After following these steps, the sample application runs and produces the following output:</span></span>

```
connected!
readDefaultfunc query completed!
readFromNearestfunc query completed!
readFromRegionfunc query completed!
readDefaultfunc query completed!
readFromNearestfunc query completed!
readFromRegionfunc query completed!
readDefaultfunc query completed!
readFromSecondaryfunc query completed!
```

## <a name="read-using-read-preference-mode"></a><span data-ttu-id="8d4cf-126">Read using Read Preference mode</span><span class="sxs-lookup"><span data-stu-id="8d4cf-126">Read using Read Preference mode</span></span>

<span data-ttu-id="8d4cf-127">MongoDB provides the following Read Preference modes for clients to use:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-127">MongoDB provides the following Read Preference modes for clients to use:</span></span>

1. <span data-ttu-id="8d4cf-128">PRIMARY</span><span class="sxs-lookup"><span data-stu-id="8d4cf-128">PRIMARY</span></span>
2. <span data-ttu-id="8d4cf-129">PRIMARY_PREFERRED</span><span class="sxs-lookup"><span data-stu-id="8d4cf-129">PRIMARY_PREFERRED</span></span>
3. <span data-ttu-id="8d4cf-130">SECONDARY</span><span class="sxs-lookup"><span data-stu-id="8d4cf-130">SECONDARY</span></span>
4. <span data-ttu-id="8d4cf-131">SECONDARY_PREFERRED</span><span class="sxs-lookup"><span data-stu-id="8d4cf-131">SECONDARY_PREFERRED</span></span>
5. <span data-ttu-id="8d4cf-132">NEAREST</span><span class="sxs-lookup"><span data-stu-id="8d4cf-132">NEAREST</span></span>

<span data-ttu-id="8d4cf-133">Refer to the detailed [MongoDB Read Preference behavior](https://docs.mongodb.com/manual/core/read-preference-mechanics/#replica-set-read-preference-behavior) documentation for details on the behavior of each of these read preference modes.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-133">Refer to the detailed [MongoDB Read Preference behavior](https://docs.mongodb.com/manual/core/read-preference-mechanics/#replica-set-read-preference-behavior) documentation for details on the behavior of each of these read preference modes.</span></span> <span data-ttu-id="8d4cf-134">In Azure Cosmos DB, primary maps to WRITE region and secondary maps to READ region.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-134">In Azure Cosmos DB, primary maps to WRITE region and secondary maps to READ region.</span></span>

<span data-ttu-id="8d4cf-135">Based on common scenarios, we recommend using the following settings:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-135">Based on common scenarios, we recommend using the following settings:</span></span>

1. <span data-ttu-id="8d4cf-136">If **low latency reads** are required, use the **NEAREST** read preference mode.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-136">If **low latency reads** are required, use the **NEAREST** read preference mode.</span></span> <span data-ttu-id="8d4cf-137">This setting directs the read operations to the nearest available region.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-137">This setting directs the read operations to the nearest available region.</span></span> <span data-ttu-id="8d4cf-138">Note that if the nearest region is the WRITE region, then these operations are directed to that region.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-138">Note that if the nearest region is the WRITE region, then these operations are directed to that region.</span></span>
2. <span data-ttu-id="8d4cf-139">If **high availability and geo distribution of reads** are required (latency is not a constraint), then use the **SECONDARY PREFERRED** read preference mode.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-139">If **high availability and geo distribution of reads** are required (latency is not a constraint), then use the **SECONDARY PREFERRED** read preference mode.</span></span> <span data-ttu-id="8d4cf-140">This setting directs read operations to an available READ region.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-140">This setting directs read operations to an available READ region.</span></span> <span data-ttu-id="8d4cf-141">If no READ region is available, then requests are directed to the WRITE region.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-141">If no READ region is available, then requests are directed to the WRITE region.</span></span>

<span data-ttu-id="8d4cf-142">The following snippet from the sample application shows how to configure NEAREST Read Preference in NodeJS:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-142">The following snippet from the sample application shows how to configure NEAREST Read Preference in NodeJS:</span></span>

```javascript
  var query = {};
  var readcoll = client.db('regionDB').collection('regionTest', {readPreference: ReadPreference.NEAREST});
  readcoll.find(query).toArray(function(err, data) {
    assert.equal(null, err);
    console.log("readFromNearestfunc query completed!");
  });
```

<span data-ttu-id="8d4cf-143">Similarly, the snippet below shows how to configure the SECONDARY_PREFERRED Read Preference in NodeJS:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-143">Similarly, the snippet below shows how to configure the SECONDARY_PREFERRED Read Preference in NodeJS:</span></span>

```javascript
  var query = {};
  var readcoll = client.db('regionDB').collection('regionTest', {readPreference: ReadPreference.SECONDARY_PREFERRED});
  readcoll.find(query).toArray(function(err, data) {
    assert.equal(null, err);
    console.log("readFromSecondaryPreferredfunc query completed!");
  });
```

<span data-ttu-id="8d4cf-144">Refer to the corresponding sample application repos for other platforms, such as [.NET](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-geo-readpreference) and [Java](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-geo-readpreference).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-144">Refer to the corresponding sample application repos for other platforms, such as [.NET](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-geo-readpreference) and [Java](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-geo-readpreference).</span></span>

## <a name="read-using-tags"></a><span data-ttu-id="8d4cf-145">Read using tags</span><span class="sxs-lookup"><span data-stu-id="8d4cf-145">Read using tags</span></span>

<span data-ttu-id="8d4cf-146">In addition to the Read Preference mode, MongoDB allows use of tags to direct read operations.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-146">In addition to the Read Preference mode, MongoDB allows use of tags to direct read operations.</span></span> <span data-ttu-id="8d4cf-147">In Azure Cosmos DB for MongoDB API, the `region` tag is included by default as a part of the `isMaster` response:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-147">In Azure Cosmos DB for MongoDB API, the `region` tag is included by default as a part of the `isMaster` response:</span></span>

```json
"tags": {
         "region": "West US"
      }
```

<span data-ttu-id="8d4cf-148">Hence, MongoClient can use the `region` tag along with the region name to direct read operations to specific regions.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-148">Hence, MongoClient can use the `region` tag along with the region name to direct read operations to specific regions.</span></span> <span data-ttu-id="8d4cf-149">For Azure Cosmos DB accounts, region names can be found in Azure portal on the left under **Settings->Replica data globally**.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-149">For Azure Cosmos DB accounts, region names can be found in Azure portal on the left under **Settings->Replica data globally**.</span></span> <span data-ttu-id="8d4cf-150">This setting is useful for achieving **read isolation** - cases in which client application want to direct read operations to a specific region only.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-150">This setting is useful for achieving **read isolation** - cases in which client application want to direct read operations to a specific region only.</span></span> <span data-ttu-id="8d4cf-151">This setting is ideal for non-production/analytics type scenarios, which run in the background and are not production critical services.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-151">This setting is ideal for non-production/analytics type scenarios, which run in the background and are not production critical services.</span></span>

<span data-ttu-id="8d4cf-152">The following snippet from the sample application shows how to configure the Read Preference with tags in NodeJS:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-152">The following snippet from the sample application shows how to configure the Read Preference with tags in NodeJS:</span></span>

```javascript
 var query = {};
  var readcoll = client.db('regionDB').collection('regionTest',{readPreference: new ReadPreference(ReadPreference.SECONDARY_PREFERRED, {"region": "West US"})});
  readcoll.find(query).toArray(function(err, data) {
    assert.equal(null, err);
    console.log("readFromRegionfunc query completed!");
  });
```

<span data-ttu-id="8d4cf-153">Refer to the corresponding sample application repos for other platforms, such as [.NET](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-geo-readpreference) and [Java](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-geo-readpreference).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-153">Refer to the corresponding sample application repos for other platforms, such as [.NET](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-geo-readpreference) and [Java](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-geo-readpreference).</span></span>

<span data-ttu-id="8d4cf-154">In this article, you've learned how to globally distribute read operations using Read Preference with Azure Cosmos DB's MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-154">In this article, you've learned how to globally distribute read operations using Read Preference with Azure Cosmos DB's MongoDB API.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="8d4cf-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8d4cf-155">Clean up resources</span></span>

<span data-ttu-id="8d4cf-156">If you're not going to continue to use this app, delete all resources created by this article in the Azure portal with the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-156">If you're not going to continue to use this app, delete all resources created by this article in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="8d4cf-157">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-157">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="8d4cf-158">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-158">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d4cf-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d4cf-159">Next steps</span></span>

* [<span data-ttu-id="8d4cf-160">Import MongoDB data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8d4cf-160">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
* [<span data-ttu-id="8d4cf-161">Setup a globally replicated Azure Cosmos DB account and use it with MongoDB API</span><span class="sxs-lookup"><span data-stu-id="8d4cf-161">Setup a globally replicated Azure Cosmos DB account and use it with MongoDB API</span></span>](tutorial-global-distribution-mongodb.md)
* [<span data-ttu-id="8d4cf-162">Develop locally with the emulator</span><span class="sxs-lookup"><span data-stu-id="8d4cf-162">Develop locally with the emulator</span></span>](local-emulator.md)
