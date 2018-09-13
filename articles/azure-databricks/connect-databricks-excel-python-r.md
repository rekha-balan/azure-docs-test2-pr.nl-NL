---
title: Connect to Azure Databricks from Excel, Python, or R | Microsoft Docs
description: Learn how to use the Simba driver to connect Azure Databricks to Excel, Python, or R.
services: azure-databricks
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: nitinme
ms.openlocfilehash: 333ff3ac3de053eae604ffeab600df7d35874f69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871444"
---
# <a name="connect-to-azure-databricks-from-excel-python-or-r"></a><span data-ttu-id="ceca5-103">Connect to Azure Databricks from Excel, Python, or R</span><span class="sxs-lookup"><span data-stu-id="ceca5-103">Connect to Azure Databricks from Excel, Python, or R</span></span>

<span data-ttu-id="ceca5-104">In this article, you learn how to use the Databricks ODBC driver to connect Azure Databricks with Microsoft Excel, Python, or R language.</span><span class="sxs-lookup"><span data-stu-id="ceca5-104">In this article, you learn how to use the Databricks ODBC driver to connect Azure Databricks with Microsoft Excel, Python, or R language.</span></span> <span data-ttu-id="ceca5-105">Once you establish the connection, you can access the data in Azure Databricks from the Excel, Python, or R clients.</span><span class="sxs-lookup"><span data-stu-id="ceca5-105">Once you establish the connection, you can access the data in Azure Databricks from the Excel, Python, or R clients.</span></span> <span data-ttu-id="ceca5-106">You can also use the clients to further analyze the data.</span><span class="sxs-lookup"><span data-stu-id="ceca5-106">You can also use the clients to further analyze the data.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ceca5-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ceca5-107">Prerequisites</span></span>

