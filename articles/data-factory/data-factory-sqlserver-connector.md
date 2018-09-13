---
title: Move data to and from SQL Server | Microsoft Docs
description: Learn about how to move data to/from SQL Server database that is on-premises or in an Azure VM using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2017
ms.author: jingwang
ms.openlocfilehash: 7a5ba2a47211f709016d1c559d48e83a2a8f0605
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552213"
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="9079b-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9079b-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="9079b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="9079b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="9079b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="9079b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="9079b-106">You can copy data from any supported source data store to SQL Server database or from SQL Server database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="9079b-106">You can copy data from any supported source data store to SQL Server database or from SQL Server database to any supported sink data store.</span></span> <span data-ttu-id="9079b-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="9079b-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="supported-sql-server-versions"></a><span data-ttu-id="9079b-108">Supported SQL Server versions</span><span class="sxs-lookup"><span data-stu-id="9079b-108">Supported SQL Server versions</span></span>
<span data-ttu-id="9079b-109">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="9079b-109">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="9079b-110">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="9079b-110">Enabling connectivity</span></span>
<span data-ttu-id="9079b-111">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span><span class="sxs-lookup"><span data-stu-id="9079b-111">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="9079b-112">In both cases, you need to use Data Management Gateway for connectivity.</span><span class="sxs-lookup"><span data-stu-id="9079b-112">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="9079b-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="9079b-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="9079b-114">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9079b-114">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="9079b-115">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span><span class="sxs-lookup"><span data-stu-id="9079b-115">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="9079b-116">Having the gateway and SQL Server on separate machines reduces resource contention.</span><span class="sxs-lookup"><span data-stu-id="9079b-116">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9079b-117">Getting started</span><span class="sxs-lookup"><span data-stu-id="9079b-117">Getting started</span></span>
<span data-ttu-id="9079b-118">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="9079b-118">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="9079b-119">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="9079b-119">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="9079b-120">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="9079b-120">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="9079b-121">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="9079b-121">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9079b-122">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="9079b-122">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9079b-123">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="9079b-123">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="9079b-124">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="9079b-124">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="9079b-125">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="9079b-125">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="9079b-126">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="9079b-126">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9079b-127">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="9079b-127">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9079b-128">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="9079b-128">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="9079b-129">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="9079b-129">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="9079b-130">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span><span class="sxs-lookup"><span data-stu-id="9079b-130">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="9079b-131">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="9079b-131">Linked service properties</span></span>
<span data-ttu-id="9079b-132">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span><span class="sxs-lookup"><span data-stu-id="9079b-132">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="9079b-133">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="9079b-133">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="9079b-134">The following table provides description for JSON elements specific to SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="9079b-134">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="9079b-135">Property</span><span class="sxs-lookup"><span data-stu-id="9079b-135">Property</span></span> | <span data-ttu-id="9079b-136">Description</span><span class="sxs-lookup"><span data-stu-id="9079b-136">Description</span></span> | <span data-ttu-id="9079b-137">Required</span><span class="sxs-lookup"><span data-stu-id="9079b-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9079b-138">type</span><span class="sxs-lookup"><span data-stu-id="9079b-138">type</span></span> |<span data-ttu-id="9079b-139">The type property should be set to: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="9079b-139">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="9079b-140">Yes</span><span class="sxs-lookup"><span data-stu-id="9079b-140">Yes</span></span> |
| <span data-ttu-id="9079b-141">connectionString</span><span class="sxs-lookup"><span data-stu-id="9079b-141">connectionString</span></span> |<span data-ttu-id="9079b-142">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="9079b-142">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="9079b-143">Yes</span><span class="sxs-lookup"><span data-stu-id="9079b-143">Yes</span></span> |
| <span data-ttu-id="9079b-144">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9079b-144">gatewayName</span></span> |<span data-ttu-id="9079b-145">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="9079b-145">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="9079b-146">Yes</span><span class="sxs-lookup"><span data-stu-id="9079b-146">Yes</span></span> |
| <span data-ttu-id="9079b-147">username</span><span class="sxs-lookup"><span data-stu-id="9079b-147">username</span></span> |<span data-ttu-id="9079b-148">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="9079b-148">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="9079b-149">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="9079b-149">Example: **domainname\\username**.</span></span> |<span data-ttu-id="9079b-150">No</span><span class="sxs-lookup"><span data-stu-id="9079b-150">No</span></span> |
| <span data-ttu-id="9079b-151">password</span><span class="sxs-lookup"><span data-stu-id="9079b-151">password</span></span> |<span data-ttu-id="9079b-152">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="9079b-152">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="9079b-153">No</span><span class="sxs-lookup"><span data-stu-id="9079b-153">No</span></span> |

