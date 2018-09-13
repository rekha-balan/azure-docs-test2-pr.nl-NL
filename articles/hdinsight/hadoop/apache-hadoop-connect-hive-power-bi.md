---
title: Visualize big data with Power BI in Azure HDInsight
description: Learn how to use Microsoft Power BI to visualize Hive data processed by Azure HDInsight.
keywords: hdinsight,hadoop,hive,interactive query,interactive hive,LLAP,odbc
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: c24818f6b746754111540bae5fbf7f21d22c3a61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965796"
---
# <a name="visualize-hive-data-with-microsoft-power-bi-using-odbc-in-azure-hdinsight"></a><span data-ttu-id="874fd-104">Visualize Hive data with Microsoft Power BI using ODBC in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="874fd-104">Visualize Hive data with Microsoft Power BI using ODBC in Azure HDInsight</span></span>

<span data-ttu-id="874fd-105">Learn how to connect Microsoft Power BI to Azure HDInsight using ODBC and visualize the Hive data.</span><span class="sxs-lookup"><span data-stu-id="874fd-105">Learn how to connect Microsoft Power BI to Azure HDInsight using ODBC and visualize the Hive data.</span></span> 

>[!IMPORTANT]
> <span data-ttu-id="874fd-106">You can leverage the Hive ODBC driver to do import via the generic ODBC connector in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="874fd-106">You can leverage the Hive ODBC driver to do import via the generic ODBC connector in Power BI Desktop.</span></span> <span data-ttu-id="874fd-107">However it is not recommended for BI workloads given non-interactive nature of the Hive query engine.</span><span class="sxs-lookup"><span data-stu-id="874fd-107">However it is not recommended for BI workloads given non-interactive nature of the Hive query engine.</span></span> <span data-ttu-id="874fd-108">[HDInsight Interactive Query connector](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md) and [HDInsight Spark connector](https://docs.microsoft.com/power-bi/spark-on-hdinsight-with-direct-connect) are better choices for their performance.</span><span class="sxs-lookup"><span data-stu-id="874fd-108">[HDInsight Interactive Query connector](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md) and [HDInsight Spark connector](https://docs.microsoft.com/power-bi/spark-on-hdinsight-with-direct-connect) are better choices for their performance.</span></span>

<span data-ttu-id="874fd-109">In this tutorial, you load the data from a hivesampletable Hive table to Power BI.</span><span class="sxs-lookup"><span data-stu-id="874fd-109">In this tutorial, you load the data from a hivesampletable Hive table to Power BI.</span></span> <span data-ttu-id="874fd-110">The Hive table contains some mobile phone usage data.</span><span class="sxs-lookup"><span data-stu-id="874fd-110">The Hive table contains some mobile phone usage data.</span></span> <span data-ttu-id="874fd-111">Then you plot the usage data on a world map:</span><span class="sxs-lookup"><span data-stu-id="874fd-111">Then you plot the usage data on a world map:</span></span>

![HDInsight Power BI the map report](./media/apache-hadoop-connect-hive-power-bi/hdinsight-power-bi-visualization.png)

<span data-ttu-id="874fd-113">The information also applies to the new [Interactive Query](../interactive-query/apache-interactive-query-get-started.md) cluster type.</span><span class="sxs-lookup"><span data-stu-id="874fd-113">The information also applies to the new [Interactive Query](../interactive-query/apache-interactive-query-get-started.md) cluster type.</span></span> <span data-ttu-id="874fd-114">For how to connect to HDInsight Interactive Query using direct query, see [Visualize Interactive Query Hive data with Microsoft Power BI using direct query in Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-114">For how to connect to HDInsight Interactive Query using direct query, see [Visualize Interactive Query Hive data with Microsoft Power BI using direct query in Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span></span>



## <a name="prerequisites"></a><span data-ttu-id="874fd-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="874fd-115">Prerequisites</span></span>
<span data-ttu-id="874fd-116">Before going through this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="874fd-116">Before going through this article, you must have the following items:</span></span>

* <span data-ttu-id="874fd-117">**HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="874fd-117">**HDInsight cluster**.</span></span> <span data-ttu-id="874fd-118">The cluster can be either a HDInsight cluster with Hive or a newly released Interactive Query cluster.</span><span class="sxs-lookup"><span data-stu-id="874fd-118">The cluster can be either a HDInsight cluster with Hive or a newly released Interactive Query cluster.</span></span> <span data-ttu-id="874fd-119">For creating clusters, see [Create cluster](apache-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="874fd-119">For creating clusters, see [Create cluster](apache-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>
* <span data-ttu-id="874fd-120">**[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)**.</span><span class="sxs-lookup"><span data-stu-id="874fd-120">**[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)**.</span></span> <span data-ttu-id="874fd-121">You can download a copy from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="874fd-121">You can download a copy from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45331).</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="874fd-122">Create Hive ODBC data source</span><span class="sxs-lookup"><span data-stu-id="874fd-122">Create Hive ODBC data source</span></span>

<span data-ttu-id="874fd-123">See [Create Hive ODBC data source](apache-hadoop-connect-excel-hive-odbc-driver.md#create-hive-odbc-data-source).</span><span class="sxs-lookup"><span data-stu-id="874fd-123">See [Create Hive ODBC data source](apache-hadoop-connect-excel-hive-odbc-driver.md#create-hive-odbc-data-source).</span></span>

## <a name="load-data-from-hdinsight"></a><span data-ttu-id="874fd-124">Load data from HDInsight</span><span class="sxs-lookup"><span data-stu-id="874fd-124">Load data from HDInsight</span></span>

<span data-ttu-id="874fd-125">The hivesampletable Hive table comes with all HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="874fd-125">The hivesampletable Hive table comes with all HDInsight clusters.</span></span>

1. <span data-ttu-id="874fd-126">Sign in to Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="874fd-126">Sign in to Power BI Desktop.</span></span>
2. <span data-ttu-id="874fd-127">Click the **Home** tab, click **Get Data** from the **External data** ribbon, and then select **More**.</span><span class="sxs-lookup"><span data-stu-id="874fd-127">Click the **Home** tab, click **Get Data** from the **External data** ribbon, and then select **More**.</span></span>

    ![HDInsight Power BI open data](./media/apache-hadoop-connect-hive-power-bi/hdinsight-power-bi-open-odbc.png)
3. <span data-ttu-id="874fd-129">From the **Get Data** pane, click **Other** from the left, click **ODBC** from the right, and then click **Connect** on the bottom.</span><span class="sxs-lookup"><span data-stu-id="874fd-129">From the **Get Data** pane, click **Other** from the left, click **ODBC** from the right, and then click **Connect** on the bottom.</span></span>
4. <span data-ttu-id="874fd-130">From the **From ODBC** pane, select the data source name you created in the last section, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="874fd-130">From the **From ODBC** pane, select the data source name you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="874fd-131">From the **Navigator** pane, expand **ODBC->HIVE->default**, select **hivesampletable**, and then click **Load**.</span><span class="sxs-lookup"><span data-stu-id="874fd-131">From the **Navigator** pane, expand **ODBC->HIVE->default**, select **hivesampletable**, and then click **Load**.</span></span>

## <a name="visualize-data"></a><span data-ttu-id="874fd-132">Visualize data</span><span class="sxs-lookup"><span data-stu-id="874fd-132">Visualize data</span></span>

<span data-ttu-id="874fd-133">Continue from the last procedure.</span><span class="sxs-lookup"><span data-stu-id="874fd-133">Continue from the last procedure.</span></span>

1. <span data-ttu-id="874fd-134">From the Visualizations pane, select **Map**.</span><span class="sxs-lookup"><span data-stu-id="874fd-134">From the Visualizations pane, select **Map**.</span></span>  <span data-ttu-id="874fd-135">It is a globe icon.</span><span class="sxs-lookup"><span data-stu-id="874fd-135">It is a globe icon.</span></span>

    ![HDInsight Power BI customizes report](./media/apache-hadoop-connect-hive-power-bi/hdinsight-power-bi-customize.png)
2. <span data-ttu-id="874fd-137">From the Fields pane, select **country** and **devicemake**.</span><span class="sxs-lookup"><span data-stu-id="874fd-137">From the Fields pane, select **country** and **devicemake**.</span></span> <span data-ttu-id="874fd-138">You can see the data plotted on the map.</span><span class="sxs-lookup"><span data-stu-id="874fd-138">You can see the data plotted on the map.</span></span>
3. <span data-ttu-id="874fd-139">Expand the map.</span><span class="sxs-lookup"><span data-stu-id="874fd-139">Expand the map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="874fd-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="874fd-140">Next steps</span></span>
<span data-ttu-id="874fd-141">In this article, you learned how to visualize data from HDInsight using Power BI.</span><span class="sxs-lookup"><span data-stu-id="874fd-141">In this article, you learned how to visualize data from HDInsight using Power BI.</span></span>  <span data-ttu-id="874fd-142">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="874fd-142">To learn more, see the following articles:</span></span>

* <span data-ttu-id="874fd-143">[Use Zeppelin to run Hive queries in Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-143">[Use Zeppelin to run Hive queries in Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).</span></span>
* <span data-ttu-id="874fd-144">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](./apache-hadoop-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-144">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](./apache-hadoop-connect-excel-hive-odbc-driver.md).</span></span>
* <span data-ttu-id="874fd-145">[Connect Excel to Hadoop by using Power Query](apache-hadoop-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-145">[Connect Excel to Hadoop by using Power Query](apache-hadoop-connect-excel-power-query.md).</span></span>
* <span data-ttu-id="874fd-146">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-146">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](apache-hadoop-visual-studio-tools-get-started.md).</span></span>
* <span data-ttu-id="874fd-147">[Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-147">[Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).</span></span>
* <span data-ttu-id="874fd-148">[Upload Data to HDInsight](./../hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="874fd-148">[Upload Data to HDInsight](./../hdinsight-upload-data.md).</span></span>
