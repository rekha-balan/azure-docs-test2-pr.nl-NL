---
title: Visualize Interactive Query Hive data with Power BI in Azure HDInsight
description: Learn how to use Microsoft Power BI to visualize Interactive Query Hive data processed by Azure HDInsight.
keywords: hdinsight,hadoop,hive,interactive query,interactive hive,LLAP,directquery
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 03/14/2018
ms.openlocfilehash: 1779151f3768542c08ea62d2c9109d4cd66a1e3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869560"
---
# <a name="visualize-interactive-query-hive-data-with-microsoft-power-bi-using-direct-query-in-azure-hdinsight"></a><span data-ttu-id="49e01-104">Visualize Interactive Query Hive data with Microsoft Power BI using direct query in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="49e01-104">Visualize Interactive Query Hive data with Microsoft Power BI using direct query in Azure HDInsight</span></span>

<span data-ttu-id="49e01-105">Learn how to connect Microsoft Power BI to Azure HDInsight Interactive Query clusters and visualize the Hive data using direct query.</span><span class="sxs-lookup"><span data-stu-id="49e01-105">Learn how to connect Microsoft Power BI to Azure HDInsight Interactive Query clusters and visualize the Hive data using direct query.</span></span> <span data-ttu-id="49e01-106">In this tutorial, you load the data from a hivesampletable Hive table to Power BI.</span><span class="sxs-lookup"><span data-stu-id="49e01-106">In this tutorial, you load the data from a hivesampletable Hive table to Power BI.</span></span> <span data-ttu-id="49e01-107">The Hive table contains some mobile phone usage data.</span><span class="sxs-lookup"><span data-stu-id="49e01-107">The Hive table contains some mobile phone usage data.</span></span> <span data-ttu-id="49e01-108">Then you plot the usage data on a world map:</span><span class="sxs-lookup"><span data-stu-id="49e01-108">Then you plot the usage data on a world map:</span></span>

![HDInsight Power BI the map report](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-power-bi-visualization.png)

