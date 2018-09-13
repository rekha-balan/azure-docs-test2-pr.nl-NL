---
title: Run SSIS package with Stored Procedure Activity - Azure | Microsoft Docs
description: This article describes how to run a SQL Server Integration Services (SSIS) package in an Azure Data Factory pipeline by using the Stored Procedure Activity.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: jingwang
ms.openlocfilehash: 42abb5fdaf05424d5f39ecf4a2c88afcefd17312
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867547"
---
# <a name="run-an-ssis-package-with-the-stored-procedure-activity-in-azure-data-factory"></a><span data-ttu-id="b6028-103">Run an SSIS package with the Stored Procedure activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b6028-103">Run an SSIS package with the Stored Procedure activity in Azure Data Factory</span></span>
<span data-ttu-id="b6028-104">This article describes how to run an SSIS package in an Azure Data Factory pipeline by using a Stored Procedure activity.</span><span class="sxs-lookup"><span data-stu-id="b6028-104">This article describes how to run an SSIS package in an Azure Data Factory pipeline by using a Stored Procedure activity.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b6028-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b6028-105">Prerequisites</span></span>

### <a name="azure-sql-database"></a><span data-ttu-id="b6028-106">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b6028-106">Azure SQL Database</span></span> 
<span data-ttu-id="b6028-107">The walkthrough in this article uses an Azure SQL database that hosts the SSIS catalog.</span><span class="sxs-lookup"><span data-stu-id="b6028-107">The walkthrough in this article uses an Azure SQL database that hosts the SSIS catalog.</span></span> <span data-ttu-id="b6028-108">You can also use an Azure SQL Managed Instance (Preview).</span><span class="sxs-lookup"><span data-stu-id="b6028-108">You can also use an Azure SQL Managed Instance (Preview).</span></span>

## <a name="create-an-azure-ssis-integration-runtime"></a><span data-ttu-id="b6028-109">Create an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="b6028-109">Create an Azure-SSIS integration runtime</span></span>
<span data-ttu-id="b6028-110">Create an Azure-SSIS integration runtime if you don't have one by following the step-by-step instruction in the [Tutorial: Deploy SSIS packages](tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b6028-110">Create an Azure-SSIS integration runtime if you don't have one by following the step-by-step instruction in the [Tutorial: Deploy SSIS packages](tutorial-create-azure-ssis-runtime-portal.md).</span></span>

## <a name="data-factory-ui-azure-portal"></a><span data-ttu-id="b6028-111">Data Factory UI (Azure portal)</span><span class="sxs-lookup"><span data-stu-id="b6028-111">Data Factory UI (Azure portal)</span></span>
<span data-ttu-id="b6028-112">In this section, you use Data Factory UI to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="b6028-112">In this section, you use Data Factory UI to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="b6028-113">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="b6028-113">Create a data factory</span></span>
<span data-ttu-id="b6028-114">First step is to create a data factory by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b6028-114">First step is to create a data factory by using the Azure portal.</span></span> 

1. <span data-ttu-id="b6028-115">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="b6028-115">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="b6028-116">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="b6028-116">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
2. <span data-ttu-id="b6028-117">Navigate to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6028-117">Navigate to the [Azure portal](https://portal.azure.com).</span></span> 
3. <span data-ttu-id="b6028-118">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="b6028-118">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-data-factory-menu.png)
2. <span data-ttu-id="b6028-120">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="b6028-120">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-data-factory.png)
 
   <span data-ttu-id="b6028-122">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="b6028-122">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="b6028-123">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span><span class="sxs-lookup"><span data-stu-id="b6028-123">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span></span> <span data-ttu-id="b6028-124">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="b6028-124">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
     ![Name not available - error](./media/how-to-invoke-ssis-package-stored-procedure-activity/name-not-available-error.png)
3. <span data-ttu-id="b6028-126">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="b6028-126">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="b6028-127">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="b6028-127">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="b6028-128">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b6028-128">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="b6028-129">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="b6028-129">Select **Create new**, and enter the name of a resource group.</span></span>   
         
    <span data-ttu-id="b6028-130">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6028-130">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="b6028-131">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="b6028-131">Select **V2** for the **version**.</span></span>
