---
title: Install published application - Datameer - Azure HDInsight
description: Install and use the Datameer third-party Hadoop application.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: 377dbadd7b696e62d8464258d22d0dd5ed926208
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865953"
---
# <a name="install-published-application---cask-data-application-platform-cdap"></a><span data-ttu-id="f4ea3-103">Install published application - Cask Data Application Platform (CDAP)</span><span class="sxs-lookup"><span data-stu-id="f4ea3-103">Install published application - Cask Data Application Platform (CDAP)</span></span>

<span data-ttu-id="f4ea3-104">This article describes how to install and run the [CDAP](http://cask.co/products/cdap/) published Hadoop application on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-104">This article describes how to install and run the [CDAP](http://cask.co/products/cdap/) published Hadoop application on Azure HDInsight.</span></span> <span data-ttu-id="f4ea3-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f4ea3-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span> <span data-ttu-id="f4ea3-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f4ea3-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>

## <a name="about-cdap"></a><span data-ttu-id="f4ea3-107">About CDAP</span><span class="sxs-lookup"><span data-stu-id="f4ea3-107">About CDAP</span></span>

<span data-ttu-id="f4ea3-108">Developing applications in Hadoop can be challenging.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-108">Developing applications in Hadoop can be challenging.</span></span>  <span data-ttu-id="f4ea3-109">There is a large and growing number of Hadoop technology extensions, which can take some time to integrate.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-109">There is a large and growing number of Hadoop technology extensions, which can take some time to integrate.</span></span> <span data-ttu-id="f4ea3-110">Monitoring data flow and collecting metrics can require building a separate solution.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-110">Monitoring data flow and collecting metrics can require building a separate solution.</span></span>

### <a name="how-does-cdap-help"></a><span data-ttu-id="f4ea3-111">How does CDAP help?</span><span class="sxs-lookup"><span data-stu-id="f4ea3-111">How does CDAP help?</span></span>

<span data-ttu-id="f4ea3-112">The Cask Data Application Platform (CDAP) is an integration platform for Big Data.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-112">The Cask Data Application Platform (CDAP) is an integration platform for Big Data.</span></span> <span data-ttu-id="f4ea3-113">CDAP enables you to focus on building applications rather than on the underlying infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-113">CDAP enables you to focus on building applications rather than on the underlying infrastructure.</span></span>

<span data-ttu-id="f4ea3-114">CDAP uses high-level concepts and abstractions that are familiar to developers.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-114">CDAP uses high-level concepts and abstractions that are familiar to developers.</span></span> <span data-ttu-id="f4ea3-115">These abstractions hide the complexities of internal systems and encourage reusability of solutions.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-115">These abstractions hide the complexities of internal systems and encourage reusability of solutions.</span></span>

<span data-ttu-id="f4ea3-116">A CDAP extension called [Cask Hydrator](http://cask.co/products/hydrator/) provides a user interface to develop and manage data pipelines.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-116">A CDAP extension called [Cask Hydrator](http://cask.co/products/hydrator/) provides a user interface to develop and manage data pipelines.</span></span> <span data-ttu-id="f4ea3-117">A data pipeline is composed of various \*plugins that perform tasks like data acquisition, transformation, analysis, and post-run operations.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-117">A data pipeline is composed of various \*plugins that perform tasks like data acquisition, transformation, analysis, and post-run operations.</span></span>

<span data-ttu-id="f4ea3-118">Each CDAP plugin has a well-defined interface so that evaluating different technologies is just a matter of replacing one plugin with another one, without having to touch the rest of the application.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-118">Each CDAP plugin has a well-defined interface so that evaluating different technologies is just a matter of replacing one plugin with another one, without having to touch the rest of the application.</span></span>

<span data-ttu-id="f4ea3-119">CDAP *pipelines* provide a high-level pictorial flow of the data in your application.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-119">CDAP *pipelines* provide a high-level pictorial flow of the data in your application.</span></span> <span data-ttu-id="f4ea3-120">This visualization shows the end-to-end flow of the data from ingestion, through the data transformations and analyses, and finally into an external data store.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-120">This visualization shows the end-to-end flow of the data from ingestion, through the data transformations and analyses, and finally into an external data store.</span></span>

<span data-ttu-id="f4ea3-121">The following example of a data pipeline ingests twitter data in real time, then filters out some tweets based on pre-defined criteria.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-121">The following example of a data pipeline ingests twitter data in real time, then filters out some tweets based on pre-defined criteria.</span></span> <span data-ttu-id="f4ea3-122">The data pipeline transforms raw tweet data and projects that data into a more readable format, then groups the tweets according to a set of values and writes the results into an HBase store.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-122">The data pipeline transforms raw tweet data and projects that data into a more readable format, then groups the tweets according to a set of values and writes the results into an HBase store.</span></span>

![CDAP pipeline](./media/hdinsight-apps-install-cask/pipeline.png)

<span data-ttu-id="f4ea3-124">This end-to-end pipeline is built using the **Cask Hydrator UI**, using its plugin interface and drag-and-drop functionality to form connections between each stage.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-124">This end-to-end pipeline is built using the **Cask Hydrator UI**, using its plugin interface and drag-and-drop functionality to form connections between each stage.</span></span> <span data-ttu-id="f4ea3-125">You can isolate and modify the functionality of each plugin independently.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-125">You can isolate and modify the functionality of each plugin independently.</span></span> <span data-ttu-id="f4ea3-126">Using CDAP, similar pipelines can be built and validated in hours.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-126">Using CDAP, similar pipelines can be built and validated in hours.</span></span> <span data-ttu-id="f4ea3-127">In the typical Hadoop world, constructing such solutions might take several days.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-127">In the typical Hadoop world, constructing such solutions might take several days.</span></span>

<span data-ttu-id="f4ea3-128">CDAP also provides an extension called [Cask Tracker](http://cask.co/products/tracker/) to visually trace data as it flows through the application.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-128">CDAP also provides an extension called [Cask Tracker](http://cask.co/products/tracker/) to visually trace data as it flows through the application.</span></span> <span data-ttu-id="f4ea3-129">Cask Tracker adds *data governance* to the system so that data assets are formally managed throughout the application.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-129">Cask Tracker adds *data governance* to the system so that data assets are formally managed throughout the application.</span></span> <span data-ttu-id="f4ea3-130">You can track each data point's lineage, collect relevant metrics, and audit the data trail throughout the process.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-130">You can track each data point's lineage, collect relevant metrics, and audit the data trail throughout the process.</span></span>

<span data-ttu-id="f4ea3-131">Here is an illustration of how data is flowing in the above pipeline:</span><span class="sxs-lookup"><span data-stu-id="f4ea3-131">Here is an illustration of how data is flowing in the above pipeline:</span></span>

![CDAP tracker](./media/hdinsight-apps-install-cask/tracker.png)

## <a name="prerequisites"></a><span data-ttu-id="f4ea3-133">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4ea3-133">Prerequisites</span></span>

<span data-ttu-id="f4ea3-134">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span><span class="sxs-lookup"><span data-stu-id="f4ea3-134">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span></span>

* <span data-ttu-id="f4ea3-135">Cluster tier: Standard</span><span class="sxs-lookup"><span data-stu-id="f4ea3-135">Cluster tier: Standard</span></span>
* <span data-ttu-id="f4ea3-136">Cluster type: HBase</span><span class="sxs-lookup"><span data-stu-id="f4ea3-136">Cluster type: HBase</span></span>
* <span data-ttu-id="f4ea3-137">Cluster version: 3.4, 3.5</span><span class="sxs-lookup"><span data-stu-id="f4ea3-137">Cluster version: 3.4, 3.5</span></span>

## <a name="install-the-cdap-published-application"></a><span data-ttu-id="f4ea3-138">Install the CDAP published application</span><span class="sxs-lookup"><span data-stu-id="f4ea3-138">Install the CDAP published application</span></span>

<span data-ttu-id="f4ea3-139">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f4ea3-139">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span>

## <a name="launch-cdap"></a><span data-ttu-id="f4ea3-140">Launch CDAP</span><span class="sxs-lookup"><span data-stu-id="f4ea3-140">Launch CDAP</span></span>

1. <span data-ttu-id="f4ea3-141">After installation, launch CDAP from your cluster in Azure portal by going to the **Settings** pane, then selecting **Applications** under the **General** category.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-141">After installation, launch CDAP from your cluster in Azure portal by going to the **Settings** pane, then selecting **Applications** under the **General** category.</span></span> <span data-ttu-id="f4ea3-142">The Installed Apps pane lists all the installed applications.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-142">The Installed Apps pane lists all the installed applications.</span></span>

    ![Installed CDAP app](./media/hdinsight-apps-install-cask/cdap-app.png)

2. <span data-ttu-id="f4ea3-144">When you select CDAP, you see a link to the web page and HTTP Endpoint, and also the SSH endpoint path.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-144">When you select CDAP, you see a link to the web page and HTTP Endpoint, and also the SSH endpoint path.</span></span> <span data-ttu-id="f4ea3-145">Select the WEBPAGE link.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-145">Select the WEBPAGE link.</span></span>

3. <span data-ttu-id="f4ea3-146">When prompted, enter your cluster administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-146">When prompted, enter your cluster administrator credentials.</span></span>

    ![Authentication](./media/hdinsight-apps-install-cask/auth.png)

4. <span data-ttu-id="f4ea3-148">After signing in, you see the Cask CDAP GUI home page.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-148">After signing in, you see the Cask CDAP GUI home page.</span></span>

    ![Cask GUI home page](./media/hdinsight-apps-install-cask/gui.png)

5. <span data-ttu-id="f4ea3-150">To explore the CDAP interface, click the **Cask Market** menu link on top of the page.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-150">To explore the CDAP interface, click the **Cask Market** menu link on top of the page.</span></span>

    ![Cask Market link](./media/hdinsight-apps-install-cask/cask-market.png)

6. <span data-ttu-id="f4ea3-152">Select **Access Log Sample** from the list.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-152">Select **Access Log Sample** from the list.</span></span>

    ![Access Log Sample](./media/hdinsight-apps-install-cask/market-log-sample.png)

7. <span data-ttu-id="f4ea3-154">Click **Load** to confirm.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-154">Click **Load** to confirm.</span></span>

    ![Click Load](./media/hdinsight-apps-install-cask/market-load.png)

8. <span data-ttu-id="f4ea3-156">A view of the included sample data is displayed.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-156">A view of the included sample data is displayed.</span></span> <span data-ttu-id="f4ea3-157">select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-157">select **Next**.</span></span>

    ![Access Log Sample - View Data](./media/hdinsight-apps-install-cask/market-view-data.png)

9. <span data-ttu-id="f4ea3-159">Select **Stream** as the Destination Type, enter a Destination Name, then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-159">Select **Stream** as the Destination Type, enter a Destination Name, then select **Finish**.</span></span>

    ![Access Log Sample - Select Destination](./media/hdinsight-apps-install-cask/market-destination.png)

10. <span data-ttu-id="f4ea3-161">After the datapack has been successfully loaded, select **View Stream Details**.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-161">After the datapack has been successfully loaded, select **View Stream Details**.</span></span>

    ![Datapack successfully uploaded](./media/hdinsight-apps-install-cask/market-view-details.png)

11. <span data-ttu-id="f4ea3-163">To enable metadata for the namespace, select **Enable** in the Usage tab on the Access Log details page.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-163">To enable metadata for the namespace, select **Enable** in the Usage tab on the Access Log details page.</span></span>

    ![Access Log Sample - Loaded - enable metadata](./media/hdinsight-apps-install-cask/log-loaded.png)

12. <span data-ttu-id="f4ea3-165">After metadata is enabled, you see a graph displaying audit message information.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-165">After metadata is enabled, you see a graph displaying audit message information.</span></span>

    ![Access Log Sample - Metadata enabled](./media/hdinsight-apps-install-cask/log-metadata.png)

13. <span data-ttu-id="f4ea3-167">To explore the log data, select the **Explore** icon on top of the page.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-167">To explore the log data, select the **Explore** icon on top of the page.</span></span>

    ![Access Log Sample - Explore](./media/hdinsight-apps-install-cask/log-explore.png)

14. <span data-ttu-id="f4ea3-169">You see a sample SQL query.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-169">You see a sample SQL query.</span></span> <span data-ttu-id="f4ea3-170">Feel free to modify it as desired, then select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-170">Feel free to modify it as desired, then select **Execute**.</span></span>

    ![Access Log Sample - Explore dataset with a query](./media/hdinsight-apps-install-cask/log-query.png)

15. <span data-ttu-id="f4ea3-172">After the query has finished, select the **View** icon under the Actions column.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-172">After the query has finished, select the **View** icon under the Actions column.</span></span>

    ![Access Log Sample - View completed query](./media/hdinsight-apps-install-cask/log-query-view.png)

16. <span data-ttu-id="f4ea3-174">You see the query results.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-174">You see the query results.</span></span>

    ![Access Log Sample - Query results](./media/hdinsight-apps-install-cask/log-query-results.png)

## <a name="next-steps"></a><span data-ttu-id="f4ea3-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4ea3-176">Next steps</span></span>

* <span data-ttu-id="f4ea3-177">[Cask documentation](http://cask.co/resources/documentation/).</span><span class="sxs-lookup"><span data-stu-id="f4ea3-177">[Cask documentation](http://cask.co/resources/documentation/).</span></span>
* <span data-ttu-id="f4ea3-178">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-178">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="f4ea3-179">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-179">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="f4ea3-180">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-180">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="f4ea3-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="f4ea3-182">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="f4ea3-182">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span></span>
