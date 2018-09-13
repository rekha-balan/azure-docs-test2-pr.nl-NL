---
title: 'Tutorial: Analyze Apache Spark data using Power BI in Azure HDInsight '
description: Use Microsoft Power BI to visualize Spark data stored HDInsight clusters
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,mvc
ms.topic: tutorial
ms.date: 05/07/2018
ms.openlocfilehash: b8f952f27b5971704c8202fe80a95026e513b373
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870443"
---
# <a name="tutorial-analyze-spark-data-using-power-bi-in-hdinsight"></a><span data-ttu-id="32ed8-103">Tutorial: Analyze Spark data using Power BI in HDInsight</span><span class="sxs-lookup"><span data-stu-id="32ed8-103">Tutorial: Analyze Spark data using Power BI in HDInsight</span></span> 

<span data-ttu-id="32ed8-104">Learn how to use Microsoft Power BI to visualize data in Apache Spark cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="32ed8-104">Learn how to use Microsoft Power BI to visualize data in Apache Spark cluster in Azure HDInsight.</span></span>

<span data-ttu-id="32ed8-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="32ed8-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="32ed8-106">Visualize Spark data using Power BI</span><span class="sxs-lookup"><span data-stu-id="32ed8-106">Visualize Spark data using Power BI</span></span>

<span data-ttu-id="32ed8-107">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="32ed8-107">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32ed8-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="32ed8-108">Prerequisites</span></span>