5. <span data-ttu-id="b6028-132">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="b6028-132">Select the **location** for the data factory.</span></span> <span data-ttu-id="b6028-133">Only locations that are supported by Data Factory are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b6028-133">Only locations that are supported by Data Factory are shown in the drop-down list.</span></span> <span data-ttu-id="b6028-134">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other locations.</span><span class="sxs-lookup"><span data-stu-id="b6028-134">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other locations.</span></span>
6. <span data-ttu-id="b6028-135">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b6028-135">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="b6028-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b6028-136">Click **Create**.</span></span>
8. <span data-ttu-id="b6028-137">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="b6028-137">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media//how-to-invoke-ssis-package-stored-procedure-activity/deploying-data-factory.png)
9. <span data-ttu-id="b6028-139">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="b6028-139">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
    ![Data factory home page](./media/how-to-invoke-ssis-package-stored-procedure-activity/data-factory-home-page.png)
10. <span data-ttu-id="b6028-141">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) application in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="b6028-141">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) application in a separate tab.</span></span> 

### <a name="create-a-pipeline-with-stored-procedure-activity"></a><span data-ttu-id="b6028-142">Create a pipeline with stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="b6028-142">Create a pipeline with stored procedure activity</span></span>
<span data-ttu-id="b6028-143">In this step, you use the Data Factory UI to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="b6028-143">In this step, you use the Data Factory UI to create a pipeline.</span></span> <span data-ttu-id="b6028-144">You add a stored procedure activity to the pipeline and configure it to run the SSIS package by using the sp_executesql stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b6028-144">You add a stored procedure activity to the pipeline and configure it to run the SSIS package by using the sp_executesql stored procedure.</span></span> 

1. <span data-ttu-id="b6028-145">In the get started page, click **Create pipeline**:</span><span class="sxs-lookup"><span data-stu-id="b6028-145">In the get started page, click **Create pipeline**:</span></span> 

    ![Get started page](./media/how-to-invoke-ssis-package-stored-procedure-activity/get-started-page.png)
2. <span data-ttu-id="b6028-147">In the **Activities** toolbox, expand **General**, and drag-drop **Stored Procedure** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="b6028-147">In the **Activities** toolbox, expand **General**, and drag-drop **Stored Procedure** activity to the pipeline designer surface.</span></span> 

    ![Drag-and-drop stored procedure activity](./media/how-to-invoke-ssis-package-stored-procedure-activity/drag-drop-sproc-activity.png)
3. <span data-ttu-id="b6028-149">In the properties window for the stored procedure activity, switch to the **SQL Account** tab, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="b6028-149">In the properties window for the stored procedure activity, switch to the **SQL Account** tab, and click **+ New**.</span></span> <span data-ttu-id="b6028-150">You create a connection to the Azure SQL database that hosts the SSIS Catalog (SSIDB database).</span><span class="sxs-lookup"><span data-stu-id="b6028-150">You create a connection to the Azure SQL database that hosts the SSIS Catalog (SSIDB database).</span></span> 
   
    ![New linked service button](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-linked-service-button.png)
4. <span data-ttu-id="b6028-152">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b6028-152">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="b6028-153">Select **Azure SQL Database** for **Type**.</span><span class="sxs-lookup"><span data-stu-id="b6028-153">Select **Azure SQL Database** for **Type**.</span></span>
    2. <span data-ttu-id="b6028-154">Select the **Default** Azure Integration Runtime to connect to the Azure SQL Database that hosts the `SSISDB` database.</span><span class="sxs-lookup"><span data-stu-id="b6028-154">Select the **Default** Azure Integration Runtime to connect to the Azure SQL Database that hosts the `SSISDB` database.</span></span>
    3. <span data-ttu-id="b6028-155">Select the Azure SQL Database that hosts the SSISDB database for the **Server name** field.</span><span class="sxs-lookup"><span data-stu-id="b6028-155">Select the Azure SQL Database that hosts the SSISDB database for the **Server name** field.</span></span>
    4. <span data-ttu-id="b6028-156">Select **SSISDB** for **Database name**.</span><span class="sxs-lookup"><span data-stu-id="b6028-156">Select **SSISDB** for **Database name**.</span></span>
    5. <span data-ttu-id="b6028-157">For **User name**, enter the name of user who has access to the database.</span><span class="sxs-lookup"><span data-stu-id="b6028-157">For **User name**, enter the name of user who has access to the database.</span></span>
    6. <span data-ttu-id="b6028-158">For **Password**, enter the password of the user.</span><span class="sxs-lookup"><span data-stu-id="b6028-158">For **Password**, enter the password of the user.</span></span> 
    7. <span data-ttu-id="b6028-159">Test the connection to the database by clicking **Test connection** button.</span><span class="sxs-lookup"><span data-stu-id="b6028-159">Test the connection to the database by clicking **Test connection** button.</span></span>
    8. <span data-ttu-id="b6028-160">Save the linked service by clicking the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b6028-160">Save the linked service by clicking the **Save** button.</span></span> 

        ![Azure SQL Database linked service](./media/how-to-invoke-ssis-package-stored-procedure-activity/azure-sql-database-linked-service-settings.png)
