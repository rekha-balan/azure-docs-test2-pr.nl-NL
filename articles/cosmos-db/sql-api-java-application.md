---
title: Java application development tutorial using Azure Cosmos DB | Microsoft Docs
description: This Java web application tutorial shows you how to use the Azure Cosmos DB and the SQL API to store and access data from a Java application hosted on Azure Websites.
keywords: Application development, database tutorial, java application, java web application tutorial, azure, Microsoft azure
services: cosmos-db
author: tknandu
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: java
ms.topic: tutorial
ms.date: 08/22/2017
ms.author: ramkris
ms.openlocfilehash: 17c856918b1c128ab5ece6ee45b9525ad0be900e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866060"
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-sql-api"></a><span data-ttu-id="55d29-104">Build a Java web application using Azure Cosmos DB and the SQL API</span><span class="sxs-lookup"><span data-stu-id="55d29-104">Build a Java web application using Azure Cosmos DB and the SQL API</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Java](sql-api-java-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Node.js- v2](sql-api-nodejs-application-preview.md)
> * [Python](sql-api-python-application.md)
> * [Xamarin](mobile-apps-with-xamarin.md)
> 

<span data-ttu-id="55d29-111">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="55d29-111">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="55d29-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="55d29-112">In this article, you will learn:</span></span>

* <span data-ttu-id="55d29-113">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="55d29-113">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="55d29-114">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="55d29-114">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="55d29-115">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="55d29-115">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="55d29-116">Each of the tasks in the ToDo list is stored as JSON documents in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="55d29-116">Each of the tasks in the ToDo list is stored as JSON documents in Azure Cosmos DB.</span></span>

![My ToDo List Java application](./media/sql-api-java-application/image1.png)

> [!TIP]
> This application development tutorial assumes that you have prior experience using Java. If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject). Once you have it built, you can review the article to gain insight on the code in the context of the project.  
> 
> 

## <a id="Prerequisites"></a><span data-ttu-id="55d29-121">Prerequisites for this Java web application tutorial</span><span class="sxs-lookup"><span data-stu-id="55d29-121">Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="55d29-122">Before you begin this application development tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="55d29-122">Before you begin this application development tutorial, you must have the following:</span></span>

*  <span data-ttu-id="55d29-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="55d29-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="55d29-124">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="55d29-124">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="55d29-125">Eclipse IDE for Java EE Developers.</span><span class="sxs-lookup"><span data-stu-id="55d29-125">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/release/luna/sr1/eclipse-ide-java-ee-developers)
* [<span data-ttu-id="55d29-126">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span><span class="sxs-lookup"><span data-stu-id="55d29-126">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service/app-service-web-get-started-java.md)

<span data-ttu-id="55d29-127">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span><span class="sxs-lookup"><span data-stu-id="55d29-127">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <a id="CreateDB"></a><span data-ttu-id="55d29-128">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="55d29-128">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="55d29-129">Let's start by creating an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="55d29-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="55d29-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="55d29-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a><span data-ttu-id="55d29-131">Step 2: Create the Java JSP application</span><span class="sxs-lookup"><span data-stu-id="55d29-131">Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="55d29-132">To create the JSP application:</span><span class="sxs-lookup"><span data-stu-id="55d29-132">To create the JSP application:</span></span>

1. <span data-ttu-id="55d29-133">First, we’ll start off by creating a Java project.</span><span class="sxs-lookup"><span data-stu-id="55d29-133">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="55d29-134">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span><span class="sxs-lookup"><span data-stu-id="55d29-134">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="55d29-135">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-135">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java Application Development](./media/sql-api-java-application/image10.png)
2. <span data-ttu-id="55d29-137">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="55d29-137">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="55d29-138">Selecting a target runtime enables you to run your project locally through Eclipse.</span><span class="sxs-lookup"><span data-stu-id="55d29-138">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="55d29-139">In Eclipse, in the Project Explorer view, expand your project.</span><span class="sxs-lookup"><span data-stu-id="55d29-139">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="55d29-140">Right-click **WebContent**, click **New**, and then click **JSP File**.</span><span class="sxs-lookup"><span data-stu-id="55d29-140">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="55d29-141">In the **New JSP File** dialog box, name the file **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="55d29-141">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="55d29-142">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-142">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Make a New JSP File - Java Web Application Tutorial](./media/sql-api-java-application/image11.png)
5. <span data-ttu-id="55d29-144">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="55d29-144">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="55d29-145">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="55d29-145">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="55d29-146">within the existing <body> element.</span><span class="sxs-lookup"><span data-stu-id="55d29-146">within the existing <body> element.</span></span> <span data-ttu-id="55d29-147">The updated <body> content should look like the following code:</span><span class="sxs-lookup"><span data-stu-id="55d29-147">The updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="55d29-148">Save the index.jsp file.</span><span class="sxs-lookup"><span data-stu-id="55d29-148">Save the index.jsp file.</span></span>
8. <span data-ttu-id="55d29-149">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span><span class="sxs-lookup"><span data-stu-id="55d29-149">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World – Java Application Tutorial](./media/sql-api-java-application/image12.png)

