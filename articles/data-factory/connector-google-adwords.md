---
title: Copy data from Google AdWords using Azure Data Factory (Preview) | Microsoft Docs
description: Learn how to copy data from Google AdWords to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 09/07/2018
ms.author: jingwang
ms.openlocfilehash: 402d4fb0c1eb7c6760f800bdd408e9a4d8161ccc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871597"
---
# <a name="copy-data-from-google-adwords-using-azure-data-factory-preview"></a><span data-ttu-id="cf67c-103">Copy data from Google AdWords using Azure Data Factory (Preview)</span><span class="sxs-lookup"><span data-stu-id="cf67c-103">Copy data from Google AdWords using Azure Data Factory (Preview)</span></span>

<span data-ttu-id="cf67c-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Google AdWords.</span><span class="sxs-lookup"><span data-stu-id="cf67c-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Google AdWords.</span></span> <span data-ttu-id="cf67c-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="cf67c-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf67c-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="cf67c-106">This connector is currently in preview.</span></span> <span data-ttu-id="cf67c-107">You can try it out and provide feedback.</span><span class="sxs-lookup"><span data-stu-id="cf67c-107">You can try it out and provide feedback.</span></span> <span data-ttu-id="cf67c-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="cf67c-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="cf67c-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="cf67c-109">Supported capabilities</span></span>

<span data-ttu-id="cf67c-110">You can copy data from Google AdWords to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="cf67c-110">You can copy data from Google AdWords to any supported sink data store.</span></span> <span data-ttu-id="cf67c-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="cf67c-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="cf67c-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="cf67c-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cf67c-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="cf67c-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="cf67c-114">The following sections provide details about properties that are used to define Data Factory entities specific to Google AdWords connector.</span><span class="sxs-lookup"><span data-stu-id="cf67c-114">The following sections provide details about properties that are used to define Data Factory entities specific to Google AdWords connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cf67c-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="cf67c-115">Linked service properties</span></span>

<span data-ttu-id="cf67c-116">The following properties are supported for Google AdWords linked service:</span><span class="sxs-lookup"><span data-stu-id="cf67c-116">The following properties are supported for Google AdWords linked service:</span></span>

