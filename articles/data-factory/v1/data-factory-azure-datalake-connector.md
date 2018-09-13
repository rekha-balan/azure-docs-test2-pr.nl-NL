---
title: Copy data to and from Azure Data Lake Storage Gen1 | Microsoft Docs
description: Learn how to copy data to and from Data Lake Store by using Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 97bd2081df8c90f885996629862f25cbec8fd2c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864698"
---
# <a name="copy-data-to-and-from-data-lake-storage-gen1-by-using-data-factory"></a><span data-ttu-id="7220f-103">Copy data to and from Data Lake Storage Gen1 by using Data Factory</span><span class="sxs-lookup"><span data-stu-id="7220f-103">Copy data to and from Data Lake Storage Gen1 by using Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-datalake-connector.md)
> * [Version 2 (current version)](../connector-azure-data-lake-store.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure Data Lake Storage Gen1 connector in V2](../connector-azure-data-lake-store.md).

<span data-ttu-id="7220f-108">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Storage Gen1 (previously known as Azure Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="7220f-108">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Storage Gen1 (previously known as Azure Data Lake Store).</span></span> <span data-ttu-id="7220f-109">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="7220f-109">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="7220f-110">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="7220f-110">Supported scenarios</span></span>
<span data-ttu-id="7220f-111">You can copy data **from Azure Data Lake Store** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="7220f-111">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="7220f-112">You can copy data from the following data stores **to Azure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="7220f-112">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Create a Data Lake Store account before creating a pipeline with Copy Activity. For more information, see [Get started with Azure Data Lake Store](../../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a><span data-ttu-id="7220f-115">Supported authentication types</span><span class="sxs-lookup"><span data-stu-id="7220f-115">Supported authentication types</span></span>
<span data-ttu-id="7220f-116">The Data Lake Store connector supports these authentication types:</span><span class="sxs-lookup"><span data-stu-id="7220f-116">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="7220f-117">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="7220f-117">Service principal authentication</span></span>
* <span data-ttu-id="7220f-118">User credential (OAuth) authentication</span><span class="sxs-lookup"><span data-stu-id="7220f-118">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="7220f-119">We recommend that you use service principal authentication, especially for a scheduled data copy.</span><span class="sxs-lookup"><span data-stu-id="7220f-119">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="7220f-120">Token expiration behavior can occur with user credential authentication.</span><span class="sxs-lookup"><span data-stu-id="7220f-120">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="7220f-121">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="7220f-121">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="7220f-122">Get started</span><span class="sxs-lookup"><span data-stu-id="7220f-122">Get started</span></span>
<span data-ttu-id="7220f-123">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="7220f-123">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="7220f-124">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="7220f-124">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7220f-125">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7220f-125">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="7220f-126">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="7220f-126">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7220f-127">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="7220f-127">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="7220f-128">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="7220f-128">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="7220f-129">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="7220f-129">Create a **data factory**.</span></span> <span data-ttu-id="7220f-130">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="7220f-130">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="7220f-131">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7220f-131">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="7220f-132">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7220f-132">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="7220f-133">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="7220f-133">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="7220f-134">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="7220f-134">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="7220f-135">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="7220f-135">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="7220f-136">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span><span class="sxs-lookup"><span data-stu-id="7220f-136">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="7220f-137">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="7220f-137">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="7220f-138">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="7220f-138">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="7220f-139">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="7220f-139">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="7220f-140">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="7220f-140">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="7220f-141">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="7220f-141">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="7220f-142">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="7220f-142">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="7220f-143">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="7220f-143">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="7220f-144">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="7220f-144">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="7220f-145">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span><span class="sxs-lookup"><span data-stu-id="7220f-145">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="7220f-146">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7220f-146">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7220f-147">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="7220f-147">Linked service properties</span></span>
<span data-ttu-id="7220f-148">A linked service links a data store to a data factory.</span><span class="sxs-lookup"><span data-stu-id="7220f-148">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="7220f-149">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7220f-149">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="7220f-150">The following table describes JSON elements specific to Data Lake Store linked services.</span><span class="sxs-lookup"><span data-stu-id="7220f-150">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="7220f-151">You can choose between service principal and user credential authentication.</span><span class="sxs-lookup"><span data-stu-id="7220f-151">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="7220f-152">Property</span><span class="sxs-lookup"><span data-stu-id="7220f-152">Property</span></span> | <span data-ttu-id="7220f-153">Description</span><span class="sxs-lookup"><span data-stu-id="7220f-153">Description</span></span> | <span data-ttu-id="7220f-154">Required</span><span class="sxs-lookup"><span data-stu-id="7220f-154">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7220f-155">**type**</span><span class="sxs-lookup"><span data-stu-id="7220f-155">**type**</span></span> | <span data-ttu-id="7220f-156">The type property must be set to **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="7220f-156">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="7220f-157">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-157">Yes</span></span> |
| <span data-ttu-id="7220f-158">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="7220f-158">**dataLakeStoreUri**</span></span> | <span data-ttu-id="7220f-159">Information about the Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="7220f-159">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="7220f-160">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="7220f-160">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="7220f-161">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-161">Yes</span></span> |
| <span data-ttu-id="7220f-162">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="7220f-162">**subscriptionId**</span></span> | <span data-ttu-id="7220f-163">Azure subscription ID to which the Data Lake Store account belongs.</span><span class="sxs-lookup"><span data-stu-id="7220f-163">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="7220f-164">Required for sink</span><span class="sxs-lookup"><span data-stu-id="7220f-164">Required for sink</span></span> |
| <span data-ttu-id="7220f-165">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="7220f-165">**resourceGroupName**</span></span> | <span data-ttu-id="7220f-166">Azure resource group name to which the Data Lake Store account belongs.</span><span class="sxs-lookup"><span data-stu-id="7220f-166">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="7220f-167">Required for sink</span><span class="sxs-lookup"><span data-stu-id="7220f-167">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="7220f-168">Service principal authentication (recommended)</span><span class="sxs-lookup"><span data-stu-id="7220f-168">Service principal authentication (recommended)</span></span>
<span data-ttu-id="7220f-169">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7220f-169">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="7220f-170">For detailed steps, see [Service-to-service authentication](../../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="7220f-170">For detailed steps, see [Service-to-service authentication](../../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="7220f-171">Make note of the following values, which you use to define the linked service:</span><span class="sxs-lookup"><span data-stu-id="7220f-171">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="7220f-172">Application ID</span><span class="sxs-lookup"><span data-stu-id="7220f-172">Application ID</span></span>
* <span data-ttu-id="7220f-173">Application key</span><span class="sxs-lookup"><span data-stu-id="7220f-173">Application key</span></span> 
* <span data-ttu-id="7220f-174">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="7220f-174">Tenant ID</span></span>

> [!IMPORTANT]
> Make sure you grant the service principal proper permission in Azure Data Lake Store:
>- **To use Data Lake Store as source**, grant at least **Read + Execute** data access permission to list and copy the contents of a folder, or **Read** permission to copy a single file. No requirement on account level access control.
>- **To use Data Lake Store as sink**, grant at least **Write + Execute** data access permission to create child items in the folder. And if you use Azure IR to empower copy (both source and sink are in cloud), in order to let Data Factory detect Data Lake Store's region, grant at least **Reader** role in account access control (IAM). If you want to avoid this IAM role, [specify executionLocation](data-factory-data-movement-activities.md#global) with the location of your Data Lake Store in copy activity.
>- If you **use Copy Wizard to author pipelines**, grant at least **Reader** role in account access control (IAM). Also, grant at least **Read + Execute** permission to your Data Lake Store root ("/") and its children. Otherwise you might see the message "The credentials provided are invalid."

<span data-ttu-id="7220f-184">Use service principal authentication by specifying the following properties:</span><span class="sxs-lookup"><span data-stu-id="7220f-184">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="7220f-185">Property</span><span class="sxs-lookup"><span data-stu-id="7220f-185">Property</span></span> | <span data-ttu-id="7220f-186">Description</span><span class="sxs-lookup"><span data-stu-id="7220f-186">Description</span></span> | <span data-ttu-id="7220f-187">Required</span><span class="sxs-lookup"><span data-stu-id="7220f-187">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7220f-188">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="7220f-188">**servicePrincipalId**</span></span> | <span data-ttu-id="7220f-189">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="7220f-189">Specify the application's client ID.</span></span> | <span data-ttu-id="7220f-190">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-190">Yes</span></span> |
| <span data-ttu-id="7220f-191">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="7220f-191">**servicePrincipalKey**</span></span> | <span data-ttu-id="7220f-192">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="7220f-192">Specify the application's key.</span></span> | <span data-ttu-id="7220f-193">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-193">Yes</span></span> |
| <span data-ttu-id="7220f-194">**tenant**</span><span class="sxs-lookup"><span data-stu-id="7220f-194">**tenant**</span></span> | <span data-ttu-id="7220f-195">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="7220f-195">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="7220f-196">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7220f-196">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="7220f-197">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-197">Yes</span></span> |

<span data-ttu-id="7220f-198">**Example: Service principal authentication**</span><span class="sxs-lookup"><span data-stu-id="7220f-198">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="7220f-199">User credential authentication</span><span class="sxs-lookup"><span data-stu-id="7220f-199">User credential authentication</span></span>
<span data-ttu-id="7220f-200">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span><span class="sxs-lookup"><span data-stu-id="7220f-200">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="7220f-201">Property</span><span class="sxs-lookup"><span data-stu-id="7220f-201">Property</span></span> | <span data-ttu-id="7220f-202">Description</span><span class="sxs-lookup"><span data-stu-id="7220f-202">Description</span></span> | <span data-ttu-id="7220f-203">Required</span><span class="sxs-lookup"><span data-stu-id="7220f-203">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7220f-204">**authorization**</span><span class="sxs-lookup"><span data-stu-id="7220f-204">**authorization**</span></span> | <span data-ttu-id="7220f-205">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span><span class="sxs-lookup"><span data-stu-id="7220f-205">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="7220f-206">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-206">Yes</span></span> |
| <span data-ttu-id="7220f-207">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="7220f-207">**sessionId**</span></span> | <span data-ttu-id="7220f-208">OAuth session ID from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="7220f-208">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="7220f-209">Each session ID is unique and can be used only once.</span><span class="sxs-lookup"><span data-stu-id="7220f-209">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="7220f-210">This setting is automatically generated when you use the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="7220f-210">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="7220f-211">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-211">Yes</span></span> |

> [!IMPORTANT]
> Make sure you grant the user proper permission in Azure Data Lake Store:
>- **To use Data Lake Store as source**, grant at least **Read + Execute** data access permission to list and copy the contents of a folder, or **Read** permission to copy a single file. No requirement on account level access control.
>- **To use Data Lake Store as sink**, grant at least **Write + Execute** data access permission to create child items in the folder. And if you use Azure IR to empower copy (both source and sink are in cloud), in order to let Data Factory detect Data Lake Store's region, grant at least **Reader** role in account access control (IAM). If you want to avoid this IAM role, [specify executionLocation](data-factory-data-movement-activities.md#global) with the location of your Data Lake Store in copy activity.
>- If you **use Copy Wizard to author pipelines**, grant at least **Reader** role in account access control (IAM). Also, grant at least **Read + Execute** permission to your Data Lake Store root ("/") and its children. Otherwise you might see the message "The credentials provided are invalid."

<span data-ttu-id="7220f-221">**Example: User credential authentication**</span><span class="sxs-lookup"><span data-stu-id="7220f-221">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="7220f-222">Token expiration</span><span class="sxs-lookup"><span data-stu-id="7220f-222">Token expiration</span></span>
<span data-ttu-id="7220f-223">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span><span class="sxs-lookup"><span data-stu-id="7220f-223">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="7220f-224">The following message means that the authentication token has expired:</span><span class="sxs-lookup"><span data-stu-id="7220f-224">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="7220f-225">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="7220f-225">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7220f-226">AADSTS70008: The provided access grant is expired or revoked.</span><span class="sxs-lookup"><span data-stu-id="7220f-226">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="7220f-227">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="7220f-227">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="7220f-228">The following table shows the expiration times of different types of user accounts:</span><span class="sxs-lookup"><span data-stu-id="7220f-228">The following table shows the expiration times of different types of user accounts:</span></span>

| <span data-ttu-id="7220f-229">User type</span><span class="sxs-lookup"><span data-stu-id="7220f-229">User type</span></span> | <span data-ttu-id="7220f-230">Expires after</span><span class="sxs-lookup"><span data-stu-id="7220f-230">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="7220f-231">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span><span class="sxs-lookup"><span data-stu-id="7220f-231">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="7220f-232">12 hours</span><span class="sxs-lookup"><span data-stu-id="7220f-232">12 hours</span></span> |
| <span data-ttu-id="7220f-233">Users accounts managed by Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7220f-233">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="7220f-234">14 days after the last slice run</span><span class="sxs-lookup"><span data-stu-id="7220f-234">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="7220f-235">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span><span class="sxs-lookup"><span data-stu-id="7220f-235">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="7220f-236">If you change your password before the token expiration time, the token expires immediately.</span><span class="sxs-lookup"><span data-stu-id="7220f-236">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="7220f-237">You will see the message mentioned earlier in this section.</span><span class="sxs-lookup"><span data-stu-id="7220f-237">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="7220f-238">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="7220f-238">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="7220f-239">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span><span class="sxs-lookup"><span data-stu-id="7220f-239">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="7220f-240">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span><span class="sxs-lookup"><span data-stu-id="7220f-240">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="7220f-241">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span><span class="sxs-lookup"><span data-stu-id="7220f-241">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="7220f-242">Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="7220f-242">Troubleshooting tips</span></span>

<span data-ttu-id="7220f-243">**Symptom:** When copying data **into** Azure Data Lake Store, if your copy activity fail with the following error:</span><span class="sxs-lookup"><span data-stu-id="7220f-243">**Symptom:** When copying data **into** Azure Data Lake Store, if your copy activity fail with the following error:</span></span>

  ```
  Failed to detect the region for Azure Data Lake account {your account name}. Please make sure that the Resource Group name: {resource group name} and subscription ID: {subscription ID} of this Azure Data Lake Store resource are correct.
  ```

<span data-ttu-id="7220f-244">**Root cause:** There are 2 possible reasons:</span><span class="sxs-lookup"><span data-stu-id="7220f-244">**Root cause:** There are 2 possible reasons:</span></span>

1. <span data-ttu-id="7220f-245">The `resourceGroupName` and/or `subscriptionId` specified in Azure Data Lake Store linked service is incorrect;</span><span class="sxs-lookup"><span data-stu-id="7220f-245">The `resourceGroupName` and/or `subscriptionId` specified in Azure Data Lake Store linked service is incorrect;</span></span>
2. <span data-ttu-id="7220f-246">The user or the service principal doesn't have the needed permission.</span><span class="sxs-lookup"><span data-stu-id="7220f-246">The user or the service principal doesn't have the needed permission.</span></span>

<span data-ttu-id="7220f-247">**Resolution:**</span><span class="sxs-lookup"><span data-stu-id="7220f-247">**Resolution:**</span></span>

1. <span data-ttu-id="7220f-248">Make sure the `subscriptionId` and `resourceGroupName` you specify in the linked service `typeProperties` are indeed the ones that your data lake account belongs to.</span><span class="sxs-lookup"><span data-stu-id="7220f-248">Make sure the `subscriptionId` and `resourceGroupName` you specify in the linked service `typeProperties` are indeed the ones that your data lake account belongs to.</span></span>

2. <span data-ttu-id="7220f-249">Make sure you grant at least "**Reader**" role to the user or service principal on the data lake account.</span><span class="sxs-lookup"><span data-stu-id="7220f-249">Make sure you grant at least "**Reader**" role to the user or service principal on the data lake account.</span></span> <span data-ttu-id="7220f-250">Here is how to make it:</span><span class="sxs-lookup"><span data-stu-id="7220f-250">Here is how to make it:</span></span>

    1. <span data-ttu-id="7220f-251">Go to Azure Portal -> your Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="7220f-251">Go to Azure Portal -> your Data Lake Store account</span></span>
    2. <span data-ttu-id="7220f-252">Click "Access Control (IAM)" on the blade of the Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7220f-252">Click "Access Control (IAM)" on the blade of the Data Lake Store</span></span>
    3. <span data-ttu-id="7220f-253">Click "Add" in the blade of "Access Control (IAM)"</span><span class="sxs-lookup"><span data-stu-id="7220f-253">Click "Add" in the blade of "Access Control (IAM)"</span></span>
    4. <span data-ttu-id="7220f-254">Set "Role" as "Reader", and select the user or the service principal you use for copy to grant access</span><span class="sxs-lookup"><span data-stu-id="7220f-254">Set "Role" as "Reader", and select the user or the service principal you use for copy to grant access</span></span>

3. <span data-ttu-id="7220f-255">If you don't want to grant "Reader" role to the user or service principal, alernative is to [explicitly specify an execution location](data-factory-data-movement-activities.md#global) in copy activitywith the location of your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7220f-255">If you don't want to grant "Reader" role to the user or service principal, alernative is to [explicitly specify an execution location](data-factory-data-movement-activities.md#global) in copy activitywith the location of your Data Lake Store.</span></span> <span data-ttu-id="7220f-256">Example:</span><span class="sxs-lookup"><span data-stu-id="7220f-256">Example:</span></span>

    ```json
    {
      "name": "CopyToADLS",
      "type": "Copy",
      ......
      "typeProperties": {
        "source": {
          "type": "<source type>"
        },
        "sink": {
          "type": "AzureDataLakeStoreSink"
        },
        "exeuctionLocation": "West US"
      }
    }
    ```

## <a name="dataset-properties"></a><span data-ttu-id="7220f-257">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="7220f-257">Dataset properties</span></span>
<span data-ttu-id="7220f-258">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="7220f-258">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="7220f-259">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span><span class="sxs-lookup"><span data-stu-id="7220f-259">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="7220f-260">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-260">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7220f-261">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span><span class="sxs-lookup"><span data-stu-id="7220f-261">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="7220f-262">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="7220f-262">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="7220f-263">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="7220f-263">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="7220f-264">Property</span><span class="sxs-lookup"><span data-stu-id="7220f-264">Property</span></span> | <span data-ttu-id="7220f-265">Description</span><span class="sxs-lookup"><span data-stu-id="7220f-265">Description</span></span> | <span data-ttu-id="7220f-266">Required</span><span class="sxs-lookup"><span data-stu-id="7220f-266">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7220f-267">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="7220f-267">**folderPath**</span></span> |<span data-ttu-id="7220f-268">Path to the container and folder in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7220f-268">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="7220f-269">Yes</span><span class="sxs-lookup"><span data-stu-id="7220f-269">Yes</span></span> |
| <span data-ttu-id="7220f-270">**fileName**</span><span class="sxs-lookup"><span data-stu-id="7220f-270">**fileName**</span></span> |<span data-ttu-id="7220f-271">Name of the file in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7220f-271">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="7220f-272">The **fileName** property is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="7220f-272">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="7220f-273">If you specify **fileName**, the activity (including Copy) works on the specific file.</span><span class="sxs-lookup"><span data-stu-id="7220f-273">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="7220f-274">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span><span class="sxs-lookup"><span data-stu-id="7220f-274">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="7220f-275">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span><span class="sxs-lookup"><span data-stu-id="7220f-275">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="7220f-276">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="7220f-276">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="7220f-277">No</span><span class="sxs-lookup"><span data-stu-id="7220f-277">No</span></span> |
| <span data-ttu-id="7220f-278">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="7220f-278">**partitionedBy**</span></span> |<span data-ttu-id="7220f-279">The **partitionedBy** property is optional.</span><span class="sxs-lookup"><span data-stu-id="7220f-279">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="7220f-280">You can use it to specify a dynamic path and file name for time-series data.</span><span class="sxs-lookup"><span data-stu-id="7220f-280">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="7220f-281">For example, **folderPath** can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="7220f-281">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="7220f-282">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="7220f-282">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="7220f-283">No</span><span class="sxs-lookup"><span data-stu-id="7220f-283">No</span></span> |
| <span data-ttu-id="7220f-284">**format**</span><span class="sxs-lookup"><span data-stu-id="7220f-284">**format**</span></span> | <span data-ttu-id="7220f-285">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7220f-285">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="7220f-286">Set the **type** property under **format** to one of these values.</span><span class="sxs-lookup"><span data-stu-id="7220f-286">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="7220f-287">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-287">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="7220f-288">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="7220f-288">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="7220f-289">No</span><span class="sxs-lookup"><span data-stu-id="7220f-289">No</span></span> |
| <span data-ttu-id="7220f-290">**compression**</span><span class="sxs-lookup"><span data-stu-id="7220f-290">**compression**</span></span> | <span data-ttu-id="7220f-291">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="7220f-291">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="7220f-292">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7220f-292">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7220f-293">Supported levels are **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="7220f-293">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7220f-294">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7220f-294">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7220f-295">No</span><span class="sxs-lookup"><span data-stu-id="7220f-295">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="7220f-296">The partitionedBy property</span><span class="sxs-lookup"><span data-stu-id="7220f-296">The partitionedBy property</span></span>
<span data-ttu-id="7220f-297">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span><span class="sxs-lookup"><span data-stu-id="7220f-297">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="7220f-298">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-298">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="7220f-299">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="7220f-299">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="7220f-300">The name `SliceStart` refers to the start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="7220f-300">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="7220f-301">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="7220f-301">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="7220f-302">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span><span class="sxs-lookup"><span data-stu-id="7220f-302">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="7220f-303">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span><span class="sxs-lookup"><span data-stu-id="7220f-303">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="7220f-304">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="7220f-304">Copy activity properties</span></span>
<span data-ttu-id="7220f-305">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-305">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7220f-306">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="7220f-306">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7220f-307">The properties available in the **typeProperties** section of an activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="7220f-307">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="7220f-308">For a copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="7220f-308">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7220f-309">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="7220f-309">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="7220f-310">Property</span><span class="sxs-lookup"><span data-stu-id="7220f-310">Property</span></span> | <span data-ttu-id="7220f-311">Description</span><span class="sxs-lookup"><span data-stu-id="7220f-311">Description</span></span> | <span data-ttu-id="7220f-312">Allowed values</span><span class="sxs-lookup"><span data-stu-id="7220f-312">Allowed values</span></span> | <span data-ttu-id="7220f-313">Required</span><span class="sxs-lookup"><span data-stu-id="7220f-313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7220f-314">**recursive**</span><span class="sxs-lookup"><span data-stu-id="7220f-314">**recursive**</span></span> |<span data-ttu-id="7220f-315">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="7220f-315">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="7220f-316">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="7220f-316">True (default value), False</span></span> |<span data-ttu-id="7220f-317">No</span><span class="sxs-lookup"><span data-stu-id="7220f-317">No</span></span> |


<span data-ttu-id="7220f-318">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="7220f-318">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="7220f-319">Property</span><span class="sxs-lookup"><span data-stu-id="7220f-319">Property</span></span> | <span data-ttu-id="7220f-320">Description</span><span class="sxs-lookup"><span data-stu-id="7220f-320">Description</span></span> | <span data-ttu-id="7220f-321">Allowed values</span><span class="sxs-lookup"><span data-stu-id="7220f-321">Allowed values</span></span> | <span data-ttu-id="7220f-322">Required</span><span class="sxs-lookup"><span data-stu-id="7220f-322">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7220f-323">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="7220f-323">**copyBehavior**</span></span> |<span data-ttu-id="7220f-324">Specifies the copy behavior.</span><span class="sxs-lookup"><span data-stu-id="7220f-324">Specifies the copy behavior.</span></span> |<span data-ttu-id="7220f-325"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="7220f-325"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="7220f-326">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="7220f-326">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="7220f-327"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span><span class="sxs-lookup"><span data-stu-id="7220f-327"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="7220f-328">The target files are created with autogenerated names.</span><span class="sxs-lookup"><span data-stu-id="7220f-328">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="7220f-329"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="7220f-329"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="7220f-330">If the file or blob name is specified, the merged file name is the specified name.</span><span class="sxs-lookup"><span data-stu-id="7220f-330">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="7220f-331">Otherwise, the file name is autogenerated.</span><span class="sxs-lookup"><span data-stu-id="7220f-331">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="7220f-332">No</span><span class="sxs-lookup"><span data-stu-id="7220f-332">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="7220f-333">recursive and copyBehavior examples</span><span class="sxs-lookup"><span data-stu-id="7220f-333">recursive and copyBehavior examples</span></span>
<span data-ttu-id="7220f-334">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span><span class="sxs-lookup"><span data-stu-id="7220f-334">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="7220f-335">recursive</span><span class="sxs-lookup"><span data-stu-id="7220f-335">recursive</span></span> | <span data-ttu-id="7220f-336">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="7220f-336">copyBehavior</span></span> | <span data-ttu-id="7220f-337">Resulting behavior</span><span class="sxs-lookup"><span data-stu-id="7220f-337">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7220f-338">true</span><span class="sxs-lookup"><span data-stu-id="7220f-338">true</span></span> |<span data-ttu-id="7220f-339">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="7220f-339">preserveHierarchy</span></span> |<span data-ttu-id="7220f-340">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-340">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7220f-341">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-341">Folder1</span></span><br/><span data-ttu-id="7220f-342">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-342">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-343">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-343">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-344">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-344">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-345">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-345">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-346">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-346">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7220f-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7220f-348">the target folder Folder1 is created with the same structure as the source</span><span class="sxs-lookup"><span data-stu-id="7220f-348">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="7220f-349">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-349">Folder1</span></span><br/><span data-ttu-id="7220f-350">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-350">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-351">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-351">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-352">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-352">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-354">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-354">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-355">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="7220f-355">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="7220f-356">true</span><span class="sxs-lookup"><span data-stu-id="7220f-356">true</span></span> |<span data-ttu-id="7220f-357">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="7220f-357">flattenHierarchy</span></span> |<span data-ttu-id="7220f-358">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-358">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7220f-359">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-359">Folder1</span></span><br/><span data-ttu-id="7220f-360">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-360">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-361">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-361">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-362">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-362">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7220f-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7220f-366">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-366">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="7220f-367">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-367">Folder1</span></span><br/><span data-ttu-id="7220f-368">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="7220f-368">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="7220f-369">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="7220f-369">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="7220f-370">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span><span class="sxs-lookup"><span data-stu-id="7220f-370">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="7220f-371">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span><span class="sxs-lookup"><span data-stu-id="7220f-371">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="7220f-372">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span><span class="sxs-lookup"><span data-stu-id="7220f-372">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="7220f-373">true</span><span class="sxs-lookup"><span data-stu-id="7220f-373">true</span></span> |<span data-ttu-id="7220f-374">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="7220f-374">mergeFiles</span></span> |<span data-ttu-id="7220f-375">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-375">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7220f-376">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-376">Folder1</span></span><br/><span data-ttu-id="7220f-377">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-377">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-378">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-378">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-379">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-379">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-381">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-381">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-382">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7220f-382">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7220f-383">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-383">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="7220f-384">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-384">Folder1</span></span><br/><span data-ttu-id="7220f-385">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span><span class="sxs-lookup"><span data-stu-id="7220f-385">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="7220f-386">false</span><span class="sxs-lookup"><span data-stu-id="7220f-386">false</span></span> |<span data-ttu-id="7220f-387">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="7220f-387">preserveHierarchy</span></span> |<span data-ttu-id="7220f-388">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-388">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7220f-389">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-389">Folder1</span></span><br/><span data-ttu-id="7220f-390">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-390">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-391">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-391">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-392">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-392">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-395">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7220f-395">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7220f-396">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="7220f-396">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="7220f-397">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-397">Folder1</span></span><br/><span data-ttu-id="7220f-398">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-398">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-399">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-399">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="7220f-400">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="7220f-400">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="7220f-401">false</span><span class="sxs-lookup"><span data-stu-id="7220f-401">false</span></span> |<span data-ttu-id="7220f-402">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="7220f-402">flattenHierarchy</span></span> |<span data-ttu-id="7220f-403">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-403">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="7220f-404">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-404">Folder1</span></span><br/><span data-ttu-id="7220f-405">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-405">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-406">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-406">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-407">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-407">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-409">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-409">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-410">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7220f-410">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7220f-411">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="7220f-411">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="7220f-412">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-412">Folder1</span></span><br/><span data-ttu-id="7220f-413">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="7220f-413">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="7220f-414">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="7220f-414">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="7220f-415">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="7220f-415">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="7220f-416">false</span><span class="sxs-lookup"><span data-stu-id="7220f-416">false</span></span> |<span data-ttu-id="7220f-417">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="7220f-417">mergeFiles</span></span> |<span data-ttu-id="7220f-418">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7220f-418">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="7220f-419">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-419">Folder1</span></span><br/><span data-ttu-id="7220f-420">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7220f-420">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7220f-421">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7220f-421">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7220f-422">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7220f-422">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7220f-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7220f-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7220f-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7220f-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7220f-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7220f-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7220f-426">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="7220f-426">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="7220f-427">Folder1</span><span class="sxs-lookup"><span data-stu-id="7220f-427">Folder1</span></span><br/><span data-ttu-id="7220f-428">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="7220f-428">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="7220f-429">auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="7220f-429">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="7220f-430">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="7220f-430">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7220f-431">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="7220f-431">Supported file and compression formats</span></span>
<span data-ttu-id="7220f-432">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-432">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="7220f-433">JSON examples for copying data to and from Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7220f-433">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="7220f-434">The following examples provide sample JSON definitions.</span><span class="sxs-lookup"><span data-stu-id="7220f-434">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="7220f-435">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7220f-435">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7220f-436">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7220f-436">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="7220f-437">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span><span class="sxs-lookup"><span data-stu-id="7220f-437">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="7220f-438">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-438">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="7220f-439">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7220f-439">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="7220f-440">The example code in this section shows:</span><span class="sxs-lookup"><span data-stu-id="7220f-440">The example code in this section shows:</span></span>

* <span data-ttu-id="7220f-441">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-441">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="7220f-442">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-442">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="7220f-443">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-443">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="7220f-444">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-444">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="7220f-445">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-445">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="7220f-446">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span><span class="sxs-lookup"><span data-stu-id="7220f-446">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="7220f-447">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="7220f-447">**Azure Storage linked service**</span></span>

```JSON
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

<span data-ttu-id="7220f-448">**Azure Data Lake Store linked service**</span><span class="sxs-lookup"><span data-stu-id="7220f-448">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> For configuration details, see the [Linked service properties](#linked-service-properties) section.
>

<span data-ttu-id="7220f-450">**Azure blob input dataset**</span><span class="sxs-lookup"><span data-stu-id="7220f-450">**Azure blob input dataset**</span></span>

<span data-ttu-id="7220f-451">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="7220f-451">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="7220f-452">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="7220f-452">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="7220f-453">The folder path uses the year, month, and day portion of the start time.</span><span class="sxs-lookup"><span data-stu-id="7220f-453">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="7220f-454">The file name uses the hour portion of the start time.</span><span class="sxs-lookup"><span data-stu-id="7220f-454">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="7220f-455">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7220f-455">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="7220f-456">**Azure Data Lake Store output dataset**</span><span class="sxs-lookup"><span data-stu-id="7220f-456">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="7220f-457">The following example copies data to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7220f-457">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="7220f-458">New data is copied to Data Lake Store every hour.</span><span class="sxs-lookup"><span data-stu-id="7220f-458">New data is copied to Data Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="7220f-459">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span><span class="sxs-lookup"><span data-stu-id="7220f-459">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="7220f-460">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="7220f-460">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="7220f-461">The copy activity is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="7220f-461">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="7220f-462">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="7220f-462">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="7220f-463">Example: Copy data from Azure Data Lake Store to an Azure blob</span><span class="sxs-lookup"><span data-stu-id="7220f-463">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="7220f-464">The example code in this section shows:</span><span class="sxs-lookup"><span data-stu-id="7220f-464">The example code in this section shows:</span></span>

* <span data-ttu-id="7220f-465">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-465">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="7220f-466">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-466">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="7220f-467">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-467">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="7220f-468">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-468">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="7220f-469">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7220f-469">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7220f-470">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="7220f-470">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="7220f-471">**Azure Data Lake Store linked service**</span><span class="sxs-lookup"><span data-stu-id="7220f-471">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> For configuration details, see the [Linked service properties](#linked-service-properties) section.
>

<span data-ttu-id="7220f-473">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="7220f-473">**Azure Storage linked service**</span></span>

```JSON
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
<span data-ttu-id="7220f-474">**Azure Data Lake input dataset**</span><span class="sxs-lookup"><span data-stu-id="7220f-474">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="7220f-475">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7220f-475">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
<span data-ttu-id="7220f-476">**Azure blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="7220f-476">**Azure blob output dataset**</span></span>

<span data-ttu-id="7220f-477">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="7220f-477">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="7220f-478">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="7220f-478">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="7220f-479">The folder path uses the year, month, day, and hours portion of the start time.</span><span class="sxs-lookup"><span data-stu-id="7220f-479">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

```JSON
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

<span data-ttu-id="7220f-480">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span><span class="sxs-lookup"><span data-stu-id="7220f-480">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="7220f-481">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="7220f-481">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="7220f-482">The copy activity is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="7220f-482">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="7220f-483">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="7220f-483">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="7220f-484">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span><span class="sxs-lookup"><span data-stu-id="7220f-484">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="7220f-485">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7220f-485">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7220f-486">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="7220f-486">Performance and tuning</span></span>
<span data-ttu-id="7220f-487">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span><span class="sxs-lookup"><span data-stu-id="7220f-487">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
