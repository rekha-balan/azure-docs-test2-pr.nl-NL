---
title: Install published application - StreamSets Data Collector - Azure HDInsight
description: Install and use the StreamSets Data Collector third-party Hadoop application.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: 72ace99a8124b0a288e8facf630e947151169d0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856553"
---
# <a name="install-published-application---streamsets-data-collector"></a><span data-ttu-id="6b96b-103">Install published application - StreamSets Data Collector</span><span class="sxs-lookup"><span data-stu-id="6b96b-103">Install published application - StreamSets Data Collector</span></span>

<span data-ttu-id="6b96b-104">This article describes how to install and run the [StreamSets Data Collector for HDInsight](https://streamsets.com/) published Hadoop application on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b96b-104">This article describes how to install and run the [StreamSets Data Collector for HDInsight](https://streamsets.com/) published Hadoop application on Azure HDInsight.</span></span> <span data-ttu-id="6b96b-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6b96b-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span> <span data-ttu-id="6b96b-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6b96b-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>

## <a name="about-streamsets-data-collector"></a><span data-ttu-id="6b96b-107">About StreamSets Data Collector</span><span class="sxs-lookup"><span data-stu-id="6b96b-107">About StreamSets Data Collector</span></span>

<span data-ttu-id="6b96b-108">The StreamSets Data Collector deploys on top of an Azure HDInsight application.</span><span class="sxs-lookup"><span data-stu-id="6b96b-108">The StreamSets Data Collector deploys on top of an Azure HDInsight application.</span></span> <span data-ttu-id="6b96b-109">StreamSets Data Collector provides a full-featured integrated development environment (IDE) that lets you design, test, deploy, and manage any-to-any ingest pipelines.</span><span class="sxs-lookup"><span data-stu-id="6b96b-109">StreamSets Data Collector provides a full-featured integrated development environment (IDE) that lets you design, test, deploy, and manage any-to-any ingest pipelines.</span></span> <span data-ttu-id="6b96b-110">These pipelines can mesh stream and batch data, and include a variety of in-stream transformations, all without having to write custom code.</span><span class="sxs-lookup"><span data-stu-id="6b96b-110">These pipelines can mesh stream and batch data, and include a variety of in-stream transformations, all without having to write custom code.</span></span>

<span data-ttu-id="6b96b-111">StreamSets Data Collector lets you build data flows using numerous Big Data components such as HDFS, Kafka, Solr, Hive, HBASE, and Kudu.</span><span class="sxs-lookup"><span data-stu-id="6b96b-111">StreamSets Data Collector lets you build data flows using numerous Big Data components such as HDFS, Kafka, Solr, Hive, HBASE, and Kudu.</span></span> <span data-ttu-id="6b96b-112">Once StreamSets Data Collector is running on an edge server, or in your Hadoop cluster, you get real-time monitoring for both data anomalies and data flow operations.</span><span class="sxs-lookup"><span data-stu-id="6b96b-112">Once StreamSets Data Collector is running on an edge server, or in your Hadoop cluster, you get real-time monitoring for both data anomalies and data flow operations.</span></span> <span data-ttu-id="6b96b-113">This monitoring includes threshold-based alerting, anomaly detection, and automatic remediation of error records.</span><span class="sxs-lookup"><span data-stu-id="6b96b-113">This monitoring includes threshold-based alerting, anomaly detection, and automatic remediation of error records.</span></span>

<span data-ttu-id="6b96b-114">StreamSets Data Collector is designed to logically isolate each stage in a pipeline, so you can meet new business requirements by dropping in new processors and connectors without coding and with minimal downtime.</span><span class="sxs-lookup"><span data-stu-id="6b96b-114">StreamSets Data Collector is designed to logically isolate each stage in a pipeline, so you can meet new business requirements by dropping in new processors and connectors without coding and with minimal downtime.</span></span>

### <a name="streamsets-resource-links"></a><span data-ttu-id="6b96b-115">StreamSets resource links</span><span class="sxs-lookup"><span data-stu-id="6b96b-115">StreamSets resource links</span></span>

* [<span data-ttu-id="6b96b-116">Documentation</span><span class="sxs-lookup"><span data-stu-id="6b96b-116">Documentation</span></span>](https://streamsets.com/documentation/datacollector/latest/help/#Getting_Started/GettingStarted_Title.html)
* [<span data-ttu-id="6b96b-117">Blog</span><span class="sxs-lookup"><span data-stu-id="6b96b-117">Blog</span></span>](https://streamsets.com/blog/)
* [<span data-ttu-id="6b96b-118">Tutorials</span><span class="sxs-lookup"><span data-stu-id="6b96b-118">Tutorials</span></span>](https://github.com/streamsets/tutorials)
* [<span data-ttu-id="6b96b-119">Developer Support Forum</span><span class="sxs-lookup"><span data-stu-id="6b96b-119">Developer Support Forum</span></span>](https://groups.google.com/a/streamsets.com/forum/#!forum/sdc-user)
* [<span data-ttu-id="6b96b-120">Slack Public StreamSets Channel</span><span class="sxs-lookup"><span data-stu-id="6b96b-120">Slack Public StreamSets Channel</span></span>](https://streamsetters.slack.com/)
* [<span data-ttu-id="6b96b-121">Source Code</span><span class="sxs-lookup"><span data-stu-id="6b96b-121">Source Code</span></span>](https://github.com/streamsets)

## <a name="prerequisites"></a><span data-ttu-id="6b96b-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6b96b-122">Prerequisites</span></span>

<span data-ttu-id="6b96b-123">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span><span class="sxs-lookup"><span data-stu-id="6b96b-123">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span></span>

* <span data-ttu-id="6b96b-124">Cluster tier(s): Standard or Premium</span><span class="sxs-lookup"><span data-stu-id="6b96b-124">Cluster tier(s): Standard or Premium</span></span>
* <span data-ttu-id="6b96b-125">Cluster version(s): 3.5 and above</span><span class="sxs-lookup"><span data-stu-id="6b96b-125">Cluster version(s): 3.5 and above</span></span>

## <a name="install-the-streamsets-data-collector-published-application"></a><span data-ttu-id="6b96b-126">Install the StreamSets Data Collector published application</span><span class="sxs-lookup"><span data-stu-id="6b96b-126">Install the StreamSets Data Collector published application</span></span>

<span data-ttu-id="6b96b-127">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6b96b-127">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span>

## <a name="launch-streamsets-data-collector"></a><span data-ttu-id="6b96b-128">Launch StreamSets Data Collector</span><span class="sxs-lookup"><span data-stu-id="6b96b-128">Launch StreamSets Data Collector</span></span>

1. <span data-ttu-id="6b96b-129">After installation, you can launch StreamSets from your cluster in Azure portal by going to the **Settings** pane, then selecting **Applications** under the **General** category.</span><span class="sxs-lookup"><span data-stu-id="6b96b-129">After installation, you can launch StreamSets from your cluster in Azure portal by going to the **Settings** pane, then selecting **Applications** under the **General** category.</span></span> <span data-ttu-id="6b96b-130">The Installed Apps pane lists the installed applications.</span><span class="sxs-lookup"><span data-stu-id="6b96b-130">The Installed Apps pane lists the installed applications.</span></span>

    ![Installed StreamSets app](./media/hdinsight-apps-install-streamsets/streamsets.png)

2. <span data-ttu-id="6b96b-132">When you select StreamSets Data Collector, you see a link to the web page, and the SSH endpoint path.</span><span class="sxs-lookup"><span data-stu-id="6b96b-132">When you select StreamSets Data Collector, you see a link to the web page, and the SSH endpoint path.</span></span> <span data-ttu-id="6b96b-133">Select the WEBPAGE link.</span><span class="sxs-lookup"><span data-stu-id="6b96b-133">Select the WEBPAGE link.</span></span>

3. <span data-ttu-id="6b96b-134">In the Login dialog box, use the following credentials to log in: `admin` and `admin`.</span><span class="sxs-lookup"><span data-stu-id="6b96b-134">In the Login dialog box, use the following credentials to log in: `admin` and `admin`.</span></span>

4. <span data-ttu-id="6b96b-135">On the Get Started page, click **Create New Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="6b96b-135">On the Get Started page, click **Create New Pipeline**.</span></span>

    ![Create new pipeline](./media/hdinsight-apps-install-streamsets/get-started.png)

5. <span data-ttu-id="6b96b-137">In the New Pipeline window, enter a name for the pipeline ("Hello World"), optionally enter a description, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6b96b-137">In the New Pipeline window, enter a name for the pipeline ("Hello World"), optionally enter a description, and select **Save**.</span></span>

6. <span data-ttu-id="6b96b-138">The Data Collector console is shown.</span><span class="sxs-lookup"><span data-stu-id="6b96b-138">The Data Collector console is shown.</span></span> <span data-ttu-id="6b96b-139">The Properties panel displays pipeline properties.</span><span class="sxs-lookup"><span data-stu-id="6b96b-139">The Properties panel displays pipeline properties.</span></span>
 
    ![Data Collector console](./media/hdinsight-apps-install-streamsets/pipeline-canvas.png)

7. <span data-ttu-id="6b96b-141">You are now ready to follow the [StreamSets tutorial](https://streamsets.com/documentation/datacollector/latest/help/#Tutorial/Tutorial-title.html).</span><span class="sxs-lookup"><span data-stu-id="6b96b-141">You are now ready to follow the [StreamSets tutorial](https://streamsets.com/documentation/datacollector/latest/help/#Tutorial/Tutorial-title.html).</span></span> <span data-ttu-id="6b96b-142">The tutorial provides step-by-step directions for creating your first pipeline.</span><span class="sxs-lookup"><span data-stu-id="6b96b-142">The tutorial provides step-by-step directions for creating your first pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b96b-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b96b-143">Next steps</span></span>

* <span data-ttu-id="6b96b-144">[StreamSets Data Collector documentation](https://streamsets.com/documentation/datacollector/latest/help/#Getting_Started/GettingStarted_Title.html#concept_htw_ghg_jq).</span><span class="sxs-lookup"><span data-stu-id="6b96b-144">[StreamSets Data Collector documentation](https://streamsets.com/documentation/datacollector/latest/help/#Getting_Started/GettingStarted_Title.html#concept_htw_ghg_jq).</span></span>
* <span data-ttu-id="6b96b-145">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b96b-145">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="6b96b-146">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6b96b-146">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="6b96b-147">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="6b96b-147">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="6b96b-148">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="6b96b-148">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="6b96b-149">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="6b96b-149">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span></span>
