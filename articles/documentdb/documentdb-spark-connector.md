---
title: Connecting Apache Spark to Azure DocumentDB | Microsoft Docs
description: Use this tutorial to learn about the Azure DocumentDB Spark connector that enables you to connect Apache Spark to Azure DocumentDB to perform distributed aggregations and data sciences on Microsoft's multi-tenant globally distributed database system designed for the cloud.
keywords: apache spark
services: documentdb
documentationcenter: ''
author: dennyglee
manager: jhubbard
editor: ''
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: denlee
ms.openlocfilehash: 8c129e3e88d878d37508e0e427112cc654293639
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554930"
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-documentdb-connector"></a><span data-ttu-id="fdc73-104">Accelerate real-time big-data analytics with the Spark to DocumentDB connector</span><span class="sxs-lookup"><span data-stu-id="fdc73-104">Accelerate real-time big-data analytics with the Spark to DocumentDB connector</span></span>

<span data-ttu-id="fdc73-105">The Spark to DocumentDB connector enables Azure DocumentDB to act as an input source or output sink for Apache Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="fdc73-105">The Spark to DocumentDB connector enables Azure DocumentDB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="fdc73-106">Connecting [Spark](http://spark.apache.org/) to [DocumentDB](https://azure.microsoft.com/services/documentdb/) accelerates your ability to solve fast-moving data science problems, where data can be quickly persisted and queried using DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fdc73-106">Connecting [Spark](http://spark.apache.org/) to [DocumentDB](https://azure.microsoft.com/services/documentdb/) accelerates your ability to solve fast-moving data science problems, where data can be quickly persisted and queried using DocumentDB.</span></span> <span data-ttu-id="fdc73-107">The Spark to DocumentDB connector efficiently utilizes the native DocumentDB managed indexes and enables updateable columns when performing analytics, push-down predicate filtering against fast-changing globally distributed data, ranging from IoT, data science, and analytics scenarios.</span><span class="sxs-lookup"><span data-stu-id="fdc73-107">The Spark to DocumentDB connector efficiently utilizes the native DocumentDB managed indexes and enables updateable columns when performing analytics, push-down predicate filtering against fast-changing globally distributed data, ranging from IoT, data science, and analytics scenarios.</span></span> 

## <a name="download"></a><span data-ttu-id="fdc73-108">Download</span><span class="sxs-lookup"><span data-stu-id="fdc73-108">Download</span></span>

<span data-ttu-id="fdc73-109">Get started by downloading the Spark to DocumentDB connector (preview) from the [azure-documentdb-spark](https://github.com/Azure/azure-documentdb-spark/) repo on GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdc73-109">Get started by downloading the Spark to DocumentDB connector (preview) from the [azure-documentdb-spark](https://github.com/Azure/azure-documentdb-spark/) repo on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="fdc73-110">Connector components</span><span class="sxs-lookup"><span data-stu-id="fdc73-110">Connector components</span></span>

<span data-ttu-id="fdc73-111">The connector utilizes the following components:</span><span class="sxs-lookup"><span data-stu-id="fdc73-111">The connector utilizes the following components:</span></span>

* <span data-ttu-id="fdc73-112">[DocumentDB](http://documentdb.com), Microsoft’s multi-tenant, [globally distributed database system](documentdb-distribute-data-globally.md) designed for the cloud.</span><span class="sxs-lookup"><span data-stu-id="fdc73-112">[DocumentDB](http://documentdb.com), Microsoft’s multi-tenant, [globally distributed database system](documentdb-distribute-data-globally.md) designed for the cloud.</span></span> <span data-ttu-id="fdc73-113">DocumentDB enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span><span class="sxs-lookup"><span data-stu-id="fdc73-113">DocumentDB enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="fdc73-114">The service offers guaranteed low latency at the 99th percentile, a guaranteed 99.99% high availability, and [multiple well-defined consistency models](documentdb-consistency-levels.md) to developers.</span><span class="sxs-lookup"><span data-stu-id="fdc73-114">The service offers guaranteed low latency at the 99th percentile, a guaranteed 99.99% high availability, and [multiple well-defined consistency models](documentdb-consistency-levels.md) to developers.</span></span>

* <span data-ttu-id="fdc73-115">[Apache Spark](http://spark.apache.org/), which is a powerful open source processing engine built around speed, ease of use, and sophisticated analytics.</span><span class="sxs-lookup"><span data-stu-id="fdc73-115">[Apache Spark](http://spark.apache.org/), which is a powerful open source processing engine built around speed, ease of use, and sophisticated analytics.</span></span> 

* <span data-ttu-id="fdc73-116">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="fdc73-116">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="fdc73-117">You can deploy Apache Spark in the cloud for mission critical deployments using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="fdc73-117">You can deploy Apache Spark in the cloud for mission critical deployments using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="fdc73-118">Officially supported versions:</span><span class="sxs-lookup"><span data-stu-id="fdc73-118">Officially supported versions:</span></span>

| <span data-ttu-id="fdc73-119">Component</span><span class="sxs-lookup"><span data-stu-id="fdc73-119">Component</span></span> | <span data-ttu-id="fdc73-120">Version</span><span class="sxs-lookup"><span data-stu-id="fdc73-120">Version</span></span> |
|---------|-------|
|<span data-ttu-id="fdc73-121">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="fdc73-121">Apache Spark</span></span>|<span data-ttu-id="fdc73-122">2.0+</span><span class="sxs-lookup"><span data-stu-id="fdc73-122">2.0+</span></span>|
| <span data-ttu-id="fdc73-123">Scala</span><span class="sxs-lookup"><span data-stu-id="fdc73-123">Scala</span></span>| <span data-ttu-id="fdc73-124">2.11</span><span class="sxs-lookup"><span data-stu-id="fdc73-124">2.11</span></span>|
| <span data-ttu-id="fdc73-125">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="fdc73-125">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="fdc73-126">1.9.6</span><span class="sxs-lookup"><span data-stu-id="fdc73-126">1.9.6</span></span> |
 
<span data-ttu-id="fdc73-127">This article helps you run some simple samples with Python (via pyDocumentDB) and the scala interface.</span><span class="sxs-lookup"><span data-stu-id="fdc73-127">This article helps you run some simple samples with Python (via pyDocumentDB) and the scala interface.</span></span>

<span data-ttu-id="fdc73-128">There are two approaches to connect Apache Spark and Azure DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="fdc73-128">There are two approaches to connect Apache Spark and Azure DocumentDB:</span></span>
- <span data-ttu-id="fdc73-129">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="fdc73-129">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="fdc73-130">Create a Java-based Spark to DocumentDB connector utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="fdc73-130">Create a Java-based Spark to DocumentDB connector utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="fdc73-131">pyDocumentDB implementation</span><span class="sxs-lookup"><span data-stu-id="fdc73-131">pyDocumentDB implementation</span></span> 
<span data-ttu-id="fdc73-132">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables us to connect Spark to DocumentDB as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="fdc73-132">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables us to connect Spark to DocumentDB as shown in the following diagram:</span></span>

![Spark to DocumentDB data flow via pyDocumentDB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="fdc73-134">Data flow of the pyDocumentDB implementation</span><span class="sxs-lookup"><span data-stu-id="fdc73-134">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="fdc73-135">The data flow is as follows:</span><span class="sxs-lookup"><span data-stu-id="fdc73-135">The data flow is as follows:</span></span>

1. <span data-ttu-id="fdc73-136">Connection is made from Spark master node to DocumentDB gateway node via pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fdc73-136">Connection is made from Spark master node to DocumentDB gateway node via pyDocumentDB.</span></span>  <span data-ttu-id="fdc73-137">Note, user only specifies Spark and DocumentDB connections, the fact that it connects to the respective master and gateway nodes is transparent to the user.</span><span class="sxs-lookup"><span data-stu-id="fdc73-137">Note, user only specifies Spark and DocumentDB connections, the fact that it connects to the respective master and gateway nodes is transparent to the user.</span></span>
2. <span data-ttu-id="fdc73-138">Query is made against DocumentDB (via the gateway node) where the query subsequently runs the query against the collection's partitions in the data nodes.</span><span class="sxs-lookup"><span data-stu-id="fdc73-138">Query is made against DocumentDB (via the gateway node) where the query subsequently runs the query against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="fdc73-139">The response for those queries is sent back to the gateway node and that resultset is returned to Spark master node.</span><span class="sxs-lookup"><span data-stu-id="fdc73-139">The response for those queries is sent back to the gateway node and that resultset is returned to Spark master node.</span></span>
3. <span data-ttu-id="fdc73-140">Any subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span><span class="sxs-lookup"><span data-stu-id="fdc73-140">Any subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="fdc73-141">The important call out is that communication between Spark and DocumentDB is limited to the Spark master node and DocumentDB gateway nodes.</span><span class="sxs-lookup"><span data-stu-id="fdc73-141">The important call out is that communication between Spark and DocumentDB is limited to the Spark master node and DocumentDB gateway nodes.</span></span>  <span data-ttu-id="fdc73-142">The queries go as fast as the transport layer is between these two nodes.</span><span class="sxs-lookup"><span data-stu-id="fdc73-142">The queries go as fast as the transport layer is between these two nodes.</span></span>

### <a name="installing-pydocumentdb"></a><span data-ttu-id="fdc73-143">Installing pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="fdc73-143">Installing pyDocumentDB</span></span>
<span data-ttu-id="fdc73-144">You can install pyDocumentDB on your driver node using **pip**, for example:</span><span class="sxs-lookup"><span data-stu-id="fdc73-144">You can install pyDocumentDB on your driver node using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connecting-spark-to-documentdb-via-pydocumentdb"></a><span data-ttu-id="fdc73-145">Connecting Spark to DocumentDB via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="fdc73-145">Connecting Spark to DocumentDB via pyDocumentDB</span></span> 
<span data-ttu-id="fdc73-146">In return for the simplicity of the communication transport, executing a query from Spark to DocumentDB using pyDocumentDB is relatively simple.</span><span class="sxs-lookup"><span data-stu-id="fdc73-146">In return for the simplicity of the communication transport, executing a query from Spark to DocumentDB using pyDocumentDB is relatively simple.</span></span>

<span data-ttu-id="fdc73-147">The following code snippet shows how to use pyDocumentDB within a Spark context.</span><span class="sxs-lookup"><span data-stu-id="fdc73-147">The following code snippet shows how to use pyDocumentDB within a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery 
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to DocumentDB 
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==' 
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="fdc73-148">As noted in the code snippet:</span><span class="sxs-lookup"><span data-stu-id="fdc73-148">As noted in the code snippet:</span></span>

* <span data-ttu-id="fdc73-149">The DocumentDB Python SDK contains the all the necessary connection parameters including the preferred locations (that is, choosing which read replica in what priority order).</span><span class="sxs-lookup"><span data-stu-id="fdc73-149">The DocumentDB Python SDK contains the all the necessary connection parameters including the preferred locations (that is, choosing which read replica in what priority order).</span></span>
*  <span data-ttu-id="fdc73-150">Import the necessary libraries and configure your **masterKey** and **host** to create the DocumentDB *client* (**pydocumentdb.document_client**).</span><span class="sxs-lookup"><span data-stu-id="fdc73-150">Import the necessary libraries and configure your **masterKey** and **host** to create the DocumentDB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="executing-spark-queries-via-pydocumentdb"></a><span data-ttu-id="fdc73-151">Executing Spark Queries via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="fdc73-151">Executing Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="fdc73-152">The following examples use the DocumentDB instance created in the previous snippet using the specified read-only keys.</span><span class="sxs-lookup"><span data-stu-id="fdc73-152">The following examples use the DocumentDB instance created in the previous snippet using the specified read-only keys.</span></span>  <span data-ttu-id="fdc73-153">The following code snippet connects to the **airports.codes** collection (in the DoctorWho account as specified earlier) running a query to extract the airport cities in Washington state.</span><span class="sxs-lookup"><span data-stu-id="fdc73-153">The following code snippet connects to the **airports.codes** collection (in the DoctorWho account as specified earlier) running a query to extract the airport cities in Washington state.</span></span> 

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the DocumentDB client will use to connect to the database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

<span data-ttu-id="fdc73-154">Once the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted into a Python list.</span><span class="sxs-lookup"><span data-stu-id="fdc73-154">Once the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted into a Python list.</span></span> <span data-ttu-id="fdc73-155">A Python list can be easily converted into a Spark DataFrame using the following code:</span><span class="sxs-lookup"><span data-stu-id="fdc73-155">A Python list can be easily converted into a Spark DataFrame using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-documentdb"></a><span data-ttu-id="fdc73-156">Why use the pyDocumentDB to connect Spark to DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="fdc73-156">Why use the pyDocumentDB to connect Spark to DocumentDB?</span></span>
<span data-ttu-id="fdc73-157">Connecting Spark to DocumentDB using pyDocumentDB is typically for scenarios where:</span><span class="sxs-lookup"><span data-stu-id="fdc73-157">Connecting Spark to DocumentDB using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="fdc73-158">You want to use python.</span><span class="sxs-lookup"><span data-stu-id="fdc73-158">You want to use python.</span></span>
* <span data-ttu-id="fdc73-159">You are returning a relatively small result set from DocumentDB to Spark.</span><span class="sxs-lookup"><span data-stu-id="fdc73-159">You are returning a relatively small result set from DocumentDB to Spark.</span></span>  <span data-ttu-id="fdc73-160">Note that the underlying dataset within DocumentDB can be quite large.</span><span class="sxs-lookup"><span data-stu-id="fdc73-160">Note that the underlying dataset within DocumentDB can be quite large.</span></span> <span data-ttu-id="fdc73-161">It is more that you are applying filters - that is running predicate filters - against your DocumentDB source.</span><span class="sxs-lookup"><span data-stu-id="fdc73-161">It is more that you are applying filters - that is running predicate filters - against your DocumentDB source.</span></span>  

## <a name="spark-to-documentdb-connector"></a><span data-ttu-id="fdc73-162">Spark to DocumentDB connector</span><span class="sxs-lookup"><span data-stu-id="fdc73-162">Spark to DocumentDB connector</span></span>

<span data-ttu-id="fdc73-163">The Spark to DocumentDB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and DocumentDB as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="fdc73-163">The Spark to DocumentDB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and DocumentDB as shown in the following diagram:</span></span>

![Data flow in the Spark to DocumentDB connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-spark-connector.png)

<span data-ttu-id="fdc73-165">The data flow is as follows:</span><span class="sxs-lookup"><span data-stu-id="fdc73-165">The data flow is as follows:</span></span>

1. <span data-ttu-id="fdc73-166">A connection is made from the Spark master node to the DocumentDB gateway node to obtain the partition map.</span><span class="sxs-lookup"><span data-stu-id="fdc73-166">A connection is made from the Spark master node to the DocumentDB gateway node to obtain the partition map.</span></span>  <span data-ttu-id="fdc73-167">Note, the user only specifies the Spark and DocumentDB connections, the fact that it connects to the respective master and gateway nodes is transparent to the user.</span><span class="sxs-lookup"><span data-stu-id="fdc73-167">Note, the user only specifies the Spark and DocumentDB connections, the fact that it connects to the respective master and gateway nodes is transparent to the user.</span></span>
2. <span data-ttu-id="fdc73-168">This information is provided back to the Spark master node.</span><span class="sxs-lookup"><span data-stu-id="fdc73-168">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="fdc73-169">At this point, you should be able to parse the query to determine which partitions (and their locations) within DocumentDB you need to access.</span><span class="sxs-lookup"><span data-stu-id="fdc73-169">At this point, you should be able to parse the query to determine which partitions (and their locations) within DocumentDB you need to access.</span></span>
3. <span data-ttu-id="fdc73-170">This information is transmitted to the Spark worker nodes ...</span><span class="sxs-lookup"><span data-stu-id="fdc73-170">This information is transmitted to the Spark worker nodes ...</span></span>
4. <span data-ttu-id="fdc73-171">Thus allowing the Spark worker nodes to connect directly to the DocumentDB partitions directly to extract the data that is needed and bring the data back to the Spark partitions within the Spark worker nodes.</span><span class="sxs-lookup"><span data-stu-id="fdc73-171">Thus allowing the Spark worker nodes to connect directly to the DocumentDB partitions directly to extract the data that is needed and bring the data back to the Spark partitions within the Spark worker nodes.</span></span>

<span data-ttu-id="fdc73-172">The important call out is that communication between Spark and DocumentDB is significantly faster because the data movement is between the Spark worker nodes and the DocumentDB data nodes (partitions).</span><span class="sxs-lookup"><span data-stu-id="fdc73-172">The important call out is that communication between Spark and DocumentDB is significantly faster because the data movement is between the Spark worker nodes and the DocumentDB data nodes (partitions).</span></span>

### <a name="building-the-spark-to-documentdb-connector"></a><span data-ttu-id="fdc73-173">Building the Spark to DocumentDB connector</span><span class="sxs-lookup"><span data-stu-id="fdc73-173">Building the Spark to DocumentDB connector</span></span>
<span data-ttu-id="fdc73-174">Currently, the connector project uses maven.</span><span class="sxs-lookup"><span data-stu-id="fdc73-174">Currently, the connector project uses maven.</span></span> <span data-ttu-id="fdc73-175">To build the connector without dependencies, you can run:</span><span class="sxs-lookup"><span data-stu-id="fdc73-175">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="fdc73-176">You can also download the latest versions of the jar within the *releases* folder.</span><span class="sxs-lookup"><span data-stu-id="fdc73-176">You can also download the latest versions of the jar within the *releases* folder.</span></span>

### <a name="including-the-azure-documentdb-spark-jar"></a><span data-ttu-id="fdc73-177">Including the Azure DocumentDB Spark JAR</span><span class="sxs-lookup"><span data-stu-id="fdc73-177">Including the Azure DocumentDB Spark JAR</span></span>
<span data-ttu-id="fdc73-178">Prior to executing any code, you first need to include the Azure DocumentDB Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="fdc73-178">Prior to executing any code, you first need to include the Azure DocumentDB Spark JAR.</span></span>  <span data-ttu-id="fdc73-179">If you are using the **spark-shell**, then you can include the JAR using the **--jars** option.</span><span class="sxs-lookup"><span data-stu-id="fdc73-179">If you are using the **spark-shell**, then you can include the JAR using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-documentdb-spark-0.0.1-jar-with-dependencies.jar
```

<span data-ttu-id="fdc73-180">or if you want to execute the jar without dependencies:</span><span class="sxs-lookup"><span data-stu-id="fdc73-180">or if you want to execute the jar without dependencies:</span></span>

```
spark-shell --master $master --jars /$location/azure-documentdb-spark-0.0.1.jar,/$location/azure-documentdb-1.9.6.jar
```

<span data-ttu-id="fdc73-181">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span><span class="sxs-lookup"><span data-stu-id="fdc73-181">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.9.6.jar","wasb:///example/jars/azure-documentdb-spark-0.0.1.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="fdc73-182">The **jars** command enables you to include the two jars needed for **azure-documentdb-spark** (itself and the Azure DocumentDB Java SDK) and excludes **scala-reflect** so it does not interfere with the Livy calls made (Jupyter notebook > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="fdc73-182">The **jars** command enables you to include the two jars needed for **azure-documentdb-spark** (itself and the Azure DocumentDB Java SDK) and excludes **scala-reflect** so it does not interfere with the Livy calls made (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connecting-spark-to-documentdb-using-the-connector"></a><span data-ttu-id="fdc73-183">Connecting Spark to DocumentDB using the connector</span><span class="sxs-lookup"><span data-stu-id="fdc73-183">Connecting Spark to DocumentDB using the connector</span></span>
<span data-ttu-id="fdc73-184">While the communication transport is a little more complicated, executing a query from Spark to DocumentDB using the connector is significantly faster.</span><span class="sxs-lookup"><span data-stu-id="fdc73-184">While the communication transport is a little more complicated, executing a query from Spark to DocumentDB using the connector is significantly faster.</span></span>

<span data-ttu-id="fdc73-185">The following code snippet shows how to use the connector within a Spark context.</span><span class="sxs-lookup"><span data-stu-id="fdc73-185">The following code snippet shows how to use the connector within a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.documentdb.spark.schema._
import com.microsoft.azure.documentdb.spark._
import com.microsoft.azure.documentdb.spark.config.Config

// Configure connection to your collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll", 
"SamplingRatio" -> "1.0"))
 
// Create collection connection 
val coll = spark.sqlContext.read.DocumentDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="fdc73-186">As noted in the code snippet:</span><span class="sxs-lookup"><span data-stu-id="fdc73-186">As noted in the code snippet:</span></span>

- <span data-ttu-id="fdc73-187">**azure-documentdb-spark** contains the all the necessary connection parameters including the preferred locations (for example, choosing which read replica in what priority order).</span><span class="sxs-lookup"><span data-stu-id="fdc73-187">**azure-documentdb-spark** contains the all the necessary connection parameters including the preferred locations (for example, choosing which read replica in what priority order).</span></span>
- <span data-ttu-id="fdc73-188">Just import the necessary libraries and configure your masterKey and host to create the DocumentDB client.</span><span class="sxs-lookup"><span data-stu-id="fdc73-188">Just import the necessary libraries and configure your masterKey and host to create the DocumentDB client.</span></span>

### <a name="executing-spark-queries-via-the-connector"></a><span data-ttu-id="fdc73-189">Executing Spark queries via the connector</span><span class="sxs-lookup"><span data-stu-id="fdc73-189">Executing Spark queries via the connector</span></span>

<span data-ttu-id="fdc73-190">The following example uses the DocumentDB instance created in the previous snippet using the specified read-only keys.</span><span class="sxs-lookup"><span data-stu-id="fdc73-190">The following example uses the DocumentDB instance created in the previous snippet using the specified read-only keys.</span></span> <span data-ttu-id="fdc73-191">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) running a query to extract the flight delay information of flights departing from Seattle.</span><span class="sxs-lookup"><span data-stu-id="fdc73-191">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) running a query to extract the flight delay information of flights departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-documentdb-connector-implementation"></a><span data-ttu-id="fdc73-192">Why use the Spark to DocumentDB connector implementation?</span><span class="sxs-lookup"><span data-stu-id="fdc73-192">Why use the Spark to DocumentDB connector implementation?</span></span>

<span data-ttu-id="fdc73-193">Connecting Spark to DocumentDB using the connector is typically for scenarios where:</span><span class="sxs-lookup"><span data-stu-id="fdc73-193">Connecting Spark to DocumentDB using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="fdc73-194">You want to use Scala (and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-documentdb-spark/issues/3)).</span><span class="sxs-lookup"><span data-stu-id="fdc73-194">You want to use Scala (and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-documentdb-spark/issues/3)).</span></span>
* <span data-ttu-id="fdc73-195">You have a large amount of data to transfer between Apache Spark and DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fdc73-195">You have a large amount of data to transfer between Apache Spark and DocumentDB.</span></span>

<span data-ttu-id="fdc73-196">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-documentdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="fdc73-196">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-documentdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="fdc73-197">Distributed aggregation example</span><span class="sxs-lookup"><span data-stu-id="fdc73-197">Distributed aggregation example</span></span>
<span data-ttu-id="fdc73-198">This section provides some examples of how you can do distributed aggregations and analytics using Apache Spark and Azure DocumentDB together.</span><span class="sxs-lookup"><span data-stu-id="fdc73-198">This section provides some examples of how you can do distributed aggregations and analytics using Apache Spark and Azure DocumentDB together.</span></span>  <span data-ttu-id="fdc73-199">Note, Azure DocumentDB already has support for aggregations, as discussed in the [Planet scale aggregates with Azure DocumentDB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/), so here is how you can take it to the next level with Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="fdc73-199">Note, Azure DocumentDB already has support for aggregations, as discussed in the [Planet scale aggregates with Azure DocumentDB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/), so here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="fdc73-200">Note, these aggregations are in reference to the [Spark to DocumentDB Connector notebook](https://github.com/Azure/azure-documentdb-spark/blob/master/samples/notebooks/Spark-to-DocumentDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="fdc73-200">Note, these aggregations are in reference to the [Spark to DocumentDB Connector notebook](https://github.com/Azure/azure-documentdb-spark/blob/master/samples/notebooks/Spark-to-DocumentDB_Connector.ipynb).</span></span>

### <a name="connecting-to-flights-sample-data"></a><span data-ttu-id="fdc73-201">Connecting to flights sample data</span><span class="sxs-lookup"><span data-stu-id="fdc73-201">Connecting to flights sample data</span></span>
<span data-ttu-id="fdc73-202">For these aggregations examples, we are accessing some flight performance data stored in our **DoctorWho** DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="fdc73-202">For these aggregations examples, we are accessing some flight performance data stored in our **DoctorWho** DocumentDB database.</span></span>  <span data-ttu-id="fdc73-203">To connect to it, you need to utilize the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="fdc73-203">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to DocumentDB connector
import com.microsoft.azure.documentdb.spark.schema._
import com.microsoft.azure.documentdb.spark._
import com.microsoft.azure.documentdb.spark.config.Config

// Connect to DocumentDB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll", 
"SamplingRatio" -> "1.0"))

// Create collection connection 
val coll = spark.sqlContext.read.DocumentDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="fdc73-204">With this snippet, we are also going to run a base query that transfers the filtered set of data we want from DocumentDB to Spark (where the latter can perform distributed aggregates).</span><span class="sxs-lookup"><span data-stu-id="fdc73-204">With this snippet, we are also going to run a base query that transfers the filtered set of data we want from DocumentDB to Spark (where the latter can perform distributed aggregates).</span></span>  <span data-ttu-id="fdc73-205">In this case, we are asking for flights departing from Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="fdc73-205">In this case, we are asking for flights departing from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="fdc73-206">The following results were generated by running the queries from the Jupyter notebook service.</span><span class="sxs-lookup"><span data-stu-id="fdc73-206">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="fdc73-207">Note that all the code snippets are generic and not specific to any service.</span><span class="sxs-lookup"><span data-stu-id="fdc73-207">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="fdc73-208">Running LIMIT and COUNT queries</span><span class="sxs-lookup"><span data-stu-id="fdc73-208">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="fdc73-209">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span><span class="sxs-lookup"><span data-stu-id="fdc73-209">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark LIMIT query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-spark-sql-query.png)

<span data-ttu-id="fdc73-211">The next query being a simple and fast **COUNT** query:</span><span class="sxs-lookup"><span data-stu-id="fdc73-211">The next query being a simple and fast **COUNT** query:</span></span>

![Spark COUNT query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="fdc73-213">GROUP BY query</span><span class="sxs-lookup"><span data-stu-id="fdc73-213">GROUP BY query</span></span>
<span data-ttu-id="fdc73-214">In this next set, now we can easily run **GROUP BY** queries against our DocumentDB database:</span><span class="sxs-lookup"><span data-stu-id="fdc73-214">In this next set, now we can easily run **GROUP BY** queries against our DocumentDB database:</span></span>

```
select destination, sum(delay) as TotalDelays 
from originSEA 
group by destination 
order by sum(delay) desc limit 10
```

![Spark GROUP BY query graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="fdc73-216">DISTINCT, ORDER BY query</span><span class="sxs-lookup"><span data-stu-id="fdc73-216">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="fdc73-217">And here is a **DISTINCT, ORDER BY** query:</span><span class="sxs-lookup"><span data-stu-id="fdc73-217">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Spark GROUP BY query graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="fdc73-219">Continue the flight data analysis</span><span class="sxs-lookup"><span data-stu-id="fdc73-219">Continue the flight data analysis</span></span>
<span data-ttu-id="fdc73-220">You can use the following example queries to continue analysis of the flight data:</span><span class="sxs-lookup"><span data-stu-id="fdc73-220">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="fdc73-221">Top 5 delayed destinations (cities) departing from Seattle</span><span class="sxs-lookup"><span data-stu-id="fdc73-221">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay) 
from originSEA
where delay < 0 
group by destination 
order by sum(delay) limit 5
```
![Spark top delays graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="fdc73-223">Calculate median delays by destination cities departing from Seattle</span><span class="sxs-lookup"><span data-stu-id="fdc73-223">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay 
from originSEA
where delay < 0 
group by destination 
order by percentile_approx(delay, 0.5)
```

![Spark median delays graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-spark-connector/azure-documentdb-median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="fdc73-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="fdc73-225">Next steps</span></span>

<span data-ttu-id="fdc73-226">If you haven't already, download the Spark to DocumentDB connector from the [azure-documentdb-spark](https://github.com/Azure/azure-documentdb-spark) GitHub repository and explore the additional resources in the repo:</span><span class="sxs-lookup"><span data-stu-id="fdc73-226">If you haven't already, download the Spark to DocumentDB connector from the [azure-documentdb-spark](https://github.com/Azure/azure-documentdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* [<span data-ttu-id="fdc73-227">Distributed Aggregations Examples</span><span class="sxs-lookup"><span data-stu-id="fdc73-227">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-documentdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="fdc73-228">Sample Scripts and Notebooks</span><span class="sxs-lookup"><span data-stu-id="fdc73-228">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-documentdb-spark/tree/master/samples)

<span data-ttu-id="fdc73-229">You may also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span><span class="sxs-lookup"><span data-stu-id="fdc73-229">You may also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>










