---
title: Operationalize a data analytics pipeline - Azure
description: Set up and run an example data pipeline that is triggered by new data and produces concise results.
services: hdinsight
ms.service: hdinsight
author: ashishthaps
ms.author: ashishth
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/11/2018
ms.openlocfilehash: 9057d9f5d63598ea249e8f3193b84fd715018829
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969499"
---
# <a name="operationalize-a-data-analytics-pipeline"></a><span data-ttu-id="0f2ed-103">Operationalize a data analytics pipeline</span><span class="sxs-lookup"><span data-stu-id="0f2ed-103">Operationalize a data analytics pipeline</span></span>

<span data-ttu-id="0f2ed-104">*Data pipelines* underly many data analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-104">*Data pipelines* underly many data analytics solutions.</span></span> <span data-ttu-id="0f2ed-105">As the name suggests, a data pipeline takes in raw data, cleans and reshapes it as needed, and then typically performs calculations or aggregations before storing the processed data.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-105">As the name suggests, a data pipeline takes in raw data, cleans and reshapes it as needed, and then typically performs calculations or aggregations before storing the processed data.</span></span> <span data-ttu-id="0f2ed-106">The processed data is consumed by clients, reports, or APIs.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-106">The processed data is consumed by clients, reports, or APIs.</span></span> <span data-ttu-id="0f2ed-107">A data pipeline must provide repeatable results, whether on a schedule or when triggered by new data.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-107">A data pipeline must provide repeatable results, whether on a schedule or when triggered by new data.</span></span>

<span data-ttu-id="0f2ed-108">This article describes how to operationalize your data pipelines for repeatability, using Oozie running on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-108">This article describes how to operationalize your data pipelines for repeatability, using Oozie running on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0f2ed-109">The example scenario walks you through a data pipeline that prepares and processes airline flight time-series data.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-109">The example scenario walks you through a data pipeline that prepares and processes airline flight time-series data.</span></span>

<span data-ttu-id="0f2ed-110">In the following scenario, the input data is a flat file containing a batch of flight data for one month.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-110">In the following scenario, the input data is a flat file containing a batch of flight data for one month.</span></span> <span data-ttu-id="0f2ed-111">This flight data includes information such as the origin and destination airport, the miles flown, the departure and arrival times, and so forth.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-111">This flight data includes information such as the origin and destination airport, the miles flown, the departure and arrival times, and so forth.</span></span> <span data-ttu-id="0f2ed-112">The goal with this pipeline is to summarize daily airline performance, where each airline has one row for each day with the average departure and arrival delays in minutes, and the total miles flown that day.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-112">The goal with this pipeline is to summarize daily airline performance, where each airline has one row for each day with the average departure and arrival delays in minutes, and the total miles flown that day.</span></span>

| <span data-ttu-id="0f2ed-113">YEAR</span><span class="sxs-lookup"><span data-stu-id="0f2ed-113">YEAR</span></span> | <span data-ttu-id="0f2ed-114">MONTH</span><span class="sxs-lookup"><span data-stu-id="0f2ed-114">MONTH</span></span> | <span data-ttu-id="0f2ed-115">DAY_OF_MONTH</span><span class="sxs-lookup"><span data-stu-id="0f2ed-115">DAY_OF_MONTH</span></span> | <span data-ttu-id="0f2ed-116">CARRIER</span><span class="sxs-lookup"><span data-stu-id="0f2ed-116">CARRIER</span></span> |<span data-ttu-id="0f2ed-117">AVG_DEP_DELAY</span><span class="sxs-lookup"><span data-stu-id="0f2ed-117">AVG_DEP_DELAY</span></span> | <span data-ttu-id="0f2ed-118">AVG_ARR_DELAY</span><span class="sxs-lookup"><span data-stu-id="0f2ed-118">AVG_ARR_DELAY</span></span> |<span data-ttu-id="0f2ed-119">TOTAL_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="0f2ed-119">TOTAL_DISTANCE</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0f2ed-120">2017</span><span class="sxs-lookup"><span data-stu-id="0f2ed-120">2017</span></span> | <span data-ttu-id="0f2ed-121">1</span><span class="sxs-lookup"><span data-stu-id="0f2ed-121">1</span></span> | <span data-ttu-id="0f2ed-122">3</span><span class="sxs-lookup"><span data-stu-id="0f2ed-122">3</span></span> | <span data-ttu-id="0f2ed-123">AA</span><span class="sxs-lookup"><span data-stu-id="0f2ed-123">AA</span></span> | <span data-ttu-id="0f2ed-124">10.142229</span><span class="sxs-lookup"><span data-stu-id="0f2ed-124">10.142229</span></span> | <span data-ttu-id="0f2ed-125">7.862926</span><span class="sxs-lookup"><span data-stu-id="0f2ed-125">7.862926</span></span> | <span data-ttu-id="0f2ed-126">2644539</span><span class="sxs-lookup"><span data-stu-id="0f2ed-126">2644539</span></span> |
| <span data-ttu-id="0f2ed-127">2017</span><span class="sxs-lookup"><span data-stu-id="0f2ed-127">2017</span></span> | <span data-ttu-id="0f2ed-128">1</span><span class="sxs-lookup"><span data-stu-id="0f2ed-128">1</span></span> | <span data-ttu-id="0f2ed-129">3</span><span class="sxs-lookup"><span data-stu-id="0f2ed-129">3</span></span> | <span data-ttu-id="0f2ed-130">AS</span><span class="sxs-lookup"><span data-stu-id="0f2ed-130">AS</span></span> | <span data-ttu-id="0f2ed-131">9.435449</span><span class="sxs-lookup"><span data-stu-id="0f2ed-131">9.435449</span></span> | <span data-ttu-id="0f2ed-132">5.482143</span><span class="sxs-lookup"><span data-stu-id="0f2ed-132">5.482143</span></span> | <span data-ttu-id="0f2ed-133">572289</span><span class="sxs-lookup"><span data-stu-id="0f2ed-133">572289</span></span> |
| <span data-ttu-id="0f2ed-134">2017</span><span class="sxs-lookup"><span data-stu-id="0f2ed-134">2017</span></span> | <span data-ttu-id="0f2ed-135">1</span><span class="sxs-lookup"><span data-stu-id="0f2ed-135">1</span></span> | <span data-ttu-id="0f2ed-136">3</span><span class="sxs-lookup"><span data-stu-id="0f2ed-136">3</span></span> | <span data-ttu-id="0f2ed-137">DL</span><span class="sxs-lookup"><span data-stu-id="0f2ed-137">DL</span></span> | <span data-ttu-id="0f2ed-138">6.935409</span><span class="sxs-lookup"><span data-stu-id="0f2ed-138">6.935409</span></span> | <span data-ttu-id="0f2ed-139">-2.1893024</span><span class="sxs-lookup"><span data-stu-id="0f2ed-139">-2.1893024</span></span> | <span data-ttu-id="0f2ed-140">1909696</span><span class="sxs-lookup"><span data-stu-id="0f2ed-140">1909696</span></span> |

<span data-ttu-id="0f2ed-141">The example pipeline waits until a new time period's flight data arrives, then stores that detailed flight information into your Hive data warehouse for long-term analyses.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-141">The example pipeline waits until a new time period's flight data arrives, then stores that detailed flight information into your Hive data warehouse for long-term analyses.</span></span> <span data-ttu-id="0f2ed-142">The pipeline also creates a much smaller dataset that summarizes just the daily flight data.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-142">The pipeline also creates a much smaller dataset that summarizes just the daily flight data.</span></span> <span data-ttu-id="0f2ed-143">This daily flight summary data is sent to a SQL database to provide reports, such as for a website.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-143">This daily flight summary data is sent to a SQL database to provide reports, such as for a website.</span></span>

<span data-ttu-id="0f2ed-144">The following diagram illustrates the example pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-144">The following diagram illustrates the example pipeline.</span></span>

![Flight Data Pipeline](./media/hdinsight-operationalize-data-pipeline/pipeline-overview.png)

## <a name="oozie-solution-overview"></a><span data-ttu-id="0f2ed-146">Oozie solution overview</span><span class="sxs-lookup"><span data-stu-id="0f2ed-146">Oozie solution overview</span></span>

