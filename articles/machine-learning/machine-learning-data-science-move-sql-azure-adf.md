---
title: Move data from an on-premise SQL Server to SQL Azure with Azure Data Factory | Microsoft Docs
description: Set up an ADF pipeline that composes two data migration activities that together move data on a daily basis between databases on-premise and in the cloud.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: bfe98d9a1d5024f080e95fd5354cd8b792d03bbc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662878"
---
# <a name="move-data-from-an-on-premise-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="63dc1-103">Move data from an on-premise SQL server to SQL Azure with Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="63dc1-103">Move data from an on-premise SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="63dc1-104">This topic shows how to move data from an on-premise SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="63dc1-104">This topic shows how to move data from an on-premise SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="63dc1-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="63dc1-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <a name="intro"></a><span data-ttu-id="63dc1-106">Introduction: What is ADF and when should it be used to migrate data?</span><span class="sxs-lookup"><span data-stu-id="63dc1-106">Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="63dc1-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span><span class="sxs-lookup"><span data-stu-id="63dc1-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="63dc1-108">The key concept in the ADF model is pipeline.</span><span class="sxs-lookup"><span data-stu-id="63dc1-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="63dc1-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span><span class="sxs-lookup"><span data-stu-id="63dc1-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="63dc1-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span><span class="sxs-lookup"><span data-stu-id="63dc1-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="63dc1-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span><span class="sxs-lookup"><span data-stu-id="63dc1-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="63dc1-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span><span class="sxs-lookup"><span data-stu-id="63dc1-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="63dc1-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span><span class="sxs-lookup"><span data-stu-id="63dc1-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="63dc1-114">Consider using ADF:</span><span class="sxs-lookup"><span data-stu-id="63dc1-114">Consider using ADF:</span></span>

* <span data-ttu-id="63dc1-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premise and cloud resources</span><span class="sxs-lookup"><span data-stu-id="63dc1-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premise and cloud resources</span></span>
* <span data-ttu-id="63dc1-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span><span class="sxs-lookup"><span data-stu-id="63dc1-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="63dc1-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span><span class="sxs-lookup"><span data-stu-id="63dc1-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="63dc1-118">ADF also has other capabilities such as support for complex operations.</span><span class="sxs-lookup"><span data-stu-id="63dc1-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="63dc1-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="63dc1-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <a name="scenario"></a><span data-ttu-id="63dc1-120">The Scenario</span><span class="sxs-lookup"><span data-stu-id="63dc1-120">The Scenario</span></span>
<span data-ttu-id="63dc1-121">We set up an ADF pipeline that composes two data migration activities.</span><span class="sxs-lookup"><span data-stu-id="63dc1-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="63dc1-122">Together they move data on a daily basis between an on-premise SQL database and an Azure SQL Database in the cloud.</span><span class="sxs-lookup"><span data-stu-id="63dc1-122">Together they move data on a daily basis between an on-premise SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="63dc1-123">The two activities are:</span><span class="sxs-lookup"><span data-stu-id="63dc1-123">The two activities are:</span></span>

* <span data-ttu-id="63dc1-124">copy data from an on-premise SQL Server database to an Azure Blob Storage account</span><span class="sxs-lookup"><span data-stu-id="63dc1-124">copy data from an on-premise SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="63dc1-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="63dc1-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="63dc1-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span><span class="sxs-lookup"><span data-stu-id="63dc1-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <a name="prereqs"></a><span data-ttu-id="63dc1-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63dc1-127">Prerequisites</span></span>
<span data-ttu-id="63dc1-128">This tutorial assumes you have:</span><span class="sxs-lookup"><span data-stu-id="63dc1-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="63dc1-129">An **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="63dc1-129">An **Azure subscription**.</span></span> <span data-ttu-id="63dc1-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63dc1-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="63dc1-131">An **Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="63dc1-131">An **Azure storage account**.</span></span> <span data-ttu-id="63dc1-132">You use an Azure storage account for storing the data in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="63dc1-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="63dc1-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article.</span><span class="sxs-lookup"><span data-stu-id="63dc1-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="63dc1-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span><span class="sxs-lookup"><span data-stu-id="63dc1-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="63dc1-135">See [Manage your storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="63dc1-135">See [Manage your storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="63dc1-136">Access to an **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="63dc1-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="63dc1-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="63dc1-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="63dc1-138">Installed and configured **Azure PowerShell** locally.</span><span class="sxs-lookup"><span data-stu-id="63dc1-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="63dc1-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="63dc1-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

