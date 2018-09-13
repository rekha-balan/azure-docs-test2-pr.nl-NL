---
title: Use Apache Spark with Kafka on Azure HDInsight | Microsoft Docs
description: Learn how to use Spark on HDInsight to read and write data to a Kafka on HDInsight cluster. This example uses Scala in a Jupyter Notebook to write random data to Kafka on HDInsight, then read it back using Spark streaming.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: ''
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/13/2017
ms.author: larryfr
ms.openlocfilehash: 4dab2cff411ea76d181ecbd9f59848ab7772e10b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552124"
---
# <a name="use-apache-spark-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="0ec4a-104">Use Apache Spark with Kafka (preview) on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ec4a-104">Use Apache Spark with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="0ec4a-105">Apache Spark can be used to stream data into or out of Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-105">Apache Spark can be used to stream data into or out of Apache Kafka.</span></span> <span data-ttu-id="0ec4a-106">In this document, learn how to stream data into and out of Kafka using a Jupyter notebook from Spark on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-106">In this document, learn how to stream data into and out of Kafka using a Jupyter notebook from Spark on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec4a-107">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-107">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="0ec4a-108">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-108">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="0ec4a-109">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-109">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ec4a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0ec4a-110">Prerequisites</span></span>

* <span data-ttu-id="0ec4a-111">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0ec4a-111">An Azure subscription</span></span>