<span data-ttu-id="49e01-110">You can leverage the [Hive ODBC driver](../hadoop/apache-hadoop-connect-hive-power-bi.md) to do import via the generic ODBC connector in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="49e01-110">You can leverage the [Hive ODBC driver](../hadoop/apache-hadoop-connect-hive-power-bi.md) to do import via the generic ODBC connector in Power BI Desktop.</span></span> <span data-ttu-id="49e01-111">However it is not recommended for BI workloads given non-interactive nature of the Hive query engine.</span><span class="sxs-lookup"><span data-stu-id="49e01-111">However it is not recommended for BI workloads given non-interactive nature of the Hive query engine.</span></span> <span data-ttu-id="49e01-112">[HDInsight Interactive Query connector](./apache-hadoop-connect-hive-power-bi-directquery.md) and [HDInsight Spark connector](https://docs.microsoft.com/power-bi/spark-on-hdinsight-with-direct-connect) are better choices for their performance.</span><span class="sxs-lookup"><span data-stu-id="49e01-112">[HDInsight Interactive Query connector](./apache-hadoop-connect-hive-power-bi-directquery.md) and [HDInsight Spark connector](https://docs.microsoft.com/power-bi/spark-on-hdinsight-with-direct-connect) are better choices for their performance.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49e01-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49e01-113">Prerequisites</span></span>
<span data-ttu-id="49e01-114">Before going through this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="49e01-114">Before going through this article, you must have the following items:</span></span>

* <span data-ttu-id="49e01-115">**HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="49e01-115">**HDInsight cluster**.</span></span> <span data-ttu-id="49e01-116">The cluster can be either an HDInsight cluster with Hive or a newly released Interactive Query cluster.</span><span class="sxs-lookup"><span data-stu-id="49e01-116">The cluster can be either an HDInsight cluster with Hive or a newly released Interactive Query cluster.</span></span> <span data-ttu-id="49e01-117">For creating clusters, see [Create cluster](../hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="49e01-117">For creating clusters, see [Create cluster](../hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>
* <span data-ttu-id="49e01-118">**[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)**.</span><span class="sxs-lookup"><span data-stu-id="49e01-118">**[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)**.</span></span> <span data-ttu-id="49e01-119">You can download a copy from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="49e01-119">You can download a copy from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45331).</span></span>

## <a name="load-data-from-hdinsight"></a><span data-ttu-id="49e01-120">Load data from HDInsight</span><span class="sxs-lookup"><span data-stu-id="49e01-120">Load data from HDInsight</span></span>

<span data-ttu-id="49e01-121">The hivesampletable Hive table comes with all HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="49e01-121">The hivesampletable Hive table comes with all HDInsight clusters.</span></span>

1. <span data-ttu-id="49e01-122">Sign in to Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="49e01-122">Sign in to Power BI Desktop.</span></span>
2. <span data-ttu-id="49e01-123">Click the **Home** tab, click **Get Data** from the **External data** ribbon, and then select **More**.</span><span class="sxs-lookup"><span data-stu-id="49e01-123">Click the **Home** tab, click **Get Data** from the **External data** ribbon, and then select **More**.</span></span>

    ![HDInsight Power BI open data](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-power-bi-open-odbc.png)
3. <span data-ttu-id="49e01-125">From the **Get Data** pane, type **hdinsight** in the search box.</span><span class="sxs-lookup"><span data-stu-id="49e01-125">From the **Get Data** pane, type **hdinsight** in the search box.</span></span> <span data-ttu-id="49e01-126">If you don't see **HDInsight Interactive Query (Beta)**, you need to update your Power BI Desktop to the latest version.</span><span class="sxs-lookup"><span data-stu-id="49e01-126">If you don't see **HDInsight Interactive Query (Beta)**, you need to update your Power BI Desktop to the latest version.</span></span>
4. <span data-ttu-id="49e01-127">Click **HDInsight Interactive Query (Beta)**, and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="49e01-127">Click **HDInsight Interactive Query (Beta)**, and then click **Connect**.</span></span>
5. <span data-ttu-id="49e01-128">Click **Continue** to close the **Preview connector** warning dialog.</span><span class="sxs-lookup"><span data-stu-id="49e01-128">Click **Continue** to close the **Preview connector** warning dialog.</span></span>
6. <span data-ttu-id="49e01-129">From **HDInsight Interactive Query**, select or enter the following information:</span><span class="sxs-lookup"><span data-stu-id="49e01-129">From **HDInsight Interactive Query**, select or enter the following information:</span></span>

    - <span data-ttu-id="49e01-130">**Server**: Enter the Interactive Query cluster name, for example *myiqcluster.azurehdinsight.net*.</span><span class="sxs-lookup"><span data-stu-id="49e01-130">**Server**: Enter the Interactive Query cluster name, for example *myiqcluster.azurehdinsight.net*.</span></span>
    - <span data-ttu-id="49e01-131">**Database**: For this tutorial, enter **default**.</span><span class="sxs-lookup"><span data-stu-id="49e01-131">**Database**: For this tutorial, enter **default**.</span></span>
    - <span data-ttu-id="49e01-132">**Data Connectivity mode**: For this tutorial, select **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="49e01-132">**Data Connectivity mode**: For this tutorial, select **DirectQuery**.</span></span>

    ![HDInsight interactive query power bi directquery connect](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-interactive-query-power-bi-connect.png)
7. <span data-ttu-id="49e01-134">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49e01-134">Click **OK**.</span></span>
8. <span data-ttu-id="49e01-135">Enter the HTTP user credential, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49e01-135">Enter the HTTP user credential, and then click **OK**.</span></span>  <span data-ttu-id="49e01-136">The default username is **admin**</span><span class="sxs-lookup"><span data-stu-id="49e01-136">The default username is **admin**</span></span>
9. <span data-ttu-id="49e01-137">From the left pane, select **hivesampletale**, and then click **Load**.</span><span class="sxs-lookup"><span data-stu-id="49e01-137">From the left pane, select **hivesampletale**, and then click **Load**.</span></span>

    ![HDInsight interactive query power bi hivesampletable](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-interactive-query-power-bi-hivesampletable.png)

## <a name="visualize-data"></a><span data-ttu-id="49e01-139">Visualize data</span><span class="sxs-lookup"><span data-stu-id="49e01-139">Visualize data</span></span>

<span data-ttu-id="49e01-140">Continue from the last procedure.</span><span class="sxs-lookup"><span data-stu-id="49e01-140">Continue from the last procedure.</span></span>

1. <span data-ttu-id="49e01-141">From the Visualizations pane, select **Map**.</span><span class="sxs-lookup"><span data-stu-id="49e01-141">From the Visualizations pane, select **Map**.</span></span>  <span data-ttu-id="49e01-142">It is a globe icon.</span><span class="sxs-lookup"><span data-stu-id="49e01-142">It is a globe icon.</span></span>

    ![HDInsight Power BI customizes report](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-power-bi-customize.png)
2. <span data-ttu-id="49e01-144">From the Fields pane, select **country** and **devicemake**.</span><span class="sxs-lookup"><span data-stu-id="49e01-144">From the Fields pane, select **country** and **devicemake**.</span></span> <span data-ttu-id="49e01-145">You can see the data plotted on the map.</span><span class="sxs-lookup"><span data-stu-id="49e01-145">You can see the data plotted on the map.</span></span>
3. <span data-ttu-id="49e01-146">Expand the map.</span><span class="sxs-lookup"><span data-stu-id="49e01-146">Expand the map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49e01-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="49e01-147">Next steps</span></span>
<span data-ttu-id="49e01-148">In this article, you learned how to visualize data from HDInsight using Power BI.</span><span class="sxs-lookup"><span data-stu-id="49e01-148">In this article, you learned how to visualize data from HDInsight using Power BI.</span></span>  <span data-ttu-id="49e01-149">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="49e01-149">To learn more, see the following articles:</span></span>

* <span data-ttu-id="49e01-150">[Visualize Hive data with Microsoft Power BI using ODBC in Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-150">[Visualize Hive data with Microsoft Power BI using ODBC in Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md).</span></span> 
* <span data-ttu-id="49e01-151">[Use Zeppelin to run Hive queries in Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-151">[Use Zeppelin to run Hive queries in Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).</span></span>
* <span data-ttu-id="49e01-152">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-152">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span></span>
* <span data-ttu-id="49e01-153">[Connect Excel to Hadoop by using Power Query](../hadoop/apache-hadoop-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-153">[Connect Excel to Hadoop by using Power Query](../hadoop/apache-hadoop-connect-excel-power-query.md).</span></span>
* <span data-ttu-id="49e01-154">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-154">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>
* <span data-ttu-id="49e01-155">[Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-155">[Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).</span></span>
* <span data-ttu-id="49e01-156">[Upload Data to HDInsight](./../hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="49e01-156">[Upload Data to HDInsight](./../hdinsight-upload-data.md).</span></span>
