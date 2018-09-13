---
title: Move data from an on-premises SQL Server to SQL Azure with Azure Data Factory | Microsoft Docs
description: Set up an ADF pipeline that composes two data migration activities that together move data on a daily basis between databases on-premises and in the cloud.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: 5e5e8c3a81d911cb47edfcb5432bc423872a29ec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866778"
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="bad76-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bad76-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="bad76-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="bad76-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="bad76-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bad76-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](move-sql-azure.md).</span></span>

## <a name="intro"></a><span data-ttu-id="bad76-106">Introduction: What is ADF and when should it be used to migrate data?</span><span class="sxs-lookup"><span data-stu-id="bad76-106">Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="bad76-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span><span class="sxs-lookup"><span data-stu-id="bad76-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="bad76-108">The key concept in the ADF model is pipeline.</span><span class="sxs-lookup"><span data-stu-id="bad76-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="bad76-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span><span class="sxs-lookup"><span data-stu-id="bad76-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="bad76-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span><span class="sxs-lookup"><span data-stu-id="bad76-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="bad76-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span><span class="sxs-lookup"><span data-stu-id="bad76-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="bad76-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span><span class="sxs-lookup"><span data-stu-id="bad76-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="bad76-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span><span class="sxs-lookup"><span data-stu-id="bad76-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="bad76-114">Consider using ADF:</span><span class="sxs-lookup"><span data-stu-id="bad76-114">Consider using ADF:</span></span>

* <span data-ttu-id="bad76-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span><span class="sxs-lookup"><span data-stu-id="bad76-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="bad76-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span><span class="sxs-lookup"><span data-stu-id="bad76-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="bad76-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span><span class="sxs-lookup"><span data-stu-id="bad76-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="bad76-118">ADF also has other capabilities such as support for complex operations.</span><span class="sxs-lookup"><span data-stu-id="bad76-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="bad76-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bad76-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <a name="scenario"></a><span data-ttu-id="bad76-120">The Scenario</span><span class="sxs-lookup"><span data-stu-id="bad76-120">The Scenario</span></span>
<span data-ttu-id="bad76-121">We set up an ADF pipeline that composes two data migration activities.</span><span class="sxs-lookup"><span data-stu-id="bad76-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="bad76-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span><span class="sxs-lookup"><span data-stu-id="bad76-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="bad76-123">The two activities are:</span><span class="sxs-lookup"><span data-stu-id="bad76-123">The two activities are:</span></span>

* <span data-ttu-id="bad76-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span><span class="sxs-lookup"><span data-stu-id="bad76-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="bad76-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bad76-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="bad76-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../../data-factory/tutorial-hybrid-copy-portal.md) References to the relevant sections of that topic are provided when appropriate.</span><span class="sxs-lookup"><span data-stu-id="bad76-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../../data-factory/tutorial-hybrid-copy-portal.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <a name="prereqs"></a><span data-ttu-id="bad76-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bad76-127">Prerequisites</span></span>
<span data-ttu-id="bad76-128">This tutorial assumes you have:</span><span class="sxs-lookup"><span data-stu-id="bad76-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="bad76-129">An **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="bad76-129">An **Azure subscription**.</span></span> <span data-ttu-id="bad76-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bad76-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bad76-131">An **Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="bad76-131">An **Azure storage account**.</span></span> <span data-ttu-id="bad76-132">You use an Azure storage account for storing the data in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bad76-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="bad76-133">If you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article.</span><span class="sxs-lookup"><span data-stu-id="bad76-133">If you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article.</span></span> <span data-ttu-id="bad76-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span><span class="sxs-lookup"><span data-stu-id="bad76-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="bad76-135">See [Manage your storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="bad76-135">See [Manage your storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="bad76-136">Access to an **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="bad76-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="bad76-137">If you must set up an Azure SQL Database, the topic [Getting Started with Microsoft Azure SQL Database ](../../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bad76-137">If you must set up an Azure SQL Database, the topic [Getting Started with Microsoft Azure SQL Database ](../../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="bad76-138">Installed and configured **Azure PowerShell** locally.</span><span class="sxs-lookup"><span data-stu-id="bad76-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="bad76-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bad76-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="bad76-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bad76-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <a name="upload-data"></a> <span data-ttu-id="bad76-141">Upload the data to your on-premises SQL Server</span><span class="sxs-lookup"><span data-stu-id="bad76-141">Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="bad76-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span><span class="sxs-lookup"><span data-stu-id="bad76-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="bad76-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="bad76-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="bad76-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="bad76-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="bad76-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="bad76-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="bad76-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span><span class="sxs-lookup"><span data-stu-id="bad76-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="bad76-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="bad76-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="bad76-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span><span class="sxs-lookup"><span data-stu-id="bad76-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <a name="create-adf"></a> <span data-ttu-id="bad76-149">Create an Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bad76-149">Create an Azure Data Factory</span></span>
<span data-ttu-id="bad76-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-data-factory).</span><span class="sxs-lookup"><span data-stu-id="bad76-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-data-factory).</span></span> <span data-ttu-id="bad76-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="bad76-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="bad76-152">Install and configure up the Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="bad76-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="bad76-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span><span class="sxs-lookup"><span data-stu-id="bad76-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="bad76-154">To create a Linked Service for an on-premises SQL Server, you must:</span><span class="sxs-lookup"><span data-stu-id="bad76-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="bad76-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="bad76-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="bad76-156">configure the linked service for the on-premises data source to use the gateway.</span><span class="sxs-lookup"><span data-stu-id="bad76-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="bad76-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span><span class="sxs-lookup"><span data-stu-id="bad76-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="bad76-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../../data-factory/tutorial-hybrid-copy-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bad76-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../../data-factory/tutorial-hybrid-copy-portal.md)</span></span>

