---
title: 'Quickstart: Cassandra API with Java - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Cassandra API to create a profile application with the Azure portal and Java
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-cassandra
ms.custom: quick start connect, mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 11/15/2017
ms.author: sngun
ms.openlocfilehash: e0344aadbbf263fa3c84ee37f2527eb41b19b7d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869463"
---
# <a name="quickstart-build-a-cassandra-app-with-java-and-azure-cosmos-db"></a><span data-ttu-id="e4674-103">Quickstart: Build a Cassandra app with Java and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4674-103">Quickstart: Build a Cassandra app with Java and Azure Cosmos DB</span></span>

<span data-ttu-id="e4674-104">This quickstart shows how to use Java and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="e4674-104">This quickstart shows how to use Java and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span></span> <span data-ttu-id="e4674-105">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e4674-105">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span></span>

<span data-ttu-id="e4674-106">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="e4674-106">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="e4674-107">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4674-107">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e4674-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4674-108">Prerequisites</span></span>

<span data-ttu-id="e4674-109">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="e4674-109">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="e4674-110">Access to the Azure Cosmos DB Cassandra API preview program.</span><span class="sxs-lookup"><span data-stu-id="e4674-110">Access to the Azure Cosmos DB Cassandra API preview program.</span></span> <span data-ttu-id="e4674-111">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span><span class="sxs-lookup"><span data-stu-id="e4674-111">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span></span>

<span data-ttu-id="e4674-112">In addition:</span><span class="sxs-lookup"><span data-stu-id="e4674-112">In addition:</span></span> 