> [!NOTE]
> <span data-ttu-id="63dc1-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="63dc1-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <a name="upload-data"></a> <span data-ttu-id="63dc1-141">Upload the data to your on-premise SQL Server</span><span class="sxs-lookup"><span data-stu-id="63dc1-141">Upload the data to your on-premise SQL Server</span></span>
<span data-ttu-id="63dc1-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span><span class="sxs-lookup"><span data-stu-id="63dc1-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="63dc1-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="63dc1-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="63dc1-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="63dc1-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="63dc1-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="63dc1-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="63dc1-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span><span class="sxs-lookup"><span data-stu-id="63dc1-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="63dc1-147">To upload the NYC Taxi dataset into your on-premise SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="63dc1-147">To upload the NYC Taxi dataset into your on-premise SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="63dc1-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premise SQL Server is the same.</span><span class="sxs-lookup"><span data-stu-id="63dc1-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premise SQL Server is the same.</span></span>

## <a name="create-adf"></a> <span data-ttu-id="63dc1-149">Create an Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="63dc1-149">Create an Azure Data Factory</span></span>
<span data-ttu-id="63dc1-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="63dc1-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="63dc1-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="63dc1-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="63dc1-152">Install and configure up the Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="63dc1-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="63dc1-153">To enable your pipelines in an Azure data factory to work with an on-premise SQL Server, you need to add it as a Linked Service to the data factory.</span><span class="sxs-lookup"><span data-stu-id="63dc1-153">To enable your pipelines in an Azure data factory to work with an on-premise SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="63dc1-154">To create a Linked Service for an on-premise SQL Server, you must:</span><span class="sxs-lookup"><span data-stu-id="63dc1-154">To create a Linked Service for an on-premise SQL Server, you must:</span></span>

* <span data-ttu-id="63dc1-155">download and install Microsoft Data Management Gateway onto the on-premise computer.</span><span class="sxs-lookup"><span data-stu-id="63dc1-155">download and install Microsoft Data Management Gateway onto the on-premise computer.</span></span>
* <span data-ttu-id="63dc1-156">configure the linked service for the on-premises data source to use the gateway.</span><span class="sxs-lookup"><span data-stu-id="63dc1-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="63dc1-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span><span class="sxs-lookup"><span data-stu-id="63dc1-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="63dc1-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="63dc1-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <a name="adflinkedservices"></a><span data-ttu-id="63dc1-159">Create linked services to connect to the data resources</span><span class="sxs-lookup"><span data-stu-id="63dc1-159">Create linked services to connect to the data resources</span></span>
<span data-ttu-id="63dc1-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span><span class="sxs-lookup"><span data-stu-id="63dc1-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="63dc1-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="63dc1-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="63dc1-162">We have three resources in this scenario for which linked services are needed.</span><span class="sxs-lookup"><span data-stu-id="63dc1-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="63dc1-163">Linked service for on-premise SQL Server</span><span class="sxs-lookup"><span data-stu-id="63dc1-163">Linked service for on-premise SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="63dc1-164">Linked service for Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="63dc1-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="63dc1-165">Linked service for Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="63dc1-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a><span data-ttu-id="63dc1-166">Linked service for on-premise SQL Server database</span><span class="sxs-lookup"><span data-stu-id="63dc1-166">Linked service for on-premise SQL Server database</span></span>
<span data-ttu-id="63dc1-167">To create the linked service for the on-premise SQL Server:</span><span class="sxs-lookup"><span data-stu-id="63dc1-167">To create the linked service for the on-premise SQL Server:</span></span>

