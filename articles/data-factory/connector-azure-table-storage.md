---
title: Copy data to and from Azure Table storage by using Data Factory | Microsoft Docs
description: Learn how to copy data from supported source stores to Azure Table storage, or from Table storage to supported sink stores, by using Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/17/2018
ms.author: jingwang
ms.openlocfilehash: 0399836191050996ac3eaf0fbe59496e10e2b426
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866223"
---
# <a name="copy-data-to-and-from-azure-table-storage-by-using-azure-data-factory"></a><span data-ttu-id="0f59a-103">Copy data to and from Azure Table storage by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0f59a-103">Copy data to and from Azure Table storage by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-azure-table-connector.md)
> * [Current version](connector-azure-table-storage.md)

<span data-ttu-id="0f59a-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data to and from Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0f59a-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data to and from Azure Table storage.</span></span> <span data-ttu-id="0f59a-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="0f59a-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="0f59a-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="0f59a-108">Supported capabilities</span></span>

<span data-ttu-id="0f59a-109">You can copy data from any supported source data store to Table storage.</span><span class="sxs-lookup"><span data-stu-id="0f59a-109">You can copy data from any supported source data store to Table storage.</span></span> <span data-ttu-id="0f59a-110">You also can copy data from Table storage to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="0f59a-110">You also can copy data from Table storage to any supported sink data store.</span></span> <span data-ttu-id="0f59a-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="0f59a-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="0f59a-112">Specifically, this Azure Table connector supports copying data by using account key and service shared access signature authentications.</span><span class="sxs-lookup"><span data-stu-id="0f59a-112">Specifically, this Azure Table connector supports copying data by using account key and service shared access signature authentications.</span></span>

## <a name="get-started"></a><span data-ttu-id="0f59a-113">Get started</span><span class="sxs-lookup"><span data-stu-id="0f59a-113">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="0f59a-114">The following sections provide details about properties that are used to define Data Factory entities specific to Table storage.</span><span class="sxs-lookup"><span data-stu-id="0f59a-114">The following sections provide details about properties that are used to define Data Factory entities specific to Table storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0f59a-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="0f59a-115">Linked service properties</span></span>

### <a name="use-an-account-key"></a><span data-ttu-id="0f59a-116">Use an account key</span><span class="sxs-lookup"><span data-stu-id="0f59a-116">Use an account key</span></span>

<span data-ttu-id="0f59a-117">You can create an Azure Storage linked service by using the account key.</span><span class="sxs-lookup"><span data-stu-id="0f59a-117">You can create an Azure Storage linked service by using the account key.</span></span> <span data-ttu-id="0f59a-118">It provides the data factory with global access to Storage.</span><span class="sxs-lookup"><span data-stu-id="0f59a-118">It provides the data factory with global access to Storage.</span></span> <span data-ttu-id="0f59a-119">The following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="0f59a-119">The following properties are supported.</span></span>

| <span data-ttu-id="0f59a-120">Property</span><span class="sxs-lookup"><span data-stu-id="0f59a-120">Property</span></span> | <span data-ttu-id="0f59a-121">Description</span><span class="sxs-lookup"><span data-stu-id="0f59a-121">Description</span></span> | <span data-ttu-id="0f59a-122">Required</span><span class="sxs-lookup"><span data-stu-id="0f59a-122">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0f59a-123">type</span><span class="sxs-lookup"><span data-stu-id="0f59a-123">type</span></span> | <span data-ttu-id="0f59a-124">The type property must be set to **AzureTableStorage**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-124">The type property must be set to **AzureTableStorage**.</span></span> |<span data-ttu-id="0f59a-125">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-125">Yes</span></span> |
| <span data-ttu-id="0f59a-126">connectionString</span><span class="sxs-lookup"><span data-stu-id="0f59a-126">connectionString</span></span> | <span data-ttu-id="0f59a-127">Specify the information needed to connect to Storage for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="0f59a-127">Specify the information needed to connect to Storage for the connectionString property.</span></span> <span data-ttu-id="0f59a-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="0f59a-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="0f59a-129">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-129">Yes</span></span> |
| <span data-ttu-id="0f59a-130">connectVia</span><span class="sxs-lookup"><span data-stu-id="0f59a-130">connectVia</span></span> | <span data-ttu-id="0f59a-131">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="0f59a-131">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="0f59a-132">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in a private network).</span><span class="sxs-lookup"><span data-stu-id="0f59a-132">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in a private network).</span></span> <span data-ttu-id="0f59a-133">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="0f59a-133">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="0f59a-134">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-134">No</span></span> |

