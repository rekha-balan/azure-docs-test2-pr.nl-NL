---
title: Use Redgate to load data to your Azure data warehouse | Microsoft Docs
description: Learn how to use Redgate's Data Platform Studio for data warehousing scenarios.
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: ''
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.openlocfilehash: 9b88890c2b3bcbfddc7dd864b16fbdadcf02b57e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552532"
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="35347-103">Load data with Redgate Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="35347-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="35347-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premise SQL Server to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="35347-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premise SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="35347-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="35347-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> [Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools. This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="35347-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="35347-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="35347-113">Create or identify resources</span><span class="sxs-lookup"><span data-stu-id="35347-113">Create or identify resources</span></span>
<span data-ttu-id="35347-114">Before starting this tutorial, you need to have:</span><span class="sxs-lookup"><span data-stu-id="35347-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="35347-115">**On-premise SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premise SQL Server (version 2008R2 or above).</span><span class="sxs-lookup"><span data-stu-id="35347-115">**On-premise SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premise SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="35347-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span><span class="sxs-lookup"><span data-stu-id="35347-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="35347-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="35347-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="35347-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span><span class="sxs-lookup"><span data-stu-id="35347-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="35347-119">If you don't have a storage account, learn how to Create a storage account.</span><span class="sxs-lookup"><span data-stu-id="35347-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="35347-120">**SQL Data Warehouse**: This tutorial moves the data from on-premise SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span><span class="sxs-lookup"><span data-stu-id="35347-120">**SQL Data Warehouse**: This tutorial moves the data from on-premise SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="35347-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="35347-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> Performance is improved if the storage account and the data warehouse are created in the same region.
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="35347-123">Step 1: Sign in to Data Platform Studio with your Azure account</span><span class="sxs-lookup"><span data-stu-id="35347-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="35347-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span><span class="sxs-lookup"><span data-stu-id="35347-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="35347-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span><span class="sxs-lookup"><span data-stu-id="35347-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="35347-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span><span class="sxs-lookup"><span data-stu-id="35347-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="35347-128">Step 2: Start the Import Wizard</span><span class="sxs-lookup"><span data-stu-id="35347-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="35347-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span><span class="sxs-lookup"><span data-stu-id="35347-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="35347-130">Step 3: Install the Data Platform Studio Gateway</span><span class="sxs-lookup"><span data-stu-id="35347-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="35347-131">To connect to your on-premise SQL Server database, you need to install the DPS Gateway.</span><span class="sxs-lookup"><span data-stu-id="35347-131">To connect to your on-premise SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="35347-132">The gateway is a client agent that provides access to your on-premise environment, extracts the data, and uploads it to your storage account.</span><span class="sxs-lookup"><span data-stu-id="35347-132">The gateway is a client agent that provides access to your on-premise environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="35347-133">Your data never passes through Redgate’s servers.</span><span class="sxs-lookup"><span data-stu-id="35347-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="35347-134">To install the Gateway:</span><span class="sxs-lookup"><span data-stu-id="35347-134">To install the Gateway:</span></span>

1. <span data-ttu-id="35347-135">Click the **Create Gateway** link</span><span class="sxs-lookup"><span data-stu-id="35347-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="35347-136">Download and install the Gateway using the provided installer</span><span class="sxs-lookup"><span data-stu-id="35347-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> The Gateway can be installed on any machine with network access to the source SQL Server database. It accesses the SQL Server database using Windows authentication with the credentials of the current user.
> 
> 

<span data-ttu-id="35347-139">Once installed, the Gateway status changes to Connected and you can select Next.</span><span class="sxs-lookup"><span data-stu-id="35347-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="35347-140">Step 4: Identify the source database</span><span class="sxs-lookup"><span data-stu-id="35347-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="35347-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="35347-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="35347-142">Then, from the drop-down menu, select the database you want to import data from.</span><span class="sxs-lookup"><span data-stu-id="35347-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="35347-143">DPS inspects the selected database for tables to import.</span><span class="sxs-lookup"><span data-stu-id="35347-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="35347-144">By default, DPS imports all the tables in the database.</span><span class="sxs-lookup"><span data-stu-id="35347-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="35347-145">You can select or deselect tables by expanding the All Tables link.</span><span class="sxs-lookup"><span data-stu-id="35347-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="35347-146">Select the Next button to move forward.</span><span class="sxs-lookup"><span data-stu-id="35347-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="35347-147">Step 5: Choose a storage account to stage the data</span><span class="sxs-lookup"><span data-stu-id="35347-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="35347-148">DPS prompts you for a location to stage the data.</span><span class="sxs-lookup"><span data-stu-id="35347-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="35347-149">Choose an existing storage account from your subscription and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="35347-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="35347-151">Step 6: Select a data warehouse</span><span class="sxs-lookup"><span data-stu-id="35347-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="35347-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span><span class="sxs-lookup"><span data-stu-id="35347-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="35347-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="35347-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> DPS merges the source data tables into the data warehouse. DPS warns you if the table name requires it to overwrite existing tables in the data warehouse. You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="35347-157">Step 7: Import the data</span><span class="sxs-lookup"><span data-stu-id="35347-157">Step 7: Import the data</span></span>
<span data-ttu-id="35347-158">DPS confirms that you would like to import the data.</span><span class="sxs-lookup"><span data-stu-id="35347-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="35347-159">Simply click the Start import button to begin the data import.</span><span class="sxs-lookup"><span data-stu-id="35347-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="35347-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premise SQL Server and the progress of the import into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="35347-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premise SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="35347-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span><span class="sxs-lookup"><span data-stu-id="35347-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="35347-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="35347-162">Next steps</span></span>
<span data-ttu-id="35347-163">To explore your data within SQL Data Warehouse, start by viewing:</span><span class="sxs-lookup"><span data-stu-id="35347-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="35347-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="35347-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="35347-165">[Visualize data with Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="35347-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="35347-166">To learn more about Redgate’s Data Platform Studio:</span><span class="sxs-lookup"><span data-stu-id="35347-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="35347-167">Visit the DPS homepage</span><span class="sxs-lookup"><span data-stu-id="35347-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="35347-168">Watch a demo of DPS on Channel9</span><span class="sxs-lookup"><span data-stu-id="35347-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="35347-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span><span class="sxs-lookup"><span data-stu-id="35347-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="35347-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="35347-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="35347-171">Load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35347-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="35347-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="35347-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md








