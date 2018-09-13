---
title: Copy data from Google BigQuery by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Google BigQuery to supported sink data stores by using a copy activity in a data factory pipeline.
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
ms.date: 02/12/2018
ms.author: jingwang
ms.openlocfilehash: 51cacb385f28cf70a65b9c0e1c14d48e22be0a4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865548"
---
# <a name="copy-data-from-google-bigquery-by-using-azure-data-factory"></a><span data-ttu-id="e2b39-103">Copy data from Google BigQuery by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2b39-103">Copy data from Google BigQuery by using Azure Data Factory</span></span>

<span data-ttu-id="e2b39-104">This article outlines how to use Copy Activity in Azure Data Factory to copy data from Google BigQuery.</span><span class="sxs-lookup"><span data-stu-id="e2b39-104">This article outlines how to use Copy Activity in Azure Data Factory to copy data from Google BigQuery.</span></span> <span data-ttu-id="e2b39-105">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span><span class="sxs-lookup"><span data-stu-id="e2b39-105">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="e2b39-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="e2b39-106">Supported capabilities</span></span>

<span data-ttu-id="e2b39-107">You can copy data from Google BigQuery to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="e2b39-107">You can copy data from Google BigQuery to any supported sink data store.</span></span> <span data-ttu-id="e2b39-108">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="e2b39-108">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

 <span data-ttu-id="e2b39-109">Data Factory provides a built-in driver to enable connectivity.</span><span class="sxs-lookup"><span data-stu-id="e2b39-109">Data Factory provides a built-in driver to enable connectivity.</span></span> <span data-ttu-id="e2b39-110">Therefore, you don't need to manually install a driver to use this connector.</span><span class="sxs-lookup"><span data-stu-id="e2b39-110">Therefore, you don't need to manually install a driver to use this connector.</span></span>

## <a name="get-started"></a><span data-ttu-id="e2b39-111">Get started</span><span class="sxs-lookup"><span data-stu-id="e2b39-111">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="e2b39-112">The following sections provide details about properties that are used to define Data Factory entities specific to the Google BigQuery connector.</span><span class="sxs-lookup"><span data-stu-id="e2b39-112">The following sections provide details about properties that are used to define Data Factory entities specific to the Google BigQuery connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e2b39-113">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="e2b39-113">Linked service properties</span></span>

<span data-ttu-id="e2b39-114">The following properties are supported for the Google BigQuery linked service.</span><span class="sxs-lookup"><span data-stu-id="e2b39-114">The following properties are supported for the Google BigQuery linked service.</span></span>

| <span data-ttu-id="e2b39-115">Property</span><span class="sxs-lookup"><span data-stu-id="e2b39-115">Property</span></span> | <span data-ttu-id="e2b39-116">Description</span><span class="sxs-lookup"><span data-stu-id="e2b39-116">Description</span></span> | <span data-ttu-id="e2b39-117">Required</span><span class="sxs-lookup"><span data-stu-id="e2b39-117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e2b39-118">type</span><span class="sxs-lookup"><span data-stu-id="e2b39-118">type</span></span> | <span data-ttu-id="e2b39-119">The type property must be set to **GoogleBigQuery**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-119">The type property must be set to **GoogleBigQuery**.</span></span> | <span data-ttu-id="e2b39-120">Yes</span><span class="sxs-lookup"><span data-stu-id="e2b39-120">Yes</span></span> |
| <span data-ttu-id="e2b39-121">project</span><span class="sxs-lookup"><span data-stu-id="e2b39-121">project</span></span> | <span data-ttu-id="e2b39-122">The project ID of the default BigQuery project to query against.</span><span class="sxs-lookup"><span data-stu-id="e2b39-122">The project ID of the default BigQuery project to query against.</span></span>  | <span data-ttu-id="e2b39-123">Yes</span><span class="sxs-lookup"><span data-stu-id="e2b39-123">Yes</span></span> |
| <span data-ttu-id="e2b39-124">additionalProjects</span><span class="sxs-lookup"><span data-stu-id="e2b39-124">additionalProjects</span></span> | <span data-ttu-id="e2b39-125">A comma-separated list of project IDs of public BigQuery projects to access.</span><span class="sxs-lookup"><span data-stu-id="e2b39-125">A comma-separated list of project IDs of public BigQuery projects to access.</span></span>  | <span data-ttu-id="e2b39-126">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-126">No</span></span> |
| <span data-ttu-id="e2b39-127">requestGoogleDriveScope</span><span class="sxs-lookup"><span data-stu-id="e2b39-127">requestGoogleDriveScope</span></span> | <span data-ttu-id="e2b39-128">Whether to request access to Google Drive.</span><span class="sxs-lookup"><span data-stu-id="e2b39-128">Whether to request access to Google Drive.</span></span> <span data-ttu-id="e2b39-129">Allowing Google Drive access enables support for federated tables that combine BigQuery data with data from Google Drive.</span><span class="sxs-lookup"><span data-stu-id="e2b39-129">Allowing Google Drive access enables support for federated tables that combine BigQuery data with data from Google Drive.</span></span> <span data-ttu-id="e2b39-130">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-130">The default value is **false**.</span></span>  | <span data-ttu-id="e2b39-131">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-131">No</span></span> |
| <span data-ttu-id="e2b39-132">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e2b39-132">authenticationType</span></span> | <span data-ttu-id="e2b39-133">The OAuth 2.0 authentication mechanism used for authentication.</span><span class="sxs-lookup"><span data-stu-id="e2b39-133">The OAuth 2.0 authentication mechanism used for authentication.</span></span> <span data-ttu-id="e2b39-134">ServiceAuthentication can be used only on Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="e2b39-134">ServiceAuthentication can be used only on Self-hosted Integration Runtime.</span></span> <br/><span data-ttu-id="e2b39-135">Allowed values are **UserAuthentication** and **ServiceAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-135">Allowed values are **UserAuthentication** and **ServiceAuthentication**.</span></span> <span data-ttu-id="e2b39-136">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span><span class="sxs-lookup"><span data-stu-id="e2b39-136">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="e2b39-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e2b39-137">Yes</span></span> |