| <span data-ttu-id="cf67c-117">Property</span><span class="sxs-lookup"><span data-stu-id="cf67c-117">Property</span></span> | <span data-ttu-id="cf67c-118">Description</span><span class="sxs-lookup"><span data-stu-id="cf67c-118">Description</span></span> | <span data-ttu-id="cf67c-119">Required</span><span class="sxs-lookup"><span data-stu-id="cf67c-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="cf67c-120">type</span><span class="sxs-lookup"><span data-stu-id="cf67c-120">type</span></span> | <span data-ttu-id="cf67c-121">The type property must be set to: **GoogleAdWords**</span><span class="sxs-lookup"><span data-stu-id="cf67c-121">The type property must be set to: **GoogleAdWords**</span></span> | <span data-ttu-id="cf67c-122">Yes</span><span class="sxs-lookup"><span data-stu-id="cf67c-122">Yes</span></span> |
| <span data-ttu-id="cf67c-123">clientCustomerID</span><span class="sxs-lookup"><span data-stu-id="cf67c-123">clientCustomerID</span></span> | <span data-ttu-id="cf67c-124">The Client customer ID of the AdWords account that you want to fetch report data for.</span><span class="sxs-lookup"><span data-stu-id="cf67c-124">The Client customer ID of the AdWords account that you want to fetch report data for.</span></span>  | <span data-ttu-id="cf67c-125">Yes</span><span class="sxs-lookup"><span data-stu-id="cf67c-125">Yes</span></span> |
| <span data-ttu-id="cf67c-126">developerToken</span><span class="sxs-lookup"><span data-stu-id="cf67c-126">developerToken</span></span> | <span data-ttu-id="cf67c-127">The developer token associated with the manager account that you use to grant access to the AdWords API.</span><span class="sxs-lookup"><span data-stu-id="cf67c-127">The developer token associated with the manager account that you use to grant access to the AdWords API.</span></span>  <span data-ttu-id="cf67c-128">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cf67c-128">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="cf67c-129">Yes</span><span class="sxs-lookup"><span data-stu-id="cf67c-129">Yes</span></span> |
| <span data-ttu-id="cf67c-130">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cf67c-130">authenticationType</span></span> | <span data-ttu-id="cf67c-131">The OAuth 2.0 authentication mechanism used for authentication.</span><span class="sxs-lookup"><span data-stu-id="cf67c-131">The OAuth 2.0 authentication mechanism used for authentication.</span></span> <span data-ttu-id="cf67c-132">ServiceAuthentication can only be used on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="cf67c-132">ServiceAuthentication can only be used on self-hosted IR.</span></span> <br/><span data-ttu-id="cf67c-133">Allowed values are: **ServiceAuthentication**, **UserAuthentication**</span><span class="sxs-lookup"><span data-stu-id="cf67c-133">Allowed values are: **ServiceAuthentication**, **UserAuthentication**</span></span> | <span data-ttu-id="cf67c-134">Yes</span><span class="sxs-lookup"><span data-stu-id="cf67c-134">Yes</span></span> |
| <span data-ttu-id="cf67c-135">refreshToken</span><span class="sxs-lookup"><span data-stu-id="cf67c-135">refreshToken</span></span> | <span data-ttu-id="cf67c-136">The refresh token obtained from Google for authorizing access to AdWords for UserAuthentication.</span><span class="sxs-lookup"><span data-stu-id="cf67c-136">The refresh token obtained from Google for authorizing access to AdWords for UserAuthentication.</span></span> <span data-ttu-id="cf67c-137">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cf67c-137">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="cf67c-138">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-138">No</span></span> |
| <span data-ttu-id="cf67c-139">clientId</span><span class="sxs-lookup"><span data-stu-id="cf67c-139">clientId</span></span> | <span data-ttu-id="cf67c-140">The client id of the google application used to acquire the refresh token.</span><span class="sxs-lookup"><span data-stu-id="cf67c-140">The client id of the google application used to acquire the refresh token.</span></span> <span data-ttu-id="cf67c-141">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cf67c-141">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="cf67c-142">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-142">No</span></span> |
| <span data-ttu-id="cf67c-143">clientSecret</span><span class="sxs-lookup"><span data-stu-id="cf67c-143">clientSecret</span></span> | <span data-ttu-id="cf67c-144">The client secret of the google application used to acquire the refresh token.</span><span class="sxs-lookup"><span data-stu-id="cf67c-144">The client secret of the google application used to acquire the refresh token.</span></span> <span data-ttu-id="cf67c-145">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cf67c-145">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="cf67c-146">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-146">No</span></span> |
| <span data-ttu-id="cf67c-147">email</span><span class="sxs-lookup"><span data-stu-id="cf67c-147">email</span></span> | <span data-ttu-id="cf67c-148">The service account email ID that is used for ServiceAuthentication and can only be used on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="cf67c-148">The service account email ID that is used for ServiceAuthentication and can only be used on self-hosted IR.</span></span>  | <span data-ttu-id="cf67c-149">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-149">No</span></span> |
| <span data-ttu-id="cf67c-150">keyFilePath</span><span class="sxs-lookup"><span data-stu-id="cf67c-150">keyFilePath</span></span> | <span data-ttu-id="cf67c-151">The full path to the .p12 key file that is used to authenticate the service account email address and can only be used on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="cf67c-151">The full path to the .p12 key file that is used to authenticate the service account email address and can only be used on self-hosted IR.</span></span>  | <span data-ttu-id="cf67c-152">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-152">No</span></span> |
| <span data-ttu-id="cf67c-153">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="cf67c-153">trustedCertPath</span></span> | <span data-ttu-id="cf67c-154">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="cf67c-154">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span></span> <span data-ttu-id="cf67c-155">This property can only be set when using SSL on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="cf67c-155">This property can only be set when using SSL on self-hosted IR.</span></span> <span data-ttu-id="cf67c-156">The default value is the cacerts.pem file installed with the IR.</span><span class="sxs-lookup"><span data-stu-id="cf67c-156">The default value is the cacerts.pem file installed with the IR.</span></span>  | <span data-ttu-id="cf67c-157">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-157">No</span></span> |
| <span data-ttu-id="cf67c-158">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="cf67c-158">useSystemTrustStore</span></span> | <span data-ttu-id="cf67c-159">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="cf67c-159">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span></span> <span data-ttu-id="cf67c-160">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="cf67c-160">The default value is false.</span></span>  | <span data-ttu-id="cf67c-161">No</span><span class="sxs-lookup"><span data-stu-id="cf67c-161">No</span></span> |

<span data-ttu-id="cf67c-162">**Example:**</span><span class="sxs-lookup"><span data-stu-id="cf67c-162">**Example:**</span></span>

