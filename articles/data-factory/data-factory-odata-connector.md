---
title: Move data from OData sources | Microsoft Docs
description: Learn about how to move data from OData sources using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jingwang
ms.openlocfilehash: 2cb8c9b50f3067561c63be194151d6128cd45299
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554565"
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="6d80c-103">Move data From a OData source using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6d80c-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="6d80c-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span><span class="sxs-lookup"><span data-stu-id="6d80c-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="6d80c-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="6d80c-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6d80c-106">You can copy data from an OData source to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="6d80c-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="6d80c-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="6d80c-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6d80c-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span><span class="sxs-lookup"><span data-stu-id="6d80c-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="6d80c-109">Supported versions and authentication types</span><span class="sxs-lookup"><span data-stu-id="6d80c-109">Supported versions and authentication types</span></span>
<span data-ttu-id="6d80c-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span><span class="sxs-lookup"><span data-stu-id="6d80c-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="6d80c-111">For the latter, you need to install the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="6d80c-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="6d80c-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="6d80c-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="6d80c-113">Below authentication types are supported:</span><span class="sxs-lookup"><span data-stu-id="6d80c-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="6d80c-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span><span class="sxs-lookup"><span data-stu-id="6d80c-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="6d80c-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="6d80c-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6d80c-116">Getting started</span><span class="sxs-lookup"><span data-stu-id="6d80c-116">Getting started</span></span>
<span data-ttu-id="6d80c-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="6d80c-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="6d80c-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="6d80c-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6d80c-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="6d80c-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="6d80c-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6d80c-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6d80c-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="6d80c-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6d80c-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="6d80c-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="6d80c-123">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="6d80c-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6d80c-124">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="6d80c-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6d80c-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="6d80c-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6d80c-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="6d80c-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6d80c-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="6d80c-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6d80c-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="6d80c-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6d80c-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span><span class="sxs-lookup"><span data-stu-id="6d80c-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6d80c-130">Linked Service properties</span><span class="sxs-lookup"><span data-stu-id="6d80c-130">Linked Service properties</span></span>
<span data-ttu-id="6d80c-131">The following table provides description for JSON elements specific to OData linked service.</span><span class="sxs-lookup"><span data-stu-id="6d80c-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="6d80c-132">Property</span><span class="sxs-lookup"><span data-stu-id="6d80c-132">Property</span></span> | <span data-ttu-id="6d80c-133">Description</span><span class="sxs-lookup"><span data-stu-id="6d80c-133">Description</span></span> | <span data-ttu-id="6d80c-134">Required</span><span class="sxs-lookup"><span data-stu-id="6d80c-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d80c-135">type</span><span class="sxs-lookup"><span data-stu-id="6d80c-135">type</span></span> |<span data-ttu-id="6d80c-136">The type property must be set to: **OData**</span><span class="sxs-lookup"><span data-stu-id="6d80c-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="6d80c-137">Yes</span><span class="sxs-lookup"><span data-stu-id="6d80c-137">Yes</span></span> |
| <span data-ttu-id="6d80c-138">url</span><span class="sxs-lookup"><span data-stu-id="6d80c-138">url</span></span> |<span data-ttu-id="6d80c-139">Url of the OData service.</span><span class="sxs-lookup"><span data-stu-id="6d80c-139">Url of the OData service.</span></span> |<span data-ttu-id="6d80c-140">Yes</span><span class="sxs-lookup"><span data-stu-id="6d80c-140">Yes</span></span> |
| <span data-ttu-id="6d80c-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6d80c-141">authenticationType</span></span> |<span data-ttu-id="6d80c-142">Type of authentication used to connect to the OData source.</span><span class="sxs-lookup"><span data-stu-id="6d80c-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="6d80c-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span><span class="sxs-lookup"><span data-stu-id="6d80c-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="6d80c-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="6d80c-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6d80c-145">Yes</span><span class="sxs-lookup"><span data-stu-id="6d80c-145">Yes</span></span> |
| <span data-ttu-id="6d80c-146">username</span><span class="sxs-lookup"><span data-stu-id="6d80c-146">username</span></span> |<span data-ttu-id="6d80c-147">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="6d80c-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="6d80c-148">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="6d80c-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="6d80c-149">password</span><span class="sxs-lookup"><span data-stu-id="6d80c-149">password</span></span> |<span data-ttu-id="6d80c-150">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="6d80c-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6d80c-151">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="6d80c-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="6d80c-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="6d80c-152">authorizedCredential</span></span> |<span data-ttu-id="6d80c-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span><span class="sxs-lookup"><span data-stu-id="6d80c-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="6d80c-154">Yes (only if you are using OAuth authentication)</span><span class="sxs-lookup"><span data-stu-id="6d80c-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="6d80c-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6d80c-155">gatewayName</span></span> |<span data-ttu-id="6d80c-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span><span class="sxs-lookup"><span data-stu-id="6d80c-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="6d80c-157">Specify only if you are copying data from on-prem OData source.</span><span class="sxs-lookup"><span data-stu-id="6d80c-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="6d80c-158">No</span><span class="sxs-lookup"><span data-stu-id="6d80c-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="6d80c-159">Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="6d80c-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="6d80c-160">Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="6d80c-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="6d80c-161">Using Windows authentication accessing on-premises OData source</span><span class="sxs-lookup"><span data-stu-id="6d80c-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="6d80c-162">Using OAuth authentication accessing cloud OData source</span><span class="sxs-lookup"><span data-stu-id="6d80c-162">Using OAuth authentication accessing cloud OData source</span></span>
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

