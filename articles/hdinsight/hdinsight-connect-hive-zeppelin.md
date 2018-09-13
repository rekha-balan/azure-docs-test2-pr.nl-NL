---
title: Use Zeppelin to run Hive queries in Azure HDInsight
description: Learn how to use Zeppelin to run Hive queries.
keywords: hdinsight,hadoop,hive,interactive query,LLAP
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,
ms.topic: conceptual
ms.date: 05/14/2018
ms.author: jasonh
ms.openlocfilehash: 3064c9cd141458307891f666bd5af9aa738cc021
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870702"
---
# <a name="use-zeppelin-to-run-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="3be76-104">Use Zeppelin to run Hive queries in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3be76-104">Use Zeppelin to run Hive queries in Azure HDInsight</span></span> 

<span data-ttu-id="3be76-105">HDInsight Interactive Query clusters include Zeppelin notebooks that you can use to run interactive Hive queries.</span><span class="sxs-lookup"><span data-stu-id="3be76-105">HDInsight Interactive Query clusters include Zeppelin notebooks that you can use to run interactive Hive queries.</span></span> <span data-ttu-id="3be76-106">In this article, you learn how to use Zeppelin to run Hive queries in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3be76-106">In this article, you learn how to use Zeppelin to run Hive queries in Azure HDInsight.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3be76-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3be76-107">Prerequisites</span></span>
<span data-ttu-id="3be76-108">Before going through this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="3be76-108">Before going through this article, you must have the following items:</span></span>

* <span data-ttu-id="3be76-109">**HDInsight Interactive Query cluster**.</span><span class="sxs-lookup"><span data-stu-id="3be76-109">**HDInsight Interactive Query cluster**.</span></span> <span data-ttu-id="3be76-110">See [Create cluster](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster) to create a HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3be76-110">See [Create cluster](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster) to create a HDInsight cluster.</span></span>  <span data-ttu-id="3be76-111">Make sure to choose the Interactive Query type.</span><span class="sxs-lookup"><span data-stu-id="3be76-111">Make sure to choose the Interactive Query type.</span></span> 

## <a name="create-a-zeppelin-note"></a><span data-ttu-id="3be76-112">Create a Zeppelin Note</span><span class="sxs-lookup"><span data-stu-id="3be76-112">Create a Zeppelin Note</span></span>

1. <span data-ttu-id="3be76-113">Browse to the following URL:</span><span class="sxs-lookup"><span data-stu-id="3be76-113">Browse to the following URL:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/zeppelin
    <span data-ttu-id="3be76-114">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="3be76-114">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

2. <span data-ttu-id="3be76-115">Enter your Hadoop username and password.</span><span class="sxs-lookup"><span data-stu-id="3be76-115">Enter your Hadoop username and password.</span></span> <span data-ttu-id="3be76-116">From the Zeppelin page, you can either create a new note or open existing notes.</span><span class="sxs-lookup"><span data-stu-id="3be76-116">From the Zeppelin page, you can either create a new note or open existing notes.</span></span> <span data-ttu-id="3be76-117">HiveSample contains some sample Hive queries.</span><span class="sxs-lookup"><span data-stu-id="3be76-117">HiveSample contains some sample Hive queries.</span></span>  

    ![HDInsight Interactive Query zeppelin](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin.png)
3. <span data-ttu-id="3be76-119">Click **Create new Note**.</span><span class="sxs-lookup"><span data-stu-id="3be76-119">Click **Create new Note**.</span></span>
4. <span data-ttu-id="3be76-120">Type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="3be76-120">Type or select the following values:</span></span>

    - <span data-ttu-id="3be76-121">Note name: enter a name for the note.</span><span class="sxs-lookup"><span data-stu-id="3be76-121">Note name: enter a name for the note.</span></span>
    - <span data-ttu-id="3be76-122">Default interpreter: select **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="3be76-122">Default interpreter: select **JDBC**.</span></span>

5. <span data-ttu-id="3be76-123">Click **Create Note**.</span><span class="sxs-lookup"><span data-stu-id="3be76-123">Click **Create Note**.</span></span>
6. <span data-ttu-id="3be76-124">Run the following Hive query:</span><span class="sxs-lookup"><span data-stu-id="3be76-124">Run the following Hive query:</span></span>

        %jdbc(hive)
        show tables

    ![HDInsight Interactive Query zeppelin runs query](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin-query.png)

    <span data-ttu-id="3be76-126">The **%jdbc(hive)** statement in the first line tells the notebook to use the Hive JDBC interpreter.</span><span class="sxs-lookup"><span data-stu-id="3be76-126">The **%jdbc(hive)** statement in the first line tells the notebook to use the Hive JDBC interpreter.</span></span>

    <span data-ttu-id="3be76-127">The query shall return one Hive table called *hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="3be76-127">The query shall return one Hive table called *hivesampletable*.</span></span>

    <span data-ttu-id="3be76-128">The following are two more Hive queries that you can run against the hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="3be76-128">The following are two more Hive queries that you can run against the hivesampletable.</span></span> 

        %jdbc(hive)
        select * from hivesampletable limit 10

        %jdbc(hive)
        select ${group_name}, count(*) as total_count
        from hivesampletable
        group by ${group_name=market,market|deviceplatform|devicemake}
        limit ${total_count=10}

    <span data-ttu-id="3be76-129">Comparing to the traditional Hive, the query results come back must faster.</span><span class="sxs-lookup"><span data-stu-id="3be76-129">Comparing to the traditional Hive, the query results come back must faster.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3be76-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="3be76-130">Next steps</span></span>
<span data-ttu-id="3be76-131">In this article, you learned how to visualize data from HDInsight using Power BI.</span><span class="sxs-lookup"><span data-stu-id="3be76-131">In this article, you learned how to visualize data from HDInsight using Power BI.</span></span>  <span data-ttu-id="3be76-132">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="3be76-132">To learn more, see the following articles:</span></span>

* <span data-ttu-id="3be76-133">[Visualize Hive data with Microsoft Power BI in Azure HDInsight](hadoop/apache-hadoop-connect-hive-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-133">[Visualize Hive data with Microsoft Power BI in Azure HDInsight](hadoop/apache-hadoop-connect-hive-power-bi.md).</span></span>
* <span data-ttu-id="3be76-134">[Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-134">[Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span></span>
* <span data-ttu-id="3be76-135">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-135">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span></span>
* <span data-ttu-id="3be76-136">[Connect Excel to Hadoop by using Power Query](hadoop/apache-hadoop-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-136">[Connect Excel to Hadoop by using Power Query](hadoop/apache-hadoop-connect-excel-power-query.md).</span></span>
* <span data-ttu-id="3be76-137">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-137">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>
* <span data-ttu-id="3be76-138">[Use Azure HDInsight Tool for Visual Studio Code](hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-138">[Use Azure HDInsight Tool for Visual Studio Code](hdinsight-for-vscode.md).</span></span>
* <span data-ttu-id="3be76-139">[Upload Data to HDInsight](./hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="3be76-139">[Upload Data to HDInsight](./hdinsight-upload-data.md).</span></span>