<span data-ttu-id="0f2ed-147">This pipeline uses Apache Oozie running on an HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-147">This pipeline uses Apache Oozie running on an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="0f2ed-148">Oozie describes its pipelines in terms of *actions*, *workflows*, and *coordinators*.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-148">Oozie describes its pipelines in terms of *actions*, *workflows*, and *coordinators*.</span></span> <span data-ttu-id="0f2ed-149">Actions determine the actual work to perform, such as running a Hive query.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-149">Actions determine the actual work to perform, such as running a Hive query.</span></span> <span data-ttu-id="0f2ed-150">Workflows define the sequence of actions.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-150">Workflows define the sequence of actions.</span></span> <span data-ttu-id="0f2ed-151">Coordinators define the schedule for when the workflow is run.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-151">Coordinators define the schedule for when the workflow is run.</span></span> <span data-ttu-id="0f2ed-152">Coordinators can also wait on the availability of new data before launching an instance of the workflow.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-152">Coordinators can also wait on the availability of new data before launching an instance of the workflow.</span></span>

<span data-ttu-id="0f2ed-153">The following diagram shows the high-level design of this example Oozie pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-153">The following diagram shows the high-level design of this example Oozie pipeline.</span></span>

![Oozie Flight Data Pipeline](./media/hdinsight-operationalize-data-pipeline/pipeline-overview-oozie.png)

### <a name="provision-azure-resources"></a><span data-ttu-id="0f2ed-155">Provision Azure resources</span><span class="sxs-lookup"><span data-stu-id="0f2ed-155">Provision Azure resources</span></span>

<span data-ttu-id="0f2ed-156">This pipeline requires an Azure SQL Database and an HDInsight Hadoop cluster in the same location.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-156">This pipeline requires an Azure SQL Database and an HDInsight Hadoop cluster in the same location.</span></span> <span data-ttu-id="0f2ed-157">The Azure SQL Database stores both the summary data produced by the pipeline and the Oozie metadata store.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-157">The Azure SQL Database stores both the summary data produced by the pipeline and the Oozie metadata store.</span></span>

#### <a name="provision-azure-sql-database"></a><span data-ttu-id="0f2ed-158">Provision Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0f2ed-158">Provision Azure SQL Database</span></span>

1. <span data-ttu-id="0f2ed-159">Using the Azure portal, create a new Resource Group named `oozie` to contain all the resources used by this example.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-159">Using the Azure portal, create a new Resource Group named `oozie` to contain all the resources used by this example.</span></span>
2. <span data-ttu-id="0f2ed-160">Within the `oozie` resource group, provision an Azure SQL Server and Database.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-160">Within the `oozie` resource group, provision an Azure SQL Server and Database.</span></span> <span data-ttu-id="0f2ed-161">You do not need a database larger than the S1 Standard pricing tier.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-161">You do not need a database larger than the S1 Standard pricing tier.</span></span>
3. <span data-ttu-id="0f2ed-162">Using the Azure portal, navigate to the pane for your newly deployed SQL Database, and select **Tools**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-162">Using the Azure portal, navigate to the pane for your newly deployed SQL Database, and select **Tools**.</span></span>

    ![Tools button](./media/hdinsight-operationalize-data-pipeline/sql-db-tools.png)

4. <span data-ttu-id="0f2ed-164">Select **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-164">Select **Query Editor**.</span></span>

    ![Query Editor button](./media/hdinsight-operationalize-data-pipeline/sql-db-query-editor.png)

5. <span data-ttu-id="0f2ed-166">In the **Query Editor** pane, select **Login**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-166">In the **Query Editor** pane, select **Login**.</span></span>

    ![Login button](./media/hdinsight-operationalize-data-pipeline/sql-db-login1.png)

6. <span data-ttu-id="0f2ed-168">Enter your SQL Database credentials and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-168">Enter your SQL Database credentials and select **OK**.</span></span>

   ![Login form](./media/hdinsight-operationalize-data-pipeline/sql-db-login2.png)

7. <span data-ttu-id="0f2ed-170">In the Query Editor text area, enter the following SQL statements to create the `dailyflights` table that will store the summarized data from each run of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-170">In the Query Editor text area, enter the following SQL statements to create the `dailyflights` table that will store the summarized data from each run of the pipeline.</span></span>

    ```
    CREATE TABLE dailyflights
    (
        YEAR INT,
        MONTH INT,
        DAY_OF_MONTH INT,
        CARRIER CHAR(2),
        AVG_DEP_DELAY FLOAT,
        AVG_ARR_DELAY FLOAT,
        TOTAL_DISTANCE FLOAT
    )
    GO

    CREATE CLUSTERED INDEX dailyflights_clustered_index on dailyflights(YEAR,MONTH,DAY_OF_MONTH,CARRIER)
    GO
    ```

8. <span data-ttu-id="0f2ed-171">Select **Run** to execute the SQL statements.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-171">Select **Run** to execute the SQL statements.</span></span>

    ![Run button](./media/hdinsight-operationalize-data-pipeline/sql-db-run.png)

<span data-ttu-id="0f2ed-173">Your Azure SQL Database is now ready.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-173">Your Azure SQL Database is now ready.</span></span>

#### <a name="provision-an-hdinsight-hadoop-cluster"></a><span data-ttu-id="0f2ed-174">Provision an HDInsight Hadoop Cluster</span><span class="sxs-lookup"><span data-stu-id="0f2ed-174">Provision an HDInsight Hadoop Cluster</span></span>

1. <span data-ttu-id="0f2ed-175">In the Azure portal, select **+New** and search for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-175">In the Azure portal, select **+New** and search for HDInsight.</span></span>
2. <span data-ttu-id="0f2ed-176">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-176">Select **Create**.</span></span>
3. <span data-ttu-id="0f2ed-177">On the Basics pane, provide a unique name for your cluster and choose your Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-177">On the Basics pane, provide a unique name for your cluster and choose your Azure Subscription.</span></span>

    ![HDInsight cluster name and subscription](./media/hdinsight-operationalize-data-pipeline/hdi-name-sub.png)

4. <span data-ttu-id="0f2ed-179">In the **Cluster type** pane, select the **Hadoop** cluster type, **Linux** operating system, and the latest version of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-179">In the **Cluster type** pane, select the **Hadoop** cluster type, **Linux** operating system, and the latest version of the HDInsight cluster.</span></span> <span data-ttu-id="0f2ed-180">Leave the **Cluster tier** at **Standard**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-180">Leave the **Cluster tier** at **Standard**.</span></span>

    ![HDInsight cluster type](./media/hdinsight-operationalize-data-pipeline/hdi-cluster-type.png)

5. <span data-ttu-id="0f2ed-182">Choose **Select** to apply your cluster type selection.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-182">Choose **Select** to apply your cluster type selection.</span></span>
6. <span data-ttu-id="0f2ed-183">Complete the **Basics** pane by providing a login password and selecting your `oozie` resource group from the list, then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-183">Complete the **Basics** pane by providing a login password and selecting your `oozie` resource group from the list, then select **Next**.</span></span>

    ![HDInsight Basics pane](./media/hdinsight-operationalize-data-pipeline/hdi-basics.png)

7. <span data-ttu-id="0f2ed-185">In the **Storage** pane, leave the primary storage type set to **Azure Storage**, select **Create new**, and provide a name for the new account.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-185">In the **Storage** pane, leave the primary storage type set to **Azure Storage**, select **Create new**, and provide a name for the new account.</span></span>

    ![HDInsight Storage Account Settings](./media/hdinsight-operationalize-data-pipeline/hdi-storage.png)

8. <span data-ttu-id="0f2ed-187">For the **Metastore Settings**, under **Select a SQL database for Hive**, choose the database you previously created.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-187">For the **Metastore Settings**, under **Select a SQL database for Hive**, choose the database you previously created.</span></span>

    ![HDInsight Hive Metastore Settings](./media/hdinsight-operationalize-data-pipeline/hdi-metastore-hive.png)

9. <span data-ttu-id="0f2ed-189">Select **Authenticate SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-189">Select **Authenticate SQL Database**.</span></span>

    ![HDInsight Hive Metastore Authenticate](./media/hdinsight-operationalize-data-pipeline/hdi-authenticate-sql.png)