<span data-ttu-id="9079b-154">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span><span class="sxs-lookup"><span data-stu-id="9079b-154">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="9079b-155">Samples</span><span class="sxs-lookup"><span data-stu-id="9079b-155">Samples</span></span>
<span data-ttu-id="9079b-156">**JSON for using SQL Authentication**</span><span class="sxs-lookup"><span data-stu-id="9079b-156">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="9079b-157">**JSON for using Windows Authentication**</span><span class="sxs-lookup"><span data-stu-id="9079b-157">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="9079b-158">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="9079b-158">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="9079b-159">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span><span class="sxs-lookup"><span data-stu-id="9079b-159">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="9079b-160">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="9079b-160">Dataset properties</span></span>
<span data-ttu-id="9079b-161">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="9079b-161">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="9079b-162">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="9079b-162">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9079b-163">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="9079b-163">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9079b-164">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="9079b-164">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="9079b-165">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="9079b-165">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="9079b-166">Property</span><span class="sxs-lookup"><span data-stu-id="9079b-166">Property</span></span> | <span data-ttu-id="9079b-167">Description</span><span class="sxs-lookup"><span data-stu-id="9079b-167">Description</span></span> | <span data-ttu-id="9079b-168">Required</span><span class="sxs-lookup"><span data-stu-id="9079b-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9079b-169">tableName</span><span class="sxs-lookup"><span data-stu-id="9079b-169">tableName</span></span> |<span data-ttu-id="9079b-170">Name of the table or view in the SQL Server Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="9079b-170">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="9079b-171">Yes</span><span class="sxs-lookup"><span data-stu-id="9079b-171">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="9079b-172">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="9079b-172">Copy activity properties</span></span>
<span data-ttu-id="9079b-173">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="9079b-173">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="9079b-174">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="9079b-174">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="9079b-175">This section provides a list of properties supported by SqlSource and SqlSink.</span><span class="sxs-lookup"><span data-stu-id="9079b-175">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="9079b-176">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="9079b-176">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9079b-177">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="9079b-177">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="9079b-178">The Copy Activity takes only one input and produces only one output.</span><span class="sxs-lookup"><span data-stu-id="9079b-178">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="9079b-179">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="9079b-179">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="9079b-180">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="9079b-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="9079b-181">SqlSource</span><span class="sxs-lookup"><span data-stu-id="9079b-181">SqlSource</span></span>
<span data-ttu-id="9079b-182">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="9079b-182">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="9079b-183">Property</span><span class="sxs-lookup"><span data-stu-id="9079b-183">Property</span></span> | <span data-ttu-id="9079b-184">Description</span><span class="sxs-lookup"><span data-stu-id="9079b-184">Description</span></span> | <span data-ttu-id="9079b-185">Allowed values</span><span class="sxs-lookup"><span data-stu-id="9079b-185">Allowed values</span></span> | <span data-ttu-id="9079b-186">Required</span><span class="sxs-lookup"><span data-stu-id="9079b-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9079b-187">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="9079b-187">sqlReaderQuery</span></span> |<span data-ttu-id="9079b-188">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="9079b-188">Use the custom query to read data.</span></span> |<span data-ttu-id="9079b-189">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="9079b-189">SQL query string.</span></span> <span data-ttu-id="9079b-190">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="9079b-190">For example: select \* from MyTable.</span></span> <span data-ttu-id="9079b-191">May reference multiple tables from the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="9079b-191">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="9079b-192">If not specified, the SQL statement that is executed: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="9079b-192">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="9079b-193">No</span><span class="sxs-lookup"><span data-stu-id="9079b-193">No</span></span> |
| <span data-ttu-id="9079b-194">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="9079b-194">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="9079b-195">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="9079b-195">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="9079b-196">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9079b-196">Name of the stored procedure.</span></span> <span data-ttu-id="9079b-197">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9079b-197">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="9079b-198">No</span><span class="sxs-lookup"><span data-stu-id="9079b-198">No</span></span> |
| <span data-ttu-id="9079b-199">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="9079b-199">storedProcedureParameters</span></span> |<span data-ttu-id="9079b-200">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9079b-200">Parameters for the stored procedure.</span></span> |<span data-ttu-id="9079b-201">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="9079b-201">Name/value pairs.</span></span> <span data-ttu-id="9079b-202">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="9079b-202">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="9079b-203">No</span><span class="sxs-lookup"><span data-stu-id="9079b-203">No</span></span> |