* <span data-ttu-id="32ed8-109">**Complete the article [Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight](./apache-spark-load-data-run-query.md)**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-109">**Complete the article [Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight](./apache-spark-load-data-run-query.md)**.</span></span>
* <span data-ttu-id="32ed8-110">**Power BI**: [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/) and [Power BI trial subscription](https://app.powerbi.com/signupredirect?pbi_source=web) (optional).</span><span class="sxs-lookup"><span data-stu-id="32ed8-110">**Power BI**: [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/) and [Power BI trial subscription](https://app.powerbi.com/signupredirect?pbi_source=web) (optional).</span></span>


## <a name="verify-the-data"></a><span data-ttu-id="32ed8-111">Verify the data</span><span class="sxs-lookup"><span data-stu-id="32ed8-111">Verify the data</span></span>

<span data-ttu-id="32ed8-112">The Jupyter notebook that you created in the [previous tutorial](apache-spark-load-data-run-query.md) includes code to create an `hvac` table.</span><span class="sxs-lookup"><span data-stu-id="32ed8-112">The Jupyter notebook that you created in the [previous tutorial](apache-spark-load-data-run-query.md) includes code to create an `hvac` table.</span></span> <span data-ttu-id="32ed8-113">This table is based on the CSV file available on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-113">This table is based on the CSV file available on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="32ed8-114">Use the following procedure to verify the data.</span><span class="sxs-lookup"><span data-stu-id="32ed8-114">Use the following procedure to verify the data.</span></span>

1. <span data-ttu-id="32ed8-115">From the Jupyter notebook, paste the following code, and then press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-115">From the Jupyter notebook, paste the following code, and then press **SHIFT + ENTER**.</span></span> <span data-ttu-id="32ed8-116">The code verifies the existence of the tables.</span><span class="sxs-lookup"><span data-stu-id="32ed8-116">The code verifies the existence of the tables.</span></span>

    ```PySpark
    %%sql
    SHOW TABLES
    ```

    <span data-ttu-id="32ed8-117">The output looks like:</span><span class="sxs-lookup"><span data-stu-id="32ed8-117">The output looks like:</span></span>

    ![Show tables in Spark](./media/apache-spark-use-bi-tools/show-tables.png)

    <span data-ttu-id="32ed8-119">If you closed the notebook before starting this tutorial, `hvactemptable` is cleaned up, so it's not included in the output.</span><span class="sxs-lookup"><span data-stu-id="32ed8-119">If you closed the notebook before starting this tutorial, `hvactemptable` is cleaned up, so it's not included in the output.</span></span>  <span data-ttu-id="32ed8-120">Only Hive tables that are stored in the metastore (indicated by **False** under the **isTemporary** column) can be accessed from the BI tools.</span><span class="sxs-lookup"><span data-stu-id="32ed8-120">Only Hive tables that are stored in the metastore (indicated by **False** under the **isTemporary** column) can be accessed from the BI tools.</span></span> <span data-ttu-id="32ed8-121">In this tutorial, you connect to the **hvac** table that you created.</span><span class="sxs-lookup"><span data-stu-id="32ed8-121">In this tutorial, you connect to the **hvac** table that you created.</span></span>

2. <span data-ttu-id="32ed8-122">Paste the following code in an empty cell, and then press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-122">Paste the following code in an empty cell, and then press **SHIFT + ENTER**.</span></span> <span data-ttu-id="32ed8-123">The code verifies the data in the table.</span><span class="sxs-lookup"><span data-stu-id="32ed8-123">The code verifies the data in the table.</span></span>

    ```PySpark
    %%sql
    SELECT * FROM hvac LIMIT 10
    ```

    <span data-ttu-id="32ed8-124">The output looks like:</span><span class="sxs-lookup"><span data-stu-id="32ed8-124">The output looks like:</span></span>

    ![Show rows from hvac table in Spark](./media/apache-spark-use-bi-tools/select-limit.png)

3. <span data-ttu-id="32ed8-126">From the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-126">From the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="32ed8-127">Shut down the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="32ed8-127">Shut down the notebook to release the resources.</span></span> 

## <a name="visualize-the-data"></a><span data-ttu-id="32ed8-128">Visualize the data</span><span class="sxs-lookup"><span data-stu-id="32ed8-128">Visualize the data</span></span>

<span data-ttu-id="32ed8-129">In this section, you use Power BI to create visualizations, reports, and dashboards from the Spark cluster data.</span><span class="sxs-lookup"><span data-stu-id="32ed8-129">In this section, you use Power BI to create visualizations, reports, and dashboards from the Spark cluster data.</span></span> 

### <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="32ed8-130">Create a report in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="32ed8-130">Create a report in Power BI Desktop</span></span>
<span data-ttu-id="32ed8-131">The first steps in working with Spark are to connect to the cluster in Power BI Desktop, load data from the cluster, and create a basic visualization based on that data.</span><span class="sxs-lookup"><span data-stu-id="32ed8-131">The first steps in working with Spark are to connect to the cluster in Power BI Desktop, load data from the cluster, and create a basic visualization based on that data.</span></span>

> [!NOTE]
> <span data-ttu-id="32ed8-132">The connector demonstrated in this article is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="32ed8-132">The connector demonstrated in this article is currently in preview.</span></span> <span data-ttu-id="32ed8-133">Provide any feedback you have through the [Power BI Community](https://community.powerbi.com/) site or [Power BI Ideas](https://ideas.powerbi.com/forums/265200-power-bi-ideas).</span><span class="sxs-lookup"><span data-stu-id="32ed8-133">Provide any feedback you have through the [Power BI Community](https://community.powerbi.com/) site or [Power BI Ideas](https://ideas.powerbi.com/forums/265200-power-bi-ideas).</span></span>

1. <span data-ttu-id="32ed8-134">Open [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="32ed8-134">Open [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>
1. <span data-ttu-id="32ed8-135">From the **Home** tab, click **Get Data**, then **More**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-135">From the **Home** tab, click **Get Data**, then **More**.</span></span>

    <span data-ttu-id="32ed8-136">![Get data into Power BI Desktop from HDInsight Apache Spark](./media/apache-spark-use-bi-tools/hdinsight-spark-power-bi-desktop-get-data.png "Get data into Power BI from Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="32ed8-136">![Get data into Power BI Desktop from HDInsight Apache Spark](./media/apache-spark-use-bi-tools/hdinsight-spark-power-bi-desktop-get-data.png "Get data into Power BI from Apache Spark BI")</span></span>


2. <span data-ttu-id="32ed8-137">Enter `Spark` in the search box, select **Azure HDInsight Spark (Beta)**, and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-137">Enter `Spark` in the search box, select **Azure HDInsight Spark (Beta)**, and then click **Connect**.</span></span>

    <span data-ttu-id="32ed8-138">![Get data into Power BI from Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI from Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="32ed8-138">![Get data into Power BI from Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI from Apache Spark BI")</span></span>

3. <span data-ttu-id="32ed8-139">Enter your cluster URL (in the form `mysparkcluster.azurehdinsight.net`), select **DirectQuery**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-139">Enter your cluster URL (in the form `mysparkcluster.azurehdinsight.net`), select **DirectQuery**, and then click **OK**.</span></span>

    <span data-ttu-id="32ed8-140">You can use either data connectivity mode with Spark.</span><span class="sxs-lookup"><span data-stu-id="32ed8-140">You can use either data connectivity mode with Spark.</span></span> <span data-ttu-id="32ed8-141">If you use DirectQuery, changes are reflected in reports without refreshing the entire dataset.</span><span class="sxs-lookup"><span data-stu-id="32ed8-141">If you use DirectQuery, changes are reflected in reports without refreshing the entire dataset.</span></span> <span data-ttu-id="32ed8-142">If you import data, you must refresh the data set to see changes.</span><span class="sxs-lookup"><span data-stu-id="32ed8-142">If you import data, you must refresh the data set to see changes.</span></span> <span data-ttu-id="32ed8-143">For more information on how and when to use DirectQuery, see [Using DirectQuery in Power BI](https://powerbi.microsoft.com/documentation/powerbi-desktop-directquery-about/).</span><span class="sxs-lookup"><span data-stu-id="32ed8-143">For more information on how and when to use DirectQuery, see [Using DirectQuery in Power BI](https://powerbi.microsoft.com/documentation/powerbi-desktop-directquery-about/).</span></span> 

4. <span data-ttu-id="32ed8-144">Enter the HDInsight login account information, then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-144">Enter the HDInsight login account information, then click **Connect**.</span></span> <span data-ttu-id="32ed8-145">The default account name is *admin*.</span><span class="sxs-lookup"><span data-stu-id="32ed8-145">The default account name is *admin*.</span></span>

5. <span data-ttu-id="32ed8-146">Select the `hvac` table, wait to see a preview of the data, and then click **Load**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-146">Select the `hvac` table, wait to see a preview of the data, and then click **Load**.</span></span>

    <span data-ttu-id="32ed8-147">![Spark cluster user name and password](./media/apache-spark-use-bi-tools/apache-spark-bi-select-table.png "Spark cluster user name and password")</span><span class="sxs-lookup"><span data-stu-id="32ed8-147">![Spark cluster user name and password](./media/apache-spark-use-bi-tools/apache-spark-bi-select-table.png "Spark cluster user name and password")</span></span>

    <span data-ttu-id="32ed8-148">Power BI Desktop has the information it needs to connect to the Spark cluster and load data from the `hvac` table.</span><span class="sxs-lookup"><span data-stu-id="32ed8-148">Power BI Desktop has the information it needs to connect to the Spark cluster and load data from the `hvac` table.</span></span> <span data-ttu-id="32ed8-149">The table and its columns are displayed in the **Fields** pane.</span><span class="sxs-lookup"><span data-stu-id="32ed8-149">The table and its columns are displayed in the **Fields** pane.</span></span>  <span data-ttu-id="32ed8-150">See the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="32ed8-150">See the following screenshot:</span></span>

6. <span data-ttu-id="32ed8-151">Visualize the variance between target temperature and actual temperature for each building:</span><span class="sxs-lookup"><span data-stu-id="32ed8-151">Visualize the variance between target temperature and actual temperature for each building:</span></span> 

    1. <span data-ttu-id="32ed8-152">In the **VISUALIZATIONS** pane, select **Area Chart**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-152">In the **VISUALIZATIONS** pane, select **Area Chart**.</span></span> 
    2. <span data-ttu-id="32ed8-153">Drag the **BuildingID** field to **Axis**, and drag the **ActualTemp** and **TargetTemp** fields to **Value**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-153">Drag the **BuildingID** field to **Axis**, and drag the **ActualTemp** and **TargetTemp** fields to **Value**.</span></span>

        <span data-ttu-id="32ed8-154">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="32ed8-154">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

        <span data-ttu-id="32ed8-155">The diagram looks like:</span><span class="sxs-lookup"><span data-stu-id="32ed8-155">The diagram looks like:</span></span>

        <span data-ttu-id="32ed8-156">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="32ed8-156">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

        <span data-ttu-id="32ed8-157">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-157">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="32ed8-158">Click the down arrow next to **ActualTemp** and **TragetTemp** in the Visualizations pane, you can see **Sum** is selected.</span><span class="sxs-lookup"><span data-stu-id="32ed8-158">Click the down arrow next to **ActualTemp** and **TragetTemp** in the Visualizations pane, you can see **Sum** is selected.</span></span>

    3. <span data-ttu-id="32ed8-159">Click the down arrows next to **ActualTemp** and **TragetTemp** in the Visualizations pane, select **Average** to get an average of actual and target temperatures for each building.</span><span class="sxs-lookup"><span data-stu-id="32ed8-159">Click the down arrows next to **ActualTemp** and **TragetTemp** in the Visualizations pane, select **Average** to get an average of actual and target temperatures for each building.</span></span>

        <span data-ttu-id="32ed8-160">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="32ed8-160">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

        <span data-ttu-id="32ed8-161">Your data visualization shall be similar to the one in the screenshot.</span><span class="sxs-lookup"><span data-stu-id="32ed8-161">Your data visualization shall be similar to the one in the screenshot.</span></span> <span data-ttu-id="32ed8-162">Move your cursor over the visualization to get tool tips with relevant data.</span><span class="sxs-lookup"><span data-stu-id="32ed8-162">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

        <span data-ttu-id="32ed8-163">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-area-graph-sum.png "Create Spark data visualizations using Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="32ed8-163">![Create Spark data visualizations using Apache Spark BI](./media/apache-spark-use-bi-tools/apache-spark-bi-area-graph-sum.png "Create Spark data visualizations using Apache Spark BI")</span></span>

7. <span data-ttu-id="32ed8-164">Click **File** then **Save**, and enter the name `BuildingTemperature.pbix` for the file.</span><span class="sxs-lookup"><span data-stu-id="32ed8-164">Click **File** then **Save**, and enter the name `BuildingTemperature.pbix` for the file.</span></span> 

### <a name="publish-the-report-to-the-power-bi-service-optional"></a><span data-ttu-id="32ed8-165">Publish the report to the Power BI Service (optional)</span><span class="sxs-lookup"><span data-stu-id="32ed8-165">Publish the report to the Power BI Service (optional)</span></span>

<span data-ttu-id="32ed8-166">The Power BI service allows you to share reports and dashboards across your organization.</span><span class="sxs-lookup"><span data-stu-id="32ed8-166">The Power BI service allows you to share reports and dashboards across your organization.</span></span> <span data-ttu-id="32ed8-167">In this section, you first publish the dataset and the report.</span><span class="sxs-lookup"><span data-stu-id="32ed8-167">In this section, you first publish the dataset and the report.</span></span> <span data-ttu-id="32ed8-168">Then, you pin the report to a dashboard.</span><span class="sxs-lookup"><span data-stu-id="32ed8-168">Then, you pin the report to a dashboard.</span></span> <span data-ttu-id="32ed8-169">Dashboards are typically used to focus on a subset of data in a report; you have only one visualization in your report, but it's still useful to go through the steps.</span><span class="sxs-lookup"><span data-stu-id="32ed8-169">Dashboards are typically used to focus on a subset of data in a report; you have only one visualization in your report, but it's still useful to go through the steps.</span></span>

1. <span data-ttu-id="32ed8-170">Open Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="32ed8-170">Open Power BI Desktop.</span></span>
2. <span data-ttu-id="32ed8-171">From the **Home** tab, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-171">From the **Home** tab, click **Publish**.</span></span>

    <span data-ttu-id="32ed8-172">![Publish from Power BI Desktop](./media/apache-spark-use-bi-tools/apache-spark-bi-publish.png "Publish from Power BI Desktop")</span><span class="sxs-lookup"><span data-stu-id="32ed8-172">![Publish from Power BI Desktop](./media/apache-spark-use-bi-tools/apache-spark-bi-publish.png "Publish from Power BI Desktop")</span></span>

2. <span data-ttu-id="32ed8-173">Select a workspace to publish your dataset and report to, then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-173">Select a workspace to publish your dataset and report to, then click **Select**.</span></span> <span data-ttu-id="32ed8-174">In the following image, the default **My Workspace** is selected.</span><span class="sxs-lookup"><span data-stu-id="32ed8-174">In the following image, the default **My Workspace** is selected.</span></span>

    <span data-ttu-id="32ed8-175">![Select workspace to publish dataset and report to](./media/apache-spark-use-bi-tools/apache-spark-bi-select-workspace.png "Select workspace to publish dataset and report to")</span><span class="sxs-lookup"><span data-stu-id="32ed8-175">![Select workspace to publish dataset and report to](./media/apache-spark-use-bi-tools/apache-spark-bi-select-workspace.png "Select workspace to publish dataset and report to")</span></span> 

3. <span data-ttu-id="32ed8-176">After the publishing is succeeded, click **Open 'BuildingTemperature.pbix' in Power BI**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-176">After the publishing is succeeded, click **Open 'BuildingTemperature.pbix' in Power BI**.</span></span>

    <span data-ttu-id="32ed8-177">![Publish success, click to enter credentials](./media/apache-spark-use-bi-tools/apache-spark-bi-publish-success.png "Publish success, click to enter credentials")</span><span class="sxs-lookup"><span data-stu-id="32ed8-177">![Publish success, click to enter credentials](./media/apache-spark-use-bi-tools/apache-spark-bi-publish-success.png "Publish success, click to enter credentials")</span></span> 

4. <span data-ttu-id="32ed8-178">In the Power BI service, click **Enter credentials**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-178">In the Power BI service, click **Enter credentials**.</span></span>

    <span data-ttu-id="32ed8-179">![Enter credentials in Power BI service](./media/apache-spark-use-bi-tools/apache-spark-bi-enter-credentials.png "Enter credentials in Power BI service")</span><span class="sxs-lookup"><span data-stu-id="32ed8-179">![Enter credentials in Power BI service](./media/apache-spark-use-bi-tools/apache-spark-bi-enter-credentials.png "Enter credentials in Power BI service")</span></span>

5. <span data-ttu-id="32ed8-180">Click **Edit credentials**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-180">Click **Edit credentials**.</span></span>

    <span data-ttu-id="32ed8-181">![Edit credentials in Power BI service](./media/apache-spark-use-bi-tools/apache-spark-bi-edit-credentials.png "Edit credentials in Power BI service")</span><span class="sxs-lookup"><span data-stu-id="32ed8-181">![Edit credentials in Power BI service](./media/apache-spark-use-bi-tools/apache-spark-bi-edit-credentials.png "Edit credentials in Power BI service")</span></span>

6. <span data-ttu-id="32ed8-182">Enter the HDInsight login account information, and then click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-182">Enter the HDInsight login account information, and then click **Sign in**.</span></span> <span data-ttu-id="32ed8-183">The default account name is *admin*.</span><span class="sxs-lookup"><span data-stu-id="32ed8-183">The default account name is *admin*.</span></span>

    <span data-ttu-id="32ed8-184">![Sign in to Spark cluster](./media/apache-spark-use-bi-tools/apache-spark-bi-sign-in.png "Sign in to Spark cluster")</span><span class="sxs-lookup"><span data-stu-id="32ed8-184">![Sign in to Spark cluster](./media/apache-spark-use-bi-tools/apache-spark-bi-sign-in.png "Sign in to Spark cluster")</span></span>

7. <span data-ttu-id="32ed8-185">In the left pane, go to **Workspaces** > **My Workspace** > **REPORTS**, then click **BuildingTemperature**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-185">In the left pane, go to **Workspaces** > **My Workspace** > **REPORTS**, then click **BuildingTemperature**.</span></span>

    <span data-ttu-id="32ed8-186">![Report listed under reports in left pane](./media/apache-spark-use-bi-tools/apache-spark-bi-service-left-pane.png "Report listed under reports in left pane")</span><span class="sxs-lookup"><span data-stu-id="32ed8-186">![Report listed under reports in left pane](./media/apache-spark-use-bi-tools/apache-spark-bi-service-left-pane.png "Report listed under reports in left pane")</span></span>

    <span data-ttu-id="32ed8-187">You should also see **BuildingTemperature** listed under **DATASETS** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="32ed8-187">You should also see **BuildingTemperature** listed under **DATASETS** in the left pane.</span></span>

    <span data-ttu-id="32ed8-188">The visual you created in Power BI Desktop is now available in the Power BI service.</span><span class="sxs-lookup"><span data-stu-id="32ed8-188">The visual you created in Power BI Desktop is now available in the Power BI service.</span></span> 

8. <span data-ttu-id="32ed8-189">Hover your cursor over the visualization, and then click the pin icon on the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="32ed8-189">Hover your cursor over the visualization, and then click the pin icon on the upper right corner.</span></span>

    <span data-ttu-id="32ed8-190">![Report in the Power BI service](./media/apache-spark-use-bi-tools/apache-spark-bi-service-report.png "Report in the Power BI service")</span><span class="sxs-lookup"><span data-stu-id="32ed8-190">![Report in the Power BI service](./media/apache-spark-use-bi-tools/apache-spark-bi-service-report.png "Report in the Power BI service")</span></span>

9. <span data-ttu-id="32ed8-191">Select "New dashboard", enter the name `Building temperature`, then click **Pin**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-191">Select "New dashboard", enter the name `Building temperature`, then click **Pin**.</span></span>

    <span data-ttu-id="32ed8-192">![Pin to new dashboard](./media/apache-spark-use-bi-tools/apache-spark-bi-pin-dashboard.png "Pin to new dashboard")</span><span class="sxs-lookup"><span data-stu-id="32ed8-192">![Pin to new dashboard](./media/apache-spark-use-bi-tools/apache-spark-bi-pin-dashboard.png "Pin to new dashboard")</span></span>

10. <span data-ttu-id="32ed8-193">In the report, click **Go to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="32ed8-193">In the report, click **Go to dashboard**.</span></span> 

<span data-ttu-id="32ed8-194">Your visual is pinned to the dashboard - you can add other visuals to the report and pin them to the same dashboard.</span><span class="sxs-lookup"><span data-stu-id="32ed8-194">Your visual is pinned to the dashboard - you can add other visuals to the report and pin them to the same dashboard.</span></span> <span data-ttu-id="32ed8-195">For more information about reports and dashboards, see [Reports in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-reports/)and [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="32ed8-195">For more information about reports and dashboards, see [Reports in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-reports/)and [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>

<!--
## <a name="tableau"></a>Use Tableau Desktop 

> [!NOTE]
> This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.
>
>

1. Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.

2. Make sure that computer also has Microsoft Spark ODBC driver installed. You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Launch Tableau Desktop. In the left pane, from the list of server to connect to, click **Spark SQL**. If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.
2. In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.

    ![Connect to a cluster for Apache Spark BI](./media/apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")

    The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.
3. On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.

    ![Find schema for Apache Spark BI](./media/apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")
4. For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster. You should see the **hvac** table you created earlier using the notebook.

    ![Find table for Apache Spark BI](./media/apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")
5. Drag and drop the table to the top box on the right. Tableau imports the data and displays the schema as highlighted by the red box.

    ![Add tables to Tableau for Apache Spark BI](./media/apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")
6. Click the **Sheet1** tab at the bottom left. Make a visualization that shows the average target and actual temperatures for all buildings for each date. Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**. Under **Marks**, select **Area** to use an area map for Spark data visualization.

     ![Add fields for Spark data visualization](./media/apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")
7. By default, the temperature fields are shown as aggregate. If you want to show the average temperatures instead, you can do so from the drop-down, as shown in the following screenshot:

    ![Take average of temperature for Spark data visualization](./media/apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")

8. You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures. Move the mouse to the corner of the lower area map until you see the handle shape highlighted in a red circle. Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.

    ![Merge maps for Spark data visualization](./media/apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")

     Your data visualization should change as shown in the screenshot:

    ![Tableau output for Spark data visualization](./media/apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")
9. Click **Save** to save the worksheet. You can create dashboards and add one or more sheets to it.
-->

## <a name="next-steps"></a><span data-ttu-id="32ed8-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="32ed8-196">Next steps</span></span>

<span data-ttu-id="32ed8-197">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="32ed8-197">In this tutorial, you learned how to:</span></span>

- <span data-ttu-id="32ed8-198">Visualize Spark data using Power BI.</span><span class="sxs-lookup"><span data-stu-id="32ed8-198">Visualize Spark data using Power BI.</span></span>

<span data-ttu-id="32ed8-199">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI.</span><span class="sxs-lookup"><span data-stu-id="32ed8-199">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI.</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="32ed8-200">Run a Spark streaming job</span><span class="sxs-lookup"><span data-stu-id="32ed8-200">Run a Spark streaming job</span></span>](apache-spark-eventhub-streaming.md)

