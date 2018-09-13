---
title: Apache Spark Structured Streaming from Kafka to Azure Cosmos DB - Azure HDInsight
description: Learn how to use Apache Spark Structured Streaming to read data from Apache Kafka and then store it into Azure Cosmos DB. In this example, you stream data using a Jupyter notebook from Spark on HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 03/26/2018
ms.author: jasonh
ms.openlocfilehash: c18234e50711b2496b793263ca8d314f16347cbe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868131"
---
# <a name="use-spark-structured-streaming-with-kafka-and-azure-cosmos-db"></a><span data-ttu-id="bf2cf-104">Use Spark Structured Streaming with Kafka and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf2cf-104">Use Spark Structured Streaming with Kafka and Azure Cosmos DB</span></span>

<span data-ttu-id="bf2cf-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight, and then store the data into Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight, and then store the data into Azure Cosmos DB.</span></span>

<span data-ttu-id="bf2cf-106">Azure Cosmos DB is a globally distributed, multi-model database.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-106">Azure Cosmos DB is a globally distributed, multi-model database.</span></span> <span data-ttu-id="bf2cf-107">This example uses a SQL API database model.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-107">This example uses a SQL API database model.</span></span> <span data-ttu-id="bf2cf-108">For more information, see the [Welcome to Azure Cosmos DB](../cosmos-db/introduction.md) document.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-108">For more information, see the [Welcome to Azure Cosmos DB](../cosmos-db/introduction.md) document.</span></span>

<span data-ttu-id="bf2cf-109">Spark structured streaming is a stream processing engine built on Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-109">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="bf2cf-110">It allows you to express streaming computations the same as batch computation on static data.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-110">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="bf2cf-111">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-111">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf2cf-112">This example used Spark 2.2 on HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-112">This example used Spark 2.2 on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="bf2cf-113">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-113">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="bf2cf-114">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-114">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="bf2cf-115">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-115">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="bf2cf-116">Create the clusters</span><span class="sxs-lookup"><span data-stu-id="bf2cf-116">Create the clusters</span></span>

