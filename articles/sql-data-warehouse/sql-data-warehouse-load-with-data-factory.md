---
title: Load data into Azure SQL Data Warehouse – Data Factory | Microsoft Docs
description: This tutorial loads data into Azure SQL Data Warehouse by using Azure Data Factory, and uses a SQL Server database as the data source.
services: sql-data-warehouse
documentationcenter: NA
author: linda33wj
manager: jhubbard
editor: ''
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: jingwang;kevin;barbkess
ms.openlocfilehash: 33ed3ccbb33d108f33b4824e73e3ea9d5a692cf1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661366"
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="5c610-103">Load data into SQL Data Warehouse with Data Factory</span><span class="sxs-lookup"><span data-stu-id="5c610-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="5c610-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="5c610-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="5c610-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5c610-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="5c610-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="5c610-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="5c610-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span><span class="sxs-lookup"><span data-stu-id="5c610-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c610-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5c610-108">Prerequisites</span></span>

- <span data-ttu-id="5c610-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="5c610-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="5c610-110">You need an online **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="5c610-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="5c610-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="5c610-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="5c610-112">You need an **Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="5c610-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="5c610-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5c610-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/storage-create-storage-account.md).</span></span> <span data-ttu-id="5c610-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="5c610-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="5c610-115">Configure a data factory</span><span class="sxs-lookup"><span data-stu-id="5c610-115">Configure a data factory</span></span>
1. <span data-ttu-id="5c610-116">Log in to the [Azure portal][].</span><span class="sxs-lookup"><span data-stu-id="5c610-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="5c610-117">Locate your data warehouse and click to open it.</span><span class="sxs-lookup"><span data-stu-id="5c610-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="5c610-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="5c610-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Launch Load Data wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="5c610-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span><span class="sxs-lookup"><span data-stu-id="5c610-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="5c610-121">Fill in the requested information, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c610-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="5c610-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5c610-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="5c610-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5c610-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="5c610-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span><span class="sxs-lookup"><span data-stu-id="5c610-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![Configure Data Factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="5c610-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span><span class="sxs-lookup"><span data-stu-id="5c610-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="5c610-127">Click **Next** to start creating a data loading task.</span><span class="sxs-lookup"><span data-stu-id="5c610-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="5c610-128">Configure the data factory properties</span><span class="sxs-lookup"><span data-stu-id="5c610-128">Configure the data factory properties</span></span>
<span data-ttu-id="5c610-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span><span class="sxs-lookup"><span data-stu-id="5c610-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="5c610-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="5c610-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="5c610-131">Use the default **Run once now** option, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![Configure load schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="5c610-133">Configure the source data store and gateway</span><span class="sxs-lookup"><span data-stu-id="5c610-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="5c610-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span><span class="sxs-lookup"><span data-stu-id="5c610-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="5c610-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![Choose SQL Server source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="5c610-137">A **Specify the on-premises SQL Server database** dialog appears.</span><span class="sxs-lookup"><span data-stu-id="5c610-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="5c610-138">The first  **Connection name** field is auto filled in.</span><span class="sxs-lookup"><span data-stu-id="5c610-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="5c610-139">The second field asks for the name of the **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="5c610-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="5c610-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="5c610-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="5c610-141">Click the **Create Gateway** link to create a Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="5c610-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5c610-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span><span class="sxs-lookup"><span data-stu-id="5c610-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="5c610-143">A gateway has a 1-1 relationship with a data factory.</span><span class="sxs-lookup"><span data-stu-id="5c610-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="5c610-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span><span class="sxs-lookup"><span data-stu-id="5c610-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="5c610-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span><span class="sxs-lookup"><span data-stu-id="5c610-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="5c610-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span><span class="sxs-lookup"><span data-stu-id="5c610-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="5c610-147">A **Create Gateway** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="5c610-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="5c610-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c610-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="5c610-149">A **Configure Gateway** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="5c610-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="5c610-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span><span class="sxs-lookup"><span data-stu-id="5c610-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="5c610-151">The progress is shown in a pop-up window.</span><span class="sxs-lookup"><span data-stu-id="5c610-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="5c610-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span><span class="sxs-lookup"><span data-stu-id="5c610-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="5c610-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5c610-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="5c610-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span><span class="sxs-lookup"><span data-stu-id="5c610-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![Launch Express setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="5c610-156">Wait for the gateway setup to complete.</span><span class="sxs-lookup"><span data-stu-id="5c610-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="5c610-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span><span class="sxs-lookup"><span data-stu-id="5c610-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="5c610-158">Then fill in the rest required fields as follows, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="5c610-159">**Server name**: Name of the on-premises SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5c610-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="5c610-160">**Database name**: SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="5c610-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="5c610-161">**Credential encryption**: Use the default "By web browser".</span><span class="sxs-lookup"><span data-stu-id="5c610-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="5c610-162">**Authentication type**: Choose the type of authentication you are using.</span><span class="sxs-lookup"><span data-stu-id="5c610-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="5c610-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span><span class="sxs-lookup"><span data-stu-id="5c610-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![Launch Express setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="5c610-165">The next step is to choose the tables from which to copy the data.</span><span class="sxs-lookup"><span data-stu-id="5c610-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="5c610-166">You can filter the tables by using keywords.</span><span class="sxs-lookup"><span data-stu-id="5c610-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="5c610-167">And you can preview the data and table schema in the bottom panel.</span><span class="sxs-lookup"><span data-stu-id="5c610-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="5c610-168">After you finish your selection, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-168">After you finish your selection, click **Next**.</span></span>

    ![Select tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="5c610-170">Configure the destination, your SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5c610-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="5c610-171">Now you tell Data Factory about the destination information.</span><span class="sxs-lookup"><span data-stu-id="5c610-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="5c610-172">Your SQL Data Warehouse connection information is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="5c610-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="5c610-173">Enter the password for the user name.</span><span class="sxs-lookup"><span data-stu-id="5c610-173">Enter the password for the user name.</span></span> <span data-ttu-id="5c610-174">and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-174">and click **Next**.</span></span>

    ![Configure destination](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="5c610-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span><span class="sxs-lookup"><span data-stu-id="5c610-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="5c610-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span><span class="sxs-lookup"><span data-stu-id="5c610-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="5c610-178">You can also choose to map to an existing table.</span><span class="sxs-lookup"><span data-stu-id="5c610-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="5c610-179">Review and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-179">Review and click **Next**.</span></span>

    ![Map tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="5c610-181">Review the schema mapping and look for error or warning messages.</span><span class="sxs-lookup"><span data-stu-id="5c610-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="5c610-182">Intelligent mapping is based on column name.</span><span class="sxs-lookup"><span data-stu-id="5c610-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="5c610-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span><span class="sxs-lookup"><span data-stu-id="5c610-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="5c610-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span><span class="sxs-lookup"><span data-stu-id="5c610-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![Map schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="5c610-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="5c610-187">Configure the performance settings</span><span class="sxs-lookup"><span data-stu-id="5c610-187">Configure the performance settings</span></span>
<span data-ttu-id="5c610-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="5c610-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="5c610-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span><span class="sxs-lookup"><span data-stu-id="5c610-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="5c610-190">Select an existing Azure Storage account, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c610-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configure staging blob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="5c610-192">Review summary information and deploy the pipeline</span><span class="sxs-lookup"><span data-stu-id="5c610-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="5c610-193">Review the configuration and click **Finish** button to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="5c610-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![Deploy data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="5c610-195">Monitor data loading progress</span><span class="sxs-lookup"><span data-stu-id="5c610-195">Monitor data loading progress</span></span>

<span data-ttu-id="5c610-196">You can see the deployment progress and results in the **Deployment** page.</span><span class="sxs-lookup"><span data-stu-id="5c610-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="5c610-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span><span class="sxs-lookup"><span data-stu-id="5c610-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![Monitor pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="5c610-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5c610-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![View pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="5c610-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span><span class="sxs-lookup"><span data-stu-id="5c610-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![View table activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="5c610-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span><span class="sxs-lookup"><span data-stu-id="5c610-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![View table activity details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="5c610-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span><span class="sxs-lookup"><span data-stu-id="5c610-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c610-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c610-206">Next steps</span></span>

<span data-ttu-id="5c610-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="5c610-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="5c610-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="5c610-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="5c610-209">Introduction to Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5c610-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="5c610-210">Move data by using Copy Activity</span><span class="sxs-lookup"><span data-stu-id="5c610-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="5c610-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5c610-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="5c610-212">To explore your data in SQL Data Warehouse, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="5c610-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="5c610-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span><span class="sxs-lookup"><span data-stu-id="5c610-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="5c610-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="5c610-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure portal]: https://portal.azure.com
















