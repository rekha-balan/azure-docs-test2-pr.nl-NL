---
title: Apache Spark streaming with Kafka - Azure HDInsight
description: Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka using DStreams. In this example, you stream data using a Jupyter notebook from Spark on HDInsight.
keywords: kafka example,kafka zookeeper,spark streaming kafka,spark streaming kafka example
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/23/2018
ms.author: jasonh
ms.openlocfilehash: d06e9d26051fbfafc4d717ec180e8760157aefd9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783008"
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-on-hdinsight"></a><span data-ttu-id="c7dee-105">Apache Spark streaming (DStream) example with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7dee-105">Apache Spark streaming (DStream) example with Kafka on HDInsight</span></span>

<span data-ttu-id="c7dee-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span><span class="sxs-lookup"><span data-stu-id="c7dee-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="c7dee-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="c7dee-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c7dee-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c7dee-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="c7dee-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="c7dee-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="c7dee-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span><span class="sxs-lookup"><span data-stu-id="c7dee-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7dee-111">This example uses DStreams, which is an older Spark streaming technology.</span><span class="sxs-lookup"><span data-stu-id="c7dee-111">This example uses DStreams, which is an older Spark streaming technology.</span></span> <span data-ttu-id="c7dee-112">For an example that uses newer Spark streaming features, see the [Spark Structured Streaming with Kafka](hdinsight-apache-kafka-spark-structured-streaming.md) document.</span><span class="sxs-lookup"><span data-stu-id="c7dee-112">For an example that uses newer Spark streaming features, see the [Spark Structured Streaming with Kafka](hdinsight-apache-kafka-spark-structured-streaming.md) document.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="c7dee-113">Create the clusters</span><span class="sxs-lookup"><span data-stu-id="c7dee-113">Create the clusters</span></span>

<span data-ttu-id="c7dee-114">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span><span class="sxs-lookup"><span data-stu-id="c7dee-114">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="c7dee-115">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="c7dee-115">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="c7dee-116">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="c7dee-116">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="c7dee-117">The following diagram shows how communication flows between the clusters:</span><span class="sxs-lookup"><span data-stu-id="c7dee-117">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram of Spark and Kafka clusters in an Azure virtual network](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="c7dee-119">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="c7dee-119">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="c7dee-120">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="c7dee-120">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="c7dee-121">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="c7dee-121">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="c7dee-122">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c7dee-122">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="c7dee-123">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7dee-123">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="c7dee-124">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="c7dee-124">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c7dee-125">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="c7dee-125">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="c7dee-126">This template creates a Kafka cluster that contains three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="c7dee-126">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="c7dee-127">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span><span class="sxs-lookup"><span data-stu-id="c7dee-127">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="c7dee-128">Use the following information to populate the entries on the **Custom deployment** section:</span><span class="sxs-lookup"><span data-stu-id="c7dee-128">Use the following information to populate the entries on the **Custom deployment** section:</span></span>
   
    ![HDInsight custom deployment](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="c7dee-130">**Resource group**: Create a group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="c7dee-130">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="c7dee-131">This group contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c7dee-131">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="c7dee-132">**Location**: Select a location geographically close to you.</span><span class="sxs-lookup"><span data-stu-id="c7dee-132">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="c7dee-133">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-133">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="c7dee-134">For example, entering **hdi** creates a Spark cluster named __spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="c7dee-134">For example, entering **hdi** creates a Spark cluster named __spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="c7dee-135">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-135">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c7dee-136">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-136">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c7dee-137">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-137">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c7dee-138">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-138">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="c7dee-139">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="c7dee-139">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="c7dee-140">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="c7dee-140">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="c7dee-141">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-141">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="c7dee-142">Once the resources have been created, a summary page appears.</span><span class="sxs-lookup"><span data-stu-id="c7dee-142">Once the resources have been created, a summary page appears.</span></span>

![Resource group summary for the vnet and clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="c7dee-144">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span><span class="sxs-lookup"><span data-stu-id="c7dee-144">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="c7dee-145">You use these names in later steps when connecting to the clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-145">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="c7dee-146">Use the notebooks</span><span class="sxs-lookup"><span data-stu-id="c7dee-146">Use the notebooks</span></span>

<span data-ttu-id="c7dee-147">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="c7dee-147">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="c7dee-148">To complete this example, follow the steps in the `README.md`.</span><span class="sxs-lookup"><span data-stu-id="c7dee-148">To complete this example, follow the steps in the `README.md`.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="c7dee-149">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="c7dee-149">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c7dee-150">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7dee-150">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="c7dee-151">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span><span class="sxs-lookup"><span data-stu-id="c7dee-151">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7dee-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7dee-152">Next steps</span></span>

<span data-ttu-id="c7dee-153">In this example, you learned how to use Spark to read and write to Kafka.</span><span class="sxs-lookup"><span data-stu-id="c7dee-153">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="c7dee-154">Use the following links to discover other ways to work with Kafka:</span><span class="sxs-lookup"><span data-stu-id="c7dee-154">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="c7dee-155">Get started with Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7dee-155">Get started with Apache Kafka on HDInsight</span></span>](kafka/apache-kafka-get-started.md)
* [<span data-ttu-id="c7dee-156">Use MirrorMaker to create a replica of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7dee-156">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](kafka/apache-kafka-mirroring.md)
* [<span data-ttu-id="c7dee-157">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7dee-157">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