<span data-ttu-id="bf2cf-117">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-117">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="bf2cf-118">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-118">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="bf2cf-119">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-119">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="bf2cf-120">The following diagram shows how communication flows between the clusters:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-120">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram of Spark and Kafka clusters in an Azure virtual network](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="bf2cf-122">The Kafka service is limited to communication within the virtual network.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-122">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="bf2cf-123">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-123">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="bf2cf-124">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="bf2cf-124">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="bf2cf-125">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-125">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="bf2cf-126">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-126">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="bf2cf-127">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-127">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fhdinsight-spark-scala-kafka-cosmosdb%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
    </a>

    <span data-ttu-id="bf2cf-128">The Azure Resource Manager template is located in the GitHub repository for this project ([https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb)).</span><span class="sxs-lookup"><span data-stu-id="bf2cf-128">The Azure Resource Manager template is located in the GitHub repository for this project ([https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb)).</span></span>

    <span data-ttu-id="bf2cf-129">This template creates the following resources:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-129">This template creates the following resources:</span></span>

    * <span data-ttu-id="bf2cf-130">A Kafka on HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-130">A Kafka on HDInsight 3.6 cluster.</span></span>

    * <span data-ttu-id="bf2cf-131">A Spark on HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-131">A Spark on HDInsight 3.6 cluster.</span></span>

    * <span data-ttu-id="bf2cf-132">An Azure Virtual Network, which contains the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-132">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

        > [!NOTE]
        > <span data-ttu-id="bf2cf-133">The virtual network created by the template uses the 10.0.0.0/16 address space.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-133">The virtual network created by the template uses the 10.0.0.0/16 address space.</span></span>

    * <span data-ttu-id="bf2cf-134">An Azure Cosmos DB SQL API database.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-134">An Azure Cosmos DB SQL API database.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bf2cf-135">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-135">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="bf2cf-136">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-136">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="bf2cf-137">Use the following information to populate the entries on the **Custom deployment** section:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-137">Use the following information to populate the entries on the **Custom deployment** section:</span></span>
   
    ![HDInsight custom deployment](./media/apache-kafka-spark-structured-streaming-cosmosdb/parameters.png)

    * <span data-ttu-id="bf2cf-139">**Subscription**: Select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-139">**Subscription**: Select your Azure subscription.</span></span>
   
    * <span data-ttu-id="bf2cf-140">**Resource group**: Create a group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-140">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="bf2cf-141">This group contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-141">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="bf2cf-142">**Location**: Select a location geographically close to you.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-142">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="bf2cf-143">**Cosmos DB Account Name**: This value is used as the name for the Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-143">**Cosmos DB Account Name**: This value is used as the name for the Cosmos DB account.</span></span>

    * <span data-ttu-id="bf2cf-144">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-144">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="bf2cf-145">For example, entering **myhdi** creates a Spark cluster named __spark-myhdi__ and a Kafka cluster named **kafka-myhdi**.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-145">For example, entering **myhdi** creates a Spark cluster named __spark-myhdi__ and a Kafka cluster named **kafka-myhdi**.</span></span>

    * <span data-ttu-id="bf2cf-146">**Cluster Version**: The HDInsight cluster version.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-146">**Cluster Version**: The HDInsight cluster version.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="bf2cf-147">This example is tested with HDInsight 3.6, and may not work with other cluster types.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-147">This example is tested with HDInsight 3.6, and may not work with other cluster types.</span></span>

    * <span data-ttu-id="bf2cf-148">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-148">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="bf2cf-149">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-149">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="bf2cf-150">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-150">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="bf2cf-151">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-151">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="bf2cf-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="bf2cf-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="bf2cf-154">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-154">It takes about 20 minutes to create the clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf2cf-155">It may take up to 45 minutes to create the clusters, virtual network, and Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-155">It may take up to 45 minutes to create the clusters, virtual network, and Cosmos DB account.</span></span>

## <a name="create-the-cosmos-db-database-and-collection"></a><span data-ttu-id="bf2cf-156">Create the Cosmos DB database and collection</span><span class="sxs-lookup"><span data-stu-id="bf2cf-156">Create the Cosmos DB database and collection</span></span>

<span data-ttu-id="bf2cf-157">The project used in this document stores data in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-157">The project used in this document stores data in Cosmos DB.</span></span> <span data-ttu-id="bf2cf-158">Before running the code, you must first create a _database_ and _collection_ in your Cosmos DB instance.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-158">Before running the code, you must first create a _database_ and _collection_ in your Cosmos DB instance.</span></span> <span data-ttu-id="bf2cf-159">You must also retrieve the document endpoint and the _key_ used to authenticate requests to Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-159">You must also retrieve the document endpoint and the _key_ used to authenticate requests to Cosmos DB.</span></span> 

<span data-ttu-id="bf2cf-160">One way to do this is to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="bf2cf-160">One way to do this is to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest).</span></span> <span data-ttu-id="bf2cf-161">The following script will create a database named `kafkadata` and a collection named `kafkacollection`.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-161">The following script will create a database named `kafkadata` and a collection named `kafkacollection`.</span></span> <span data-ttu-id="bf2cf-162">It then returns the primary key.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-162">It then returns the primary key.</span></span>

```azurecli
#!/bin/bash

# Replace 'myresourcegroup' with the name of your resource group
resourceGroupName='myresourcegroup'
# Replace 'mycosmosaccount' with the name of your Cosmos DB account name
name='mycosmosaccount'

# WARNING: If you change the databaseName or collectionName
#          then you must update the values in the Jupyter notebook
databaseName='kafkadata'
collectionName='kafkacollection'

# Create the database
az cosmosdb database create --name $name --db-name $databaseName --resource-group $resourceGroupName
# Create the collection
az cosmosdb collection create --collection-name $collectionName --name $name --db-name $databaseName --resource-group $resourceGroupName

# Get the endpoint
az cosmosdb show --name $name --resource-group $resourceGroupName --query documentEndpoint

# Get the primary key
az cosmosdb list-keys --name $name --resource-group $resourceGroupName --query primaryMasterKey
```

<span data-ttu-id="bf2cf-163">The document endpoint and primary key information is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-163">The document endpoint and primary key information is similar to the following text:</span></span>

```text
# endpoint
"https://mycosmosaccount.documents.azure.com:443/"
# key
"YqPXw3RP7TsJoBF5imkYR0QNA02IrreNAlkrUMkL8EW94YHs41bktBhIgWq4pqj6HCGYijQKMRkCTsSaKUO2pw=="
```

> [!IMPORTANT]
> <span data-ttu-id="bf2cf-164">Save the endpoint and key values, as they are needed in the Jupyter Notebooks.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-164">Save the endpoint and key values, as they are needed in the Jupyter Notebooks.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="bf2cf-165">Get the Kafka brokers</span><span class="sxs-lookup"><span data-stu-id="bf2cf-165">Get the Kafka brokers</span></span>

<span data-ttu-id="bf2cf-166">The code in this example connects to Kafka broker hosts in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-166">The code in this example connects to Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="bf2cf-167">To find the addresses of the two Kafka broker hosts, use the following PowerShell or Bash example:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-167">To find the addresses of the two Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds `
    -UseBasicParsing
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
($brokerHosts -join ":9092,") + ":9092"
```

