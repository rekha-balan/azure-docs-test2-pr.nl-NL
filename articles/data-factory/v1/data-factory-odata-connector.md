---
title: Move data from OData sources | Microsoft Docs
description: Learn about how to move data from OData sources using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: be2150147d950d708404aff53ce0aa4e0776ac33
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865047"
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="2b0b4-103">Move data From a OData source using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2b0b4-103">Move data From a OData source using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-odata-connector.md)
> * [Version 2 (current version)](../connector-odata.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [OData connector in V2](../connector-odata.md).


<span data-ttu-id="2b0b4-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="2b0b4-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="2b0b4-110">You can copy data from an OData source to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-110">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="2b0b4-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2b0b4-112">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-112">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="2b0b4-113">Supported versions and authentication types</span><span class="sxs-lookup"><span data-stu-id="2b0b4-113">Supported versions and authentication types</span></span>
<span data-ttu-id="2b0b4-114">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-114">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="2b0b4-115">For the latter, you need to install the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-115">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="2b0b4-116">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-116">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="2b0b4-117">Below authentication types are supported:</span><span class="sxs-lookup"><span data-stu-id="2b0b4-117">Below authentication types are supported:</span></span>

* <span data-ttu-id="2b0b4-118">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-118">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="2b0b4-119">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-119">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2b0b4-120">Getting started</span><span class="sxs-lookup"><span data-stu-id="2b0b4-120">Getting started</span></span>
<span data-ttu-id="2b0b4-121">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-121">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="2b0b4-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2b0b4-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="2b0b4-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2b0b4-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2b0b4-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="2b0b4-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="2b0b4-127">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2b0b4-128">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="2b0b4-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2b0b4-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2b0b4-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2b0b4-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2b0b4-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span><span class="sxs-lookup"><span data-stu-id="2b0b4-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2b0b4-134">Linked Service properties</span><span class="sxs-lookup"><span data-stu-id="2b0b4-134">Linked Service properties</span></span>
<span data-ttu-id="2b0b4-135">The following table provides description for JSON elements specific to OData linked service.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-135">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="2b0b4-136">Property</span><span class="sxs-lookup"><span data-stu-id="2b0b4-136">Property</span></span> | <span data-ttu-id="2b0b4-137">Description</span><span class="sxs-lookup"><span data-stu-id="2b0b4-137">Description</span></span> | <span data-ttu-id="2b0b4-138">Required</span><span class="sxs-lookup"><span data-stu-id="2b0b4-138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b0b4-139">type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-139">type</span></span> |<span data-ttu-id="2b0b4-140">The type property must be set to: **OData**</span><span class="sxs-lookup"><span data-stu-id="2b0b4-140">The type property must be set to: **OData**</span></span> |<span data-ttu-id="2b0b4-141">Yes</span><span class="sxs-lookup"><span data-stu-id="2b0b4-141">Yes</span></span> |
| <span data-ttu-id="2b0b4-142">url</span><span class="sxs-lookup"><span data-stu-id="2b0b4-142">url</span></span> |<span data-ttu-id="2b0b4-143">Url of the OData service.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-143">Url of the OData service.</span></span> |<span data-ttu-id="2b0b4-144">Yes</span><span class="sxs-lookup"><span data-stu-id="2b0b4-144">Yes</span></span> |
| <span data-ttu-id="2b0b4-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2b0b4-145">authenticationType</span></span> |<span data-ttu-id="2b0b4-146">Type of authentication used to connect to the OData source.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-146">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="2b0b4-147">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-147">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="2b0b4-148">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-148">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="2b0b4-149">Yes</span><span class="sxs-lookup"><span data-stu-id="2b0b4-149">Yes</span></span> |
| <span data-ttu-id="2b0b4-150">username</span><span class="sxs-lookup"><span data-stu-id="2b0b4-150">username</span></span> |<span data-ttu-id="2b0b4-151">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-151">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="2b0b4-152">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="2b0b4-152">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="2b0b4-153">password</span><span class="sxs-lookup"><span data-stu-id="2b0b4-153">password</span></span> |<span data-ttu-id="2b0b4-154">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-154">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="2b0b4-155">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="2b0b4-155">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="2b0b4-156">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="2b0b4-156">authorizedCredential</span></span> |<span data-ttu-id="2b0b4-157">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-157">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="2b0b4-158">Yes (only if you are using OAuth authentication)</span><span class="sxs-lookup"><span data-stu-id="2b0b4-158">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="2b0b4-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2b0b4-159">gatewayName</span></span> |<span data-ttu-id="2b0b4-160">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-160">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="2b0b4-161">Specify only if you are copying data from on-prem OData source.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-161">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="2b0b4-162">No</span><span class="sxs-lookup"><span data-stu-id="2b0b4-162">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="2b0b4-163">Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="2b0b4-163">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="2b0b4-164">Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="2b0b4-164">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="2b0b4-165">Using Windows authentication accessing on-premises OData source</span><span class="sxs-lookup"><span data-stu-id="2b0b4-165">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="2b0b4-166">Using OAuth authentication accessing cloud OData source</span><span class="sxs-lookup"><span data-stu-id="2b0b4-166">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="2b0b4-167">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="2b0b4-167">Dataset properties</span></span>
<span data-ttu-id="2b0b4-168">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-168">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2b0b4-169">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-169">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2b0b4-170">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-170">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2b0b4-171">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="2b0b4-171">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="2b0b4-172">Property</span><span class="sxs-lookup"><span data-stu-id="2b0b4-172">Property</span></span> | <span data-ttu-id="2b0b4-173">Description</span><span class="sxs-lookup"><span data-stu-id="2b0b4-173">Description</span></span> | <span data-ttu-id="2b0b4-174">Required</span><span class="sxs-lookup"><span data-stu-id="2b0b4-174">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b0b4-175">path</span><span class="sxs-lookup"><span data-stu-id="2b0b4-175">path</span></span> |<span data-ttu-id="2b0b4-176">Path to the OData resource</span><span class="sxs-lookup"><span data-stu-id="2b0b4-176">Path to the OData resource</span></span> |<span data-ttu-id="2b0b4-177">No</span><span class="sxs-lookup"><span data-stu-id="2b0b4-177">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2b0b4-178">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="2b0b4-178">Copy activity properties</span></span>
<span data-ttu-id="2b0b4-179">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-179">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2b0b4-180">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-180">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2b0b4-181">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-181">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="2b0b4-182">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-182">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2b0b4-183">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="2b0b4-183">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2b0b4-184">Property</span><span class="sxs-lookup"><span data-stu-id="2b0b4-184">Property</span></span> | <span data-ttu-id="2b0b4-185">Description</span><span class="sxs-lookup"><span data-stu-id="2b0b4-185">Description</span></span> | <span data-ttu-id="2b0b4-186">Example</span><span class="sxs-lookup"><span data-stu-id="2b0b4-186">Example</span></span> | <span data-ttu-id="2b0b4-187">Required</span><span class="sxs-lookup"><span data-stu-id="2b0b4-187">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2b0b4-188">query</span><span class="sxs-lookup"><span data-stu-id="2b0b4-188">query</span></span> |<span data-ttu-id="2b0b4-189">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-189">Use the custom query to read data.</span></span> |<span data-ttu-id="2b0b4-190">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="2b0b4-190">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="2b0b4-191">No</span><span class="sxs-lookup"><span data-stu-id="2b0b4-191">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="2b0b4-192">Type Mapping for OData</span><span class="sxs-lookup"><span data-stu-id="2b0b4-192">Type Mapping for OData</span></span>
<span data-ttu-id="2b0b4-193">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-193">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="2b0b4-194">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-194">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="2b0b4-195">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-195">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="2b0b4-196">When moving data from OData, the following mappings are used from OData types to .NET type.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-196">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="2b0b4-197">OData Data Type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-197">OData Data Type</span></span> | <span data-ttu-id="2b0b4-198">.NET Type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-198">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="2b0b4-199">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="2b0b4-199">Edm.Binary</span></span> |<span data-ttu-id="2b0b4-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2b0b4-200">Byte[]</span></span> |
| <span data-ttu-id="2b0b4-201">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="2b0b4-201">Edm.Boolean</span></span> |<span data-ttu-id="2b0b4-202">Bool</span><span class="sxs-lookup"><span data-stu-id="2b0b4-202">Bool</span></span> |
| <span data-ttu-id="2b0b4-203">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="2b0b4-203">Edm.Byte</span></span> |<span data-ttu-id="2b0b4-204">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2b0b4-204">Byte[]</span></span> |
| <span data-ttu-id="2b0b4-205">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="2b0b4-205">Edm.DateTime</span></span> |<span data-ttu-id="2b0b4-206">DateTime</span><span class="sxs-lookup"><span data-stu-id="2b0b4-206">DateTime</span></span> |
| <span data-ttu-id="2b0b4-207">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="2b0b4-207">Edm.Decimal</span></span> |<span data-ttu-id="2b0b4-208">Decimal</span><span class="sxs-lookup"><span data-stu-id="2b0b4-208">Decimal</span></span> |
| <span data-ttu-id="2b0b4-209">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="2b0b4-209">Edm.Double</span></span> |<span data-ttu-id="2b0b4-210">Double</span><span class="sxs-lookup"><span data-stu-id="2b0b4-210">Double</span></span> |
| <span data-ttu-id="2b0b4-211">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="2b0b4-211">Edm.Single</span></span> |<span data-ttu-id="2b0b4-212">Single</span><span class="sxs-lookup"><span data-stu-id="2b0b4-212">Single</span></span> |
| <span data-ttu-id="2b0b4-213">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="2b0b4-213">Edm.Guid</span></span> |<span data-ttu-id="2b0b4-214">Guid</span><span class="sxs-lookup"><span data-stu-id="2b0b4-214">Guid</span></span> |
| <span data-ttu-id="2b0b4-215">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="2b0b4-215">Edm.Int16</span></span> |<span data-ttu-id="2b0b4-216">Int16</span><span class="sxs-lookup"><span data-stu-id="2b0b4-216">Int16</span></span> |
| <span data-ttu-id="2b0b4-217">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="2b0b4-217">Edm.Int32</span></span> |<span data-ttu-id="2b0b4-218">Int32</span><span class="sxs-lookup"><span data-stu-id="2b0b4-218">Int32</span></span> |
| <span data-ttu-id="2b0b4-219">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="2b0b4-219">Edm.Int64</span></span> |<span data-ttu-id="2b0b4-220">Int64</span><span class="sxs-lookup"><span data-stu-id="2b0b4-220">Int64</span></span> |
| <span data-ttu-id="2b0b4-221">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="2b0b4-221">Edm.SByte</span></span> |<span data-ttu-id="2b0b4-222">Int16</span><span class="sxs-lookup"><span data-stu-id="2b0b4-222">Int16</span></span> |
| <span data-ttu-id="2b0b4-223">Edm.String</span><span class="sxs-lookup"><span data-stu-id="2b0b4-223">Edm.String</span></span> |<span data-ttu-id="2b0b4-224">String</span><span class="sxs-lookup"><span data-stu-id="2b0b4-224">String</span></span> |
| <span data-ttu-id="2b0b4-225">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="2b0b4-225">Edm.Time</span></span> |<span data-ttu-id="2b0b4-226">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2b0b4-226">TimeSpan</span></span> |
| <span data-ttu-id="2b0b4-227">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="2b0b4-227">Edm.DateTimeOffset</span></span> |<span data-ttu-id="2b0b4-228">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="2b0b4-228">DateTimeOffset</span></span> |

> [!Note]
> OData complex data types e.g. Object are not supported.

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="2b0b4-230">JSON example: Copy data from OData source to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="2b0b4-230">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="2b0b4-231">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-231">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2b0b4-232">They show how to copy data from an OData source to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-232">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="2b0b4-233">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-233">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="2b0b4-234">The sample has the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="2b0b4-234">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="2b0b4-235">A linked service of type [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-235">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="2b0b4-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2b0b4-237">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-237">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="2b0b4-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2b0b4-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2b0b4-240">The sample copies data from querying against an OData source to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-240">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="2b0b4-241">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2b0b4-242">**OData linked service:** This example uses the Anonymous authentication.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-242">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="2b0b4-243">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-243">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="2b0b4-244">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="2b0b4-244">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="2b0b4-245">**OData input dataset:**</span><span class="sxs-lookup"><span data-stu-id="2b0b4-245">**OData input dataset:**</span></span>

<span data-ttu-id="2b0b4-246">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-246">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="2b0b4-247">Specifying **path** in the dataset definition is optional.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-247">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="2b0b4-248">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="2b0b4-248">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2b0b4-249">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-249">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2b0b4-250">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-250">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2b0b4-251">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-251">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="2b0b4-252">**Copy activity in a pipeline with OData source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="2b0b4-252">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="2b0b4-253">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-253">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2b0b4-254">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-254">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="2b0b4-255">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-255">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="2b0b4-256">Specifying **query** in the pipeline definition is optional.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-256">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="2b0b4-257">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-257">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="2b0b4-258">Type mapping for OData</span><span class="sxs-lookup"><span data-stu-id="2b0b4-258">Type mapping for OData</span></span>
<span data-ttu-id="2b0b4-259">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="2b0b4-259">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="2b0b4-260">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-260">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="2b0b4-261">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="2b0b4-261">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="2b0b4-262">When moving data from OData data stores, OData data types are mapped to .NET types.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-262">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="2b0b4-263">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="2b0b4-263">Map source to sink columns</span></span>
<span data-ttu-id="2b0b4-264">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-264">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2b0b4-265">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="2b0b4-265">Repeatable read from relational sources</span></span>
<span data-ttu-id="2b0b4-266">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-266">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="2b0b4-267">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-267">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2b0b4-268">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-268">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2b0b4-269">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-269">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2b0b4-270">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2b0b4-270">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2b0b4-271">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="2b0b4-271">Performance and Tuning</span></span>
<span data-ttu-id="2b0b4-272">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="2b0b4-272">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
