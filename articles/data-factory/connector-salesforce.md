---
title: Copy data from and to Salesforce by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Salesforce to supported sink data stores or from supported source data stores to Salesforce by using a copy activity in a data factory pipeline.
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
ms.date: 08/21/2018
ms.author: jingwang
ms.openlocfilehash: 56f1721240d4b685133149d50dd7c2a0e6b7e974
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857195"
---
# <a name="copy-data-from-and-to-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="ab02c-103">Copy data from and to Salesforce by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ab02c-103">Copy data from and to Salesforce by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-salesforce-connector.md)
> * [Current version](connector-salesforce.md)

<span data-ttu-id="ab02c-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data from and to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ab02c-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data from and to Salesforce.</span></span> <span data-ttu-id="ab02c-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span><span class="sxs-lookup"><span data-stu-id="ab02c-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="ab02c-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="ab02c-108">Supported capabilities</span></span>

<span data-ttu-id="ab02c-109">You can copy data from Salesforce to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="ab02c-109">You can copy data from Salesforce to any supported sink data store.</span></span> <span data-ttu-id="ab02c-110">You also can copy data from any supported source data store to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ab02c-110">You also can copy data from any supported source data store to Salesforce.</span></span> <span data-ttu-id="ab02c-111">For a list of data stores that are supported as sources or sinks by the Copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="ab02c-111">For a list of data stores that are supported as sources or sinks by the Copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="ab02c-112">Specifically, this Salesforce connector supports:</span><span class="sxs-lookup"><span data-stu-id="ab02c-112">Specifically, this Salesforce connector supports:</span></span>

- <span data-ttu-id="ab02c-113">Salesforce Developer, Professional, Enterprise, or Unlimited editions.</span><span class="sxs-lookup"><span data-stu-id="ab02c-113">Salesforce Developer, Professional, Enterprise, or Unlimited editions.</span></span>
- <span data-ttu-id="ab02c-114">Copying data from and to Salesforce production, sandbox, and custom domain.</span><span class="sxs-lookup"><span data-stu-id="ab02c-114">Copying data from and to Salesforce production, sandbox, and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab02c-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab02c-115">Prerequisites</span></span>

<span data-ttu-id="ab02c-116">API permission must be enabled in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ab02c-116">API permission must be enabled in Salesforce.</span></span> <span data-ttu-id="ab02c-117">For more information, see [Enable API access in Salesforce by permission set](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="ab02c-117">For more information, see [Enable API access in Salesforce by permission set](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="ab02c-118">Salesforce request limits</span><span class="sxs-lookup"><span data-stu-id="ab02c-118">Salesforce request limits</span></span>

<span data-ttu-id="ab02c-119">Salesforce has limits for both total API requests and concurrent API requests.</span><span class="sxs-lookup"><span data-stu-id="ab02c-119">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="ab02c-120">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="ab02c-120">Note the following points:</span></span>

- <span data-ttu-id="ab02c-121">If the number of concurrent requests exceeds the limit, throttling occurs and you see random failures.</span><span class="sxs-lookup"><span data-stu-id="ab02c-121">If the number of concurrent requests exceeds the limit, throttling occurs and you see random failures.</span></span>
- <span data-ttu-id="ab02c-122">If the total number of requests exceeds the limit, the Salesforce account is blocked for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="ab02c-122">If the total number of requests exceeds the limit, the Salesforce account is blocked for 24 hours.</span></span>

<span data-ttu-id="ab02c-123">You might also receive the "REQUEST_LIMIT_EXCEEDED" error message in both scenarios.</span><span class="sxs-lookup"><span data-stu-id="ab02c-123">You might also receive the "REQUEST_LIMIT_EXCEEDED" error message in both scenarios.</span></span> <span data-ttu-id="ab02c-124">For more information, see the "API request limits" section in [Salesforce developer limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf).</span><span class="sxs-lookup"><span data-stu-id="ab02c-124">For more information, see the "API request limits" section in [Salesforce developer limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf).</span></span>

## <a name="get-started"></a><span data-ttu-id="ab02c-125">Get started</span><span class="sxs-lookup"><span data-stu-id="ab02c-125">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="ab02c-126">The following sections provide details about properties that are used to define Data Factory entities specific to the Salesforce connector.</span><span class="sxs-lookup"><span data-stu-id="ab02c-126">The following sections provide details about properties that are used to define Data Factory entities specific to the Salesforce connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ab02c-127">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="ab02c-127">Linked service properties</span></span>

<span data-ttu-id="ab02c-128">The following properties are supported for the Salesforce linked service.</span><span class="sxs-lookup"><span data-stu-id="ab02c-128">The following properties are supported for the Salesforce linked service.</span></span>