* [<span data-ttu-id="e4674-113">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="e4674-113">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="e4674-114">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="e4674-114">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="e4674-115">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="e4674-115">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="e4674-116">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span><span class="sxs-lookup"><span data-stu-id="e4674-116">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="e4674-117">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="e4674-117">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="e4674-118">Git</span><span class="sxs-lookup"><span data-stu-id="e4674-118">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="e4674-119">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="e4674-119">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>



## <a name="create-a-database-account"></a><span data-ttu-id="e4674-120">Create a database account</span><span class="sxs-lookup"><span data-stu-id="e4674-120">Create a database account</span></span>

<span data-ttu-id="e4674-121">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4674-121">Before you can create a document database, you need to create a Cassandra account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-cassandra](../../includes/cosmos-db-create-dbaccount-cassandra.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="e4674-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="e4674-122">Clone the sample application</span></span>

<span data-ttu-id="e4674-123">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="e4674-123">Now let's switch to working with code.</span></span> <span data-ttu-id="e4674-124">Let's clone a Cassandra app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="e4674-124">Let's clone a Cassandra app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="e4674-125">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="e4674-125">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="e4674-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="e4674-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="e4674-127">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="e4674-127">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="e4674-128">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="e4674-128">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="e4674-129">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="e4674-129">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-cassandra-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="e4674-130">Review the code</span><span class="sxs-lookup"><span data-stu-id="e4674-130">Review the code</span></span>

<span data-ttu-id="e4674-131">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="e4674-131">This step is optional.</span></span> <span data-ttu-id="e4674-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="e4674-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="e4674-133">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="e4674-133">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> <span data-ttu-id="e4674-134">These snippets are all taken from the src/main/java/com/azure/cosmosdb/cassandra/util/CassandraUtils.java file.</span><span class="sxs-lookup"><span data-stu-id="e4674-134">These snippets are all taken from the src/main/java/com/azure/cosmosdb/cassandra/util/CassandraUtils.java file.</span></span>  

* <span data-ttu-id="e4674-135">Cassandra host, port, user name, password, and SSL options are set.</span><span class="sxs-lookup"><span data-stu-id="e4674-135">Cassandra host, port, user name, password, and SSL options are set.</span></span> <span data-ttu-id="e4674-136">The connection string information comes from the connection string page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e4674-136">The connection string information comes from the connection string page in the Azure portal.</span></span>

   ```java
   cluster = Cluster.builder().addContactPoint(cassandraHost).withPort(cassandraPort).withCredentials(cassandraUsername, cassandraPassword).withSSL(sslOptions).build();
   ```

* <span data-ttu-id="e4674-137">The `cluster` connects to the Azure Cosmos DB Cassandra API and returns a session to access.</span><span class="sxs-lookup"><span data-stu-id="e4674-137">The `cluster` connects to the Azure Cosmos DB Cassandra API and returns a session to access.</span></span>

    ```java
    return cluster.connect();
    ```

<span data-ttu-id="e4674-138">The following snippets are from the src/main/java/com/azure/cosmosdb/cassandra/repository/UserRepository.java file.</span><span class="sxs-lookup"><span data-stu-id="e4674-138">The following snippets are from the src/main/java/com/azure/cosmosdb/cassandra/repository/UserRepository.java file.</span></span>

* <span data-ttu-id="e4674-139">Create a new keyspace.</span><span class="sxs-lookup"><span data-stu-id="e4674-139">Create a new keyspace.</span></span>

    ```java
    public void createKeyspace() {
        final String query = "CREATE KEYSPACE IF NOT EXISTS uprofile WITH replication = {'class': 'SimpleStrategy', 'replication_factor': '3' } ";
        session.execute(query);
        LOGGER.info("Created keyspace 'uprofile'");
    }
    ```

* <span data-ttu-id="e4674-140">Create a new table.</span><span class="sxs-lookup"><span data-stu-id="e4674-140">Create a new table.</span></span>

   ```java
   public void createTable() {
        final String query = "CREATE TABLE IF NOT EXISTS uprofile.user (user_id int PRIMARY KEY, user_name text, user_bcity text)";
        session.execute(query);
        LOGGER.info("Created table 'user'");
   }
   ```

* <span data-ttu-id="e4674-141">Insert user entities using a prepared statement object.</span><span class="sxs-lookup"><span data-stu-id="e4674-141">Insert user entities using a prepared statement object.</span></span>

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

* <span data-ttu-id="e4674-142">Query to get all user information.</span><span class="sxs-lookup"><span data-stu-id="e4674-142">Query to get all user information.</span></span>

    ```java
   public void selectAllUsers() {
        final String query = "SELECT * FROM uprofile.user";
        List<Row> rows = session.execute(query).all();

        for (Row row : rows) {
            LOGGER.info("Obtained row: {} | {} | {} ", row.getInt("user_id"), row.getString("user_name"), row.getString("user_bcity"));
        }
    }
    ```

* <span data-ttu-id="e4674-143">Query to get a single user's information.</span><span class="sxs-lookup"><span data-stu-id="e4674-143">Query to get a single user's information.</span></span>

    ```java
    public void selectUser(int id) {
        final String query = "SELECT * FROM uprofile.user where user_id = 3";
        Row row = session.execute(query).one();

        LOGGER.info("Obtained row: {} | {} | {} ", row.getInt("user_id"), row.getString("user_name"), row.getString("user_bcity"));
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="e4674-144">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="e4674-144">Update your connection string</span></span>

<span data-ttu-id="e4674-145">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="e4674-145">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="e4674-146">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="e4674-146">This enables your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="e4674-147">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="e4674-147">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    ![View and copy a username from the Azure portal, Connection String page](./media/create-cassandra-java/keys.png)

2. <span data-ttu-id="e4674-149">Use the</span><span class="sxs-lookup"><span data-stu-id="e4674-149">Use the</span></span> ![Copy button](./media/create-cassandra-java/copy.png) <span data-ttu-id="e4674-151">button on the right side of the screen to copy the CONTACT POINT value.</span><span class="sxs-lookup"><span data-stu-id="e4674-151">button on the right side of the screen to copy the CONTACT POINT value.</span></span>

3. <span data-ttu-id="e4674-152">Open the `config.properties` file from C:\git-samples\azure-cosmosdb-cassandra-java-getting-started\java-examples\src\main\resources folder.</span><span class="sxs-lookup"><span data-stu-id="e4674-152">Open the `config.properties` file from C:\git-samples\azure-cosmosdb-cassandra-java-getting-started\java-examples\src\main\resources folder.</span></span> 

3. <span data-ttu-id="e4674-153">Paste the CONTACT POINT value from the portal over `<Cassandra endpoint host>` on line 2.</span><span class="sxs-lookup"><span data-stu-id="e4674-153">Paste the CONTACT POINT value from the portal over `<Cassandra endpoint host>` on line 2.</span></span>

    <span data-ttu-id="e4674-154">Line 2 of config.properties should now look similar to</span><span class="sxs-lookup"><span data-stu-id="e4674-154">Line 2 of config.properties should now look similar to</span></span> 

    `cassandra_host=cosmos-db-quickstarts.cassandra.cosmosdb.azure.com`

3. <span data-ttu-id="e4674-155">Go back to portal and copy the USERNAME value.</span><span class="sxs-lookup"><span data-stu-id="e4674-155">Go back to portal and copy the USERNAME value.</span></span> <span data-ttu-id="e4674-156">Past the USERNAME value from the portal over `<cassandra endpoint username>` on line 4.</span><span class="sxs-lookup"><span data-stu-id="e4674-156">Past the USERNAME value from the portal over `<cassandra endpoint username>` on line 4.</span></span>

    <span data-ttu-id="e4674-157">Line 4 of config.properties should now look similar to</span><span class="sxs-lookup"><span data-stu-id="e4674-157">Line 4 of config.properties should now look similar to</span></span> 

    `cassandra_username=cosmos-db-quickstart`

4. <span data-ttu-id="e4674-158">Go back to portal and copy the PASSWORD value.</span><span class="sxs-lookup"><span data-stu-id="e4674-158">Go back to portal and copy the PASSWORD value.</span></span> <span data-ttu-id="e4674-159">Paste the PASSWORD value from the portal over `<cassandra endpoint password>` on line 5.</span><span class="sxs-lookup"><span data-stu-id="e4674-159">Paste the PASSWORD value from the portal over `<cassandra endpoint password>` on line 5.</span></span>

    <span data-ttu-id="e4674-160">Line 5 of config.properties should now look similar to</span><span class="sxs-lookup"><span data-stu-id="e4674-160">Line 5 of config.properties should now look similar to</span></span> 

    `cassandra_password=2Ggkr662ifxz2Mg...==`

5. <span data-ttu-id="e4674-161">On line 6, if you want to use a specific SSL certificate, then replace `<SSL key store file location>` with the location of the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="e4674-161">On line 6, if you want to use a specific SSL certificate, then replace `<SSL key store file location>` with the location of the SSL certificate.</span></span> <span data-ttu-id="e4674-162">If a value is not provided, the JDK certificate installed at <JAVA_HOME>/jre/lib/security/cacerts is used.</span><span class="sxs-lookup"><span data-stu-id="e4674-162">If a value is not provided, the JDK certificate installed at <JAVA_HOME>/jre/lib/security/cacerts is used.</span></span> 

6. <span data-ttu-id="e4674-163">If you changed line 6 to use a specific SSL certificate, update line 7 to use the password for that certificate.</span><span class="sxs-lookup"><span data-stu-id="e4674-163">If you changed line 6 to use a specific SSL certificate, update line 7 to use the password for that certificate.</span></span> 

7. <span data-ttu-id="e4674-164">Save the config.properties file.</span><span class="sxs-lookup"><span data-stu-id="e4674-164">Save the config.properties file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="e4674-165">Run the app</span><span class="sxs-lookup"><span data-stu-id="e4674-165">Run the app</span></span>

1. <span data-ttu-id="e4674-166">In the git terminal window, `cd` to the azure-cosmosdb-cassandra-java-getting-started\java-examples folder.</span><span class="sxs-lookup"><span data-stu-id="e4674-166">In the git terminal window, `cd` to the azure-cosmosdb-cassandra-java-getting-started\java-examples folder.</span></span>

    ```git
    cd "C:\git-samples\azure-cosmosdb-cassandra-java-getting-started\java-examples"
    ```

2. <span data-ttu-id="e4674-167">In the git terminal window, use the following command to generate the cosmosdb-cassandra-examples.jar file.</span><span class="sxs-lookup"><span data-stu-id="e4674-167">In the git terminal window, use the following command to generate the cosmosdb-cassandra-examples.jar file.</span></span>

    ```git
    mvn clean install
    ```

3. <span data-ttu-id="e4674-168">In the git terminal window, run the following command to start the Java application.</span><span class="sxs-lookup"><span data-stu-id="e4674-168">In the git terminal window, run the following command to start the Java application.</span></span>

    ```git
    java -cp target/cosmosdb-cassandra-examples.jar com.azure.cosmosdb.cassandra.examples.UserProfile
    ```

    <span data-ttu-id="e4674-169">The terminal window displays notifications that the keyspace and table are created.</span><span class="sxs-lookup"><span data-stu-id="e4674-169">The terminal window displays notifications that the keyspace and table are created.</span></span> <span data-ttu-id="e4674-170">It then selects and returns all users in the table and displays the output, and then selects a row by id and displays the value.</span><span class="sxs-lookup"><span data-stu-id="e4674-170">It then selects and returns all users in the table and displays the output, and then selects a row by id and displays the value.</span></span>  

    <span data-ttu-id="e4674-171">Press CTRL + C to stop exection of the program and close the console window.</span><span class="sxs-lookup"><span data-stu-id="e4674-171">Press CTRL + C to stop exection of the program and close the console window.</span></span> 
    
    <span data-ttu-id="e4674-172">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="e4674-172">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span></span> 

    ![View the data in Data Explorer](./media/create-cassandra-java/data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="e4674-174">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4674-174">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e4674-175">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e4674-175">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="e4674-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4674-176">Next steps</span></span>

<span data-ttu-id="e4674-177">In this quickstart, you've learned how to create an Azure Cosmos DB account, Cassandra database, and container using the Data Explorer, and run an app to do the same thing programmatically.</span><span class="sxs-lookup"><span data-stu-id="e4674-177">In this quickstart, you've learned how to create an Azure Cosmos DB account, Cassandra database, and container using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="e4674-178">You can now import additional data into your Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="e4674-178">You can now import additional data into your Azure Cosmos DB container.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4674-179">Import Cassandra data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4674-179">Import Cassandra data into Azure Cosmos DB</span></span>](cassandra-import-data.md)
