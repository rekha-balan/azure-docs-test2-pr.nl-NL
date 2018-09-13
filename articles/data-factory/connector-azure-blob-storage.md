---
title: Copy data to or from Azure Blob storage by using Data Factory | Microsoft Docs
description: Learn how to copy data from supported source data stores to Azure Blob storage, or from Blob storage to supported sink data stores, by using Data Factory.
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 08/17/2018
ms.author: jingwang
ms.openlocfilehash: 46e12378812788d147c903046b50a93c13119f2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856175"
---
# <a name="copy-data-to-or-from-azure-blob-storage-by-using-azure-data-factory"></a><span data-ttu-id="d3252-103">Copy data to or from Azure Blob storage by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d3252-103">Copy data to or from Azure Blob storage by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-azure-blob-connector.md)
> * [Current version](connector-azure-blob-storage.md)

<span data-ttu-id="d3252-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data to and from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data to and from Azure Blob storage.</span></span> <span data-ttu-id="d3252-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="d3252-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="d3252-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="d3252-108">Supported capabilities</span></span>

<span data-ttu-id="d3252-109">You can copy data from any supported source data store to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-109">You can copy data from any supported source data store to Blob storage.</span></span> <span data-ttu-id="d3252-110">You also can copy data from Blob storage to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="d3252-110">You also can copy data from Blob storage to any supported sink data store.</span></span> <span data-ttu-id="d3252-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md) table.</span><span class="sxs-lookup"><span data-stu-id="d3252-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md) table.</span></span>

<span data-ttu-id="d3252-112">Specifically, this Blob storage connector supports:</span><span class="sxs-lookup"><span data-stu-id="d3252-112">Specifically, this Blob storage connector supports:</span></span>