| <span data-ttu-id="ab02c-129">Property</span><span class="sxs-lookup"><span data-stu-id="ab02c-129">Property</span></span> | <span data-ttu-id="ab02c-130">Description</span><span class="sxs-lookup"><span data-stu-id="ab02c-130">Description</span></span> | <span data-ttu-id="ab02c-131">Required</span><span class="sxs-lookup"><span data-stu-id="ab02c-131">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab02c-132">type</span><span class="sxs-lookup"><span data-stu-id="ab02c-132">type</span></span> |<span data-ttu-id="ab02c-133">The type property must be set to **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-133">The type property must be set to **Salesforce**.</span></span> |<span data-ttu-id="ab02c-134">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-134">Yes</span></span> |
| <span data-ttu-id="ab02c-135">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="ab02c-135">environmentUrl</span></span> | <span data-ttu-id="ab02c-136">Specify the URL of the Salesforce instance.</span><span class="sxs-lookup"><span data-stu-id="ab02c-136">Specify the URL of the Salesforce instance.</span></span> <br> <span data-ttu-id="ab02c-137">- Default is `"https://login.salesforce.com"`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-137">- Default is `"https://login.salesforce.com"`.</span></span> <br> <span data-ttu-id="ab02c-138">- To copy data from sandbox, specify `"https://test.salesforce.com"`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-138">- To copy data from sandbox, specify `"https://test.salesforce.com"`.</span></span> <br> <span data-ttu-id="ab02c-139">- To copy data from custom domain, specify, for example, `"https://[domain].my.salesforce.com"`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-139">- To copy data from custom domain, specify, for example, `"https://[domain].my.salesforce.com"`.</span></span> |<span data-ttu-id="ab02c-140">No</span><span class="sxs-lookup"><span data-stu-id="ab02c-140">No</span></span> |
| <span data-ttu-id="ab02c-141">username</span><span class="sxs-lookup"><span data-stu-id="ab02c-141">username</span></span> |<span data-ttu-id="ab02c-142">Specify a user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="ab02c-142">Specify a user name for the user account.</span></span> |<span data-ttu-id="ab02c-143">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-143">Yes</span></span> |
| <span data-ttu-id="ab02c-144">password</span><span class="sxs-lookup"><span data-stu-id="ab02c-144">password</span></span> |<span data-ttu-id="ab02c-145">Specify a password for the user account.</span><span class="sxs-lookup"><span data-stu-id="ab02c-145">Specify a password for the user account.</span></span><br/><br/><span data-ttu-id="ab02c-146">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ab02c-146">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="ab02c-147">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-147">Yes</span></span> |
| <span data-ttu-id="ab02c-148">securityToken</span><span class="sxs-lookup"><span data-stu-id="ab02c-148">securityToken</span></span> |<span data-ttu-id="ab02c-149">Specify a security token for the user account.</span><span class="sxs-lookup"><span data-stu-id="ab02c-149">Specify a security token for the user account.</span></span> <span data-ttu-id="ab02c-150">For instructions on how to reset and get a security token, see [Get a security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm).</span><span class="sxs-lookup"><span data-stu-id="ab02c-150">For instructions on how to reset and get a security token, see [Get a security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm).</span></span> <span data-ttu-id="ab02c-151">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="ab02c-151">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span><br/><br/><span data-ttu-id="ab02c-152">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ab02c-152">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="ab02c-153">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-153">Yes</span></span> |
| <span data-ttu-id="ab02c-154">connectVia</span><span class="sxs-lookup"><span data-stu-id="ab02c-154">connectVia</span></span> | <span data-ttu-id="ab02c-155">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="ab02c-155">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="ab02c-156">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="ab02c-156">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="ab02c-157">No for source, Yes for sink if the source linked service doesn't have integration runtime</span><span class="sxs-lookup"><span data-stu-id="ab02c-157">No for source, Yes for sink if the source linked service doesn't have integration runtime</span></span> |

