---
title: Move data from ODBC data stores | Microsoft Docs
description: Learn about how to move data from ODBC data stores using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jingwang
ms.openlocfilehash: bbdd4a413b7c803fc0e1345dcb13aa407fb4f956
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563574"
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="56397-103">Move data From ODBC data stores using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="56397-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="56397-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="56397-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="56397-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="56397-106">You can copy data from an ODBC data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="56397-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="56397-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="56397-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="56397-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="56397-109">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="56397-109">Enabling connectivity</span></span>
<span data-ttu-id="56397-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="56397-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="56397-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="56397-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="56397-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="56397-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="56397-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="56397-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span><span class="sxs-lookup"><span data-stu-id="56397-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="56397-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="56397-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="56397-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="56397-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="56397-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="56397-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="56397-118">Getting started</span></span>
<span data-ttu-id="56397-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="56397-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="56397-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="56397-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="56397-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="56397-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="56397-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="56397-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="56397-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="56397-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="56397-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="56397-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="56397-125">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="56397-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="56397-126">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="56397-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="56397-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="56397-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="56397-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="56397-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="56397-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="56397-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="56397-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="56397-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="56397-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span><span class="sxs-lookup"><span data-stu-id="56397-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="56397-132">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="56397-132">Linked service properties</span></span>
<span data-ttu-id="56397-133">The following table provides description for JSON elements specific to ODBC linked service.</span><span class="sxs-lookup"><span data-stu-id="56397-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="56397-134">Property</span><span class="sxs-lookup"><span data-stu-id="56397-134">Property</span></span> | <span data-ttu-id="56397-135">Description</span><span class="sxs-lookup"><span data-stu-id="56397-135">Description</span></span> | <span data-ttu-id="56397-136">Required</span><span class="sxs-lookup"><span data-stu-id="56397-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56397-137">type</span><span class="sxs-lookup"><span data-stu-id="56397-137">type</span></span> |<span data-ttu-id="56397-138">The type property must be set to: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="56397-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="56397-139">Yes</span><span class="sxs-lookup"><span data-stu-id="56397-139">Yes</span></span> |
| <span data-ttu-id="56397-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="56397-140">connectionString</span></span> |<span data-ttu-id="56397-141">The non-access credential portion of the connection string and an optional encrypted credential.</span><span class="sxs-lookup"><span data-stu-id="56397-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="56397-142">See examples in the following sections.</span><span class="sxs-lookup"><span data-stu-id="56397-142">See examples in the following sections.</span></span> |<span data-ttu-id="56397-143">Yes</span><span class="sxs-lookup"><span data-stu-id="56397-143">Yes</span></span> |
| <span data-ttu-id="56397-144">credential</span><span class="sxs-lookup"><span data-stu-id="56397-144">credential</span></span> |<span data-ttu-id="56397-145">The access credential portion of the connection string specified in driver-specific property-value format.</span><span class="sxs-lookup"><span data-stu-id="56397-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="56397-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="56397-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="56397-147">No</span><span class="sxs-lookup"><span data-stu-id="56397-147">No</span></span> |
| <span data-ttu-id="56397-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="56397-148">authenticationType</span></span> |<span data-ttu-id="56397-149">Type of authentication used to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="56397-150">Possible values are: Anonymous and Basic.</span><span class="sxs-lookup"><span data-stu-id="56397-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="56397-151">Yes</span><span class="sxs-lookup"><span data-stu-id="56397-151">Yes</span></span> |
| <span data-ttu-id="56397-152">username</span><span class="sxs-lookup"><span data-stu-id="56397-152">username</span></span> |<span data-ttu-id="56397-153">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="56397-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="56397-154">No</span><span class="sxs-lookup"><span data-stu-id="56397-154">No</span></span> |
| <span data-ttu-id="56397-155">password</span><span class="sxs-lookup"><span data-stu-id="56397-155">password</span></span> |<span data-ttu-id="56397-156">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="56397-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="56397-157">No</span><span class="sxs-lookup"><span data-stu-id="56397-157">No</span></span> |
| <span data-ttu-id="56397-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="56397-158">gatewayName</span></span> |<span data-ttu-id="56397-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="56397-160">Yes</span><span class="sxs-lookup"><span data-stu-id="56397-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="56397-161">Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="56397-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="56397-162">Using Basic authentication with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="56397-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="56397-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="56397-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="56397-164">Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="56397-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="56397-165">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="56397-165">Dataset properties</span></span>
<span data-ttu-id="56397-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="56397-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="56397-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="56397-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="56397-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="56397-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="56397-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="56397-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="56397-170">Property</span><span class="sxs-lookup"><span data-stu-id="56397-170">Property</span></span> | <span data-ttu-id="56397-171">Description</span><span class="sxs-lookup"><span data-stu-id="56397-171">Description</span></span> | <span data-ttu-id="56397-172">Required</span><span class="sxs-lookup"><span data-stu-id="56397-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56397-173">tableName</span><span class="sxs-lookup"><span data-stu-id="56397-173">tableName</span></span> |<span data-ttu-id="56397-174">Name of the table in the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="56397-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="56397-175">Yes</span><span class="sxs-lookup"><span data-stu-id="56397-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="56397-176">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="56397-176">Copy activity properties</span></span>
<span data-ttu-id="56397-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="56397-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="56397-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="56397-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="56397-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="56397-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="56397-180">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="56397-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="56397-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="56397-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="56397-182">Property</span><span class="sxs-lookup"><span data-stu-id="56397-182">Property</span></span> | <span data-ttu-id="56397-183">Description</span><span class="sxs-lookup"><span data-stu-id="56397-183">Description</span></span> | <span data-ttu-id="56397-184">Allowed values</span><span class="sxs-lookup"><span data-stu-id="56397-184">Allowed values</span></span> | <span data-ttu-id="56397-185">Required</span><span class="sxs-lookup"><span data-stu-id="56397-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56397-186">query</span><span class="sxs-lookup"><span data-stu-id="56397-186">query</span></span> |<span data-ttu-id="56397-187">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="56397-187">Use the custom query to read data.</span></span> |<span data-ttu-id="56397-188">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="56397-188">SQL query string.</span></span> <span data-ttu-id="56397-189">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="56397-189">For example: select \* from MyTable.</span></span> |<span data-ttu-id="56397-190">Yes</span><span class="sxs-lookup"><span data-stu-id="56397-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="56397-191">JSON example: Copy data from ODBC data store to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="56397-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="56397-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="56397-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="56397-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="56397-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="56397-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="56397-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="56397-195">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="56397-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="56397-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="56397-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="56397-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="56397-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="56397-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="56397-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="56397-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="56397-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="56397-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="56397-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="56397-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="56397-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="56397-202">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="56397-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="56397-203">As a first step, set up the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="56397-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="56397-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="56397-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="56397-205">**ODBC linked service** This example uses the Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="56397-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="56397-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="56397-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="56397-207">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="56397-207">**Azure Storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```