* <span data-ttu-id="63dc1-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span><span class="sxs-lookup"><span data-stu-id="63dc1-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="63dc1-169">select **SQL** and enter the *username* and *password* credentials for the on-premise SQL Server.</span><span class="sxs-lookup"><span data-stu-id="63dc1-169">select **SQL** and enter the *username* and *password* credentials for the on-premise SQL Server.</span></span> <span data-ttu-id="63dc1-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span><span class="sxs-lookup"><span data-stu-id="63dc1-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="63dc1-171">Name the linked service *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="63dc1-171">Name the linked service *adfonpremsql*.</span></span>

### <a name="adf-linked-service-blob-store"></a><span data-ttu-id="63dc1-172">Linked service for Blob</span><span class="sxs-lookup"><span data-stu-id="63dc1-172">Linked service for Blob</span></span>
<span data-ttu-id="63dc1-173">To create the linked service for the Azure Blob Storage account:</span><span class="sxs-lookup"><span data-stu-id="63dc1-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="63dc1-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span><span class="sxs-lookup"><span data-stu-id="63dc1-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="63dc1-175">select **Azure Storage Account**</span><span class="sxs-lookup"><span data-stu-id="63dc1-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="63dc1-176">enter the Azure Blob Storage account key and container name.</span><span class="sxs-lookup"><span data-stu-id="63dc1-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="63dc1-177">Name the Linked Service *adfds*.</span><span class="sxs-lookup"><span data-stu-id="63dc1-177">Name the Linked Service *adfds*.</span></span>

### <a name="adf-linked-service-azure-sql"></a><span data-ttu-id="63dc1-178">Linked service for Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="63dc1-178">Linked service for Azure SQL database</span></span>
<span data-ttu-id="63dc1-179">To create the linked service for the Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="63dc1-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="63dc1-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span><span class="sxs-lookup"><span data-stu-id="63dc1-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="63dc1-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="63dc1-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="63dc1-182">The *username* must be specified as *user@servername*.</span><span class="sxs-lookup"><span data-stu-id="63dc1-182">The *username* must be specified as *user@servername*.</span></span>   

## <a name="adf-tables"></a><span data-ttu-id="63dc1-183">Define and create tables to specify how to access the datasets</span><span class="sxs-lookup"><span data-stu-id="63dc1-183">Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="63dc1-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span><span class="sxs-lookup"><span data-stu-id="63dc1-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="63dc1-185">JSON files are used to define the tables.</span><span class="sxs-lookup"><span data-stu-id="63dc1-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="63dc1-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="63dc1-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="63dc1-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span><span class="sxs-lookup"><span data-stu-id="63dc1-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="63dc1-188">For documentation of this cmdlet, see [Add-AzureAccount](https://msdn.microsoft.com/library/azure/dn790372.aspx).</span><span class="sxs-lookup"><span data-stu-id="63dc1-188">For documentation of this cmdlet, see [Add-AzureAccount](https://msdn.microsoft.com/library/azure/dn790372.aspx).</span></span>
>
>

