---
title: 'Quickstart: Cassandra API with Python - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB's Apache Cassandra API to create a profile application  with Python
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-cassandra
ms.custom: quick start connect, mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 11/15/2017
ms.author: sngun
ms.openlocfilehash: 8f662f1d7b39e1757786193911e9fd2623b0a09a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866777"
---
# <a name="quickstart-build-a-cassandra-app-with-python-and-azure-cosmos-db"></a><span data-ttu-id="b5cac-103">Quickstart: Build a Cassandra app with Python and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5cac-103">Quickstart: Build a Cassandra app with Python and Azure Cosmos DB</span></span>

<span data-ttu-id="b5cac-104">This quickstart shows how to use Python and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5cac-104">This quickstart shows how to use Python and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span></span> <span data-ttu-id="b5cac-105">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5cac-105">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span></span>

<span data-ttu-id="b5cac-106">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="b5cac-106">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="b5cac-107">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5cac-107">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="b5cac-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b5cac-108">Prerequisites</span></span>

<span data-ttu-id="b5cac-109">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="b5cac-109">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="b5cac-110">Access to the Azure Cosmos DB Cassandra API preview program.</span><span class="sxs-lookup"><span data-stu-id="b5cac-110">Access to the Azure Cosmos DB Cassandra API preview program.</span></span> <span data-ttu-id="b5cac-111">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span><span class="sxs-lookup"><span data-stu-id="b5cac-111">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span></span>