<span data-ttu-id="9079b-204">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="9079b-204">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="9079b-205">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="9079b-205">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="9079b-206">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="9079b-206">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="9079b-207">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="9079b-207">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="9079b-208">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="9079b-208">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="9079b-209">There are no validations performed against this table though.</span><span class="sxs-lookup"><span data-stu-id="9079b-209">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="9079b-210">SqlSink</span><span class="sxs-lookup"><span data-stu-id="9079b-210">SqlSink</span></span>
<span data-ttu-id="9079b-211">**SqlSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="9079b-211">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="9079b-212">Property</span><span class="sxs-lookup"><span data-stu-id="9079b-212">Property</span></span> | <span data-ttu-id="9079b-213">Description</span><span class="sxs-lookup"><span data-stu-id="9079b-213">Description</span></span> | <span data-ttu-id="9079b-214">Allowed values</span><span class="sxs-lookup"><span data-stu-id="9079b-214">Allowed values</span></span> | <span data-ttu-id="9079b-215">Required</span><span class="sxs-lookup"><span data-stu-id="9079b-215">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9079b-216">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="9079b-216">writeBatchTimeout</span></span> |<span data-ttu-id="9079b-217">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="9079b-217">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="9079b-218">timespan</span><span class="sxs-lookup"><span data-stu-id="9079b-218">timespan</span></span><br/><br/> <span data-ttu-id="9079b-219">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="9079b-219">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="9079b-220">No</span><span class="sxs-lookup"><span data-stu-id="9079b-220">No</span></span> |
| <span data-ttu-id="9079b-221">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="9079b-221">writeBatchSize</span></span> |<span data-ttu-id="9079b-222">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="9079b-222">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="9079b-223">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="9079b-223">Integer (number of rows)</span></span> |<span data-ttu-id="9079b-224">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="9079b-224">No (default: 10000)</span></span> |
| <span data-ttu-id="9079b-225">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="9079b-225">sqlWriterCleanupScript</span></span> |<span data-ttu-id="9079b-226">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="9079b-226">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="9079b-227">For more information, see [repeatability](#repeatability-during-copy) section.</span><span class="sxs-lookup"><span data-stu-id="9079b-227">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="9079b-228">A query statement.</span><span class="sxs-lookup"><span data-stu-id="9079b-228">A query statement.</span></span> |<span data-ttu-id="9079b-229">No</span><span class="sxs-lookup"><span data-stu-id="9079b-229">No</span></span> |
| <span data-ttu-id="9079b-230">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="9079b-230">sliceIdentifierColumnName</span></span> |<span data-ttu-id="9079b-231">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="9079b-231">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="9079b-232">For more information, see [repeatability](#repeatability-during-copy) section.</span><span class="sxs-lookup"><span data-stu-id="9079b-232">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="9079b-233">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="9079b-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="9079b-234">No</span><span class="sxs-lookup"><span data-stu-id="9079b-234">No</span></span> |
| <span data-ttu-id="9079b-235">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="9079b-235">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="9079b-236">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span><span class="sxs-lookup"><span data-stu-id="9079b-236">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="9079b-237">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9079b-237">Name of the stored procedure.</span></span> |<span data-ttu-id="9079b-238">No</span><span class="sxs-lookup"><span data-stu-id="9079b-238">No</span></span> |
| <span data-ttu-id="9079b-239">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="9079b-239">storedProcedureParameters</span></span> |<span data-ttu-id="9079b-240">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9079b-240">Parameters for the stored procedure.</span></span> |<span data-ttu-id="9079b-241">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="9079b-241">Name/value pairs.</span></span> <span data-ttu-id="9079b-242">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="9079b-242">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="9079b-243">No</span><span class="sxs-lookup"><span data-stu-id="9079b-243">No</span></span> |
| <span data-ttu-id="9079b-244">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="9079b-244">sqlWriterTableType</span></span> |<span data-ttu-id="9079b-245">Specify table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9079b-245">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="9079b-246">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="9079b-246">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="9079b-247">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="9079b-247">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="9079b-248">A table type name.</span><span class="sxs-lookup"><span data-stu-id="9079b-248">A table type name.</span></span> |<span data-ttu-id="9079b-249">No</span><span class="sxs-lookup"><span data-stu-id="9079b-249">No</span></span> |


## <a name="json-examples"></a><span data-ttu-id="9079b-250">JSON examples</span><span class="sxs-lookup"><span data-stu-id="9079b-250">JSON examples</span></span>
<span data-ttu-id="9079b-251">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9079b-251">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9079b-252">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9079b-252">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="9079b-253">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9079b-253">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="9079b-254">Example: Copy data from SQL Server to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="9079b-254">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="9079b-255">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="9079b-255">The following sample shows:</span></span>

1. <span data-ttu-id="9079b-256">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-256">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="9079b-257">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-257">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9079b-258">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-258">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="9079b-259">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-259">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9079b-260">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-260">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9079b-261">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="9079b-261">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="9079b-262">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="9079b-262">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="9079b-263">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="9079b-263">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="9079b-264">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="9079b-264">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="9079b-265">**SQL Server linked service**</span><span class="sxs-lookup"><span data-stu-id="9079b-265">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="9079b-266">**Azure Blob storage linked service**</span><span class="sxs-lookup"><span data-stu-id="9079b-266">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="9079b-267">**SQL Server input dataset**</span><span class="sxs-lookup"><span data-stu-id="9079b-267">**SQL Server input dataset**</span></span>

<span data-ttu-id="9079b-268">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="9079b-268">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="9079b-269">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="9079b-269">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="9079b-270">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="9079b-270">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="9079b-271">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="9079b-271">**Azure Blob output dataset**</span></span>

<span data-ttu-id="9079b-272">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="9079b-272">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9079b-273">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="9079b-273">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9079b-274">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="9079b-274">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="9079b-275">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="9079b-275">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="9079b-276">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="9079b-276">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="9079b-277">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9079b-277">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="9079b-278">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="9079b-278">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="9079b-279">In this example, **sqlReaderQuery** is specified for the SqlSource.</span><span class="sxs-lookup"><span data-stu-id="9079b-279">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="9079b-280">The Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="9079b-280">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="9079b-281">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="9079b-281">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="9079b-282">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="9079b-282">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="9079b-283">It is not limited to only the table set as the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="9079b-283">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="9079b-284">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="9079b-284">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="9079b-285">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="9079b-285">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="9079b-286">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span><span class="sxs-lookup"><span data-stu-id="9079b-286">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="9079b-287">Example: Copy data from Azure Blob to SQL Server</span><span class="sxs-lookup"><span data-stu-id="9079b-287">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="9079b-288">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="9079b-288">The following sample shows:</span></span>

1. <span data-ttu-id="9079b-289">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-289">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="9079b-290">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-290">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9079b-291">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-291">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="9079b-292">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-292">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9079b-293">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="9079b-293">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="9079b-294">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span><span class="sxs-lookup"><span data-stu-id="9079b-294">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="9079b-295">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="9079b-295">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="9079b-296">**SQL Server linked service**</span><span class="sxs-lookup"><span data-stu-id="9079b-296">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="9079b-297">**Azure Blob storage linked service**</span><span class="sxs-lookup"><span data-stu-id="9079b-297">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="9079b-298">**Azure Blob input dataset**</span><span class="sxs-lookup"><span data-stu-id="9079b-298">**Azure Blob input dataset**</span></span>

<span data-ttu-id="9079b-299">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="9079b-299">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9079b-300">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="9079b-300">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9079b-301">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="9079b-301">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="9079b-302">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="9079b-302">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="9079b-303">**SQL Server output dataset**</span><span class="sxs-lookup"><span data-stu-id="9079b-303">**SQL Server output dataset**</span></span>

<span data-ttu-id="9079b-304">The sample copies data to a table named “MyTable” in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9079b-304">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="9079b-305">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="9079b-305">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="9079b-306">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="9079b-306">New rows are added to the table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="9079b-307">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="9079b-307">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="9079b-308">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="9079b-308">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="9079b-309">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="9079b-309">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="9079b-310">Troubleshooting connection issues</span><span class="sxs-lookup"><span data-stu-id="9079b-310">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="9079b-311">Configure your SQL Server to accept remote connections.</span><span class="sxs-lookup"><span data-stu-id="9079b-311">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="9079b-312">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="9079b-312">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="9079b-313">Select **Connections** from the list and check **Allow remote connections to the server**.</span><span class="sxs-lookup"><span data-stu-id="9079b-313">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Enable remote connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="9079b-315">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="9079b-315">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="9079b-316">Launch **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="9079b-316">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="9079b-317">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="9079b-317">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="9079b-318">You should see protocols in the right-pane.</span><span class="sxs-lookup"><span data-stu-id="9079b-318">You should see protocols in the right-pane.</span></span> <span data-ttu-id="9079b-319">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span><span class="sxs-lookup"><span data-stu-id="9079b-319">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Enable TCP/IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="9079b-321">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span><span class="sxs-lookup"><span data-stu-id="9079b-321">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="9079b-322">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span><span class="sxs-lookup"><span data-stu-id="9079b-322">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="9079b-323">Switch to the **IP Addresses** tab. Scroll down to see **IPAll** section.</span><span class="sxs-lookup"><span data-stu-id="9079b-323">Switch to the **IP Addresses** tab. Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="9079b-324">Note down the \*\*TCP Port \*\*(default is **1433**).</span><span class="sxs-lookup"><span data-stu-id="9079b-324">Note down the \*\*TCP Port \*\*(default is **1433**).</span></span>
5. <span data-ttu-id="9079b-325">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span><span class="sxs-lookup"><span data-stu-id="9079b-325">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="9079b-326">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span><span class="sxs-lookup"><span data-stu-id="9079b-326">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="9079b-327">For example: "<machine>.<domain>.corp.<company>.com,1433."</span><span class="sxs-lookup"><span data-stu-id="9079b-327">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="9079b-328">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="9079b-328">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="9079b-329">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="9079b-329">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="9079b-330">Identity columns in the target database</span><span class="sxs-lookup"><span data-stu-id="9079b-330">Identity columns in the target database</span></span>
<span data-ttu-id="9079b-331">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span><span class="sxs-lookup"><span data-stu-id="9079b-331">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="9079b-332">**Source table:**</span><span class="sxs-lookup"><span data-stu-id="9079b-332">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="9079b-333">**Destination table:**</span><span class="sxs-lookup"><span data-stu-id="9079b-333">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="9079b-334">Notice that the target table has an identity column.</span><span class="sxs-lookup"><span data-stu-id="9079b-334">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="9079b-335">**Source dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="9079b-335">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="9079b-336">**Destination dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="9079b-336">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="9079b-337">Notice that as your source and target table have different schema (target has an additional column with identity).</span><span class="sxs-lookup"><span data-stu-id="9079b-337">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="9079b-338">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span><span class="sxs-lookup"><span data-stu-id="9079b-338">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="9079b-339">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="9079b-339">Map source to sink columns</span></span>
<span data-ttu-id="9079b-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9079b-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="9079b-341">Repeatable copy</span><span class="sxs-lookup"><span data-stu-id="9079b-341">Repeatable copy</span></span>
<span data-ttu-id="9079b-342">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span><span class="sxs-lookup"><span data-stu-id="9079b-342">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="9079b-343">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span><span class="sxs-lookup"><span data-stu-id="9079b-343">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="9079b-344">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="9079b-344">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="9079b-345">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="9079b-345">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9079b-346">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="9079b-346">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="9079b-347">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="9079b-347">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="9079b-348">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="9079b-348">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="9079b-349">Invoke stored procedure from SQL sink</span><span class="sxs-lookup"><span data-stu-id="9079b-349">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="9079b-350">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span><span class="sxs-lookup"><span data-stu-id="9079b-350">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server--azure-sql"></a><span data-ttu-id="9079b-351">Type mapping for SQL server & Azure SQL</span><span class="sxs-lookup"><span data-stu-id="9079b-351">Type mapping for SQL server & Azure SQL</span></span>
<span data-ttu-id="9079b-352">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="9079b-352">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="9079b-353">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="9079b-353">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="9079b-354">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="9079b-354">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="9079b-355">When moving data to & from Azure SQL, SQL server, Sybase the following mappings are used from SQL type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="9079b-355">When moving data to & from Azure SQL, SQL server, Sybase the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="9079b-356">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="9079b-356">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="9079b-357">SQL Server Database Engine type</span><span class="sxs-lookup"><span data-stu-id="9079b-357">SQL Server Database Engine type</span></span> | <span data-ttu-id="9079b-358">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="9079b-358">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="9079b-359">bigint</span><span class="sxs-lookup"><span data-stu-id="9079b-359">bigint</span></span> |<span data-ttu-id="9079b-360">Int64</span><span class="sxs-lookup"><span data-stu-id="9079b-360">Int64</span></span> |
| <span data-ttu-id="9079b-361">binary</span><span class="sxs-lookup"><span data-stu-id="9079b-361">binary</span></span> |<span data-ttu-id="9079b-362">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9079b-362">Byte[]</span></span> |
| <span data-ttu-id="9079b-363">bit</span><span class="sxs-lookup"><span data-stu-id="9079b-363">bit</span></span> |<span data-ttu-id="9079b-364">Boolean</span><span class="sxs-lookup"><span data-stu-id="9079b-364">Boolean</span></span> |
| <span data-ttu-id="9079b-365">char</span><span class="sxs-lookup"><span data-stu-id="9079b-365">char</span></span> |<span data-ttu-id="9079b-366">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="9079b-366">String, Char[]</span></span> |
| <span data-ttu-id="9079b-367">date</span><span class="sxs-lookup"><span data-stu-id="9079b-367">date</span></span> |<span data-ttu-id="9079b-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="9079b-368">DateTime</span></span> |
| <span data-ttu-id="9079b-369">Datetime</span><span class="sxs-lookup"><span data-stu-id="9079b-369">Datetime</span></span> |<span data-ttu-id="9079b-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="9079b-370">DateTime</span></span> |
| <span data-ttu-id="9079b-371">datetime2</span><span class="sxs-lookup"><span data-stu-id="9079b-371">datetime2</span></span> |<span data-ttu-id="9079b-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="9079b-372">DateTime</span></span> |
| <span data-ttu-id="9079b-373">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="9079b-373">Datetimeoffset</span></span> |<span data-ttu-id="9079b-374">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="9079b-374">DateTimeOffset</span></span> |
| <span data-ttu-id="9079b-375">Decimal</span><span class="sxs-lookup"><span data-stu-id="9079b-375">Decimal</span></span> |<span data-ttu-id="9079b-376">Decimal</span><span class="sxs-lookup"><span data-stu-id="9079b-376">Decimal</span></span> |
| <span data-ttu-id="9079b-377">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="9079b-377">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="9079b-378">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9079b-378">Byte[]</span></span> |
| <span data-ttu-id="9079b-379">Float</span><span class="sxs-lookup"><span data-stu-id="9079b-379">Float</span></span> |<span data-ttu-id="9079b-380">Double</span><span class="sxs-lookup"><span data-stu-id="9079b-380">Double</span></span> |
| <span data-ttu-id="9079b-381">image</span><span class="sxs-lookup"><span data-stu-id="9079b-381">image</span></span> |<span data-ttu-id="9079b-382">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9079b-382">Byte[]</span></span> |
| <span data-ttu-id="9079b-383">int</span><span class="sxs-lookup"><span data-stu-id="9079b-383">int</span></span> |<span data-ttu-id="9079b-384">Int32</span><span class="sxs-lookup"><span data-stu-id="9079b-384">Int32</span></span> |
| <span data-ttu-id="9079b-385">money</span><span class="sxs-lookup"><span data-stu-id="9079b-385">money</span></span> |<span data-ttu-id="9079b-386">Decimal</span><span class="sxs-lookup"><span data-stu-id="9079b-386">Decimal</span></span> |
| <span data-ttu-id="9079b-387">nchar</span><span class="sxs-lookup"><span data-stu-id="9079b-387">nchar</span></span> |<span data-ttu-id="9079b-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="9079b-388">String, Char[]</span></span> |
| <span data-ttu-id="9079b-389">ntext</span><span class="sxs-lookup"><span data-stu-id="9079b-389">ntext</span></span> |<span data-ttu-id="9079b-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="9079b-390">String, Char[]</span></span> |
| <span data-ttu-id="9079b-391">numeric</span><span class="sxs-lookup"><span data-stu-id="9079b-391">numeric</span></span> |<span data-ttu-id="9079b-392">Decimal</span><span class="sxs-lookup"><span data-stu-id="9079b-392">Decimal</span></span> |
| <span data-ttu-id="9079b-393">nvarchar</span><span class="sxs-lookup"><span data-stu-id="9079b-393">nvarchar</span></span> |<span data-ttu-id="9079b-394">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="9079b-394">String, Char[]</span></span> |
| <span data-ttu-id="9079b-395">real</span><span class="sxs-lookup"><span data-stu-id="9079b-395">real</span></span> |<span data-ttu-id="9079b-396">Single</span><span class="sxs-lookup"><span data-stu-id="9079b-396">Single</span></span> |
| <span data-ttu-id="9079b-397">rowversion</span><span class="sxs-lookup"><span data-stu-id="9079b-397">rowversion</span></span> |<span data-ttu-id="9079b-398">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9079b-398">Byte[]</span></span> |
| <span data-ttu-id="9079b-399">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="9079b-399">smalldatetime</span></span> |<span data-ttu-id="9079b-400">DateTime</span><span class="sxs-lookup"><span data-stu-id="9079b-400">DateTime</span></span> |
| <span data-ttu-id="9079b-401">smallint</span><span class="sxs-lookup"><span data-stu-id="9079b-401">smallint</span></span> |<span data-ttu-id="9079b-402">Int16</span><span class="sxs-lookup"><span data-stu-id="9079b-402">Int16</span></span> |
| <span data-ttu-id="9079b-403">smallmoney</span><span class="sxs-lookup"><span data-stu-id="9079b-403">smallmoney</span></span> |<span data-ttu-id="9079b-404">Decimal</span><span class="sxs-lookup"><span data-stu-id="9079b-404">Decimal</span></span> |
| <span data-ttu-id="9079b-405">sql_variant</span><span class="sxs-lookup"><span data-stu-id="9079b-405">sql_variant</span></span> |<span data-ttu-id="9079b-406">Object \*</span><span class="sxs-lookup"><span data-stu-id="9079b-406">Object \*</span></span> |
| <span data-ttu-id="9079b-407">text</span><span class="sxs-lookup"><span data-stu-id="9079b-407">text</span></span> |<span data-ttu-id="9079b-408">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="9079b-408">String, Char[]</span></span> |
| <span data-ttu-id="9079b-409">time</span><span class="sxs-lookup"><span data-stu-id="9079b-409">time</span></span> |<span data-ttu-id="9079b-410">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9079b-410">TimeSpan</span></span> |
| <span data-ttu-id="9079b-411">timestamp</span><span class="sxs-lookup"><span data-stu-id="9079b-411">timestamp</span></span> |<span data-ttu-id="9079b-412">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9079b-412">Byte[]</span></span> |
| <span data-ttu-id="9079b-413">tinyint</span><span class="sxs-lookup"><span data-stu-id="9079b-413">tinyint</span></span> |<span data-ttu-id="9079b-414">Byte</span><span class="sxs-lookup"><span data-stu-id="9079b-414">Byte</span></span> |
| <span data-ttu-id="9079b-415">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="9079b-415">uniqueidentifier</span></span> |<span data-ttu-id="9079b-416">Guid</span><span class="sxs-lookup"><span data-stu-id="9079b-416">Guid</span></span> |
| <span data-ttu-id="9079b-417">varbinary</span><span class="sxs-lookup"><span data-stu-id="9079b-417">varbinary</span></span> |<span data-ttu-id="9079b-418">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9079b-418">Byte[]</span></span> |
| <span data-ttu-id="9079b-419">varchar</span><span class="sxs-lookup"><span data-stu-id="9079b-419">varchar</span></span> |<span data-ttu-id="9079b-420">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="9079b-420">String, Char[]</span></span> |
| <span data-ttu-id="9079b-421">xml</span><span class="sxs-lookup"><span data-stu-id="9079b-421">xml</span></span> |<span data-ttu-id="9079b-422">Xml</span><span class="sxs-lookup"><span data-stu-id="9079b-422">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="9079b-423">Mapping source to sink columns</span><span class="sxs-lookup"><span data-stu-id="9079b-423">Mapping source to sink columns</span></span>
<span data-ttu-id="9079b-424">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9079b-424">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9079b-425">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="9079b-425">Performance and Tuning</span></span>
<span data-ttu-id="9079b-426">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="9079b-426">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>