<span data-ttu-id="56397-208">**ODBC input dataset**</span><span class="sxs-lookup"><span data-stu-id="56397-208">**ODBC input dataset**</span></span>

<span data-ttu-id="56397-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="56397-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="56397-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="56397-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="56397-211">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="56397-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="56397-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="56397-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="56397-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="56397-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="56397-214">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="56397-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


<span data-ttu-id="56397-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="56397-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="56397-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="56397-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="56397-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="56397-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="56397-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="56397-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="56397-219">Type mapping for ODBC</span><span class="sxs-lookup"><span data-stu-id="56397-219">Type mapping for ODBC</span></span>
<span data-ttu-id="56397-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="56397-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="56397-221">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="56397-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="56397-222">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="56397-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="56397-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="56397-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="56397-224">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="56397-224">Map source to sink columns</span></span>
<span data-ttu-id="56397-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="56397-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="56397-226">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="56397-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="56397-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="56397-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="56397-228">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="56397-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="56397-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="56397-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="56397-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="56397-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="56397-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="56397-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="56397-232">GE Historian store</span><span class="sxs-lookup"><span data-stu-id="56397-232">GE Historian store</span></span>
<span data-ttu-id="56397-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="56397-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="56397-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span><span class="sxs-lookup"><span data-stu-id="56397-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="56397-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span><span class="sxs-lookup"><span data-stu-id="56397-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="56397-236">Therefore, install the driver if it is not already installed on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="56397-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="56397-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span><span class="sxs-lookup"><span data-stu-id="56397-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="56397-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span><span class="sxs-lookup"><span data-stu-id="56397-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="56397-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="56397-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="56397-240">Troubleshoot connectivity issues</span><span class="sxs-lookup"><span data-stu-id="56397-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="56397-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="56397-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="56397-242">Launch **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="56397-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="56397-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="56397-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Search gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="56397-245">Switch to the **Diagnostics** tab.</span><span class="sxs-lookup"><span data-stu-id="56397-245">Switch to the **Diagnostics** tab.</span></span>

    ![Gateway diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="56397-247">Select the **type** of data store (linked service).</span><span class="sxs-lookup"><span data-stu-id="56397-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="56397-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="56397-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="56397-249">Click **Test connection** to test the connection to the data store.</span><span class="sxs-lookup"><span data-stu-id="56397-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="56397-250">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="56397-250">Performance and Tuning</span></span>
<span data-ttu-id="56397-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="56397-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>


