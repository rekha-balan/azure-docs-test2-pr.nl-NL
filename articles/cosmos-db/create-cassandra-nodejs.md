---
title: 'Quickstart: Cassandra API with Node.js - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Cassandra API to create a profile application with Node.js
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-cassandra
ms.custom: quick start connect, mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 11/15/2017
ms.author: sngun
ms.openlocfilehash: e86b80328c3717220b2771a1bf8f4232f9a51748
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870927"
---
# <a name="quickstart-build-a-cassandra-app-with-nodejs-and-azure-cosmos-db"></a><span data-ttu-id="29286-103">Quickstart: Build a Cassandra app with Node.js and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29286-103">Quickstart: Build a Cassandra app with Node.js and Azure Cosmos DB</span></span>

<span data-ttu-id="29286-104">This quickstart shows how to use Node.js and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="29286-104">This quickstart shows how to use Node.js and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span></span> <span data-ttu-id="29286-105">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="29286-105">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span></span>

<span data-ttu-id="29286-106">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="29286-106">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="29286-107">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29286-107">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="29286-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="29286-108">Prerequisites</span></span>

<span data-ttu-id="29286-109">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="29286-109">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="29286-110">Access to the Azure Cosmos DB Cassandra API preview program.</span><span class="sxs-lookup"><span data-stu-id="29286-110">Access to the Azure Cosmos DB Cassandra API preview program.</span></span> <span data-ttu-id="29286-111">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span><span class="sxs-lookup"><span data-stu-id="29286-111">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span></span>