* <span data-ttu-id="0ec4a-112">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0ec4a-112">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="0ec4a-113">[cURL](https://curl.haxx.se/) - A cross platform utility for making HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-113">[cURL](https://curl.haxx.se/) - A cross platform utility for making HTTP requests.</span></span>

* <span data-ttu-id="0ec4a-114">[jq](https://stedolan.github.io/jq/) - A cross platform utility for parsing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-114">[jq](https://stedolan.github.io/jq/) - A cross platform utility for parsing JSON documents.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="0ec4a-115">Create the clusters</span><span class="sxs-lookup"><span data-stu-id="0ec4a-115">Create the clusters</span></span>

<span data-ttu-id="0ec4a-116">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-116">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="0ec4a-117">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-117">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="0ec4a-118">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-118">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="0ec4a-119">The following diagram shows how communication flows between the clusters:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-119">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram of Spark and Kafka clusters in an Azure virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="0ec4a-121">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-121">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="0ec4a-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="0ec4a-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="0ec4a-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="0ec4a-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="0ec4a-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="0ec4a-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet.json**.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet.json**.</span></span>

2. <span data-ttu-id="0ec4a-127">Use the following information to populate the entries on the **Custom deployment** blade:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-127">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight custom deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="0ec4a-129">**Resource group**: Create a group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-129">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="0ec4a-130">This group contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-130">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="0ec4a-131">**Location**: Select a location geographically close to you.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-131">**Location**: Select a location geographically close to you.</span></span> <span data-ttu-id="0ec4a-132">This location must match the location in the __SETTINGS__ section.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-132">This location must match the location in the __SETTINGS__ section.</span></span>

    * <span data-ttu-id="0ec4a-133">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-133">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="0ec4a-134">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-134">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="0ec4a-135">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-135">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="0ec4a-136">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-136">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="0ec4a-137">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-137">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="0ec4a-138">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-138">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="0ec4a-139">**Location**: The region that the clusters are created in.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-139">**Location**: The region that the clusters are created in.</span></span>

3. <span data-ttu-id="0ec4a-140">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-140">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="0ec4a-141">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-141">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="0ec4a-142">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-142">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="0ec4a-143">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-143">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Resource group blade for the vnet and clusters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="0ec4a-145">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-145">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="0ec4a-146">You use these names in later steps when connecting to the clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-146">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="0ec4a-147">Get the code</span><span class="sxs-lookup"><span data-stu-id="0ec4a-147">Get the code</span></span>

<span data-ttu-id="0ec4a-148">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="0ec4a-148">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="0ec4a-149">Understand the code</span><span class="sxs-lookup"><span data-stu-id="0ec4a-149">Understand the code</span></span>

<span data-ttu-id="0ec4a-150">This example uses a Scala application in a Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-150">This example uses a Scala application in a Jupyter notebook.</span></span> <span data-ttu-id="0ec4a-151">The code in the notebook relies on the following pieces of data:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-151">The code in the notebook relies on the following pieces of data:</span></span>

* <span data-ttu-id="0ec4a-152">__Kafka brokers__: The broker process runs on each workernode on the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-152">__Kafka brokers__: The broker process runs on each workernode on the Kafka cluster.</span></span> <span data-ttu-id="0ec4a-153">The list of brokers is required by the producer component, which writes data to Kafka.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-153">The list of brokers is required by the producer component, which writes data to Kafka.</span></span>

* <span data-ttu-id="0ec4a-154">__Zookeeper hosts__: The Zookeeper hosts for the Kafka cluster are used when consuming (reading) data from Kafka.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-154">__Zookeeper hosts__: The Zookeeper hosts for the Kafka cluster are used when consuming (reading) data from Kafka.</span></span>

* <span data-ttu-id="0ec4a-155">__Topic name__: The name of the topic that data is written to and read from.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-155">__Topic name__: The name of the topic that data is written to and read from.</span></span> <span data-ttu-id="0ec4a-156">This example expects a topic named `sparktest`.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-156">This example expects a topic named `sparktest`.</span></span>

<span data-ttu-id="0ec4a-157">See the [Kafka host information](#kafkahosts) section for information on how to obtain the Kafka broker and Zookeeper host information.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-157">See the [Kafka host information](#kafkahosts) section for information on how to obtain the Kafka broker and Zookeeper host information.</span></span>

<span data-ttu-id="0ec4a-158">The code in the notebook performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-158">The code in the notebook performs the following tasks:</span></span>

* <span data-ttu-id="0ec4a-159">Creates a consumer that reads data from a Kafka topic named `sparktest`, counts each word in the data, and stores the word and count into a temporary table named `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-159">Creates a consumer that reads data from a Kafka topic named `sparktest`, counts each word in the data, and stores the word and count into a temporary table named `wordcounts`.</span></span>

* <span data-ttu-id="0ec4a-160">Creates a producer that writes random sentences to the Kafka topic named `sparktest`.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-160">Creates a producer that writes random sentences to the Kafka topic named `sparktest`.</span></span>

* <span data-ttu-id="0ec4a-161">Selects data from the `wordcounts` table to display the counts.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-161">Selects data from the `wordcounts` table to display the counts.</span></span>

<span data-ttu-id="0ec4a-162">Each cell in the project contains comments or a text section that explains what the code does.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-162">Each cell in the project contains comments or a text section that explains what the code does.</span></span>

##<a id="kafkahosts"></a><span data-ttu-id="0ec4a-163">Kafka host information</span><span class="sxs-lookup"><span data-stu-id="0ec4a-163">Kafka host information</span></span>

<span data-ttu-id="0ec4a-164">The first thing you should do when creating an application that works with Kafka on HDInsight is to get the Kafka broker and Zookeeper host information for the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-164">The first thing you should do when creating an application that works with Kafka on HDInsight is to get the Kafka broker and Zookeeper host information for the Kafka cluster.</span></span> <span data-ttu-id="0ec4a-165">This is used by client applications to communicate with Kafka.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-165">This is used by client applications to communicate with Kafka.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec4a-166">The Kafka broker and Zookeeper hosts are not directly accessible over the Internet.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-166">The Kafka broker and Zookeeper hosts are not directly accessible over the Internet.</span></span> <span data-ttu-id="0ec4a-167">Any application that uses Kafka must either run on the Kafka cluster or within the same Azure Virtual Network as the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-167">Any application that uses Kafka must either run on the Kafka cluster or within the same Azure Virtual Network as the Kafka cluster.</span></span> <span data-ttu-id="0ec4a-168">In this case, the example runs on a Spark on HDInsight cluster in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-168">In this case, the example runs on a Spark on HDInsight cluster in the same virtual network.</span></span>

<span data-ttu-id="0ec4a-169">From your development environment, use the following commands to retrieve the broker and Zookeeper information.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-169">From your development environment, use the following commands to retrieve the broker and Zookeeper information.</span></span> <span data-ttu-id="0ec4a-170">Replace __PASSWORD__ with the login (admin) password you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-170">Replace __PASSWORD__ with the login (admin) password you used when creating the cluster.</span></span> <span data-ttu-id="0ec4a-171">Replace __BASENAME__ with the base name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-171">Replace __BASENAME__ with the base name you used when creating the cluster.</span></span>

* <span data-ttu-id="0ec4a-172">To get the __Kafka broker__ information:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-172">To get the __Kafka broker__ information:</span></span>

        curl -u admin:PASSWORD -G "https://kafka-BASENAME.azurehdinsight.net/api/v1/clusters/kafka-BASENAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'

    > [!IMPORTANT]
    > <span data-ttu-id="0ec4a-173">When using this command from Windows PowerShell, you may receive an error about shell quoting.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-173">When using this command from Windows PowerShell, you may receive an error about shell quoting.</span></span> <span data-ttu-id="0ec4a-174">If so, use the following command: `curl -u admin:PASSWORD -G "https://kafka-BASENAME.azurehdinsight.net/api/v1/clusters/kafka-BASENAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["""\(.host_components[].HostRoles.host_name):9092"""] | join(""",""")'`</span><span class="sxs-lookup"><span data-stu-id="0ec4a-174">If so, use the following command: `curl -u admin:PASSWORD -G "https://kafka-BASENAME.azurehdinsight.net/api/v1/clusters/kafka-BASENAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["""\(.host_components[].HostRoles.host_name):9092"""] | join(""",""")'`</span></span>

* <span data-ttu-id="0ec4a-175">To get the __Zookeeper host__ information:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-175">To get the __Zookeeper host__ information:</span></span>

        curl -u admin:PASSWORD -G "https://kafka-BASENAME.azurehdinsight.net/api/v1/clusters/kafka-BASENAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")'
    
    > [!IMPORTANT]
    > <span data-ttu-id="0ec4a-176">When using this command from Windows PowerShell, you may receive an error about shell quoting.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-176">When using this command from Windows PowerShell, you may receive an error about shell quoting.</span></span> <span data-ttu-id="0ec4a-177">If so, use the following command: `curl -u admin:PASSWORD -G "https://kafka-BASENAME.azurehdinsight.net/api/v1/clusters/kafka-BASENAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["""\(.host_components[].HostRoles.host_name):2181"""] | join(""",""")'`</span><span class="sxs-lookup"><span data-stu-id="0ec4a-177">If so, use the following command: `curl -u admin:PASSWORD -G "https://kafka-BASENAME.azurehdinsight.net/api/v1/clusters/kafka-BASENAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["""\(.host_components[].HostRoles.host_name):2181"""] | join(""",""")'`</span></span>

<span data-ttu-id="0ec4a-178">Both commands return information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-178">Both commands return information similar to the following text:</span></span>

* <span data-ttu-id="0ec4a-179">__Kafka brokers__: `wn0-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:9092,wn1-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:9092`</span><span class="sxs-lookup"><span data-stu-id="0ec4a-179">__Kafka brokers__: `wn0-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:9092,wn1-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:9092`</span></span>

* <span data-ttu-id="0ec4a-180">__Zookeeper hosts__: `zk0-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181,zk1-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181,zk2-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181`</span><span class="sxs-lookup"><span data-stu-id="0ec4a-180">__Zookeeper hosts__: `zk0-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181,zk1-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181,zk2-kafka.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ec4a-181">Save this information as it is used in several steps in this document.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-181">Save this information as it is used in several steps in this document.</span></span>

## <a name="use-the-jupyter-notebook"></a><span data-ttu-id="0ec4a-182">Use the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="0ec4a-182">Use the Jupyter notebook</span></span>

<span data-ttu-id="0ec4a-183">To use the example Jupyter notebook, you must upload it to the Jupyter Notebook server on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-183">To use the example Jupyter notebook, you must upload it to the Jupyter Notebook server on the Spark cluster.</span></span> <span data-ttu-id="0ec4a-184">Use the following steps to upload the notebook:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-184">Use the following steps to upload the notebook:</span></span>

1. <span data-ttu-id="0ec4a-185">In your web browser, use the following URL to connect to the Jupyter Notebook server on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-185">In your web browser, use the following URL to connect to the Jupyter Notebook server on the Spark cluster.</span></span> <span data-ttu-id="0ec4a-186">Replace __BASENAME__ with the base name used when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-186">Replace __BASENAME__ with the base name used when you created the cluster.</span></span>

        https://spark-BASENAME.azurehdinsight.net/jupyter

    <span data-ttu-id="0ec4a-187">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-187">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="0ec4a-188">From the upper right side of the page, use the __Upload__ button to upload the `KafkaStreaming.ipynb` file.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-188">From the upper right side of the page, use the __Upload__ button to upload the `KafkaStreaming.ipynb` file.</span></span> <span data-ttu-id="0ec4a-189">Select the file in the file browser dialog and select __Open__.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-189">Select the file in the file browser dialog and select __Open__.</span></span> 

    ![Use the upload button to select and upload a notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/upload-button.png)

    ![Select the KafkaStreaming.ipynb file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/select-notebook.png)

3. <span data-ttu-id="0ec4a-192">Find the __KafkaStreaming.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-192">Find the __KafkaStreaming.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Use the upload button beside the KafkaStreaming.ipynb entry to upload it to the notebook server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-with-kafka/upload-notebook.png)

4. <span data-ttu-id="0ec4a-194">Once the file has uploaded, select the __KafkaStreaming.ipynb__ entry to open the notebook.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-194">Once the file has uploaded, select the __KafkaStreaming.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="0ec4a-195">To complete this example, follow the instructions in the notebook.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-195">To complete this example, follow the instructions in the notebook.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="0ec4a-196">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="0ec4a-196">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="0ec4a-197">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-197">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="0ec4a-198">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-198">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ec4a-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ec4a-199">Next steps</span></span>

<span data-ttu-id="0ec4a-200">In this document, you learned how to use Spark to read and write to Kafka.</span><span class="sxs-lookup"><span data-stu-id="0ec4a-200">In this document, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="0ec4a-201">Use the following links to discover other ways to work with Kafka:</span><span class="sxs-lookup"><span data-stu-id="0ec4a-201">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="0ec4a-202">Get started with Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ec4a-202">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="0ec4a-203">Use MirrorMaker to create a replica of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ec4a-203">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="0ec4a-204">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ec4a-204">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)