<span data-ttu-id="63dc1-189">The JSON-based definitions in the tables use the following names:</span><span class="sxs-lookup"><span data-stu-id="63dc1-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="63dc1-190">the **table name** in the on-premise SQL server is *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="63dc1-190">the **table name** in the on-premise SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="63dc1-191">the **container name** in the Azure Blob Storage account is *containername*</span><span class="sxs-lookup"><span data-stu-id="63dc1-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="63dc1-192">Three table definitions are needed for this ADF pipeline:</span><span class="sxs-lookup"><span data-stu-id="63dc1-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="63dc1-193">SQL on-premise Table</span><span class="sxs-lookup"><span data-stu-id="63dc1-193">SQL on-premise Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="63dc1-194">Blob Table </span><span class="sxs-lookup"><span data-stu-id="63dc1-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="63dc1-195">SQL Azure Table</span><span class="sxs-lookup"><span data-stu-id="63dc1-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="63dc1-196">These procedures use Azure PowerShell to define and create the ADF activities.</span><span class="sxs-lookup"><span data-stu-id="63dc1-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="63dc1-197">But these tasks can also be accomplished using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="63dc1-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="63dc1-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="63dc1-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <a name="adf-table-onprem-sql"></a><span data-ttu-id="63dc1-199">SQL on-premise Table</span><span class="sxs-lookup"><span data-stu-id="63dc1-199">SQL on-premise Table</span></span>
<span data-ttu-id="63dc1-200">The table definition for the on-premise SQL Server is specified in the following JSON file:</span><span class="sxs-lookup"><span data-stu-id="63dc1-200">The table definition for the on-premise SQL Server is specified in the following JSON file:</span></span>

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

<span data-ttu-id="63dc1-201">The column names were not included here.</span><span class="sxs-lookup"><span data-stu-id="63dc1-201">The column names were not included here.</span></span> <span data-ttu-id="63dc1-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span><span class="sxs-lookup"><span data-stu-id="63dc1-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="63dc1-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="63dc1-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="63dc1-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="63dc1-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a><span data-ttu-id="63dc1-205">Blob Table</span><span class="sxs-lookup"><span data-stu-id="63dc1-205">Blob Table</span></span>
<span data-ttu-id="63dc1-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premise to Azure blob):</span><span class="sxs-lookup"><span data-stu-id="63dc1-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premise to Azure blob):</span></span>

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

<span data-ttu-id="63dc1-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="63dc1-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="63dc1-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="63dc1-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a><span data-ttu-id="63dc1-209">SQL Azure Table</span><span class="sxs-lookup"><span data-stu-id="63dc1-209">SQL Azure Table</span></span>
<span data-ttu-id="63dc1-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span><span class="sxs-lookup"><span data-stu-id="63dc1-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

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

<span data-ttu-id="63dc1-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="63dc1-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="63dc1-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="63dc1-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a><span data-ttu-id="63dc1-213">Define and create the pipeline</span><span class="sxs-lookup"><span data-stu-id="63dc1-213">Define and create the pipeline</span></span>
<span data-ttu-id="63dc1-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span><span class="sxs-lookup"><span data-stu-id="63dc1-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="63dc1-215">A JSON file is used to define the pipeline properties.</span><span class="sxs-lookup"><span data-stu-id="63dc1-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="63dc1-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="63dc1-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="63dc1-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span><span class="sxs-lookup"><span data-stu-id="63dc1-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="63dc1-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span><span class="sxs-lookup"><span data-stu-id="63dc1-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="63dc1-219">But this task can also be accomplished using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="63dc1-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="63dc1-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="63dc1-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="63dc1-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span><span class="sxs-lookup"><span data-stu-id="63dc1-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premise SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premise SQL server to blob",     
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

<span data-ttu-id="63dc1-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="63dc1-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="63dc1-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="63dc1-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="63dc1-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span><span class="sxs-lookup"><span data-stu-id="63dc1-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![ADF pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a><span data-ttu-id="63dc1-226">Start the Pipeline</span><span class="sxs-lookup"><span data-stu-id="63dc1-226">Start the Pipeline</span></span>
<span data-ttu-id="63dc1-227">The pipeline can now be run using the following command:</span><span class="sxs-lookup"><span data-stu-id="63dc1-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="63dc1-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span><span class="sxs-lookup"><span data-stu-id="63dc1-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="63dc1-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span><span class="sxs-lookup"><span data-stu-id="63dc1-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="63dc1-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span><span class="sxs-lookup"><span data-stu-id="63dc1-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="63dc1-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="63dc1-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>