5. <span data-ttu-id="b6028-162">In the properties window, switch to the **Stored Procedure** tab from the **SQL Account** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b6028-162">In the properties window, switch to the **Stored Procedure** tab from the **SQL Account** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="b6028-163">Select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="b6028-163">Select **Edit**.</span></span> 
    2. <span data-ttu-id="b6028-164">For the **Stored procedure name** field, Enter `sp_executesql`.</span><span class="sxs-lookup"><span data-stu-id="b6028-164">For the **Stored procedure name** field, Enter `sp_executesql`.</span></span> 
    3. <span data-ttu-id="b6028-165">Click **+ New** in the **Stored procedure parameters** section.</span><span class="sxs-lookup"><span data-stu-id="b6028-165">Click **+ New** in the **Stored procedure parameters** section.</span></span> 
    4. <span data-ttu-id="b6028-166">For **name** of the parameter, enter **stmt**.</span><span class="sxs-lookup"><span data-stu-id="b6028-166">For **name** of the parameter, enter **stmt**.</span></span> 
    5. <span data-ttu-id="b6028-167">For **type** of the parameter, enter **String**.</span><span class="sxs-lookup"><span data-stu-id="b6028-167">For **type** of the parameter, enter **String**.</span></span> 
    6. <span data-ttu-id="b6028-168">For **value** of the parameter, enter the following SQL query:</span><span class="sxs-lookup"><span data-stu-id="b6028-168">For **value** of the parameter, enter the following SQL query:</span></span>

        <span data-ttu-id="b6028-169">In the SQL query, specify the right values for the **folder_name**, **project_name**, and **package_name** parameters.</span><span class="sxs-lookup"><span data-stu-id="b6028-169">In the SQL query, specify the right values for the **folder_name**, **project_name**, and **package_name** parameters.</span></span> 

        ```sql
        DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'<FOLDER name in SSIS Catalog>', @project_name=N'<PROJECT name in SSIS Catalog>', @package_name=N'<PACKAGE name>.dtsx', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END
        ```

        ![Azure SQL Database linked service](./media/how-to-invoke-ssis-package-stored-procedure-activity/stored-procedure-settings.png)
6. <span data-ttu-id="b6028-171">To validate the pipeline configuration, click **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="b6028-171">To validate the pipeline configuration, click **Validate** on the toolbar.</span></span> <span data-ttu-id="b6028-172">To close the **Pipeline Validation Report**, click **>>**.</span><span class="sxs-lookup"><span data-stu-id="b6028-172">To close the **Pipeline Validation Report**, click **>>**.</span></span>

    ![Validate pipeline](./media/how-to-invoke-ssis-package-stored-procedure-activity/validate-pipeline.png)
7. <span data-ttu-id="b6028-174">Publish the pipeline to Data Factory by clicking **Publish All** button.</span><span class="sxs-lookup"><span data-stu-id="b6028-174">Publish the pipeline to Data Factory by clicking **Publish All** button.</span></span> 

    ![Publish](./media/how-to-invoke-ssis-package-stored-procedure-activity/publish-all-button.png)    

