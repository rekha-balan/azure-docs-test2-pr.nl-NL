---
title: Move data to and from SQL Server | Microsoft Docs
description: Learn about how to move data to/from SQL Server database that is on-premises or in an Azure VM using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: c4038ea5a450f32a46f24a306d1ee30bd61308a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871271"
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="1f4c4-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1f4c4-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-sqlserver-connector.md)
> * [Version 2 (current version)](../connector-sql-server.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [SQL Server connector in V2](../connector-sql-server.md).

<span data-ttu-id="1f4c4-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="1f4c4-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="1f4c4-110">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="1f4c4-110">Supported scenarios</span></span>
<span data-ttu-id="1f4c4-111">You can copy data **from a SQL Server database** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-111">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="1f4c4-112">You can copy data from the following data stores **to a SQL Server database**:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-112">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="1f4c4-113">Supported SQL Server versions</span><span class="sxs-lookup"><span data-stu-id="1f4c4-113">Supported SQL Server versions</span></span>
<span data-ttu-id="1f4c4-114">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="1f4c4-114">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="1f4c4-115">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="1f4c4-115">Enabling connectivity</span></span>
<span data-ttu-id="1f4c4-116">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-116">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="1f4c4-117">In both cases, you need to use Data Management Gateway for connectivity.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-117">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="1f4c4-118">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-118">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="1f4c4-119">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-119">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="1f4c4-120">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-120">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="1f4c4-121">Having the gateway and SQL Server on separate machines reduces resource contention.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-121">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1f4c4-122">Getting started</span><span class="sxs-lookup"><span data-stu-id="1f4c4-122">Getting started</span></span>
<span data-ttu-id="1f4c4-123">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-123">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="1f4c4-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1f4c4-125">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-125">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="1f4c4-126">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-126">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1f4c4-127">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-127">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1f4c4-128">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-128">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="1f4c4-129">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-129">Create a **data factory**.</span></span> <span data-ttu-id="1f4c4-130">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-130">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="1f4c4-131">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-131">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="1f4c4-132">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-132">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="1f4c4-133">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-133">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="1f4c4-134">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-134">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="1f4c4-135">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-135">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="1f4c4-136">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-136">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="1f4c4-137">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-137">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="1f4c4-138">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-138">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="1f4c4-139">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-139">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="1f4c4-140">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-140">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="1f4c4-141">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-141">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="1f4c4-142">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-142">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="1f4c4-143">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-143">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1f4c4-144">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-144">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1f4c4-145">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-145">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="1f4c4-146">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-146">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="1f4c4-147">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="1f4c4-147">Linked service properties</span></span>
<span data-ttu-id="1f4c4-148">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-148">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="1f4c4-149">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-149">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="1f4c4-150">The following table provides description for JSON elements specific to SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-150">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="1f4c4-151">Property</span><span class="sxs-lookup"><span data-stu-id="1f4c4-151">Property</span></span> | <span data-ttu-id="1f4c4-152">Description</span><span class="sxs-lookup"><span data-stu-id="1f4c4-152">Description</span></span> | <span data-ttu-id="1f4c4-153">Required</span><span class="sxs-lookup"><span data-stu-id="1f4c4-153">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f4c4-154">type</span><span class="sxs-lookup"><span data-stu-id="1f4c4-154">type</span></span> |<span data-ttu-id="1f4c4-155">The type property should be set to: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-155">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="1f4c4-156">Yes</span><span class="sxs-lookup"><span data-stu-id="1f4c4-156">Yes</span></span> |
| <span data-ttu-id="1f4c4-157">connectionString</span><span class="sxs-lookup"><span data-stu-id="1f4c4-157">connectionString</span></span> |<span data-ttu-id="1f4c4-158">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-158">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="1f4c4-159">Yes</span><span class="sxs-lookup"><span data-stu-id="1f4c4-159">Yes</span></span> |
| <span data-ttu-id="1f4c4-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1f4c4-160">gatewayName</span></span> |<span data-ttu-id="1f4c4-161">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-161">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="1f4c4-162">Yes</span><span class="sxs-lookup"><span data-stu-id="1f4c4-162">Yes</span></span> |
| <span data-ttu-id="1f4c4-163">username</span><span class="sxs-lookup"><span data-stu-id="1f4c4-163">username</span></span> |<span data-ttu-id="1f4c4-164">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-164">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="1f4c4-165">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-165">Example: **domainname\\username**.</span></span> |<span data-ttu-id="1f4c4-166">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-166">No</span></span> |
| <span data-ttu-id="1f4c4-167">password</span><span class="sxs-lookup"><span data-stu-id="1f4c4-167">password</span></span> |<span data-ttu-id="1f4c4-168">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-168">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1f4c4-169">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-169">No</span></span> |

<span data-ttu-id="1f4c4-170">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span><span class="sxs-lookup"><span data-stu-id="1f4c4-170">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="1f4c4-171">Samples</span><span class="sxs-lookup"><span data-stu-id="1f4c4-171">Samples</span></span>
<span data-ttu-id="1f4c4-172">**JSON for using SQL Authentication**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-172">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="1f4c4-173">**JSON for using Windows Authentication**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-173">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="1f4c4-174">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-174">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="1f4c4-175">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="1f4c4-175">Dataset properties</span></span>
<span data-ttu-id="1f4c4-176">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-176">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="1f4c4-177">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-177">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1f4c4-178">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-178">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1f4c4-179">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-179">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1f4c4-180">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-180">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="1f4c4-181">Property</span><span class="sxs-lookup"><span data-stu-id="1f4c4-181">Property</span></span> | <span data-ttu-id="1f4c4-182">Description</span><span class="sxs-lookup"><span data-stu-id="1f4c4-182">Description</span></span> | <span data-ttu-id="1f4c4-183">Required</span><span class="sxs-lookup"><span data-stu-id="1f4c4-183">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f4c4-184">tableName</span><span class="sxs-lookup"><span data-stu-id="1f4c4-184">tableName</span></span> |<span data-ttu-id="1f4c4-185">Name of the table or view in the SQL Server Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-185">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="1f4c4-186">Yes</span><span class="sxs-lookup"><span data-stu-id="1f4c4-186">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="1f4c4-187">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="1f4c4-187">Copy activity properties</span></span>
<span data-ttu-id="1f4c4-188">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-188">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="1f4c4-189">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-189">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="1f4c4-190">This section provides a list of properties supported by SqlSource and SqlSink.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-190">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="1f4c4-191">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-191">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1f4c4-192">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-192">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> The Copy Activity takes only one input and produces only one output.

<span data-ttu-id="1f4c4-194">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-194">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="1f4c4-195">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-195">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="1f4c4-196">SqlSource</span><span class="sxs-lookup"><span data-stu-id="1f4c4-196">SqlSource</span></span>
<span data-ttu-id="1f4c4-197">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-197">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="1f4c4-198">Property</span><span class="sxs-lookup"><span data-stu-id="1f4c4-198">Property</span></span> | <span data-ttu-id="1f4c4-199">Description</span><span class="sxs-lookup"><span data-stu-id="1f4c4-199">Description</span></span> | <span data-ttu-id="1f4c4-200">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1f4c4-200">Allowed values</span></span> | <span data-ttu-id="1f4c4-201">Required</span><span class="sxs-lookup"><span data-stu-id="1f4c4-201">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f4c4-202">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="1f4c4-202">sqlReaderQuery</span></span> |<span data-ttu-id="1f4c4-203">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-203">Use the custom query to read data.</span></span> |<span data-ttu-id="1f4c4-204">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-204">SQL query string.</span></span> <span data-ttu-id="1f4c4-205">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-205">For example: select \* from MyTable.</span></span> <span data-ttu-id="1f4c4-206">May reference multiple tables from the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-206">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="1f4c4-207">If not specified, the SQL statement that is executed: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-207">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="1f4c4-208">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-208">No</span></span> |
| <span data-ttu-id="1f4c4-209">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1f4c4-209">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="1f4c4-210">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-210">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="1f4c4-211">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-211">Name of the stored procedure.</span></span> <span data-ttu-id="1f4c4-212">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-212">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="1f4c4-213">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-213">No</span></span> |
| <span data-ttu-id="1f4c4-214">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1f4c4-214">storedProcedureParameters</span></span> |<span data-ttu-id="1f4c4-215">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-215">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1f4c4-216">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-216">Name/value pairs.</span></span> <span data-ttu-id="1f4c4-217">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-217">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1f4c4-218">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-218">No</span></span> |

<span data-ttu-id="1f4c4-219">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-219">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="1f4c4-220">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-220">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="1f4c4-221">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-221">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="1f4c4-222">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-222">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON. There are no validations performed against this table though.

### <a name="sqlsink"></a><span data-ttu-id="1f4c4-225">SqlSink</span><span class="sxs-lookup"><span data-stu-id="1f4c4-225">SqlSink</span></span>
<span data-ttu-id="1f4c4-226">**SqlSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-226">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="1f4c4-227">Property</span><span class="sxs-lookup"><span data-stu-id="1f4c4-227">Property</span></span> | <span data-ttu-id="1f4c4-228">Description</span><span class="sxs-lookup"><span data-stu-id="1f4c4-228">Description</span></span> | <span data-ttu-id="1f4c4-229">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1f4c4-229">Allowed values</span></span> | <span data-ttu-id="1f4c4-230">Required</span><span class="sxs-lookup"><span data-stu-id="1f4c4-230">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f4c4-231">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1f4c4-231">writeBatchTimeout</span></span> |<span data-ttu-id="1f4c4-232">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-232">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="1f4c4-233">timespan</span><span class="sxs-lookup"><span data-stu-id="1f4c4-233">timespan</span></span><br/><br/> <span data-ttu-id="1f4c4-234">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-234">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="1f4c4-235">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-235">No</span></span> |
| <span data-ttu-id="1f4c4-236">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1f4c4-236">writeBatchSize</span></span> |<span data-ttu-id="1f4c4-237">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-237">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="1f4c4-238">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="1f4c4-238">Integer (number of rows)</span></span> |<span data-ttu-id="1f4c4-239">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="1f4c4-239">No (default: 10000)</span></span> |
| <span data-ttu-id="1f4c4-240">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1f4c4-240">sqlWriterCleanupScript</span></span> |<span data-ttu-id="1f4c4-241">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-241">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="1f4c4-242">For more information, see [repeatable copy](#repeatable-copy) section.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-242">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="1f4c4-243">A query statement.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-243">A query statement.</span></span> |<span data-ttu-id="1f4c4-244">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-244">No</span></span> |
| <span data-ttu-id="1f4c4-245">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="1f4c4-245">sliceIdentifierColumnName</span></span> |<span data-ttu-id="1f4c4-246">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-246">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="1f4c4-247">For more information, see [repeatable copy](#repeatable-copy) section.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-247">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="1f4c4-248">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-248">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="1f4c4-249">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-249">No</span></span> |
| <span data-ttu-id="1f4c4-250">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1f4c4-250">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="1f4c4-251">Name of the stored procedure that defines how to apply source data into target table, e.g. to do upserts or transform using your own business logic.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-251">Name of the stored procedure that defines how to apply source data into target table, e.g. to do upserts or transform using your own business logic.</span></span> <br/><br/><span data-ttu-id="1f4c4-252">Note this stored procedure will be **invoked per batch**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-252">Note this stored procedure will be **invoked per batch**.</span></span> <span data-ttu-id="1f4c4-253">If you want to do operation that only runs once and has nothing to do with source data e.g. delete/truncate, use `sqlWriterCleanupScript` property.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-253">If you want to do operation that only runs once and has nothing to do with source data e.g. delete/truncate, use `sqlWriterCleanupScript` property.</span></span> |<span data-ttu-id="1f4c4-254">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-254">Name of the stored procedure.</span></span> |<span data-ttu-id="1f4c4-255">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-255">No</span></span> |
| <span data-ttu-id="1f4c4-256">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1f4c4-256">storedProcedureParameters</span></span> |<span data-ttu-id="1f4c4-257">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-257">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1f4c4-258">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-258">Name/value pairs.</span></span> <span data-ttu-id="1f4c4-259">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-259">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1f4c4-260">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-260">No</span></span> |
| <span data-ttu-id="1f4c4-261">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="1f4c4-261">sqlWriterTableType</span></span> |<span data-ttu-id="1f4c4-262">Specify table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-262">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="1f4c4-263">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-263">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="1f4c4-264">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-264">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="1f4c4-265">A table type name.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-265">A table type name.</span></span> |<span data-ttu-id="1f4c4-266">No</span><span class="sxs-lookup"><span data-stu-id="1f4c4-266">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="1f4c4-267">JSON examples for copying data from and to SQL Server</span><span class="sxs-lookup"><span data-stu-id="1f4c4-267">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="1f4c4-268">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-268">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1f4c4-269">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-269">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="1f4c4-270">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-270">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="1f4c4-271">Example: Copy data from SQL Server to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1f4c4-271">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="1f4c4-272">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-272">The following sample shows:</span></span>

1. <span data-ttu-id="1f4c4-273">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-273">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="1f4c4-274">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-274">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1f4c4-275">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-275">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1f4c4-276">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-276">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1f4c4-277">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-277">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1f4c4-278">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-278">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="1f4c4-279">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-279">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1f4c4-280">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-280">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="1f4c4-281">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-281">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="1f4c4-282">**SQL Server linked service**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-282">**SQL Server linked service**</span></span>
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
<span data-ttu-id="1f4c4-283">**Azure Blob storage linked service**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-283">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="1f4c4-284">**SQL Server input dataset**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-284">**SQL Server input dataset**</span></span>

<span data-ttu-id="1f4c4-285">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-285">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="1f4c4-286">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-286">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="1f4c4-287">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-287">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="1f4c4-288">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-288">**Azure Blob output dataset**</span></span>

<span data-ttu-id="1f4c4-289">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-289">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1f4c4-290">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-290">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1f4c4-291">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-291">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="1f4c4-292">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-292">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="1f4c4-293">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-293">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1f4c4-294">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-294">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="1f4c4-295">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-295">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="1f4c4-296">In this example, **sqlReaderQuery** is specified for the SqlSource.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-296">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="1f4c4-297">The Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-297">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="1f4c4-298">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-298">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="1f4c4-299">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-299">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="1f4c4-300">It is not limited to only the table set as the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-300">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="1f4c4-301">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-301">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="1f4c4-302">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-302">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="1f4c4-303">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-303">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="1f4c4-304">Example: Copy data from Azure Blob to SQL Server</span><span class="sxs-lookup"><span data-stu-id="1f4c4-304">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="1f4c4-305">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-305">The following sample shows:</span></span>

1. <span data-ttu-id="1f4c4-306">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-306">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="1f4c4-307">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-307">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1f4c4-308">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-308">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="1f4c4-309">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-309">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1f4c4-310">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-310">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="1f4c4-311">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-311">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="1f4c4-312">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-312">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1f4c4-313">**SQL Server linked service**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-313">**SQL Server linked service**</span></span>

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
<span data-ttu-id="1f4c4-314">**Azure Blob storage linked service**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-314">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="1f4c4-315">**Azure Blob input dataset**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-315">**Azure Blob input dataset**</span></span>

<span data-ttu-id="1f4c4-316">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-316">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1f4c4-317">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-317">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1f4c4-318">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-318">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="1f4c4-319">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-319">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="1f4c4-320">**SQL Server output dataset**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-320">**SQL Server output dataset**</span></span>

<span data-ttu-id="1f4c4-321">The sample copies data to a table named “MyTable” in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-321">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="1f4c4-322">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-322">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="1f4c4-323">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-323">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="1f4c4-324">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-324">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="1f4c4-325">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-325">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1f4c4-326">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-326">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="1f4c4-327">Troubleshooting connection issues</span><span class="sxs-lookup"><span data-stu-id="1f4c4-327">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="1f4c4-328">Configure your SQL Server to accept remote connections.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-328">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="1f4c4-329">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-329">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="1f4c4-330">Select **Connections** from the list and check **Allow remote connections to the server**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-330">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Enable remote connections](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="1f4c4-332">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-332">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="1f4c4-333">Launch **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-333">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="1f4c4-334">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-334">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="1f4c4-335">You should see protocols in the right-pane.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-335">You should see protocols in the right-pane.</span></span> <span data-ttu-id="1f4c4-336">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-336">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Enable TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="1f4c4-338">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-338">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="1f4c4-339">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-339">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="1f4c4-340">Switch to the **IP Addresses** tab. Scroll down to see **IPAll** section.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-340">Switch to the **IP Addresses** tab. Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="1f4c4-341">Note down the \*\*TCP Port \*\*(default is **1433**).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-341">Note down the \*\*TCP Port \*\*(default is **1433**).</span></span>
5. <span data-ttu-id="1f4c4-342">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-342">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="1f4c4-343">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-343">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="1f4c4-344">For example: "<machine>.<domain>.corp.<company>.com,1433."</span><span class="sxs-lookup"><span data-stu-id="1f4c4-344">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.
   >
   > See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="1f4c4-347">Identity columns in the target database</span><span class="sxs-lookup"><span data-stu-id="1f4c4-347">Identity columns in the target database</span></span>
<span data-ttu-id="1f4c4-348">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-348">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="1f4c4-349">**Source table:**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-349">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="1f4c4-350">**Destination table:**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-350">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="1f4c4-351">Notice that the target table has an identity column.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-351">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="1f4c4-352">**Source dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-352">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="1f4c4-353">**Destination dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-353">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="1f4c4-354">Notice that as your source and target table have different schema (target has an additional column with identity).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-354">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="1f4c4-355">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-355">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="1f4c4-356">Invoke stored procedure from SQL sink</span><span class="sxs-lookup"><span data-stu-id="1f4c4-356">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="1f4c4-357">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-357">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="1f4c4-358">Type mapping for SQL server</span><span class="sxs-lookup"><span data-stu-id="1f4c4-358">Type mapping for SQL server</span></span>
<span data-ttu-id="1f4c4-359">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-359">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="1f4c4-360">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="1f4c4-360">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="1f4c4-361">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="1f4c4-361">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="1f4c4-362">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-362">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="1f4c4-363">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-363">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="1f4c4-364">SQL Server Database Engine type</span><span class="sxs-lookup"><span data-stu-id="1f4c4-364">SQL Server Database Engine type</span></span> | <span data-ttu-id="1f4c4-365">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="1f4c4-365">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="1f4c4-366">bigint</span><span class="sxs-lookup"><span data-stu-id="1f4c4-366">bigint</span></span> |<span data-ttu-id="1f4c4-367">Int64</span><span class="sxs-lookup"><span data-stu-id="1f4c4-367">Int64</span></span> |
| <span data-ttu-id="1f4c4-368">binary</span><span class="sxs-lookup"><span data-stu-id="1f4c4-368">binary</span></span> |<span data-ttu-id="1f4c4-369">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-369">Byte[]</span></span> |
| <span data-ttu-id="1f4c4-370">bit</span><span class="sxs-lookup"><span data-stu-id="1f4c4-370">bit</span></span> |<span data-ttu-id="1f4c4-371">Boolean</span><span class="sxs-lookup"><span data-stu-id="1f4c4-371">Boolean</span></span> |
| <span data-ttu-id="1f4c4-372">char</span><span class="sxs-lookup"><span data-stu-id="1f4c4-372">char</span></span> |<span data-ttu-id="1f4c4-373">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-373">String, Char[]</span></span> |
| <span data-ttu-id="1f4c4-374">date</span><span class="sxs-lookup"><span data-stu-id="1f4c4-374">date</span></span> |<span data-ttu-id="1f4c4-375">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f4c4-375">DateTime</span></span> |
| <span data-ttu-id="1f4c4-376">Datetime</span><span class="sxs-lookup"><span data-stu-id="1f4c4-376">Datetime</span></span> |<span data-ttu-id="1f4c4-377">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f4c4-377">DateTime</span></span> |
| <span data-ttu-id="1f4c4-378">datetime2</span><span class="sxs-lookup"><span data-stu-id="1f4c4-378">datetime2</span></span> |<span data-ttu-id="1f4c4-379">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f4c4-379">DateTime</span></span> |
| <span data-ttu-id="1f4c4-380">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="1f4c4-380">Datetimeoffset</span></span> |<span data-ttu-id="1f4c4-381">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="1f4c4-381">DateTimeOffset</span></span> |
| <span data-ttu-id="1f4c4-382">Decimal</span><span class="sxs-lookup"><span data-stu-id="1f4c4-382">Decimal</span></span> |<span data-ttu-id="1f4c4-383">Decimal</span><span class="sxs-lookup"><span data-stu-id="1f4c4-383">Decimal</span></span> |
| <span data-ttu-id="1f4c4-384">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="1f4c4-384">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="1f4c4-385">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-385">Byte[]</span></span> |
| <span data-ttu-id="1f4c4-386">Float</span><span class="sxs-lookup"><span data-stu-id="1f4c4-386">Float</span></span> |<span data-ttu-id="1f4c4-387">Double</span><span class="sxs-lookup"><span data-stu-id="1f4c4-387">Double</span></span> |
| <span data-ttu-id="1f4c4-388">image</span><span class="sxs-lookup"><span data-stu-id="1f4c4-388">image</span></span> |<span data-ttu-id="1f4c4-389">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-389">Byte[]</span></span> |
| <span data-ttu-id="1f4c4-390">int</span><span class="sxs-lookup"><span data-stu-id="1f4c4-390">int</span></span> |<span data-ttu-id="1f4c4-391">Int32</span><span class="sxs-lookup"><span data-stu-id="1f4c4-391">Int32</span></span> |
| <span data-ttu-id="1f4c4-392">money</span><span class="sxs-lookup"><span data-stu-id="1f4c4-392">money</span></span> |<span data-ttu-id="1f4c4-393">Decimal</span><span class="sxs-lookup"><span data-stu-id="1f4c4-393">Decimal</span></span> |
| <span data-ttu-id="1f4c4-394">nchar</span><span class="sxs-lookup"><span data-stu-id="1f4c4-394">nchar</span></span> |<span data-ttu-id="1f4c4-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-395">String, Char[]</span></span> |
| <span data-ttu-id="1f4c4-396">ntext</span><span class="sxs-lookup"><span data-stu-id="1f4c4-396">ntext</span></span> |<span data-ttu-id="1f4c4-397">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-397">String, Char[]</span></span> |
| <span data-ttu-id="1f4c4-398">numeric</span><span class="sxs-lookup"><span data-stu-id="1f4c4-398">numeric</span></span> |<span data-ttu-id="1f4c4-399">Decimal</span><span class="sxs-lookup"><span data-stu-id="1f4c4-399">Decimal</span></span> |
| <span data-ttu-id="1f4c4-400">nvarchar</span><span class="sxs-lookup"><span data-stu-id="1f4c4-400">nvarchar</span></span> |<span data-ttu-id="1f4c4-401">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-401">String, Char[]</span></span> |
| <span data-ttu-id="1f4c4-402">real</span><span class="sxs-lookup"><span data-stu-id="1f4c4-402">real</span></span> |<span data-ttu-id="1f4c4-403">Single</span><span class="sxs-lookup"><span data-stu-id="1f4c4-403">Single</span></span> |
| <span data-ttu-id="1f4c4-404">rowversion</span><span class="sxs-lookup"><span data-stu-id="1f4c4-404">rowversion</span></span> |<span data-ttu-id="1f4c4-405">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-405">Byte[]</span></span> |
| <span data-ttu-id="1f4c4-406">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="1f4c4-406">smalldatetime</span></span> |<span data-ttu-id="1f4c4-407">DateTime</span><span class="sxs-lookup"><span data-stu-id="1f4c4-407">DateTime</span></span> |
| <span data-ttu-id="1f4c4-408">smallint</span><span class="sxs-lookup"><span data-stu-id="1f4c4-408">smallint</span></span> |<span data-ttu-id="1f4c4-409">Int16</span><span class="sxs-lookup"><span data-stu-id="1f4c4-409">Int16</span></span> |
| <span data-ttu-id="1f4c4-410">smallmoney</span><span class="sxs-lookup"><span data-stu-id="1f4c4-410">smallmoney</span></span> |<span data-ttu-id="1f4c4-411">Decimal</span><span class="sxs-lookup"><span data-stu-id="1f4c4-411">Decimal</span></span> |
| <span data-ttu-id="1f4c4-412">sql_variant</span><span class="sxs-lookup"><span data-stu-id="1f4c4-412">sql_variant</span></span> |<span data-ttu-id="1f4c4-413">Object \*</span><span class="sxs-lookup"><span data-stu-id="1f4c4-413">Object \*</span></span> |
| <span data-ttu-id="1f4c4-414">text</span><span class="sxs-lookup"><span data-stu-id="1f4c4-414">text</span></span> |<span data-ttu-id="1f4c4-415">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-415">String, Char[]</span></span> |
| <span data-ttu-id="1f4c4-416">time</span><span class="sxs-lookup"><span data-stu-id="1f4c4-416">time</span></span> |<span data-ttu-id="1f4c4-417">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1f4c4-417">TimeSpan</span></span> |
| <span data-ttu-id="1f4c4-418">timestamp</span><span class="sxs-lookup"><span data-stu-id="1f4c4-418">timestamp</span></span> |<span data-ttu-id="1f4c4-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-419">Byte[]</span></span> |
| <span data-ttu-id="1f4c4-420">tinyint</span><span class="sxs-lookup"><span data-stu-id="1f4c4-420">tinyint</span></span> |<span data-ttu-id="1f4c4-421">Byte</span><span class="sxs-lookup"><span data-stu-id="1f4c4-421">Byte</span></span> |
| <span data-ttu-id="1f4c4-422">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="1f4c4-422">uniqueidentifier</span></span> |<span data-ttu-id="1f4c4-423">Guid</span><span class="sxs-lookup"><span data-stu-id="1f4c4-423">Guid</span></span> |
| <span data-ttu-id="1f4c4-424">varbinary</span><span class="sxs-lookup"><span data-stu-id="1f4c4-424">varbinary</span></span> |<span data-ttu-id="1f4c4-425">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-425">Byte[]</span></span> |
| <span data-ttu-id="1f4c4-426">varchar</span><span class="sxs-lookup"><span data-stu-id="1f4c4-426">varchar</span></span> |<span data-ttu-id="1f4c4-427">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="1f4c4-427">String, Char[]</span></span> |
| <span data-ttu-id="1f4c4-428">xml</span><span class="sxs-lookup"><span data-stu-id="1f4c4-428">xml</span></span> |<span data-ttu-id="1f4c4-429">Xml</span><span class="sxs-lookup"><span data-stu-id="1f4c4-429">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="1f4c4-430">Mapping source to sink columns</span><span class="sxs-lookup"><span data-stu-id="1f4c4-430">Mapping source to sink columns</span></span>
<span data-ttu-id="1f4c4-431">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-431">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="1f4c4-432">Repeatable copy</span><span class="sxs-lookup"><span data-stu-id="1f4c4-432">Repeatable copy</span></span>
<span data-ttu-id="1f4c4-433">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-433">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="1f4c4-434">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-434">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="1f4c4-435">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-435">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="1f4c4-436">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-436">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1f4c4-437">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-437">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1f4c4-438">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-438">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1f4c4-439">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="1f4c4-439">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1f4c4-440">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="1f4c4-440">Performance and Tuning</span></span>
<span data-ttu-id="1f4c4-441">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-441">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
