---
title: Move data from Salesforce by using Data Factory | Microsoft Docs
description: Learn about how to move data from Salesforce by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: a9dba65591479033a892615ff053eebd0862851e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869434"
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="e668e-103">Move data from Salesforce by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e668e-103">Move data from Salesforce by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-salesforce-connector.md)
> * [Version 2 (current version)](../connector-salesforce.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Salesforce connector in V2](../connector-salesforce.md).


<span data-ttu-id="e668e-108">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="e668e-108">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e668e-109">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span><span class="sxs-lookup"><span data-stu-id="e668e-109">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="e668e-110">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e668e-110">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="e668e-111">Supported versions</span><span class="sxs-lookup"><span data-stu-id="e668e-111">Supported versions</span></span>
<span data-ttu-id="e668e-112">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span><span class="sxs-lookup"><span data-stu-id="e668e-112">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="e668e-113">And it supports copying from Salesforce production, sandbox and custom domain.</span><span class="sxs-lookup"><span data-stu-id="e668e-113">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e668e-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e668e-114">Prerequisites</span></span>
* <span data-ttu-id="e668e-115">API permission must be enabled.</span><span class="sxs-lookup"><span data-stu-id="e668e-115">API permission must be enabled.</span></span> <span data-ttu-id="e668e-116">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="e668e-116">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="e668e-117">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="e668e-117">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="e668e-118">Salesforce request limits</span><span class="sxs-lookup"><span data-stu-id="e668e-118">Salesforce request limits</span></span>
<span data-ttu-id="e668e-119">Salesforce has limits for both total API requests and concurrent API requests.</span><span class="sxs-lookup"><span data-stu-id="e668e-119">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="e668e-120">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e668e-120">Note the following points:</span></span>