<span data-ttu-id="b5cac-112">In addition:</span><span class="sxs-lookup"><span data-stu-id="b5cac-112">In addition:</span></span>
* <span data-ttu-id="b5cac-113">[Python](https://www.python.org/downloads/) version v2.7.14</span><span class="sxs-lookup"><span data-stu-id="b5cac-113">[Python](https://www.python.org/downloads/) version v2.7.14</span></span>
* [<span data-ttu-id="b5cac-114">Git</span><span class="sxs-lookup"><span data-stu-id="b5cac-114">Git</span></span>](http://git-scm.com/)
* [<span data-ttu-id="b5cac-115">Python Driver for Apache Cassandra</span><span class="sxs-lookup"><span data-stu-id="b5cac-115">Python Driver for Apache Cassandra</span></span>](https://github.com/datastax/python-driver)

## <a name="create-a-database-account"></a><span data-ttu-id="b5cac-116">Create a database account</span><span class="sxs-lookup"><span data-stu-id="b5cac-116">Create a database account</span></span>

<span data-ttu-id="b5cac-117">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5cac-117">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-cassandra](../../includes/cosmos-db-create-dbaccount-cassandra.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="b5cac-118">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="b5cac-118">Clone the sample application</span></span>

<span data-ttu-id="b5cac-119">Now let's clone a Cassandra API app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="b5cac-119">Now let's clone a Cassandra API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="b5cac-120">You see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="b5cac-120">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="b5cac-121">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="b5cac-121">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="b5cac-122">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="b5cac-122">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="b5cac-123">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="b5cac-123">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="b5cac-124">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="b5cac-124">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="b5cac-125">Review the code</span><span class="sxs-lookup"><span data-stu-id="b5cac-125">Review the code</span></span>

<span data-ttu-id="b5cac-126">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="b5cac-126">This step is optional.</span></span> <span data-ttu-id="b5cac-127">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="b5cac-127">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="b5cac-128">The snippets are all taken from the pyquickstart.py file.</span><span class="sxs-lookup"><span data-stu-id="b5cac-128">The snippets are all taken from the pyquickstart.py file.</span></span> <span data-ttu-id="b5cac-129">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="b5cac-129">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

* <span data-ttu-id="b5cac-130">User name and password is set using the connection string page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5cac-130">User name and password is set using the connection string page in the Azure portal.</span></span> <span data-ttu-id="b5cac-131">You replace the path\to\cert with the path to your X509 certificate.</span><span class="sxs-lookup"><span data-stu-id="b5cac-131">You replace the path\to\cert with the path to your X509 certificate.</span></span>

   ```python
    ssl_opts = {
            'ca_certs': 'path\to\cert',
            'ssl_version': ssl.PROTOCOL_TLSv1_2
            }
    auth_provider = PlainTextAuthProvider( username=cfg.config['username'], password=cfg.config['password'])
    cluster = Cluster([cfg.config['contactPoint']], port = cfg.config['port'], auth_provider=auth_provider, ssl_options=ssl_opts)
    session = cluster.connect()
   
   ```

* <span data-ttu-id="b5cac-132">The `cluster` is initialized with contactPoint information.</span><span class="sxs-lookup"><span data-stu-id="b5cac-132">The `cluster` is initialized with contactPoint information.</span></span> <span data-ttu-id="b5cac-133">The contactPoint is retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5cac-133">The contactPoint is retrieved from the Azure portal.</span></span>

    ```python
   cluster = Cluster([cfg.config['contactPoint']], port = cfg.config['port'], auth_provider=auth_provider)
    ```

* <span data-ttu-id="b5cac-134">The `cluster` connects to the Azure Cosmos DB Cassandra API.</span><span class="sxs-lookup"><span data-stu-id="b5cac-134">The `cluster` connects to the Azure Cosmos DB Cassandra API.</span></span>

    ```python
    session = cluster.connect()
    ```

* <span data-ttu-id="b5cac-135">A new keyspace is created.</span><span class="sxs-lookup"><span data-stu-id="b5cac-135">A new keyspace is created.</span></span>

    ```python
   session.execute('CREATE KEYSPACE IF NOT EXISTS uprofile WITH replication = {\'class\': \'NetworkTopologyStrategy\', \'datacenter1\' : \'1\' }')
    ```

* <span data-ttu-id="b5cac-136">A new table is created.</span><span class="sxs-lookup"><span data-stu-id="b5cac-136">A new table is created.</span></span>

   ```
   session.execute('CREATE TABLE IF NOT EXISTS uprofile.user (user_id int PRIMARY KEY, user_name text, user_bcity text)');
   ```

* <span data-ttu-id="b5cac-137">Key/value entities are inserted.</span><span class="sxs-lookup"><span data-stu-id="b5cac-137">Key/value entities are inserted.</span></span>

    ```Python
    insert_data = session.prepare("INSERT INTO  uprofile.user  (user_id, user_name , user_bcity) VALUES (?,?,?)")
    batch = BatchStatement()
    batch.add(insert_data, (1, 'LyubovK', 'Dubai'))
    batch.add(insert_data, (2, 'JiriK', 'Toronto'))
    batch.add(insert_data, (3, 'IvanH', 'Mumbai'))
    batch.add(insert_data, (4, 'YuliaT', 'Seattle'))
    ....
    session.execute(batch)
    ```

* <span data-ttu-id="b5cac-138">Query to get all key values.</span><span class="sxs-lookup"><span data-stu-id="b5cac-138">Query to get all key values.</span></span>

    ```Python
    rows = session.execute('SELECT * FROM uprofile.user')
    ```  
    
* <span data-ttu-id="b5cac-139">Query to get a key-value.</span><span class="sxs-lookup"><span data-stu-id="b5cac-139">Query to get a key-value.</span></span>

    ```Python
    
    rows = session.execute('SELECT * FROM uprofile.user where user_id=1')
    ```  

## <a name="update-your-connection-string"></a><span data-ttu-id="b5cac-140">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="b5cac-140">Update your connection string</span></span>

<span data-ttu-id="b5cac-141">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="b5cac-141">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="b5cac-142">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="b5cac-142">This enables your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="b5cac-143">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="b5cac-143">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    <span data-ttu-id="b5cac-144">Use the</span><span class="sxs-lookup"><span data-stu-id="b5cac-144">Use the</span></span> ![Copy button](./media/create-cassandra-python/copy.png) <span data-ttu-id="b5cac-146">button on the right side of the screen to copy the top value, the CONTACT POINT.</span><span class="sxs-lookup"><span data-stu-id="b5cac-146">button on the right side of the screen to copy the top value, the CONTACT POINT.</span></span>

    ![View and copy an access user name, password and contact point in the Azure portal, connection string blade](./media/create-cassandra-python/keys.png)

2. <span data-ttu-id="b5cac-148">Open the `config.py` file.</span><span class="sxs-lookup"><span data-stu-id="b5cac-148">Open the `config.py` file.</span></span> 

3. <span data-ttu-id="b5cac-149">Paste the CONTACT POINT value from the portal over `<FILLME>` on line 10.</span><span class="sxs-lookup"><span data-stu-id="b5cac-149">Paste the CONTACT POINT value from the portal over `<FILLME>` on line 10.</span></span>

    <span data-ttu-id="b5cac-150">Line 10 should now look similar to</span><span class="sxs-lookup"><span data-stu-id="b5cac-150">Line 10 should now look similar to</span></span> 

    `'contactPoint': 'cosmos-db-quickstarts.cassandra.cosmosdb.azure.com:10350'`

4. <span data-ttu-id="b5cac-151">Copy the USERNAME value from the portal and paste it over `<FILLME>` on line 6.</span><span class="sxs-lookup"><span data-stu-id="b5cac-151">Copy the USERNAME value from the portal and paste it over `<FILLME>` on line 6.</span></span>

    <span data-ttu-id="b5cac-152">Line 6 should now look similar to</span><span class="sxs-lookup"><span data-stu-id="b5cac-152">Line 6 should now look similar to</span></span> 

    `'username': 'cosmos-db-quickstart',`
    
5. <span data-ttu-id="b5cac-153">Copy the PASSWORD value from the portal and paste it over `<FILLME>` on line 8.</span><span class="sxs-lookup"><span data-stu-id="b5cac-153">Copy the PASSWORD value from the portal and paste it over `<FILLME>` on line 8.</span></span>

    <span data-ttu-id="b5cac-154">Line 8 should now look similar to</span><span class="sxs-lookup"><span data-stu-id="b5cac-154">Line 8 should now look similar to</span></span>

    <span data-ttu-id="b5cac-155">`'password' = '2Ggkr662ifxz2Mg==`';\`</span><span class="sxs-lookup"><span data-stu-id="b5cac-155">`'password' = '2Ggkr662ifxz2Mg==`';\`</span></span>

6. <span data-ttu-id="b5cac-156">Save the config.py file.</span><span class="sxs-lookup"><span data-stu-id="b5cac-156">Save the config.py file.</span></span>
    
## <a name="use-the-x509-certificate"></a><span data-ttu-id="b5cac-157">Use the X509 certificate</span><span class="sxs-lookup"><span data-stu-id="b5cac-157">Use the X509 certificate</span></span>

1. <span data-ttu-id="b5cac-158">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4🇩🇪20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span><span class="sxs-lookup"><span data-stu-id="b5cac-158">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4🇩🇪20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="b5cac-159">It can be downloaded from https://cacert.omniroot.com/bc2025.crt, saved to a local file with extension .cer</span><span class="sxs-lookup"><span data-stu-id="b5cac-159">It can be downloaded from https://cacert.omniroot.com/bc2025.crt, saved to a local file with extension .cer</span></span>

2. <span data-ttu-id="b5cac-160">Open pyquickstart.py and change the 'path\to\cert' to point to your new certificate.</span><span class="sxs-lookup"><span data-stu-id="b5cac-160">Open pyquickstart.py and change the 'path\to\cert' to point to your new certificate.</span></span>

3. <span data-ttu-id="b5cac-161">Save pyquickstart.py.</span><span class="sxs-lookup"><span data-stu-id="b5cac-161">Save pyquickstart.py.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="b5cac-162">Run the app</span><span class="sxs-lookup"><span data-stu-id="b5cac-162">Run the app</span></span>

1. <span data-ttu-id="b5cac-163">Use the cd command in the git terminal to change into the azure-cosmos-db-cassandra-python-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="b5cac-163">Use the cd command in the git terminal to change into the azure-cosmos-db-cassandra-python-getting-started folder.</span></span> 

2. <span data-ttu-id="b5cac-164">Run the following commands to install the required modules:</span><span class="sxs-lookup"><span data-stu-id="b5cac-164">Run the following commands to install the required modules:</span></span>

    ```python
    python -m pip install cassandra-driver
    python -m pip install prettytable
    python -m pip install requests
    python -m pip install pyopenssl
    ```

2. <span data-ttu-id="b5cac-165">Run the following command to start your node application:</span><span class="sxs-lookup"><span data-stu-id="b5cac-165">Run the following command to start your node application:</span></span>

    ```
    python pyquickstart.py
    ```

3. <span data-ttu-id="b5cac-166">Verify the results as expected from the command line.</span><span class="sxs-lookup"><span data-stu-id="b5cac-166">Verify the results as expected from the command line.</span></span>

    <span data-ttu-id="b5cac-167">Press CTRL + C to stop exection of the program and close the console window.</span><span class="sxs-lookup"><span data-stu-id="b5cac-167">Press CTRL + C to stop exection of the program and close the console window.</span></span> 

    ![View and verify the output](./media/create-cassandra-python/output.png)
    
    <span data-ttu-id="b5cac-169">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="b5cac-169">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span></span> 

    ![View the data in Data Explorer](./media/create-cassandra-python/data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="b5cac-171">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b5cac-171">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b5cac-172">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b5cac-172">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="b5cac-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5cac-173">Next steps</span></span>

<span data-ttu-id="b5cac-174">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a container using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="b5cac-174">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a container using the Data Explorer, and run an app.</span></span> <span data-ttu-id="b5cac-175">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="b5cac-175">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5cac-176">Import Cassandra data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5cac-176">Import Cassandra data into Azure Cosmos DB</span></span>](cassandra-import-data.md)