### <a name="run-and-monitor-the-pipeline"></a><span data-ttu-id="b6028-176">Run and monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="b6028-176">Run and monitor the pipeline</span></span>
<span data-ttu-id="b6028-177">In this section, you trigger a pipeline run and then monitor it.</span><span class="sxs-lookup"><span data-stu-id="b6028-177">In this section, you trigger a pipeline run and then monitor it.</span></span> 

1. <span data-ttu-id="b6028-178">To trigger a pipeline run, click **Trigger** on the toolbar, and click **Trigger now**.</span><span class="sxs-lookup"><span data-stu-id="b6028-178">To trigger a pipeline run, click **Trigger** on the toolbar, and click **Trigger now**.</span></span> 

    ![Trigger now](media/how-to-invoke-ssis-package-stored-procedure-activity/trigger-now.png)

2. <span data-ttu-id="b6028-180">In the **Pipeline Run** window, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b6028-180">In the **Pipeline Run** window, select **Finish**.</span></span> 
3. <span data-ttu-id="b6028-181">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="b6028-181">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="b6028-182">You see the pipeline run and its status along with other information (such as Run Start time).</span><span class="sxs-lookup"><span data-stu-id="b6028-182">You see the pipeline run and its status along with other information (such as Run Start time).</span></span> <span data-ttu-id="b6028-183">To refresh the view, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="b6028-183">To refresh the view, click **Refresh**.</span></span>

    ![Pipeline runs](./media/how-to-invoke-ssis-package-stored-procedure-activity/pipeline-runs.png)

3. <span data-ttu-id="b6028-185">Click **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="b6028-185">Click **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="b6028-186">You see only one activity run as the pipeline has only one activity (stored procedure activity).</span><span class="sxs-lookup"><span data-stu-id="b6028-186">You see only one activity run as the pipeline has only one activity (stored procedure activity).</span></span>

    ![Activity runs](./media/how-to-invoke-ssis-package-stored-procedure-activity/activity-runs.png)

4. <span data-ttu-id="b6028-188">You can run the following **query** against the SSISDB database in your Azure SQL server to verify that the package executed.</span><span class="sxs-lookup"><span data-stu-id="b6028-188">You can run the following **query** against the SSISDB database in your Azure SQL server to verify that the package executed.</span></span> 

    ```sql
    select * from catalog.executions
    ```

    ![Verify package executions](./media/how-to-invoke-ssis-package-stored-procedure-activity/verify-package-executions.png)


