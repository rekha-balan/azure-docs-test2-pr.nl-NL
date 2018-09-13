---
title: 'Azure Cosmos DB: Develop with the Cassandra API in Java | Microsoft Docs'
description: Learn how to develop with Azure Cosmos DB's Cassandra API using Java
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: ''
tags: ''
ms.service: cosmos-db
ms.component: cosmosdb-cassandra
ms.devlang: java
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: sngun
ms.custom: mvc
ms.openlocfilehash: 13e757d3d6d35227667e23eb6000eace56a0674e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868479"
---
# <a name="azure-cosmosdb-develop-with-the-cassandra-api-in-java"></a><span data-ttu-id="8de8c-103">Azure CosmosDB: Develop with the Cassandra API in Java</span><span class="sxs-lookup"><span data-stu-id="8de8c-103">Azure CosmosDB: Develop with the Cassandra API in Java</span></span>

<span data-ttu-id="8de8c-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="8de8c-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="8de8c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8de8c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="8de8c-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a Cassandra Table(sql-api-partition-data.md#partition-keys) using the [Cassandra API](cassandra-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8de8c-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a Cassandra Table(sql-api-partition-data.md#partition-keys) using the [Cassandra API](cassandra-introduction.md).</span></span> <span data-ttu-id="8de8c-107">By defining a primary key when you create a Table, your application is prepared to scale effortlessly as your data grows.</span><span class="sxs-lookup"><span data-stu-id="8de8c-107">By defining a primary key when you create a Table, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="8de8c-108">This tutorial covers the following tasks by using the Cassandra API:</span><span class="sxs-lookup"><span data-stu-id="8de8c-108">This tutorial covers the following tasks by using the Cassandra API:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8de8c-109">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="8de8c-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="8de8c-110">Create a keyspace and table with a primary key</span><span class="sxs-lookup"><span data-stu-id="8de8c-110">Create a keyspace and table with a primary key</span></span>
> * <span data-ttu-id="8de8c-111">Insert data</span><span class="sxs-lookup"><span data-stu-id="8de8c-111">Insert data</span></span>
> * <span data-ttu-id="8de8c-112">Query data</span><span class="sxs-lookup"><span data-stu-id="8de8c-112">Query data</span></span>
> * <span data-ttu-id="8de8c-113">Review SLAs</span><span class="sxs-lookup"><span data-stu-id="8de8c-113">Review SLAs</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8de8c-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8de8c-114">Prerequisites</span></span>

<span data-ttu-id="8de8c-115">Access to the Azure Cosmos DB Cassandra API preview program.</span><span class="sxs-lookup"><span data-stu-id="8de8c-115">Access to the Azure Cosmos DB Cassandra API preview program.</span></span> <span data-ttu-id="8de8c-116">If you haven't applied for access yet, [sign up now](https://aka.ms/cosmosdb-cassandra-signup).</span><span class="sxs-lookup"><span data-stu-id="8de8c-116">If you haven't applied for access yet, [sign up now](https://aka.ms/cosmosdb-cassandra-signup).</span></span>

<span data-ttu-id="8de8c-117">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="8de8c-117">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="8de8c-118">In addition:</span><span class="sxs-lookup"><span data-stu-id="8de8c-118">In addition:</span></span> 

* [<span data-ttu-id="8de8c-119">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="8de8c-119">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="8de8c-120">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="8de8c-120">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="8de8c-121">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="8de8c-121">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="8de8c-122">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span><span class="sxs-lookup"><span data-stu-id="8de8c-122">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="8de8c-123">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="8de8c-123">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="8de8c-124">Git</span><span class="sxs-lookup"><span data-stu-id="8de8c-124">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="8de8c-125">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="8de8c-125">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="8de8c-126">Create a database account</span><span class="sxs-lookup"><span data-stu-id="8de8c-126">Create a database account</span></span>

<span data-ttu-id="8de8c-127">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8de8c-127">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-cassandra](../../includes/cosmos-db-create-dbaccount-cassandra.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="8de8c-128">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="8de8c-128">Clone the sample application</span></span>

<span data-ttu-id="8de8c-129">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="8de8c-129">Now let's switch to working with code.</span></span> <span data-ttu-id="8de8c-130">Let's clone a Cassandra app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="8de8c-130">Let's clone a Cassandra app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="8de8c-131">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="8de8c-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="8de8c-132">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="8de8c-132">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span></span> 

    ```bash
    cd "C:\git-samples"
    ```

2. <span data-ttu-id="8de8c-133">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="8de8c-133">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="8de8c-134">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="8de8c-134">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-cassandra-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="8de8c-135">Review the code</span><span class="sxs-lookup"><span data-stu-id="8de8c-135">Review the code</span></span>

<span data-ttu-id="8de8c-136">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="8de8c-136">This step is optional.</span></span> <span data-ttu-id="8de8c-137">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="8de8c-137">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="8de8c-138">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="8de8c-138">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> <span data-ttu-id="8de8c-139">These snippets are all taken from the src/main/java/com/azure/cosmosdb/cassandra/util/CassandraUtils.java.</span><span class="sxs-lookup"><span data-stu-id="8de8c-139">These snippets are all taken from the src/main/java/com/azure/cosmosdb/cassandra/util/CassandraUtils.java.</span></span>  

* <span data-ttu-id="8de8c-140">Cassandra host, port, user name, password, and SSL options are set.</span><span class="sxs-lookup"><span data-stu-id="8de8c-140">Cassandra host, port, user name, password, and SSL options are set.</span></span> <span data-ttu-id="8de8c-141">The connection string information comes from the connection string page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8de8c-141">The connection string information comes from the connection string page in the Azure portal.</span></span>

   ```java
   cluster = Cluster.builder().addContactPoint(cassandraHost).withPort(cassandraPort).withCredentials(cassandraUsername, cassandraPassword).withSSL(sslOptions).build();
   ```

* <span data-ttu-id="8de8c-142">The `cluster` connects to the Azure Cosmos DB Cassandra API and returns a session to access.</span><span class="sxs-lookup"><span data-stu-id="8de8c-142">The `cluster` connects to the Azure Cosmos DB Cassandra API and returns a session to access.</span></span>

    ```java
    return cluster.connect();
    ```

<span data-ttu-id="8de8c-143">The following snippets are from the src/main/java/com/azure/cosmosdb/cassandra/repository/UserRepository.java file.</span><span class="sxs-lookup"><span data-stu-id="8de8c-143">The following snippets are from the src/main/java/com/azure/cosmosdb/cassandra/repository/UserRepository.java file.</span></span>

* <span data-ttu-id="8de8c-144">Create a new keyspace.</span><span class="sxs-lookup"><span data-stu-id="8de8c-144">Create a new keyspace.</span></span>

    ```java
    public void createKeyspace() {
        final String query = "CREATE KEYSPACE IF NOT EXISTS uprofile WITH replication = {'class': 'SimpleStrategy', 'replication_factor': '3' } ";
        session.execute(query);
        LOGGER.info("Created keyspace 'uprofile'");
    }
    ```

* <span data-ttu-id="8de8c-145">Create a new table.</span><span class="sxs-lookup"><span data-stu-id="8de8c-145">Create a new table.</span></span>

   ```java
   public void createTable() {
        final String query = "CREATE TABLE IF NOT EXISTS uprofile.user (user_id int PRIMARY KEY, user_name text, user_bcity text)";
        session.execute(query);
        LOGGER.info("Created table 'user'");
   }
   ```

* <span data-ttu-id="8de8c-146">Insert user entities using a prepared statement object.</span><span class="sxs-lookup"><span data-stu-id="8de8c-146">Insert user entities using a prepared statement object.</span></span>

    ```java
    public PreparedStatement prepareInsertStatement() {
        final String insertStatement = "INSERT INTO  uprofile.user (user_id, user_name , user_bcity) VALUES (?,?,?)";
        return session.prepare(insertStatement);
    }

    public void insertUser(PreparedStatement statement, int id, String name, String city) {
        BoundStatement boundStatement = new BoundStatement(statement);
        session.execute(boundStatement.bind(id, name, city));
    }
    ```

* <span data-ttu-id="8de8c-147">Query to get all user information.</span><span class="sxs-lookup"><span data-stu-id="8de8c-147">Query to get all user information.</span></span>

    ```java
   public void selectAllUsers() {
        final String query = "SELECT * FROM uprofile.user";
        List<Row> rows = session.execute(query).all();

        for (Row row : rows) {
            LOGGER.info("Obtained row: {} | {} | {} ", row.getInt("user_id"), row.getString("user_name"), row.getString("user_bcity"));
        }
    }
    ```

* <span data-ttu-id="8de8c-148">Query to get a single user's information.</span><span class="sxs-lookup"><span data-stu-id="8de8c-148">Query to get a single user's information.</span></span>

    ```java
    public void selectUser(int id) {
        final String query = "SELECT * FROM uprofile.user where user_id = 3";
        Row row = session.execute(query).one();

        LOGGER.info("Obtained row: {} | {} | {} ", row.getInt("user_id"), row.getString("user_name"), row.getString("user_bcity"));
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="8de8c-149">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="8de8c-149">Update your connection string</span></span>

<span data-ttu-id="8de8c-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="8de8c-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="8de8c-151">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="8de8c-151">This enables your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="8de8c-152">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="8de8c-152">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    ![View and copy a username from the Azure portal, Connection String page](./media/tutorial-develop-cassandra-java/keys.png)

2. <span data-ttu-id="8de8c-154">Use the</span><span class="sxs-lookup"><span data-stu-id="8de8c-154">Use the</span></span> ![Copy button](./media/tutorial-develop-cassandra-java/copy.png) <span data-ttu-id="8de8c-156">button on the right side of the screen to copy the CONTACT POINT value.</span><span class="sxs-lookup"><span data-stu-id="8de8c-156">button on the right side of the screen to copy the CONTACT POINT value.</span></span>

3. <span data-ttu-id="8de8c-157">Open the `config.properties` file from C:\git-samples\azure-cosmosdb-cassandra-java-getting-started\java-examples\src\main\resources folder.</span><span class="sxs-lookup"><span data-stu-id="8de8c-157">Open the `config.properties` file from C:\git-samples\azure-cosmosdb-cassandra-java-getting-started\java-examples\src\main\resources folder.</span></span> 

3. <span data-ttu-id="8de8c-158">Paste the CONTACT POINT value from the portal over `<Cassandra endpoint host>` on line 2.</span><span class="sxs-lookup"><span data-stu-id="8de8c-158">Paste the CONTACT POINT value from the portal over `<Cassandra endpoint host>` on line 2.</span></span>

    <span data-ttu-id="8de8c-159">Line 2 of config.properties should now look similar to</span><span class="sxs-lookup"><span data-stu-id="8de8c-159">Line 2 of config.properties should now look similar to</span></span> 

    `cassandra_host=cosmos-db-quickstarts.documents.azure.com`

3. <span data-ttu-id="8de8c-160">Go back to portal and copy the USERNAME value.</span><span class="sxs-lookup"><span data-stu-id="8de8c-160">Go back to portal and copy the USERNAME value.</span></span> <span data-ttu-id="8de8c-161">Past the USERNAME value from the portal over `<cassandra endpoint username>` on line 4.</span><span class="sxs-lookup"><span data-stu-id="8de8c-161">Past the USERNAME value from the portal over `<cassandra endpoint username>` on line 4.</span></span>

    <span data-ttu-id="8de8c-162">Line 4 of config.properties should now look similar to</span><span class="sxs-lookup"><span data-stu-id="8de8c-162">Line 4 of config.properties should now look similar to</span></span> 

    `cassandra_username=cosmos-db-quickstart`

4. <span data-ttu-id="8de8c-163">Go back to portal and copy the PASSWORD value.</span><span class="sxs-lookup"><span data-stu-id="8de8c-163">Go back to portal and copy the PASSWORD value.</span></span> <span data-ttu-id="8de8c-164">Paste the PASSWORD value from the portal over `<cassandra endpoint password>` on line 5.</span><span class="sxs-lookup"><span data-stu-id="8de8c-164">Paste the PASSWORD value from the portal over `<cassandra endpoint password>` on line 5.</span></span>

    <span data-ttu-id="8de8c-165">Line 5 of config.properties should now look similar to</span><span class="sxs-lookup"><span data-stu-id="8de8c-165">Line 5 of config.properties should now look similar to</span></span> 

    `cassandra_password=2Ggkr662ifxz2Mg...==`

5. <span data-ttu-id="8de8c-166">On line 6, if you want to use a specific SSL certificate, then replace `<SSL key store file location>` with the location of the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="8de8c-166">On line 6, if you want to use a specific SSL certificate, then replace `<SSL key store file location>` with the location of the SSL certificate.</span></span> <span data-ttu-id="8de8c-167">If a value is not provided, the JDK certificate installed at <JAVA_HOME>/jre/lib/security/cacerts is used.</span><span class="sxs-lookup"><span data-stu-id="8de8c-167">If a value is not provided, the JDK certificate installed at <JAVA_HOME>/jre/lib/security/cacerts is used.</span></span> 

6. <span data-ttu-id="8de8c-168">If you changed line 6 to use a specific SSL certificate, update line 7 to use the password for that certificate.</span><span class="sxs-lookup"><span data-stu-id="8de8c-168">If you changed line 6 to use a specific SSL certificate, update line 7 to use the password for that certificate.</span></span> 

7. <span data-ttu-id="8de8c-169">Save the config.properties file.</span><span class="sxs-lookup"><span data-stu-id="8de8c-169">Save the config.properties file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="8de8c-170">Run the app</span><span class="sxs-lookup"><span data-stu-id="8de8c-170">Run the app</span></span>

1. <span data-ttu-id="8de8c-171">In the git terminal window, `cd` to the azure-cosmosdb-cassandra-java-getting-started\java-examples folder.</span><span class="sxs-lookup"><span data-stu-id="8de8c-171">In the git terminal window, `cd` to the azure-cosmosdb-cassandra-java-getting-started\java-examples folder.</span></span>

    ```git
    cd "C:\git-samples\azure-cosmosdb-cassandra-java-getting-started\java-examples"
    ```

2. <span data-ttu-id="8de8c-172">In the git terminal window, use the following command to generate the cosmosdb-cassandra-examples.jar file.</span><span class="sxs-lookup"><span data-stu-id="8de8c-172">In the git terminal window, use the following command to generate the cosmosdb-cassandra-examples.jar file.</span></span>

    ```git
    mvn clean install
    ```

3. <span data-ttu-id="8de8c-173">In the git terminal window, run the following command to start the Java application.</span><span class="sxs-lookup"><span data-stu-id="8de8c-173">In the git terminal window, run the following command to start the Java application.</span></span>

    ```git
    java -cp target/cosmosdb-cassandra-examples.jar com.azure.cosmosdb.cassandra.examples.UserProfile
    ```

    <span data-ttu-id="8de8c-174">The terminal window displays notifications that the keyspace and table are created.</span><span class="sxs-lookup"><span data-stu-id="8de8c-174">The terminal window displays notifications that the keyspace and table are created.</span></span> <span data-ttu-id="8de8c-175">It then selects and returns all users in the table and displays the output, and then selects a row by id and displays the value.</span><span class="sxs-lookup"><span data-stu-id="8de8c-175">It then selects and returns all users in the table and displays the output, and then selects a row by id and displays the value.</span></span>  
    
    <span data-ttu-id="8de8c-176">You can now go back to Data Explorer and see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="8de8c-176">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="8de8c-177">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8de8c-177">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8de8c-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8de8c-178">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="8de8c-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="8de8c-179">Next steps</span></span>

<span data-ttu-id="8de8c-180">In this quickstart, you've learned how to do the following:</span><span class="sxs-lookup"><span data-stu-id="8de8c-180">In this quickstart, you've learned how to do the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8de8c-181">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="8de8c-181">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="8de8c-182">Create a keyspace and table with a primary key</span><span class="sxs-lookup"><span data-stu-id="8de8c-182">Create a keyspace and table with a primary key</span></span>
> * <span data-ttu-id="8de8c-183">Insert data</span><span class="sxs-lookup"><span data-stu-id="8de8c-183">Insert data</span></span>
> * <span data-ttu-id="8de8c-184">Query data</span><span class="sxs-lookup"><span data-stu-id="8de8c-184">Query data</span></span>
> * <span data-ttu-id="8de8c-185">Reivew SLAs</span><span class="sxs-lookup"><span data-stu-id="8de8c-185">Reivew SLAs</span></span>

<span data-ttu-id="8de8c-186">You can now import additional data into your Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="8de8c-186">You can now import additional data into your Azure Cosmos DB container.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8de8c-187">Import Cassandra data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8de8c-187">Import Cassandra data into Azure Cosmos DB</span></span>](cassandra-import-data.md)