>[!NOTE]
>If you were using "AzureStorage" type linked service, it is still supported as-is, while you are suggested to use this new "AzureTableStorage" linked service type going forward.

<span data-ttu-id="0f59a-136">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0f59a-136">**Example:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureTableStorage",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="use-shared-access-signature-authentication"></a><span data-ttu-id="0f59a-137">Use shared access signature authentication</span><span class="sxs-lookup"><span data-stu-id="0f59a-137">Use shared access signature authentication</span></span>

<span data-ttu-id="0f59a-138">You also can create a Storage linked service by using a shared access signature.</span><span class="sxs-lookup"><span data-stu-id="0f59a-138">You also can create a Storage linked service by using a shared access signature.</span></span> <span data-ttu-id="0f59a-139">It provides the data factory with restricted/time-bound access to all/specific resources in the storage.</span><span class="sxs-lookup"><span data-stu-id="0f59a-139">It provides the data factory with restricted/time-bound access to all/specific resources in the storage.</span></span>

<span data-ttu-id="0f59a-140">A shared access signature provides delegated access to resources in your storage account.</span><span class="sxs-lookup"><span data-stu-id="0f59a-140">A shared access signature provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="0f59a-141">You can use it to grant a client limited permissions to objects in your storage account for a specified time and with a specified set of permissions.</span><span class="sxs-lookup"><span data-stu-id="0f59a-141">You can use it to grant a client limited permissions to objects in your storage account for a specified time and with a specified set of permissions.</span></span> <span data-ttu-id="0f59a-142">You don't have to share your account access keys.</span><span class="sxs-lookup"><span data-stu-id="0f59a-142">You don't have to share your account access keys.</span></span> <span data-ttu-id="0f59a-143">The shared access signature is a URI that encompasses in its query parameters all the information necessary for authenticated access to a storage resource.</span><span class="sxs-lookup"><span data-stu-id="0f59a-143">The shared access signature is a URI that encompasses in its query parameters all the information necessary for authenticated access to a storage resource.</span></span> <span data-ttu-id="0f59a-144">To access storage resources with the shared access signature, the client only needs to pass in the shared access signature to the appropriate constructor or method.</span><span class="sxs-lookup"><span data-stu-id="0f59a-144">To access storage resources with the shared access signature, the client only needs to pass in the shared access signature to the appropriate constructor or method.</span></span> <span data-ttu-id="0f59a-145">For more information about shared access signatures, see [Shared access signatures: Understand the shared access signature model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="0f59a-145">For more information about shared access signatures, see [Shared access signatures: Understand the shared access signature model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

> [!NOTE]
> Data Factory now supports both **service shared access signatures** and **account shared access signatures**. For more information about these two types and how to construct them, see [Types of shared access signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures). 

> [!TIP]
> To generate a service shared access signature for your storage account, you can execute the following PowerShell commands. Replace the placeholders and grant the needed permission.
> `$context = New-AzureStorageContext -StorageAccountName <accountName> -StorageAccountKey <accountKey>`
> `New-AzureStorageContainerSASToken -Name <containerName> -Context $context -Permission rwdl -StartTime <startTime> -ExpiryTime <endTime> -FullUri`

<span data-ttu-id="0f59a-150">To use shared access signature authentication, the following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="0f59a-150">To use shared access signature authentication, the following properties are supported.</span></span>

| <span data-ttu-id="0f59a-151">Property</span><span class="sxs-lookup"><span data-stu-id="0f59a-151">Property</span></span> | <span data-ttu-id="0f59a-152">Description</span><span class="sxs-lookup"><span data-stu-id="0f59a-152">Description</span></span> | <span data-ttu-id="0f59a-153">Required</span><span class="sxs-lookup"><span data-stu-id="0f59a-153">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0f59a-154">type</span><span class="sxs-lookup"><span data-stu-id="0f59a-154">type</span></span> | <span data-ttu-id="0f59a-155">The type property must be set to **AzureTableStorage**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-155">The type property must be set to **AzureTableStorage**.</span></span> |<span data-ttu-id="0f59a-156">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-156">Yes</span></span> |
| <span data-ttu-id="0f59a-157">sasUri</span><span class="sxs-lookup"><span data-stu-id="0f59a-157">sasUri</span></span> | <span data-ttu-id="0f59a-158">Specify the shared access signature URI to the Storage resources, such as blob, container, or table.</span><span class="sxs-lookup"><span data-stu-id="0f59a-158">Specify the shared access signature URI to the Storage resources, such as blob, container, or table.</span></span> <span data-ttu-id="0f59a-159">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="0f59a-159">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="0f59a-160">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-160">Yes</span></span> |
| <span data-ttu-id="0f59a-161">connectVia</span><span class="sxs-lookup"><span data-stu-id="0f59a-161">connectVia</span></span> | <span data-ttu-id="0f59a-162">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="0f59a-162">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="0f59a-163">You can use the Azure Integration Runtime or the Self-hosted Integration Runtime (if your data store is located in a private network).</span><span class="sxs-lookup"><span data-stu-id="0f59a-163">You can use the Azure Integration Runtime or the Self-hosted Integration Runtime (if your data store is located in a private network).</span></span> <span data-ttu-id="0f59a-164">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="0f59a-164">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="0f59a-165">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-165">No</span></span> |

>[!NOTE]
>If you were using "AzureStorage" type linked service, it is still supported as-is, while you are suggested to use this new "AzureTableStorage" linked service type going forward.

<span data-ttu-id="0f59a-167">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0f59a-167">**Example:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureTableStorage",
        "typeProperties": {
            "sasUri": {
                "type": "SecureString",
                "value": "<SAS URI of the Azure Storage resource>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="0f59a-168">When you create a shared access signature URI, consider the following points:</span><span class="sxs-lookup"><span data-stu-id="0f59a-168">When you create a shared access signature URI, consider the following points:</span></span>

- <span data-ttu-id="0f59a-169">Set appropriate read/write permissions on objects based on how the linked service (read, write, read/write) is used in your data factory.</span><span class="sxs-lookup"><span data-stu-id="0f59a-169">Set appropriate read/write permissions on objects based on how the linked service (read, write, read/write) is used in your data factory.</span></span>
- <span data-ttu-id="0f59a-170">Set **Expiry time** appropriately.</span><span class="sxs-lookup"><span data-stu-id="0f59a-170">Set **Expiry time** appropriately.</span></span> <span data-ttu-id="0f59a-171">Make sure that the access to Storage objects doesn't expire within the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f59a-171">Make sure that the access to Storage objects doesn't expire within the active period of the pipeline.</span></span>
- <span data-ttu-id="0f59a-172">The URI should be created at the right table level based on the need.</span><span class="sxs-lookup"><span data-stu-id="0f59a-172">The URI should be created at the right table level based on the need.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="0f59a-173">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="0f59a-173">Dataset properties</span></span>

<span data-ttu-id="0f59a-174">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="0f59a-174">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="0f59a-175">This section provides a list of properties supported by the Azure Table dataset.</span><span class="sxs-lookup"><span data-stu-id="0f59a-175">This section provides a list of properties supported by the Azure Table dataset.</span></span>

<span data-ttu-id="0f59a-176">To copy data to and from Azure Table, set the type property of the dataset to **AzureTable**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-176">To copy data to and from Azure Table, set the type property of the dataset to **AzureTable**.</span></span> <span data-ttu-id="0f59a-177">The following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="0f59a-177">The following properties are supported.</span></span>

| <span data-ttu-id="0f59a-178">Property</span><span class="sxs-lookup"><span data-stu-id="0f59a-178">Property</span></span> | <span data-ttu-id="0f59a-179">Description</span><span class="sxs-lookup"><span data-stu-id="0f59a-179">Description</span></span> | <span data-ttu-id="0f59a-180">Required</span><span class="sxs-lookup"><span data-stu-id="0f59a-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0f59a-181">type</span><span class="sxs-lookup"><span data-stu-id="0f59a-181">type</span></span> | <span data-ttu-id="0f59a-182">The type property of the dataset must be set to **AzureTable**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-182">The type property of the dataset must be set to **AzureTable**.</span></span> |<span data-ttu-id="0f59a-183">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-183">Yes</span></span> |
| <span data-ttu-id="0f59a-184">tableName</span><span class="sxs-lookup"><span data-stu-id="0f59a-184">tableName</span></span> |<span data-ttu-id="0f59a-185">The name of the table in the Table storage database instance that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="0f59a-185">The name of the table in the Table storage database instance that the linked service refers to.</span></span> |<span data-ttu-id="0f59a-186">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-186">Yes</span></span> |

<span data-ttu-id="0f59a-187">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0f59a-187">**Example:**</span></span>

```json
{
    "name": "AzureTableDataset",
    "properties":
    {
        "type": "AzureTable",
        "linkedServiceName": {
            "referenceName": "<Azure Table storage linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

### <a name="schema-by-data-factory"></a><span data-ttu-id="0f59a-188">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="0f59a-188">Schema by Data Factory</span></span>

<span data-ttu-id="0f59a-189">For schema-free data stores such as Azure Table, Data Factory infers the schema in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="0f59a-189">For schema-free data stores such as Azure Table, Data Factory infers the schema in one of the following ways:</span></span>

* <span data-ttu-id="0f59a-190">If you specify the structure of data by using the **structure** property in the dataset definition, Data Factory honors this structure as the schema.</span><span class="sxs-lookup"><span data-stu-id="0f59a-190">If you specify the structure of data by using the **structure** property in the dataset definition, Data Factory honors this structure as the schema.</span></span> <span data-ttu-id="0f59a-191">In this case, if a row doesn't contain a value for a column, a null value is provided for it.</span><span class="sxs-lookup"><span data-stu-id="0f59a-191">In this case, if a row doesn't contain a value for a column, a null value is provided for it.</span></span>
* <span data-ttu-id="0f59a-192">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span><span class="sxs-lookup"><span data-stu-id="0f59a-192">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="0f59a-193">In this case, if the first row doesn't contain the full schema, some columns are missed in the result of the copy operation.</span><span class="sxs-lookup"><span data-stu-id="0f59a-193">In this case, if the first row doesn't contain the full schema, some columns are missed in the result of the copy operation.</span></span>

<span data-ttu-id="0f59a-194">For schema-free data sources, the best practice is to specify the structure of data by using the **structure** property.</span><span class="sxs-lookup"><span data-stu-id="0f59a-194">For schema-free data sources, the best practice is to specify the structure of data by using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="0f59a-195">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="0f59a-195">Copy activity properties</span></span>

<span data-ttu-id="0f59a-196">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="0f59a-196">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="0f59a-197">This section provides a list of properties supported by the Azure Table source and sink.</span><span class="sxs-lookup"><span data-stu-id="0f59a-197">This section provides a list of properties supported by the Azure Table source and sink.</span></span>

### <a name="azure-table-as-a-source-type"></a><span data-ttu-id="0f59a-198">Azure Table as a source type</span><span class="sxs-lookup"><span data-stu-id="0f59a-198">Azure Table as a source type</span></span>

<span data-ttu-id="0f59a-199">To copy data from Azure Table, set the source type in the copy activity to **AzureTableSource**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-199">To copy data from Azure Table, set the source type in the copy activity to **AzureTableSource**.</span></span> <span data-ttu-id="0f59a-200">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="0f59a-200">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="0f59a-201">Property</span><span class="sxs-lookup"><span data-stu-id="0f59a-201">Property</span></span> | <span data-ttu-id="0f59a-202">Description</span><span class="sxs-lookup"><span data-stu-id="0f59a-202">Description</span></span> | <span data-ttu-id="0f59a-203">Required</span><span class="sxs-lookup"><span data-stu-id="0f59a-203">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0f59a-204">type</span><span class="sxs-lookup"><span data-stu-id="0f59a-204">type</span></span> | <span data-ttu-id="0f59a-205">The type property of the copy activity source must be set to **AzureTableSource**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-205">The type property of the copy activity source must be set to **AzureTableSource**.</span></span> |<span data-ttu-id="0f59a-206">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-206">Yes</span></span> |
| <span data-ttu-id="0f59a-207">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="0f59a-207">azureTableSourceQuery</span></span> |<span data-ttu-id="0f59a-208">Use the custom Table storage query to read data.</span><span class="sxs-lookup"><span data-stu-id="0f59a-208">Use the custom Table storage query to read data.</span></span> <span data-ttu-id="0f59a-209">See examples in the following section.</span><span class="sxs-lookup"><span data-stu-id="0f59a-209">See examples in the following section.</span></span> |<span data-ttu-id="0f59a-210">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-210">No</span></span> |
| <span data-ttu-id="0f59a-211">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="0f59a-211">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="0f59a-212">Indicates whether to allow the exception of the table to not exist.</span><span class="sxs-lookup"><span data-stu-id="0f59a-212">Indicates whether to allow the exception of the table to not exist.</span></span><br/><span data-ttu-id="0f59a-213">Allowed values are **True** and **False** (default).</span><span class="sxs-lookup"><span data-stu-id="0f59a-213">Allowed values are **True** and **False** (default).</span></span> |<span data-ttu-id="0f59a-214">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-214">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="0f59a-215">azureTableSourceQuery examples</span><span class="sxs-lookup"><span data-stu-id="0f59a-215">azureTableSourceQuery examples</span></span>

<span data-ttu-id="0f59a-216">If the Azure Table column is of the datetime type:</span><span class="sxs-lookup"><span data-stu-id="0f59a-216">If the Azure Table column is of the datetime type:</span></span>

```json
"azureTableSourceQuery": "LastModifiedTime gt datetime'2017-10-01T00:00:00' and LastModifiedTime le datetime'2017-10-02T00:00:00'"
```

<span data-ttu-id="0f59a-217">If the Azure Table column is of the string type:</span><span class="sxs-lookup"><span data-stu-id="0f59a-217">If the Azure Table column is of the string type:</span></span>

```json
"azureTableSourceQuery": "LastModifiedTime ge '201710010000_0000' and LastModifiedTime le '201710010000_9999'"
```

<span data-ttu-id="0f59a-218">If you use the pipeline parameter, cast the datetime value to proper format according to the previous samples.</span><span class="sxs-lookup"><span data-stu-id="0f59a-218">If you use the pipeline parameter, cast the datetime value to proper format according to the previous samples.</span></span>

### <a name="azure-table-as-a-sink-type"></a><span data-ttu-id="0f59a-219">Azure Table as a sink type</span><span class="sxs-lookup"><span data-stu-id="0f59a-219">Azure Table as a sink type</span></span>

<span data-ttu-id="0f59a-220">To copy data to Azure Table, set the sink type in the copy activity to **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-220">To copy data to Azure Table, set the sink type in the copy activity to **AzureTableSink**.</span></span> <span data-ttu-id="0f59a-221">The following properties are supported in the copy activity **sink** section.</span><span class="sxs-lookup"><span data-stu-id="0f59a-221">The following properties are supported in the copy activity **sink** section.</span></span>

| <span data-ttu-id="0f59a-222">Property</span><span class="sxs-lookup"><span data-stu-id="0f59a-222">Property</span></span> | <span data-ttu-id="0f59a-223">Description</span><span class="sxs-lookup"><span data-stu-id="0f59a-223">Description</span></span> | <span data-ttu-id="0f59a-224">Required</span><span class="sxs-lookup"><span data-stu-id="0f59a-224">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0f59a-225">type</span><span class="sxs-lookup"><span data-stu-id="0f59a-225">type</span></span> | <span data-ttu-id="0f59a-226">The type property of the copy activity sink must be set to **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-226">The type property of the copy activity sink must be set to **AzureTableSink**.</span></span> |<span data-ttu-id="0f59a-227">Yes</span><span class="sxs-lookup"><span data-stu-id="0f59a-227">Yes</span></span> |
| <span data-ttu-id="0f59a-228">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="0f59a-228">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="0f59a-229">The default partition key value that can be used by the sink.</span><span class="sxs-lookup"><span data-stu-id="0f59a-229">The default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="0f59a-230">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-230">No</span></span> |
| <span data-ttu-id="0f59a-231">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="0f59a-231">azureTablePartitionKeyName</span></span> |<span data-ttu-id="0f59a-232">Specify the name of the column whose values are used as partition keys.</span><span class="sxs-lookup"><span data-stu-id="0f59a-232">Specify the name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="0f59a-233">If not specified, "AzureTableDefaultPartitionKeyValue" is used as the partition key.</span><span class="sxs-lookup"><span data-stu-id="0f59a-233">If not specified, "AzureTableDefaultPartitionKeyValue" is used as the partition key.</span></span> |<span data-ttu-id="0f59a-234">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-234">No</span></span> |
| <span data-ttu-id="0f59a-235">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="0f59a-235">azureTableRowKeyName</span></span> |<span data-ttu-id="0f59a-236">Specify the name of the column whose column values are used as the row key.</span><span class="sxs-lookup"><span data-stu-id="0f59a-236">Specify the name of the column whose column values are used as the row key.</span></span> <span data-ttu-id="0f59a-237">If not specified, use a GUID for each row.</span><span class="sxs-lookup"><span data-stu-id="0f59a-237">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="0f59a-238">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-238">No</span></span> |
| <span data-ttu-id="0f59a-239">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="0f59a-239">azureTableInsertType</span></span> |<span data-ttu-id="0f59a-240">The mode to insert data into Azure Table.</span><span class="sxs-lookup"><span data-stu-id="0f59a-240">The mode to insert data into Azure Table.</span></span> <span data-ttu-id="0f59a-241">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span><span class="sxs-lookup"><span data-stu-id="0f59a-241">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="0f59a-242">Allowed values are **merge** (default) and **replace**.</span><span class="sxs-lookup"><span data-stu-id="0f59a-242">Allowed values are **merge** (default) and **replace**.</span></span> <br/><br> <span data-ttu-id="0f59a-243">This setting applies at the row level not the table level.</span><span class="sxs-lookup"><span data-stu-id="0f59a-243">This setting applies at the row level not the table level.</span></span> <span data-ttu-id="0f59a-244">Neither option deletes rows in the output table that do not exist in the input.</span><span class="sxs-lookup"><span data-stu-id="0f59a-244">Neither option deletes rows in the output table that do not exist in the input.</span></span> <span data-ttu-id="0f59a-245">To learn about how the merge and replace settings work, see [Insert or merge entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or replace entity](https://msdn.microsoft.com/library/azure/hh452242.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f59a-245">To learn about how the merge and replace settings work, see [Insert or merge entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or replace entity](https://msdn.microsoft.com/library/azure/hh452242.aspx).</span></span> |<span data-ttu-id="0f59a-246">No</span><span class="sxs-lookup"><span data-stu-id="0f59a-246">No</span></span> |
| <span data-ttu-id="0f59a-247">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0f59a-247">writeBatchSize</span></span> |<span data-ttu-id="0f59a-248">Inserts data into Azure Table when writeBatchSize or writeBatchTimeout is hit.</span><span class="sxs-lookup"><span data-stu-id="0f59a-248">Inserts data into Azure Table when writeBatchSize or writeBatchTimeout is hit.</span></span><br/><span data-ttu-id="0f59a-249">Allowed values are integer (number of rows).</span><span class="sxs-lookup"><span data-stu-id="0f59a-249">Allowed values are integer (number of rows).</span></span> |<span data-ttu-id="0f59a-250">No (default is 10,000)</span><span class="sxs-lookup"><span data-stu-id="0f59a-250">No (default is 10,000)</span></span> |
| <span data-ttu-id="0f59a-251">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0f59a-251">writeBatchTimeout</span></span> |<span data-ttu-id="0f59a-252">Inserts data into Azure Table when writeBatchSize or writeBatchTimeout is hit.</span><span class="sxs-lookup"><span data-stu-id="0f59a-252">Inserts data into Azure Table when writeBatchSize or writeBatchTimeout is hit.</span></span><br/><span data-ttu-id="0f59a-253">Allowed values are timespan.</span><span class="sxs-lookup"><span data-stu-id="0f59a-253">Allowed values are timespan.</span></span> <span data-ttu-id="0f59a-254">An example is "00:20:00" (20 minutes).</span><span class="sxs-lookup"><span data-stu-id="0f59a-254">An example is "00:20:00" (20 minutes).</span></span> |<span data-ttu-id="0f59a-255">No (default is 90 seconds, storage client's default timeout)</span><span class="sxs-lookup"><span data-stu-id="0f59a-255">No (default is 90 seconds, storage client's default timeout)</span></span> |

<span data-ttu-id="0f59a-256">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0f59a-256">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToAzureTable",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure Table output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "AzureTableSink",
                "azureTablePartitionKeyName": "<column name>",
                "azureTableRowKeyName": "<column name>"
            }
        }
    }
]
```

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="0f59a-257">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="0f59a-257">azureTablePartitionKeyName</span></span>

<span data-ttu-id="0f59a-258">Map a source column to a destination column by using the **"translator"** property before you can use the destination column as azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="0f59a-258">Map a source column to a destination column by using the **"translator"** property before you can use the destination column as azureTablePartitionKeyName.</span></span>

<span data-ttu-id="0f59a-259">In the following example, source column DivisionID is mapped to the destination column DivisionID:</span><span class="sxs-lookup"><span data-stu-id="0f59a-259">In the following example, source column DivisionID is mapped to the destination column DivisionID:</span></span>

```json
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```

<span data-ttu-id="0f59a-260">"DivisionID" is specified as the partition key.</span><span class="sxs-lookup"><span data-stu-id="0f59a-260">"DivisionID" is specified as the partition key.</span></span>

```json
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID"
}
```

## <a name="data-type-mapping-for-azure-table"></a><span data-ttu-id="0f59a-261">Data type mapping for Azure Table</span><span class="sxs-lookup"><span data-stu-id="0f59a-261">Data type mapping for Azure Table</span></span>

<span data-ttu-id="0f59a-262">When you copy data from and to Azure Table, the following mappings are used from Azure Table data types to Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="0f59a-262">When you copy data from and to Azure Table, the following mappings are used from Azure Table data types to Data Factory interim data types.</span></span> <span data-ttu-id="0f59a-263">To learn about how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="0f59a-263">To learn about how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span></span>

<span data-ttu-id="0f59a-264">When you move data to and from Azure Table, the following [mappings defined by Azure Table](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="0f59a-264">When you move data to and from Azure Table, the following [mappings defined by Azure Table](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="0f59a-265">Azure Table data type</span><span class="sxs-lookup"><span data-stu-id="0f59a-265">Azure Table data type</span></span> | <span data-ttu-id="0f59a-266">Data Factory interim data type</span><span class="sxs-lookup"><span data-stu-id="0f59a-266">Data Factory interim data type</span></span> | <span data-ttu-id="0f59a-267">Details</span><span class="sxs-lookup"><span data-stu-id="0f59a-267">Details</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0f59a-268">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="0f59a-268">Edm.Binary</span></span> |<span data-ttu-id="0f59a-269">byte[]</span><span class="sxs-lookup"><span data-stu-id="0f59a-269">byte[]</span></span> |<span data-ttu-id="0f59a-270">An array of bytes up to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="0f59a-270">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="0f59a-271">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="0f59a-271">Edm.Boolean</span></span> |<span data-ttu-id="0f59a-272">bool</span><span class="sxs-lookup"><span data-stu-id="0f59a-272">bool</span></span> |<span data-ttu-id="0f59a-273">A Boolean value.</span><span class="sxs-lookup"><span data-stu-id="0f59a-273">A Boolean value.</span></span> |
| <span data-ttu-id="0f59a-274">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="0f59a-274">Edm.DateTime</span></span> |<span data-ttu-id="0f59a-275">DateTime</span><span class="sxs-lookup"><span data-stu-id="0f59a-275">DateTime</span></span> |<span data-ttu-id="0f59a-276">A 64-bit value expressed as Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="0f59a-276">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="0f59a-277">The supported DateTime range begins midnight, January 1, 1601 A.D.</span><span class="sxs-lookup"><span data-stu-id="0f59a-277">The supported DateTime range begins midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="0f59a-278">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="0f59a-278">(C.E.), UTC.</span></span> <span data-ttu-id="0f59a-279">The range ends December 31, 9999.</span><span class="sxs-lookup"><span data-stu-id="0f59a-279">The range ends December 31, 9999.</span></span> |
| <span data-ttu-id="0f59a-280">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="0f59a-280">Edm.Double</span></span> |<span data-ttu-id="0f59a-281">double</span><span class="sxs-lookup"><span data-stu-id="0f59a-281">double</span></span> |<span data-ttu-id="0f59a-282">A 64-bit floating point value.</span><span class="sxs-lookup"><span data-stu-id="0f59a-282">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="0f59a-283">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="0f59a-283">Edm.Guid</span></span> |<span data-ttu-id="0f59a-284">Guid</span><span class="sxs-lookup"><span data-stu-id="0f59a-284">Guid</span></span> |<span data-ttu-id="0f59a-285">A 128-bit globally unique identifier.</span><span class="sxs-lookup"><span data-stu-id="0f59a-285">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="0f59a-286">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="0f59a-286">Edm.Int32</span></span> |<span data-ttu-id="0f59a-287">Int32</span><span class="sxs-lookup"><span data-stu-id="0f59a-287">Int32</span></span> |<span data-ttu-id="0f59a-288">A 32-bit integer.</span><span class="sxs-lookup"><span data-stu-id="0f59a-288">A 32-bit integer.</span></span> |
| <span data-ttu-id="0f59a-289">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="0f59a-289">Edm.Int64</span></span> |<span data-ttu-id="0f59a-290">Int64</span><span class="sxs-lookup"><span data-stu-id="0f59a-290">Int64</span></span> |<span data-ttu-id="0f59a-291">A 64-bit integer.</span><span class="sxs-lookup"><span data-stu-id="0f59a-291">A 64-bit integer.</span></span> |
| <span data-ttu-id="0f59a-292">Edm.String</span><span class="sxs-lookup"><span data-stu-id="0f59a-292">Edm.String</span></span> |<span data-ttu-id="0f59a-293">String</span><span class="sxs-lookup"><span data-stu-id="0f59a-293">String</span></span> |<span data-ttu-id="0f59a-294">A UTF-16-encoded value.</span><span class="sxs-lookup"><span data-stu-id="0f59a-294">A UTF-16-encoded value.</span></span> <span data-ttu-id="0f59a-295">String values can be up to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="0f59a-295">String values can be up to 64 KB.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f59a-296">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f59a-296">Next steps</span></span>
<span data-ttu-id="0f59a-297">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0f59a-297">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
