---
title: Connect Apache Spark to Azure Cosmos DB | Microsoft Docs
description: Learn about the Azure Cosmos DB Spark connector that enables you to connect Apache Spark to Azure Cosmos DB. You can perform distributed aggregations on the multi-tenant, globally distributed database system from Microsoft.
keywords: apache spark
services: cosmos-db
author: tknandu
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: ramkris
ms.openlocfilehash: 6d5ee59271f0c091a1d60504db594407e30641ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867241"
---
# <a name="accelerate-big-data-analytics-by-using-the-apache-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="d748e-105">Accelerate big data analytics by using the Apache Spark to Azure Cosmos DB connector</span><span class="sxs-lookup"><span data-stu-id="d748e-105">Accelerate big data analytics by using the Apache Spark to Azure Cosmos DB connector</span></span>
 
<span data-ttu-id="d748e-106">The Apache Spark to Azure Cosmos DB connector enables Azure Cosmos DB to be an input or output for Apache Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="d748e-106">The Apache Spark to Azure Cosmos DB connector enables Azure Cosmos DB to be an input or output for Apache Spark jobs.</span></span> <span data-ttu-id="d748e-107">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems.</span><span class="sxs-lookup"><span data-stu-id="d748e-107">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems.</span></span> <span data-ttu-id="d748e-108">You can use Azure Cosmos DB to quickly persist and query data.</span><span class="sxs-lookup"><span data-stu-id="d748e-108">You can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="d748e-109">The connector efficiently uses the native Azure Cosmos DB managed indexes.</span><span class="sxs-lookup"><span data-stu-id="d748e-109">The connector efficiently uses the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="d748e-110">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing, globally distributed data.</span><span class="sxs-lookup"><span data-stu-id="d748e-110">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing, globally distributed data.</span></span> <span data-ttu-id="d748e-111">This kind of data can range from Internet of Things (IoT) to data science and analytics scenarios.</span><span class="sxs-lookup"><span data-stu-id="d748e-111">This kind of data can range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

## <a name="connector-components"></a><span data-ttu-id="d748e-112">Connector components</span><span class="sxs-lookup"><span data-stu-id="d748e-112">Connector components</span></span>

<span data-ttu-id="d748e-113">The Spark to Azure Cosmos DB connector has the following components:</span><span class="sxs-lookup"><span data-stu-id="d748e-113">The Spark to Azure Cosmos DB connector has the following components:</span></span>