## <a id="InstallSDK"></a><span data-ttu-id="55d29-151">Step 3: Install the SQL Java SDK</span><span class="sxs-lookup"><span data-stu-id="55d29-151">Step 3: Install the SQL Java SDK</span></span>
<span data-ttu-id="55d29-152">The easiest way to pull in the SQL Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="55d29-152">The easiest way to pull in the SQL Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="55d29-153">To do this, you will need to convert your project to a maven project by completing the following steps:</span><span class="sxs-lookup"><span data-stu-id="55d29-153">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="55d29-154">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span><span class="sxs-lookup"><span data-stu-id="55d29-154">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="55d29-155">In the **Create new POM** window, accept the defaults, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="55d29-155">In the **Create new POM** window, accept the defaults, and click **Finish**.</span></span>
3. <span data-ttu-id="55d29-156">In **Project Explorer**, open the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="55d29-156">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="55d29-157">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="55d29-157">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="55d29-158">In the **Select Dependency** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="55d29-158">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="55d29-159">In the **Group Id** box, enter com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="55d29-159">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="55d29-160">In the **Artifact Id** box, enter azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="55d29-160">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="55d29-161">In the **Version** box, enter 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="55d29-161">In the **Version** box, enter 1.5.1.</span></span>
     
   ![Install SQL Java Application SDK](./media/sql-api-java-application/image13.png)
     
   * <span data-ttu-id="55d29-163">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span><span class="sxs-lookup"><span data-stu-id="55d29-163">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="55d29-164"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="55d29-164"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="55d29-165">Click **OK** and Maven will install the SQL Java SDK.</span><span class="sxs-lookup"><span data-stu-id="55d29-165">Click **OK** and Maven will install the SQL Java SDK.</span></span>
7. <span data-ttu-id="55d29-166">Save the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="55d29-166">Save the pom.xml file.</span></span>