## <a name="dataset-properties"></a><span data-ttu-id="6d80c-163">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="6d80c-163">Dataset properties</span></span>
<span data-ttu-id="6d80c-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="6d80c-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6d80c-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="6d80c-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6d80c-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="6d80c-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6d80c-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="6d80c-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="6d80c-168">Property</span><span class="sxs-lookup"><span data-stu-id="6d80c-168">Property</span></span> | <span data-ttu-id="6d80c-169">Description</span><span class="sxs-lookup"><span data-stu-id="6d80c-169">Description</span></span> | <span data-ttu-id="6d80c-170">Required</span><span class="sxs-lookup"><span data-stu-id="6d80c-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d80c-171">path</span><span class="sxs-lookup"><span data-stu-id="6d80c-171">path</span></span> |<span data-ttu-id="6d80c-172">Path to the OData resource</span><span class="sxs-lookup"><span data-stu-id="6d80c-172">Path to the OData resource</span></span> |<span data-ttu-id="6d80c-173">No</span><span class="sxs-lookup"><span data-stu-id="6d80c-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6d80c-174">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="6d80c-174">Copy activity properties</span></span>
<span data-ttu-id="6d80c-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="6d80c-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6d80c-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="6d80c-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="6d80c-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="6d80c-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="6d80c-178">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="6d80c-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6d80c-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="6d80c-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6d80c-180">Property</span><span class="sxs-lookup"><span data-stu-id="6d80c-180">Property</span></span> | <span data-ttu-id="6d80c-181">Description</span><span class="sxs-lookup"><span data-stu-id="6d80c-181">Description</span></span> | <span data-ttu-id="6d80c-182">Example</span><span class="sxs-lookup"><span data-stu-id="6d80c-182">Example</span></span> | <span data-ttu-id="6d80c-183">Required</span><span class="sxs-lookup"><span data-stu-id="6d80c-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6d80c-184">query</span><span class="sxs-lookup"><span data-stu-id="6d80c-184">query</span></span> |<span data-ttu-id="6d80c-185">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="6d80c-185">Use the custom query to read data.</span></span> |<span data-ttu-id="6d80c-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="6d80c-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="6d80c-187">No</span><span class="sxs-lookup"><span data-stu-id="6d80c-187">No</span></span> |

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="6d80c-188">JSON example: Copy data from OData source to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="6d80c-188">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="6d80c-189">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6d80c-189">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6d80c-190">They show how to copy data from an OData source to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="6d80c-190">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="6d80c-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6d80c-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="6d80c-192">The sample has the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="6d80c-192">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="6d80c-193">A linked service of type [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6d80c-193">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="6d80c-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6d80c-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6d80c-195">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6d80c-195">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="6d80c-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6d80c-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6d80c-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6d80c-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6d80c-198">The sample copies data from querying against an OData source to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="6d80c-198">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="6d80c-199">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="6d80c-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6d80c-200">**OData linked service:** This example uses the Anonymous authentication.</span><span class="sxs-lookup"><span data-stu-id="6d80c-200">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="6d80c-201">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="6d80c-201">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="6d80c-202">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="6d80c-202">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="6d80c-203">**OData input dataset:**</span><span class="sxs-lookup"><span data-stu-id="6d80c-203">**OData input dataset:**</span></span>

<span data-ttu-id="6d80c-204">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="6d80c-204">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="6d80c-205">Specifying **path** in the dataset definition is optional.</span><span class="sxs-lookup"><span data-stu-id="6d80c-205">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="6d80c-206">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="6d80c-206">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6d80c-207">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6d80c-207">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6d80c-208">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="6d80c-208">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6d80c-209">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="6d80c-209">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="6d80c-210">**Copy activity in a pipeline with OData source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="6d80c-210">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="6d80c-211">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="6d80c-211">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6d80c-212">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6d80c-212">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="6d80c-213">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span><span class="sxs-lookup"><span data-stu-id="6d80c-213">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

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

<span data-ttu-id="6d80c-214">Specifying **query** in the pipeline definition is optional.</span><span class="sxs-lookup"><span data-stu-id="6d80c-214">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="6d80c-215">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span><span class="sxs-lookup"><span data-stu-id="6d80c-215">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="6d80c-216">Type mapping for OData</span><span class="sxs-lookup"><span data-stu-id="6d80c-216">Type mapping for OData</span></span>
<span data-ttu-id="6d80c-217">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="6d80c-217">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="6d80c-218">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="6d80c-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6d80c-219">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="6d80c-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6d80c-220">When moving data from OData data stores, OData data types are mapped to .NET types.</span><span class="sxs-lookup"><span data-stu-id="6d80c-220">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6d80c-221">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="6d80c-221">Map source to sink columns</span></span>
<span data-ttu-id="6d80c-222">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6d80c-222">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6d80c-223">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="6d80c-223">Repeatable read from relational sources</span></span>
<span data-ttu-id="6d80c-224">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="6d80c-224">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6d80c-225">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="6d80c-225">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6d80c-226">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="6d80c-226">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6d80c-227">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="6d80c-227">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6d80c-228">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6d80c-228">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6d80c-229">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="6d80c-229">Performance and Tuning</span></span>
<span data-ttu-id="6d80c-230">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="6d80c-230">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