- <span data-ttu-id="d3252-113">Copying blobs to and from general-purpose Azure storage accounts and hot/cool blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-113">Copying blobs to and from general-purpose Azure storage accounts and hot/cool blob storage.</span></span> 
- <span data-ttu-id="d3252-114">Copying blobs by using account key, service shared access signature, service principal or managed service identity authentications.</span><span class="sxs-lookup"><span data-stu-id="d3252-114">Copying blobs by using account key, service shared access signature, service principal or managed service identity authentications.</span></span>
- <span data-ttu-id="d3252-115">Copying blobs from block, append, or page blobs and copying data to only block blobs.</span><span class="sxs-lookup"><span data-stu-id="d3252-115">Copying blobs from block, append, or page blobs and copying data to only block blobs.</span></span> <span data-ttu-id="d3252-116">Azure Premium Storage isn't supported as a sink because it's backed by page blobs.</span><span class="sxs-lookup"><span data-stu-id="d3252-116">Azure Premium Storage isn't supported as a sink because it's backed by page blobs.</span></span>
- <span data-ttu-id="d3252-117">Copying blobs as is or parsing or generating blobs with [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-117">Copying blobs as is or parsing or generating blobs with [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="d3252-118">Get started</span><span class="sxs-lookup"><span data-stu-id="d3252-118">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="d3252-119">The following sections provide details about properties that are used to define Data Factory entities specific to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-119">The following sections provide details about properties that are used to define Data Factory entities specific to Blob storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d3252-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="d3252-120">Linked service properties</span></span>

<span data-ttu-id="d3252-121">Azure Blob connector support the following authentication types, refer to the corresponding section on details:</span><span class="sxs-lookup"><span data-stu-id="d3252-121">Azure Blob connector support the following authentication types, refer to the corresponding section on details:</span></span>

- [<span data-ttu-id="d3252-122">Account key authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-122">Account key authentication</span></span>](#account-key-authentication)
- [<span data-ttu-id="d3252-123">Shared access signature authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-123">Shared access signature authentication</span></span>](#shared-access-signature-authentication)
- [<span data-ttu-id="d3252-124">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-124">Service principal authentication</span></span>](#service-principal-authentication)
- [<span data-ttu-id="d3252-125">Managed service identity authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-125">Managed service identity authentication</span></span>](#managed-service-identity-authentication)

>[!NOTE]
>HDInsights, Azure Machine Learning and Azure SQL Data Warehouse PolyBase load only support Azure Blob storage account key authentication.

### <a name="account-key-authentication"></a><span data-ttu-id="d3252-127">Account key authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-127">Account key authentication</span></span>

<span data-ttu-id="d3252-128">To use storage account key authentication, the following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="d3252-128">To use storage account key authentication, the following properties are supported:</span></span>

| <span data-ttu-id="d3252-129">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-129">Property</span></span> | <span data-ttu-id="d3252-130">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-130">Description</span></span> | <span data-ttu-id="d3252-131">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-131">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-132">type</span><span class="sxs-lookup"><span data-stu-id="d3252-132">type</span></span> | <span data-ttu-id="d3252-133">The type property must be set to **AzureBlobStorage** (suggested) or **AzureStorage** (see notes below).</span><span class="sxs-lookup"><span data-stu-id="d3252-133">The type property must be set to **AzureBlobStorage** (suggested) or **AzureStorage** (see notes below).</span></span> |<span data-ttu-id="d3252-134">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-134">Yes</span></span> |
| <span data-ttu-id="d3252-135">connectionString</span><span class="sxs-lookup"><span data-stu-id="d3252-135">connectionString</span></span> | <span data-ttu-id="d3252-136">Specify the information needed to connect to Storage for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="d3252-136">Specify the information needed to connect to Storage for the connectionString property.</span></span> <span data-ttu-id="d3252-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="d3252-138">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-138">Yes</span></span> |
| <span data-ttu-id="d3252-139">connectVia</span><span class="sxs-lookup"><span data-stu-id="d3252-139">connectVia</span></span> | <span data-ttu-id="d3252-140">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d3252-140">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d3252-141">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is in a private network).</span><span class="sxs-lookup"><span data-stu-id="d3252-141">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is in a private network).</span></span> <span data-ttu-id="d3252-142">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d3252-142">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d3252-143">No</span><span class="sxs-lookup"><span data-stu-id="d3252-143">No</span></span> |

>[!NOTE]
>If you were using "AzureStorage" type linked service, it is still supported as-is, while you are suggested to use this new "AzureBlobStorage" linked service type going forward.

<span data-ttu-id="d3252-145">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-145">**Example:**</span></span>

```json
{
    "name": "AzureBlobStorageLinkedService",
    "properties": {
        "type": "AzureBlobStorage",
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

### <a name="shared-access-signature-authentication"></a><span data-ttu-id="d3252-146">Shared access signature authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-146">Shared access signature authentication</span></span>

<span data-ttu-id="d3252-147">A shared access signature provides delegated access to resources in your storage account.</span><span class="sxs-lookup"><span data-stu-id="d3252-147">A shared access signature provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="d3252-148">You can use a shared access signature to grant a client limited permissions to objects in your storage account for a specified time.</span><span class="sxs-lookup"><span data-stu-id="d3252-148">You can use a shared access signature to grant a client limited permissions to objects in your storage account for a specified time.</span></span> <span data-ttu-id="d3252-149">You don't have to share your account access keys.</span><span class="sxs-lookup"><span data-stu-id="d3252-149">You don't have to share your account access keys.</span></span> <span data-ttu-id="d3252-150">The shared access signature is a URI that encompasses in its query parameters all the information necessary for authenticated access to a storage resource.</span><span class="sxs-lookup"><span data-stu-id="d3252-150">The shared access signature is a URI that encompasses in its query parameters all the information necessary for authenticated access to a storage resource.</span></span> <span data-ttu-id="d3252-151">To access storage resources with the shared access signature, the client only needs to pass in the shared access signature to the appropriate constructor or method.</span><span class="sxs-lookup"><span data-stu-id="d3252-151">To access storage resources with the shared access signature, the client only needs to pass in the shared access signature to the appropriate constructor or method.</span></span> <span data-ttu-id="d3252-152">For more information about shared access signatures, see [Shared access signatures: Understand the shared access signature model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-152">For more information about shared access signatures, see [Shared access signatures: Understand the shared access signature model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

> [!NOTE]
> Data Factory now supports both **service shared access signatures** and **account shared access signatures**. For more information about these two types and how to construct them, see [Types of shared access signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures). 

> [!TIP]
> To generate a service shared access signature for your storage account, you can execute the following PowerShell commands. Replace the placeholders and grant the needed permission.
> `$context = New-AzureStorageContext -StorageAccountName <accountName> -StorageAccountKey <accountKey>`
> `New-AzureStorageContainerSASToken -Name <containerName> -Context $context -Permission rwdl -StartTime <startTime> -ExpiryTime <endTime> -FullUri`

<span data-ttu-id="d3252-157">To use shared access signature authentication, the following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="d3252-157">To use shared access signature authentication, the following properties are supported:</span></span>

| <span data-ttu-id="d3252-158">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-158">Property</span></span> | <span data-ttu-id="d3252-159">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-159">Description</span></span> | <span data-ttu-id="d3252-160">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-160">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-161">type</span><span class="sxs-lookup"><span data-stu-id="d3252-161">type</span></span> | <span data-ttu-id="d3252-162">The type property must be set to **AzureBlobStorage** (suggested) or **AzureStorage** (see notes below).</span><span class="sxs-lookup"><span data-stu-id="d3252-162">The type property must be set to **AzureBlobStorage** (suggested) or **AzureStorage** (see notes below).</span></span> |<span data-ttu-id="d3252-163">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-163">Yes</span></span> |
| <span data-ttu-id="d3252-164">sasUri</span><span class="sxs-lookup"><span data-stu-id="d3252-164">sasUri</span></span> | <span data-ttu-id="d3252-165">Specify the shared access signature URI to the Storage resources, such as blob, container, or table.</span><span class="sxs-lookup"><span data-stu-id="d3252-165">Specify the shared access signature URI to the Storage resources, such as blob, container, or table.</span></span> <span data-ttu-id="d3252-166">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-166">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="d3252-167">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-167">Yes</span></span> |
| <span data-ttu-id="d3252-168">connectVia</span><span class="sxs-lookup"><span data-stu-id="d3252-168">connectVia</span></span> | <span data-ttu-id="d3252-169">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d3252-169">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d3252-170">You can use the Azure Integration Runtime or the Self-hosted Integration Runtime (if your data store is located in a private network).</span><span class="sxs-lookup"><span data-stu-id="d3252-170">You can use the Azure Integration Runtime or the Self-hosted Integration Runtime (if your data store is located in a private network).</span></span> <span data-ttu-id="d3252-171">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d3252-171">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d3252-172">No</span><span class="sxs-lookup"><span data-stu-id="d3252-172">No</span></span> |

>[!NOTE]
>If you were using "AzureStorage" type linked service, it is still supported as-is, while you are suggested to use this new "AzureBlobStorage" linked service type going forward.

<span data-ttu-id="d3252-174">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-174">**Example:**</span></span>

```json
{
    "name": "AzureBlobStorageLinkedService",
    "properties": {
        "type": "AzureBlobStorage",
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

<span data-ttu-id="d3252-175">When you create a shared access signature URI, consider the following points:</span><span class="sxs-lookup"><span data-stu-id="d3252-175">When you create a shared access signature URI, consider the following points:</span></span>

- <span data-ttu-id="d3252-176">Set appropriate read/write permissions on objects based on how the linked service (read, write, read/write) is used in your data factory.</span><span class="sxs-lookup"><span data-stu-id="d3252-176">Set appropriate read/write permissions on objects based on how the linked service (read, write, read/write) is used in your data factory.</span></span>
- <span data-ttu-id="d3252-177">Set **Expiry time** appropriately.</span><span class="sxs-lookup"><span data-stu-id="d3252-177">Set **Expiry time** appropriately.</span></span> <span data-ttu-id="d3252-178">Make sure that the access to Storage objects doesn't expire within the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3252-178">Make sure that the access to Storage objects doesn't expire within the active period of the pipeline.</span></span>
- <span data-ttu-id="d3252-179">The URI should be created at the right container/blob or table level based on the need.</span><span class="sxs-lookup"><span data-stu-id="d3252-179">The URI should be created at the right container/blob or table level based on the need.</span></span> <span data-ttu-id="d3252-180">A shared access signature URI to a blob allows Data Factory to access that particular blob.</span><span class="sxs-lookup"><span data-stu-id="d3252-180">A shared access signature URI to a blob allows Data Factory to access that particular blob.</span></span> <span data-ttu-id="d3252-181">A shared access signature URI to an Blob storage container allows Data Factory to iterate through blobs in that container.</span><span class="sxs-lookup"><span data-stu-id="d3252-181">A shared access signature URI to an Blob storage container allows Data Factory to iterate through blobs in that container.</span></span> <span data-ttu-id="d3252-182">To provide access to more or fewer objects later, or to update the shared access signature URI, remember to update the linked service with the new URI.</span><span class="sxs-lookup"><span data-stu-id="d3252-182">To provide access to more or fewer objects later, or to update the shared access signature URI, remember to update the linked service with the new URI.</span></span>

### <a name="service-principal-authentication"></a><span data-ttu-id="d3252-183">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-183">Service principal authentication</span></span>

<span data-ttu-id="d3252-184">For Azure Storage service principal authentication in general, refer to [Authenticate access to Azure Storage using Azure Active Directory](../storage/common/storage-auth-aad.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-184">For Azure Storage service principal authentication in general, refer to [Authenticate access to Azure Storage using Azure Active Directory](../storage/common/storage-auth-aad.md).</span></span>

<span data-ttu-id="d3252-185">To use service principal authentication, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d3252-185">To use service principal authentication, follow these steps:</span></span>

1. <span data-ttu-id="d3252-186">Register an application entity in Azure Active Directory (Azure AD) by following [Register your application with an Azure AD tenant](../storage/common/storage-auth-aad-app.md#register-your-application-with-an-azure-ad-tenant).</span><span class="sxs-lookup"><span data-stu-id="d3252-186">Register an application entity in Azure Active Directory (Azure AD) by following [Register your application with an Azure AD tenant](../storage/common/storage-auth-aad-app.md#register-your-application-with-an-azure-ad-tenant).</span></span> <span data-ttu-id="d3252-187">Make note of the following values, which you use to define the linked service:</span><span class="sxs-lookup"><span data-stu-id="d3252-187">Make note of the following values, which you use to define the linked service:</span></span>

    - <span data-ttu-id="d3252-188">Application ID</span><span class="sxs-lookup"><span data-stu-id="d3252-188">Application ID</span></span>
    - <span data-ttu-id="d3252-189">Application key</span><span class="sxs-lookup"><span data-stu-id="d3252-189">Application key</span></span>
    - <span data-ttu-id="d3252-190">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="d3252-190">Tenant ID</span></span>

2. <span data-ttu-id="d3252-191">Grant the service principal proper permission in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-191">Grant the service principal proper permission in Azure Blob storage.</span></span> <span data-ttu-id="d3252-192">Refer to [Manage access rights to Azure Storage data with RBAC](../storage/common/storage-auth-aad-rbac.md) with more details on the roles.</span><span class="sxs-lookup"><span data-stu-id="d3252-192">Refer to [Manage access rights to Azure Storage data with RBAC](../storage/common/storage-auth-aad-rbac.md) with more details on the roles.</span></span>

    - <span data-ttu-id="d3252-193">**As source**, in Access control (IAM), grant at least **Storage Blob Data Reader** role.</span><span class="sxs-lookup"><span data-stu-id="d3252-193">**As source**, in Access control (IAM), grant at least **Storage Blob Data Reader** role.</span></span>
    - <span data-ttu-id="d3252-194">**As sink**, in Access control (IAM), grant at least **Storage Blob Data Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="d3252-194">**As sink**, in Access control (IAM), grant at least **Storage Blob Data Contributor** role.</span></span>

<span data-ttu-id="d3252-195">These properties are supported for an Azure Blob storage linked service:</span><span class="sxs-lookup"><span data-stu-id="d3252-195">These properties are supported for an Azure Blob storage linked service:</span></span>

| <span data-ttu-id="d3252-196">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-196">Property</span></span> | <span data-ttu-id="d3252-197">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-197">Description</span></span> | <span data-ttu-id="d3252-198">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-198">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-199">type</span><span class="sxs-lookup"><span data-stu-id="d3252-199">type</span></span> | <span data-ttu-id="d3252-200">The type property must be set to **AzureBlobStorage**.</span><span class="sxs-lookup"><span data-stu-id="d3252-200">The type property must be set to **AzureBlobStorage**.</span></span> |<span data-ttu-id="d3252-201">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-201">Yes</span></span> |
| <span data-ttu-id="d3252-202">serviceEndpoint</span><span class="sxs-lookup"><span data-stu-id="d3252-202">serviceEndpoint</span></span> | <span data-ttu-id="d3252-203">Specify the Azure Blob storage service endpoint with the pattern of `https://<accountName>.blob.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="d3252-203">Specify the Azure Blob storage service endpoint with the pattern of `https://<accountName>.blob.core.windows.net/`.</span></span> |<span data-ttu-id="d3252-204">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-204">Yes</span></span> |
| <span data-ttu-id="d3252-205">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="d3252-205">servicePrincipalId</span></span> | <span data-ttu-id="d3252-206">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="d3252-206">Specify the application's client ID.</span></span> | <span data-ttu-id="d3252-207">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-207">Yes</span></span> |
| <span data-ttu-id="d3252-208">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="d3252-208">servicePrincipalKey</span></span> | <span data-ttu-id="d3252-209">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="d3252-209">Specify the application's key.</span></span> <span data-ttu-id="d3252-210">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-210">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="d3252-211">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-211">Yes</span></span> |
| <span data-ttu-id="d3252-212">tenant</span><span class="sxs-lookup"><span data-stu-id="d3252-212">tenant</span></span> | <span data-ttu-id="d3252-213">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="d3252-213">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="d3252-214">Retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3252-214">Retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="d3252-215">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-215">Yes</span></span> |
| <span data-ttu-id="d3252-216">connectVia</span><span class="sxs-lookup"><span data-stu-id="d3252-216">connectVia</span></span> | <span data-ttu-id="d3252-217">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d3252-217">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d3252-218">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is in a private network).</span><span class="sxs-lookup"><span data-stu-id="d3252-218">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is in a private network).</span></span> <span data-ttu-id="d3252-219">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d3252-219">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d3252-220">No</span><span class="sxs-lookup"><span data-stu-id="d3252-220">No</span></span> |

>[!NOTE]
>Service principal authentication is only supported by "AzureBlobStorage" type linked service but not previous "AzureStorage" type linked service.

<span data-ttu-id="d3252-222">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-222">**Example:**</span></span>

```json
{
    "name": "AzureBlobStorageLinkedService",
    "properties": {
        "type": "AzureBlobStorage",
        "typeProperties": {            
            "serviceEndpoint": "https://<accountName>.blob.core.windows.net/",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": {
                "type": "SecureString",
                "value": "<service principal key>"
            },
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>" 
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="managed-service-identity-authentication"></a><span data-ttu-id="d3252-223">Managed service identity authentication</span><span class="sxs-lookup"><span data-stu-id="d3252-223">Managed service identity authentication</span></span>

<span data-ttu-id="d3252-224">A data factory can be associated with a [managed service identity](data-factory-service-identity.md), which represents this specific data factory.</span><span class="sxs-lookup"><span data-stu-id="d3252-224">A data factory can be associated with a [managed service identity](data-factory-service-identity.md), which represents this specific data factory.</span></span> <span data-ttu-id="d3252-225">You can directly use this service identity for Blob storage authentication similar to using your own service principal.</span><span class="sxs-lookup"><span data-stu-id="d3252-225">You can directly use this service identity for Blob storage authentication similar to using your own service principal.</span></span> <span data-ttu-id="d3252-226">It allows this designated factory to access and copy data from/to your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-226">It allows this designated factory to access and copy data from/to your Blob storage.</span></span>

<span data-ttu-id="d3252-227">For Azure Storage MSI authentication in general, refer to [Authenticate access to Azure Storage using Azure Active Directory](../storage/common/storage-auth-aad.md).</span><span class="sxs-lookup"><span data-stu-id="d3252-227">For Azure Storage MSI authentication in general, refer to [Authenticate access to Azure Storage using Azure Active Directory](../storage/common/storage-auth-aad.md).</span></span>

<span data-ttu-id="d3252-228">To use managed service identity (MSI) authentication, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d3252-228">To use managed service identity (MSI) authentication, follow these steps:</span></span>

1. <span data-ttu-id="d3252-229">[Retrieve data factory service identity](data-factory-service-identity.md#retrieve-service-identity) by copying the value of "SERVICE IDENTITY APPLICATION ID" generated along with your factory.</span><span class="sxs-lookup"><span data-stu-id="d3252-229">[Retrieve data factory service identity](data-factory-service-identity.md#retrieve-service-identity) by copying the value of "SERVICE IDENTITY APPLICATION ID" generated along with your factory.</span></span>

2. <span data-ttu-id="d3252-230">Grant the service principal proper permission in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-230">Grant the service principal proper permission in Azure Blob storage.</span></span> <span data-ttu-id="d3252-231">Refer to [Manage access rights to Azure Storage data with RBAC](../storage/common/storage-auth-aad-rbac.md) with more details on the roles.</span><span class="sxs-lookup"><span data-stu-id="d3252-231">Refer to [Manage access rights to Azure Storage data with RBAC](../storage/common/storage-auth-aad-rbac.md) with more details on the roles.</span></span>

    - <span data-ttu-id="d3252-232">**As source**, in Access control (IAM), grant at least **Storage Blob Data Reader** role.</span><span class="sxs-lookup"><span data-stu-id="d3252-232">**As source**, in Access control (IAM), grant at least **Storage Blob Data Reader** role.</span></span>
    - <span data-ttu-id="d3252-233">**As sink**, in Access control (IAM), grant at least **Storage Blob Data Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="d3252-233">**As sink**, in Access control (IAM), grant at least **Storage Blob Data Contributor** role.</span></span>

<span data-ttu-id="d3252-234">These properties are supported for an Azure Blob storage linked service:</span><span class="sxs-lookup"><span data-stu-id="d3252-234">These properties are supported for an Azure Blob storage linked service:</span></span>

| <span data-ttu-id="d3252-235">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-235">Property</span></span> | <span data-ttu-id="d3252-236">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-236">Description</span></span> | <span data-ttu-id="d3252-237">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-237">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-238">type</span><span class="sxs-lookup"><span data-stu-id="d3252-238">type</span></span> | <span data-ttu-id="d3252-239">The type property must be set to **AzureBlobStorage**.</span><span class="sxs-lookup"><span data-stu-id="d3252-239">The type property must be set to **AzureBlobStorage**.</span></span> |<span data-ttu-id="d3252-240">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-240">Yes</span></span> |
| <span data-ttu-id="d3252-241">serviceEndpoint</span><span class="sxs-lookup"><span data-stu-id="d3252-241">serviceEndpoint</span></span> | <span data-ttu-id="d3252-242">Specify the Azure Blob storage service endpoint with the pattern of `https://<accountName>.blob.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="d3252-242">Specify the Azure Blob storage service endpoint with the pattern of `https://<accountName>.blob.core.windows.net/`.</span></span> |<span data-ttu-id="d3252-243">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-243">Yes</span></span> |
| <span data-ttu-id="d3252-244">connectVia</span><span class="sxs-lookup"><span data-stu-id="d3252-244">connectVia</span></span> | <span data-ttu-id="d3252-245">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d3252-245">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d3252-246">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is in a private network).</span><span class="sxs-lookup"><span data-stu-id="d3252-246">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is in a private network).</span></span> <span data-ttu-id="d3252-247">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d3252-247">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d3252-248">No</span><span class="sxs-lookup"><span data-stu-id="d3252-248">No</span></span> |

>[!NOTE]
>Managed service identity authentication is only supported by "AzureBlobStorage" type linked service but not previous "AzureStorage" type linked service. 

<span data-ttu-id="d3252-250">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-250">**Example:**</span></span>

```json
{
    "name": "AzureBlobStorageLinkedService",
    "properties": {
        "type": "AzureBlobStorage",
        "typeProperties": {            
            "serviceEndpoint": "https://<accountName>.blob.core.windows.net/"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d3252-251">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="d3252-251">Dataset properties</span></span>

<span data-ttu-id="d3252-252">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="d3252-252">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="d3252-253">This section provides a list of properties supported by the Blob storage dataset.</span><span class="sxs-lookup"><span data-stu-id="d3252-253">This section provides a list of properties supported by the Blob storage dataset.</span></span>

<span data-ttu-id="d3252-254">To copy data to and from Blob storage, set the type property of the dataset to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="d3252-254">To copy data to and from Blob storage, set the type property of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="d3252-255">The following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="d3252-255">The following properties are supported.</span></span>

| <span data-ttu-id="d3252-256">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-256">Property</span></span> | <span data-ttu-id="d3252-257">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-257">Description</span></span> | <span data-ttu-id="d3252-258">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-258">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-259">type</span><span class="sxs-lookup"><span data-stu-id="d3252-259">type</span></span> | <span data-ttu-id="d3252-260">The type property of the dataset must be set to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="d3252-260">The type property of the dataset must be set to **AzureBlob**.</span></span> |<span data-ttu-id="d3252-261">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-261">Yes</span></span> |
| <span data-ttu-id="d3252-262">folderPath</span><span class="sxs-lookup"><span data-stu-id="d3252-262">folderPath</span></span> | <span data-ttu-id="d3252-263">Path to the container and folder in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3252-263">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="d3252-264">Wildcard filter is not supported.</span><span class="sxs-lookup"><span data-stu-id="d3252-264">Wildcard filter is not supported.</span></span> <span data-ttu-id="d3252-265">An example is myblobcontainer/myblobfolder/.</span><span class="sxs-lookup"><span data-stu-id="d3252-265">An example is myblobcontainer/myblobfolder/.</span></span> |<span data-ttu-id="d3252-266">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-266">Yes</span></span> |
| <span data-ttu-id="d3252-267">fileName</span><span class="sxs-lookup"><span data-stu-id="d3252-267">fileName</span></span> | <span data-ttu-id="d3252-268">**Name or wildcard filter** for the blob(s) under the specified "folderPath".</span><span class="sxs-lookup"><span data-stu-id="d3252-268">**Name or wildcard filter** for the blob(s) under the specified "folderPath".</span></span> <span data-ttu-id="d3252-269">If you don't specify a value for this property, the dataset points to all blobs in the folder.</span><span class="sxs-lookup"><span data-stu-id="d3252-269">If you don't specify a value for this property, the dataset points to all blobs in the folder.</span></span> <br/><br/><span data-ttu-id="d3252-270">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span><span class="sxs-lookup"><span data-stu-id="d3252-270">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span></span><br/><span data-ttu-id="d3252-271">- Example 1: `"fileName": "*.csv"`</span><span class="sxs-lookup"><span data-stu-id="d3252-271">- Example 1: `"fileName": "*.csv"`</span></span><br/><span data-ttu-id="d3252-272">- Example 2: `"fileName": "???20180427.txt"`</span><span class="sxs-lookup"><span data-stu-id="d3252-272">- Example 2: `"fileName": "???20180427.txt"`</span></span><br/><span data-ttu-id="d3252-273">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span><span class="sxs-lookup"><span data-stu-id="d3252-273">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span></span><br/><br/><span data-ttu-id="d3252-274">When fileName isn't specified for an output dataset and **preserveHierarchy** isn't specified in the activity sink, the copy activity automatically generates the blob name with the following pattern: "*Data.[activity run id GUID].[GUID if FlattenHierarchy].[format if configured].[compression if configured]*".</span><span class="sxs-lookup"><span data-stu-id="d3252-274">When fileName isn't specified for an output dataset and **preserveHierarchy** isn't specified in the activity sink, the copy activity automatically generates the blob name with the following pattern: "*Data.[activity run id GUID].[GUID if FlattenHierarchy].[format if configured].[compression if configured]*".</span></span> <span data-ttu-id="d3252-275">An example is "Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.gz".</span><span class="sxs-lookup"><span data-stu-id="d3252-275">An example is "Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.gz".</span></span> |<span data-ttu-id="d3252-276">No</span><span class="sxs-lookup"><span data-stu-id="d3252-276">No</span></span> |
| <span data-ttu-id="d3252-277">format</span><span class="sxs-lookup"><span data-stu-id="d3252-277">format</span></span> | <span data-ttu-id="d3252-278">If you want to copy files as is between file-based stores (binary copy), skip the format section in both the input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="d3252-278">If you want to copy files as is between file-based stores (binary copy), skip the format section in both the input and output dataset definitions.</span></span><br/><br/><span data-ttu-id="d3252-279">If you want to parse or generate files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d3252-279">If you want to parse or generate files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="d3252-280">Set the **type** property under **format** to one of these values.</span><span class="sxs-lookup"><span data-stu-id="d3252-280">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="d3252-281">For more information, see the [Text format](supported-file-formats-and-compression-codecs.md#text-format), [JSON format](supported-file-formats-and-compression-codecs.md#json-format), [Avro format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="d3252-281">For more information, see the [Text format](supported-file-formats-and-compression-codecs.md#text-format), [JSON format](supported-file-formats-and-compression-codecs.md#json-format), [Avro format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span></span> |<span data-ttu-id="d3252-282">No (only for binary copy scenario)</span><span class="sxs-lookup"><span data-stu-id="d3252-282">No (only for binary copy scenario)</span></span> |
| <span data-ttu-id="d3252-283">compression</span><span class="sxs-lookup"><span data-stu-id="d3252-283">compression</span></span> | <span data-ttu-id="d3252-284">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="d3252-284">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="d3252-285">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d3252-285">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span></span><br/><span data-ttu-id="d3252-286">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d3252-286">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span><br/><span data-ttu-id="d3252-287">Supported levels are **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="d3252-287">Supported levels are **Optimal** and **Fastest**.</span></span> |<span data-ttu-id="d3252-288">No</span><span class="sxs-lookup"><span data-stu-id="d3252-288">No</span></span> |

>[!TIP]
>To copy all blobs under a folder, specify **folderPath** only.<br>To copy a single blob with a given name, specify **folderPath** with folder part and **fileName** with file name.<br>To copy a subset of blobs under a folder, specify **folderPath** with folder part and **fileName** with wildcard filter. 

<span data-ttu-id="d3252-292">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-292">**Example:**</span></span>

```json
{
    "name": "AzureBlobDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": {
            "referenceName": "<Azure Blob storage linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName": "myfile.csv.gz",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="d3252-293">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="d3252-293">Copy activity properties</span></span>

<span data-ttu-id="d3252-294">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="d3252-294">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="d3252-295">This section provides a list of properties supported by the Blob storage source and sink.</span><span class="sxs-lookup"><span data-stu-id="d3252-295">This section provides a list of properties supported by the Blob storage source and sink.</span></span>

### <a name="blob-storage-as-a-source-type"></a><span data-ttu-id="d3252-296">Blob storage as a source type</span><span class="sxs-lookup"><span data-stu-id="d3252-296">Blob storage as a source type</span></span>

<span data-ttu-id="d3252-297">To copy data from Blob storage, set the source type in the copy activity to **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="d3252-297">To copy data from Blob storage, set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="d3252-298">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="d3252-298">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="d3252-299">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-299">Property</span></span> | <span data-ttu-id="d3252-300">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-300">Description</span></span> | <span data-ttu-id="d3252-301">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-301">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-302">type</span><span class="sxs-lookup"><span data-stu-id="d3252-302">type</span></span> | <span data-ttu-id="d3252-303">The type property of the copy activity source must be set to **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="d3252-303">The type property of the copy activity source must be set to **BlobSource**.</span></span> |<span data-ttu-id="d3252-304">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-304">Yes</span></span> |
| <span data-ttu-id="d3252-305">recursive</span><span class="sxs-lookup"><span data-stu-id="d3252-305">recursive</span></span> | <span data-ttu-id="d3252-306">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="d3252-306">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> <span data-ttu-id="d3252-307">Note that when recursive is set to true and the sink is a file-based store, an empty folder or subfolder isn't copied or created at the sink.</span><span class="sxs-lookup"><span data-stu-id="d3252-307">Note that when recursive is set to true and the sink is a file-based store, an empty folder or subfolder isn't copied or created at the sink.</span></span><br/><span data-ttu-id="d3252-308">Allowed values are **true** (default) and **false**.</span><span class="sxs-lookup"><span data-stu-id="d3252-308">Allowed values are **true** (default) and **false**.</span></span> | <span data-ttu-id="d3252-309">No</span><span class="sxs-lookup"><span data-stu-id="d3252-309">No</span></span> |

<span data-ttu-id="d3252-310">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-310">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromBlob",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure Blob input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="blob-storage-as-a-sink-type"></a><span data-ttu-id="d3252-311">Blob storage as a sink type</span><span class="sxs-lookup"><span data-stu-id="d3252-311">Blob storage as a sink type</span></span>

<span data-ttu-id="d3252-312">To copy data to Blob storage, set the sink type in the copy activity to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d3252-312">To copy data to Blob storage, set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="d3252-313">The following properties are supported in the **sink** section.</span><span class="sxs-lookup"><span data-stu-id="d3252-313">The following properties are supported in the **sink** section.</span></span>

| <span data-ttu-id="d3252-314">Property</span><span class="sxs-lookup"><span data-stu-id="d3252-314">Property</span></span> | <span data-ttu-id="d3252-315">Description</span><span class="sxs-lookup"><span data-stu-id="d3252-315">Description</span></span> | <span data-ttu-id="d3252-316">Required</span><span class="sxs-lookup"><span data-stu-id="d3252-316">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d3252-317">type</span><span class="sxs-lookup"><span data-stu-id="d3252-317">type</span></span> | <span data-ttu-id="d3252-318">The type property of the copy activity sink must be set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d3252-318">The type property of the copy activity sink must be set to **BlobSink**.</span></span> |<span data-ttu-id="d3252-319">Yes</span><span class="sxs-lookup"><span data-stu-id="d3252-319">Yes</span></span> |
| <span data-ttu-id="d3252-320">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d3252-320">copyBehavior</span></span> | <span data-ttu-id="d3252-321">Defines the copy behavior when the source is files from a file-based data store.</span><span class="sxs-lookup"><span data-stu-id="d3252-321">Defines the copy behavior when the source is files from a file-based data store.</span></span><br/><br/><span data-ttu-id="d3252-322">Allowed values are:</span><span class="sxs-lookup"><span data-stu-id="d3252-322">Allowed values are:</span></span><br/><span data-ttu-id="d3252-323"><b>- PreserveHierarchy (default)</b>: Preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="d3252-323"><b>- PreserveHierarchy (default)</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="d3252-324">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="d3252-324">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><span data-ttu-id="d3252-325"><b>- FlattenHierarchy</b>: All files from the source folder are in the first level of the target folder.</span><span class="sxs-lookup"><span data-stu-id="d3252-325"><b>- FlattenHierarchy</b>: All files from the source folder are in the first level of the target folder.</span></span> <span data-ttu-id="d3252-326">The target files have autogenerated names.</span><span class="sxs-lookup"><span data-stu-id="d3252-326">The target files have autogenerated names.</span></span> <br/><span data-ttu-id="d3252-327"><b>- MergeFiles</b>: Merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="d3252-327"><b>- MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="d3252-328">If the file or blob name is specified, the merged file name is the specified name.</span><span class="sxs-lookup"><span data-stu-id="d3252-328">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="d3252-329">Otherwise, it's an autogenerated file name.</span><span class="sxs-lookup"><span data-stu-id="d3252-329">Otherwise, it's an autogenerated file name.</span></span> | <span data-ttu-id="d3252-330">No</span><span class="sxs-lookup"><span data-stu-id="d3252-330">No</span></span> |

<span data-ttu-id="d3252-331">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3252-331">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToBlob",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure Blob output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "BlobSink",
                "copyBehavior": "PreserveHierarchy"
            }
        }
    }
]
```

### <a name="some-recursive-and-copybehavior-examples"></a><span data-ttu-id="d3252-332">Some recursive and copyBehavior examples</span><span class="sxs-lookup"><span data-stu-id="d3252-332">Some recursive and copyBehavior examples</span></span>

<span data-ttu-id="d3252-333">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span><span class="sxs-lookup"><span data-stu-id="d3252-333">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="d3252-334">recursive</span><span class="sxs-lookup"><span data-stu-id="d3252-334">recursive</span></span> | <span data-ttu-id="d3252-335">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d3252-335">copyBehavior</span></span> | <span data-ttu-id="d3252-336">Source folder structure</span><span class="sxs-lookup"><span data-stu-id="d3252-336">Source folder structure</span></span> | <span data-ttu-id="d3252-337">Resulting target</span><span class="sxs-lookup"><span data-stu-id="d3252-337">Resulting target</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d3252-338">true</span><span class="sxs-lookup"><span data-stu-id="d3252-338">true</span></span> |<span data-ttu-id="d3252-339">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="d3252-339">preserveHierarchy</span></span> | <span data-ttu-id="d3252-340">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-340">Folder1</span></span><br/><span data-ttu-id="d3252-341">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-341">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-342">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-342">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-343">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-343">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-345">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-345">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-346">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-346">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> | <span data-ttu-id="d3252-347">The target folder Folder1 is created with the same structure as the source:</span><span class="sxs-lookup"><span data-stu-id="d3252-347">The target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="d3252-348">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-348">Folder1</span></span><br/><span data-ttu-id="d3252-349">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-349">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-350">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-350">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-351">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-351">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-354">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-354">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="d3252-355">true</span><span class="sxs-lookup"><span data-stu-id="d3252-355">true</span></span> |<span data-ttu-id="d3252-356">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="d3252-356">flattenHierarchy</span></span> | <span data-ttu-id="d3252-357">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-357">Folder1</span></span><br/><span data-ttu-id="d3252-358">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-358">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-359">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-359">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-360">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-360">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> | <span data-ttu-id="d3252-364">The target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="d3252-364">The target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="d3252-365">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-365">Folder1</span></span><br/><span data-ttu-id="d3252-366">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File1</span><span class="sxs-lookup"><span data-stu-id="d3252-366">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File1</span></span><br/><span data-ttu-id="d3252-367">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File2</span><span class="sxs-lookup"><span data-stu-id="d3252-367">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File2</span></span><br/><span data-ttu-id="d3252-368">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File3</span><span class="sxs-lookup"><span data-stu-id="d3252-368">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File3</span></span><br/><span data-ttu-id="d3252-369">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File4</span><span class="sxs-lookup"><span data-stu-id="d3252-369">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File4</span></span><br/><span data-ttu-id="d3252-370">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File5</span><span class="sxs-lookup"><span data-stu-id="d3252-370">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File5</span></span> |
| <span data-ttu-id="d3252-371">true</span><span class="sxs-lookup"><span data-stu-id="d3252-371">true</span></span> |<span data-ttu-id="d3252-372">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="d3252-372">mergeFiles</span></span> | <span data-ttu-id="d3252-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-373">Folder1</span></span><br/><span data-ttu-id="d3252-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> | <span data-ttu-id="d3252-380">The target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="d3252-380">The target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="d3252-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-381">Folder1</span></span><br/><span data-ttu-id="d3252-382">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File5 contents are merged into one file with an autogenerated file name.</span><span class="sxs-lookup"><span data-stu-id="d3252-382">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File5 contents are merged into one file with an autogenerated file name.</span></span> |
| <span data-ttu-id="d3252-383">false</span><span class="sxs-lookup"><span data-stu-id="d3252-383">false</span></span> |<span data-ttu-id="d3252-384">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="d3252-384">preserveHierarchy</span></span> | <span data-ttu-id="d3252-385">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-385">Folder1</span></span><br/><span data-ttu-id="d3252-386">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-386">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-387">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-387">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-388">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-388">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-389">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-389">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-390">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-390">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-391">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-391">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> | <span data-ttu-id="d3252-392">The target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="d3252-392">The target folder Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="d3252-393">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-393">Folder1</span></span><br/><span data-ttu-id="d3252-394">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-394">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-395">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-395">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="d3252-396">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="d3252-396">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="d3252-397">false</span><span class="sxs-lookup"><span data-stu-id="d3252-397">false</span></span> |<span data-ttu-id="d3252-398">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="d3252-398">flattenHierarchy</span></span> | <span data-ttu-id="d3252-399">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-399">Folder1</span></span><br/><span data-ttu-id="d3252-400">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-400">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-401">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-401">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-402">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-402">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-403">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-403">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-404">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-404">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-405">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-405">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> | <span data-ttu-id="d3252-406">The target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="d3252-406">The target folder Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="d3252-407">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-407">Folder1</span></span><br/><span data-ttu-id="d3252-408">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File1</span><span class="sxs-lookup"><span data-stu-id="d3252-408">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File1</span></span><br/><span data-ttu-id="d3252-409">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File2</span><span class="sxs-lookup"><span data-stu-id="d3252-409">&nbsp;&nbsp;&nbsp;&nbsp;autogenerated name for File2</span></span><br/><br/><span data-ttu-id="d3252-410">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="d3252-410">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="d3252-411">false</span><span class="sxs-lookup"><span data-stu-id="d3252-411">false</span></span> |<span data-ttu-id="d3252-412">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="d3252-412">mergeFiles</span></span> | <span data-ttu-id="d3252-413">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-413">Folder1</span></span><br/><span data-ttu-id="d3252-414">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d3252-414">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d3252-415">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d3252-415">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d3252-416">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d3252-416">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d3252-417">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d3252-417">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d3252-418">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d3252-418">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d3252-419">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d3252-419">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> | <span data-ttu-id="d3252-420">The target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="d3252-420">The target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="d3252-421">Folder1</span><span class="sxs-lookup"><span data-stu-id="d3252-421">Folder1</span></span><br/><span data-ttu-id="d3252-422">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an autogenerated file name.</span><span class="sxs-lookup"><span data-stu-id="d3252-422">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an autogenerated file name.</span></span> <span data-ttu-id="d3252-423">autogenerated name for File1</span><span class="sxs-lookup"><span data-stu-id="d3252-423">autogenerated name for File1</span></span><br/><br/><span data-ttu-id="d3252-424">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="d3252-424">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3252-425">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3252-425">Next steps</span></span>
<span data-ttu-id="d3252-426">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d3252-426">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