```json
{
    "name": "GoogleAdWordsLinkedService",
    "properties": {
        "type": "GoogleAdWords",
        "typeProperties": {
            "clientCustomerID" : "<clientCustomerID>",
            "developerToken": {
                 "type": "SecureString",
                 "value": "<developerToken>"
            },
            "authenticationType" : "ServiceAuthentication",
            "refreshToken": {
                 "type": "SecureString",
                 "value": "<refreshToken>"
            },
            "clientId": {
                 "type": "SecureString",
                 "value": "<clientId>"
            },
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            },
            "email" : "<email>",
            "keyFilePath" : "<keyFilePath>",
            "trustedCertPath" : "<trustedCertPath>",
            "useSystemTrustStore" : true,
        }
    }
}

```

## <a name="dataset-properties"></a><span data-ttu-id="cf67c-163">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="cf67c-163">Dataset properties</span></span>

<span data-ttu-id="cf67c-164">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="cf67c-164">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="cf67c-165">This section provides a list of properties supported by Google AdWords dataset.</span><span class="sxs-lookup"><span data-stu-id="cf67c-165">This section provides a list of properties supported by Google AdWords dataset.</span></span>

<span data-ttu-id="cf67c-166">To copy data from Google AdWords, set the type property of the dataset to **GoogleAdWordsObject**.</span><span class="sxs-lookup"><span data-stu-id="cf67c-166">To copy data from Google AdWords, set the type property of the dataset to **GoogleAdWordsObject**.</span></span> <span data-ttu-id="cf67c-167">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="cf67c-167">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="cf67c-168">**Example**</span><span class="sxs-lookup"><span data-stu-id="cf67c-168">**Example**</span></span>

```json
{
    "name": "GoogleAdWordsDataset",
    "properties": {
        "type": "GoogleAdWordsObject",
        "linkedServiceName": {
            "referenceName": "<GoogleAdWords linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}

```

## <a name="copy-activity-properties"></a><span data-ttu-id="cf67c-169">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="cf67c-169">Copy activity properties</span></span>

<span data-ttu-id="cf67c-170">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="cf67c-170">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="cf67c-171">This section provides a list of properties supported by Google AdWords source.</span><span class="sxs-lookup"><span data-stu-id="cf67c-171">This section provides a list of properties supported by Google AdWords source.</span></span>

### <a name="google-adwords-as-source"></a><span data-ttu-id="cf67c-172">Google AdWords as source</span><span class="sxs-lookup"><span data-stu-id="cf67c-172">Google AdWords as source</span></span>

<span data-ttu-id="cf67c-173">To copy data from Google AdWords, set the source type in the copy activity to **GoogleAdWordsSource**.</span><span class="sxs-lookup"><span data-stu-id="cf67c-173">To copy data from Google AdWords, set the source type in the copy activity to **GoogleAdWordsSource**.</span></span> <span data-ttu-id="cf67c-174">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="cf67c-174">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="cf67c-175">Property</span><span class="sxs-lookup"><span data-stu-id="cf67c-175">Property</span></span> | <span data-ttu-id="cf67c-176">Description</span><span class="sxs-lookup"><span data-stu-id="cf67c-176">Description</span></span> | <span data-ttu-id="cf67c-177">Required</span><span class="sxs-lookup"><span data-stu-id="cf67c-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="cf67c-178">type</span><span class="sxs-lookup"><span data-stu-id="cf67c-178">type</span></span> | <span data-ttu-id="cf67c-179">The type property of the copy activity source must be set to: **GoogleAdWordsSource**</span><span class="sxs-lookup"><span data-stu-id="cf67c-179">The type property of the copy activity source must be set to: **GoogleAdWordsSource**</span></span> | <span data-ttu-id="cf67c-180">Yes</span><span class="sxs-lookup"><span data-stu-id="cf67c-180">Yes</span></span> |
| <span data-ttu-id="cf67c-181">query</span><span class="sxs-lookup"><span data-stu-id="cf67c-181">query</span></span> | <span data-ttu-id="cf67c-182">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="cf67c-182">Use the custom SQL query to read data.</span></span> <span data-ttu-id="cf67c-183">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="cf67c-183">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="cf67c-184">Yes</span><span class="sxs-lookup"><span data-stu-id="cf67c-184">Yes</span></span> |

<span data-ttu-id="cf67c-185">**Example:**</span><span class="sxs-lookup"><span data-stu-id="cf67c-185">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromGoogleAdWords",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<GoogleAdWords input dataset name>",
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
                "type": "GoogleAdWordsSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="cf67c-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf67c-186">Next steps</span></span>
<span data-ttu-id="cf67c-187">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="cf67c-187">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