* <span data-ttu-id="d748e-114">[Azure Cosmos DB](http://documentdb.com) enables you to provision and elastically scale both throughput and storage, across any number of geographical regions.</span><span class="sxs-lookup"><span data-stu-id="d748e-114">[Azure Cosmos DB](http://documentdb.com) enables you to provision and elastically scale both throughput and storage, across any number of geographical regions.</span></span>  

* <span data-ttu-id="d748e-115">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine, built around speed, ease of use, and sophisticated analytics.</span><span class="sxs-lookup"><span data-stu-id="d748e-115">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine, built around speed, ease of use, and sophisticated analytics.</span></span>  

* <span data-ttu-id="d748e-116">[Apache Spark cluster on Azure Databricks](https://docs.azuredatabricks.net/getting-started/index.html) enables you to run Spark jobs on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="d748e-116">[Apache Spark cluster on Azure Databricks](https://docs.azuredatabricks.net/getting-started/index.html) enables you to run Spark jobs on the Spark cluster.</span></span>

## <a name="connect-apache-spark-to-azure-cosmos-db"></a><span data-ttu-id="d748e-117">Connect Apache Spark to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d748e-117">Connect Apache Spark to Azure Cosmos DB</span></span>

<span data-ttu-id="d748e-118">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d748e-118">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>

- <span data-ttu-id="d748e-119">[Azure Cosmos DB SQL Python SDK](https://github.com/Azure/azure-documentdb-python), a Python-based connector, which is also referred to as *pyDocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="d748e-119">[Azure Cosmos DB SQL Python SDK](https://github.com/Azure/azure-documentdb-python), a Python-based connector, which is also referred to as *pyDocumentDB*.</span></span>  

- <span data-ttu-id="d748e-120">[Azure Cosmos DB SQL Java SDK](https://github.com/Azure/azure-documentdb-java), a Java-based connector.</span><span class="sxs-lookup"><span data-stu-id="d748e-120">[Azure Cosmos DB SQL Java SDK](https://github.com/Azure/azure-documentdb-java), a Java-based connector.</span></span>


<span data-ttu-id="d748e-121">**Supported versions**</span><span class="sxs-lookup"><span data-stu-id="d748e-121">**Supported versions**</span></span>

| <span data-ttu-id="d748e-122">Component</span><span class="sxs-lookup"><span data-stu-id="d748e-122">Component</span></span> | <span data-ttu-id="d748e-123">Version</span><span class="sxs-lookup"><span data-stu-id="d748e-123">Version</span></span> |
|---------|-------|
|<span data-ttu-id="d748e-124">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="d748e-124">Apache Spark</span></span>| <span data-ttu-id="d748e-125">2.1.x, 2.2.x, 2.3.x</span><span class="sxs-lookup"><span data-stu-id="d748e-125">2.1.x, 2.2.x, 2.3.x</span></span> |
| <span data-ttu-id="d748e-126">Scala</span><span class="sxs-lookup"><span data-stu-id="d748e-126">Scala</span></span>|<span data-ttu-id="d748e-127">2.11</span><span class="sxs-lookup"><span data-stu-id="d748e-127">2.11</span></span>|
| <span data-ttu-id="d748e-128">Azure Databricks runtime version</span><span class="sxs-lookup"><span data-stu-id="d748e-128">Azure Databricks runtime version</span></span> | <span data-ttu-id="d748e-129">> 3.4</span><span class="sxs-lookup"><span data-stu-id="d748e-129">> 3.4</span></span> |
| <span data-ttu-id="d748e-130">Azure Cosmos DB SQL Java SDK</span><span class="sxs-lookup"><span data-stu-id="d748e-130">Azure Cosmos DB SQL Java SDK</span></span> | <span data-ttu-id="d748e-131">1.16.2</span><span class="sxs-lookup"><span data-stu-id="d748e-131">1.16.2</span></span> |

## <a name="connect-by-using-python-or-pydocumentdb-sdk"></a><span data-ttu-id="d748e-132">Connect by using Python or pyDocumentDB SDK</span><span class="sxs-lookup"><span data-stu-id="d748e-132">Connect by using Python or pyDocumentDB SDK</span></span>

<span data-ttu-id="d748e-133">The following diagram shows the architecture of the pyDocumentDB SDK implementation:</span><span class="sxs-lookup"><span data-stu-id="d748e-133">The following diagram shows the architecture of the pyDocumentDB SDK implementation:</span></span>

![Diagram of Spark to Azure Cosmos DB data flow via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow"></a><span data-ttu-id="d748e-135">Data flow</span><span class="sxs-lookup"><span data-stu-id="d748e-135">Data flow</span></span>

<span data-ttu-id="d748e-136">Data flow of the pyDocumentDB implementation is as follows:</span><span class="sxs-lookup"><span data-stu-id="d748e-136">Data flow of the pyDocumentDB implementation is as follows:</span></span>

* <span data-ttu-id="d748e-137">The master node of Spark connects to the Azure Cosmos DB gateway node through pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d748e-137">The master node of Spark connects to the Azure Cosmos DB gateway node through pyDocumentDB.</span></span> <span data-ttu-id="d748e-138">You specify the Spark and Azure Cosmos DB connections only.</span><span class="sxs-lookup"><span data-stu-id="d748e-138">You specify the Spark and Azure Cosmos DB connections only.</span></span> <span data-ttu-id="d748e-139">Connections to the respective master and gateway nodes are transparent.</span><span class="sxs-lookup"><span data-stu-id="d748e-139">Connections to the respective master and gateway nodes are transparent.</span></span>  

* <span data-ttu-id="d748e-140">The gateway node makes the query against Azure Cosmos DB, where the query subsequently runs against the collection's partitions in the data nodes.</span><span class="sxs-lookup"><span data-stu-id="d748e-140">The gateway node makes the query against Azure Cosmos DB, where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="d748e-141">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span><span class="sxs-lookup"><span data-stu-id="d748e-141">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>  

* <span data-ttu-id="d748e-142">Subsequent queries (for example, against a Spark data frame) are sent to the Spark worker nodes for processing.</span><span class="sxs-lookup"><span data-stu-id="d748e-142">Subsequent queries (for example, against a Spark data frame) are sent to the Spark worker nodes for processing.</span></span>  

<span data-ttu-id="d748e-143">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span><span class="sxs-lookup"><span data-stu-id="d748e-143">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span> <span data-ttu-id="d748e-144">The queries go as fast as the transport layer between these two nodes allows.</span><span class="sxs-lookup"><span data-stu-id="d748e-144">The queries go as fast as the transport layer between these two nodes allows.</span></span>

<span data-ttu-id="d748e-145">Run the following steps to connect Spark to Azure Cosmos DB by using pyDocumentDB SDK:</span><span class="sxs-lookup"><span data-stu-id="d748e-145">Run the following steps to connect Spark to Azure Cosmos DB by using pyDocumentDB SDK:</span></span>

1. <span data-ttu-id="d748e-146">Create an [Azure Databricks workspace](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-an-azure-databricks-workspace) and a [Spark cluster](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-a-spark-cluster-in-databricks).</span><span class="sxs-lookup"><span data-stu-id="d748e-146">Create an [Azure Databricks workspace](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-an-azure-databricks-workspace) and a [Spark cluster](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-a-spark-cluster-in-databricks).</span></span> <span data-ttu-id="d748e-147">Azure Databricks runtime version 4.0 includes Apache Spark 2.3.0 and Scala 2.11 within that workspace.</span><span class="sxs-lookup"><span data-stu-id="d748e-147">Azure Databricks runtime version 4.0 includes Apache Spark 2.3.0 and Scala 2.11 within that workspace.</span></span>  

2. <span data-ttu-id="d748e-148">When the cluster is created and is running, go to **Workspace** > **Create** > **Library**.</span><span class="sxs-lookup"><span data-stu-id="d748e-148">When the cluster is created and is running, go to **Workspace** > **Create** > **Library**.</span></span>  
3. <span data-ttu-id="d748e-149">From the New Library dialog box, choose **Upload Python Egg or PyPi** as the source.</span><span class="sxs-lookup"><span data-stu-id="d748e-149">From the New Library dialog box, choose **Upload Python Egg or PyPi** as the source.</span></span> <span data-ttu-id="d748e-150">Provide **pydocumentdb** as the name, and select **Install Library**.</span><span class="sxs-lookup"><span data-stu-id="d748e-150">Provide **pydocumentdb** as the name, and select **Install Library**.</span></span> <span data-ttu-id="d748e-151">pyDocumentdb SDK is already published to the pip packages, so you can find and install it.</span><span class="sxs-lookup"><span data-stu-id="d748e-151">pyDocumentdb SDK is already published to the pip packages, so you can find and install it.</span></span> 

   ![Screenshot of the New Library dialog box](./media/spark-connector/create-library.png)

4. <span data-ttu-id="d748e-153">After the library is installed, attach it to the cluster you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d748e-153">After the library is installed, attach it to the cluster you created earlier.</span></span>  

5. <span data-ttu-id="d748e-154">Go to **Workspace** > **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d748e-154">Go to **Workspace** > **Create** > **Notebook**.</span></span>  

6. <span data-ttu-id="d748e-155">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Python** as the language.</span><span class="sxs-lookup"><span data-stu-id="d748e-155">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Python** as the language.</span></span> <span data-ttu-id="d748e-156">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d748e-156">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span></span>  

7. <span data-ttu-id="d748e-157">Run a few Spark queries by using the flights sample data hosted in the "doctorwho" Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d748e-157">Run a few Spark queries by using the flights sample data hosted in the "doctorwho" Azure Cosmos DB account.</span></span> <span data-ttu-id="d748e-158">(This account is publicly accessible.) The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span><span class="sxs-lookup"><span data-stu-id="d748e-158">(This account is publicly accessible.) The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span></span> <span data-ttu-id="d748e-159">Download the repository files, and go to `\samples\Documentation_Samples\Read_Batch_PyDocumentDB.html`.</span><span class="sxs-lookup"><span data-stu-id="d748e-159">Download the repository files, and go to `\samples\Documentation_Samples\Read_Batch_PyDocumentDB.html`.</span></span> <span data-ttu-id="d748e-160">You can import the notebook to your Azure Databricks account and run it.</span><span class="sxs-lookup"><span data-stu-id="d748e-160">You can import the notebook to your Azure Databricks account and run it.</span></span> <span data-ttu-id="d748e-161">The following section explains the functionality of the code blocks in detail.</span><span class="sxs-lookup"><span data-stu-id="d748e-161">The following section explains the functionality of the code blocks in detail.</span></span>

<span data-ttu-id="d748e-162">The following code snippet shows how to import the pyDocumentDB SDK, and run a query in the Spark context.</span><span class="sxs-lookup"><span data-stu-id="d748e-162">The following code snippet shows how to import the pyDocumentDB SDK, and run a query in the Spark context.</span></span> <span data-ttu-id="d748e-163">As noted in the code snippet, the pyDocumentDB SDK contains the connection parameters required to connect to the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d748e-163">As noted in the code snippet, the pyDocumentDB SDK contains the connection parameters required to connect to the Azure Cosmos DB account.</span></span> <span data-ttu-id="d748e-164">It imports the required libraries, and configures the master key and host, to create the Azure Cosmos DB client (pydocumentdb.document_client).</span><span class="sxs-lookup"><span data-stu-id="d748e-164">It imports the required libraries, and configures the master key and host, to create the Azure Cosmos DB client (pydocumentdb.document_client).</span></span>


```python
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]

# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)

```

<span data-ttu-id="d748e-165">Next, you can run queries.</span><span class="sxs-lookup"><span data-stu-id="d748e-165">Next, you can run queries.</span></span> <span data-ttu-id="d748e-166">The following code snippet connects to the airports.codes collection in the doctorwho account, and runs a query to extract the airport cities in Washington state.</span><span class="sxs-lookup"><span data-stu-id="d748e-166">The following code snippet connects to the airports.codes collection in the doctorwho account, and runs a query to extract the airport cities in Washington state.</span></span> 

```python
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

```

<span data-ttu-id="d748e-167">After you run the query, the result is a "query_iterable.QueryIterable" that is converted to a Python list.</span><span class="sxs-lookup"><span data-stu-id="d748e-167">After you run the query, the result is a "query_iterable.QueryIterable" that is converted to a Python list.</span></span> <span data-ttu-id="d748e-168">This list, in turn, is converted to a Spark data frame.</span><span class="sxs-lookup"><span data-stu-id="d748e-168">This list, in turn, is converted to a Spark data frame.</span></span> 

```python
# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(list(query))

# Show data
df.show()
```

### <a name="considerations-when-using-pydocumentdb-sdk"></a><span data-ttu-id="d748e-169">Considerations when using pyDocumentDB SDK</span><span class="sxs-lookup"><span data-stu-id="d748e-169">Considerations when using pyDocumentDB SDK</span></span>
<span data-ttu-id="d748e-170">Connecting Spark to Azure Cosmos DB by using pyDocumentDB SDK is recommended in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="d748e-170">Connecting Spark to Azure Cosmos DB by using pyDocumentDB SDK is recommended in the following scenarios:</span></span>

* <span data-ttu-id="d748e-171">You want to use Python.</span><span class="sxs-lookup"><span data-stu-id="d748e-171">You want to use Python.</span></span>  

* <span data-ttu-id="d748e-172">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span><span class="sxs-lookup"><span data-stu-id="d748e-172">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="d748e-173">Note that the underlying dataset in Azure Cosmos DB can be quite large, and you are applying filters or running predicate filters against your Azure Cosmos DB source.</span><span class="sxs-lookup"><span data-stu-id="d748e-173">Note that the underlying dataset in Azure Cosmos DB can be quite large, and you are applying filters or running predicate filters against your Azure Cosmos DB source.</span></span>

## <a name="connect-by-using-the-java-sdk"></a><span data-ttu-id="d748e-174">Connect by using the Java SDK</span><span class="sxs-lookup"><span data-stu-id="d748e-174">Connect by using the Java SDK</span></span>

<span data-ttu-id="d748e-175">The following diagram shows the architecture of Azure Cosmos DB SQL Java SDK implementation, and data moves between the Spark worker nodes:</span><span class="sxs-lookup"><span data-stu-id="d748e-175">The following diagram shows the architecture of Azure Cosmos DB SQL Java SDK implementation, and data moves between the Spark worker nodes:</span></span>

![Diagram of data flow in the Spark to Azure Cosmos DB connector](./media/spark-connector/spark-connector.png)

### <a name="data-flow"></a><span data-ttu-id="d748e-177">Data flow</span><span class="sxs-lookup"><span data-stu-id="d748e-177">Data flow</span></span>

<span data-ttu-id="d748e-178">The data flow of the Java SDK implementation is as follows:</span><span class="sxs-lookup"><span data-stu-id="d748e-178">The data flow of the Java SDK implementation is as follows:</span></span>

* <span data-ttu-id="d748e-179">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span><span class="sxs-lookup"><span data-stu-id="d748e-179">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="d748e-180">You specify only the Spark and Azure Cosmos DB connections.</span><span class="sxs-lookup"><span data-stu-id="d748e-180">You specify only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d748e-181">Connections to the respective master and gateway nodes are transparent.</span><span class="sxs-lookup"><span data-stu-id="d748e-181">Connections to the respective master and gateway nodes are transparent.</span></span>  

* <span data-ttu-id="d748e-182">This information is provided back to the Spark master node.</span><span class="sxs-lookup"><span data-stu-id="d748e-182">This information is provided back to the Spark master node.</span></span> <span data-ttu-id="d748e-183">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span><span class="sxs-lookup"><span data-stu-id="d748e-183">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>  

* <span data-ttu-id="d748e-184">This information is transmitted to the Spark worker nodes.</span><span class="sxs-lookup"><span data-stu-id="d748e-184">This information is transmitted to the Spark worker nodes.</span></span>  

* <span data-ttu-id="d748e-185">The Spark worker nodes connect to the Azure Cosmos DB partitions directly, to extract and return the data to the Spark partitions in the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="d748e-185">The Spark worker nodes connect to the Azure Cosmos DB partitions directly, to extract and return the data to the Spark partitions in the worker nodes.</span></span>  

<span data-ttu-id="d748e-186">Communication between Spark and Azure Cosmos DB is significantly faster, because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span><span class="sxs-lookup"><span data-stu-id="d748e-186">Communication between Spark and Azure Cosmos DB is significantly faster, because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span> <span data-ttu-id="d748e-187">In this example, you send some sample Twitter data to the Azure Cosmos DB account, and run Spark queries by using that data.</span><span class="sxs-lookup"><span data-stu-id="d748e-187">In this example, you send some sample Twitter data to the Azure Cosmos DB account, and run Spark queries by using that data.</span></span> <span data-ttu-id="d748e-188">Use the following steps to write sample Twitter data to Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d748e-188">Use the following steps to write sample Twitter data to Azure Cosmos DB:</span></span>

1. <span data-ttu-id="d748e-189">Create an [Azure Cosmos DB SQL API account](create-sql-api-dotnet.md#create-a-database-account) and [add a collection](create-sql-api-dotnet.md#add-a-collection) to the account.</span><span class="sxs-lookup"><span data-stu-id="d748e-189">Create an [Azure Cosmos DB SQL API account](create-sql-api-dotnet.md#create-a-database-account) and [add a collection](create-sql-api-dotnet.md#add-a-collection) to the account.</span></span>  

2. <span data-ttu-id="d748e-190">Download the [TwitterCosmosDBFeed](https://github.com/tknandu/TwitterCosmosDBFeed) sample from GitHub.</span><span class="sxs-lookup"><span data-stu-id="d748e-190">Download the [TwitterCosmosDBFeed](https://github.com/tknandu/TwitterCosmosDBFeed) sample from GitHub.</span></span> <span data-ttu-id="d748e-191">You use this feed to write sample Twitter data to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-191">You use this feed to write sample Twitter data to Azure Cosmos DB.</span></span>  

3. <span data-ttu-id="d748e-192">Open a command prompt, and install Tweepy and pyDocumentdb modules by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="d748e-192">Open a command prompt, and install Tweepy and pyDocumentdb modules by running the following commands:</span></span>

   ```bash
   pip install tweepy==3.3.0
   pip install pyDocumentDB
   ```

4. <span data-ttu-id="d748e-193">Extract the contents of the Twitter feed sample and open the config.py file.</span><span class="sxs-lookup"><span data-stu-id="d748e-193">Extract the contents of the Twitter feed sample and open the config.py file.</span></span> <span data-ttu-id="d748e-194">Update the masterKey, host, databaseId, collectionId, and preferredLocations values.</span><span class="sxs-lookup"><span data-stu-id="d748e-194">Update the masterKey, host, databaseId, collectionId, and preferredLocations values.</span></span>  

5. <span data-ttu-id="d748e-195">Go to `http://apps.twitter.com/`, and register the Twitter feed script as a new application.</span><span class="sxs-lookup"><span data-stu-id="d748e-195">Go to `http://apps.twitter.com/`, and register the Twitter feed script as a new application.</span></span> <span data-ttu-id="d748e-196">After choosing a name and application for your app, you will be provided with a **consumer key, consumer secret, access token and access token secret**.</span><span class="sxs-lookup"><span data-stu-id="d748e-196">After choosing a name and application for your app, you will be provided with a **consumer key, consumer secret, access token and access token secret**.</span></span> <span data-ttu-id="d748e-197">Copy these values and update them in config.py file to provide the application programmatic access to Twitter.</span><span class="sxs-lookup"><span data-stu-id="d748e-197">Copy these values and update them in config.py file to provide the application programmatic access to Twitter.</span></span>   

6. <span data-ttu-id="d748e-198">Save the config.py file.</span><span class="sxs-lookup"><span data-stu-id="d748e-198">Save the config.py file.</span></span> <span data-ttu-id="d748e-199">Open a command prompt, and run the Python application by using the following command:</span><span class="sxs-lookup"><span data-stu-id="d748e-199">Open a command prompt, and run the Python application by using the following command:</span></span>

   ```bash
   Python driver.py
   ```

7. <span data-ttu-id="d748e-200">Go to the Azure Cosmos DB collection in the portal, and verify that the Twitter data is written to the collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-200">Go to the Azure Cosmos DB collection in the portal, and verify that the Twitter data is written to the collection.</span></span>

### <a name="find-and-attach-the-java-sdk-to-the-spark-cluster"></a><span data-ttu-id="d748e-201">Find and attach the Java SDK to the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="d748e-201">Find and attach the Java SDK to the Spark cluster</span></span>

1. <span data-ttu-id="d748e-202">Create an [Azure Databricks workspace](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-an-azure-databricks-workspace) and a [Spark cluster](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-a-spark-cluster-in-databricks).</span><span class="sxs-lookup"><span data-stu-id="d748e-202">Create an [Azure Databricks workspace](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-an-azure-databricks-workspace) and a [Spark cluster](../azure-databricks/quickstart-create-databricks-workspace-portal.md#create-a-spark-cluster-in-databricks).</span></span> <span data-ttu-id="d748e-203">Azure Databricks runtime version 4.0 includes Apache Spark 2.3.0 and Scala 2.11 within that workspace.</span><span class="sxs-lookup"><span data-stu-id="d748e-203">Azure Databricks runtime version 4.0 includes Apache Spark 2.3.0 and Scala 2.11 within that workspace.</span></span>  

2. <span data-ttu-id="d748e-204">When the cluster is created and is running, go to **Workspace** > **Create** > **Library**.</span><span class="sxs-lookup"><span data-stu-id="d748e-204">When the cluster is created and is running, go to **Workspace** > **Create** > **Library**.</span></span>  

3. <span data-ttu-id="d748e-205">From the **New Library** dialog box, choose **Maven Coordinate** as the source.</span><span class="sxs-lookup"><span data-stu-id="d748e-205">From the **New Library** dialog box, choose **Maven Coordinate** as the source.</span></span> <span data-ttu-id="d748e-206">Provide the coordinate value **com.microsoft.azure:azure-cosmosdb-spark_2.3.0_2.11:1.2.0**, and select **Create Library**.</span><span class="sxs-lookup"><span data-stu-id="d748e-206">Provide the coordinate value **com.microsoft.azure:azure-cosmosdb-spark_2.3.0_2.11:1.2.0**, and select **Create Library**.</span></span> <span data-ttu-id="d748e-207">The Maven dependencies are resolved, and the package is added to your workspace.</span><span class="sxs-lookup"><span data-stu-id="d748e-207">The Maven dependencies are resolved, and the package is added to your workspace.</span></span> <span data-ttu-id="d748e-208">In the preceding Maven coordinate format, 2.3.0 represents the Spark version, 2.11 represents the Scala version, and 1.2.0 represents the Azure Cosmos DB connector version.</span><span class="sxs-lookup"><span data-stu-id="d748e-208">In the preceding Maven coordinate format, 2.3.0 represents the Spark version, 2.11 represents the Scala version, and 1.2.0 represents the Azure Cosmos DB connector version.</span></span> 

4. <span data-ttu-id="d748e-209">After the library is installed, attach it to the cluster you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d748e-209">After the library is installed, attach it to the cluster you created earlier.</span></span> 

<span data-ttu-id="d748e-210">This article demonstrates the use of the Spark connector Java SDK in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="d748e-210">This article demonstrates the use of the Spark connector Java SDK in the following scenarios:</span></span>

* <span data-ttu-id="d748e-211">Read Twitter data from Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-211">Read Twitter data from Azure Cosmos DB.</span></span>  

* <span data-ttu-id="d748e-212">Read Twitter data that is streaming to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-212">Read Twitter data that is streaming to Azure Cosmos DB.</span></span>  

* <span data-ttu-id="d748e-213">Write Twitter data to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-213">Write Twitter data to Azure Cosmos DB.</span></span> 

### <a name="read-twitter-data-from-azure-cosmos-db"></a><span data-ttu-id="d748e-214">Read Twitter data from Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d748e-214">Read Twitter data from Azure Cosmos DB</span></span>
 
<span data-ttu-id="d748e-215">In this section, you run Spark queries to read a batch of Twitter data from Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-215">In this section, you run Spark queries to read a batch of Twitter data from Azure Cosmos DB.</span></span> <span data-ttu-id="d748e-216">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span><span class="sxs-lookup"><span data-stu-id="d748e-216">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span></span> <span data-ttu-id="d748e-217">Download the repository files and go to `\samples\Documentation_Samples\Read_Batch_Twitter_Data.html`.</span><span class="sxs-lookup"><span data-stu-id="d748e-217">Download the repository files and go to `\samples\Documentation_Samples\Read_Batch_Twitter_Data.html`.</span></span> <span data-ttu-id="d748e-218">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span><span class="sxs-lookup"><span data-stu-id="d748e-218">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span></span> <span data-ttu-id="d748e-219">You can run the notebook, or create it as follows:</span><span class="sxs-lookup"><span data-stu-id="d748e-219">You can run the notebook, or create it as follows:</span></span>

1. <span data-ttu-id="d748e-220">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d748e-220">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span></span> 

2. <span data-ttu-id="d748e-221">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Python** as the language.</span><span class="sxs-lookup"><span data-stu-id="d748e-221">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Python** as the language.</span></span> <span data-ttu-id="d748e-222">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d748e-222">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span></span>  

3. <span data-ttu-id="d748e-223">Update the endpoint, master key, database, and collection values to connect to the account.</span><span class="sxs-lookup"><span data-stu-id="d748e-223">Update the endpoint, master key, database, and collection values to connect to the account.</span></span> <span data-ttu-id="d748e-224">Read tweets by using the spark.read.format() command.</span><span class="sxs-lookup"><span data-stu-id="d748e-224">Read tweets by using the spark.read.format() command.</span></span>

   ```python
   # Configuration Map
   tweetsConfig = {
   "Endpoint" : "<Your Azure Cosmos DB endpoint>",
   "Masterkey" : "<Primary key of your Azure Cosmos DB account>",
   "Database" : "<Your Azure Cosmos DB database name>",
   "Collection" : "<Your Azure Cosmos DB collection name>", 
   "preferredRegions" : "East US",
   "SamplingRatio" : "1.0",
   "schema_samplesize" : "200000",
   "query_custom" : "SELECT c.id, c.created_at, c.user.screen_name, c.user.lang, c.user.location, c.text, c.retweet_count, c.entities.hashtags, c.entities.user_mentions, c.favorited, c.source FROM c"
   }
   # Read Tweets
   tweets = spark.read.format("com.microsoft.azure.cosmosdb.spark").options(**tweetsConfig).load()
   tweets.createOrReplaceTempView("tweets")
   #tweets.cache()

   ```

4. <span data-ttu-id="d748e-225">Run the query to get the count of tweets by different hashtags from the cached data.</span><span class="sxs-lookup"><span data-stu-id="d748e-225">Run the query to get the count of tweets by different hashtags from the cached data.</span></span> 

   ```python
   %sql
   select hashtags.text, count(distinct id) as tweets
   from (
   select 
     explode(hashtags) as hashtags,
     id
   from tweets
   ) a
   group by hashtags.text
   order by tweets desc
   limit 10
   ```

<span data-ttu-id="d748e-226">Java SDK supports the following values for configuration mapping:</span><span class="sxs-lookup"><span data-stu-id="d748e-226">Java SDK supports the following values for configuration mapping:</span></span> 

|<span data-ttu-id="d748e-227">Setting</span><span class="sxs-lookup"><span data-stu-id="d748e-227">Setting</span></span>  |<span data-ttu-id="d748e-228">Description</span><span class="sxs-lookup"><span data-stu-id="d748e-228">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d748e-229">query_maxdegreeofparallelism</span><span class="sxs-lookup"><span data-stu-id="d748e-229">query_maxdegreeofparallelism</span></span>  | <span data-ttu-id="d748e-230">Sets the number of concurrent operations run at the client side during parallel query execution.</span><span class="sxs-lookup"><span data-stu-id="d748e-230">Sets the number of concurrent operations run at the client side during parallel query execution.</span></span> <span data-ttu-id="d748e-231">If it is set to a value that is greater than 0, it limits the number of concurrent operations to the assigned value.</span><span class="sxs-lookup"><span data-stu-id="d748e-231">If it is set to a value that is greater than 0, it limits the number of concurrent operations to the assigned value.</span></span> <span data-ttu-id="d748e-232">If it is set to less than 0, the system automatically decides the number of concurrent operations to run.</span><span class="sxs-lookup"><span data-stu-id="d748e-232">If it is set to less than 0, the system automatically decides the number of concurrent operations to run.</span></span> <span data-ttu-id="d748e-233">As the connector maps each collection partition with an executor, this value won't have any effect on the reading operation.</span><span class="sxs-lookup"><span data-stu-id="d748e-233">As the connector maps each collection partition with an executor, this value won't have any effect on the reading operation.</span></span>        |
|<span data-ttu-id="d748e-234">query_maxbuffereditemcount</span><span class="sxs-lookup"><span data-stu-id="d748e-234">query_maxbuffereditemcount</span></span>     |    <span data-ttu-id="d748e-235">Sets the maximum number of items that can be buffered at the client side during parallel query execution.</span><span class="sxs-lookup"><span data-stu-id="d748e-235">Sets the maximum number of items that can be buffered at the client side during parallel query execution.</span></span> <span data-ttu-id="d748e-236">If it is set to a value that is greater than 0, it limits the number of buffered items to the assigned value.</span><span class="sxs-lookup"><span data-stu-id="d748e-236">If it is set to a value that is greater than 0, it limits the number of buffered items to the assigned value.</span></span> <span data-ttu-id="d748e-237">If it is set to less than 0, the system automatically decides the number of items to buffer.</span><span class="sxs-lookup"><span data-stu-id="d748e-237">If it is set to less than 0, the system automatically decides the number of items to buffer.</span></span>     |
|<span data-ttu-id="d748e-238">query_enablescan</span><span class="sxs-lookup"><span data-stu-id="d748e-238">query_enablescan</span></span>    |   <span data-ttu-id="d748e-239">Sets the option to enable scans on the queries that couldn't be served because indexing was opted out on the requested paths.</span><span class="sxs-lookup"><span data-stu-id="d748e-239">Sets the option to enable scans on the queries that couldn't be served because indexing was opted out on the requested paths.</span></span>       |
|<span data-ttu-id="d748e-240">query_disableruperminuteusage</span><span class="sxs-lookup"><span data-stu-id="d748e-240">query_disableruperminuteusage</span></span>  |  <span data-ttu-id="d748e-241">Disables request units (RUs)/minute capacity to serve the query, if regular provisioned RUs/second is exhausted.</span><span class="sxs-lookup"><span data-stu-id="d748e-241">Disables request units (RUs)/minute capacity to serve the query, if regular provisioned RUs/second is exhausted.</span></span>       |
|<span data-ttu-id="d748e-242">query_emitverbosetraces</span><span class="sxs-lookup"><span data-stu-id="d748e-242">query_emitverbosetraces</span></span>   |   <span data-ttu-id="d748e-243">Sets the option to allow queries to emit out verbose traces for investigation.</span><span class="sxs-lookup"><span data-stu-id="d748e-243">Sets the option to allow queries to emit out verbose traces for investigation.</span></span>      |
|<span data-ttu-id="d748e-244">query_pagesize</span><span class="sxs-lookup"><span data-stu-id="d748e-244">query_pagesize</span></span>  |   <span data-ttu-id="d748e-245">Sets the size of the query result page for each query request.</span><span class="sxs-lookup"><span data-stu-id="d748e-245">Sets the size of the query result page for each query request.</span></span> <span data-ttu-id="d748e-246">To optimize throughput, use a large page size to reduce the number of round trips to fetch results.</span><span class="sxs-lookup"><span data-stu-id="d748e-246">To optimize throughput, use a large page size to reduce the number of round trips to fetch results.</span></span>      |
|<span data-ttu-id="d748e-247">query_custom</span><span class="sxs-lookup"><span data-stu-id="d748e-247">query_custom</span></span>  |  <span data-ttu-id="d748e-248">Sets the Azure Cosmos DB query to override the default query when fetching data from Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-248">Sets the Azure Cosmos DB query to override the default query when fetching data from Azure Cosmos DB.</span></span> <span data-ttu-id="d748e-249">Note that when you provide this value, it is used in place of a query with pushed down predicates as well.</span><span class="sxs-lookup"><span data-stu-id="d748e-249">Note that when you provide this value, it is used in place of a query with pushed down predicates as well.</span></span>     |

<span data-ttu-id="d748e-250">Depending on the scenario, you should use different configuration values to optimize the performance and throughput.</span><span class="sxs-lookup"><span data-stu-id="d748e-250">Depending on the scenario, you should use different configuration values to optimize the performance and throughput.</span></span> <span data-ttu-id="d748e-251">Note that the configuration key is currently case-insensitive, and the configuration value is always a string.</span><span class="sxs-lookup"><span data-stu-id="d748e-251">Note that the configuration key is currently case-insensitive, and the configuration value is always a string.</span></span>

### <a name="read-twitter-data-that-is-streaming-to-azure-cosmos-db"></a><span data-ttu-id="d748e-252">Read Twitter data that is streaming to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d748e-252">Read Twitter data that is streaming to Azure Cosmos DB</span></span>

<span data-ttu-id="d748e-253">In this section, you run Spark queries to read a change feed of streaming Twitter data.</span><span class="sxs-lookup"><span data-stu-id="d748e-253">In this section, you run Spark queries to read a change feed of streaming Twitter data.</span></span> <span data-ttu-id="d748e-254">While you run the queries in this section, make sure that your Twitter feed app is running and pumping data to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-254">While you run the queries in this section, make sure that your Twitter feed app is running and pumping data to Azure Cosmos DB.</span></span> <span data-ttu-id="d748e-255">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span><span class="sxs-lookup"><span data-stu-id="d748e-255">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span></span> <span data-ttu-id="d748e-256">Download the repository files, and go to `\samples\Documentation_Samples\Read_Stream_Twitter_Data.html`.</span><span class="sxs-lookup"><span data-stu-id="d748e-256">Download the repository files, and go to `\samples\Documentation_Samples\Read_Stream_Twitter_Data.html`.</span></span> <span data-ttu-id="d748e-257">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span><span class="sxs-lookup"><span data-stu-id="d748e-257">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span></span> <span data-ttu-id="d748e-258">You can run the notebook, or create it as follows:</span><span class="sxs-lookup"><span data-stu-id="d748e-258">You can run the notebook, or create it as follows:</span></span>

1. <span data-ttu-id="d748e-259">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d748e-259">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span></span>  

2. <span data-ttu-id="d748e-260">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Scala** as the language.</span><span class="sxs-lookup"><span data-stu-id="d748e-260">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Scala** as the language.</span></span> <span data-ttu-id="d748e-261">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d748e-261">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span></span>  

3. <span data-ttu-id="d748e-262">Update the endpoint, master key, database, and collection values to connect to the account.</span><span class="sxs-lookup"><span data-stu-id="d748e-262">Update the endpoint, master key, database, and collection values to connect to the account.</span></span>

   ```scala
   // This script does the following:
   // - creates a structured stream from a Twitter feed CosmosDB collection (on top of change feed)
   // - get the count of tweets
   import com.microsoft.azure.cosmosdb.spark._
   import com.microsoft.azure.cosmosdb.spark.schema._
   import com.microsoft.azure.cosmosdb.spark.config.Config
   import org.codehaus.jackson.map.ObjectMapper
   import com.microsoft.azure.cosmosdb.spark.streaming._
   import java.time._

   val sourceConfigMap = Map(
   "Endpoint" -> "<Your Azure Cosmos DB endpoint>",
   "Masterkey" -> "<Primary key of your Azure Cosmos DB account>",
   "Database" -> "<Your Azure Cosmos DB database name>",
   "Collection" -> "<Your Azure Cosmos DB collection name>", 
   "ConnectionMode" -> "Gateway",
   "ChangeFeedCheckpointLocation" -> "/tmp",
   "changefeedqueryname" -> "Streaming Query from Cosmos DB Change Feed Internal Count")
   ```
4. <span data-ttu-id="d748e-263">Start reading the change feed as a stream by using the spark.readStream.format() command:</span><span class="sxs-lookup"><span data-stu-id="d748e-263">Start reading the change feed as a stream by using the spark.readStream.format() command:</span></span>

   ```scala
   var streamData = spark.readStream.format(classOf[CosmosDBSourceProvider].getName).options(sourceConfigMap).load()
   ```
5. <span data-ttu-id="d748e-264">Start streaming the query to your console:</span><span class="sxs-lookup"><span data-stu-id="d748e-264">Start streaming the query to your console:</span></span>

   ```scala
   //**RUN THE ABOVE FIRST AND KEEP BELOW IN SEPARATE CELL
   val query = streamData.withColumn("countcol", streamData.col("id").substr(0,0)).groupBy("countcol").count().writeStream.outputMode("complete").format("console").start()
   ```

<span data-ttu-id="d748e-265">Java SDK supports the following values for configuration mapping:</span><span class="sxs-lookup"><span data-stu-id="d748e-265">Java SDK supports the following values for configuration mapping:</span></span>

|<span data-ttu-id="d748e-266">Setting</span><span class="sxs-lookup"><span data-stu-id="d748e-266">Setting</span></span>  |<span data-ttu-id="d748e-267">Description</span><span class="sxs-lookup"><span data-stu-id="d748e-267">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d748e-268">readchangefeed</span><span class="sxs-lookup"><span data-stu-id="d748e-268">readchangefeed</span></span>   |  <span data-ttu-id="d748e-269">Indicates that the collection content is fetched from CosmosDB Change Feed.</span><span class="sxs-lookup"><span data-stu-id="d748e-269">Indicates that the collection content is fetched from CosmosDB Change Feed.</span></span> <span data-ttu-id="d748e-270">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="d748e-270">The default value is false.</span></span>       |
|<span data-ttu-id="d748e-271">changefeedqueryname</span><span class="sxs-lookup"><span data-stu-id="d748e-271">changefeedqueryname</span></span> |   <span data-ttu-id="d748e-272">A custom string to identify the query.</span><span class="sxs-lookup"><span data-stu-id="d748e-272">A custom string to identify the query.</span></span> <span data-ttu-id="d748e-273">The connector keeps track of the collection continuation tokens for different change feed queries separately.</span><span class="sxs-lookup"><span data-stu-id="d748e-273">The connector keeps track of the collection continuation tokens for different change feed queries separately.</span></span> <span data-ttu-id="d748e-274">If readchangefeed is true, this is a required configuration that cannot take empty value.</span><span class="sxs-lookup"><span data-stu-id="d748e-274">If readchangefeed is true, this is a required configuration that cannot take empty value.</span></span>      |
|<span data-ttu-id="d748e-275">changefeedcheckpointlocation</span><span class="sxs-lookup"><span data-stu-id="d748e-275">changefeedcheckpointlocation</span></span>  |   <span data-ttu-id="d748e-276">A path to local file storage to persist continuation tokens in case of node failures.</span><span class="sxs-lookup"><span data-stu-id="d748e-276">A path to local file storage to persist continuation tokens in case of node failures.</span></span>      |
|<span data-ttu-id="d748e-277">changefeedstartfromthebeginning</span><span class="sxs-lookup"><span data-stu-id="d748e-277">changefeedstartfromthebeginning</span></span>  |  <span data-ttu-id="d748e-278">Sets whether change feed should start from the beginning (true) or from the current point (false).</span><span class="sxs-lookup"><span data-stu-id="d748e-278">Sets whether change feed should start from the beginning (true) or from the current point (false).</span></span> <span data-ttu-id="d748e-279">By default, it starts from the current (false).</span><span class="sxs-lookup"><span data-stu-id="d748e-279">By default, it starts from the current (false).</span></span>       |
|<span data-ttu-id="d748e-280">rollingchangefeed</span><span class="sxs-lookup"><span data-stu-id="d748e-280">rollingchangefeed</span></span>  |   <span data-ttu-id="d748e-281">A Boolean value indicating whether the change feed should be from the last query.</span><span class="sxs-lookup"><span data-stu-id="d748e-281">A Boolean value indicating whether the change feed should be from the last query.</span></span> <span data-ttu-id="d748e-282">The default value is false, which means the changes are counted from the first read of the collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-282">The default value is false, which means the changes are counted from the first read of the collection.</span></span>      |
|<span data-ttu-id="d748e-283">changefeedusenexttoken</span><span class="sxs-lookup"><span data-stu-id="d748e-283">changefeedusenexttoken</span></span>  |   <span data-ttu-id="d748e-284">A Boolean value to support processing failure scenarios.</span><span class="sxs-lookup"><span data-stu-id="d748e-284">A Boolean value to support processing failure scenarios.</span></span> <span data-ttu-id="d748e-285">It indicates that the current change feed batch has been handled gracefully.</span><span class="sxs-lookup"><span data-stu-id="d748e-285">It indicates that the current change feed batch has been handled gracefully.</span></span> <span data-ttu-id="d748e-286">The Resiliant Distributed Dataset should use the next continuation tokens to get the subsequent batch of changes.</span><span class="sxs-lookup"><span data-stu-id="d748e-286">The Resiliant Distributed Dataset should use the next continuation tokens to get the subsequent batch of changes.</span></span>      |
| <span data-ttu-id="d748e-287">InferStreamSchema</span><span class="sxs-lookup"><span data-stu-id="d748e-287">InferStreamSchema</span></span> | <span data-ttu-id="d748e-288">A Boolean value that indicates whether the schema of the streaming data should be sampled at the start of streaming.</span><span class="sxs-lookup"><span data-stu-id="d748e-288">A Boolean value that indicates whether the schema of the streaming data should be sampled at the start of streaming.</span></span> <span data-ttu-id="d748e-289">By default, this value is set to true.</span><span class="sxs-lookup"><span data-stu-id="d748e-289">By default, this value is set to true.</span></span> <span data-ttu-id="d748e-290">If this parameter is set to true and the streaming data’s schema changes after the data is sampled, newly added properties will be dropped in the streaming data frame.</span><span class="sxs-lookup"><span data-stu-id="d748e-290">If this parameter is set to true and the streaming data’s schema changes after the data is sampled, newly added properties will be dropped in the streaming data frame.</span></span> <br/><br/> <span data-ttu-id="d748e-291">If you want the streaming data frame to be schema agnostic, set this parameter to false.</span><span class="sxs-lookup"><span data-stu-id="d748e-291">If you want the streaming data frame to be schema agnostic, set this parameter to false.</span></span> <span data-ttu-id="d748e-292">In this mode, the body of the documents read from the Azure Cosmos DB change feed are wrapped into a body property.</span><span class="sxs-lookup"><span data-stu-id="d748e-292">In this mode, the body of the documents read from the Azure Cosmos DB change feed are wrapped into a body property.</span></span> <span data-ttu-id="d748e-293">This property is in the resultant streaming data frame, aside from system property values.</span><span class="sxs-lookup"><span data-stu-id="d748e-293">This property is in the resultant streaming data frame, aside from system property values.</span></span>
 |

### <a name="connection-settings"></a><span data-ttu-id="d748e-294">Connection settings</span><span class="sxs-lookup"><span data-stu-id="d748e-294">Connection settings</span></span>

<span data-ttu-id="d748e-295">Java SDK supports the following connection settings:</span><span class="sxs-lookup"><span data-stu-id="d748e-295">Java SDK supports the following connection settings:</span></span>

|<span data-ttu-id="d748e-296">Setting</span><span class="sxs-lookup"><span data-stu-id="d748e-296">Setting</span></span>  |<span data-ttu-id="d748e-297">Description</span><span class="sxs-lookup"><span data-stu-id="d748e-297">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d748e-298">connectionmode</span><span class="sxs-lookup"><span data-stu-id="d748e-298">connectionmode</span></span>   |  <span data-ttu-id="d748e-299">Sets the connection mode that the internal DocumentClient should use to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-299">Sets the connection mode that the internal DocumentClient should use to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="d748e-300">Allowed values are **DirectHttps** (default value) and **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d748e-300">Allowed values are **DirectHttps** (default value) and **Gateway**.</span></span> <span data-ttu-id="d748e-301">The DirectHttps connection mode routes the requests directly to the CosmosDB partitions and provides some latency advantage.</span><span class="sxs-lookup"><span data-stu-id="d748e-301">The DirectHttps connection mode routes the requests directly to the CosmosDB partitions and provides some latency advantage.</span></span>       |
|<span data-ttu-id="d748e-302">connectionmaxpoolsize</span><span class="sxs-lookup"><span data-stu-id="d748e-302">connectionmaxpoolsize</span></span>   |  <span data-ttu-id="d748e-303">Sets the value of connection pool size that is used by internal DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="d748e-303">Sets the value of connection pool size that is used by internal DocumentClient.</span></span> <span data-ttu-id="d748e-304">The default value is 100.</span><span class="sxs-lookup"><span data-stu-id="d748e-304">The default value is 100.</span></span>       |
|<span data-ttu-id="d748e-305">connectionidletimeout</span><span class="sxs-lookup"><span data-stu-id="d748e-305">connectionidletimeout</span></span>  |  <span data-ttu-id="d748e-306">Sets the timeout value, in seconds, for idle connections.</span><span class="sxs-lookup"><span data-stu-id="d748e-306">Sets the timeout value, in seconds, for idle connections.</span></span> <span data-ttu-id="d748e-307">The default value is 60.</span><span class="sxs-lookup"><span data-stu-id="d748e-307">The default value is 60.</span></span>       |
|<span data-ttu-id="d748e-308">query_maxretryattemptsonthrottledrequests</span><span class="sxs-lookup"><span data-stu-id="d748e-308">query_maxretryattemptsonthrottledrequests</span></span>    |  <span data-ttu-id="d748e-309">Sets the maximum number of retries.</span><span class="sxs-lookup"><span data-stu-id="d748e-309">Sets the maximum number of retries.</span></span> <span data-ttu-id="d748e-310">You use this value in case of a request failure due to rate limiting on the client.</span><span class="sxs-lookup"><span data-stu-id="d748e-310">You use this value in case of a request failure due to rate limiting on the client.</span></span> <span data-ttu-id="d748e-311">If it's not specified, the default value is 1000 retry attempts.</span><span class="sxs-lookup"><span data-stu-id="d748e-311">If it's not specified, the default value is 1000 retry attempts.</span></span>       |
|<span data-ttu-id="d748e-312">query_maxretrywaittimeinseconds</span><span class="sxs-lookup"><span data-stu-id="d748e-312">query_maxretrywaittimeinseconds</span></span>   |  <span data-ttu-id="d748e-313">Sets the maximum retry time in seconds.</span><span class="sxs-lookup"><span data-stu-id="d748e-313">Sets the maximum retry time in seconds.</span></span> <span data-ttu-id="d748e-314">By default, it is 1000 seconds.</span><span class="sxs-lookup"><span data-stu-id="d748e-314">By default, it is 1000 seconds.</span></span>       |

### <a name="write-twitter-data-to-azure-cosmos-db"></a><span data-ttu-id="d748e-315">Write Twitter data to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d748e-315">Write Twitter data to Azure Cosmos DB</span></span> 

<span data-ttu-id="d748e-316">In this section, you run Spark queries to write a batch of Twitter data to a new collection in the same database.</span><span class="sxs-lookup"><span data-stu-id="d748e-316">In this section, you run Spark queries to write a batch of Twitter data to a new collection in the same database.</span></span> <span data-ttu-id="d748e-317">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span><span class="sxs-lookup"><span data-stu-id="d748e-317">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span></span> <span data-ttu-id="d748e-318">Download the repository files, and go to `\samples\Documentation_Samples\Write_Batch_Twitter_Data.html`.</span><span class="sxs-lookup"><span data-stu-id="d748e-318">Download the repository files, and go to `\samples\Documentation_Samples\Write_Batch_Twitter_Data.html`.</span></span> <span data-ttu-id="d748e-319">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span><span class="sxs-lookup"><span data-stu-id="d748e-319">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span></span> <span data-ttu-id="d748e-320">You can run the notebook, or create it as follows:</span><span class="sxs-lookup"><span data-stu-id="d748e-320">You can run the notebook, or create it as follows:</span></span>

1. <span data-ttu-id="d748e-321">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d748e-321">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span></span>  

2. <span data-ttu-id="d748e-322">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Scala** as the language.</span><span class="sxs-lookup"><span data-stu-id="d748e-322">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Scala** as the language.</span></span> <span data-ttu-id="d748e-323">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d748e-323">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span></span>  

3. <span data-ttu-id="d748e-324">Update the endpoint, master key, database, and collection values to connect to the database collection to read and write Twitter data.</span><span class="sxs-lookup"><span data-stu-id="d748e-324">Update the endpoint, master key, database, and collection values to connect to the database collection to read and write Twitter data.</span></span>

   ```scala
   %scala
   // Import Necessary Libraries
   import org.joda.time._
   import org.joda.time.format._
   import com.microsoft.azure.cosmosdb.spark.schema._
   import com.microsoft.azure.cosmosdb.spark._
   import com.microsoft.azure.cosmosdb.spark.config.Config

   // Maps
   val readConfigMap = Map(
   "Endpoint" -> "<Your Azure Cosmos DB endpoint>",
   "Masterkey" -> "<Primary key of your Azure Cosmos DB account>",
   "Database" -> "<Your Azure Cosmos DB database name>",
   "Collection" -> "<Your Azure Cosmos DB source collection name>", 
   "preferredRegions" -> "East US",
   "SamplingRatio" -> "1.0",
   "schema_samplesize" -> "200000",
   "query_custom" -> "SELECT c.id, c.created_at, c.user.screen_name, c.user.location, c.text, c.retweet_count, c.entities.hashtags, c.entities.user_mentions, c.favorited, c.source FROM c"
   )
   val writeConfigMap = Map(
   "Endpoint" -> "<Your Azure Cosmos DB endpoint>",
   "Masterkey" -> "<Primary key of your Azure Cosmos DB account>",
   "Database" -> "<Your Azure Cosmos DB database name>",
   "Collection" -> "<Your Azure Cosmos DB destination collection name>", 
   "preferredRegions" -> "East US",
   "SamplingRatio" -> "1.0",
   "schema_samplesize" -> "200000"
   ) 

   // Configs
   // get read
   val readConfig = Config(readConfigMap)
   val tweets = spark.read.cosmosDB(readConfig)
   tweets.createOrReplaceTempView("tweets")
   tweets.cache()

   // get write
   val writeConfig = Config(writeConfigMap)
   ```
4. <span data-ttu-id="d748e-325">Run the query to get the count of tweets by different hashtags from the cached data.</span><span class="sxs-lookup"><span data-stu-id="d748e-325">Run the query to get the count of tweets by different hashtags from the cached data.</span></span> 

   ```scala
   %sql
   select hashtags.text, count(distinct id) as tweets
   from (
   select 
     explode(hashtags) as hashtags,
     id
   from tweets
   ) a
   group by hashtags.text
   order by tweets desc
   limit 10
   ```

5. <span data-ttu-id="d748e-326">Create a new data frame of tweets tags, and save the data to the new collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-326">Create a new data frame of tweets tags, and save the data to the new collection.</span></span> <span data-ttu-id="d748e-327">After running the following code, you can go back to portal and verify that the data is written to the collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-327">After running the following code, you can go back to portal and verify that the data is written to the collection.</span></span> 

   ```scala
   %scala
   // Import SaveMode so you can Overwrite, Append, ErrorIfExists, Ignore
   import org.apache.spark.sql.{Row, SaveMode, SparkSession}

   // Create new DataFrame of tweets tags
   val tweets_bytags = spark.sql("select '2018-06-12' as currdt, hashtags.text as hashtags, count(distinct id) as tweets from ( select explode(hashtags) as hashtags, id from tweets ) a group by hashtags.text order by tweets desc limit 10")

   // Save to Cosmos DB (using Append in this case)
   // Ensure the baseConfig contains a Read-Write Key
   // The key provided in our examples is a Read-Only Key

   tweets_bytags.write.mode(SaveMode.Overwrite).cosmosDB(writeConfig)
   ```

<span data-ttu-id="d748e-328">Java SDK supports the following values for configuration mapping:</span><span class="sxs-lookup"><span data-stu-id="d748e-328">Java SDK supports the following values for configuration mapping:</span></span>

|<span data-ttu-id="d748e-329">Setting</span><span class="sxs-lookup"><span data-stu-id="d748e-329">Setting</span></span>  |<span data-ttu-id="d748e-330">Description</span><span class="sxs-lookup"><span data-stu-id="d748e-330">Description</span></span>  |
|---------|---------|
| <span data-ttu-id="d748e-331">BulkImport</span><span class="sxs-lookup"><span data-stu-id="d748e-331">BulkImport</span></span> | <span data-ttu-id="d748e-332">A Boolean value that indicates whether data should be imported by using the BulkExecutor library.</span><span class="sxs-lookup"><span data-stu-id="d748e-332">A Boolean value that indicates whether data should be imported by using the BulkExecutor library.</span></span> <span data-ttu-id="d748e-333">By default, this value is set to true.</span><span class="sxs-lookup"><span data-stu-id="d748e-333">By default, this value is set to true.</span></span> |
|<span data-ttu-id="d748e-334">WritingBatchSize</span><span class="sxs-lookup"><span data-stu-id="d748e-334">WritingBatchSize</span></span>  |   <span data-ttu-id="d748e-335">Indicates the batch size to use when you are writing data to Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-335">Indicates the batch size to use when you are writing data to Azure Cosmos DB collection.</span></span> <br/><br/> <span data-ttu-id="d748e-336">If BulkImport parameter is set to true, then WritingBatchSize parameter indicates the batch size of documents supplied as input to the importAll API of the BulkExecutor library.</span><span class="sxs-lookup"><span data-stu-id="d748e-336">If BulkImport parameter is set to true, then WritingBatchSize parameter indicates the batch size of documents supplied as input to the importAll API of the BulkExecutor library.</span></span> <span data-ttu-id="d748e-337">By default, this value is set to 100K.</span><span class="sxs-lookup"><span data-stu-id="d748e-337">By default, this value is set to 100K.</span></span> <br/><br/> <span data-ttu-id="d748e-338">If BulkImport parameter is set to false, then WritingBatchSize parameter indicates the batch size to use when you are writing to the Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-338">If BulkImport parameter is set to false, then WritingBatchSize parameter indicates the batch size to use when you are writing to the Azure Cosmos DB collection.</span></span> <span data-ttu-id="d748e-339">The connector sends createDocument and upsertDocument requests asynchronously in batch.</span><span class="sxs-lookup"><span data-stu-id="d748e-339">The connector sends createDocument and upsertDocument requests asynchronously in batch.</span></span> <span data-ttu-id="d748e-340">The larger the batch size, the more throughput you can achieve, as long as the cluster resources are available.</span><span class="sxs-lookup"><span data-stu-id="d748e-340">The larger the batch size, the more throughput you can achieve, as long as the cluster resources are available.</span></span> <span data-ttu-id="d748e-341">On the other hand, specify a smaller number batch size to limit the rate and RU consumption.</span><span class="sxs-lookup"><span data-stu-id="d748e-341">On the other hand, specify a smaller number batch size to limit the rate and RU consumption.</span></span> <span data-ttu-id="d748e-342">By default, writing batch size is set to 500.</span><span class="sxs-lookup"><span data-stu-id="d748e-342">By default, writing batch size is set to 500.</span></span>  |
|<span data-ttu-id="d748e-343">Upsert</span><span class="sxs-lookup"><span data-stu-id="d748e-343">Upsert</span></span>   |  <span data-ttu-id="d748e-344">A Boolean value string indicating whether to use upsertDocument instead of CreateDocument when you are writing to the Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-344">A Boolean value string indicating whether to use upsertDocument instead of CreateDocument when you are writing to the Azure Cosmos DB collection.</span></span>   |
| <span data-ttu-id="d748e-345">WriteThroughputBudget</span><span class="sxs-lookup"><span data-stu-id="d748e-345">WriteThroughputBudget</span></span> |  <span data-ttu-id="d748e-346">An integer string that represents the number of RU\s that you want to allocate to the bulk ingestion Spark job, out of the total throughput allocated to the collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-346">An integer string that represents the number of RU\s that you want to allocate to the bulk ingestion Spark job, out of the total throughput allocated to the collection.</span></span> |


### <a name="write-twitter-data-that-is-streaming-to-azure-cosmos-db"></a><span data-ttu-id="d748e-347">Write Twitter data that is streaming to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d748e-347">Write Twitter data that is streaming to Azure Cosmos DB</span></span> 

<span data-ttu-id="d748e-348">In this section, you run Spark queries to write a change feed of streaming Twitter data to a new collection in the same database.</span><span class="sxs-lookup"><span data-stu-id="d748e-348">In this section, you run Spark queries to write a change feed of streaming Twitter data to a new collection in the same database.</span></span> <span data-ttu-id="d748e-349">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span><span class="sxs-lookup"><span data-stu-id="d748e-349">The [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/tree/master) GitHub repository hosts the HTML version of the notebook.</span></span> <span data-ttu-id="d748e-350">Download the repository files, and go to `\samples\Documentation_Samples\Write_Stream_Twitter_Data.html`.</span><span class="sxs-lookup"><span data-stu-id="d748e-350">Download the repository files, and go to `\samples\Documentation_Samples\Write_Stream_Twitter_Data.html`.</span></span> <span data-ttu-id="d748e-351">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span><span class="sxs-lookup"><span data-stu-id="d748e-351">You can import the notebook to your Azure Databricks account, and update the account URI, master key, database, and collection names.</span></span> <span data-ttu-id="d748e-352">You can run the notebook, or create it as follows:</span><span class="sxs-lookup"><span data-stu-id="d748e-352">You can run the notebook, or create it as follows:</span></span>

1. <span data-ttu-id="d748e-353">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d748e-353">Go to your Azure Databricks account, and select **Workspace** > **Create** > **Notebook**.</span></span>  

2. <span data-ttu-id="d748e-354">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Scala** as the language.</span><span class="sxs-lookup"><span data-stu-id="d748e-354">In the **Create Notebook** dialog box, enter a user-friendly name, and choose **Scala** as the language.</span></span> <span data-ttu-id="d748e-355">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d748e-355">From the drop-down list, select the cluster that you created earlier, and select **Create**.</span></span>  

3. <span data-ttu-id="d748e-356">Update the endpoint, master key, database, and collection values to connect to the database collection to read and write Twitter data.</span><span class="sxs-lookup"><span data-stu-id="d748e-356">Update the endpoint, master key, database, and collection values to connect to the database collection to read and write Twitter data.</span></span>

   ```scala
   import com.microsoft.azure.cosmosdb.spark._
   import com.microsoft.azure.cosmosdb.spark.schema._
   import com.microsoft.azure.cosmosdb.spark.config.Config
   import com.microsoft.azure.cosmosdb.spark.streaming._

   // Configure connection to Azure Cosmos DB Change Feed (Trades)
   val ConfigMap = Map(
   // Account settings
   "Endpoint" -> "<Your Azure Cosmos DB endpoint>",
   "Masterkey" -> "<Primary key of your Azure Cosmos DB account>",
   "Database" -> "<Your Azure Cosmos DB database name>",
   "Collection" -> "<Your Azure Cosmos DB source collection name>", 
   // Change feed settings
   "ReadChangeFeed" -> "true",
   "ChangeFeedStartFromTheBeginning" -> "true",
   "ChangeFeedCheckpointLocation" -> "dbfs:/cosmos-feed",
   "ChangeFeedQueryName" -> "Structured Stream Read",
   "InferStreamSchema" -> "true"
   )
   ```
4. <span data-ttu-id="d748e-357">Start reading the change feed as a stream by using the spark.readStream.format() command:</span><span class="sxs-lookup"><span data-stu-id="d748e-357">Start reading the change feed as a stream by using the spark.readStream.format() command:</span></span>
 
   ```scala
   // Start reading change feed of trades as a stream
   var streamdata = spark
     .readStream
     .format(classOf[CosmosDBSourceProvider].getName)
     .options(ConfigMap)
     .load()
   ```

5. <span data-ttu-id="d748e-358">Define the configuration of the destination collection, and start the streaming job by using writeStream.format() method:</span><span class="sxs-lookup"><span data-stu-id="d748e-358">Define the configuration of the destination collection, and start the streaming job by using writeStream.format() method:</span></span>

   ```scala
   val sinkConfigMap = Map(
   "Endpoint" -> "<Your Azure Cosmos DB endpoint>",
   "Masterkey" -> "<Primary key of your Azure Cosmos DB account>",
   "Database" -> "<Your Azure Cosmos DB database name>",
   "Collection" -> "<Your Azure Cosmos DB destination collection name>", 
   "checkpointLocation" -> "streamingcheckpointlocation6",
   "WritingBatchSize" -> "100",
   "Upsert" -> "true")

   // Start the stream writer
   val streamingQueryWriter = streamdata
    .writeStream
    .format(classOf[CosmosDBSinkProvider].getName)
    .outputMode("append")
    .options(sinkConfigMap)
    .start()
    ```

<span data-ttu-id="d748e-359">Java SDK supports the following values for configuration mapping:</span><span class="sxs-lookup"><span data-stu-id="d748e-359">Java SDK supports the following values for configuration mapping:</span></span>

|<span data-ttu-id="d748e-360">Setting</span><span class="sxs-lookup"><span data-stu-id="d748e-360">Setting</span></span>  |<span data-ttu-id="d748e-361">Description</span><span class="sxs-lookup"><span data-stu-id="d748e-361">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d748e-362">Upsert</span><span class="sxs-lookup"><span data-stu-id="d748e-362">Upsert</span></span>   |  <span data-ttu-id="d748e-363">A Boolean value string indicating whether to use upsertDocument instead of CreateDocument when you are writing to the Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-363">A Boolean value string indicating whether to use upsertDocument instead of CreateDocument when you are writing to the Azure Cosmos DB collection.</span></span>   |
|<span data-ttu-id="d748e-364">checkpointlocation</span><span class="sxs-lookup"><span data-stu-id="d748e-364">checkpointlocation</span></span>  |   <span data-ttu-id="d748e-365">A path to local file storage to persist continuation tokens in case of node failures.</span><span class="sxs-lookup"><span data-stu-id="d748e-365">A path to local file storage to persist continuation tokens in case of node failures.</span></span>   |
|<span data-ttu-id="d748e-366">WritingBatchSize</span><span class="sxs-lookup"><span data-stu-id="d748e-366">WritingBatchSize</span></span>  |  <span data-ttu-id="d748e-367">Indicates the batch size to use when writing data to the Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="d748e-367">Indicates the batch size to use when writing data to the Azure Cosmos DB collection.</span></span> <span data-ttu-id="d748e-368">The connector sends createDocument and upsertDocument requests asynchronously in batch.</span><span class="sxs-lookup"><span data-stu-id="d748e-368">The connector sends createDocument and upsertDocument requests asynchronously in batch.</span></span> <span data-ttu-id="d748e-369">The larger the batch size, the more throughput you can achieve, as long as the cluster resources are available.</span><span class="sxs-lookup"><span data-stu-id="d748e-369">The larger the batch size, the more throughput you can achieve, as long as the cluster resources are available.</span></span> <span data-ttu-id="d748e-370">On the other hand, specify a smaller number batch size to limit the rate and RU consumption.</span><span class="sxs-lookup"><span data-stu-id="d748e-370">On the other hand, specify a smaller number batch size to limit the rate and RU consumption.</span></span> <span data-ttu-id="d748e-371">By default, writing batch size is set to 500.</span><span class="sxs-lookup"><span data-stu-id="d748e-371">By default, writing batch size is set to 500.</span></span>  |


### <a name="considerations-when-using-java-sdk"></a><span data-ttu-id="d748e-372">Considerations when using Java SDK</span><span class="sxs-lookup"><span data-stu-id="d748e-372">Considerations when using Java SDK</span></span>

<span data-ttu-id="d748e-373">Connecting Spark to Azure Cosmos DB by using Java SDK is recommended in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="d748e-373">Connecting Spark to Azure Cosmos DB by using Java SDK is recommended in the following scenarios:</span></span>

* <span data-ttu-id="d748e-374">You want to use Python or Scala.</span><span class="sxs-lookup"><span data-stu-id="d748e-374">You want to use Python or Scala.</span></span>  

* <span data-ttu-id="d748e-375">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d748e-375">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span> <span data-ttu-id="d748e-376">The Java SDK performs better than the pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d748e-376">The Java SDK performs better than the pyDocumentDB.</span></span> <span data-ttu-id="d748e-377">For more information about the query performance difference, see the [Query test runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="d748e-377">For more information about the query performance difference, see the [Query test runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d748e-378">Next steps</span><span class="sxs-lookup"><span data-stu-id="d748e-378">Next steps</span></span>

<span data-ttu-id="d748e-379">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="d748e-379">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository.</span></span> <span data-ttu-id="d748e-380">Explore the following additional resources in the repo:</span><span class="sxs-lookup"><span data-stu-id="d748e-380">Explore the following additional resources in the repo:</span></span>

* [<span data-ttu-id="d748e-381">Aggregations examples</span><span class="sxs-lookup"><span data-stu-id="d748e-381">Aggregations examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="d748e-382">Sample scripts and notebooks</span><span class="sxs-lookup"><span data-stu-id="d748e-382">Sample scripts and notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="d748e-383">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html), and the [Apache Spark on Azure HDInsight](../hdinsight/spark/apache-spark-jupyter-spark-sql.md) article.</span><span class="sxs-lookup"><span data-stu-id="d748e-383">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html), and the [Apache Spark on Azure HDInsight](../hdinsight/spark/apache-spark-jupyter-spark-sql.md) article.</span></span>
