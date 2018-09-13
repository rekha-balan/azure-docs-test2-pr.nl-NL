---
title: Move data to/from Azure Data Lake Store | Microsoft Docs
description: Learn how to move data to/from Azure Data Lake Store using Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: jingwang
ms.openlocfilehash: 3f0575a170eb20d136858bedc1f87d4f4375c812
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660662"
---
# <a name="move-data-to-and-from-azure-data-lake-store-using-azure-data-factory"></a><span data-ttu-id="e0a0d-103">Move data to and from Azure Data Lake Store using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e0a0d-103">Move data to and from Azure Data Lake Store using Azure Data Factory</span></span>
<span data-ttu-id="e0a0d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Data Lake Store.</span></span> <span data-ttu-id="e0a0d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="e0a0d-106">You can copy data from any supported source data store to Azure Data Lake Store or from Azure Data Lake Store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-106">You can copy data from any supported source data store to Azure Data Lake Store or from Azure Data Lake Store to any supported sink data store.</span></span> <span data-ttu-id="e0a0d-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span>  

> [!NOTE]
> <span data-ttu-id="e0a0d-108">Create an Azure Data Lake Store account before creating a pipeline with a Copy Activity to move data to/from an Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-108">Create an Azure Data Lake Store account before creating a pipeline with a Copy Activity to move data to/from an Azure Data Lake store.</span></span> <span data-ttu-id="e0a0d-109">To learn about Azure Data Lake Store, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-109">To learn about Azure Data Lake Store, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="e0a0d-110">Supported authentication types</span><span class="sxs-lookup"><span data-stu-id="e0a0d-110">Supported authentication types</span></span>
<span data-ttu-id="e0a0d-111">Azure Data Lake Store connector support **service principal** authentication and **user credential** (OAuth) authentication.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-111">Azure Data Lake Store connector support **service principal** authentication and **user credential** (OAuth) authentication.</span></span> <span data-ttu-id="e0a0d-112">You are suggested to use the former especially for scheduled data copy to avoid token expiration behavior with the latter.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-112">You are suggested to use the former especially for scheduled data copy to avoid token expiration behavior with the latter.</span></span> <span data-ttu-id="e0a0d-113">See [Linked service properties](#linked-service-properties) section with configuration details.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-113">See [Linked service properties](#linked-service-properties) section with configuration details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e0a0d-114">Getting started</span><span class="sxs-lookup"><span data-stu-id="e0a0d-114">Getting started</span></span>
<span data-ttu-id="e0a0d-115">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-115">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="e0a0d-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e0a0d-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="e0a0d-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e0a0d-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="e0a0d-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="e0a0d-121">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="e0a0d-122">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-122">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="e0a0d-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="e0a0d-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e0a0d-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e0a0d-126">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-126">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples) section of this article.</span></span>

<span data-ttu-id="e0a0d-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Data Lake Store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e0a0d-128">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="e0a0d-128">Linked service properties</span></span>
<span data-ttu-id="e0a0d-129">A linked service links a data store to a data factory.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-129">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="e0a0d-130">You create a linked service of type **AzureDataLakeStore** to link your Azure Data Lake store to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-130">You create a linked service of type **AzureDataLakeStore** to link your Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="e0a0d-131">The following table provides description for JSON elements specific to Azure Data Lake Store linked service, and you can choose between **service principal** and **user credential** authentication.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-131">The following table provides description for JSON elements specific to Azure Data Lake Store linked service, and you can choose between **service principal** and **user credential** authentication.</span></span>

| <span data-ttu-id="e0a0d-132">Property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-132">Property</span></span> | <span data-ttu-id="e0a0d-133">Description</span><span class="sxs-lookup"><span data-stu-id="e0a0d-133">Description</span></span> | <span data-ttu-id="e0a0d-134">Required</span><span class="sxs-lookup"><span data-stu-id="e0a0d-134">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e0a0d-135">type</span><span class="sxs-lookup"><span data-stu-id="e0a0d-135">type</span></span> | <span data-ttu-id="e0a0d-136">The type property must be set to: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-136">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="e0a0d-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-137">Yes</span></span> |
| <span data-ttu-id="e0a0d-138">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="e0a0d-138">dataLakeStoreUri</span></span> | <span data-ttu-id="e0a0d-139">Specify information about the Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-139">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="e0a0d-140">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-140">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="e0a0d-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-141">Yes</span></span> |
| <span data-ttu-id="e0a0d-142">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e0a0d-142">subscriptionId</span></span> | <span data-ttu-id="e0a0d-143">Azure subscription Id to which Data Lake Store belongs.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-143">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="e0a0d-144">Required for sink</span><span class="sxs-lookup"><span data-stu-id="e0a0d-144">Required for sink</span></span> |
| <span data-ttu-id="e0a0d-145">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e0a0d-145">resourceGroupName</span></span> | <span data-ttu-id="e0a0d-146">Azure resource group name to which Data Lake Store belongs.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-146">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="e0a0d-147">Required for sink</span><span class="sxs-lookup"><span data-stu-id="e0a0d-147">Required for sink</span></span> |

### <a name="using-service-principal-authentication-recommended"></a><span data-ttu-id="e0a0d-148">Using service principal authentication (recommended)</span><span class="sxs-lookup"><span data-stu-id="e0a0d-148">Using service principal authentication (recommended)</span></span>
<span data-ttu-id="e0a0d-149">To use service principal authentication, register an application entity in Azure Active Directory (AAD) and grant it the access to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-149">To use service principal authentication, register an application entity in Azure Active Directory (AAD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="e0a0d-150">See [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-150">See [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) for detailed steps.</span></span> <span data-ttu-id="e0a0d-151">Note down the following values: **application ID**, **application key**, and **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-151">Note down the following values: **application ID**, **application key**, and **tenant ID**.</span></span> <span data-ttu-id="e0a0d-152">You use this information in defining the linked service.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-152">You use this information in defining the linked service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0a0d-153">If you are using Copy Wizard to author data pipelines, make sure that you grant the service principal at least Reader role in Access control (IAM) for the Data Lake Store account and at least Read+Execute permission to your Data Lake Store root ("/") and its children.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-153">If you are using Copy Wizard to author data pipelines, make sure that you grant the service principal at least Reader role in Access control (IAM) for the Data Lake Store account and at least Read+Execute permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="e0a0d-154">Otherwise you may see "The credentials provided are invalid" error.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-154">Otherwise you may see "The credentials provided are invalid" error.</span></span>
>
> <span data-ttu-id="e0a0d-155">After you create/update a service principal in AAD, it may take a few minutes for the changes to actually take effect.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-155">After you create/update a service principal in AAD, it may take a few minutes for the changes to actually take effect.</span></span> <span data-ttu-id="e0a0d-156">First, double check the service principal and Data Lake Store ACL configuration.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-156">First, double check the service principal and Data Lake Store ACL configuration.</span></span> <span data-ttu-id="e0a0d-157">If you still see error: "The credentials provided are invalid", wait a while and try again.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-157">If you still see error: "The credentials provided are invalid", wait a while and try again.</span></span>

| <span data-ttu-id="e0a0d-158">Property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-158">Property</span></span> | <span data-ttu-id="e0a0d-159">Description</span><span class="sxs-lookup"><span data-stu-id="e0a0d-159">Description</span></span> | <span data-ttu-id="e0a0d-160">Required</span><span class="sxs-lookup"><span data-stu-id="e0a0d-160">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e0a0d-161">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="e0a0d-161">servicePrincipalId</span></span> | <span data-ttu-id="e0a0d-162">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-162">Specify the application's client ID.</span></span> | <span data-ttu-id="e0a0d-163">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-163">Yes</span></span> |
| <span data-ttu-id="e0a0d-164">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="e0a0d-164">servicePrincipalKey</span></span> | <span data-ttu-id="e0a0d-165">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-165">Specify the application's key.</span></span> | <span data-ttu-id="e0a0d-166">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-166">Yes</span></span> |
| <span data-ttu-id="e0a0d-167">tenant</span><span class="sxs-lookup"><span data-stu-id="e0a0d-167">tenant</span></span> | <span data-ttu-id="e0a0d-168">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-168">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="e0a0d-169">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-169">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="e0a0d-170">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-170">Yes</span></span> |

<span data-ttu-id="e0a0d-171">**Example: using service principal authentication**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-171">**Example: using service principal authentication**</span></span>
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

### <a name="using-user-credential-authentication"></a><span data-ttu-id="e0a0d-172">Using user credential authentication</span><span class="sxs-lookup"><span data-stu-id="e0a0d-172">Using user credential authentication</span></span>
<span data-ttu-id="e0a0d-173">Alternatively, you can use user credential authentication to copy from/to Data Lake Store by specifying the following properties:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-173">Alternatively, you can use user credential authentication to copy from/to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="e0a0d-174">Property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-174">Property</span></span> | <span data-ttu-id="e0a0d-175">Description</span><span class="sxs-lookup"><span data-stu-id="e0a0d-175">Description</span></span> | <span data-ttu-id="e0a0d-176">Required</span><span class="sxs-lookup"><span data-stu-id="e0a0d-176">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e0a0d-177">authorization</span><span class="sxs-lookup"><span data-stu-id="e0a0d-177">authorization</span></span> | <span data-ttu-id="e0a0d-178">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-178">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="e0a0d-179">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-179">Yes</span></span> |
| <span data-ttu-id="e0a0d-180">sessionId</span><span class="sxs-lookup"><span data-stu-id="e0a0d-180">sessionId</span></span> | <span data-ttu-id="e0a0d-181">OAuth session id from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-181">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="e0a0d-182">Each session id is unique and may only be used once.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-182">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="e0a0d-183">This setting is automatically generated when you use Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-183">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="e0a0d-184">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-184">Yes</span></span> |

<span data-ttu-id="e0a0d-185">**Example: using user credential authentication**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-185">**Example: using user credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="e0a0d-186">Token expiration</span><span class="sxs-lookup"><span data-stu-id="e0a0d-186">Token expiration</span></span>
<span data-ttu-id="e0a0d-187">The authorization code you generate by using the **Authorize** button expires after sometime.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-187">The authorization code you generate by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="e0a0d-188">See the following table for the expiration times for different types of user accounts.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-188">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="e0a0d-189">You may see the following error message when the authentication **token expires**:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-189">You may see the following error message when the authentication **token expires**:</span></span>

```
"Credential operation error: invalid_grant - AADSTS70002: Error validating credentials. AADSTS70008: The provided access grant is expired or revoked. Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z".
```

| <span data-ttu-id="e0a0d-190">User type</span><span class="sxs-lookup"><span data-stu-id="e0a0d-190">User type</span></span> | <span data-ttu-id="e0a0d-191">Expires after</span><span class="sxs-lookup"><span data-stu-id="e0a0d-191">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="e0a0d-192">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-192">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.).</span></span> |<span data-ttu-id="e0a0d-193">12 hours</span><span class="sxs-lookup"><span data-stu-id="e0a0d-193">12 hours</span></span> |
| <span data-ttu-id="e0a0d-194">Users accounts managed by Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="e0a0d-194">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="e0a0d-195">14 days after the last slice run.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-195">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="e0a0d-196">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-196">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="e0a0d-197">If you change your password before this token expiration time, the token expires immediately and you see the error mentioned in this section.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-197">If you change your password before this token expiration time, the token expires immediately and you see the error mentioned in this section.</span></span>

<span data-ttu-id="e0a0d-198">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-198">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="e0a0d-199">You can also generate values for **sessionId** and **authorization** properties programmatically using code in the following section:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-199">You can also generate values for **sessionId** and **authorization** properties programmatically using code in the following section:</span></span>

#### <a name="to-programmatically-generate-sessionid-and-authorization-values"></a><span data-ttu-id="e0a0d-200">To programmatically generate sessionId and authorization values</span><span class="sxs-lookup"><span data-stu-id="e0a0d-200">To programmatically generate sessionId and authorization values</span></span>

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
<span data-ttu-id="e0a0d-201">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-201">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="e0a0d-202">Add a reference to **2.9.10826.1824** version of **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll** for the WindowsFormsWebAuthenticationDialog class used in the code.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-202">Add a reference to **2.9.10826.1824** version of **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll** for the WindowsFormsWebAuthenticationDialog class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="e0a0d-203">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="e0a0d-203">Dataset properties</span></span>
<span data-ttu-id="e0a0d-204">To specify a dataset to represent input data in an Azure Data Lake Store, you set the type property of the dataset to: **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-204">To specify a dataset to represent input data in an Azure Data Lake Store, you set the type property of the dataset to: **AzureDataLakeStore**.</span></span> <span data-ttu-id="e0a0d-205">Set the **linkedServiceName** property of the dataset to the name of the Azure Data Lake Store linked service.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-205">Set the **linkedServiceName** property of the dataset to the name of the Azure Data Lake Store linked service.</span></span> <span data-ttu-id="e0a0d-206">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-206">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e0a0d-207">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-207">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span> <span data-ttu-id="e0a0d-208">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-208">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="e0a0d-209">The typeProperties section for dataset of type **AzureDataLakeStore** dataset has the following properties:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-209">The typeProperties section for dataset of type **AzureDataLakeStore** dataset has the following properties:</span></span>

| <span data-ttu-id="e0a0d-210">Property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-210">Property</span></span> | <span data-ttu-id="e0a0d-211">Description</span><span class="sxs-lookup"><span data-stu-id="e0a0d-211">Description</span></span> | <span data-ttu-id="e0a0d-212">Required</span><span class="sxs-lookup"><span data-stu-id="e0a0d-212">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e0a0d-213">folderPath</span><span class="sxs-lookup"><span data-stu-id="e0a0d-213">folderPath</span></span> |<span data-ttu-id="e0a0d-214">Path to the container and folder in the Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-214">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="e0a0d-215">Yes</span><span class="sxs-lookup"><span data-stu-id="e0a0d-215">Yes</span></span> |
| <span data-ttu-id="e0a0d-216">fileName</span><span class="sxs-lookup"><span data-stu-id="e0a0d-216">fileName</span></span> |<span data-ttu-id="e0a0d-217">Name of the file in the Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-217">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="e0a0d-218">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-218">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="e0a0d-219">If you specify a filename, the activity (including Copy) works on the specific file.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-219">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="e0a0d-220">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-220">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="e0a0d-221">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="e0a0d-221">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="e0a0d-222">No</span><span class="sxs-lookup"><span data-stu-id="e0a0d-222">No</span></span> |
| <span data-ttu-id="e0a0d-223">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e0a0d-223">partitionedBy</span></span> |<span data-ttu-id="e0a0d-224">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-224">partitionedBy is an optional property.</span></span> <span data-ttu-id="e0a0d-225">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-225">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="e0a0d-226">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-226">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="e0a0d-227">See the [Using partitionedBy property](#using-partitionedby-property) section for details and examples.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-227">See the [Using partitionedBy property](#using-partitionedby-property) section for details and examples.</span></span> |<span data-ttu-id="e0a0d-228">No</span><span class="sxs-lookup"><span data-stu-id="e0a0d-228">No</span></span> |
| <span data-ttu-id="e0a0d-229">format</span><span class="sxs-lookup"><span data-stu-id="e0a0d-229">format</span></span> | <span data-ttu-id="e0a0d-230">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-230">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e0a0d-231">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-231">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="e0a0d-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e0a0d-233">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-233">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e0a0d-234">No</span><span class="sxs-lookup"><span data-stu-id="e0a0d-234">No</span></span> |
| <span data-ttu-id="e0a0d-235">compression</span><span class="sxs-lookup"><span data-stu-id="e0a0d-235">compression</span></span> | <span data-ttu-id="e0a0d-236">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-236">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="e0a0d-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e0a0d-238">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e0a0d-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e0a0d-240">No</span><span class="sxs-lookup"><span data-stu-id="e0a0d-240">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="e0a0d-241">Using partitionedBy property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-241">Using partitionedBy property</span></span>
<span data-ttu-id="e0a0d-242">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-242">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="e0a0d-243">See [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles to understand more details on time series datasets, scheduling, and slices.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-243">See [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles to understand more details on time series datasets, scheduling, and slices.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="e0a0d-244">Sample 1</span><span class="sxs-lookup"><span data-stu-id="e0a0d-244">Sample 1</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="e0a0d-245">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-245">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="e0a0d-246">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-246">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="e0a0d-247">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-247">The folderPath is different for each slice.</span></span> <span data-ttu-id="e0a0d-248">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="e0a0d-248">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="e0a0d-249">Sample 2</span><span class="sxs-lookup"><span data-stu-id="e0a0d-249">Sample 2</span></span>
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
<span data-ttu-id="e0a0d-250">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-250">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e0a0d-251">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="e0a0d-251">Copy activity properties</span></span>
<span data-ttu-id="e0a0d-252">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-252">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e0a0d-253">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-253">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="e0a0d-254">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-254">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="e0a0d-255">For Copy activity, they vary depending on the types of sources and sinks</span><span class="sxs-lookup"><span data-stu-id="e0a0d-255">For Copy activity, they vary depending on the types of sources and sinks</span></span>

<span data-ttu-id="e0a0d-256">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-256">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="e0a0d-257">Property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-257">Property</span></span> | <span data-ttu-id="e0a0d-258">Description</span><span class="sxs-lookup"><span data-stu-id="e0a0d-258">Description</span></span> | <span data-ttu-id="e0a0d-259">Allowed values</span><span class="sxs-lookup"><span data-stu-id="e0a0d-259">Allowed values</span></span> | <span data-ttu-id="e0a0d-260">Required</span><span class="sxs-lookup"><span data-stu-id="e0a0d-260">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e0a0d-261">recursive</span><span class="sxs-lookup"><span data-stu-id="e0a0d-261">recursive</span></span> |<span data-ttu-id="e0a0d-262">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-262">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="e0a0d-263">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="e0a0d-263">True (default value), False</span></span> |<span data-ttu-id="e0a0d-264">No</span><span class="sxs-lookup"><span data-stu-id="e0a0d-264">No</span></span> |

<span data-ttu-id="e0a0d-265">**AzureDataLakeStoreSink** supports the following properties **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-265">**AzureDataLakeStoreSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="e0a0d-266">Property</span><span class="sxs-lookup"><span data-stu-id="e0a0d-266">Property</span></span> | <span data-ttu-id="e0a0d-267">Description</span><span class="sxs-lookup"><span data-stu-id="e0a0d-267">Description</span></span> | <span data-ttu-id="e0a0d-268">Allowed values</span><span class="sxs-lookup"><span data-stu-id="e0a0d-268">Allowed values</span></span> | <span data-ttu-id="e0a0d-269">Required</span><span class="sxs-lookup"><span data-stu-id="e0a0d-269">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e0a0d-270">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e0a0d-270">copyBehavior</span></span> |<span data-ttu-id="e0a0d-271">Specifies the copy behavior.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-271">Specifies the copy behavior.</span></span> |<span data-ttu-id="e0a0d-272"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-272"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="e0a0d-273">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-273">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="e0a0d-274"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-274"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="e0a0d-275">The target files are created with auto generated name.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-275">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="e0a0d-276"><b>MergeFiles</b>: merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-276"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="e0a0d-277">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-277">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="e0a0d-278">No</span><span class="sxs-lookup"><span data-stu-id="e0a0d-278">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="e0a0d-279">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="e0a0d-279">Supported file and compression formats</span></span>
<span data-ttu-id="e0a0d-280">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-280">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="e0a0d-281">JSON examples</span><span class="sxs-lookup"><span data-stu-id="e0a0d-281">JSON examples</span></span>
<span data-ttu-id="e0a0d-282">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-282">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e0a0d-283">They show how to copy data to and from Azure Data Lake Store and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-283">They show how to copy data to and from Azure Data Lake Store and Azure Blob Storage.</span></span> <span data-ttu-id="e0a0d-284">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-284">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="e0a0d-285">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-285">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>  
## <a name="example-copy-data-from-azure-blob-to-azure-data-lake-store"></a><span data-ttu-id="e0a0d-286">Example: Copy data from Azure Blob to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e0a0d-286">Example: Copy data from Azure Blob to Azure Data Lake Store</span></span>
<span data-ttu-id="e0a0d-287">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-287">The following sample shows:</span></span>

1. <span data-ttu-id="e0a0d-288">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-288">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e0a0d-289">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-289">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
3. <span data-ttu-id="e0a0d-290">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-290">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e0a0d-291">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-291">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
5. <span data-ttu-id="e0a0d-292">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-292">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="e0a0d-293">The sample copies time-series data from an Azure Blob Storage to Azure Data Lake Store every hour.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-293">The sample copies time-series data from an Azure Blob Storage to Azure Data Lake Store every hour.</span></span> <span data-ttu-id="e0a0d-294">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-294">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e0a0d-295">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-295">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="e0a0d-296">**Azure Data Lake Store linked service**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-296">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="e0a0d-297">See the steps in [Azure Data Lake Store Linked Service properties](#linked-service-properties) section with configuration details.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-297">See the steps in [Azure Data Lake Store Linked Service properties](#linked-service-properties) section with configuration details.</span></span>
>

<span data-ttu-id="e0a0d-298">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-298">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="e0a0d-299">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-299">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e0a0d-300">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-300">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e0a0d-301">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-301">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="e0a0d-302">“external”: “true” setting informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-302">“external”: “true” setting informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="e0a0d-303">**Azure Data Lake Store output dataset:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-303">**Azure Data Lake Store output dataset:**</span></span>

<span data-ttu-id="e0a0d-304">The sample copies data to an Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-304">The sample copies data to an Azure Data Lake store.</span></span> <span data-ttu-id="e0a0d-305">New data is copies to Data Lake store every hour.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-305">New data is copies to Data Lake store every hour.</span></span>

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


<span data-ttu-id="e0a0d-306">**A copy activity in a pipeline with Blob source and Azure Data Lake Store sink:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-306">**A copy activity in a pipeline with Blob source and Azure Data Lake Store sink:**</span></span>

<span data-ttu-id="e0a0d-307">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-307">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="e0a0d-308">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureDataLakeStoreSink**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-308">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureDataLakeStoreSink**.</span></span>

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

## <a name="example-copy-data-from-azure-data-lake-store-to-azure-blob"></a><span data-ttu-id="e0a0d-309">Example: Copy data from Azure Data Lake Store to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e0a0d-309">Example: Copy data from Azure Data Lake Store to Azure Blob</span></span>
<span data-ttu-id="e0a0d-310">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="e0a0d-310">The following sample shows:</span></span>

1. <span data-ttu-id="e0a0d-311">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-311">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
2. <span data-ttu-id="e0a0d-312">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-312">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e0a0d-313">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-313">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
4. <span data-ttu-id="e0a0d-314">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-314">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e0a0d-315">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="e0a0d-315">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="e0a0d-316">The sample copies time-series data from an Azure Data Lake store to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-316">The sample copies time-series data from an Azure Data Lake store to an Azure blob every hour.</span></span> <span data-ttu-id="e0a0d-317">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-317">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e0a0d-318">**Azure Data Lake Store linked service:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-318">**Azure Data Lake Store linked service:**</span></span>

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
> <span data-ttu-id="e0a0d-319">See the steps in [Azure Data Lake Store Linked Service properties](#linked-service-properties) section with configuration details.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-319">See the steps in [Azure Data Lake Store Linked Service properties](#linked-service-properties) section with configuration details.</span></span>
>

<span data-ttu-id="e0a0d-320">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-320">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="e0a0d-321">**Azure Data Lake input dataset:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-321">**Azure Data Lake input dataset:**</span></span>

<span data-ttu-id="e0a0d-322">Setting **"external": true** informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-322">Setting **"external": true** informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="e0a0d-323">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-323">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e0a0d-324">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-324">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e0a0d-325">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-325">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e0a0d-326">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-326">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="e0a0d-327">**A copy activity in a pipeline with Azure Data Lake Store source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="e0a0d-327">**A copy activity in a pipeline with Azure Data Lake Store source and Blob sink:**</span></span>

<span data-ttu-id="e0a0d-328">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-328">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="e0a0d-329">In the pipeline JSON definition, the **source** type is set to **AzureDataLakeStoreSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-329">In the pipeline JSON definition, the **source** type is set to **AzureDataLakeStoreSource** and **sink** type is set to **BlobSink**.</span></span>

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

<span data-ttu-id="e0a0d-330">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-330">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="e0a0d-331">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0d-331">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e0a0d-332">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="e0a0d-332">Performance and Tuning</span></span>
<span data-ttu-id="e0a0d-333">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="e0a0d-333">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