<span data-ttu-id="29286-112">In addition:</span><span class="sxs-lookup"><span data-stu-id="29286-112">In addition:</span></span>
* <span data-ttu-id="29286-113">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span><span class="sxs-lookup"><span data-stu-id="29286-113">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
* [<span data-ttu-id="29286-114">Git</span><span class="sxs-lookup"><span data-stu-id="29286-114">Git</span></span>](http://git-scm.com/)

## <a name="create-a-database-account"></a><span data-ttu-id="29286-115">Create a database account</span><span class="sxs-lookup"><span data-stu-id="29286-115">Create a database account</span></span>

<span data-ttu-id="29286-116">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29286-116">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-cassandra](../../includes/cosmos-db-create-dbaccount-cassandra.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="29286-117">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="29286-117">Clone the sample application</span></span>

<span data-ttu-id="29286-118">Now let's clone a Cassandra API app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="29286-118">Now let's clone a Cassandra API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="29286-119">You see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="29286-119">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="29286-120">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="29286-120">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="29286-121">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="29286-121">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="29286-122">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="29286-122">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="29286-123">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="29286-123">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-cassandra-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="29286-124">Review the code</span><span class="sxs-lookup"><span data-stu-id="29286-124">Review the code</span></span>

<span data-ttu-id="29286-125">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="29286-125">This step is optional.</span></span> <span data-ttu-id="29286-126">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="29286-126">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="29286-127">The snippets are all taken from the uprofile.js file in the C:\git-samples\azure-cosmos-db-cassandra-nodejs-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="29286-127">The snippets are all taken from the uprofile.js file in the C:\git-samples\azure-cosmos-db-cassandra-nodejs-getting-started folder.</span></span> <span data-ttu-id="29286-128">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="29286-128">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

* <span data-ttu-id="29286-129">User name and password is set using the connection string page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="29286-129">User name and password is set using the connection string page in the Azure portal.</span></span> <span data-ttu-id="29286-130">The \`path\to\cert' provides a path to an X509 certificate.</span><span class="sxs-lookup"><span data-stu-id="29286-130">The \`path\to\cert' provides a path to an X509 certificate.</span></span> 

   ```nodejs
   var ssl_option = {
        cert : fs.readFileSync("path\to\cert"),
        rejectUnauthorized : true,
        secureProtocol: 'TLSv1_2_method'
        };
   const authProviderLocalCassandra = new cassandra.auth.PlainTextAuthProvider(config.username, config.password);
   ```

* <span data-ttu-id="29286-131">The `client` is initialized with contactPoint information.</span><span class="sxs-lookup"><span data-stu-id="29286-131">The `client` is initialized with contactPoint information.</span></span> <span data-ttu-id="29286-132">The contactPoint is retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="29286-132">The contactPoint is retrieved from the Azure portal.</span></span>

    ```nodejs
    const client = new cassandra.Client({contactPoints: [config.contactPoint], authProvider: authProviderLocalCassandra, sslOptions:ssl_option});
    ```

* <span data-ttu-id="29286-133">The `client` connects to the Azure Cosmos DB Cassandra API.</span><span class="sxs-lookup"><span data-stu-id="29286-133">The `client` connects to the Azure Cosmos DB Cassandra API.</span></span>

    ```nodejs
    client.connect(next);
    ```

* <span data-ttu-id="29286-134">A new keyspace is created.</span><span class="sxs-lookup"><span data-stu-id="29286-134">A new keyspace is created.</span></span>

    ```nodejs
    function createKeyspace(next) {
        var query = "CREATE KEYSPACE IF NOT EXISTS uprofile WITH replication = {\'class\': \'NetworkTopologyStrategy\', \'datacenter1\' : \'1\' }";
        client.execute(query, next);
        console.log("created keyspace");    
  }
    ```

* <span data-ttu-id="29286-135">A new table is created.</span><span class="sxs-lookup"><span data-stu-id="29286-135">A new table is created.</span></span>

   ```nodejs
   function createTable(next) {
    var query = "CREATE TABLE IF NOT EXISTS uprofile.user (user_id int PRIMARY KEY, user_name text, user_bcity text)";
        client.execute(query, next);
        console.log("created table");
   },
   ```

* <span data-ttu-id="29286-136">Key/value entities are inserted.</span><span class="sxs-lookup"><span data-stu-id="29286-136">Key/value entities are inserted.</span></span>

    ```nodejs
    ...
       {
          query: 'INSERT INTO  uprofile.user  (user_id, user_name , user_bcity) VALUES (?,?,?)',
          params: [5, 'IvanaV', 'Belgaum', '2017-10-3136']
        }
    ];
    client.batch(queries, { prepare: true}, next);
    ```

* <span data-ttu-id="29286-137">Query to get all key values.</span><span class="sxs-lookup"><span data-stu-id="29286-137">Query to get all key values.</span></span>

    ```nodejs
   var query = 'SELECT * FROM uprofile.user';
    client.execute(query, { prepare: true}, function (err, result) {
      if (err) return next(err);
      result.rows.forEach(function(row) {
        console.log('Obtained row: %d | %s | %s ',row.user_id, row.user_name, row.user_bcity);
      }, this);
      next();
    });
    ```  
    
* <span data-ttu-id="29286-138">Query to get a key-value.</span><span class="sxs-lookup"><span data-stu-id="29286-138">Query to get a key-value.</span></span>

    ```nodejs
    function selectById(next) {
        console.log("\Getting by id");
        var query = 'SELECT * FROM uprofile.user where user_id=1';
        client.execute(query, { prepare: true}, function (err, result) {
        if (err) return next(err);
            result.rows.forEach(function(row) {
            console.log('Obtained row: %d | %s | %s ',row.user_id, row.user_name, row.user_bcity);
        }, this);
        next();
        });
    }
    ```  

## <a name="update-your-connection-string"></a><span data-ttu-id="29286-139">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="29286-139">Update your connection string</span></span>

<span data-ttu-id="29286-140">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="29286-140">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="29286-141">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="29286-141">This enables your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="29286-142">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="29286-142">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    <span data-ttu-id="29286-143">Use the</span><span class="sxs-lookup"><span data-stu-id="29286-143">Use the</span></span> ![Copy button](./media/create-cassandra-nodejs/copy.png) <span data-ttu-id="29286-145">button on the right side of the screen to copy the top value, the CONTACT POINT.</span><span class="sxs-lookup"><span data-stu-id="29286-145">button on the right side of the screen to copy the top value, the CONTACT POINT.</span></span>

    ![View and copy the CONTACT POINT, USERNAME,and PASSWORD from the Azure portal, connection string page](./media/create-cassandra-nodejs/keys.png)

2. <span data-ttu-id="29286-147">Open the `config.js` file.</span><span class="sxs-lookup"><span data-stu-id="29286-147">Open the `config.js` file.</span></span> 

3. <span data-ttu-id="29286-148">Paste the CONTACT POINT value from the portal over `<FillMEIN>` on line 4.</span><span class="sxs-lookup"><span data-stu-id="29286-148">Paste the CONTACT POINT value from the portal over `<FillMEIN>` on line 4.</span></span>

    <span data-ttu-id="29286-149">Line 4 should now look similar to</span><span class="sxs-lookup"><span data-stu-id="29286-149">Line 4 should now look similar to</span></span> 

    `config.contactPoint = "cosmos-db-quickstarts.cassandra.cosmosdb.azure.com:10350"`

4. <span data-ttu-id="29286-150">Copy the USERNAME value from the portal and paste it over `<FillMEIN>` on line 2.</span><span class="sxs-lookup"><span data-stu-id="29286-150">Copy the USERNAME value from the portal and paste it over `<FillMEIN>` on line 2.</span></span>

    <span data-ttu-id="29286-151">Line 2 should now look similar to</span><span class="sxs-lookup"><span data-stu-id="29286-151">Line 2 should now look similar to</span></span> 

    `config.username = 'cosmos-db-quickstart';`
    
5. <span data-ttu-id="29286-152">Copy the PASSWORD value from the portal and paste it over `<FillMEIN>` on line 3.</span><span class="sxs-lookup"><span data-stu-id="29286-152">Copy the PASSWORD value from the portal and paste it over `<FillMEIN>` on line 3.</span></span>

    <span data-ttu-id="29286-153">Line 3 should now look similar to</span><span class="sxs-lookup"><span data-stu-id="29286-153">Line 3 should now look similar to</span></span>

    `config.password = '2Ggkr662ifxz2Mg==';`

6. <span data-ttu-id="29286-154">Save the config.js file.</span><span class="sxs-lookup"><span data-stu-id="29286-154">Save the config.js file.</span></span>
    
## <a name="use-the-x509-certificate"></a><span data-ttu-id="29286-155">Use the X509 certificate</span><span class="sxs-lookup"><span data-stu-id="29286-155">Use the X509 certificate</span></span> 

1. <span data-ttu-id="29286-156">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4🇩🇪20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span><span class="sxs-lookup"><span data-stu-id="29286-156">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4🇩🇪20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="29286-157">It can be downloaded from https://cacert.omniroot.com/bc2025.crt, saved to a local file with extension .cer.</span><span class="sxs-lookup"><span data-stu-id="29286-157">It can be downloaded from https://cacert.omniroot.com/bc2025.crt, saved to a local file with extension .cer.</span></span> 

2. <span data-ttu-id="29286-158">Open uprofile.js and change the 'path\to\cert' to point to your new certificate.</span><span class="sxs-lookup"><span data-stu-id="29286-158">Open uprofile.js and change the 'path\to\cert' to point to your new certificate.</span></span> 

3. <span data-ttu-id="29286-159">Save uprofile.js.</span><span class="sxs-lookup"><span data-stu-id="29286-159">Save uprofile.js.</span></span> 

## <a name="run-the-app"></a><span data-ttu-id="29286-160">Run the app</span><span class="sxs-lookup"><span data-stu-id="29286-160">Run the app</span></span>

1. <span data-ttu-id="29286-161">In the git terminal window, run `npm install` to install the required npm modules.</span><span class="sxs-lookup"><span data-stu-id="29286-161">In the git terminal window, run `npm install` to install the required npm modules.</span></span>

2. <span data-ttu-id="29286-162">Run `node uprofile.js` to start your node application.</span><span class="sxs-lookup"><span data-stu-id="29286-162">Run `node uprofile.js` to start your node application.</span></span>

3. <span data-ttu-id="29286-163">Verify the results as expected from the command line.</span><span class="sxs-lookup"><span data-stu-id="29286-163">Verify the results as expected from the command line.</span></span>

    ![View and verify the output](./media/create-cassandra-nodejs/output.png)

    <span data-ttu-id="29286-165">Press CTRL + C to stop exection of the program and close the console window.</span><span class="sxs-lookup"><span data-stu-id="29286-165">Press CTRL + C to stop exection of the program and close the console window.</span></span> 

    <span data-ttu-id="29286-166">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="29286-166">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span></span> 

    ![View the data in Data Explorer](./media/create-cassandra-nodejs/data-explorer.png) 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="29286-168">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="29286-168">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="29286-169">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="29286-169">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="29286-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="29286-170">Next steps</span></span>

<span data-ttu-id="29286-171">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a container using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="29286-171">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a container using the Data Explorer, and run an app.</span></span> <span data-ttu-id="29286-172">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="29286-172">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="29286-173">Import Cassandra data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29286-173">Import Cassandra data into Azure Cosmos DB</span></span>](cassandra-import-data.md)


