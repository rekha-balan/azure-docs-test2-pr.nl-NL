---
title: Install published application - H2O Sparkling Water - Azure HDInsight
description: Install and use the H2O Sparkling Water third-party Hadoop application.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: e5a9505c41c14016768a5da42f9ac1836240b98f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866848"
---
# <a name="install-published-application---h2o-sparkling-water"></a><span data-ttu-id="5880d-103">Install published application - H2O Sparkling Water</span><span class="sxs-lookup"><span data-stu-id="5880d-103">Install published application - H2O Sparkling Water</span></span>

<span data-ttu-id="5880d-104">This article describes how to install and run the [H20 Sparkling Water](http://www.h2o.ai/) published Hadoop application on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5880d-104">This article describes how to install and run the [H20 Sparkling Water](http://www.h2o.ai/) published Hadoop application on Azure HDInsight.</span></span> <span data-ttu-id="5880d-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="5880d-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span> <span data-ttu-id="5880d-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="5880d-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>

## <a name="about-h2o-sparkling-water"></a><span data-ttu-id="5880d-107">About H2O Sparkling Water</span><span class="sxs-lookup"><span data-stu-id="5880d-107">About H2O Sparkling Water</span></span>

<span data-ttu-id="5880d-108">H2O Sparkling Water is an open source, fully distributed in-memory machine learning platform with linear scalability.</span><span class="sxs-lookup"><span data-stu-id="5880d-108">H2O Sparkling Water is an open source, fully distributed in-memory machine learning platform with linear scalability.</span></span> <span data-ttu-id="5880d-109">H2O Sparkling Water let you combine the fast, scalable machine learning algorithms of H2O with the capabilities of Spark.</span><span class="sxs-lookup"><span data-stu-id="5880d-109">H2O Sparkling Water let you combine the fast, scalable machine learning algorithms of H2O with the capabilities of Spark.</span></span> <span data-ttu-id="5880d-110">With Sparkling Water, users can drive computation from Scala, R, and Python using the H2O Flow UI.</span><span class="sxs-lookup"><span data-stu-id="5880d-110">With Sparkling Water, users can drive computation from Scala, R, and Python using the H2O Flow UI.</span></span>

<span data-ttu-id="5880d-111">H2O Sparkling Water provides:</span><span class="sxs-lookup"><span data-stu-id="5880d-111">H2O Sparkling Water provides:</span></span>

* <span data-ttu-id="5880d-112">**Easy-to-use WebUI and familiar interfaces** – Set up and get started quickly using either H2O’s intuitive web-based Flow GUI or programming environments such as R, Python, Java, Scala, JSON, and the H2O APIs.</span><span class="sxs-lookup"><span data-stu-id="5880d-112">**Easy-to-use WebUI and familiar interfaces** – Set up and get started quickly using either H2O’s intuitive web-based Flow GUI or programming environments such as R, Python, Java, Scala, JSON, and the H2O APIs.</span></span>
* <span data-ttu-id="5880d-113">**Data-agnostic support for all common database and file types** – Easily explore and model Big Data from within Microsoft Excel, R Studio, Tableau, and more.</span><span class="sxs-lookup"><span data-stu-id="5880d-113">**Data-agnostic support for all common database and file types** – Easily explore and model Big Data from within Microsoft Excel, R Studio, Tableau, and more.</span></span> <span data-ttu-id="5880d-114">Connect to data from HDFS, S3, SQL, and NoSQL data sources.</span><span class="sxs-lookup"><span data-stu-id="5880d-114">Connect to data from HDFS, S3, SQL, and NoSQL data sources.</span></span>
* <span data-ttu-id="5880d-115">**Massively scalable Big Data munging and analysis** – H2O Big Joins can perform 7x faster than R data.table operations, and linearly scale to 10 billion x 10 billion row joins.</span><span class="sxs-lookup"><span data-stu-id="5880d-115">**Massively scalable Big Data munging and analysis** – H2O Big Joins can perform 7x faster than R data.table operations, and linearly scale to 10 billion x 10 billion row joins.</span></span>
* <span data-ttu-id="5880d-116">**Real-time data scoring** – Rapidly deploy models to production using plain-old Java objects (POJO), model-optimized Java objects (MOJO), or the H2O REST API.</span><span class="sxs-lookup"><span data-stu-id="5880d-116">**Real-time data scoring** – Rapidly deploy models to production using plain-old Java objects (POJO), model-optimized Java objects (MOJO), or the H2O REST API.</span></span>

### <a name="resource-links"></a><span data-ttu-id="5880d-117">Resource links</span><span class="sxs-lookup"><span data-stu-id="5880d-117">Resource links</span></span>

* [<span data-ttu-id="5880d-118">H2O.ai Engineering Roadmap</span><span class="sxs-lookup"><span data-stu-id="5880d-118">H2O.ai Engineering Roadmap</span></span>](http://jira.h2o.ai/)
* [<span data-ttu-id="5880d-119">H2O.ai Home</span><span class="sxs-lookup"><span data-stu-id="5880d-119">H2O.ai Home</span></span>](http://www.h2o.ai/)
* [<span data-ttu-id="5880d-120">H2O.ai Documentation</span><span class="sxs-lookup"><span data-stu-id="5880d-120">H2O.ai Documentation</span></span>](http://docs.h2o.ai/)
* [<span data-ttu-id="5880d-121">H2O.ai Support</span><span class="sxs-lookup"><span data-stu-id="5880d-121">H2O.ai Support</span></span>](https://support.h2o.ai/)
* [<span data-ttu-id="5880d-122">H2O.ai Open Source Codebase</span><span class="sxs-lookup"><span data-stu-id="5880d-122">H2O.ai Open Source Codebase</span></span>](https://github.com/h2oai/)

## <a name="prerequisites"></a><span data-ttu-id="5880d-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5880d-123">Prerequisites</span></span>

<span data-ttu-id="5880d-124">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span><span class="sxs-lookup"><span data-stu-id="5880d-124">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span></span>

* <span data-ttu-id="5880d-125">Cluster tier(s): Standard or Premium</span><span class="sxs-lookup"><span data-stu-id="5880d-125">Cluster tier(s): Standard or Premium</span></span>
* <span data-ttu-id="5880d-126">Cluster type: Spark</span><span class="sxs-lookup"><span data-stu-id="5880d-126">Cluster type: Spark</span></span>
* <span data-ttu-id="5880d-127">Cluster version(s): 3.5 or 3.6</span><span class="sxs-lookup"><span data-stu-id="5880d-127">Cluster version(s): 3.5 or 3.6</span></span>

## <a name="install-the-h2o-sparkling-water-published-application"></a><span data-ttu-id="5880d-128">Install the H2O Sparkling Water published application</span><span class="sxs-lookup"><span data-stu-id="5880d-128">Install the H2O Sparkling Water published application</span></span>

<span data-ttu-id="5880d-129">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="5880d-129">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span>

## <a name="launch-h2o-sparkling-water"></a><span data-ttu-id="5880d-130">Launch H2O Sparkling Water</span><span class="sxs-lookup"><span data-stu-id="5880d-130">Launch H2O Sparkling Water</span></span>

1. <span data-ttu-id="5880d-131">After installation, you can start using H2O Sparkling Water (h2o-sparklingwater) from your cluster in Azure portal by opening Jupyter Notebooks (`https://<ClusterName>.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="5880d-131">After installation, you can start using H2O Sparkling Water (h2o-sparklingwater) from your cluster in Azure portal by opening Jupyter Notebooks (`https://<ClusterName>.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="5880d-132">You can also get to Jupyter by selecting **Cluster dashboard** from your cluster pane in the portal, then selecting **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="5880d-132">You can also get to Jupyter by selecting **Cluster dashboard** from your cluster pane in the portal, then selecting **Jupyter Notebook**.</span></span> <span data-ttu-id="5880d-133">You are prompted to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="5880d-133">You are prompted to enter your credentials.</span></span> <span data-ttu-id="5880d-134">Enter the cluster's Hadoop credentials as specified on cluster creation.</span><span class="sxs-lookup"><span data-stu-id="5880d-134">Enter the cluster's Hadoop credentials as specified on cluster creation.</span></span>

2. <span data-ttu-id="5880d-135">In Jupyter, you see three folders: H2O-PySparkling-Examples, PySpark Examples, and Scala Examples.</span><span class="sxs-lookup"><span data-stu-id="5880d-135">In Jupyter, you see three folders: H2O-PySparkling-Examples, PySpark Examples, and Scala Examples.</span></span> <span data-ttu-id="5880d-136">Select the **H2O-PySparkling-Examples** folder.</span><span class="sxs-lookup"><span data-stu-id="5880d-136">Select the **H2O-PySparkling-Examples** folder.</span></span>

    ![Jupyter Notebooks home](./media/hdinsight-apps-install-h2o/jupyter-home.png)

3. <span data-ttu-id="5880d-138">The first step when creating a new notebook is to configure the Spark environment.</span><span class="sxs-lookup"><span data-stu-id="5880d-138">The first step when creating a new notebook is to configure the Spark environment.</span></span> <span data-ttu-id="5880d-139">This information is included in the **Sentiment_analysis_with_Sparkling_Water** example.</span><span class="sxs-lookup"><span data-stu-id="5880d-139">This information is included in the **Sentiment_analysis_with_Sparkling_Water** example.</span></span> <span data-ttu-id="5880d-140">When configuring the Spark environment, be sure to use the correct jar, and specify the IP address provided by the output of the first cell.</span><span class="sxs-lookup"><span data-stu-id="5880d-140">When configuring the Spark environment, be sure to use the correct jar, and specify the IP address provided by the output of the first cell.</span></span>

    ![Jupyter Notebooks home](./media/hdinsight-apps-install-h2o/spark-config.png)

4. <span data-ttu-id="5880d-142">Start the H2O Cluster.</span><span class="sxs-lookup"><span data-stu-id="5880d-142">Start the H2O Cluster.</span></span>

    ![Start cluster](./media/hdinsight-apps-install-h2o/start-cluster.png)

5. <span data-ttu-id="5880d-144">After the H2O Cluster is up and running, open H2O Flow by going to **`https://<ClusterName>-h2o.apps.azurehdinsight.net:443`**.</span><span class="sxs-lookup"><span data-stu-id="5880d-144">After the H2O Cluster is up and running, open H2O Flow by going to **`https://<ClusterName>-h2o.apps.azurehdinsight.net:443`**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5880d-145">If you are unable to open H2O Flow, try clearing your browser cache.</span><span class="sxs-lookup"><span data-stu-id="5880d-145">If you are unable to open H2O Flow, try clearing your browser cache.</span></span> <span data-ttu-id="5880d-146">If you still unable to reach it, you probably do not have enough resources on your cluster.</span><span class="sxs-lookup"><span data-stu-id="5880d-146">If you still unable to reach it, you probably do not have enough resources on your cluster.</span></span> <span data-ttu-id="5880d-147">Try increasing the number of Worker nodes under the **Scale cluster** option in your cluster pane.</span><span class="sxs-lookup"><span data-stu-id="5880d-147">Try increasing the number of Worker nodes under the **Scale cluster** option in your cluster pane.</span></span>

    ![H2O Flow dashboard](./media/hdinsight-apps-install-h2o/h2o-flow.png)

6. <span data-ttu-id="5880d-149">Select the **Million_Songs.flow** example from the menu on the right.</span><span class="sxs-lookup"><span data-stu-id="5880d-149">Select the **Million_Songs.flow** example from the menu on the right.</span></span> <span data-ttu-id="5880d-150">When prompted with a warning, click **Load Notebook**.</span><span class="sxs-lookup"><span data-stu-id="5880d-150">When prompted with a warning, click **Load Notebook**.</span></span> <span data-ttu-id="5880d-151">This demo is designed to run in a few minutes using real data.</span><span class="sxs-lookup"><span data-stu-id="5880d-151">This demo is designed to run in a few minutes using real data.</span></span> <span data-ttu-id="5880d-152">The goal is to predict from the data whether the song was released before or after 2004 using binary classification.</span><span class="sxs-lookup"><span data-stu-id="5880d-152">The goal is to predict from the data whether the song was released before or after 2004 using binary classification.</span></span>

    ![Select Million_Songs.flow](./media/hdinsight-apps-install-h2o/million-songs.png)

7. <span data-ttu-id="5880d-154">Find the path containing **milsongs-cls-train.csv.gz**, and replace the entire path with **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-train.csv.gz**.</span><span class="sxs-lookup"><span data-stu-id="5880d-154">Find the path containing **milsongs-cls-train.csv.gz**, and replace the entire path with **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-train.csv.gz**.</span></span>

8. <span data-ttu-id="5880d-155">Find the path containing **milsongs-cls-test.csv.gz** and replace it with **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-test.csv.gz**.</span><span class="sxs-lookup"><span data-stu-id="5880d-155">Find the path containing **milsongs-cls-test.csv.gz** and replace it with **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-test.csv.gz**.</span></span>

9. <span data-ttu-id="5880d-156">To execute all statements within the notebook cells, select the **Run All** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="5880d-156">To execute all statements within the notebook cells, select the **Run All** button on the toolbar.</span></span>

    ![Run All](./media/hdinsight-apps-install-h2o/run-all.png)

10. <span data-ttu-id="5880d-158">After a few minutes, you should see an output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="5880d-158">After a few minutes, you should see an output similar to the following.</span></span>

    ![Output](./media/hdinsight-apps-install-h2o/output.png)

<span data-ttu-id="5880d-160">That's it!</span><span class="sxs-lookup"><span data-stu-id="5880d-160">That's it!</span></span> <span data-ttu-id="5880d-161">You've harnessed artificial intelligence in Spark within a matter of minutes.</span><span class="sxs-lookup"><span data-stu-id="5880d-161">You've harnessed artificial intelligence in Spark within a matter of minutes.</span></span> <span data-ttu-id="5880d-162">You can now explore more examples in H2O Flow that demonstrate different types of machine learning algorithms.</span><span class="sxs-lookup"><span data-stu-id="5880d-162">You can now explore more examples in H2O Flow that demonstrate different types of machine learning algorithms.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5880d-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="5880d-163">Next steps</span></span>

* [<span data-ttu-id="5880d-164">H2O documentation</span><span class="sxs-lookup"><span data-stu-id="5880d-164">H2O documentation</span></span>](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/index.html)
* <span data-ttu-id="5880d-165">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5880d-165">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="5880d-166">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5880d-166">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="5880d-167">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="5880d-167">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="5880d-168">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="5880d-168">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="5880d-169">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="5880d-169">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span></span>