## <a id="UseService"></a><span data-ttu-id="55d29-167">Step 4: Using the Azure Cosmos DB service in a Java application</span><span class="sxs-lookup"><span data-stu-id="55d29-167">Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="55d29-168">First, let's define the TodoItem object in TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="55d29-168">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="55d29-169">In this project, you are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span><span class="sxs-lookup"><span data-stu-id="55d29-169">In this project, you are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="55d29-170">Alternatively, you can write this code manually or have the IDE generate it.</span><span class="sxs-lookup"><span data-stu-id="55d29-170">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="55d29-171">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="55d29-171">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="55d29-172">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span><span class="sxs-lookup"><span data-stu-id="55d29-172">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="55d29-173">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="55d29-173">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="55d29-174">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="55d29-174">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="55d29-175">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span><span class="sxs-lookup"><span data-stu-id="55d29-175">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="55d29-176">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="55d29-176">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="55d29-177">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span><span class="sxs-lookup"><span data-stu-id="55d29-177">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="55d29-178">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span><span class="sxs-lookup"><span data-stu-id="55d29-178">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="55d29-179">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span><span class="sxs-lookup"><span data-stu-id="55d29-179">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="55d29-180">The next step is to write some code to persist the TodoItems into the collection.</span><span class="sxs-lookup"><span data-stu-id="55d29-180">The next step is to write some code to persist the TodoItems into the collection.</span></span> <span data-ttu-id="55d29-181">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span><span class="sxs-lookup"><span data-stu-id="55d29-181">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="55d29-182">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span><span class="sxs-lookup"><span data-stu-id="55d29-182">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="55d29-183">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span><span class="sxs-lookup"><span data-stu-id="55d29-183">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="55d29-184">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span><span class="sxs-lookup"><span data-stu-id="55d29-184">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="55d29-185">We can also use the DocumentClient to get a collection or list of TodoItems using SQL:</span><span class="sxs-lookup"><span data-stu-id="55d29-185">We can also use the DocumentClient to get a collection or list of TodoItems using SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="55d29-186">There are many ways to update a document with the DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="55d29-186">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="55d29-187">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span><span class="sxs-lookup"><span data-stu-id="55d29-187">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="55d29-188">This can be achieved by updating the "complete" attribute within the document:</span><span class="sxs-lookup"><span data-stu-id="55d29-188">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="55d29-189">Finally, we want the ability to delete a TodoItem from our list.</span><span class="sxs-lookup"><span data-stu-id="55d29-189">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="55d29-190">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span><span class="sxs-lookup"><span data-stu-id="55d29-190">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a><span data-ttu-id="55d29-191">Step 5: Wiring the rest of the of Java application development project together</span><span class="sxs-lookup"><span data-stu-id="55d29-191">Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="55d29-192">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span><span class="sxs-lookup"><span data-stu-id="55d29-192">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="55d29-193">First, let's start with building a controller to call our DAO:</span><span class="sxs-lookup"><span data-stu-id="55d29-193">First, let's start with building a controller to call our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="55d29-194">In a more complex application, the controller may house complicated business logic on top of the DAO.</span><span class="sxs-lookup"><span data-stu-id="55d29-194">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="55d29-195">Next, we'll create a servlet to route HTTP requests to the controller:</span><span class="sxs-lookup"><span data-stu-id="55d29-195">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="55d29-196">We'll need a web user interface to display to the user.</span><span class="sxs-lookup"><span data-stu-id="55d29-196">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="55d29-197">Let's re-write the index.jsp we created earlier:</span><span class="sxs-lookup"><span data-stu-id="55d29-197">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- The ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="55d29-198">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span><span class="sxs-lookup"><span data-stu-id="55d29-198">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api to update todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install the TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="55d29-199">Awesome!</span><span class="sxs-lookup"><span data-stu-id="55d29-199">Awesome!</span></span> <span data-ttu-id="55d29-200">Now all that's left is to test the application.</span><span class="sxs-lookup"><span data-stu-id="55d29-200">Now all that's left is to test the application.</span></span> <span data-ttu-id="55d29-201">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span><span class="sxs-lookup"><span data-stu-id="55d29-201">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="55d29-202">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span><span class="sxs-lookup"><span data-stu-id="55d29-202">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <a id="Deploy"></a><span data-ttu-id="55d29-203">Step 6: Deploy your Java application to Azure Web Sites</span><span class="sxs-lookup"><span data-stu-id="55d29-203">Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="55d29-204">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span><span class="sxs-lookup"><span data-stu-id="55d29-204">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="55d29-205">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span><span class="sxs-lookup"><span data-stu-id="55d29-205">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="55d29-206">In the **WAR Export** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="55d29-206">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="55d29-207">In the Web project box, enter azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="55d29-207">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="55d29-208">In the Destination box, choose a destination to save the WAR file.</span><span class="sxs-lookup"><span data-stu-id="55d29-208">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="55d29-209">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="55d29-209">Click **Finish**.</span></span>
3. <span data-ttu-id="55d29-210">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span><span class="sxs-lookup"><span data-stu-id="55d29-210">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="55d29-211">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="55d29-211">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="55d29-212">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span><span class="sxs-lookup"><span data-stu-id="55d29-212">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="55d29-213">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span><span class="sxs-lookup"><span data-stu-id="55d29-213">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <a id="GetProject"></a><span data-ttu-id="55d29-214">Get the project from GitHub</span><span class="sxs-lookup"><span data-stu-id="55d29-214">Get the project from GitHub</span></span>
<span data-ttu-id="55d29-215">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span><span class="sxs-lookup"><span data-stu-id="55d29-215">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="55d29-216">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span><span class="sxs-lookup"><span data-stu-id="55d29-216">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="55d29-217">Install [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="55d29-217">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="55d29-218">Lombok is used to generate constructors, getters, setters in the project.</span><span class="sxs-lookup"><span data-stu-id="55d29-218">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="55d29-219">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span><span class="sxs-lookup"><span data-stu-id="55d29-219">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="55d29-220">If Eclipse is open, close it and restart it to load Lombok.</span><span class="sxs-lookup"><span data-stu-id="55d29-220">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="55d29-221">In Eclipse, on the **File** menu, click **Import**.</span><span class="sxs-lookup"><span data-stu-id="55d29-221">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="55d29-222">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-222">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="55d29-223">On the **Select Repository Source** screen, click **Clone URI**.</span><span class="sxs-lookup"><span data-stu-id="55d29-223">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="55d29-224">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/documentdb-java-todo-app.git, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-224">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/documentdb-java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="55d29-225">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-225">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="55d29-226">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-226">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="55d29-227">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55d29-227">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="55d29-228">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="55d29-228">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="55d29-229">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span><span class="sxs-lookup"><span data-stu-id="55d29-229">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="55d29-230">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span><span class="sxs-lookup"><span data-stu-id="55d29-230">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="55d29-231">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="55d29-231">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="55d29-232">In **Project Explorer**, right-click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span><span class="sxs-lookup"><span data-stu-id="55d29-232">In **Project Explorer**, right-click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="55d29-233">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span><span class="sxs-lookup"><span data-stu-id="55d29-233">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="55d29-234">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="55d29-234">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="55d29-235">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span><span class="sxs-lookup"><span data-stu-id="55d29-235">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="55d29-236">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="55d29-236">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="55d29-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span><span class="sxs-lookup"><span data-stu-id="55d29-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="55d29-238">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="55d29-238">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="55d29-239">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span><span class="sxs-lookup"><span data-stu-id="55d29-239">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="55d29-240">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="55d29-240">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="55d29-241">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="55d29-241">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="55d29-242">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span><span class="sxs-lookup"><span data-stu-id="55d29-242">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="55d29-243">Note that if you changed your default port values, change 8080 to the value you selected.</span><span class="sxs-lookup"><span data-stu-id="55d29-243">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="55d29-244">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="55d29-244">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