### <a name="using-user-authentication"></a><span data-ttu-id="e2b39-138">Using user authentication</span><span class="sxs-lookup"><span data-stu-id="e2b39-138">Using user authentication</span></span>

<span data-ttu-id="e2b39-139">Set "authenticationType" property to **UserAuthentication**, and specify the following properties along with generic properties described in the previous section:</span><span class="sxs-lookup"><span data-stu-id="e2b39-139">Set "authenticationType" property to **UserAuthentication**, and specify the following properties along with generic properties described in the previous section:</span></span>

| <span data-ttu-id="e2b39-140">Property</span><span class="sxs-lookup"><span data-stu-id="e2b39-140">Property</span></span> | <span data-ttu-id="e2b39-141">Description</span><span class="sxs-lookup"><span data-stu-id="e2b39-141">Description</span></span> | <span data-ttu-id="e2b39-142">Required</span><span class="sxs-lookup"><span data-stu-id="e2b39-142">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e2b39-143">clientId</span><span class="sxs-lookup"><span data-stu-id="e2b39-143">clientId</span></span> | <span data-ttu-id="e2b39-144">ID of the application used to generate the refresh token.</span><span class="sxs-lookup"><span data-stu-id="e2b39-144">ID of the application used to generate the refresh token.</span></span> | <span data-ttu-id="e2b39-145">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-145">No</span></span> |
| <span data-ttu-id="e2b39-146">clientSecret</span><span class="sxs-lookup"><span data-stu-id="e2b39-146">clientSecret</span></span> | <span data-ttu-id="e2b39-147">Secret of the application used to generate the refresh token.</span><span class="sxs-lookup"><span data-stu-id="e2b39-147">Secret of the application used to generate the refresh token.</span></span> <span data-ttu-id="e2b39-148">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e2b39-148">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="e2b39-149">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-149">No</span></span> |
| <span data-ttu-id="e2b39-150">refreshToken</span><span class="sxs-lookup"><span data-stu-id="e2b39-150">refreshToken</span></span> | <span data-ttu-id="e2b39-151">The refresh token obtained from Google used to authorize access to BigQuery.</span><span class="sxs-lookup"><span data-stu-id="e2b39-151">The refresh token obtained from Google used to authorize access to BigQuery.</span></span> <span data-ttu-id="e2b39-152">Learn how to get one from [Obtaining OAuth 2.0 access tokens](https://developers.google.com/identity/protocols/OAuth2WebServer#obtainingaccesstokens) and [this community blog](https://jpd.ms/getting-your-bigquery-refresh-token-for-azure-datafactory-f884ff815a59).</span><span class="sxs-lookup"><span data-stu-id="e2b39-152">Learn how to get one from [Obtaining OAuth 2.0 access tokens](https://developers.google.com/identity/protocols/OAuth2WebServer#obtainingaccesstokens) and [this community blog](https://jpd.ms/getting-your-bigquery-refresh-token-for-azure-datafactory-f884ff815a59).</span></span> <span data-ttu-id="e2b39-153">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e2b39-153">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="e2b39-154">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-154">No</span></span> |

<span data-ttu-id="e2b39-155">**Example:**</span><span class="sxs-lookup"><span data-stu-id="e2b39-155">**Example:**</span></span>

```json
{
    "name": "GoogleBigQueryLinkedService",
    "properties": {
        "type": "GoogleBigQuery",
        "typeProperties": {
            "project" : "<project ID>",
            "additionalProjects" : "<additional project IDs>",
            "requestGoogleDriveScope" : true,
            "authenticationType" : "UserAuthentication",
            "clientId": "<id of the application used to generate the refresh token>",
            "clientSecret": {
                "type": "SecureString",
                "value":"<secret of the application used to generate the refresh token>"
            },
            "refreshToken": {
                 "type": "SecureString",
                 "value": "<refresh token>"
            }
        }
    }
}
```

### <a name="using-service-authentication"></a><span data-ttu-id="e2b39-156">Using service authentication</span><span class="sxs-lookup"><span data-stu-id="e2b39-156">Using service authentication</span></span>

<span data-ttu-id="e2b39-157">Set "authenticationType" property to **ServiceAuthentication**, and specify the following properties along with generic properties described in the previous section.</span><span class="sxs-lookup"><span data-stu-id="e2b39-157">Set "authenticationType" property to **ServiceAuthentication**, and specify the following properties along with generic properties described in the previous section.</span></span> <span data-ttu-id="e2b39-158">This authentication type can be used only on Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="e2b39-158">This authentication type can be used only on Self-hosted Integration Runtime.</span></span>

| <span data-ttu-id="e2b39-159">Property</span><span class="sxs-lookup"><span data-stu-id="e2b39-159">Property</span></span> | <span data-ttu-id="e2b39-160">Description</span><span class="sxs-lookup"><span data-stu-id="e2b39-160">Description</span></span> | <span data-ttu-id="e2b39-161">Required</span><span class="sxs-lookup"><span data-stu-id="e2b39-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e2b39-162">email</span><span class="sxs-lookup"><span data-stu-id="e2b39-162">email</span></span> | <span data-ttu-id="e2b39-163">The service account email ID that is used for ServiceAuthentication.</span><span class="sxs-lookup"><span data-stu-id="e2b39-163">The service account email ID that is used for ServiceAuthentication.</span></span> <span data-ttu-id="e2b39-164">It can be used only on Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="e2b39-164">It can be used only on Self-hosted Integration Runtime.</span></span>  | <span data-ttu-id="e2b39-165">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-165">No</span></span> |
| <span data-ttu-id="e2b39-166">keyFilePath</span><span class="sxs-lookup"><span data-stu-id="e2b39-166">keyFilePath</span></span> | <span data-ttu-id="e2b39-167">The full path to the .p12 key file that is used to authenticate the service account email address.</span><span class="sxs-lookup"><span data-stu-id="e2b39-167">The full path to the .p12 key file that is used to authenticate the service account email address.</span></span> | <span data-ttu-id="e2b39-168">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-168">No</span></span> |
| <span data-ttu-id="e2b39-169">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="e2b39-169">trustedCertPath</span></span> | <span data-ttu-id="e2b39-170">The full path of the .pem file that contains trusted CA certificates used to verify the server when you connect over SSL.</span><span class="sxs-lookup"><span data-stu-id="e2b39-170">The full path of the .pem file that contains trusted CA certificates used to verify the server when you connect over SSL.</span></span> <span data-ttu-id="e2b39-171">This property can be set only when you use SSL on Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="e2b39-171">This property can be set only when you use SSL on Self-hosted Integration Runtime.</span></span> <span data-ttu-id="e2b39-172">The default value is the cacerts.pem file installed with the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="e2b39-172">The default value is the cacerts.pem file installed with the integration runtime.</span></span>  | <span data-ttu-id="e2b39-173">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-173">No</span></span> |
| <span data-ttu-id="e2b39-174">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="e2b39-174">useSystemTrustStore</span></span> | <span data-ttu-id="e2b39-175">Specifies whether to use a CA certificate from the system trust store or from a specified .pem file.</span><span class="sxs-lookup"><span data-stu-id="e2b39-175">Specifies whether to use a CA certificate from the system trust store or from a specified .pem file.</span></span> <span data-ttu-id="e2b39-176">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-176">The default value is **false**.</span></span>  | <span data-ttu-id="e2b39-177">No</span><span class="sxs-lookup"><span data-stu-id="e2b39-177">No</span></span> |

<span data-ttu-id="e2b39-178">**Example:**</span><span class="sxs-lookup"><span data-stu-id="e2b39-178">**Example:**</span></span>

```json
{
    "name": "GoogleBigQueryLinkedService",
    "properties": {
        "type": "GoogleBigQuery",
        "typeProperties": {
            "project" : "<project id>",
            "requestGoogleDriveScope" : true,
            "authenticationType" : "ServiceAuthentication",
            "email": "<email>",
            "keyFilePath": "<.p12 key path on the IR machine>"
        },
        "connectVia": {
            "referenceName": "<name of Self-hosted Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
} 
```

## <a name="dataset-properties"></a><span data-ttu-id="e2b39-179">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="e2b39-179">Dataset properties</span></span>

<span data-ttu-id="e2b39-180">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="e2b39-180">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="e2b39-181">This section provides a list of properties supported by the Google BigQuery dataset.</span><span class="sxs-lookup"><span data-stu-id="e2b39-181">This section provides a list of properties supported by the Google BigQuery dataset.</span></span>

<span data-ttu-id="e2b39-182">To copy data from Google BigQuery, set the type property of the dataset to **GoogleBigQueryObject**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-182">To copy data from Google BigQuery, set the type property of the dataset to **GoogleBigQueryObject**.</span></span> <span data-ttu-id="e2b39-183">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="e2b39-183">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="e2b39-184">**Example**</span><span class="sxs-lookup"><span data-stu-id="e2b39-184">**Example**</span></span>

```json
{
    "name": "GoogleBigQueryDataset",
    "properties": {
        "type": "GoogleBigQueryObject",
        "linkedServiceName": {
            "referenceName": "<GoogleBigQuery linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="e2b39-185">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="e2b39-185">Copy activity properties</span></span>

<span data-ttu-id="e2b39-186">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="e2b39-186">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="e2b39-187">This section provides a list of properties supported by the Google BigQuery source type.</span><span class="sxs-lookup"><span data-stu-id="e2b39-187">This section provides a list of properties supported by the Google BigQuery source type.</span></span>

### <a name="googlebigquerysource-as-a-source-type"></a><span data-ttu-id="e2b39-188">GoogleBigQuerySource as a source type</span><span class="sxs-lookup"><span data-stu-id="e2b39-188">GoogleBigQuerySource as a source type</span></span>

<span data-ttu-id="e2b39-189">To copy data from Google BigQuery, set the source type in the copy activity to **GoogleBigQuerySource**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-189">To copy data from Google BigQuery, set the source type in the copy activity to **GoogleBigQuerySource**.</span></span> <span data-ttu-id="e2b39-190">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="e2b39-190">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="e2b39-191">Property</span><span class="sxs-lookup"><span data-stu-id="e2b39-191">Property</span></span> | <span data-ttu-id="e2b39-192">Description</span><span class="sxs-lookup"><span data-stu-id="e2b39-192">Description</span></span> | <span data-ttu-id="e2b39-193">Required</span><span class="sxs-lookup"><span data-stu-id="e2b39-193">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e2b39-194">type</span><span class="sxs-lookup"><span data-stu-id="e2b39-194">type</span></span> | <span data-ttu-id="e2b39-195">The type property of the copy activity source must be set to **GoogleBigQuerySource**.</span><span class="sxs-lookup"><span data-stu-id="e2b39-195">The type property of the copy activity source must be set to **GoogleBigQuerySource**.</span></span> | <span data-ttu-id="e2b39-196">Yes</span><span class="sxs-lookup"><span data-stu-id="e2b39-196">Yes</span></span> |
| <span data-ttu-id="e2b39-197">query</span><span class="sxs-lookup"><span data-stu-id="e2b39-197">query</span></span> | <span data-ttu-id="e2b39-198">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="e2b39-198">Use the custom SQL query to read data.</span></span> <span data-ttu-id="e2b39-199">An example is `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="e2b39-199">An example is `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="e2b39-200">Yes</span><span class="sxs-lookup"><span data-stu-id="e2b39-200">Yes</span></span> |

<span data-ttu-id="e2b39-201">**Example:**</span><span class="sxs-lookup"><span data-stu-id="e2b39-201">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromGoogleBigQuery",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<GoogleBigQuery input dataset name>",
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
                "type": "GoogleBigQuerySource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="e2b39-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2b39-202">Next steps</span></span>
<span data-ttu-id="e2b39-203">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e2b39-203">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