>[!IMPORTANT]
>When you copy data into Salesforce, the default Azure Integration Runtime can't be used to execute copy. In other words, if your source linked service doesn't have a specified integration runtime, explicitly [create an Azure Integration Runtime](create-azure-integration-runtime.md#create-azure-ir) with a location near your Salesforce instance. Associate the Salesforce linked service as in the following example.

<span data-ttu-id="ab02c-161">**Example: Store credentials in Data Factory**</span><span class="sxs-lookup"><span data-stu-id="ab02c-161">**Example: Store credentials in Data Factory**</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            },
            "securityToken": {
                "type": "SecureString",
                "value": "<security token>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="ab02c-162">**Example: Store credentials in Key Vault**</span><span class="sxs-lookup"><span data-stu-id="ab02c-162">**Example: Store credentials in Key Vault**</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of password in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            },
            "securityToken": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of security token in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="ab02c-163">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="ab02c-163">Dataset properties</span></span>

<span data-ttu-id="ab02c-164">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="ab02c-164">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="ab02c-165">This section provides a list of properties supported by the Salesforce dataset.</span><span class="sxs-lookup"><span data-stu-id="ab02c-165">This section provides a list of properties supported by the Salesforce dataset.</span></span>

<span data-ttu-id="ab02c-166">To copy data from and to Salesforce, set the type property of the dataset to **SalesforceObject**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-166">To copy data from and to Salesforce, set the type property of the dataset to **SalesforceObject**.</span></span> <span data-ttu-id="ab02c-167">The following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="ab02c-167">The following properties are supported.</span></span>

| <span data-ttu-id="ab02c-168">Property</span><span class="sxs-lookup"><span data-stu-id="ab02c-168">Property</span></span> | <span data-ttu-id="ab02c-169">Description</span><span class="sxs-lookup"><span data-stu-id="ab02c-169">Description</span></span> | <span data-ttu-id="ab02c-170">Required</span><span class="sxs-lookup"><span data-stu-id="ab02c-170">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab02c-171">type</span><span class="sxs-lookup"><span data-stu-id="ab02c-171">type</span></span> | <span data-ttu-id="ab02c-172">The type property must be set to **SalesforceObject**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-172">The type property must be set to **SalesforceObject**.</span></span>  | <span data-ttu-id="ab02c-173">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-173">Yes</span></span> |
| <span data-ttu-id="ab02c-174">objectApiName</span><span class="sxs-lookup"><span data-stu-id="ab02c-174">objectApiName</span></span> | <span data-ttu-id="ab02c-175">The Salesforce object name to retrieve data from.</span><span class="sxs-lookup"><span data-stu-id="ab02c-175">The Salesforce object name to retrieve data from.</span></span> | <span data-ttu-id="ab02c-176">No for source, Yes for sink</span><span class="sxs-lookup"><span data-stu-id="ab02c-176">No for source, Yes for sink</span></span> |

> [!IMPORTANT]
> The "__c" part of **API Name** is needed for any custom object.

![Data Factory Salesforce connection API Name](media/copy-data-from-salesforce/data-factory-salesforce-api-name.png)

<span data-ttu-id="ab02c-179">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ab02c-179">**Example:**</span></span>

```json
{
    "name": "SalesforceDataset",
    "properties": {
        "type": "SalesforceObject",
        "linkedServiceName": {
            "referenceName": "<Salesforce linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "objectApiName": "MyTable__c"
        }
    }
}
```

>[!NOTE]
>For backward compatibility: When you copy data from Salesforce, if you use the previous "RelationalTable" type dataset, it keeps working while you see a suggestion to switch to the new "SalesforceObject" type.

| <span data-ttu-id="ab02c-181">Property</span><span class="sxs-lookup"><span data-stu-id="ab02c-181">Property</span></span> | <span data-ttu-id="ab02c-182">Description</span><span class="sxs-lookup"><span data-stu-id="ab02c-182">Description</span></span> | <span data-ttu-id="ab02c-183">Required</span><span class="sxs-lookup"><span data-stu-id="ab02c-183">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab02c-184">type</span><span class="sxs-lookup"><span data-stu-id="ab02c-184">type</span></span> | <span data-ttu-id="ab02c-185">The type property of the dataset must be set to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-185">The type property of the dataset must be set to **RelationalTable**.</span></span> | <span data-ttu-id="ab02c-186">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-186">Yes</span></span> |
| <span data-ttu-id="ab02c-187">tableName</span><span class="sxs-lookup"><span data-stu-id="ab02c-187">tableName</span></span> | <span data-ttu-id="ab02c-188">Name of the table in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ab02c-188">Name of the table in Salesforce.</span></span> | <span data-ttu-id="ab02c-189">No (if "query" in the activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="ab02c-189">No (if "query" in the activity source is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ab02c-190">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="ab02c-190">Copy activity properties</span></span>

<span data-ttu-id="ab02c-191">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="ab02c-191">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="ab02c-192">This section provides a list of properties supported by Salesforce source and sink.</span><span class="sxs-lookup"><span data-stu-id="ab02c-192">This section provides a list of properties supported by Salesforce source and sink.</span></span>

### <a name="salesforce-as-a-source-type"></a><span data-ttu-id="ab02c-193">Salesforce as a source type</span><span class="sxs-lookup"><span data-stu-id="ab02c-193">Salesforce as a source type</span></span>

<span data-ttu-id="ab02c-194">To copy data from Salesforce, set the source type in the copy activity to **SalesforceSource**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-194">To copy data from Salesforce, set the source type in the copy activity to **SalesforceSource**.</span></span> <span data-ttu-id="ab02c-195">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="ab02c-195">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="ab02c-196">Property</span><span class="sxs-lookup"><span data-stu-id="ab02c-196">Property</span></span> | <span data-ttu-id="ab02c-197">Description</span><span class="sxs-lookup"><span data-stu-id="ab02c-197">Description</span></span> | <span data-ttu-id="ab02c-198">Required</span><span class="sxs-lookup"><span data-stu-id="ab02c-198">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab02c-199">type</span><span class="sxs-lookup"><span data-stu-id="ab02c-199">type</span></span> | <span data-ttu-id="ab02c-200">The type property of the copy activity source must be set to **SalesforceSource**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-200">The type property of the copy activity source must be set to **SalesforceSource**.</span></span> | <span data-ttu-id="ab02c-201">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-201">Yes</span></span> |
| <span data-ttu-id="ab02c-202">query</span><span class="sxs-lookup"><span data-stu-id="ab02c-202">query</span></span> |<span data-ttu-id="ab02c-203">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="ab02c-203">Use the custom query to read data.</span></span> <span data-ttu-id="ab02c-204">You can use [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query or SQL-92 query.</span><span class="sxs-lookup"><span data-stu-id="ab02c-204">You can use [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query or SQL-92 query.</span></span> <span data-ttu-id="ab02c-205">See more tips in [query tips](#query-tips) section.</span><span class="sxs-lookup"><span data-stu-id="ab02c-205">See more tips in [query tips](#query-tips) section.</span></span> | <span data-ttu-id="ab02c-206">No (if "tableName" in the dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="ab02c-206">No (if "tableName" in the dataset is specified)</span></span> |
| <span data-ttu-id="ab02c-207">readBehavior</span><span class="sxs-lookup"><span data-stu-id="ab02c-207">readBehavior</span></span> | <span data-ttu-id="ab02c-208">Indicates whether to query the existing records, or query all records including the deleted ones.</span><span class="sxs-lookup"><span data-stu-id="ab02c-208">Indicates whether to query the existing records, or query all records including the deleted ones.</span></span> <span data-ttu-id="ab02c-209">If not specified, the default behavior is the former.</span><span class="sxs-lookup"><span data-stu-id="ab02c-209">If not specified, the default behavior is the former.</span></span> <br><span data-ttu-id="ab02c-210">Allowed values: **query** (default), **queryAll**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-210">Allowed values: **query** (default), **queryAll**.</span></span>  | <span data-ttu-id="ab02c-211">No</span><span class="sxs-lookup"><span data-stu-id="ab02c-211">No</span></span> |

> [!IMPORTANT]
> The "__c" part of **API Name** is needed for any custom object.

![Data Factory Salesforce connection API Name list](media/copy-data-from-salesforce/data-factory-salesforce-api-name-2.png)

<span data-ttu-id="ab02c-214">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ab02c-214">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Salesforce input dataset name>",
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
                "type": "SalesforceSource",
                "query": "SELECT Col_Currency__c, Col_Date__c, Col_Email__c FROM AllDataType__c"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

>[!NOTE]
>For backward compatibility: When you copy data from Salesforce, if you use the previous "RelationalSource" type copy, the source keeps working while you see a suggestion to switch to the new "SalesforceSource" type.

### <a name="salesforce-as-a-sink-type"></a><span data-ttu-id="ab02c-216">Salesforce as a sink type</span><span class="sxs-lookup"><span data-stu-id="ab02c-216">Salesforce as a sink type</span></span>

<span data-ttu-id="ab02c-217">To copy data to Salesforce, set the sink type in the copy activity to **SalesforceSink**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-217">To copy data to Salesforce, set the sink type in the copy activity to **SalesforceSink**.</span></span> <span data-ttu-id="ab02c-218">The following properties are supported in the copy activity **sink** section.</span><span class="sxs-lookup"><span data-stu-id="ab02c-218">The following properties are supported in the copy activity **sink** section.</span></span>

| <span data-ttu-id="ab02c-219">Property</span><span class="sxs-lookup"><span data-stu-id="ab02c-219">Property</span></span> | <span data-ttu-id="ab02c-220">Description</span><span class="sxs-lookup"><span data-stu-id="ab02c-220">Description</span></span> | <span data-ttu-id="ab02c-221">Required</span><span class="sxs-lookup"><span data-stu-id="ab02c-221">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab02c-222">type</span><span class="sxs-lookup"><span data-stu-id="ab02c-222">type</span></span> | <span data-ttu-id="ab02c-223">The type property of the copy activity sink must be set to **SalesforceSink**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-223">The type property of the copy activity sink must be set to **SalesforceSink**.</span></span> | <span data-ttu-id="ab02c-224">Yes</span><span class="sxs-lookup"><span data-stu-id="ab02c-224">Yes</span></span> |
| <span data-ttu-id="ab02c-225">writeBehavior</span><span class="sxs-lookup"><span data-stu-id="ab02c-225">writeBehavior</span></span> | <span data-ttu-id="ab02c-226">The write behavior for the operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-226">The write behavior for the operation.</span></span><br/><span data-ttu-id="ab02c-227">Allowed values are **Insert** and **Upsert**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-227">Allowed values are **Insert** and **Upsert**.</span></span> | <span data-ttu-id="ab02c-228">No (default is Insert)</span><span class="sxs-lookup"><span data-stu-id="ab02c-228">No (default is Insert)</span></span> |
| <span data-ttu-id="ab02c-229">externalIdFieldName</span><span class="sxs-lookup"><span data-stu-id="ab02c-229">externalIdFieldName</span></span> | <span data-ttu-id="ab02c-230">The name of the external ID field for the upsert operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-230">The name of the external ID field for the upsert operation.</span></span> <span data-ttu-id="ab02c-231">The specified field must be defined as "External Id Field" in the Salesforce object.</span><span class="sxs-lookup"><span data-stu-id="ab02c-231">The specified field must be defined as "External Id Field" in the Salesforce object.</span></span> <span data-ttu-id="ab02c-232">It can't have NULL values in the corresponding input data.</span><span class="sxs-lookup"><span data-stu-id="ab02c-232">It can't have NULL values in the corresponding input data.</span></span> | <span data-ttu-id="ab02c-233">Yes for "Upsert"</span><span class="sxs-lookup"><span data-stu-id="ab02c-233">Yes for "Upsert"</span></span> |
| <span data-ttu-id="ab02c-234">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ab02c-234">writeBatchSize</span></span> | <span data-ttu-id="ab02c-235">The row count of data written to Salesforce in each batch.</span><span class="sxs-lookup"><span data-stu-id="ab02c-235">The row count of data written to Salesforce in each batch.</span></span> | <span data-ttu-id="ab02c-236">No (default is 5,000)</span><span class="sxs-lookup"><span data-stu-id="ab02c-236">No (default is 5,000)</span></span> |
| <span data-ttu-id="ab02c-237">ignoreNullValues</span><span class="sxs-lookup"><span data-stu-id="ab02c-237">ignoreNullValues</span></span> | <span data-ttu-id="ab02c-238">Indicates whether to ignore NULL values from input data during a write operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-238">Indicates whether to ignore NULL values from input data during a write operation.</span></span><br/><span data-ttu-id="ab02c-239">Allowed values are **true** and **false**.</span><span class="sxs-lookup"><span data-stu-id="ab02c-239">Allowed values are **true** and **false**.</span></span><br><span data-ttu-id="ab02c-240">- **True**: Leave the data in the destination object unchanged when you do an upsert or update operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-240">- **True**: Leave the data in the destination object unchanged when you do an upsert or update operation.</span></span> <span data-ttu-id="ab02c-241">Insert a defined default value when you do an insert operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-241">Insert a defined default value when you do an insert operation.</span></span><br/><span data-ttu-id="ab02c-242">- **False**: Update the data in the destination object to NULL when you do an upsert or update operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-242">- **False**: Update the data in the destination object to NULL when you do an upsert or update operation.</span></span> <span data-ttu-id="ab02c-243">Insert a NULL value when you do an insert operation.</span><span class="sxs-lookup"><span data-stu-id="ab02c-243">Insert a NULL value when you do an insert operation.</span></span> | <span data-ttu-id="ab02c-244">No (default is false)</span><span class="sxs-lookup"><span data-stu-id="ab02c-244">No (default is false)</span></span> |

<span data-ttu-id="ab02c-245">**Example: Salesforce sink in a copy activity**</span><span class="sxs-lookup"><span data-stu-id="ab02c-245">**Example: Salesforce sink in a copy activity**</span></span>

```json
"activities":[
    {
        "name": "CopyToSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Salesforce output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SalesforceSink",
                "writeBehavior": "Upsert",
                "externalIdFieldName": "CustomerId__c",
                "writeBatchSize": 10000,
                "ignoreNullValues": true
            }
        }
    }
]
```

## <a name="query-tips"></a><span data-ttu-id="ab02c-246">Query tips</span><span class="sxs-lookup"><span data-stu-id="ab02c-246">Query tips</span></span>

### <a name="retrieve-data-from-a-salesforce-report"></a><span data-ttu-id="ab02c-247">Retrieve data from a Salesforce report</span><span class="sxs-lookup"><span data-stu-id="ab02c-247">Retrieve data from a Salesforce report</span></span>

<span data-ttu-id="ab02c-248">You can retrieve data from Salesforce reports by specifying a query as `{call "<report name>"}`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-248">You can retrieve data from Salesforce reports by specifying a query as `{call "<report name>"}`.</span></span> <span data-ttu-id="ab02c-249">An example is `"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-249">An example is `"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieve-deleted-records-from-the-salesforce-recycle-bin"></a><span data-ttu-id="ab02c-250">Retrieve deleted records from the Salesforce Recycle Bin</span><span class="sxs-lookup"><span data-stu-id="ab02c-250">Retrieve deleted records from the Salesforce Recycle Bin</span></span>

<span data-ttu-id="ab02c-251">To query the soft deleted records from the Salesforce Recycle Bin, you can specify `readBehavior` as `queryAll`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-251">To query the soft deleted records from the Salesforce Recycle Bin, you can specify `readBehavior` as `queryAll`.</span></span> 

### <a name="difference-between-soql-and-sql-query-syntax"></a><span data-ttu-id="ab02c-252">Difference between SOQL and SQL query syntax</span><span class="sxs-lookup"><span data-stu-id="ab02c-252">Difference between SOQL and SQL query syntax</span></span>

<span data-ttu-id="ab02c-253">When copying data from Salesforce, you can use either SOQL query or SQL query.</span><span class="sxs-lookup"><span data-stu-id="ab02c-253">When copying data from Salesforce, you can use either SOQL query or SQL query.</span></span> <span data-ttu-id="ab02c-254">Note that these two has different syntax and functionality support, do not mix it.</span><span class="sxs-lookup"><span data-stu-id="ab02c-254">Note that these two has different syntax and functionality support, do not mix it.</span></span> <span data-ttu-id="ab02c-255">You are suggested to use the SOQL query which is natively supported by Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ab02c-255">You are suggested to use the SOQL query which is natively supported by Salesforce.</span></span> <span data-ttu-id="ab02c-256">The following table lists the main differences:</span><span class="sxs-lookup"><span data-stu-id="ab02c-256">The following table lists the main differences:</span></span>

| <span data-ttu-id="ab02c-257">Syntax</span><span class="sxs-lookup"><span data-stu-id="ab02c-257">Syntax</span></span> | <span data-ttu-id="ab02c-258">SOQL Mode</span><span class="sxs-lookup"><span data-stu-id="ab02c-258">SOQL Mode</span></span> | <span data-ttu-id="ab02c-259">SQL Mode</span><span class="sxs-lookup"><span data-stu-id="ab02c-259">SQL Mode</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab02c-260">Column selection</span><span class="sxs-lookup"><span data-stu-id="ab02c-260">Column selection</span></span> | <span data-ttu-id="ab02c-261">Need to enumarate the fields to be copied in the query, e.g. `SELECT field1, filed2 FROM objectname`</span><span class="sxs-lookup"><span data-stu-id="ab02c-261">Need to enumarate the fields to be copied in the query, e.g. `SELECT field1, filed2 FROM objectname`</span></span> | <span data-ttu-id="ab02c-262">`SELECT *` is supported in addition to column selection.</span><span class="sxs-lookup"><span data-stu-id="ab02c-262">`SELECT *` is supported in addition to column selection.</span></span> |
| <span data-ttu-id="ab02c-263">Quotation marks</span><span class="sxs-lookup"><span data-stu-id="ab02c-263">Quotation marks</span></span> | <span data-ttu-id="ab02c-264">Filed/object names cannot be quoted.</span><span class="sxs-lookup"><span data-stu-id="ab02c-264">Filed/object names cannot be quoted.</span></span> | <span data-ttu-id="ab02c-265">Field/object names can be quoted, e.g. `SELECT "id" FROM "Account"`</span><span class="sxs-lookup"><span data-stu-id="ab02c-265">Field/object names can be quoted, e.g. `SELECT "id" FROM "Account"`</span></span> |
| <span data-ttu-id="ab02c-266">Datetime format</span><span class="sxs-lookup"><span data-stu-id="ab02c-266">Datetime format</span></span> |  <span data-ttu-id="ab02c-267">Refer to details [here](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_dateformats.htm) and samples in next section.</span><span class="sxs-lookup"><span data-stu-id="ab02c-267">Refer to details [here](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_dateformats.htm) and samples in next section.</span></span> | <span data-ttu-id="ab02c-268">Refer to details [here](https://docs.microsoft.com/sql/odbc/reference/develop-app/date-time-and-timestamp-literals?view=sql-server-2017) and samples in next section.</span><span class="sxs-lookup"><span data-stu-id="ab02c-268">Refer to details [here](https://docs.microsoft.com/sql/odbc/reference/develop-app/date-time-and-timestamp-literals?view=sql-server-2017) and samples in next section.</span></span> |
| <span data-ttu-id="ab02c-269">Boolean values</span><span class="sxs-lookup"><span data-stu-id="ab02c-269">Boolean values</span></span> | <span data-ttu-id="ab02c-270">Represented as `False` and `True`, e.g. `SELECT … WHERE IsDeleted=True`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-270">Represented as `False` and `True`, e.g. `SELECT … WHERE IsDeleted=True`.</span></span> | <span data-ttu-id="ab02c-271">Represented as 0 or 1, e.g. `SELECT … WHERE IsDeleted=1`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-271">Represented as 0 or 1, e.g. `SELECT … WHERE IsDeleted=1`.</span></span> |
| <span data-ttu-id="ab02c-272">Column renaming</span><span class="sxs-lookup"><span data-stu-id="ab02c-272">Column renaming</span></span> | <span data-ttu-id="ab02c-273">Not supported.</span><span class="sxs-lookup"><span data-stu-id="ab02c-273">Not supported.</span></span> | <span data-ttu-id="ab02c-274">Supported, e.g.: `SELECT a AS b FROM …`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-274">Supported, e.g.: `SELECT a AS b FROM …`.</span></span> |
| <span data-ttu-id="ab02c-275">Relationship</span><span class="sxs-lookup"><span data-stu-id="ab02c-275">Relationship</span></span> | <span data-ttu-id="ab02c-276">Supported, e.g. `Account_vod__r.nvs_Country__c`.</span><span class="sxs-lookup"><span data-stu-id="ab02c-276">Supported, e.g. `Account_vod__r.nvs_Country__c`.</span></span> | <span data-ttu-id="ab02c-277">Not supported.</span><span class="sxs-lookup"><span data-stu-id="ab02c-277">Not supported.</span></span> |

### <a name="retrieve-data-by-using-a-where-clause-on-the-datetime-column"></a><span data-ttu-id="ab02c-278">Retrieve data by using a where clause on the DateTime column</span><span class="sxs-lookup"><span data-stu-id="ab02c-278">Retrieve data by using a where clause on the DateTime column</span></span>

<span data-ttu-id="ab02c-279">When you specify the SOQL or SQL query, pay attention to the DateTime format difference.</span><span class="sxs-lookup"><span data-stu-id="ab02c-279">When you specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="ab02c-280">For example:</span><span class="sxs-lookup"><span data-stu-id="ab02c-280">For example:</span></span>

* <span data-ttu-id="ab02c-281">**SOQL sample**: `SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= @{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-ddTHH:mm:ssZ')} AND LastModifiedDate < @{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-ddTHH:mm:ssZ')}`</span><span class="sxs-lookup"><span data-stu-id="ab02c-281">**SOQL sample**: `SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= @{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-ddTHH:mm:ssZ')} AND LastModifiedDate < @{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-ddTHH:mm:ssZ')}`</span></span>
* <span data-ttu-id="ab02c-282">**SQL sample**: `SELECT * FROM Account WHERE LastModifiedDate >= {ts'@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}'} AND LastModifiedDate < {ts'@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'}`</span><span class="sxs-lookup"><span data-stu-id="ab02c-282">**SQL sample**: `SELECT * FROM Account WHERE LastModifiedDate >= {ts'@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}'} AND LastModifiedDate < {ts'@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'}`</span></span>

## <a name="data-type-mapping-for-salesforce"></a><span data-ttu-id="ab02c-283">Data type mapping for Salesforce</span><span class="sxs-lookup"><span data-stu-id="ab02c-283">Data type mapping for Salesforce</span></span>

<span data-ttu-id="ab02c-284">When you copy data from Salesforce, the following mappings are used from Salesforce data types to Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="ab02c-284">When you copy data from Salesforce, the following mappings are used from Salesforce data types to Data Factory interim data types.</span></span> <span data-ttu-id="ab02c-285">To learn about how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="ab02c-285">To learn about how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span></span>

| <span data-ttu-id="ab02c-286">Salesforce data type</span><span class="sxs-lookup"><span data-stu-id="ab02c-286">Salesforce data type</span></span> | <span data-ttu-id="ab02c-287">Data Factory interim data type</span><span class="sxs-lookup"><span data-stu-id="ab02c-287">Data Factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab02c-288">Auto Number</span><span class="sxs-lookup"><span data-stu-id="ab02c-288">Auto Number</span></span> |<span data-ttu-id="ab02c-289">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-289">String</span></span> |
| <span data-ttu-id="ab02c-290">Checkbox</span><span class="sxs-lookup"><span data-stu-id="ab02c-290">Checkbox</span></span> |<span data-ttu-id="ab02c-291">Boolean</span><span class="sxs-lookup"><span data-stu-id="ab02c-291">Boolean</span></span> |
| <span data-ttu-id="ab02c-292">Currency</span><span class="sxs-lookup"><span data-stu-id="ab02c-292">Currency</span></span> |<span data-ttu-id="ab02c-293">Decimal</span><span class="sxs-lookup"><span data-stu-id="ab02c-293">Decimal</span></span> |
| <span data-ttu-id="ab02c-294">Date</span><span class="sxs-lookup"><span data-stu-id="ab02c-294">Date</span></span> |<span data-ttu-id="ab02c-295">DateTime</span><span class="sxs-lookup"><span data-stu-id="ab02c-295">DateTime</span></span> |
| <span data-ttu-id="ab02c-296">Date/Time</span><span class="sxs-lookup"><span data-stu-id="ab02c-296">Date/Time</span></span> |<span data-ttu-id="ab02c-297">DateTime</span><span class="sxs-lookup"><span data-stu-id="ab02c-297">DateTime</span></span> |
| <span data-ttu-id="ab02c-298">Email</span><span class="sxs-lookup"><span data-stu-id="ab02c-298">Email</span></span> |<span data-ttu-id="ab02c-299">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-299">String</span></span> |
| <span data-ttu-id="ab02c-300">Id</span><span class="sxs-lookup"><span data-stu-id="ab02c-300">Id</span></span> |<span data-ttu-id="ab02c-301">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-301">String</span></span> |
| <span data-ttu-id="ab02c-302">Lookup Relationship</span><span class="sxs-lookup"><span data-stu-id="ab02c-302">Lookup Relationship</span></span> |<span data-ttu-id="ab02c-303">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-303">String</span></span> |
| <span data-ttu-id="ab02c-304">Multi-Select Picklist</span><span class="sxs-lookup"><span data-stu-id="ab02c-304">Multi-Select Picklist</span></span> |<span data-ttu-id="ab02c-305">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-305">String</span></span> |
| <span data-ttu-id="ab02c-306">Number</span><span class="sxs-lookup"><span data-stu-id="ab02c-306">Number</span></span> |<span data-ttu-id="ab02c-307">Decimal</span><span class="sxs-lookup"><span data-stu-id="ab02c-307">Decimal</span></span> |
| <span data-ttu-id="ab02c-308">Percent</span><span class="sxs-lookup"><span data-stu-id="ab02c-308">Percent</span></span> |<span data-ttu-id="ab02c-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="ab02c-309">Decimal</span></span> |
| <span data-ttu-id="ab02c-310">Phone</span><span class="sxs-lookup"><span data-stu-id="ab02c-310">Phone</span></span> |<span data-ttu-id="ab02c-311">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-311">String</span></span> |
| <span data-ttu-id="ab02c-312">Picklist</span><span class="sxs-lookup"><span data-stu-id="ab02c-312">Picklist</span></span> |<span data-ttu-id="ab02c-313">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-313">String</span></span> |
| <span data-ttu-id="ab02c-314">Text</span><span class="sxs-lookup"><span data-stu-id="ab02c-314">Text</span></span> |<span data-ttu-id="ab02c-315">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-315">String</span></span> |
| <span data-ttu-id="ab02c-316">Text Area</span><span class="sxs-lookup"><span data-stu-id="ab02c-316">Text Area</span></span> |<span data-ttu-id="ab02c-317">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-317">String</span></span> |
| <span data-ttu-id="ab02c-318">Text Area (Long)</span><span class="sxs-lookup"><span data-stu-id="ab02c-318">Text Area (Long)</span></span> |<span data-ttu-id="ab02c-319">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-319">String</span></span> |
| <span data-ttu-id="ab02c-320">Text Area (Rich)</span><span class="sxs-lookup"><span data-stu-id="ab02c-320">Text Area (Rich)</span></span> |<span data-ttu-id="ab02c-321">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-321">String</span></span> |
| <span data-ttu-id="ab02c-322">Text (Encrypted)</span><span class="sxs-lookup"><span data-stu-id="ab02c-322">Text (Encrypted)</span></span> |<span data-ttu-id="ab02c-323">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-323">String</span></span> |
| <span data-ttu-id="ab02c-324">URL</span><span class="sxs-lookup"><span data-stu-id="ab02c-324">URL</span></span> |<span data-ttu-id="ab02c-325">String</span><span class="sxs-lookup"><span data-stu-id="ab02c-325">String</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab02c-326">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab02c-326">Next steps</span></span>
<span data-ttu-id="ab02c-327">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ab02c-327">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