10. <span data-ttu-id="0f2ed-191">Enter your SQL database username and password, and choose **Select**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-191">Enter your SQL database username and password, and choose **Select**.</span></span> 

       ![HDInsight Hive Metastore Authenticate Login](./media/hdinsight-operationalize-data-pipeline/hdi-authenticate-sql-login.png)

11. <span data-ttu-id="0f2ed-193">Back on the **Metastore Settings** pane, select your database for the Oozie metadata store and authenticate as you did previously.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-193">Back on the **Metastore Settings** pane, select your database for the Oozie metadata store and authenticate as you did previously.</span></span> 

       ![HDInsight Metastore Settings](./media/hdinsight-operationalize-data-pipeline/hdi-metastore-settings.png)

12. <span data-ttu-id="0f2ed-195">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-195">Select **Next**.</span></span>
13. <span data-ttu-id="0f2ed-196">On the **Summary** pane, select **Create** to deploy your cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-196">On the **Summary** pane, select **Create** to deploy your cluster.</span></span>

### <a name="verify-ssh-tunneling-setup"></a><span data-ttu-id="0f2ed-197">Verify SSH tunneling setup</span><span class="sxs-lookup"><span data-stu-id="0f2ed-197">Verify SSH tunneling setup</span></span>

<span data-ttu-id="0f2ed-198">To use the Oozie Web Console to view the status of your coordinator and workflow instances, set up an SSH tunnel to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-198">To use the Oozie Web Console to view the status of your coordinator and workflow instances, set up an SSH tunnel to your HDInsight cluster.</span></span> <span data-ttu-id="0f2ed-199">For more information, see [SSH Tunnel](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="0f2ed-199">For more information, see [SSH Tunnel](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0f2ed-200">You can also use Chrome with the [Foxy Proxy](https://getfoxyproxy.org/) extension to browse your cluster's web resources across the SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-200">You can also use Chrome with the [Foxy Proxy](https://getfoxyproxy.org/) extension to browse your cluster's web resources across the SSH tunnel.</span></span> <span data-ttu-id="0f2ed-201">Configure it to proxy all request through the host `localhost` on the tunnel's port 9876.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-201">Configure it to proxy all request through the host `localhost` on the tunnel's port 9876.</span></span> <span data-ttu-id="0f2ed-202">This approach is compatible with the Windows Subsystem for Linux, also known as Bash on Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-202">This approach is compatible with the Windows Subsystem for Linux, also known as Bash on Windows 10.</span></span>

1. <span data-ttu-id="0f2ed-203">Run the following command to open an SSH tunnel to your cluster:</span><span class="sxs-lookup"><span data-stu-id="0f2ed-203">Run the following command to open an SSH tunnel to your cluster:</span></span>

    ```
    ssh -C2qTnNf -D 9876 sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net
    ```

2. <span data-ttu-id="0f2ed-204">Verify the tunnel is operational by navigating to Ambari on your head node by browsing to:</span><span class="sxs-lookup"><span data-stu-id="0f2ed-204">Verify the tunnel is operational by navigating to Ambari on your head node by browsing to:</span></span>

    http://headnodehost:8080

3. <span data-ttu-id="0f2ed-205">To access the **Oozie Web Console** from within Ambari, select **Oozie**, **Quick Links**, and then select **Oozie Web Console**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-205">To access the **Oozie Web Console** from within Ambari, select **Oozie**, **Quick Links**, and then select **Oozie Web Console**.</span></span>

### <a name="configure-hive"></a><span data-ttu-id="0f2ed-206">Configure Hive</span><span class="sxs-lookup"><span data-stu-id="0f2ed-206">Configure Hive</span></span>

1. <span data-ttu-id="0f2ed-207">Download an example CSV file that contains flight data for one month.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-207">Download an example CSV file that contains flight data for one month.</span></span> <span data-ttu-id="0f2ed-208">Download its ZIP file `2017-01-FlightData.zip` from the [HDInsight Github repository](https://github.com/hdinsight/hdinsight-dev-guide) and unzip it to the CSV file `2017-01-FlightData.csv`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-208">Download its ZIP file `2017-01-FlightData.zip` from the [HDInsight Github repository](https://github.com/hdinsight/hdinsight-dev-guide) and unzip it to the CSV file `2017-01-FlightData.csv`.</span></span> 

2. <span data-ttu-id="0f2ed-209">Copy this CSV file up to the Azure Storage account attached to your HDInsight cluster and place it in the `/example/data/flights` folder.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-209">Copy this CSV file up to the Azure Storage account attached to your HDInsight cluster and place it in the `/example/data/flights` folder.</span></span>

<span data-ttu-id="0f2ed-210">You can copy the file using SCP in your `bash` shell session.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-210">You can copy the file using SCP in your `bash` shell session.</span></span>

1. <span data-ttu-id="0f2ed-211">Use SCP to copy the files from your local machine to the local storage of your HDInsight cluster head node.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-211">Use SCP to copy the files from your local machine to the local storage of your HDInsight cluster head node.</span></span>

    ```bash
    scp ./2017-01-FlightData.csv sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net:2017-01-FlightData.csv
    ```

2. <span data-ttu-id="0f2ed-212">Use the HDFS command to copy the file from your head node local storage to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-212">Use the HDFS command to copy the file from your head node local storage to Azure Storage.</span></span>

    ```bash
    hdfs dfs -put ./2017-01-FlightData.csv /example/data/flights/2017-01-FlightData.csv
    ```

<span data-ttu-id="0f2ed-213">The sample data is now available.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-213">The sample data is now available.</span></span> <span data-ttu-id="0f2ed-214">However, the pipeline requires two Hive tables for processing, one for the incoming data (`rawFlights`) and one for the summarized data (`flights`).</span><span class="sxs-lookup"><span data-stu-id="0f2ed-214">However, the pipeline requires two Hive tables for processing, one for the incoming data (`rawFlights`) and one for the summarized data (`flights`).</span></span> <span data-ttu-id="0f2ed-215">Create these tables in Ambari as follows.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-215">Create these tables in Ambari as follows.</span></span>

1. <span data-ttu-id="0f2ed-216">Log in to Ambari by navigating to [http://headnodehost:8080](http://headnodehost:8080).</span><span class="sxs-lookup"><span data-stu-id="0f2ed-216">Log in to Ambari by navigating to [http://headnodehost:8080](http://headnodehost:8080).</span></span>
2. <span data-ttu-id="0f2ed-217">From the list of services, select **Hive**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-217">From the list of services, select **Hive**.</span></span>

    ![Selecting Hive in Ambari](./media/hdinsight-operationalize-data-pipeline/hdi-ambari-services-hive.png)

3. <span data-ttu-id="0f2ed-219">Select **Go To View** next to the Hive View 2.0 label.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-219">Select **Go To View** next to the Hive View 2.0 label.</span></span>

    ![Selecting Hive View in Ambari](./media/hdinsight-operationalize-data-pipeline/hdi-ambari-services-hive-summary.png)

4. <span data-ttu-id="0f2ed-221">In the query text area, paste the following statements to create the `rawFlights` table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-221">In the query text area, paste the following statements to create the `rawFlights` table.</span></span> <span data-ttu-id="0f2ed-222">The `rawFlights` table provides a schema-on-read for the CSV files within the `/example/data/flights` folder in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-222">The `rawFlights` table provides a schema-on-read for the CSV files within the `/example/data/flights` folder in Azure Storage.</span></span> 

    ```
    CREATE EXTERNAL TABLE IF NOT EXISTS rawflights (
        YEAR INT,
        MONTH INT,
        DAY_OF_MONTH INT,
        FL_DATE STRING,
        CARRIER STRING,
        FL_NUM STRING,
        ORIGIN STRING,
        DEST STRING,
        DEP_DELAY FLOAT,
        ARR_DELAY FLOAT,
        ACTUAL_ELAPSED_TIME FLOAT,
        DISTANCE FLOAT)
    ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
    WITH SERDEPROPERTIES 
    (
        "separatorChar" = ",",
        "quoteChar"     = "\""
    ) 
    LOCATION '/example/data/flights'
    ```

5. <span data-ttu-id="0f2ed-223">Select **Execute** to create the table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-223">Select **Execute** to create the table.</span></span>

    ![Hive Query in Ambari](./media/hdinsight-operationalize-data-pipeline/hdi-ambari-services-hive-query.png)

6. <span data-ttu-id="0f2ed-225">To create the `flights` table, replace the text in the query text area with the following statements.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-225">To create the `flights` table, replace the text in the query text area with the following statements.</span></span> <span data-ttu-id="0f2ed-226">The `flights` table is a Hive managed table that partitions data loaded into it by year, month, and day of month.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-226">The `flights` table is a Hive managed table that partitions data loaded into it by year, month, and day of month.</span></span> <span data-ttu-id="0f2ed-227">This table will contain all historical flight data, with the lowest granularity present in the source data of one row per flight.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-227">This table will contain all historical flight data, with the lowest granularity present in the source data of one row per flight.</span></span>

    ```
    SET hive.exec.dynamic.partition.mode=nonstrict;

    CREATE TABLE flights
    (
        FL_DATE STRING,
        CARRIER STRING,
        FL_NUM STRING,
        ORIGIN STRING,
        DEST STRING,
        DEP_DELAY FLOAT,
        ARR_DELAY FLOAT,
        ACTUAL_ELAPSED_TIME FLOAT,
        DISTANCE FLOAT
    )
    PARTITIONED BY (YEAR INT, MONTH INT, DAY_OF_MONTH INT)
    ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
    WITH SERDEPROPERTIES 
    (
        "separatorChar" = ",",
        "quoteChar"     = "\""
    );
    ```

7. <span data-ttu-id="0f2ed-228">Select **Execute** to create the table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-228">Select **Execute** to create the table.</span></span>

### <a name="create-the-oozie-workflow"></a><span data-ttu-id="0f2ed-229">Create the Oozie workflow</span><span class="sxs-lookup"><span data-stu-id="0f2ed-229">Create the Oozie workflow</span></span>

<span data-ttu-id="0f2ed-230">Pipelines typically process data in batches by a given time interval.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-230">Pipelines typically process data in batches by a given time interval.</span></span> <span data-ttu-id="0f2ed-231">In this case, the pipeline processes the flight data daily.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-231">In this case, the pipeline processes the flight data daily.</span></span> <span data-ttu-id="0f2ed-232">This approach allows for the input CSV files to arrive daily, weekly, monthly, or annually.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-232">This approach allows for the input CSV files to arrive daily, weekly, monthly, or annually.</span></span>

<span data-ttu-id="0f2ed-233">The sample workflow processes the flight data day-by-day, in three major steps:</span><span class="sxs-lookup"><span data-stu-id="0f2ed-233">The sample workflow processes the flight data day-by-day, in three major steps:</span></span>

1. <span data-ttu-id="0f2ed-234">Run a Hive query to extract the data for that day's date range from the source CSV file represented by the `rawFlights` table and insert the data into the `flights` table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-234">Run a Hive query to extract the data for that day's date range from the source CSV file represented by the `rawFlights` table and insert the data into the `flights` table.</span></span>
2. <span data-ttu-id="0f2ed-235">Run a Hive query to dynamically create a staging table in Hive for the day, which contains a copy of the flight data summarized by day and carrier.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-235">Run a Hive query to dynamically create a staging table in Hive for the day, which contains a copy of the flight data summarized by day and carrier.</span></span>
3. <span data-ttu-id="0f2ed-236">Use Apache Sqoop to copy all the data from the daily staging table in Hive to the destination `dailyflights` table in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-236">Use Apache Sqoop to copy all the data from the daily staging table in Hive to the destination `dailyflights` table in Azure SQL Database.</span></span> <span data-ttu-id="0f2ed-237">Sqoop reads the source rows from the data behind the Hive table residing in Azure Storage and loads them into SQL Database using a JDBC connection.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-237">Sqoop reads the source rows from the data behind the Hive table residing in Azure Storage and loads them into SQL Database using a JDBC connection.</span></span>

<span data-ttu-id="0f2ed-238">These three steps are coordinated by an Oozie workflow.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-238">These three steps are coordinated by an Oozie workflow.</span></span> 

1. <span data-ttu-id="0f2ed-239">Create a query in the file `hive-load-flights-partition.hql`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-239">Create a query in the file `hive-load-flights-partition.hql`.</span></span>

    ```
    SET hive.exec.dynamic.partition.mode=nonstrict;
    
    INSERT OVERWRITE TABLE flights
    PARTITION (YEAR, MONTH, DAY_OF_MONTH)
    SELECT  
        FL_DATE,
        CARRIER,
        FL_NUM,
        ORIGIN,
        DEST,
        DEP_DELAY,
        ARR_DELAY,
        ACTUAL_ELAPSED_TIME,
        DISTANCE,
        YEAR,
        MONTH,
        DAY_OF_MONTH
    FROM rawflights
    WHERE year = ${year} AND month = ${month} AND day_of_month = ${day};
    ```

    <span data-ttu-id="0f2ed-240">Oozie variables use the syntax `${variableName}`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-240">Oozie variables use the syntax `${variableName}`.</span></span> <span data-ttu-id="0f2ed-241">These variables are set in the `job.properties` file as described in a subsequent step.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-241">These variables are set in the `job.properties` file as described in a subsequent step.</span></span> <span data-ttu-id="0f2ed-242">Oozie substitutes the actual values at runtime.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-242">Oozie substitutes the actual values at runtime.</span></span>

2. <span data-ttu-id="0f2ed-243">Create a query in the file `hive-create-daily-summary-table.hql`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-243">Create a query in the file `hive-create-daily-summary-table.hql`.</span></span>

    ```
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}
    (
        YEAR INT,
        MONTH INT,
        DAY_OF_MONTH INT,
        CARRIER STRING,
        AVG_DEP_DELAY FLOAT,
        AVG_ARR_DELAY FLOAT,
        TOTAL_DISTANCE FLOAT
    )
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName}
    SELECT  year, month, day_of_month, carrier, avg(dep_delay) avg_dep_delay, 
            avg(arr_delay) avg_arr_delay, sum(distance) total_distance 
    FROM flights
    GROUP BY year, month, day_of_month, carrier 
    HAVING year = ${year} AND month = ${month} AND day_of_month = ${day};
    ```

    <span data-ttu-id="0f2ed-244">This query creates a staging table that will store only the summarized data for one day, take note of the SELECT statement that computes the average delays and total of distance flown by carrier by day.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-244">This query creates a staging table that will store only the summarized data for one day, take note of the SELECT statement that computes the average delays and total of distance flown by carrier by day.</span></span> <span data-ttu-id="0f2ed-245">The data inserted into this table stored at a known location (the path indicated by the hiveDataFolder variable) so that it can be used as the source for Sqoop in the next step.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-245">The data inserted into this table stored at a known location (the path indicated by the hiveDataFolder variable) so that it can be used as the source for Sqoop in the next step.</span></span>

3. <span data-ttu-id="0f2ed-246">Run the following Sqoop command.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-246">Run the following Sqoop command.</span></span>

    ```
    sqoop export --connect ${sqlDatabaseConnectionString} --table ${sqlDatabaseTableName} --export-dir ${hiveDataFolder} -m 1 --input-fields-terminated-by "\t"
    ```

<span data-ttu-id="0f2ed-247">These three steps are expressed as three separate actions in the following Oozie workflow file, named `workflow.xml`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-247">These three steps are expressed as three separate actions in the following Oozie workflow file, named `workflow.xml`.</span></span>

```
<workflow-app name="loadflightstable" xmlns="uri:oozie:workflow:0.5">
    <start to = "RunHiveLoadFlightsScript"/>
    <action name="RunHiveLoadFlightsScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScriptLoadPartition}</script>
            <param>year=${year}</param>
            <param>month=${month}</param>
            <param>day=${day}</param>
        </hive>
        <ok to="RunHiveCreateDailyFlightTableScript"/>
        <error to="fail"/>
    </action>

    <action name="RunHiveCreateDailyFlightTableScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScriptCreateDailyTable}</script>
            <param>hiveTableName=${hiveDailyTableName}</param>
            <param>year=${year}</param>
            <param>month=${month}</param>
            <param>day=${day}</param>
            <param>hiveDataFolder=${hiveDataFolder}/${year}/${month}/${day}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
    </action>

    <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}/${year}/${month}/${day}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
    </action>
    <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
    </kill>
    <end name="end"/>
</workflow-app>
```

<span data-ttu-id="0f2ed-248">The two Hive queries are accessed by their path in Azure Storage, and the remaining variable values are provided by the following `job.properties` file.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-248">The two Hive queries are accessed by their path in Azure Storage, and the remaining variable values are provided by the following `job.properties` file.</span></span> <span data-ttu-id="0f2ed-249">This file configures the workflow to run for the date January 3rd, 2017.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-249">This file configures the workflow to run for the date January 3rd, 2017.</span></span>

```
nameNode=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net
jobTracker=hn0-[CLUSTERNAME].[UNIQUESTRING].dx.internal.cloudapp.net:8050
queueName=default
oozie.use.system.libpath=true
appBase=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/oozie
oozie.wf.application.path=${appBase}/load_flights_by_day
hiveScriptLoadPartition=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/oozie/load_flights_by_day/hive-load-flights-partition.hql
hiveScriptCreateDailyTable=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/oozie/load_flights_by_day/hive-create-daily-summary-table.hql
hiveDailyTableName=dailyflights${year}${month}${day}
hiveDataFolder=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/example/data/flights/day/${year}/${month}/${day}
sqlDatabaseConnectionString="jdbc:sqlserver://[SERVERNAME].database.windows.net;user=[USERNAME];password=[PASSWORD];database=[DATABASENAME]"
sqlDatabaseTableName=dailyflights
year=2017
month=01
day=03
```

<span data-ttu-id="0f2ed-250">The following table summarizes each of the properties and indicates where you can find the values for your own environment.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-250">The following table summarizes each of the properties and indicates where you can find the values for your own environment.</span></span>

| <span data-ttu-id="0f2ed-251">Property</span><span class="sxs-lookup"><span data-stu-id="0f2ed-251">Property</span></span> | <span data-ttu-id="0f2ed-252">Value source</span><span class="sxs-lookup"><span data-stu-id="0f2ed-252">Value source</span></span> |
| --- | --- |
| <span data-ttu-id="0f2ed-253">nameNode</span><span class="sxs-lookup"><span data-stu-id="0f2ed-253">nameNode</span></span> | <span data-ttu-id="0f2ed-254">The full path to the Azure Storage Container attached to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-254">The full path to the Azure Storage Container attached to your HDInsight cluster.</span></span> |
| <span data-ttu-id="0f2ed-255">jobTracker</span><span class="sxs-lookup"><span data-stu-id="0f2ed-255">jobTracker</span></span> | <span data-ttu-id="0f2ed-256">The internal hostname to your active cluster's YARN head node.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-256">The internal hostname to your active cluster's YARN head node.</span></span> <span data-ttu-id="0f2ed-257">On the Ambari home page, select YARN from the list of services, then choose Active Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-257">On the Ambari home page, select YARN from the list of services, then choose Active Resource Manager.</span></span> <span data-ttu-id="0f2ed-258">The hostname URI is displayed at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-258">The hostname URI is displayed at the top of the page.</span></span> <span data-ttu-id="0f2ed-259">Append the port 8050.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-259">Append the port 8050.</span></span> |
| <span data-ttu-id="0f2ed-260">queueName</span><span class="sxs-lookup"><span data-stu-id="0f2ed-260">queueName</span></span> | <span data-ttu-id="0f2ed-261">The name of the YARN queue used when scheduling the Hive actions.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-261">The name of the YARN queue used when scheduling the Hive actions.</span></span> <span data-ttu-id="0f2ed-262">Leave as default.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-262">Leave as default.</span></span> |
| <span data-ttu-id="0f2ed-263">oozie.use.system.libpath</span><span class="sxs-lookup"><span data-stu-id="0f2ed-263">oozie.use.system.libpath</span></span> | <span data-ttu-id="0f2ed-264">Leave as true.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-264">Leave as true.</span></span> |
| <span data-ttu-id="0f2ed-265">appBase</span><span class="sxs-lookup"><span data-stu-id="0f2ed-265">appBase</span></span> | <span data-ttu-id="0f2ed-266">The path to the subfolder in Azure Storage where you deploy the Oozie workflow and supporting files.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-266">The path to the subfolder in Azure Storage where you deploy the Oozie workflow and supporting files.</span></span> |
| <span data-ttu-id="0f2ed-267">oozie.wf.application.path</span><span class="sxs-lookup"><span data-stu-id="0f2ed-267">oozie.wf.application.path</span></span> | <span data-ttu-id="0f2ed-268">The location of the Oozie workflow `workflow.xml` to run.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-268">The location of the Oozie workflow `workflow.xml` to run.</span></span> |
| <span data-ttu-id="0f2ed-269">hiveScriptLoadPartition</span><span class="sxs-lookup"><span data-stu-id="0f2ed-269">hiveScriptLoadPartition</span></span> | <span data-ttu-id="0f2ed-270">The path in Azure Storage to the  Hive query file `hive-load-flights-partition.hql`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-270">The path in Azure Storage to the  Hive query file `hive-load-flights-partition.hql`.</span></span> |
| <span data-ttu-id="0f2ed-271">hiveScriptCreateDailyTable</span><span class="sxs-lookup"><span data-stu-id="0f2ed-271">hiveScriptCreateDailyTable</span></span> | <span data-ttu-id="0f2ed-272">The path in Azure Storage to the Hive query file `hive-create-daily-summary-table.hql`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-272">The path in Azure Storage to the Hive query file `hive-create-daily-summary-table.hql`.</span></span> |
| <span data-ttu-id="0f2ed-273">hiveDailyTableName</span><span class="sxs-lookup"><span data-stu-id="0f2ed-273">hiveDailyTableName</span></span> | <span data-ttu-id="0f2ed-274">The dynamically generated name to use for the staging table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-274">The dynamically generated name to use for the staging table.</span></span> |
| <span data-ttu-id="0f2ed-275">hiveDataFolder</span><span class="sxs-lookup"><span data-stu-id="0f2ed-275">hiveDataFolder</span></span> | <span data-ttu-id="0f2ed-276">The path in Azure Storage to the data contained by the staging table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-276">The path in Azure Storage to the data contained by the staging table.</span></span> |
| <span data-ttu-id="0f2ed-277">sqlDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="0f2ed-277">sqlDatabaseConnectionString</span></span> | <span data-ttu-id="0f2ed-278">The JDBC syntax connection string to your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-278">The JDBC syntax connection string to your Azure SQL Database.</span></span> |
| <span data-ttu-id="0f2ed-279">sqlDatabaseTableName</span><span class="sxs-lookup"><span data-stu-id="0f2ed-279">sqlDatabaseTableName</span></span> | <span data-ttu-id="0f2ed-280">The name of the table in Azure SQL Database into which summary rows are inserted.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-280">The name of the table in Azure SQL Database into which summary rows are inserted.</span></span> <span data-ttu-id="0f2ed-281">Leave as `dailyflights`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-281">Leave as `dailyflights`.</span></span> |
| <span data-ttu-id="0f2ed-282">year</span><span class="sxs-lookup"><span data-stu-id="0f2ed-282">year</span></span> | <span data-ttu-id="0f2ed-283">The year component of the day for which flight summaries are computed.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-283">The year component of the day for which flight summaries are computed.</span></span> <span data-ttu-id="0f2ed-284">Leave as is.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-284">Leave as is.</span></span> |
| <span data-ttu-id="0f2ed-285">month</span><span class="sxs-lookup"><span data-stu-id="0f2ed-285">month</span></span> | <span data-ttu-id="0f2ed-286">The month component of the day for which flight summaries are computed.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-286">The month component of the day for which flight summaries are computed.</span></span> <span data-ttu-id="0f2ed-287">Leave as is.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-287">Leave as is.</span></span> |
| <span data-ttu-id="0f2ed-288">day</span><span class="sxs-lookup"><span data-stu-id="0f2ed-288">day</span></span> | <span data-ttu-id="0f2ed-289">The day of month component of the day for which flight summaries are computed.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-289">The day of month component of the day for which flight summaries are computed.</span></span> <span data-ttu-id="0f2ed-290">Leave as is.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-290">Leave as is.</span></span> |

> [!NOTE]
> <span data-ttu-id="0f2ed-291">Be sure to update your copy of the `job.properties` file with the values specific to your environment,  before you can deploy and run your Oozie workflow.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-291">Be sure to update your copy of the `job.properties` file with the values specific to your environment,  before you can deploy and run your Oozie workflow.</span></span>

### <a name="deploy-and-run-the-oozie-workflow"></a><span data-ttu-id="0f2ed-292">Deploy and run the Oozie workflow</span><span class="sxs-lookup"><span data-stu-id="0f2ed-292">Deploy and run the Oozie workflow</span></span>

<span data-ttu-id="0f2ed-293">Use SCP from your bash session to deploy your Oozie workflow (`workflow.xml`), the Hive queries (`hive-load-flights-partition.hql` and `hive-create-daily-summary-table.hql`) and the job configuration (`job.properties`).</span><span class="sxs-lookup"><span data-stu-id="0f2ed-293">Use SCP from your bash session to deploy your Oozie workflow (`workflow.xml`), the Hive queries (`hive-load-flights-partition.hql` and `hive-create-daily-summary-table.hql`) and the job configuration (`job.properties`).</span></span>  <span data-ttu-id="0f2ed-294">In Oozie, only the `job.properties` file can exist on the local storage of the headnode.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-294">In Oozie, only the `job.properties` file can exist on the local storage of the headnode.</span></span> <span data-ttu-id="0f2ed-295">All other files must be stored in HDFS, in this case Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-295">All other files must be stored in HDFS, in this case Azure Storage.</span></span> <span data-ttu-id="0f2ed-296">The Sqoop action used by the workflow depends on a JDBC driver for communicating with your SQL Database, which must be copied from the head node to HDFS.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-296">The Sqoop action used by the workflow depends on a JDBC driver for communicating with your SQL Database, which must be copied from the head node to HDFS.</span></span>

1. <span data-ttu-id="0f2ed-297">Create the `load_flights_by_day` subfolder underneath the user's path in the local storage of the head node.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-297">Create the `load_flights_by_day` subfolder underneath the user's path in the local storage of the head node.</span></span>

        ssh sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net 'mkdir load_flights_by_day'

2. <span data-ttu-id="0f2ed-298">Copy all files in the current directory (the `workflow.xml` and `job.properties` files) up to the `load_flights_by_day` subfolder.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-298">Copy all files in the current directory (the `workflow.xml` and `job.properties` files) up to the `load_flights_by_day` subfolder.</span></span>

        scp ./* sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net:load_flights_by_day

3. <span data-ttu-id="0f2ed-299">SSH into your head node and navigate to the `load_flights_by_day` folder.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-299">SSH into your head node and navigate to the `load_flights_by_day` folder.</span></span>

        ssh sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net
        cd load_flights_by_day

4. <span data-ttu-id="0f2ed-300">Copy workflow files to HDFS.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-300">Copy workflow files to HDFS.</span></span>

        hdfs dfs -put ./* /oozie/load_flights_by_day

5. <span data-ttu-id="0f2ed-301">Copy `sqljdbc41.jar` from the local head node to the workflow folder in HDFS:</span><span class="sxs-lookup"><span data-stu-id="0f2ed-301">Copy `sqljdbc41.jar` from the local head node to the workflow folder in HDFS:</span></span>

        hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /oozie/load_flights_by_day

6. <span data-ttu-id="0f2ed-302">Run the workflow.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-302">Run the workflow.</span></span>

        oozie job -config job.properties -run

7. <span data-ttu-id="0f2ed-303">Observe the status using the Oozie Web Console.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-303">Observe the status using the Oozie Web Console.</span></span> <span data-ttu-id="0f2ed-304">From within Ambari, select **Oozie**, **Quick Links**, and then **Oozie Web Console**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-304">From within Ambari, select **Oozie**, **Quick Links**, and then **Oozie Web Console**.</span></span> <span data-ttu-id="0f2ed-305">Under the **Workflow Jobs** tab, select **All Jobs**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-305">Under the **Workflow Jobs** tab, select **All Jobs**.</span></span>

    ![Oozie Web Console Workflows](./media/hdinsight-operationalize-data-pipeline/hdi-oozie-web-console-workflows.png)

8. <span data-ttu-id="0f2ed-307">When the status is SUCCEEDED, query the SQL database table to view the inserted rows.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-307">When the status is SUCCEEDED, query the SQL database table to view the inserted rows.</span></span> <span data-ttu-id="0f2ed-308">Using the Azure portal, navigate to the pane for your SQL Database, select **Tools**, and open the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-308">Using the Azure portal, navigate to the pane for your SQL Database, select **Tools**, and open the **Query Editor**.</span></span>

        SELECT * FROM dailyflights

<span data-ttu-id="0f2ed-309">Now that the workflow is running for the single test day, you can wrap this workflow with a coordinator that schedules the workflow so it runs daily.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-309">Now that the workflow is running for the single test day, you can wrap this workflow with a coordinator that schedules the workflow so it runs daily.</span></span>

### <a name="run-the-workflow-with-a-coordinator"></a><span data-ttu-id="0f2ed-310">Run the workflow with a coordinator</span><span class="sxs-lookup"><span data-stu-id="0f2ed-310">Run the workflow with a coordinator</span></span>

<span data-ttu-id="0f2ed-311">To schedule this workflow so that it runs daily (or all days in a date range), you can use a coordinator.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-311">To schedule this workflow so that it runs daily (or all days in a date range), you can use a coordinator.</span></span> <span data-ttu-id="0f2ed-312">A coordinator is defined by an XML file, for example `coordinator.xml`:</span><span class="sxs-lookup"><span data-stu-id="0f2ed-312">A coordinator is defined by an XML file, for example `coordinator.xml`:</span></span>

```
<coordinator-app name="daily_export" start="2017-01-01T00:00Z" end="2017-01-05T00:00Z" frequency="${coord:days(1)}" timezone="UTC" xmlns="uri:oozie:coordinator:0.4">
    <datasets>
        <dataset name="ds_input1" frequency="${coord:days(1)}" initial-instance="2016-12-31T00:00Z" timezone="UTC">
            <uri-template>${sourceDataFolder}${YEAR}-${MONTH}-FlightData.csv</uri-template>
            <done-flag></done-flag>
        </dataset>
    </datasets>
    <input-events>
        <data-in name="event_input1" dataset="ds_input1">
            <instance>${coord:current(0)}</instance>
        </data-in>
    </input-events>
    <action>
        <workflow>
            <app-path>${appBase}/load_flights_by_day</app-path>
            <configuration>
                <property>
                    <name>year</name>
                    <value>${coord:formatTime(coord:nominalTime(), 'yyyy')}</value>
                </property>
                <property>
                    <name>month</name>
                    <value>${coord:formatTime(coord:nominalTime(), 'MM')}</value>
                </property>
                <property>
                    <name>day</name>
                    <value>${coord:formatTime(coord:nominalTime(), 'dd')}</value>
                </property>
                <property>
                    <name>hiveScriptLoadPartition</name>
                    <value>${hiveScriptLoadPartition}</value>
                </property>
                <property>
                    <name>hiveScriptCreateDailyTable</name>
                    <value>${hiveScriptCreateDailyTable}</value>
                </property>
                <property>
                    <name>hiveDailyTableNamePrefix</name>
                    <value>${hiveDailyTableNamePrefix}</value>
                </property>
                <property>
                    <name>hiveDailyTableName</name>
                    <value>${hiveDailyTableNamePrefix}${coord:formatTime(coord:nominalTime(), 'yyyy')}${coord:formatTime(coord:nominalTime(), 'MM')}${coord:formatTime(coord:nominalTime(), 'dd')}</value>
                </property>
                <property>
                    <name>hiveDataFolderPrefix</name>
                    <value>${hiveDataFolderPrefix}</value>
                </property>
                <property>
                    <name>hiveDataFolder</name>
                    <value>${hiveDataFolderPrefix}${coord:formatTime(coord:nominalTime(), 'yyyy')}/${coord:formatTime(coord:nominalTime(), 'MM')}/${coord:formatTime(coord:nominalTime(), 'dd')}</value>
                </property>
                <property>
                    <name>sqlDatabaseConnectionString</name>
                    <value>${sqlDatabaseConnectionString}</value>
                </property>
                <property>
                    <name>sqlDatabaseTableName</name>
                    <value>${sqlDatabaseTableName}</value>
                </property>
            </configuration>
        </workflow>
    </action>
</coordinator-app>
```

<span data-ttu-id="0f2ed-313">As you can see, the majority of the coordinator is just passing configuration information to the workflow instance.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-313">As you can see, the majority of the coordinator is just passing configuration information to the workflow instance.</span></span> <span data-ttu-id="0f2ed-314">However, there are a few important items to call out.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-314">However, there are a few important items to call out.</span></span>

* <span data-ttu-id="0f2ed-315">Point 1: The `start` and `end` attributes on the `coordinator-app` element itself control the time interval over which the coordinator runs.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-315">Point 1: The `start` and `end` attributes on the `coordinator-app` element itself control the time interval over which the coordinator runs.</span></span>

    ```
    <coordinator-app ... start="2017-01-01T00:00Z" end="2017-01-05T00:00Z" frequency="${coord:days(1)}" ...>
    ```

    <span data-ttu-id="0f2ed-316">A coordinator is responsible for scheduling actions within the `start` and `end` date range, according to the interval specified by the `frequency` attribute.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-316">A coordinator is responsible for scheduling actions within the `start` and `end` date range, according to the interval specified by the `frequency` attribute.</span></span> <span data-ttu-id="0f2ed-317">Each scheduled action in turn runs the workflow as configured.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-317">Each scheduled action in turn runs the workflow as configured.</span></span> <span data-ttu-id="0f2ed-318">In the coordinator definition above, the coordinator is configured to run actions from January 1st, 2017 to January 5th, 2017.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-318">In the coordinator definition above, the coordinator is configured to run actions from January 1st, 2017 to January 5th, 2017.</span></span> <span data-ttu-id="0f2ed-319">The frequency is set to 1 day by the [Oozie Expression Language](http://oozie.apache.org/docs/4.2.0/CoordinatorFunctionalSpec.html#a4.4._Frequency_and_Time-Period_Representation) frequency expression `${coord:days(1)}`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-319">The frequency is set to 1 day by the [Oozie Expression Language](http://oozie.apache.org/docs/4.2.0/CoordinatorFunctionalSpec.html#a4.4._Frequency_and_Time-Period_Representation) frequency expression `${coord:days(1)}`.</span></span> <span data-ttu-id="0f2ed-320">This results in the coordinator scheduling an action (and hence the workflow) once per day.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-320">This results in the coordinator scheduling an action (and hence the workflow) once per day.</span></span> <span data-ttu-id="0f2ed-321">For date ranges that are in the past, as in this example, the action will be scheduled to run without delay.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-321">For date ranges that are in the past, as in this example, the action will be scheduled to run without delay.</span></span> <span data-ttu-id="0f2ed-322">The start of the date from which an action is scheduled to run is called the *nominal time*.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-322">The start of the date from which an action is scheduled to run is called the *nominal time*.</span></span> <span data-ttu-id="0f2ed-323">For example, to process the data for January 1st, 2017 the coordinator will schedule action with a nominal time of 2017-01-01T00:00:00 GMT.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-323">For example, to process the data for January 1st, 2017 the coordinator will schedule action with a nominal time of 2017-01-01T00:00:00 GMT.</span></span>

* <span data-ttu-id="0f2ed-324">Point 2: Within the date range of the workflow, the `dataset` element specifies where to look in HDFS for the data for a particular date range, and configures how Oozie determines whether the data is available yet for processing.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-324">Point 2: Within the date range of the workflow, the `dataset` element specifies where to look in HDFS for the data for a particular date range, and configures how Oozie determines whether the data is available yet for processing.</span></span>

    ```
    <dataset name="ds_input1" frequency="${coord:days(1)}" initial-instance="2016-12-31T00:00Z" timezone="UTC">
        <uri-template>${sourceDataFolder}${YEAR}-${MONTH}-FlightData.csv</uri-template>
        <done-flag></done-flag>
    </dataset>
    ```

    <span data-ttu-id="0f2ed-325">The path to the data in HDFS is built dynamically according to the expression provided in the `uri-template` element.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-325">The path to the data in HDFS is built dynamically according to the expression provided in the `uri-template` element.</span></span> <span data-ttu-id="0f2ed-326">In this coordinator, a frequency of one day is also used with the dataset.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-326">In this coordinator, a frequency of one day is also used with the dataset.</span></span> <span data-ttu-id="0f2ed-327">While the start and end dates on the coordinator element control when the actions are scheduled (and defines their nominal times), the `initial-instance` and `frequency` on the dataset control the calculation of the date that is used in constructing the `uri-template`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-327">While the start and end dates on the coordinator element control when the actions are scheduled (and defines their nominal times), the `initial-instance` and `frequency` on the dataset control the calculation of the date that is used in constructing the `uri-template`.</span></span> <span data-ttu-id="0f2ed-328">In this case, set the initial instance to one day before the start of the coordinator to ensure that it picks up the first day's (1/1/2017) worth of data.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-328">In this case, set the initial instance to one day before the start of the coordinator to ensure that it picks up the first day's (1/1/2017) worth of data.</span></span> <span data-ttu-id="0f2ed-329">The dataset's date calculation rolls forward from the value of `initial-instance` (12/31/2016) advancing in increments of dataset frequency (1 day) until it finds the most recent date that does not pass the nominal time set by the coordinator (2017-01-01T00:00:00 GMT for the first action).</span><span class="sxs-lookup"><span data-stu-id="0f2ed-329">The dataset's date calculation rolls forward from the value of `initial-instance` (12/31/2016) advancing in increments of dataset frequency (1 day) until it finds the most recent date that does not pass the nominal time set by the coordinator (2017-01-01T00:00:00 GMT for the first action).</span></span>

    <span data-ttu-id="0f2ed-330">The empty `done-flag` element indicates that when Oozie checks for the presence of input data at the appointed time, Oozie determines data whether available by presence of a directory or file.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-330">The empty `done-flag` element indicates that when Oozie checks for the presence of input data at the appointed time, Oozie determines data whether available by presence of a directory or file.</span></span> <span data-ttu-id="0f2ed-331">In this case it is the presence of a csv file.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-331">In this case it is the presence of a csv file.</span></span> <span data-ttu-id="0f2ed-332">If a csv file is present, Oozie assumes the data is ready and launches a workflow instance to process the file.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-332">If a csv file is present, Oozie assumes the data is ready and launches a workflow instance to process the file.</span></span> <span data-ttu-id="0f2ed-333">If there is no csv file present, Oozie assumes the data is not yet ready and that run of the workflow goes into a waiting state.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-333">If there is no csv file present, Oozie assumes the data is not yet ready and that run of the workflow goes into a waiting state.</span></span>

* <span data-ttu-id="0f2ed-334">Point 3: The `data-in` element specifies the particular timestamp to use as the nominal time when replacing the values in `uri-template` for the associated dataset.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-334">Point 3: The `data-in` element specifies the particular timestamp to use as the nominal time when replacing the values in `uri-template` for the associated dataset.</span></span>

    ```
    <data-in name="event_input1" dataset="ds_input1">
        <instance>${coord:current(0)}</instance>
    </data-in>
    ```

    <span data-ttu-id="0f2ed-335">In this case, set the instance to the expression `${coord:current(0)}`, which translates to using the nominal time of the action as originally scheduled by the coordinator.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-335">In this case, set the instance to the expression `${coord:current(0)}`, which translates to using the nominal time of the action as originally scheduled by the coordinator.</span></span> <span data-ttu-id="0f2ed-336">In other words, when the coordinator schedules the action to run with a nominal time of 01/01/2017, then 01/01/2017 is what is used to replace the YEAR (2017) and MONTH (01) variables in the URI template.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-336">In other words, when the coordinator schedules the action to run with a nominal time of 01/01/2017, then 01/01/2017 is what is used to replace the YEAR (2017) and MONTH (01) variables in the URI template.</span></span> <span data-ttu-id="0f2ed-337">Once the URI template is computed for this instance, Oozie checks whether the expected directory or file is available and schedules the next run of the workflow accordingly.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-337">Once the URI template is computed for this instance, Oozie checks whether the expected directory or file is available and schedules the next run of the workflow accordingly.</span></span>

<span data-ttu-id="0f2ed-338">The three preceding points combine to yield a situation where the coordinator schedules processing of the source data in a day-by-day fashion.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-338">The three preceding points combine to yield a situation where the coordinator schedules processing of the source data in a day-by-day fashion.</span></span> 

* <span data-ttu-id="0f2ed-339">Point 1: The coordinator starts with a nominal date of 2017-01-01.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-339">Point 1: The coordinator starts with a nominal date of 2017-01-01.</span></span>

* <span data-ttu-id="0f2ed-340">Point 2: Oozie looks for data available in `sourceDataFolder/2017-01-FlightData.csv`.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-340">Point 2: Oozie looks for data available in `sourceDataFolder/2017-01-FlightData.csv`.</span></span>

* <span data-ttu-id="0f2ed-341">Point 3: When Oozie finds that file, it schedules an instance of the workflow that will process the data for 2017-01-01.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-341">Point 3: When Oozie finds that file, it schedules an instance of the workflow that will process the data for 2017-01-01.</span></span> <span data-ttu-id="0f2ed-342">Oozie then continues processing for 2017-01-02.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-342">Oozie then continues processing for 2017-01-02.</span></span> <span data-ttu-id="0f2ed-343">This evaluation repeats up to but not including 2017-01-05.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-343">This evaluation repeats up to but not including 2017-01-05.</span></span>

<span data-ttu-id="0f2ed-344">As with workflows, the configuration of a coordinator is defined in a `job.properties` file, which has a superset of the settings used by the workflow.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-344">As with workflows, the configuration of a coordinator is defined in a `job.properties` file, which has a superset of the settings used by the workflow.</span></span>

```
nameNode=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net
jobTracker=hn0-[CLUSTERNAME].[UNIQUESTRING].dx.internal.cloudapp.net:8050
queueName=default
oozie.use.system.libpath=true
appBase=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/oozie
oozie.coord.application.path=${appBase}
sourceDataFolder=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/example/data/flights/
hiveScriptLoadPartition=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/oozie/load_flights_by_day/hive-load-flights-partition.hql
hiveScriptCreateDailyTable=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/oozie/load_flights_by_day/hive-create-daily-summary-table.hql
hiveDailyTableNamePrefix=dailyflights
hiveDataFolderPrefix=wasbs://[CONTAINERNAME]@[ACCOUNTNAME].blob.core.windows.net/example/data/flights/day/
sqlDatabaseConnectionString="jdbc:sqlserver://[SERVERNAME].database.windows.net;user=[USERNAME];password=[PASSWORD];database=[DATABASENAME]"
sqlDatabaseTableName=dailyflights

```

<span data-ttu-id="0f2ed-345">The only new properties introduced in this `job.properties` file are:</span><span class="sxs-lookup"><span data-stu-id="0f2ed-345">The only new properties introduced in this `job.properties` file are:</span></span>

| <span data-ttu-id="0f2ed-346">Property</span><span class="sxs-lookup"><span data-stu-id="0f2ed-346">Property</span></span> | <span data-ttu-id="0f2ed-347">Value source</span><span class="sxs-lookup"><span data-stu-id="0f2ed-347">Value source</span></span> |
| --- | --- |
| <span data-ttu-id="0f2ed-348">oozie.coord.application.path</span><span class="sxs-lookup"><span data-stu-id="0f2ed-348">oozie.coord.application.path</span></span> | <span data-ttu-id="0f2ed-349">Indicates the location of the `coordinator.xml` file containing the Oozie coordinator to run.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-349">Indicates the location of the `coordinator.xml` file containing the Oozie coordinator to run.</span></span> |
| <span data-ttu-id="0f2ed-350">hiveDailyTableNamePrefix</span><span class="sxs-lookup"><span data-stu-id="0f2ed-350">hiveDailyTableNamePrefix</span></span> | <span data-ttu-id="0f2ed-351">The prefix used when dynamically creating the table name of the staging table.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-351">The prefix used when dynamically creating the table name of the staging table.</span></span> |
| <span data-ttu-id="0f2ed-352">hiveDataFolderPrefix</span><span class="sxs-lookup"><span data-stu-id="0f2ed-352">hiveDataFolderPrefix</span></span> | <span data-ttu-id="0f2ed-353">The prefix of the path where all the staging tables will be stored.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-353">The prefix of the path where all the staging tables will be stored.</span></span> |

### <a name="deploy-and-run-the-oozie-coordinator"></a><span data-ttu-id="0f2ed-354">Deploy and run the Oozie Coordinator</span><span class="sxs-lookup"><span data-stu-id="0f2ed-354">Deploy and run the Oozie Coordinator</span></span>

<span data-ttu-id="0f2ed-355">To run the pipeline with a coordinator, proceed in a similar fashion as for the workflow, except you work from a folder one level above the folder that contains your workflow.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-355">To run the pipeline with a coordinator, proceed in a similar fashion as for the workflow, except you work from a folder one level above the folder that contains your workflow.</span></span> <span data-ttu-id="0f2ed-356">This folder convention separates the coordinators from the workflows on disk, so you can associate one coordinator with different child workflows.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-356">This folder convention separates the coordinators from the workflows on disk, so you can associate one coordinator with different child workflows.</span></span>

1. <span data-ttu-id="0f2ed-357">Use SCP from your local machine to copy the coordinator files up to the local storage of the head node of your cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-357">Use SCP from your local machine to copy the coordinator files up to the local storage of the head node of your cluster.</span></span>

    ```bash
    scp ./* sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net:~
    ```

2. <span data-ttu-id="0f2ed-358">SSH into your head node.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-358">SSH into your head node.</span></span>

    ```bash
    ssh sshuser@[CLUSTERNAME]-ssh.azurehdinsight.net 
    ```

3. <span data-ttu-id="0f2ed-359">Copy the coordinator files to HDFS.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-359">Copy the coordinator files to HDFS.</span></span>

    ```bash
    hdfs dfs -put ./* /oozie/
    ```

4. <span data-ttu-id="0f2ed-360">Run the coordinator.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-360">Run the coordinator.</span></span>

    ```bash
    oozie job -config job.properties -run
    ```

5. <span data-ttu-id="0f2ed-361">Verify the status using the Oozie Web Console, this time selecting the **Coordinator Jobs** tab, and then  **All jobs**.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-361">Verify the status using the Oozie Web Console, this time selecting the **Coordinator Jobs** tab, and then  **All jobs**.</span></span>

    ![Oozie Web Console Coordinator Jobs](./media/hdinsight-operationalize-data-pipeline/hdi-oozie-web-console-coordinator-jobs.png)

6. <span data-ttu-id="0f2ed-363">Select a coordinator instance to display the list of scheduled actions.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-363">Select a coordinator instance to display the list of scheduled actions.</span></span> <span data-ttu-id="0f2ed-364">In this case, you should see four actions with nominal times in the range from 1/1/2017 to 1/4/2017.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-364">In this case, you should see four actions with nominal times in the range from 1/1/2017 to 1/4/2017.</span></span>

    ![Oozie Web Console Coordinator Job](./media/hdinsight-operationalize-data-pipeline/hdi-oozie-web-console-coordinator-instance.png)

    <span data-ttu-id="0f2ed-366">Each action in this list corresponds to an instance of the workflow that processes one day's worth of data, where the start of that day is indicated by the nominal time.</span><span class="sxs-lookup"><span data-stu-id="0f2ed-366">Each action in this list corresponds to an instance of the workflow that processes one day's worth of data, where the start of that day is indicated by the nominal time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f2ed-367">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f2ed-367">Next steps</span></span>

* [<span data-ttu-id="0f2ed-368">Apache Oozie Documentation</span><span class="sxs-lookup"><span data-stu-id="0f2ed-368">Apache Oozie Documentation</span></span>](http://oozie.apache.org/docs/4.2.0/index.html)

<!-- * Build the same pipeline [using Azure Data Factory](tbd.md).  -->
