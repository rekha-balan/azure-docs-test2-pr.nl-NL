---
title: Copy data in bulk using Azure Data Factory | Microsoft Docs
description: Learn how to use Azure Data Factory and Copy Activity to copy data from a source data store to a destination data store in bulk.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 06/22/2018
ms.author: jingwang
ms.openlocfilehash: e7c134881cbf8745a4e4ef9102a418f7d47a6f8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856709"
---
# <a name="copy-multiple-tables-in-bulk-by-using-azure-data-factory"></a><span data-ttu-id="afdff-103">Copy multiple tables in bulk by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="afdff-103">Copy multiple tables in bulk by using Azure Data Factory</span></span>
<span data-ttu-id="afdff-104">This tutorial demonstrates **copying a number of tables from Azure SQL Database to Azure SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="afdff-104">This tutorial demonstrates **copying a number of tables from Azure SQL Database to Azure SQL Data Warehouse**.</span></span> <span data-ttu-id="afdff-105">You can apply the same pattern in other copy scenarios as well.</span><span class="sxs-lookup"><span data-stu-id="afdff-105">You can apply the same pattern in other copy scenarios as well.</span></span> <span data-ttu-id="afdff-106">For example, copying tables from SQL Server/Oracle to Azure SQL Database/Data Warehouse/Azure Blob, copying different paths from Blob to Azure SQL Database tables.</span><span class="sxs-lookup"><span data-stu-id="afdff-106">For example, copying tables from SQL Server/Oracle to Azure SQL Database/Data Warehouse/Azure Blob, copying different paths from Blob to Azure SQL Database tables.</span></span>