## <a name="adflinkedservices"></a><span data-ttu-id="bad76-159">Create linked services to connect to the data resources</span><span class="sxs-lookup"><span data-stu-id="bad76-159">Create linked services to connect to the data resources</span></span>
<span data-ttu-id="bad76-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span><span class="sxs-lookup"><span data-stu-id="bad76-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="bad76-161">We have three resources in this scenario for which linked services are needed:</span><span class="sxs-lookup"><span data-stu-id="bad76-161">We have three resources in this scenario for which linked services are needed:</span></span>

1. <span data-ttu-id="bad76-162">On-premises SQL Server</span><span class="sxs-lookup"><span data-stu-id="bad76-162">On-premises SQL Server</span></span>
2. <span data-ttu-id="bad76-163">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bad76-163">Azure Blob Storage</span></span>
3. <span data-ttu-id="bad76-164">Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="bad76-164">Azure SQL database</span></span>

<span data-ttu-id="bad76-165">The step-by-step procedure for creating linked services is provided in [Create linked services](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bad76-165">The step-by-step procedure for creating linked services is provided in [Create linked services](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-pipeline).</span></span>


## <a name="adf-tables"></a><span data-ttu-id="bad76-166">Define and create tables to specify how to access the datasets</span><span class="sxs-lookup"><span data-stu-id="bad76-166">Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="bad76-167">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span><span class="sxs-lookup"><span data-stu-id="bad76-167">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="bad76-168">JSON files are used to define the tables.</span><span class="sxs-lookup"><span data-stu-id="bad76-168">JSON files are used to define the tables.</span></span> <span data-ttu-id="bad76-169">For more information on the structure of these files, see [Datasets](../../data-factory/concepts-datasets-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="bad76-169">For more information on the structure of these files, see [Datasets](../../data-factory/concepts-datasets-linked-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bad76-170">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span><span class="sxs-lookup"><span data-stu-id="bad76-170">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="bad76-171">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/servicemanagement/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="bad76-171">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/servicemanagement/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="bad76-172">The JSON-based definitions in the tables use the following names:</span><span class="sxs-lookup"><span data-stu-id="bad76-172">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="bad76-173">the **table name** in the on-premises SQL server is *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="bad76-173">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="bad76-174">the **container name** in the Azure Blob Storage account is *containername*</span><span class="sxs-lookup"><span data-stu-id="bad76-174">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="bad76-175">Three table definitions are needed for this ADF pipeline:</span><span class="sxs-lookup"><span data-stu-id="bad76-175">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="bad76-176">SQL on-premises Table</span><span class="sxs-lookup"><span data-stu-id="bad76-176">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="bad76-177">Blob Table </span><span class="sxs-lookup"><span data-stu-id="bad76-177">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="bad76-178">SQL Azure Table</span><span class="sxs-lookup"><span data-stu-id="bad76-178">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="bad76-179">These procedures use Azure PowerShell to define and create the ADF activities.</span><span class="sxs-lookup"><span data-stu-id="bad76-179">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="bad76-180">But these tasks can also be accomplished using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bad76-180">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="bad76-181">For details, see [Create datasets](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bad76-181">For details, see [Create datasets](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-pipeline).</span></span>
>
>

### <a name="adf-table-onprem-sql"></a><span data-ttu-id="bad76-182">SQL on-premises Table</span><span class="sxs-lookup"><span data-stu-id="bad76-182">SQL on-premises Table</span></span>
<span data-ttu-id="bad76-183">The table definition for the on-premises SQL Server is specified in the following JSON file:</span><span class="sxs-lookup"><span data-stu-id="bad76-183">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="bad76-184">The column names were not included here.</span><span class="sxs-lookup"><span data-stu-id="bad76-184">The column names were not included here.</span></span> <span data-ttu-id="bad76-185">You can sub-select on the column names by including them here (for details check the [ADF documentation](../../data-factory/copy-activity-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="bad76-185">You can sub-select on the column names by including them here (for details check the [ADF documentation](../../data-factory/copy-activity-overview.md) topic.</span></span>

<span data-ttu-id="bad76-186">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="bad76-186">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="bad76-187">Create the table in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bad76-187">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a><span data-ttu-id="bad76-188">Blob Table</span><span class="sxs-lookup"><span data-stu-id="bad76-188">Blob Table</span></span>
<span data-ttu-id="bad76-189">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span><span class="sxs-lookup"><span data-stu-id="bad76-189">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="bad76-190">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="bad76-190">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="bad76-191">Create the table in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bad76-191">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sql"></a><span data-ttu-id="bad76-192">SQL Azure Table</span><span class="sxs-lookup"><span data-stu-id="bad76-192">SQL Azure Table</span></span>
<span data-ttu-id="bad76-193">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span><span class="sxs-lookup"><span data-stu-id="bad76-193">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="bad76-194">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="bad76-194">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="bad76-195">Create the table in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bad76-195">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a><span data-ttu-id="bad76-196">Define and create the pipeline</span><span class="sxs-lookup"><span data-stu-id="bad76-196">Define and create the pipeline</span></span>
<span data-ttu-id="bad76-197">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span><span class="sxs-lookup"><span data-stu-id="bad76-197">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="bad76-198">A JSON file is used to define the pipeline properties.</span><span class="sxs-lookup"><span data-stu-id="bad76-198">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="bad76-199">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="bad76-199">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="bad76-200">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span><span class="sxs-lookup"><span data-stu-id="bad76-200">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="bad76-201">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span><span class="sxs-lookup"><span data-stu-id="bad76-201">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="bad76-202">But this task can also be accomplished using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bad76-202">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="bad76-203">For details, see [Create pipeline](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bad76-203">For details, see [Create pipeline](../../data-factory/tutorial-hybrid-copy-portal.md#create-a-pipeline).</span></span>
>
>

<span data-ttu-id="bad76-204">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span><span class="sxs-lookup"><span data-stu-id="bad76-204">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data to Sql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="bad76-205">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="bad76-205">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="bad76-206">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bad76-206">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json


## <a name="adf-pipeline-start"></a><span data-ttu-id="bad76-207">Start the Pipeline</span><span class="sxs-lookup"><span data-stu-id="bad76-207">Start the Pipeline</span></span>
<span data-ttu-id="bad76-208">The pipeline can now be run using the following command:</span><span class="sxs-lookup"><span data-stu-id="bad76-208">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="bad76-209">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span><span class="sxs-lookup"><span data-stu-id="bad76-209">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="bad76-210">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span><span class="sxs-lookup"><span data-stu-id="bad76-210">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="bad76-211">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span><span class="sxs-lookup"><span data-stu-id="bad76-211">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="bad76-212">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bad76-212">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