- <span data-ttu-id="e668e-121">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span><span class="sxs-lookup"><span data-stu-id="e668e-121">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="e668e-122">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="e668e-122">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="e668e-123">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span><span class="sxs-lookup"><span data-stu-id="e668e-123">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="e668e-124">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span><span class="sxs-lookup"><span data-stu-id="e668e-124">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e668e-125">Getting started</span><span class="sxs-lookup"><span data-stu-id="e668e-125">Getting started</span></span>
<span data-ttu-id="e668e-126">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="e668e-126">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="e668e-127">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="e668e-127">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e668e-128">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="e668e-128">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="e668e-129">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="e668e-129">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e668e-130">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="e668e-130">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e668e-131">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="e668e-131">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="e668e-132">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e668e-132">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="e668e-133">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="e668e-133">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="e668e-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="e668e-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e668e-135">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="e668e-135">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e668e-136">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="e668e-136">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e668e-137">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="e668e-137">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e668e-138">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span><span class="sxs-lookup"><span data-stu-id="e668e-138">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e668e-139">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="e668e-139">Linked service properties</span></span>
<span data-ttu-id="e668e-140">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span><span class="sxs-lookup"><span data-stu-id="e668e-140">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="e668e-141">Property</span><span class="sxs-lookup"><span data-stu-id="e668e-141">Property</span></span> | <span data-ttu-id="e668e-142">Description</span><span class="sxs-lookup"><span data-stu-id="e668e-142">Description</span></span> | <span data-ttu-id="e668e-143">Required</span><span class="sxs-lookup"><span data-stu-id="e668e-143">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e668e-144">type</span><span class="sxs-lookup"><span data-stu-id="e668e-144">type</span></span> |<span data-ttu-id="e668e-145">The type property must be set to: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="e668e-145">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="e668e-146">Yes</span><span class="sxs-lookup"><span data-stu-id="e668e-146">Yes</span></span> |
| <span data-ttu-id="e668e-147">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="e668e-147">environmentUrl</span></span> | <span data-ttu-id="e668e-148">Specify the URL of Salesforce instance.</span><span class="sxs-lookup"><span data-stu-id="e668e-148">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="e668e-149">- Default is "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="e668e-149">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="e668e-150">- To copy data from sandbox, specify "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="e668e-150">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="e668e-151">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="e668e-151">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="e668e-152">No</span><span class="sxs-lookup"><span data-stu-id="e668e-152">No</span></span> |
| <span data-ttu-id="e668e-153">username</span><span class="sxs-lookup"><span data-stu-id="e668e-153">username</span></span> |<span data-ttu-id="e668e-154">Specify a user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="e668e-154">Specify a user name for the user account.</span></span> |<span data-ttu-id="e668e-155">Yes</span><span class="sxs-lookup"><span data-stu-id="e668e-155">Yes</span></span> |
| <span data-ttu-id="e668e-156">password</span><span class="sxs-lookup"><span data-stu-id="e668e-156">password</span></span> |<span data-ttu-id="e668e-157">Specify a password for the user account.</span><span class="sxs-lookup"><span data-stu-id="e668e-157">Specify a password for the user account.</span></span> |<span data-ttu-id="e668e-158">Yes</span><span class="sxs-lookup"><span data-stu-id="e668e-158">Yes</span></span> |
| <span data-ttu-id="e668e-159">securityToken</span><span class="sxs-lookup"><span data-stu-id="e668e-159">securityToken</span></span> |<span data-ttu-id="e668e-160">Specify a security token for the user account.</span><span class="sxs-lookup"><span data-stu-id="e668e-160">Specify a security token for the user account.</span></span> <span data-ttu-id="e668e-161">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span><span class="sxs-lookup"><span data-stu-id="e668e-161">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="e668e-162">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="e668e-162">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="e668e-163">Yes</span><span class="sxs-lookup"><span data-stu-id="e668e-163">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e668e-164">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="e668e-164">Dataset properties</span></span>
<span data-ttu-id="e668e-165">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="e668e-165">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e668e-166">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span><span class="sxs-lookup"><span data-stu-id="e668e-166">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="e668e-167">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="e668e-167">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e668e-168">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="e668e-168">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="e668e-169">Property</span><span class="sxs-lookup"><span data-stu-id="e668e-169">Property</span></span> | <span data-ttu-id="e668e-170">Description</span><span class="sxs-lookup"><span data-stu-id="e668e-170">Description</span></span> | <span data-ttu-id="e668e-171">Required</span><span class="sxs-lookup"><span data-stu-id="e668e-171">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e668e-172">tableName</span><span class="sxs-lookup"><span data-stu-id="e668e-172">tableName</span></span> |<span data-ttu-id="e668e-173">Name of the table in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e668e-173">Name of the table in Salesforce.</span></span> |<span data-ttu-id="e668e-174">No (if a **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="e668e-174">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> The "__c" part of the API Name is needed for any custom object.

![Data Factory - Salesforce connection - API name](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="e668e-177">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="e668e-177">Copy activity properties</span></span>
<span data-ttu-id="e668e-178">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="e668e-178">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e668e-179">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="e668e-179">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="e668e-180">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="e668e-180">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="e668e-181">For Copy Activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="e668e-181">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="e668e-182">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="e668e-182">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="e668e-183">Property</span><span class="sxs-lookup"><span data-stu-id="e668e-183">Property</span></span> | <span data-ttu-id="e668e-184">Description</span><span class="sxs-lookup"><span data-stu-id="e668e-184">Description</span></span> | <span data-ttu-id="e668e-185">Allowed values</span><span class="sxs-lookup"><span data-stu-id="e668e-185">Allowed values</span></span> | <span data-ttu-id="e668e-186">Required</span><span class="sxs-lookup"><span data-stu-id="e668e-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e668e-187">query</span><span class="sxs-lookup"><span data-stu-id="e668e-187">query</span></span> |<span data-ttu-id="e668e-188">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="e668e-188">Use the custom query to read data.</span></span> |<span data-ttu-id="e668e-189">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span><span class="sxs-lookup"><span data-stu-id="e668e-189">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="e668e-190">For example:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="e668e-190">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="e668e-191">No (if the **tableName** of the **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="e668e-191">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> The "__c" part of the API Name is needed for any custom object.

![Data Factory - Salesforce connection - API name](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="e668e-194">Query tips</span><span class="sxs-lookup"><span data-stu-id="e668e-194">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="e668e-195">Retrieving data using where clause on DateTime column</span><span class="sxs-lookup"><span data-stu-id="e668e-195">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="e668e-196">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span><span class="sxs-lookup"><span data-stu-id="e668e-196">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="e668e-197">For example:</span><span class="sxs-lookup"><span data-stu-id="e668e-197">For example:</span></span>

* <span data-ttu-id="e668e-198">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="e668e-198">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="e668e-199">**SQL sample**:</span><span class="sxs-lookup"><span data-stu-id="e668e-199">**SQL sample**:</span></span>
    * <span data-ttu-id="e668e-200">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="e668e-200">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="e668e-201">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="e668e-201">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="e668e-202">Retrieving data from Salesforce Report</span><span class="sxs-lookup"><span data-stu-id="e668e-202">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="e668e-203">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span><span class="sxs-lookup"><span data-stu-id="e668e-203">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="e668e-204">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="e668e-204">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="e668e-205">Retrieving deleted records from Salesforce Recycle Bin</span><span class="sxs-lookup"><span data-stu-id="e668e-205">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="e668e-206">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span><span class="sxs-lookup"><span data-stu-id="e668e-206">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="e668e-207">For example,</span><span class="sxs-lookup"><span data-stu-id="e668e-207">For example,</span></span>

* <span data-ttu-id="e668e-208">To query only the deleted records, specify "select \* from MyTable__c **where IsDeleted= 1**"</span><span class="sxs-lookup"><span data-stu-id="e668e-208">To query only the deleted records, specify "select \* from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="e668e-209">To query all the records including the existing and the deleted, specify "select \* from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="e668e-209">To query all the records including the existing and the deleted, specify "select \* from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="e668e-210">JSON example: Copy data from Salesforce to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e668e-210">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="e668e-211">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e668e-211">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e668e-212">They show how to copy data from Salesforce to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e668e-212">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="e668e-213">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e668e-213">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="e668e-214">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span><span class="sxs-lookup"><span data-stu-id="e668e-214">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="e668e-215">The sections that follow the list provide details about these steps.</span><span class="sxs-lookup"><span data-stu-id="e668e-215">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="e668e-216">A linked service of the type [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="e668e-216">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="e668e-217">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="e668e-217">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="e668e-218">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="e668e-218">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="e668e-219">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="e668e-219">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="e668e-220">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="e668e-220">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="e668e-221">**Salesforce linked service**</span><span class="sxs-lookup"><span data-stu-id="e668e-221">**Salesforce linked service**</span></span>

<span data-ttu-id="e668e-222">This example uses the **Salesforce** linked service.</span><span class="sxs-lookup"><span data-stu-id="e668e-222">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="e668e-223">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="e668e-223">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="e668e-224">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span><span class="sxs-lookup"><span data-stu-id="e668e-224">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="e668e-225">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="e668e-225">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="e668e-226">**Salesforce input dataset**</span><span class="sxs-lookup"><span data-stu-id="e668e-226">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

<span data-ttu-id="e668e-227">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="e668e-227">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> The "__c" part of the API Name is needed for any custom object.

![Data Factory - Salesforce connection - API name](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="e668e-230">**Azure blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="e668e-230">**Azure blob output dataset**</span></span>

<span data-ttu-id="e668e-231">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e668e-231">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="e668e-232">**Pipeline with Copy Activity**</span><span class="sxs-lookup"><span data-stu-id="e668e-232">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="e668e-233">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="e668e-233">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="e668e-234">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e668e-234">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="e668e-235">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="e668e-235">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> The "__c" part of the API Name is needed for any custom object.

![Data Factory - Salesforce connection - API name](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="e668e-238">Type mapping for Salesforce</span><span class="sxs-lookup"><span data-stu-id="e668e-238">Type mapping for Salesforce</span></span>
| <span data-ttu-id="e668e-239">Salesforce type</span><span class="sxs-lookup"><span data-stu-id="e668e-239">Salesforce type</span></span> | <span data-ttu-id="e668e-240">.NET-based type</span><span class="sxs-lookup"><span data-stu-id="e668e-240">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="e668e-241">Auto Number</span><span class="sxs-lookup"><span data-stu-id="e668e-241">Auto Number</span></span> |<span data-ttu-id="e668e-242">String</span><span class="sxs-lookup"><span data-stu-id="e668e-242">String</span></span> |
| <span data-ttu-id="e668e-243">Checkbox</span><span class="sxs-lookup"><span data-stu-id="e668e-243">Checkbox</span></span> |<span data-ttu-id="e668e-244">Boolean</span><span class="sxs-lookup"><span data-stu-id="e668e-244">Boolean</span></span> |
| <span data-ttu-id="e668e-245">Currency</span><span class="sxs-lookup"><span data-stu-id="e668e-245">Currency</span></span> |<span data-ttu-id="e668e-246">Decimal</span><span class="sxs-lookup"><span data-stu-id="e668e-246">Decimal</span></span> |
| <span data-ttu-id="e668e-247">Date</span><span class="sxs-lookup"><span data-stu-id="e668e-247">Date</span></span> |<span data-ttu-id="e668e-248">DateTime</span><span class="sxs-lookup"><span data-stu-id="e668e-248">DateTime</span></span> |
| <span data-ttu-id="e668e-249">Date/Time</span><span class="sxs-lookup"><span data-stu-id="e668e-249">Date/Time</span></span> |<span data-ttu-id="e668e-250">DateTime</span><span class="sxs-lookup"><span data-stu-id="e668e-250">DateTime</span></span> |
| <span data-ttu-id="e668e-251">Email</span><span class="sxs-lookup"><span data-stu-id="e668e-251">Email</span></span> |<span data-ttu-id="e668e-252">String</span><span class="sxs-lookup"><span data-stu-id="e668e-252">String</span></span> |
| <span data-ttu-id="e668e-253">Id</span><span class="sxs-lookup"><span data-stu-id="e668e-253">Id</span></span> |<span data-ttu-id="e668e-254">String</span><span class="sxs-lookup"><span data-stu-id="e668e-254">String</span></span> |
| <span data-ttu-id="e668e-255">Lookup Relationship</span><span class="sxs-lookup"><span data-stu-id="e668e-255">Lookup Relationship</span></span> |<span data-ttu-id="e668e-256">String</span><span class="sxs-lookup"><span data-stu-id="e668e-256">String</span></span> |
| <span data-ttu-id="e668e-257">Multi-Select Picklist</span><span class="sxs-lookup"><span data-stu-id="e668e-257">Multi-Select Picklist</span></span> |<span data-ttu-id="e668e-258">String</span><span class="sxs-lookup"><span data-stu-id="e668e-258">String</span></span> |
| <span data-ttu-id="e668e-259">Number</span><span class="sxs-lookup"><span data-stu-id="e668e-259">Number</span></span> |<span data-ttu-id="e668e-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="e668e-260">Decimal</span></span> |
| <span data-ttu-id="e668e-261">Percent</span><span class="sxs-lookup"><span data-stu-id="e668e-261">Percent</span></span> |<span data-ttu-id="e668e-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="e668e-262">Decimal</span></span> |
| <span data-ttu-id="e668e-263">Phone</span><span class="sxs-lookup"><span data-stu-id="e668e-263">Phone</span></span> |<span data-ttu-id="e668e-264">String</span><span class="sxs-lookup"><span data-stu-id="e668e-264">String</span></span> |
| <span data-ttu-id="e668e-265">Picklist</span><span class="sxs-lookup"><span data-stu-id="e668e-265">Picklist</span></span> |<span data-ttu-id="e668e-266">String</span><span class="sxs-lookup"><span data-stu-id="e668e-266">String</span></span> |
| <span data-ttu-id="e668e-267">Text</span><span class="sxs-lookup"><span data-stu-id="e668e-267">Text</span></span> |<span data-ttu-id="e668e-268">String</span><span class="sxs-lookup"><span data-stu-id="e668e-268">String</span></span> |
| <span data-ttu-id="e668e-269">Text Area</span><span class="sxs-lookup"><span data-stu-id="e668e-269">Text Area</span></span> |<span data-ttu-id="e668e-270">String</span><span class="sxs-lookup"><span data-stu-id="e668e-270">String</span></span> |
| <span data-ttu-id="e668e-271">Text Area (Long)</span><span class="sxs-lookup"><span data-stu-id="e668e-271">Text Area (Long)</span></span> |<span data-ttu-id="e668e-272">String</span><span class="sxs-lookup"><span data-stu-id="e668e-272">String</span></span> |
| <span data-ttu-id="e668e-273">Text Area (Rich)</span><span class="sxs-lookup"><span data-stu-id="e668e-273">Text Area (Rich)</span></span> |<span data-ttu-id="e668e-274">String</span><span class="sxs-lookup"><span data-stu-id="e668e-274">String</span></span> |
| <span data-ttu-id="e668e-275">Text (Encrypted)</span><span class="sxs-lookup"><span data-stu-id="e668e-275">Text (Encrypted)</span></span> |<span data-ttu-id="e668e-276">String</span><span class="sxs-lookup"><span data-stu-id="e668e-276">String</span></span> |
| <span data-ttu-id="e668e-277">URL</span><span class="sxs-lookup"><span data-stu-id="e668e-277">URL</span></span> |<span data-ttu-id="e668e-278">String</span><span class="sxs-lookup"><span data-stu-id="e668e-278">String</span></span> |

> [!NOTE]
> To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="e668e-280">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="e668e-280">Performance and tuning</span></span>
<span data-ttu-id="e668e-281">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="e668e-281">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