* <span data-ttu-id="ceca5-108">You must have an Azure Databricks workspace, a Spark cluster, and sample data associated with your cluster.</span><span class="sxs-lookup"><span data-stu-id="ceca5-108">You must have an Azure Databricks workspace, a Spark cluster, and sample data associated with your cluster.</span></span> <span data-ttu-id="ceca5-109">If you do not already have these prerequisites, complete the quickstart at [Run a Spark job on Azure Databricks using the Azure portal](quickstart-create-databricks-workspace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ceca5-109">If you do not already have these prerequisites, complete the quickstart at [Run a Spark job on Azure Databricks using the Azure portal](quickstart-create-databricks-workspace-portal.md).</span></span>

* <span data-ttu-id="ceca5-110">Download the Databricks ODBC driver from [Databricks driver download page](https://databricks.com/spark/odbc-driver-download).</span><span class="sxs-lookup"><span data-stu-id="ceca5-110">Download the Databricks ODBC driver from [Databricks driver download page](https://databricks.com/spark/odbc-driver-download).</span></span> <span data-ttu-id="ceca5-111">Install the 32-bit or 64-bit version depending on the application from where you want to connect to Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-111">Install the 32-bit or 64-bit version depending on the application from where you want to connect to Azure Databricks.</span></span> <span data-ttu-id="ceca5-112">For example, to connect from Excel, install the 32-bit version of the driver.</span><span class="sxs-lookup"><span data-stu-id="ceca5-112">For example, to connect from Excel, install the 32-bit version of the driver.</span></span> <span data-ttu-id="ceca5-113">To connect from R and Python, install the 64-bit version of the driver.</span><span class="sxs-lookup"><span data-stu-id="ceca5-113">To connect from R and Python, install the 64-bit version of the driver.</span></span>

* <span data-ttu-id="ceca5-114">Set up a personal access token in Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-114">Set up a personal access token in Databricks.</span></span> <span data-ttu-id="ceca5-115">For instructions, see [Token management](https://docs.azuredatabricks.net/api/latest/authentication.html#token-management).</span><span class="sxs-lookup"><span data-stu-id="ceca5-115">For instructions, see [Token management](https://docs.azuredatabricks.net/api/latest/authentication.html#token-management).</span></span>

## <a name="set-up-a-dsn"></a><span data-ttu-id="ceca5-116">Set up a DSN</span><span class="sxs-lookup"><span data-stu-id="ceca5-116">Set up a DSN</span></span>

<span data-ttu-id="ceca5-117">A data source name (DSN) contains the information about a specific data source.</span><span class="sxs-lookup"><span data-stu-id="ceca5-117">A data source name (DSN) contains the information about a specific data source.</span></span> <span data-ttu-id="ceca5-118">An ODBC driver needs this DSN to connect to a data source.</span><span class="sxs-lookup"><span data-stu-id="ceca5-118">An ODBC driver needs this DSN to connect to a data source.</span></span> <span data-ttu-id="ceca5-119">In this section, you set up a DSN that can be used with the Databricks ODBC driver to connect to Azure Databricks from clients like Microsoft Excel, Python, or R.</span><span class="sxs-lookup"><span data-stu-id="ceca5-119">In this section, you set up a DSN that can be used with the Databricks ODBC driver to connect to Azure Databricks from clients like Microsoft Excel, Python, or R.</span></span>

1. <span data-ttu-id="ceca5-120">From the Azure Databricks workspace, navigate to the Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="ceca5-120">From the Azure Databricks workspace, navigate to the Databricks cluster.</span></span>

    <span data-ttu-id="ceca5-121">![Open Databricks cluster](./media/connect-databricks-excel-python-r/open-databricks-cluster.png "Open Databricks cluster")</span><span class="sxs-lookup"><span data-stu-id="ceca5-121">![Open Databricks cluster](./media/connect-databricks-excel-python-r/open-databricks-cluster.png "Open Databricks cluster")</span></span>

2. <span data-ttu-id="ceca5-122">Under the **Configuration** tab, click the **JDBC/ODBC** tab and copy the values for **Server Hostname** and **HTTP Path**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-122">Under the **Configuration** tab, click the **JDBC/ODBC** tab and copy the values for **Server Hostname** and **HTTP Path**.</span></span> <span data-ttu-id="ceca5-123">You need these values to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="ceca5-123">You need these values to complete the steps in this article.</span></span>

    <span data-ttu-id="ceca5-124">![Get Databricks configuration](./media/connect-databricks-excel-python-r/get-databricks-jdbc-configuration.png "Get Databricks configuration")</span><span class="sxs-lookup"><span data-stu-id="ceca5-124">![Get Databricks configuration](./media/connect-databricks-excel-python-r/get-databricks-jdbc-configuration.png "Get Databricks configuration")</span></span>

3. <span data-ttu-id="ceca5-125">On your computer, start **ODBC Data Sources** application (32-bit or 64-bit) depending on the application.</span><span class="sxs-lookup"><span data-stu-id="ceca5-125">On your computer, start **ODBC Data Sources** application (32-bit or 64-bit) depending on the application.</span></span> <span data-ttu-id="ceca5-126">To connect from Excel, use the 32-bit version.</span><span class="sxs-lookup"><span data-stu-id="ceca5-126">To connect from Excel, use the 32-bit version.</span></span> <span data-ttu-id="ceca5-127">To connect from R and Python, use the 64-bit version.</span><span class="sxs-lookup"><span data-stu-id="ceca5-127">To connect from R and Python, use the 64-bit version.</span></span>

    <span data-ttu-id="ceca5-128">![Launch ODBC](./media/connect-databricks-excel-python-r/launch-odbc-app.png "Launch ODBC app")</span><span class="sxs-lookup"><span data-stu-id="ceca5-128">![Launch ODBC](./media/connect-databricks-excel-python-r/launch-odbc-app.png "Launch ODBC app")</span></span>

4. <span data-ttu-id="ceca5-129">Under the **User DSN** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-129">Under the **User DSN** tab, click **Add**.</span></span> <span data-ttu-id="ceca5-130">In the **Create New Data Source** dialog box, select the **Simba Spark ODBC Driver**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-130">In the **Create New Data Source** dialog box, select the **Simba Spark ODBC Driver**, and then click **Finish**.</span></span>

    <span data-ttu-id="ceca5-131">![Launch ODBC](./media/connect-databricks-excel-python-r/add-new-user-dsn.png "Launch ODBC app")</span><span class="sxs-lookup"><span data-stu-id="ceca5-131">![Launch ODBC](./media/connect-databricks-excel-python-r/add-new-user-dsn.png "Launch ODBC app")</span></span>

5. <span data-ttu-id="ceca5-132">In the **Simba Spark ODBC Driver** dialog box, provide the following values:</span><span class="sxs-lookup"><span data-stu-id="ceca5-132">In the **Simba Spark ODBC Driver** dialog box, provide the following values:</span></span>

    <span data-ttu-id="ceca5-133">![Configure DSN](./media/connect-databricks-excel-python-r/odbc-dsn-setup.png "Configure DSN")</span><span class="sxs-lookup"><span data-stu-id="ceca5-133">![Configure DSN](./media/connect-databricks-excel-python-r/odbc-dsn-setup.png "Configure DSN")</span></span>

    <span data-ttu-id="ceca5-134">The following table provides information on the values to provide in the dialog box.</span><span class="sxs-lookup"><span data-stu-id="ceca5-134">The following table provides information on the values to provide in the dialog box.</span></span>
    
    |<span data-ttu-id="ceca5-135">Field</span><span class="sxs-lookup"><span data-stu-id="ceca5-135">Field</span></span>  | <span data-ttu-id="ceca5-136">Value</span><span class="sxs-lookup"><span data-stu-id="ceca5-136">Value</span></span>  |
    |---------|---------|
    |<span data-ttu-id="ceca5-137">**Data Source Name**</span><span class="sxs-lookup"><span data-stu-id="ceca5-137">**Data Source Name**</span></span>     | <span data-ttu-id="ceca5-138">Provide a name for the data source.</span><span class="sxs-lookup"><span data-stu-id="ceca5-138">Provide a name for the data source.</span></span>        |
    |<span data-ttu-id="ceca5-139">**Host(s)**</span><span class="sxs-lookup"><span data-stu-id="ceca5-139">**Host(s)**</span></span>     | <span data-ttu-id="ceca5-140">Provide the value that you copied from the Databricks workspace for *Server hostname*.</span><span class="sxs-lookup"><span data-stu-id="ceca5-140">Provide the value that you copied from the Databricks workspace for *Server hostname*.</span></span>        |
    |<span data-ttu-id="ceca5-141">**Port**</span><span class="sxs-lookup"><span data-stu-id="ceca5-141">**Port**</span></span>     | <span data-ttu-id="ceca5-142">Enter *443*.</span><span class="sxs-lookup"><span data-stu-id="ceca5-142">Enter *443*.</span></span>        |
    |<span data-ttu-id="ceca5-143">**Authentication** > **Mechanism**</span><span class="sxs-lookup"><span data-stu-id="ceca5-143">**Authentication** > **Mechanism**</span></span>     | <span data-ttu-id="ceca5-144">Select *User name and password*.</span><span class="sxs-lookup"><span data-stu-id="ceca5-144">Select *User name and password*.</span></span>        |
    |<span data-ttu-id="ceca5-145">**User name**</span><span class="sxs-lookup"><span data-stu-id="ceca5-145">**User name**</span></span>     | <span data-ttu-id="ceca5-146">Enter *token*.</span><span class="sxs-lookup"><span data-stu-id="ceca5-146">Enter *token*.</span></span>        |
    |<span data-ttu-id="ceca5-147">**Password**</span><span class="sxs-lookup"><span data-stu-id="ceca5-147">**Password**</span></span>     | <span data-ttu-id="ceca5-148">Enter the token value that you copied from the Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="ceca5-148">Enter the token value that you copied from the Databricks workspace.</span></span> |
    
    <span data-ttu-id="ceca5-149">Perform the following additional steps in the DSN setup dialog box.</span><span class="sxs-lookup"><span data-stu-id="ceca5-149">Perform the following additional steps in the DSN setup dialog box.</span></span>
    
    * <span data-ttu-id="ceca5-150">Click **HTTP Options**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-150">Click **HTTP Options**.</span></span> <span data-ttu-id="ceca5-151">In the dialog box that opens up, paste the value for *HTTP Path* that you copied from Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="ceca5-151">In the dialog box that opens up, paste the value for *HTTP Path* that you copied from Databricks workspace.</span></span> <span data-ttu-id="ceca5-152">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-152">Click **OK**.</span></span>
    * <span data-ttu-id="ceca5-153">Click **SSL Options**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-153">Click **SSL Options**.</span></span> <span data-ttu-id="ceca5-154">In the dialog box that opens up, select the **Enable SSL** check box.</span><span class="sxs-lookup"><span data-stu-id="ceca5-154">In the dialog box that opens up, select the **Enable SSL** check box.</span></span> <span data-ttu-id="ceca5-155">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-155">Click **OK**.</span></span>
    * <span data-ttu-id="ceca5-156">Click **Test** to test the connection to Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-156">Click **Test** to test the connection to Azure Databricks.</span></span> <span data-ttu-id="ceca5-157">Click **OK** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="ceca5-157">Click **OK** to save the configuration.</span></span>
    * <span data-ttu-id="ceca5-158">In the **ODBC Data Source Administrator** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-158">In the **ODBC Data Source Administrator** dialog box, click **OK**.</span></span>

<span data-ttu-id="ceca5-159">You now have your DSN set up.</span><span class="sxs-lookup"><span data-stu-id="ceca5-159">You now have your DSN set up.</span></span> <span data-ttu-id="ceca5-160">In the next sections, you use this DSN to connect to Azure Databricks from Excel, Python, or R.</span><span class="sxs-lookup"><span data-stu-id="ceca5-160">In the next sections, you use this DSN to connect to Azure Databricks from Excel, Python, or R.</span></span>

## <a name="connect-from-microsoft-excel"></a><span data-ttu-id="ceca5-161">Connect from Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="ceca5-161">Connect from Microsoft Excel</span></span>

<span data-ttu-id="ceca5-162">In this section, you pull data from Azure Databricks into Microsoft Excel using the DSN you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ceca5-162">In this section, you pull data from Azure Databricks into Microsoft Excel using the DSN you created earlier.</span></span> <span data-ttu-id="ceca5-163">Before you begin, make sure you have Microsoft Excel installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="ceca5-163">Before you begin, make sure you have Microsoft Excel installed on your computer.</span></span> <span data-ttu-id="ceca5-164">You can use a trial version of Excel from [Microsoft Excel trial link](https://products.office.com/excel).</span><span class="sxs-lookup"><span data-stu-id="ceca5-164">You can use a trial version of Excel from [Microsoft Excel trial link](https://products.office.com/excel).</span></span>

1. <span data-ttu-id="ceca5-165">Open a blank workbook in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="ceca5-165">Open a blank workbook in Microsoft Excel.</span></span> <span data-ttu-id="ceca5-166">From the **Data** ribbon, click **Get Data**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-166">From the **Data** ribbon, click **Get Data**.</span></span> <span data-ttu-id="ceca5-167">Click **From Other Sources** and then click **From ODBC**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-167">Click **From Other Sources** and then click **From ODBC**.</span></span>

    <span data-ttu-id="ceca5-168">![Launch ODBC from Excel](./media/connect-databricks-excel-python-r/launch-odbc-from-excel.png "Launch ODBC from Excel")</span><span class="sxs-lookup"><span data-stu-id="ceca5-168">![Launch ODBC from Excel](./media/connect-databricks-excel-python-r/launch-odbc-from-excel.png "Launch ODBC from Excel")</span></span>

2. <span data-ttu-id="ceca5-169">In the **From ODBC** dialog box, select the DSN that you created earlier and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-169">In the **From ODBC** dialog box, select the DSN that you created earlier and then click **OK**.</span></span>

    <span data-ttu-id="ceca5-170">![Select DSN](./media/connect-databricks-excel-python-r/excel-select-dsn.png "Select DSN")</span><span class="sxs-lookup"><span data-stu-id="ceca5-170">![Select DSN](./media/connect-databricks-excel-python-r/excel-select-dsn.png "Select DSN")</span></span>

3. <span data-ttu-id="ceca5-171">If you are prompted for credentials, for user name enter **token**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-171">If you are prompted for credentials, for user name enter **token**.</span></span> <span data-ttu-id="ceca5-172">For password, provide the token value that you retrieved from the Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="ceca5-172">For password, provide the token value that you retrieved from the Databricks workspace.</span></span>

    <span data-ttu-id="ceca5-173">![Provide credentials for Databricks](./media/connect-databricks-excel-python-r/excel-databricks-token.png "Select DSN")</span><span class="sxs-lookup"><span data-stu-id="ceca5-173">![Provide credentials for Databricks](./media/connect-databricks-excel-python-r/excel-databricks-token.png "Select DSN")</span></span>

4. <span data-ttu-id="ceca5-174">From the navigator window, select the table in Databricks that you want to load to Excel, and then click **Load**.</span><span class="sxs-lookup"><span data-stu-id="ceca5-174">From the navigator window, select the table in Databricks that you want to load to Excel, and then click **Load**.</span></span> 

    <span data-ttu-id="ceca5-175">![Load dta into Excel](./media/connect-databricks-excel-python-r/excel-load-data.png "Load dta into Excel")</span><span class="sxs-lookup"><span data-stu-id="ceca5-175">![Load dta into Excel](./media/connect-databricks-excel-python-r/excel-load-data.png "Load dta into Excel")</span></span>

<span data-ttu-id="ceca5-176">Once you have the data in your Excel workbook, you can perform analytical operations on it.</span><span class="sxs-lookup"><span data-stu-id="ceca5-176">Once you have the data in your Excel workbook, you can perform analytical operations on it.</span></span>

## <a name="connect-from-r"></a><span data-ttu-id="ceca5-177">Connect from R</span><span class="sxs-lookup"><span data-stu-id="ceca5-177">Connect from R</span></span>

> [!NOTE]
> <span data-ttu-id="ceca5-178">This section provides information on how to integrate an R Studio client running on your desktop with Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-178">This section provides information on how to integrate an R Studio client running on your desktop with Azure Databricks.</span></span> <span data-ttu-id="ceca5-179">For instructions on how to use R Studio on the Azure Databricks cluster itself, see [R Studio on Azure Databricks](https://docs.azuredatabricks.net/spark/latest/sparkr/rstudio.html).</span><span class="sxs-lookup"><span data-stu-id="ceca5-179">For instructions on how to use R Studio on the Azure Databricks cluster itself, see [R Studio on Azure Databricks](https://docs.azuredatabricks.net/spark/latest/sparkr/rstudio.html).</span></span>

<span data-ttu-id="ceca5-180">In this section, you use an R language IDE to reference data available in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-180">In this section, you use an R language IDE to reference data available in Azure Databricks.</span></span> <span data-ttu-id="ceca5-181">Before you begin, you must have the following installed on the computer.</span><span class="sxs-lookup"><span data-stu-id="ceca5-181">Before you begin, you must have the following installed on the computer.</span></span>

* <span data-ttu-id="ceca5-182">An IDE for R language.</span><span class="sxs-lookup"><span data-stu-id="ceca5-182">An IDE for R language.</span></span> <span data-ttu-id="ceca5-183">This article uses RStudio for Desktop.</span><span class="sxs-lookup"><span data-stu-id="ceca5-183">This article uses RStudio for Desktop.</span></span> <span data-ttu-id="ceca5-184">You can install it from [R Studio download](https://www.rstudio.com/products/rstudio/download/).</span><span class="sxs-lookup"><span data-stu-id="ceca5-184">You can install it from [R Studio download](https://www.rstudio.com/products/rstudio/download/).</span></span>
* <span data-ttu-id="ceca5-185">If you use RStudio for Desktop as your IDE, also install Microsoft R Client from [http://aka.ms/rclient/](http://aka.ms/rclient/).</span><span class="sxs-lookup"><span data-stu-id="ceca5-185">If you use RStudio for Desktop as your IDE, also install Microsoft R Client from [http://aka.ms/rclient/](http://aka.ms/rclient/).</span></span> 

<span data-ttu-id="ceca5-186">Open RStudio and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="ceca5-186">Open RStudio and do the following steps:</span></span>

- <span data-ttu-id="ceca5-187">Reference the `RODBC` package.</span><span class="sxs-lookup"><span data-stu-id="ceca5-187">Reference the `RODBC` package.</span></span> <span data-ttu-id="ceca5-188">This enables you to connect to Azure Databricks using the DSN you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ceca5-188">This enables you to connect to Azure Databricks using the DSN you created earlier.</span></span>
- <span data-ttu-id="ceca5-189">Establish a connection using the DSN.</span><span class="sxs-lookup"><span data-stu-id="ceca5-189">Establish a connection using the DSN.</span></span>
- <span data-ttu-id="ceca5-190">Run a SQL query on the data in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-190">Run a SQL query on the data in Azure Databricks.</span></span> <span data-ttu-id="ceca5-191">In the following snippet, *radio_sample_data* is a table that already exists in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-191">In the following snippet, *radio_sample_data* is a table that already exists in Azure Databricks.</span></span>
- <span data-ttu-id="ceca5-192">Perform some operations on the query to verify the output.</span><span class="sxs-lookup"><span data-stu-id="ceca5-192">Perform some operations on the query to verify the output.</span></span> 

<span data-ttu-id="ceca5-193">The following code snippet performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="ceca5-193">The following code snippet performs these tasks:</span></span>

    # reference the 'RODBC' package
    require(RODBC)
    
    # establish a connection using the DSN you created earlier
    conn <- odbcConnect("<ENTER DSN NAME HERE>")
    
    # run a SQL query using the connection you created
    res <- sqlQuery(conn, "SELECT * FROM radio_sample_data")
    
    # print out the column names in the query output
    names(res) 
        
    # print out the number of rows in the query output
    nrow (res)

## <a name="connect-from-python"></a><span data-ttu-id="ceca5-194">Connect from Python</span><span class="sxs-lookup"><span data-stu-id="ceca5-194">Connect from Python</span></span>

<span data-ttu-id="ceca5-195">In this section, you use a Python IDE (such as IDLE) to reference data available in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-195">In this section, you use a Python IDE (such as IDLE) to reference data available in Azure Databricks.</span></span> <span data-ttu-id="ceca5-196">Before you begin, complete the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="ceca5-196">Before you begin, complete the following prerequisites:</span></span>

* <span data-ttu-id="ceca5-197">Install Python from [here](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ceca5-197">Install Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="ceca5-198">Installing Python from this link also installs IDLE.</span><span class="sxs-lookup"><span data-stu-id="ceca5-198">Installing Python from this link also installs IDLE.</span></span>

* <span data-ttu-id="ceca5-199">From a command prompt on the computer, install the `pyodbc` package.</span><span class="sxs-lookup"><span data-stu-id="ceca5-199">From a command prompt on the computer, install the `pyodbc` package.</span></span> <span data-ttu-id="ceca5-200">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="ceca5-200">Run the following command:</span></span>

      pip install pyodbc

<span data-ttu-id="ceca5-201">Open IDLE and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="ceca5-201">Open IDLE and do the following steps:</span></span>

- <span data-ttu-id="ceca5-202">Import the `pyodbc` package.</span><span class="sxs-lookup"><span data-stu-id="ceca5-202">Import the `pyodbc` package.</span></span> <span data-ttu-id="ceca5-203">This enables you to connect to Azure Databricks using the DSN you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ceca5-203">This enables you to connect to Azure Databricks using the DSN you created earlier.</span></span>
- <span data-ttu-id="ceca5-204">Establish a connection using the DSN you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ceca5-204">Establish a connection using the DSN you created earlier.</span></span>
-  <span data-ttu-id="ceca5-205">Run a SQL query using the connection you created.</span><span class="sxs-lookup"><span data-stu-id="ceca5-205">Run a SQL query using the connection you created.</span></span> <span data-ttu-id="ceca5-206">In the following snippet, *radio_sample_data* is a table that already exists in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ceca5-206">In the following snippet, *radio_sample_data* is a table that already exists in Azure Databricks.</span></span>
- <span data-ttu-id="ceca5-207">Perform operations on the query to verify the output.</span><span class="sxs-lookup"><span data-stu-id="ceca5-207">Perform operations on the query to verify the output.</span></span>

<span data-ttu-id="ceca5-208">The following code snippet performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="ceca5-208">The following code snippet performs these tasks:</span></span>

```python
# import the `pyodbc` package:
import pyodbc

# establish a connection using the DSN you created earlier
conn = pyodbc.connect("DSN=<ENTER DSN NAME HERE>", autocommit = True)

# run a SQL query using the connection you created
cursor = conn.cursor()
cursor.execute("SELECT * FROM radio_sample_data")

# print the rows retrieved by the query.
for row in cursor.fetchall():
    print(row)

```

## <a name="next-steps"></a><span data-ttu-id="ceca5-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="ceca5-209">Next steps</span></span>

* <span data-ttu-id="ceca5-210">To learn about sources from where you can import data into Azure Databricks, see [Data sources for Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html#)</span><span class="sxs-lookup"><span data-stu-id="ceca5-210">To learn about sources from where you can import data into Azure Databricks, see [Data sources for Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html#)</span></span>