> [!NOTE]
> - <span data-ttu-id="afdff-107">If you are new to Azure Data Factory, see [Introduction to Azure Data Factory](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="afdff-107">If you are new to Azure Data Factory, see [Introduction to Azure Data Factory](introduction.md).</span></span>

<span data-ttu-id="afdff-108">At a high level, this tutorial involves following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-108">At a high level, this tutorial involves following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afdff-109">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-109">Create a data factory.</span></span>
> * <span data-ttu-id="afdff-110">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="afdff-110">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span></span>
> * <span data-ttu-id="afdff-111">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span><span class="sxs-lookup"><span data-stu-id="afdff-111">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span></span>
> * <span data-ttu-id="afdff-112">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span><span class="sxs-lookup"><span data-stu-id="afdff-112">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span></span> 
> * <span data-ttu-id="afdff-113">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="afdff-113">Start a pipeline run.</span></span>
> * <span data-ttu-id="afdff-114">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="afdff-114">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="afdff-115">This tutorial uses Azure portal.</span><span class="sxs-lookup"><span data-stu-id="afdff-115">This tutorial uses Azure portal.</span></span> <span data-ttu-id="afdff-116">To learn about using other tools/SDKs to create a data factory, see [Quickstarts](quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="afdff-116">To learn about using other tools/SDKs to create a data factory, see [Quickstarts](quickstart-create-data-factory-dot-net.md).</span></span> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="afdff-117">End-to-end workflow</span><span class="sxs-lookup"><span data-stu-id="afdff-117">End-to-end workflow</span></span>
<span data-ttu-id="afdff-118">In this scenario, you have a number of tables in Azure SQL Database that you want to copy to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="afdff-118">In this scenario, you have a number of tables in Azure SQL Database that you want to copy to SQL Data Warehouse.</span></span> <span data-ttu-id="afdff-119">Here is the logical sequence of steps in the workflow that happens in pipelines:</span><span class="sxs-lookup"><span data-stu-id="afdff-119">Here is the logical sequence of steps in the workflow that happens in pipelines:</span></span>

![Workflow](media/tutorial-bulk-copy-portal/tutorial-copy-multiple-tables.png)

* <span data-ttu-id="afdff-121">The first pipeline looks up the list of tables that needs to be copied over to the sink data stores.</span><span class="sxs-lookup"><span data-stu-id="afdff-121">The first pipeline looks up the list of tables that needs to be copied over to the sink data stores.</span></span>  <span data-ttu-id="afdff-122">Alternatively you can maintain a metadata table that lists all the tables to be copied to the sink data store.</span><span class="sxs-lookup"><span data-stu-id="afdff-122">Alternatively you can maintain a metadata table that lists all the tables to be copied to the sink data store.</span></span> <span data-ttu-id="afdff-123">Then, the pipeline triggers another pipeline, which iterates over each table in the database and performs the data copy operation.</span><span class="sxs-lookup"><span data-stu-id="afdff-123">Then, the pipeline triggers another pipeline, which iterates over each table in the database and performs the data copy operation.</span></span>
* <span data-ttu-id="afdff-124">The second pipeline performs the actual copy.</span><span class="sxs-lookup"><span data-stu-id="afdff-124">The second pipeline performs the actual copy.</span></span> <span data-ttu-id="afdff-125">It takes the list of tables as a parameter.</span><span class="sxs-lookup"><span data-stu-id="afdff-125">It takes the list of tables as a parameter.</span></span> <span data-ttu-id="afdff-126">For each table in the list, copy the specific table in Azure SQL Database to the corresponding table in SQL Data Warehouse using [staged copy via Blob storage and PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) for best performance.</span><span class="sxs-lookup"><span data-stu-id="afdff-126">For each table in the list, copy the specific table in Azure SQL Database to the corresponding table in SQL Data Warehouse using [staged copy via Blob storage and PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) for best performance.</span></span> <span data-ttu-id="afdff-127">In this example, the first pipeline passes the list of tables as a value for the parameter.</span><span class="sxs-lookup"><span data-stu-id="afdff-127">In this example, the first pipeline passes the list of tables as a value for the parameter.</span></span> 

<span data-ttu-id="afdff-128">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="afdff-128">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afdff-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="afdff-129">Prerequisites</span></span>
* <span data-ttu-id="afdff-130">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="afdff-130">**Azure Storage account**.</span></span> <span data-ttu-id="afdff-131">The Azure Storage account is used as staging blob storage in the bulk copy operation.</span><span class="sxs-lookup"><span data-stu-id="afdff-131">The Azure Storage account is used as staging blob storage in the bulk copy operation.</span></span> 
* <span data-ttu-id="afdff-132">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="afdff-132">**Azure SQL Database**.</span></span> <span data-ttu-id="afdff-133">This database contains the source data.</span><span class="sxs-lookup"><span data-stu-id="afdff-133">This database contains the source data.</span></span> 
* <span data-ttu-id="afdff-134">**Azure SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="afdff-134">**Azure SQL Data Warehouse**.</span></span> <span data-ttu-id="afdff-135">This data warehouse holds the data copied over from the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="afdff-135">This data warehouse holds the data copied over from the SQL Database.</span></span> 

### <a name="prepare-sql-database-and-sql-data-warehouse"></a><span data-ttu-id="afdff-136">Prepare SQL Database and SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="afdff-136">Prepare SQL Database and SQL Data Warehouse</span></span>

<span data-ttu-id="afdff-137">**Prepare the source Azure SQL Database**:</span><span class="sxs-lookup"><span data-stu-id="afdff-137">**Prepare the source Azure SQL Database**:</span></span>

<span data-ttu-id="afdff-138">Create an Azure SQL Database with Adventure Works LT sample data following [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="afdff-138">Create an Azure SQL Database with Adventure Works LT sample data following [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article.</span></span> <span data-ttu-id="afdff-139">This tutorial copies all the tables from this sample database to a SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="afdff-139">This tutorial copies all the tables from this sample database to a SQL data warehouse.</span></span>

<span data-ttu-id="afdff-140">**Prepare the sink Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="afdff-140">**Prepare the sink Azure SQL Data Warehouse**:</span></span>

1. <span data-ttu-id="afdff-141">If you don't have an Azure SQL Data Warehouse, see the [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="afdff-141">If you don't have an Azure SQL Data Warehouse, see the [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md) article for steps to create one.</span></span>

1. <span data-ttu-id="afdff-142">Create corresponding table schemas in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="afdff-142">Create corresponding table schemas in SQL Data Warehouse.</span></span> <span data-ttu-id="afdff-143">You can use [Migration Utility](https://www.microsoft.com/download/details.aspx?id=49100) to **migrate schema** from Azure SQL Database to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="afdff-143">You can use [Migration Utility](https://www.microsoft.com/download/details.aspx?id=49100) to **migrate schema** from Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="afdff-144">You use Azure Data Factory to migrate/copy data in a later step.</span><span class="sxs-lookup"><span data-stu-id="afdff-144">You use Azure Data Factory to migrate/copy data in a later step.</span></span>

## <a name="azure-services-to-access-sql-server"></a><span data-ttu-id="afdff-145">Azure services to access SQL server</span><span class="sxs-lookup"><span data-stu-id="afdff-145">Azure services to access SQL server</span></span>

<span data-ttu-id="afdff-146">For both SQL Database and SQL Data Warehouse, allow Azure services to access SQL server.</span><span class="sxs-lookup"><span data-stu-id="afdff-146">For both SQL Database and SQL Data Warehouse, allow Azure services to access SQL server.</span></span> <span data-ttu-id="afdff-147">Ensure that **Allow access to Azure services** setting is turned **ON** for your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="afdff-147">Ensure that **Allow access to Azure services** setting is turned **ON** for your Azure SQL server.</span></span> <span data-ttu-id="afdff-148">This setting allows the Data Factory service to read data from your Azure SQL Database and write data to your Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="afdff-148">This setting allows the Data Factory service to read data from your Azure SQL Database and write data to your Azure SQL Data Warehouse.</span></span> <span data-ttu-id="afdff-149">To verify and turn on this setting, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-149">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="afdff-150">Click **More services** hub on the left and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="afdff-150">Click **More services** hub on the left and click **SQL servers**.</span></span>
1. <span data-ttu-id="afdff-151">Select your server, and click **Firewall** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="afdff-151">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
1. <span data-ttu-id="afdff-152">In the **Firewall settings** page, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="afdff-152">In the **Firewall settings** page, click **ON** for **Allow access to Azure services**.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="afdff-153">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="afdff-153">Create a data factory</span></span>
1. <span data-ttu-id="afdff-154">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="afdff-154">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="afdff-155">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="afdff-155">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="afdff-156">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="afdff-156">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-bulk-copy-portal/new-azure-data-factory-menu.png)
1. <span data-ttu-id="afdff-158">In the **New data factory** page, enter **ADFTutorialBulkCopyDF** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-158">In the **New data factory** page, enter **ADFTutorialBulkCopyDF** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-bulk-copy-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="afdff-160">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="afdff-160">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="afdff-161">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialBulkCopyDF).</span><span class="sxs-lookup"><span data-stu-id="afdff-161">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialBulkCopyDF).</span></span> <span data-ttu-id="afdff-162">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="afdff-162">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name “ADFTutorialBulkCopyDF” is not available`
1. <span data-ttu-id="afdff-163">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-163">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="afdff-164">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-164">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="afdff-165">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="afdff-165">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="afdff-166">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="afdff-166">Select **Create new**, and enter the name of a resource group.</span></span>   
         
      <span data-ttu-id="afdff-167">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afdff-167">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
1. <span data-ttu-id="afdff-168">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="afdff-168">Select **V2** for the **version**.</span></span>
1. <span data-ttu-id="afdff-169">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-169">Select the **location** for the data factory.</span></span> <span data-ttu-id="afdff-170">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="afdff-170">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="afdff-171">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="afdff-171">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>
1. <span data-ttu-id="afdff-172">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="afdff-172">Select **Pin to dashboard**.</span></span>     
1. <span data-ttu-id="afdff-173">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="afdff-173">Click **Create**.</span></span>
1. <span data-ttu-id="afdff-174">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="afdff-174">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media//tutorial-bulk-copy-portal/deploying-data-factory.png)
1. <span data-ttu-id="afdff-176">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="afdff-176">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
    ![Data factory home page](./media/tutorial-bulk-copy-portal/data-factory-home-page.png)
1. <span data-ttu-id="afdff-178">Click **Author & Monitor** tile to launch the Data Factory UI application in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="afdff-178">Click **Author & Monitor** tile to launch the Data Factory UI application in a separate tab.</span></span>
1. <span data-ttu-id="afdff-179">In the **get started** page, switch to the **Edit** tab in the left panel as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="afdff-179">In the **get started** page, switch to the **Edit** tab in the left panel as shown in the following image:</span></span>  

    ![Get started page](./media/tutorial-bulk-copy-portal/get-started-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="afdff-181">Create linked services</span><span class="sxs-lookup"><span data-stu-id="afdff-181">Create linked services</span></span>
<span data-ttu-id="afdff-182">You create linked services to link your data stores and computes to a data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-182">You create linked services to link your data stores and computes to a data factory.</span></span> <span data-ttu-id="afdff-183">A linked service has the connection information that the Data Factory service uses to connect to the data store at runtime.</span><span class="sxs-lookup"><span data-stu-id="afdff-183">A linked service has the connection information that the Data Factory service uses to connect to the data store at runtime.</span></span> 

<span data-ttu-id="afdff-184">In this tutorial, you link your Azure SQL Database, Azure SQL Data Warehouse, and Azure Blob Storage data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-184">In this tutorial, you link your Azure SQL Database, Azure SQL Data Warehouse, and Azure Blob Storage data stores to your data factory.</span></span> <span data-ttu-id="afdff-185">The Azure SQL Database is the source data store.</span><span class="sxs-lookup"><span data-stu-id="afdff-185">The Azure SQL Database is the source data store.</span></span> <span data-ttu-id="afdff-186">The Azure SQL Data Warehouse is the sink/destination data store.</span><span class="sxs-lookup"><span data-stu-id="afdff-186">The Azure SQL Data Warehouse is the sink/destination data store.</span></span> <span data-ttu-id="afdff-187">The Azure Blob Storage is to stage the data before the data is loaded into SQL Data Warehouse by using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="afdff-187">The Azure Blob Storage is to stage the data before the data is loaded into SQL Data Warehouse by using PolyBase.</span></span> 

### <a name="create-the-source-azure-sql-database-linked-service"></a><span data-ttu-id="afdff-188">Create the source Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="afdff-188">Create the source Azure SQL Database linked service</span></span>
<span data-ttu-id="afdff-189">In this step, you create a linked service to link your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-189">In this step, you create a linked service to link your Azure SQL database to the data factory.</span></span> 

1. <span data-ttu-id="afdff-190">Click **Connections** at the bottom of the window, and click **+ New** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="afdff-190">Click **Connections** at the bottom of the window, and click **+ New** on the toolbar.</span></span> 

    ![New linked service button](./media/tutorial-bulk-copy-portal/new-linked-service-button.png)
1. <span data-ttu-id="afdff-192">In the **New Linked Service** window, select **Azure SQL Database**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="afdff-192">In the **New Linked Service** window, select **Azure SQL Database**, and click **Continue**.</span></span> 

    ![Select Azure SQL Database](./media/tutorial-bulk-copy-portal/select-azure-sql-database.png)
1. <span data-ttu-id="afdff-194">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-194">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-195">Enter **AzureSqlDatabaseLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-195">Enter **AzureSqlDatabaseLinkedService** for **Name**.</span></span> 
    1. <span data-ttu-id="afdff-196">Select your Azure SQL server for **Server name**</span><span class="sxs-lookup"><span data-stu-id="afdff-196">Select your Azure SQL server for **Server name**</span></span>
    1. <span data-ttu-id="afdff-197">Select your Azure SQL database for **Database name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-197">Select your Azure SQL database for **Database name**.</span></span> 
    1. <span data-ttu-id="afdff-198">Enter **name of the user** to connect to Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="afdff-198">Enter **name of the user** to connect to Azure SQL database.</span></span> 
    1. <span data-ttu-id="afdff-199">Enter **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="afdff-199">Enter **password** for the user.</span></span> 
    1. <span data-ttu-id="afdff-200">To test the connection to Azure SQL database using the specified information, click **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="afdff-200">To test the connection to Azure SQL database using the specified information, click **Test connection**.</span></span>
    1. <span data-ttu-id="afdff-201">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="afdff-201">Click **Save**.</span></span>

        ![Azure SQL Database settings](./media/tutorial-bulk-copy-portal/azure-sql-database-settings.png)

### <a name="create-the-sink-azure-sql-data-warehouse-linked-service"></a><span data-ttu-id="afdff-203">Create the sink Azure SQL Data Warehouse linked service</span><span class="sxs-lookup"><span data-stu-id="afdff-203">Create the sink Azure SQL Data Warehouse linked service</span></span>

1. <span data-ttu-id="afdff-204">In the **Connections** tab, click **+ New** on the toolbar again.</span><span class="sxs-lookup"><span data-stu-id="afdff-204">In the **Connections** tab, click **+ New** on the toolbar again.</span></span> 
1. <span data-ttu-id="afdff-205">In the **New Linked Service** window, select **Azure SQL Data Warehouse**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="afdff-205">In the **New Linked Service** window, select **Azure SQL Data Warehouse**, and click **Continue**.</span></span> 
1. <span data-ttu-id="afdff-206">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-206">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-207">Enter **AzureSqlDWLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-207">Enter **AzureSqlDWLinkedService** for **Name**.</span></span> 
    1. <span data-ttu-id="afdff-208">Select your Azure SQL server for **Server name**</span><span class="sxs-lookup"><span data-stu-id="afdff-208">Select your Azure SQL server for **Server name**</span></span>
    1. <span data-ttu-id="afdff-209">Select your Azure SQL database for **Database name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-209">Select your Azure SQL database for **Database name**.</span></span> 
    1. <span data-ttu-id="afdff-210">Enter **name of the user** to connect to Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="afdff-210">Enter **name of the user** to connect to Azure SQL database.</span></span> 
    1. <span data-ttu-id="afdff-211">Enter **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="afdff-211">Enter **password** for the user.</span></span> 
    1. <span data-ttu-id="afdff-212">To test the connection to Azure SQL database using the specified information, click **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="afdff-212">To test the connection to Azure SQL database using the specified information, click **Test connection**.</span></span>
    1. <span data-ttu-id="afdff-213">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="afdff-213">Click **Save**.</span></span>

### <a name="create-the-staging-azure-storage-linked-service"></a><span data-ttu-id="afdff-214">Create the staging Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="afdff-214">Create the staging Azure Storage linked service</span></span>
<span data-ttu-id="afdff-215">In this tutorial, you use Azure Blob storage as an interim staging area to enable PolyBase for a better copy performance.</span><span class="sxs-lookup"><span data-stu-id="afdff-215">In this tutorial, you use Azure Blob storage as an interim staging area to enable PolyBase for a better copy performance.</span></span>

1. <span data-ttu-id="afdff-216">In the **Connections** tab, click **+ New** on the toolbar again.</span><span class="sxs-lookup"><span data-stu-id="afdff-216">In the **Connections** tab, click **+ New** on the toolbar again.</span></span> 
1. <span data-ttu-id="afdff-217">In the **New Linked Service** window, select **Azure Blob Storage**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="afdff-217">In the **New Linked Service** window, select **Azure Blob Storage**, and click **Continue**.</span></span> 
1. <span data-ttu-id="afdff-218">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-218">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-219">Enter **AzureStorageLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-219">Enter **AzureStorageLinkedService** for **Name**.</span></span> 
    1. <span data-ttu-id="afdff-220">Select your **Azure Storage account** for **Storage account name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-220">Select your **Azure Storage account** for **Storage account name**.</span></span>
    1. <span data-ttu-id="afdff-221">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="afdff-221">Click **Save**.</span></span>


## <a name="create-datasets"></a><span data-ttu-id="afdff-222">Create datasets</span><span class="sxs-lookup"><span data-stu-id="afdff-222">Create datasets</span></span>
<span data-ttu-id="afdff-223">In this tutorial, you create source and sink datasets, which specify the location where the data is stored.</span><span class="sxs-lookup"><span data-stu-id="afdff-223">In this tutorial, you create source and sink datasets, which specify the location where the data is stored.</span></span> 

<span data-ttu-id="afdff-224">The input dataset **AzureSqlDatabaseDataset** refers to the **AzureSqlDatabaseLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="afdff-224">The input dataset **AzureSqlDatabaseDataset** refers to the **AzureSqlDatabaseLinkedService**.</span></span> <span data-ttu-id="afdff-225">The linked service specifies the connection string to connect to the database.</span><span class="sxs-lookup"><span data-stu-id="afdff-225">The linked service specifies the connection string to connect to the database.</span></span> <span data-ttu-id="afdff-226">The dataset specifies the name of the database and the table that contains the source data.</span><span class="sxs-lookup"><span data-stu-id="afdff-226">The dataset specifies the name of the database and the table that contains the source data.</span></span> 

<span data-ttu-id="afdff-227">The output dataset **AzureSqlDWDataset** refers to the **AzureSqlDWLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="afdff-227">The output dataset **AzureSqlDWDataset** refers to the **AzureSqlDWLinkedService**.</span></span> <span data-ttu-id="afdff-228">The linked service specifies the connection string to connect to the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="afdff-228">The linked service specifies the connection string to connect to the data warehouse.</span></span> <span data-ttu-id="afdff-229">The dataset specifies the database and the table to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="afdff-229">The dataset specifies the database and the table to which the data is copied.</span></span> 

<span data-ttu-id="afdff-230">In this tutorial, the source and destination SQL tables are not hard-coded in the dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="afdff-230">In this tutorial, the source and destination SQL tables are not hard-coded in the dataset definitions.</span></span> <span data-ttu-id="afdff-231">Instead, the ForEach activity passes the name of the table at runtime to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="afdff-231">Instead, the ForEach activity passes the name of the table at runtime to the Copy activity.</span></span> 

### <a name="create-a-dataset-for-source-sql-database"></a><span data-ttu-id="afdff-232">Create a dataset for source SQL Database</span><span class="sxs-lookup"><span data-stu-id="afdff-232">Create a dataset for source SQL Database</span></span>

1. <span data-ttu-id="afdff-233">Click **+ (plus)** in the left pane, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="afdff-233">Click **+ (plus)** in the left pane, and click **Dataset**.</span></span> 

    ![New dataset menu](./media/tutorial-bulk-copy-portal/new-dataset-menu.png)
1. <span data-ttu-id="afdff-235">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-235">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span></span> <span data-ttu-id="afdff-236">You should see a new tab titled **AzureSqlTable1**.</span><span class="sxs-lookup"><span data-stu-id="afdff-236">You should see a new tab titled **AzureSqlTable1**.</span></span> 
    
    ![Select Azure SQL Database](./media/tutorial-bulk-copy-portal/select-azure-sql-database-dataset.png)
1. <span data-ttu-id="afdff-238">In the properties window at the bottom, enter **AzureSqlDatabaseDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-238">In the properties window at the bottom, enter **AzureSqlDatabaseDataset** for **Name**.</span></span>

1. <span data-ttu-id="afdff-239">Switch to the **Connection** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-239">Switch to the **Connection** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-240">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="afdff-240">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span>
    1. <span data-ttu-id="afdff-241">Select any table for **Table**.</span><span class="sxs-lookup"><span data-stu-id="afdff-241">Select any table for **Table**.</span></span> <span data-ttu-id="afdff-242">This table is a dummy table.</span><span class="sxs-lookup"><span data-stu-id="afdff-242">This table is a dummy table.</span></span> <span data-ttu-id="afdff-243">You specify a query on the source dataset when creating a pipeline.</span><span class="sxs-lookup"><span data-stu-id="afdff-243">You specify a query on the source dataset when creating a pipeline.</span></span> <span data-ttu-id="afdff-244">The query is used to extract data from the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="afdff-244">The query is used to extract data from the Azure SQL database.</span></span> <span data-ttu-id="afdff-245">Alternatively, you can click **Edit** check box, and enter **dummyName** as the table name.</span><span class="sxs-lookup"><span data-stu-id="afdff-245">Alternatively, you can click **Edit** check box, and enter **dummyName** as the table name.</span></span> 

    ![Source dataset connection page](./media/tutorial-bulk-copy-portal/source-dataset-connection-page.png)
 

### <a name="create-a-dataset-for-sink-sql-data-warehouse"></a><span data-ttu-id="afdff-247">Create a dataset for sink SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="afdff-247">Create a dataset for sink SQL Data Warehouse</span></span>

1. <span data-ttu-id="afdff-248">Click **+ (plus)** in the left pane, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="afdff-248">Click **+ (plus)** in the left pane, and click **Dataset**.</span></span> 
1. <span data-ttu-id="afdff-249">In the **New Dataset** window, select **Azure SQL Data Warehouse**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-249">In the **New Dataset** window, select **Azure SQL Data Warehouse**, and click **Finish**.</span></span> <span data-ttu-id="afdff-250">You should see a new tab titled **AzureSqlDWTable1**.</span><span class="sxs-lookup"><span data-stu-id="afdff-250">You should see a new tab titled **AzureSqlDWTable1**.</span></span> 
1. <span data-ttu-id="afdff-251">In the properties window at the bottom, enter **AzureSqlDWDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-251">In the properties window at the bottom, enter **AzureSqlDWDataset** for **Name**.</span></span>
1. <span data-ttu-id="afdff-252">Switch to the **Parameters** tab, click **+ New**, and enter **DWTableName** for the parameter name.</span><span class="sxs-lookup"><span data-stu-id="afdff-252">Switch to the **Parameters** tab, click **+ New**, and enter **DWTableName** for the parameter name.</span></span> <span data-ttu-id="afdff-253">If you copy/paste this name from the page, ensure that there is no **trailing space character** at the end of **DWTableName**.</span><span class="sxs-lookup"><span data-stu-id="afdff-253">If you copy/paste this name from the page, ensure that there is no **trailing space character** at the end of **DWTableName**.</span></span> 

    ![Source dataset connection page](./media/tutorial-bulk-copy-portal/sink-dataset-new-parameter.png)

1. <span data-ttu-id="afdff-255">Switch to the **Connection** tab,</span><span class="sxs-lookup"><span data-stu-id="afdff-255">Switch to the **Connection** tab,</span></span> 

    <span data-ttu-id="afdff-256">a.</span><span class="sxs-lookup"><span data-stu-id="afdff-256">a.</span></span> <span data-ttu-id="afdff-257">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="afdff-257">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span>

    <span data-ttu-id="afdff-258">b.</span><span class="sxs-lookup"><span data-stu-id="afdff-258">b.</span></span> <span data-ttu-id="afdff-259">For **Table**, check the **Edit** option, click into the table name input box, then click the **Add dynamic content** link below.</span><span class="sxs-lookup"><span data-stu-id="afdff-259">For **Table**, check the **Edit** option, click into the table name input box, then click the **Add dynamic content** link below.</span></span> 
    
    ![Parameter name](./media/tutorial-bulk-copy-portal/table-name-parameter.png)

    <span data-ttu-id="afdff-261">c.</span><span class="sxs-lookup"><span data-stu-id="afdff-261">c.</span></span> <span data-ttu-id="afdff-262">In the **Add Dynamic Content** page, click the **DWTAbleName** under **Parameters** which will automatically populate the top expression text box `@dataset().DWTableName`, then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-262">In the **Add Dynamic Content** page, click the **DWTAbleName** under **Parameters** which will automatically populate the top expression text box `@dataset().DWTableName`, then click **Finish**.</span></span> <span data-ttu-id="afdff-263">The **tableName** property of the dataset is set to the value that's passed as an argument for the **DWTableName** parameter.</span><span class="sxs-lookup"><span data-stu-id="afdff-263">The **tableName** property of the dataset is set to the value that's passed as an argument for the **DWTableName** parameter.</span></span> <span data-ttu-id="afdff-264">The ForEach activity iterates through a list of tables, and passes one by one to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="afdff-264">The ForEach activity iterates through a list of tables, and passes one by one to the Copy activity.</span></span> 

    ![Dataset parameter builder](./media/tutorial-bulk-copy-portal/dataset-parameter-builder.png)

## <a name="create-pipelines"></a><span data-ttu-id="afdff-266">Create pipelines</span><span class="sxs-lookup"><span data-stu-id="afdff-266">Create pipelines</span></span>
<span data-ttu-id="afdff-267">In this tutorial, you create two pipelines: **IterateAndCopySQLTables** and **GetTableListAndTriggerCopyData**.</span><span class="sxs-lookup"><span data-stu-id="afdff-267">In this tutorial, you create two pipelines: **IterateAndCopySQLTables** and **GetTableListAndTriggerCopyData**.</span></span> 

<span data-ttu-id="afdff-268">The **GetTableListAndTriggerCopyData** pipeline performs two steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-268">The **GetTableListAndTriggerCopyData** pipeline performs two steps:</span></span>

* <span data-ttu-id="afdff-269">Looks up the Azure SQL Database system table to get the list of tables to be copied.</span><span class="sxs-lookup"><span data-stu-id="afdff-269">Looks up the Azure SQL Database system table to get the list of tables to be copied.</span></span>
* <span data-ttu-id="afdff-270">Triggers the pipeline **IterateAndCopySQLTables** to do the actual data copy.</span><span class="sxs-lookup"><span data-stu-id="afdff-270">Triggers the pipeline **IterateAndCopySQLTables** to do the actual data copy.</span></span>

<span data-ttu-id="afdff-271">The  **GetTableListAndTriggerCopyData** takes a list of tables as a parameter.</span><span class="sxs-lookup"><span data-stu-id="afdff-271">The  **GetTableListAndTriggerCopyData** takes a list of tables as a parameter.</span></span> <span data-ttu-id="afdff-272">For each table in the list, it copies data from the table in Azure SQL Database to Azure SQL Data Warehouse using staged copy and PolyBase.</span><span class="sxs-lookup"><span data-stu-id="afdff-272">For each table in the list, it copies data from the table in Azure SQL Database to Azure SQL Data Warehouse using staged copy and PolyBase.</span></span>

### <a name="create-the-pipeline-iterateandcopysqltables"></a><span data-ttu-id="afdff-273">Create the pipeline IterateAndCopySQLTables</span><span class="sxs-lookup"><span data-stu-id="afdff-273">Create the pipeline IterateAndCopySQLTables</span></span>

1. <span data-ttu-id="afdff-274">In the left pane, click **+ (plus)**, and click **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="afdff-274">In the left pane, click **+ (plus)**, and click **Pipeline**.</span></span>

    ![New pipeline menu](./media/tutorial-bulk-copy-portal/new-pipeline-menu.png)
1. <span data-ttu-id="afdff-276">In the **General** tab, specify **IterateAndCopySQLTables** for name.</span><span class="sxs-lookup"><span data-stu-id="afdff-276">In the **General** tab, specify **IterateAndCopySQLTables** for name.</span></span> 

1. <span data-ttu-id="afdff-277">Switch to the **Parameters** tab, and do the following actions:</span><span class="sxs-lookup"><span data-stu-id="afdff-277">Switch to the **Parameters** tab, and do the following actions:</span></span> 

    1. <span data-ttu-id="afdff-278">Click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="afdff-278">Click **+ New**.</span></span> 
    1. <span data-ttu-id="afdff-279">Enter **tableList** for the parameter **name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-279">Enter **tableList** for the parameter **name**.</span></span>
    1. <span data-ttu-id="afdff-280">Select **Array** for **Type**.</span><span class="sxs-lookup"><span data-stu-id="afdff-280">Select **Array** for **Type**.</span></span>

        ![Pipeline parameter](./media/tutorial-bulk-copy-portal/first-pipeline-parameter.png)
1. <span data-ttu-id="afdff-282">In the **Activities** toolbox, expand **Iteration & Conditions**, and drag-drop the **ForEach** activity to the pipeline design surface.</span><span class="sxs-lookup"><span data-stu-id="afdff-282">In the **Activities** toolbox, expand **Iteration & Conditions**, and drag-drop the **ForEach** activity to the pipeline design surface.</span></span> <span data-ttu-id="afdff-283">You can also search for activities in the **Activities** toolbox.</span><span class="sxs-lookup"><span data-stu-id="afdff-283">You can also search for activities in the **Activities** toolbox.</span></span> 

    <span data-ttu-id="afdff-284">a.</span><span class="sxs-lookup"><span data-stu-id="afdff-284">a.</span></span> <span data-ttu-id="afdff-285">In the **General** tab at the bottom, enter **IterateSQLTables** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-285">In the **General** tab at the bottom, enter **IterateSQLTables** for **Name**.</span></span> 

    <span data-ttu-id="afdff-286">b.</span><span class="sxs-lookup"><span data-stu-id="afdff-286">b.</span></span> <span data-ttu-id="afdff-287">Switch to the **Settings** tab, click the inputbox for **Items**, then click the **Add dynamic content** link below.</span><span class="sxs-lookup"><span data-stu-id="afdff-287">Switch to the **Settings** tab, click the inputbox for **Items**, then click the **Add dynamic content** link below.</span></span> 

    ![ForEach activity settings](./media/tutorial-bulk-copy-portal/for-each-activity-settings.png)

    <span data-ttu-id="afdff-289">c.</span><span class="sxs-lookup"><span data-stu-id="afdff-289">c.</span></span> <span data-ttu-id="afdff-290">In the **Add Dynamic Content** page, collapse the System Vairables and Functions section, click the **tableList** under **Parameters** which will automatically populate the top expression text box as `@pipeline().parameter.tableList`, then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-290">In the **Add Dynamic Content** page, collapse the System Vairables and Functions section, click the **tableList** under **Parameters** which will automatically populate the top expression text box as `@pipeline().parameter.tableList`, then click **Finish**.</span></span> 

    ![Foreach parameter builder](./media/tutorial-bulk-copy-portal/for-each-parameter-builder.png)
    
    <span data-ttu-id="afdff-292">d.</span><span class="sxs-lookup"><span data-stu-id="afdff-292">d.</span></span> <span data-ttu-id="afdff-293">Switch to **Activities** tab, click **Add activity** to add a child activity to the **ForEach** activity.</span><span class="sxs-lookup"><span data-stu-id="afdff-293">Switch to **Activities** tab, click **Add activity** to add a child activity to the **ForEach** activity.</span></span>

1. <span data-ttu-id="afdff-294">In the **Activities** toolbox, expand **DataFlow**, and drag-drop **Copy** activity into the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="afdff-294">In the **Activities** toolbox, expand **DataFlow**, and drag-drop **Copy** activity into the pipeline designer surface.</span></span> <span data-ttu-id="afdff-295">Notice the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="afdff-295">Notice the breadcrumb menu at the top.</span></span> <span data-ttu-id="afdff-296">The IterateAndCopySQLTable is the pipeline name and IterateSQLTables is the ForEach activity name.</span><span class="sxs-lookup"><span data-stu-id="afdff-296">The IterateAndCopySQLTable is the pipeline name and IterateSQLTables is the ForEach activity name.</span></span> <span data-ttu-id="afdff-297">The designer is in the activity scope.</span><span class="sxs-lookup"><span data-stu-id="afdff-297">The designer is in the activity scope.</span></span> <span data-ttu-id="afdff-298">To switch back to the pipeline editor from the ForEach editor, click the link in the breadcrumb menu.</span><span class="sxs-lookup"><span data-stu-id="afdff-298">To switch back to the pipeline editor from the ForEach editor, click the link in the breadcrumb menu.</span></span> 

    ![Copy in ForEach](./media/tutorial-bulk-copy-portal/copy-in-for-each.png)
1. <span data-ttu-id="afdff-300">Switch to the **Source** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-300">Switch to the **Source** tab, and do the following steps:</span></span>

    1. <span data-ttu-id="afdff-301">Select **AzureSqlDatabaseDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="afdff-301">Select **AzureSqlDatabaseDataset** for **Source Dataset**.</span></span> 
    1. <span data-ttu-id="afdff-302">Select **Query** option for **User Query**.</span><span class="sxs-lookup"><span data-stu-id="afdff-302">Select **Query** option for **User Query**.</span></span> 
    1. <span data-ttu-id="afdff-303">Click the **Query** input box -> select the **Add dynamic content** below -> enter the following expression for **Query** -> select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-303">Click the **Query** input box -> select the **Add dynamic content** below -> enter the following expression for **Query** -> select **Finish**.</span></span>

        ```sql
        SELECT * FROM [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]
        ``` 

        ![Copy source settings](./media/tutorial-bulk-copy-portal/copy-source-settings.png)
1. <span data-ttu-id="afdff-305">Switch to the **Sink** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-305">Switch to the **Sink** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-306">Select **AzureSqlDWDataset** for **Sink Dataset**.</span><span class="sxs-lookup"><span data-stu-id="afdff-306">Select **AzureSqlDWDataset** for **Sink Dataset**.</span></span>
    1. <span data-ttu-id="afdff-307">Click input box for the VALUE of DWTableName parameter -> select the **Add dynamic content** below, enter `[@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]` expression as script, -> select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-307">Click input box for the VALUE of DWTableName parameter -> select the **Add dynamic content** below, enter `[@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]` expression as script, -> select **Finish**.</span></span>
    1. <span data-ttu-id="afdff-308">Expand **Polybase Settings**, and select **Allow polybase**.</span><span class="sxs-lookup"><span data-stu-id="afdff-308">Expand **Polybase Settings**, and select **Allow polybase**.</span></span> 
    1. <span data-ttu-id="afdff-309">Clear the **Use Type default** option.</span><span class="sxs-lookup"><span data-stu-id="afdff-309">Clear the **Use Type default** option.</span></span> 
    1. <span data-ttu-id="afdff-310">Click the **Pre-copy Script** input box -> select the **Add dynamic content** below -> enter the following expression as script -> select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-310">Click the **Pre-copy Script** input box -> select the **Add dynamic content** below -> enter the following expression as script -> select **Finish**.</span></span> 

        ```sql
        TRUNCATE TABLE [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]
        ```

        ![Copy sink settings](./media/tutorial-bulk-copy-portal/copy-sink-settings.png)

1. <span data-ttu-id="afdff-312">Switch to the **Settings** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-312">Switch to the **Settings** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-313">Select **True** for **Enable Staging**.</span><span class="sxs-lookup"><span data-stu-id="afdff-313">Select **True** for **Enable Staging**.</span></span>
    1. <span data-ttu-id="afdff-314">Select **AzureStorageLinkedService** for **Store Account Linked Service**.</span><span class="sxs-lookup"><span data-stu-id="afdff-314">Select **AzureStorageLinkedService** for **Store Account Linked Service**.</span></span>

        ![Enable staging](./media/tutorial-bulk-copy-portal/copy-sink-staging-settings.png)

1. <span data-ttu-id="afdff-316">To validate the pipeline settings, click **Validate** on the top pipeline tool bar.</span><span class="sxs-lookup"><span data-stu-id="afdff-316">To validate the pipeline settings, click **Validate** on the top pipeline tool bar.</span></span> <span data-ttu-id="afdff-317">Confirm that there is no validation error.</span><span class="sxs-lookup"><span data-stu-id="afdff-317">Confirm that there is no validation error.</span></span> <span data-ttu-id="afdff-318">To close the **Pipeline Validation Report**, click **>>**.</span><span class="sxs-lookup"><span data-stu-id="afdff-318">To close the **Pipeline Validation Report**, click **>>**.</span></span>

### <a name="create-the-pipeline-gettablelistandtriggercopydata"></a><span data-ttu-id="afdff-319">Create the pipeline GetTableListAndTriggerCopyData</span><span class="sxs-lookup"><span data-stu-id="afdff-319">Create the pipeline GetTableListAndTriggerCopyData</span></span>

<span data-ttu-id="afdff-320">This pipeline performs two steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-320">This pipeline performs two steps:</span></span>

* <span data-ttu-id="afdff-321">Looks up the Azure SQL Database system table to get the list of tables to be copied.</span><span class="sxs-lookup"><span data-stu-id="afdff-321">Looks up the Azure SQL Database system table to get the list of tables to be copied.</span></span>
* <span data-ttu-id="afdff-322">Triggers the pipeline "IterateAndCopySQLTables" to do the actual data copy.</span><span class="sxs-lookup"><span data-stu-id="afdff-322">Triggers the pipeline "IterateAndCopySQLTables" to do the actual data copy.</span></span>

1. <span data-ttu-id="afdff-323">In the left pane, click **+ (plus)**, and click **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="afdff-323">In the left pane, click **+ (plus)**, and click **Pipeline**.</span></span>

    ![New pipeline menu](./media/tutorial-bulk-copy-portal/new-pipeline-menu.png)
1. <span data-ttu-id="afdff-325">In the Properties window, change the name of the pipeline to **GetTableListAndTriggerCopyData**.</span><span class="sxs-lookup"><span data-stu-id="afdff-325">In the Properties window, change the name of the pipeline to **GetTableListAndTriggerCopyData**.</span></span> 

1. <span data-ttu-id="afdff-326">In the **Activities** toolbox, expand **General**, and drag-and-drop **Lookup** activity to the pipeline designer surface, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-326">In the **Activities** toolbox, expand **General**, and drag-and-drop **Lookup** activity to the pipeline designer surface, and do the following steps:</span></span>

    1. <span data-ttu-id="afdff-327">Enter **LookupTableList** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-327">Enter **LookupTableList** for **Name**.</span></span> 
    1. <span data-ttu-id="afdff-328">Enter **Retrieve the table list from Azure SQL database** for **Description**.</span><span class="sxs-lookup"><span data-stu-id="afdff-328">Enter **Retrieve the table list from Azure SQL database** for **Description**.</span></span>

        ![Lookup activity - general page](./media/tutorial-bulk-copy-portal/lookup-general-page.png)
1. <span data-ttu-id="afdff-330">Switch to the **Settings** page, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-330">Switch to the **Settings** page, and do the following steps:</span></span>

    1. <span data-ttu-id="afdff-331">Select **AzureSqlDatabaseDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="afdff-331">Select **AzureSqlDatabaseDataset** for **Source Dataset**.</span></span> 
    1. <span data-ttu-id="afdff-332">Select **Query** for **Use Query**.</span><span class="sxs-lookup"><span data-stu-id="afdff-332">Select **Query** for **Use Query**.</span></span> 
    1. <span data-ttu-id="afdff-333">Enter the following SQL query for **Query**.</span><span class="sxs-lookup"><span data-stu-id="afdff-333">Enter the following SQL query for **Query**.</span></span>

        ```sql
        SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.TABLES WHERE TABLE_TYPE = 'BASE TABLE' and TABLE_SCHEMA = 'SalesLT' and TABLE_NAME <> 'ProductModel'
        ```
    1. <span data-ttu-id="afdff-334">Clear the checkbox for the **First row only** field.</span><span class="sxs-lookup"><span data-stu-id="afdff-334">Clear the checkbox for the **First row only** field.</span></span>

        ![Lookup activity - settings page](./media/tutorial-bulk-copy-portal/lookup-settings-page.png)
1. <span data-ttu-id="afdff-336">Drag-and-drop **Execute Pipeline** activity from the Activities toolbox to the pipeline designer surface, and set the name to **TriggerCopy**.</span><span class="sxs-lookup"><span data-stu-id="afdff-336">Drag-and-drop **Execute Pipeline** activity from the Activities toolbox to the pipeline designer surface, and set the name to **TriggerCopy**.</span></span>

    ![Execute Pipeline activity - general page](./media/tutorial-bulk-copy-portal/execute-pipeline-general-page.png)    
1. <span data-ttu-id="afdff-338">Switch to the **Settings** page, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="afdff-338">Switch to the **Settings** page, and do the following steps:</span></span> 

    1. <span data-ttu-id="afdff-339">Select **IterateAndCopySQLTables** for **Invoked pipeline**.</span><span class="sxs-lookup"><span data-stu-id="afdff-339">Select **IterateAndCopySQLTables** for **Invoked pipeline**.</span></span> 
    1. <span data-ttu-id="afdff-340">Expand the **Advanced** section.</span><span class="sxs-lookup"><span data-stu-id="afdff-340">Expand the **Advanced** section.</span></span> 
    1. <span data-ttu-id="afdff-341">Click **+ New** in the **Parameters** section.</span><span class="sxs-lookup"><span data-stu-id="afdff-341">Click **+ New** in the **Parameters** section.</span></span> 
    1. <span data-ttu-id="afdff-342">Enter **tableList** for parameter **name**.</span><span class="sxs-lookup"><span data-stu-id="afdff-342">Enter **tableList** for parameter **name**.</span></span>
    1. <span data-ttu-id="afdff-343">Click VALUE input box -> select the **Add dynamic content** below -> enter `@activity('LookupTableList').output.value` as table name value -> select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="afdff-343">Click VALUE input box -> select the **Add dynamic content** below -> enter `@activity('LookupTableList').output.value` as table name value -> select **Finish**.</span></span> <span data-ttu-id="afdff-344">You are setting the result list from the Lookup activity as an input to the second pipeline.</span><span class="sxs-lookup"><span data-stu-id="afdff-344">You are setting the result list from the Lookup activity as an input to the second pipeline.</span></span> <span data-ttu-id="afdff-345">The result list contains the list of tables whose data needs to be copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="afdff-345">The result list contains the list of tables whose data needs to be copied to the destination.</span></span> 

        ![Execute pipeline activity - settings page](./media/tutorial-bulk-copy-portal/execute-pipeline-settings-page.png)
1. <span data-ttu-id="afdff-347">**Connect** the **Lookup** activity to the **Execute Pipeline** activity by dragging the **green box** attached to the Lookup activity to the left of Execute Pipeline activity.</span><span class="sxs-lookup"><span data-stu-id="afdff-347">**Connect** the **Lookup** activity to the **Execute Pipeline** activity by dragging the **green box** attached to the Lookup activity to the left of Execute Pipeline activity.</span></span>

    ![Connect Lookup and Execute Pipeline activities](./media/tutorial-bulk-copy-portal/connect-lookup-execute-pipeline.png)
1. <span data-ttu-id="afdff-349">To validate the pipeline, click **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="afdff-349">To validate the pipeline, click **Validate** on the toolbar.</span></span> <span data-ttu-id="afdff-350">Confirm that there are no validation errors.</span><span class="sxs-lookup"><span data-stu-id="afdff-350">Confirm that there are no validation errors.</span></span> <span data-ttu-id="afdff-351">To close the **Pipeline Validation Report**, click **>>**.</span><span class="sxs-lookup"><span data-stu-id="afdff-351">To close the **Pipeline Validation Report**, click **>>**.</span></span>

1. <span data-ttu-id="afdff-352">To publish entities (datasets, pipelines, etc.) to the Data Factory service, click **Publish All** on top of the window.</span><span class="sxs-lookup"><span data-stu-id="afdff-352">To publish entities (datasets, pipelines, etc.) to the Data Factory service, click **Publish All** on top of the window.</span></span> <span data-ttu-id="afdff-353">Wait until the publishing succeeds.</span><span class="sxs-lookup"><span data-stu-id="afdff-353">Wait until the publishing succeeds.</span></span> 

## <a name="trigger-a-pipeline-run"></a><span data-ttu-id="afdff-354">Trigger a pipeline run</span><span class="sxs-lookup"><span data-stu-id="afdff-354">Trigger a pipeline run</span></span>

<span data-ttu-id="afdff-355">Go to pipeline **GetTableListAndTriggerCopyData**, click **Trigger**, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="afdff-355">Go to pipeline **GetTableListAndTriggerCopyData**, click **Trigger**, and click **Trigger Now**.</span></span> 

![Trigger now](./media/tutorial-bulk-copy-portal/trigger-now.png)

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="afdff-357">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="afdff-357">Monitor the pipeline run</span></span>

1. <span data-ttu-id="afdff-358">Switch to the **Monitor** tab. Click **Refresh** until you see runs for both the pipelines in your solution.</span><span class="sxs-lookup"><span data-stu-id="afdff-358">Switch to the **Monitor** tab. Click **Refresh** until you see runs for both the pipelines in your solution.</span></span> <span data-ttu-id="afdff-359">Continue refreshing the list until you see the **Succeeded** status.</span><span class="sxs-lookup"><span data-stu-id="afdff-359">Continue refreshing the list until you see the **Succeeded** status.</span></span> 

    ![Pipeline runs](./media/tutorial-bulk-copy-portal/pipeline-runs.png)
1. <span data-ttu-id="afdff-361">To view activity runs associated with the GetTableListAndTriggerCopyData pipeline, click the first link in the Actions link for that pipeline.</span><span class="sxs-lookup"><span data-stu-id="afdff-361">To view activity runs associated with the GetTableListAndTriggerCopyData pipeline, click the first link in the Actions link for that pipeline.</span></span> <span data-ttu-id="afdff-362">You should see two activity runs for this pipeline run.</span><span class="sxs-lookup"><span data-stu-id="afdff-362">You should see two activity runs for this pipeline run.</span></span> 

    ![Activity runs](./media/tutorial-bulk-copy-portal/activity-runs-1.png)    
1. <span data-ttu-id="afdff-364">To view the output of the **Lookup** activity, click link in the **Output** column for that activity.</span><span class="sxs-lookup"><span data-stu-id="afdff-364">To view the output of the **Lookup** activity, click link in the **Output** column for that activity.</span></span> <span data-ttu-id="afdff-365">You can maximize and restore the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="afdff-365">You can maximize and restore the **Output** window.</span></span> <span data-ttu-id="afdff-366">After reviewing, click **X** to close the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="afdff-366">After reviewing, click **X** to close the **Output** window.</span></span>

    ```json
    {
        "count": 9,
        "value": [
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "Customer"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "ProductDescription"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "Product"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "ProductModelProductDescription"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "ProductCategory"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "Address"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "CustomerAddress"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "SalesOrderDetail"
            },
            {
                "TABLE_SCHEMA": "SalesLT",
                "TABLE_NAME": "SalesOrderHeader"
            }
        ],
        "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)",
        "effectiveIntegrationRuntimes": [
            {
                "name": "DefaultIntegrationRuntime",
                "type": "Managed",
                "location": "East US",
                "billedDuration": 0,
                "nodes": null
            }
        ]
    }
    ```    
1. <span data-ttu-id="afdff-367">To switch back to the **Pipeline Runs** view, click **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="afdff-367">To switch back to the **Pipeline Runs** view, click **Pipelines** link at the top.</span></span> <span data-ttu-id="afdff-368">Click **View Activity Runs** link (first link in the **Actions** column) for the **IterateAndCopySQLTables** pipeline.</span><span class="sxs-lookup"><span data-stu-id="afdff-368">Click **View Activity Runs** link (first link in the **Actions** column) for the **IterateAndCopySQLTables** pipeline.</span></span> <span data-ttu-id="afdff-369">You should see output as shown in the following image: Notice that there is one **Copy** activity run for each table in the **Lookup** activity output.</span><span class="sxs-lookup"><span data-stu-id="afdff-369">You should see output as shown in the following image: Notice that there is one **Copy** activity run for each table in the **Lookup** activity output.</span></span> 

    ![Activity runs](./media/tutorial-bulk-copy-portal/activity-runs-2.png)
1. <span data-ttu-id="afdff-371">Confirm that the data was copied to the target SQL Data Warehouse you used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="afdff-371">Confirm that the data was copied to the target SQL Data Warehouse you used in this tutorial.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="afdff-372">Next steps</span><span class="sxs-lookup"><span data-stu-id="afdff-372">Next steps</span></span>
<span data-ttu-id="afdff-373">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="afdff-373">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="afdff-374">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="afdff-374">Create a data factory.</span></span>
> * <span data-ttu-id="afdff-375">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="afdff-375">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span></span>
> * <span data-ttu-id="afdff-376">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span><span class="sxs-lookup"><span data-stu-id="afdff-376">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span></span>
> * <span data-ttu-id="afdff-377">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span><span class="sxs-lookup"><span data-stu-id="afdff-377">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span></span> 
> * <span data-ttu-id="afdff-378">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="afdff-378">Start a pipeline run.</span></span>
> * <span data-ttu-id="afdff-379">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="afdff-379">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="afdff-380">Advance to the following tutorial to learn about copy data incrementally from a source to a destination:</span><span class="sxs-lookup"><span data-stu-id="afdff-380">Advance to the following tutorial to learn about copy data incrementally from a source to a destination:</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="afdff-381">Copy data incrementally</span><span class="sxs-lookup"><span data-stu-id="afdff-381">Copy data incrementally</span></span>](tutorial-incremental-copy-portal.md)