> [!NOTE]
> <span data-ttu-id="bf2cf-168">The Bash example expects `$CLUSTERNAME` to contain the name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-168">The Bash example expects `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="bf2cf-169">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-169">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

```bash
curl -u admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
```

<span data-ttu-id="bf2cf-170">When prompted, enter the password for the cluster login (admin) account</span><span class="sxs-lookup"><span data-stu-id="bf2cf-170">When prompted, enter the password for the cluster login (admin) account</span></span>

<span data-ttu-id="bf2cf-171">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-171">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="bf2cf-172">Save this information, as it is used in the following sections of this document.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-172">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="bf2cf-173">Get the notebooks</span><span class="sxs-lookup"><span data-stu-id="bf2cf-173">Get the notebooks</span></span>

<span data-ttu-id="bf2cf-174">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="bf2cf-174">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="bf2cf-175">Upload the notebooks</span><span class="sxs-lookup"><span data-stu-id="bf2cf-175">Upload the notebooks</span></span>

<span data-ttu-id="bf2cf-176">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-176">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="bf2cf-177">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-177">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="bf2cf-178">In the following URL, replace `CLUSTERNAME` with the name of your __Spark__ cluster:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-178">In the following URL, replace `CLUSTERNAME` with the name of your __Spark__ cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="bf2cf-179">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-179">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="bf2cf-180">From the upper right side of the page, use the __Upload__ button to upload the __Stream-taxi-data-to-kafka.ipynb__ file to the cluster.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-180">From the upper right side of the page, use the __Upload__ button to upload the __Stream-taxi-data-to-kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="bf2cf-181">Select __Open__ to start the upload.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-181">Select __Open__ to start the upload.</span></span>

3. <span data-ttu-id="bf2cf-182">Find the __Stream-taxi-data-to-kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-182">Find the __Stream-taxi-data-to-kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

4. <span data-ttu-id="bf2cf-183">Repeat steps 1-3 to load the __Stream-data-from-Kafka-to-Cosmos-DB.ipynb__ notebook.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-183">Repeat steps 1-3 to load the __Stream-data-from-Kafka-to-Cosmos-DB.ipynb__ notebook.</span></span>

## <a name="load-taxi-data-into-kafka"></a><span data-ttu-id="bf2cf-184">Load taxi data into Kafka</span><span class="sxs-lookup"><span data-stu-id="bf2cf-184">Load taxi data into Kafka</span></span>

<span data-ttu-id="bf2cf-185">Once the files have been uploaded, select the __Stream-taxi-data-to-kafka.ipynb__ entry to open the notebook.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-185">Once the files have been uploaded, select the __Stream-taxi-data-to-kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="bf2cf-186">Follow the steps in the notebook to load data into Kafka.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-186">Follow the steps in the notebook to load data into Kafka.</span></span>

## <a name="process-taxi-data-using-spark-structured-streaming"></a><span data-ttu-id="bf2cf-187">Process taxi data using Spark Structured Streaming</span><span class="sxs-lookup"><span data-stu-id="bf2cf-187">Process taxi data using Spark Structured Streaming</span></span>

<span data-ttu-id="bf2cf-188">From the Jupyter Notebook home page, select the __Stream-data-from-Kafka-to-Cosmos-DB.ipynb__ entry.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-188">From the Jupyter Notebook home page, select the __Stream-data-from-Kafka-to-Cosmos-DB.ipynb__ entry.</span></span> <span data-ttu-id="bf2cf-189">Follow the steps in the notebook to stream data from Kafka and into Azure Cosmos DB using Spark Structured Streaming.</span><span class="sxs-lookup"><span data-stu-id="bf2cf-189">Follow the steps in the notebook to stream data from Kafka and into Azure Cosmos DB using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf2cf-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf2cf-190">Next steps</span></span>

<span data-ttu-id="bf2cf-191">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark, Kafka, and Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="bf2cf-191">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark, Kafka, and Azure Cosmos DB:</span></span>

* <span data-ttu-id="bf2cf-192">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="bf2cf-192">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="bf2cf-193">Start with Jupyter Notebook and Spark on HDInsight</span><span class="sxs-lookup"><span data-stu-id="bf2cf-193">Start with Jupyter Notebook and Spark on HDInsight</span></span>](spark/apache-spark-jupyter-spark-sql.md)
* [<span data-ttu-id="bf2cf-194">Welcome to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf2cf-194">Welcome to Azure Cosmos DB</span></span>](../cosmos-db/introduction.md)