> [!NOTE]
> <span data-ttu-id="b6028-190">You can also create a scheduled trigger for your pipeline so that the pipeline runs on a schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="b6028-190">You can also create a scheduled trigger for your pipeline so that the pipeline runs on a schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="b6028-191">For an example, see [Create a data factory - Data Factory UI](quickstart-create-data-factory-portal.md#trigger-the-pipeline-on-a-schedule).</span><span class="sxs-lookup"><span data-stu-id="b6028-191">For an example, see [Create a data factory - Data Factory UI](quickstart-create-data-factory-portal.md#trigger-the-pipeline-on-a-schedule).</span></span>

## <a name="azure-powershell"></a><span data-ttu-id="b6028-192">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6028-192">Azure PowerShell</span></span>
<span data-ttu-id="b6028-193">In this section, you use Azure PowerShell to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="b6028-193">In this section, you use Azure PowerShell to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span></span> 

<span data-ttu-id="b6028-194">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b6028-194">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span> 

### <a name="create-a-data-factory"></a><span data-ttu-id="b6028-195">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="b6028-195">Create a data factory</span></span>
<span data-ttu-id="b6028-196">You can either use the same data factory that has the Azure-SSIS IR or create a separate data factory.</span><span class="sxs-lookup"><span data-stu-id="b6028-196">You can either use the same data factory that has the Azure-SSIS IR or create a separate data factory.</span></span> <span data-ttu-id="b6028-197">The following procedure provides steps to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="b6028-197">The following procedure provides steps to create a data factory.</span></span> <span data-ttu-id="b6028-198">You create a pipeline with a stored procedure activity in this data factory.</span><span class="sxs-lookup"><span data-stu-id="b6028-198">You create a pipeline with a stored procedure activity in this data factory.</span></span> <span data-ttu-id="b6028-199">The stored procedure activity executes a stored procedure in the SSISDB database to run your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="b6028-199">The stored procedure activity executes a stored procedure in the SSISDB database to run your SSIS package.</span></span> 

1. <span data-ttu-id="b6028-200">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="b6028-200">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="b6028-201">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="b6028-201">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span></span> <span data-ttu-id="b6028-202">For example: `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="b6028-202">For example: `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    <span data-ttu-id="b6028-203">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="b6028-203">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="b6028-204">Assign a different value to the `$ResourceGroupName` variable and run the command again</span><span class="sxs-lookup"><span data-stu-id="b6028-204">Assign a different value to the `$ResourceGroupName` variable and run the command again</span></span>
2. <span data-ttu-id="b6028-205">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b6028-205">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    $ResGrp = New-AzureRmResourceGroup $resourceGroupName -location 'eastus'
    ``` 
    <span data-ttu-id="b6028-206">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="b6028-206">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="b6028-207">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span><span class="sxs-lookup"><span data-stu-id="b6028-207">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span></span> 
3. <span data-ttu-id="b6028-208">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="b6028-208">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  <span data-ttu-id="b6028-209">Update the data factory name to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="b6028-209">Update the data factory name to be globally unique.</span></span> 

    ```powershell
    $DataFactoryName = "ADFTutorialFactory";
    ```

5. <span data-ttu-id="b6028-210">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span><span class="sxs-lookup"><span data-stu-id="b6028-210">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span></span> 
    
    ```powershell       
    $DataFactory = Set-AzureRmDataFactoryV2 -ResourceGroupName $ResGrp.ResourceGroupName -Location $ResGrp.Location -Name $dataFactoryName 
    ```

<span data-ttu-id="b6028-211">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="b6028-211">Note the following points:</span></span>

* <span data-ttu-id="b6028-212">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="b6028-212">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="b6028-213">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="b6028-213">If you receive the following error, change the name and try again.</span></span>

    ```
    The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
    ```
* <span data-ttu-id="b6028-214">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b6028-214">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span></span>
* <span data-ttu-id="b6028-215">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="b6028-215">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="b6028-216">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="b6028-216">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

### <a name="create-an-azure-sql-database-linked-service"></a><span data-ttu-id="b6028-217">Create an Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="b6028-217">Create an Azure SQL Database linked service</span></span>
<span data-ttu-id="b6028-218">Create a linked service to link your Azure SQL database that hosts the SSIS catalog to your data factory.</span><span class="sxs-lookup"><span data-stu-id="b6028-218">Create a linked service to link your Azure SQL database that hosts the SSIS catalog to your data factory.</span></span> <span data-ttu-id="b6028-219">Data Factory uses information in this linked service to connect to SSISDB database, and executes a stored procedure to run an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="b6028-219">Data Factory uses information in this linked service to connect to SSISDB database, and executes a stored procedure to run an SSIS package.</span></span> 

1. <span data-ttu-id="b6028-220">Create a JSON file named **AzureSqlDatabaseLinkedService.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="b6028-220">Create a JSON file named **AzureSqlDatabaseLinkedService.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="b6028-221">Replace &lt;servername&gt;, &lt;username&gt;, and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span><span class="sxs-lookup"><span data-stu-id="b6028-221">Replace &lt;servername&gt;, &lt;username&gt;, and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span></span>

    ```json
    {
        "name": "AzureSqlDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=SSISDB;User ID=<username>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="b6028-222">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span><span class="sxs-lookup"><span data-stu-id="b6028-222">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span></span>

3. <span data-ttu-id="b6028-223">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureSqlDatabaseLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b6028-223">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureSqlDatabaseLinkedService**.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -Name "AzureSqlDatabaseLinkedService" -File ".\AzureSqlDatabaseLinkedService.json"
    ```

### <a name="create-a-pipeline-with-stored-procedure-activity"></a><span data-ttu-id="b6028-224">Create a pipeline with stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="b6028-224">Create a pipeline with stored procedure activity</span></span> 
<span data-ttu-id="b6028-225">In this step, you create a pipeline with a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="b6028-225">In this step, you create a pipeline with a stored procedure activity.</span></span> <span data-ttu-id="b6028-226">The activity invokes the sp_executesql stored procedure to run your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="b6028-226">The activity invokes the sp_executesql stored procedure to run your SSIS package.</span></span> 

1. <span data-ttu-id="b6028-227">Create a JSON file named **RunSSISPackagePipeline.json** in the **C:\ADF\RunSSISPackage** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="b6028-227">Create a JSON file named **RunSSISPackagePipeline.json** in the **C:\ADF\RunSSISPackage** folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b6028-228">Replace &lt;FOLDER NAME&gt;, &lt;PROJECT NAME&gt;, &lt;PACKAGE NAME&gt; with names of folder, project, and package in the SSIS catalog before saving the file.</span><span class="sxs-lookup"><span data-stu-id="b6028-228">Replace &lt;FOLDER NAME&gt;, &lt;PROJECT NAME&gt;, &lt;PACKAGE NAME&gt; with names of folder, project, and package in the SSIS catalog before saving the file.</span></span> 

    ```json
    {
        "name": "RunSSISPackagePipeline",
        "properties": {
            "activities": [
                {
                    "name": "My SProc Activity",
                    "description":"Runs an SSIS package",
                    "type": "SqlServerStoredProcedure",
                    "linkedServiceName": {
                        "referenceName": "AzureSqlDatabaseLinkedService",
                        "type": "LinkedServiceReference"
                    },
                    "typeProperties": {
                        "storedProcedureName": "sp_executesql",
                        "storedProcedureParameters": {
                            "stmt": {
                                "value": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'<FOLDER NAME>', @project_name=N'<PROJECT NAME>', @package_name=N'<PACKAGE NAME>', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                            }
                        }
                    }
                }
            ]
        }
    }
    ```

2. <span data-ttu-id="b6028-229">To create the pipeline: **RunSSISPackagePipeline**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6028-229">To create the pipeline: **RunSSISPackagePipeline**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span>

    ```powershell
    $DFPipeLine = Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -Name "RunSSISPackagePipeline" -DefinitionFile ".\RunSSISPackagePipeline.json"
    ```

    <span data-ttu-id="b6028-230">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b6028-230">Here is the sample output:</span></span>

    ```
    PipelineName      : Adfv2QuickStartPipeline
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {CopyFromBlobToBlob}
    Parameters        : {[inputPath, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification], [outputPath, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
    ```

### <a name="create-a-pipeline-run"></a><span data-ttu-id="b6028-231">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="b6028-231">Create a pipeline run</span></span>
<span data-ttu-id="b6028-232">Use the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="b6028-232">Use the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet to run the pipeline.</span></span> <span data-ttu-id="b6028-233">The cmdlet returns the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="b6028-233">The cmdlet returns the pipeline run ID for future monitoring.</span></span>

```powershell
$RunId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -PipelineName $DFPipeLine.Name
```

### <a name="monitor-the-pipeline-run"></a><span data-ttu-id="b6028-234">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="b6028-234">Monitor the pipeline run</span></span>

<span data-ttu-id="b6028-235">Run the following PowerShell script to continuously check the pipeline run status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="b6028-235">Run the following PowerShell script to continuously check the pipeline run status until it finishes copying the data.</span></span> <span data-ttu-id="b6028-236">Copy/paste the following script in the PowerShell window, and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="b6028-236">Copy/paste the following script in the PowerShell window, and press ENTER.</span></span> 

```powershell
while ($True) {
    $Run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $ResGrp.ResourceGroupName -DataFactoryName $DataFactory.DataFactoryName -PipelineRunId $RunId

    if ($Run) {
        if ($run.Status -ne 'InProgress') {
            Write-Output ("Pipeline run finished. The status is: " +  $Run.Status)
            $Run
            break
        }
        Write-Output  "Pipeline is running...status: InProgress"
    }

    Start-Sleep -Seconds 10
}   
```

### <a name="create-a-trigger"></a><span data-ttu-id="b6028-237">Create a trigger</span><span class="sxs-lookup"><span data-stu-id="b6028-237">Create a trigger</span></span>
<span data-ttu-id="b6028-238">In the previous step, you invoked the pipeline on-demand.</span><span class="sxs-lookup"><span data-stu-id="b6028-238">In the previous step, you invoked the pipeline on-demand.</span></span> <span data-ttu-id="b6028-239">You can also create a schedule trigger to run the pipeline on a schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="b6028-239">You can also create a schedule trigger to run the pipeline on a schedule (hourly, daily, etc.).</span></span>

1. <span data-ttu-id="b6028-240">Create a JSON file named **MyTrigger.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="b6028-240">Create a JSON file named **MyTrigger.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span></span> 

    ```json
    {
        "properties": {
            "name": "MyTrigger",
            "type": "ScheduleTrigger",
            "typeProperties": {
                "recurrence": {
                    "frequency": "Hour",
                    "interval": 1,
                    "startTime": "2017-12-07T00:00:00-08:00",
                    "endTime": "2017-12-08T00:00:00-08:00"
                }
            },
            "pipelines": [{
                    "pipelineReference": {
                        "type": "PipelineReference",
                        "referenceName": "RunSSISPackagePipeline"
                    },
                    "parameters": {}
                }
            ]
        }
    }    
    ```
2. <span data-ttu-id="b6028-241">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span><span class="sxs-lookup"><span data-stu-id="b6028-241">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span></span>
3. <span data-ttu-id="b6028-242">Run the **Set-AzureRmDataFactoryV2Trigger** cmdlet, which creates the trigger.</span><span class="sxs-lookup"><span data-stu-id="b6028-242">Run the **Set-AzureRmDataFactoryV2Trigger** cmdlet, which creates the trigger.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResGrp.ResourceGroupName -DataFactoryName $DataFactory.DataFactoryName -Name "MyTrigger" -DefinitionFile ".\MyTrigger.json"
    ```
4. <span data-ttu-id="b6028-243">By default, the trigger is in stopped state.</span><span class="sxs-lookup"><span data-stu-id="b6028-243">By default, the trigger is in stopped state.</span></span> <span data-ttu-id="b6028-244">Start the trigger by running the **Start-AzureRmDataFactoryV2Trigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6028-244">Start the trigger by running the **Start-AzureRmDataFactoryV2Trigger** cmdlet.</span></span> 

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResGrp.ResourceGroupName -DataFactoryName $DataFactory.DataFactoryName -Name "MyTrigger" 
    ```
5. <span data-ttu-id="b6028-245">Confirm that the trigger is started by running the **Get-AzureRmDataFactoryV2Trigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6028-245">Confirm that the trigger is started by running the **Get-AzureRmDataFactoryV2Trigger** cmdlet.</span></span> 

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"     
    ```    
6. <span data-ttu-id="b6028-246">Run the following command after the next hour.</span><span class="sxs-lookup"><span data-stu-id="b6028-246">Run the following command after the next hour.</span></span> <span data-ttu-id="b6028-247">For example, if the current time is 3:25 PM UTC, run the command at 4 PM UTC.</span><span class="sxs-lookup"><span data-stu-id="b6028-247">For example, if the current time is 3:25 PM UTC, run the command at 4 PM UTC.</span></span> 
    
    ```powershell
    Get-AzureRmDataFactoryV2TriggerRun -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -TriggerName "MyTrigger" -TriggerRunStartedAfter "2017-12-06" -TriggerRunStartedBefore "2017-12-09"
    ```

    <span data-ttu-id="b6028-248">You can run the following query against the SSISDB database in your Azure SQL server to verify that the package executed.</span><span class="sxs-lookup"><span data-stu-id="b6028-248">You can run the following query against the SSISDB database in your Azure SQL server to verify that the package executed.</span></span> 

    ```sql
    select * from catalog.executions
    ```


## <a name="next-steps"></a><span data-ttu-id="b6028-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6028-249">Next steps</span></span>
<span data-ttu-id="b6028-250">You can also monitor the pipeline using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b6028-250">You can also monitor the pipeline using the Azure portal.</span></span> <span data-ttu-id="b6028-251">For step-by-step instructions, see [Monitor the pipeline](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b6028-251">For step-by-step instructions, see [Monitor the pipeline](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span></span>
