---
title: Move data from SAP HANA using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from SAP HANA using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: f475135f019994900f39a0a4007e8c4cf49af484
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871615"
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="1ed25-103">Move data From SAP HANA using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1ed25-103">Move data From SAP HANA using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-sap-hana-connector.md)
> * [Version 2 (current version)](../connector-sap-hana.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [SAP HANA connector in V2](../connector-sap-business-warehouse.md).

<span data-ttu-id="1ed25-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1ed25-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="1ed25-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1ed25-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="1ed25-110">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="1ed25-110">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="1ed25-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="1ed25-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1ed25-112">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1ed25-112">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="1ed25-113">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="1ed25-113">Supported versions and installation</span></span>
<span data-ttu-id="1ed25-114">This connector supports any version of SAP HANA database.</span><span class="sxs-lookup"><span data-stu-id="1ed25-114">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="1ed25-115">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span><span class="sxs-lookup"><span data-stu-id="1ed25-115">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="1ed25-116">To enable the connectivity to the SAP HANA instance, install the following components:</span><span class="sxs-lookup"><span data-stu-id="1ed25-116">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="1ed25-117">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1ed25-117">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="1ed25-118">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="1ed25-118">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="1ed25-119">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="1ed25-119">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="1ed25-120">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="1ed25-120">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="1ed25-121">**SAP HANA ODBC driver** on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="1ed25-121">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="1ed25-122">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="1ed25-122">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="1ed25-123">Search with the keyword **SAP HANA CLIENT for Windows**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-123">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="1ed25-124">Getting started</span><span class="sxs-lookup"><span data-stu-id="1ed25-124">Getting started</span></span>
<span data-ttu-id="1ed25-125">You can create a pipeline with a copy activity that moves data from an on-premises SAP HANA data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="1ed25-125">You can create a pipeline with a copy activity that moves data from an on-premises SAP HANA data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="1ed25-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1ed25-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="1ed25-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="1ed25-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1ed25-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="1ed25-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1ed25-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="1ed25-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="1ed25-131">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="1ed25-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1ed25-132">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="1ed25-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="1ed25-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="1ed25-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1ed25-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="1ed25-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1ed25-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="1ed25-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1ed25-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="1ed25-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1ed25-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span><span class="sxs-lookup"><span data-stu-id="1ed25-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1ed25-138">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="1ed25-138">Linked service properties</span></span>
<span data-ttu-id="1ed25-139">The following table provides description for JSON elements specific to SAP HANA linked service.</span><span class="sxs-lookup"><span data-stu-id="1ed25-139">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="1ed25-140">Property</span><span class="sxs-lookup"><span data-stu-id="1ed25-140">Property</span></span> | <span data-ttu-id="1ed25-141">Description</span><span class="sxs-lookup"><span data-stu-id="1ed25-141">Description</span></span> | <span data-ttu-id="1ed25-142">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1ed25-142">Allowed values</span></span> | <span data-ttu-id="1ed25-143">Required</span><span class="sxs-lookup"><span data-stu-id="1ed25-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="1ed25-144">server</span><span class="sxs-lookup"><span data-stu-id="1ed25-144">server</span></span> | <span data-ttu-id="1ed25-145">Name of the server on which the SAP HANA instance resides.</span><span class="sxs-lookup"><span data-stu-id="1ed25-145">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="1ed25-146">If your server is using a customized port, specify `server:port`.</span><span class="sxs-lookup"><span data-stu-id="1ed25-146">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="1ed25-147">string</span><span class="sxs-lookup"><span data-stu-id="1ed25-147">string</span></span> | <span data-ttu-id="1ed25-148">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed25-148">Yes</span></span>
<span data-ttu-id="1ed25-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1ed25-149">authenticationType</span></span> | <span data-ttu-id="1ed25-150">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="1ed25-150">Type of authentication.</span></span> | <span data-ttu-id="1ed25-151">string.</span><span class="sxs-lookup"><span data-stu-id="1ed25-151">string.</span></span> <span data-ttu-id="1ed25-152">"Basic" or "Windows"</span><span class="sxs-lookup"><span data-stu-id="1ed25-152">"Basic" or "Windows"</span></span> | <span data-ttu-id="1ed25-153">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed25-153">Yes</span></span> 
<span data-ttu-id="1ed25-154">username</span><span class="sxs-lookup"><span data-stu-id="1ed25-154">username</span></span> | <span data-ttu-id="1ed25-155">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="1ed25-155">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="1ed25-156">string</span><span class="sxs-lookup"><span data-stu-id="1ed25-156">string</span></span> | <span data-ttu-id="1ed25-157">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed25-157">Yes</span></span>
<span data-ttu-id="1ed25-158">password</span><span class="sxs-lookup"><span data-stu-id="1ed25-158">password</span></span> | <span data-ttu-id="1ed25-159">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="1ed25-159">Password for the user.</span></span> | <span data-ttu-id="1ed25-160">string</span><span class="sxs-lookup"><span data-stu-id="1ed25-160">string</span></span> | <span data-ttu-id="1ed25-161">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed25-161">Yes</span></span>
<span data-ttu-id="1ed25-162">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1ed25-162">gatewayName</span></span> | <span data-ttu-id="1ed25-163">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="1ed25-163">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="1ed25-164">string</span><span class="sxs-lookup"><span data-stu-id="1ed25-164">string</span></span> | <span data-ttu-id="1ed25-165">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed25-165">Yes</span></span>
<span data-ttu-id="1ed25-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1ed25-166">encryptedCredential</span></span> | <span data-ttu-id="1ed25-167">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="1ed25-167">The encrypted credential string.</span></span> | <span data-ttu-id="1ed25-168">string</span><span class="sxs-lookup"><span data-stu-id="1ed25-168">string</span></span> | <span data-ttu-id="1ed25-169">No</span><span class="sxs-lookup"><span data-stu-id="1ed25-169">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="1ed25-170">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="1ed25-170">Dataset properties</span></span>
<span data-ttu-id="1ed25-171">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="1ed25-171">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1ed25-172">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="1ed25-172">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1ed25-173">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="1ed25-173">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1ed25-174">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-174">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="1ed25-175">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="1ed25-175">Copy activity properties</span></span>
<span data-ttu-id="1ed25-176">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="1ed25-176">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1ed25-177">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="1ed25-177">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="1ed25-178">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="1ed25-178">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="1ed25-179">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="1ed25-179">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1ed25-180">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="1ed25-180">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1ed25-181">Property</span><span class="sxs-lookup"><span data-stu-id="1ed25-181">Property</span></span> | <span data-ttu-id="1ed25-182">Description</span><span class="sxs-lookup"><span data-stu-id="1ed25-182">Description</span></span> | <span data-ttu-id="1ed25-183">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1ed25-183">Allowed values</span></span> | <span data-ttu-id="1ed25-184">Required</span><span class="sxs-lookup"><span data-stu-id="1ed25-184">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ed25-185">query</span><span class="sxs-lookup"><span data-stu-id="1ed25-185">query</span></span> | <span data-ttu-id="1ed25-186">Specifies the SQL query to read data from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="1ed25-186">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="1ed25-187">SQL query.</span><span class="sxs-lookup"><span data-stu-id="1ed25-187">SQL query.</span></span> | <span data-ttu-id="1ed25-188">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed25-188">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="1ed25-189">JSON example: Copy data from SAP HANA to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1ed25-189">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="1ed25-190">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1ed25-190">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1ed25-191">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1ed25-191">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="1ed25-192">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1ed25-192">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> This sample provides JSON snippets. It does not include step-by-step instructions for creating the data factory. See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.

<span data-ttu-id="1ed25-196">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="1ed25-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="1ed25-197">A linked service of type [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1ed25-197">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="1ed25-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1ed25-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1ed25-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1ed25-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1ed25-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1ed25-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1ed25-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1ed25-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1ed25-202">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="1ed25-202">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="1ed25-203">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="1ed25-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1ed25-204">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="1ed25-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="1ed25-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="1ed25-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="1ed25-206">SAP HANA linked service</span><span class="sxs-lookup"><span data-stu-id="1ed25-206">SAP HANA linked service</span></span>
<span data-ttu-id="1ed25-207">This linked service links your SAP HANA instance to the data factory.</span><span class="sxs-lookup"><span data-stu-id="1ed25-207">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="1ed25-208">The type property is set to **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-208">The type property is set to **SapHana**.</span></span> <span data-ttu-id="1ed25-209">The typeProperties section provides connection information for the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="1ed25-209">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="1ed25-210">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="1ed25-210">Azure Storage linked service</span></span>
<span data-ttu-id="1ed25-211">This linked service links your Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="1ed25-211">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="1ed25-212">The type property is set to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-212">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="1ed25-213">The typeProperties section provides connection information for the Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="1ed25-213">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="1ed25-214">SAP HANA input dataset</span><span class="sxs-lookup"><span data-stu-id="1ed25-214">SAP HANA input dataset</span></span>

<span data-ttu-id="1ed25-215">This dataset defines the SAP HANA dataset.</span><span class="sxs-lookup"><span data-stu-id="1ed25-215">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="1ed25-216">You set the type of the Data Factory dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-216">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="1ed25-217">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span><span class="sxs-lookup"><span data-stu-id="1ed25-217">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="1ed25-218">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="1ed25-218">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="1ed25-219">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1ed25-219">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="1ed25-220">Frequency and interval properties defines the schedule.</span><span class="sxs-lookup"><span data-stu-id="1ed25-220">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="1ed25-221">In this case, the data is read from the SAP HANA instance hourly.</span><span class="sxs-lookup"><span data-stu-id="1ed25-221">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="1ed25-222">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="1ed25-222">Azure Blob output dataset</span></span>
<span data-ttu-id="1ed25-223">This dataset defines the output Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="1ed25-223">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="1ed25-224">The type property is set to AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="1ed25-224">The type property is set to AzureBlob.</span></span> <span data-ttu-id="1ed25-225">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span><span class="sxs-lookup"><span data-stu-id="1ed25-225">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="1ed25-226">The data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1ed25-226">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1ed25-227">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="1ed25-227">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1ed25-228">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="1ed25-228">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="1ed25-229">Pipeline with Copy activity</span><span class="sxs-lookup"><span data-stu-id="1ed25-229">Pipeline with Copy activity</span></span>

<span data-ttu-id="1ed25-230">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="1ed25-230">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1ed25-231">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1ed25-231">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="1ed25-232">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="1ed25-232">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="1ed25-233">Type mapping for SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1ed25-233">Type mapping for SAP HANA</span></span>
<span data-ttu-id="1ed25-234">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="1ed25-234">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="1ed25-235">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="1ed25-235">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="1ed25-236">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="1ed25-236">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="1ed25-237">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="1ed25-237">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="1ed25-238">SAP HANA Type</span><span class="sxs-lookup"><span data-stu-id="1ed25-238">SAP HANA Type</span></span> | <span data-ttu-id="1ed25-239">.NET Based Type</span><span class="sxs-lookup"><span data-stu-id="1ed25-239">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="1ed25-240">TINYINT</span><span class="sxs-lookup"><span data-stu-id="1ed25-240">TINYINT</span></span> | <span data-ttu-id="1ed25-241">Byte</span><span class="sxs-lookup"><span data-stu-id="1ed25-241">Byte</span></span>
<span data-ttu-id="1ed25-242">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="1ed25-242">SMALLINT</span></span> | <span data-ttu-id="1ed25-243">Int16</span><span class="sxs-lookup"><span data-stu-id="1ed25-243">Int16</span></span>
<span data-ttu-id="1ed25-244">INT</span><span class="sxs-lookup"><span data-stu-id="1ed25-244">INT</span></span> | <span data-ttu-id="1ed25-245">Int32</span><span class="sxs-lookup"><span data-stu-id="1ed25-245">Int32</span></span>
<span data-ttu-id="1ed25-246">BIGINT</span><span class="sxs-lookup"><span data-stu-id="1ed25-246">BIGINT</span></span> | <span data-ttu-id="1ed25-247">Int64</span><span class="sxs-lookup"><span data-stu-id="1ed25-247">Int64</span></span>
<span data-ttu-id="1ed25-248">REAL</span><span class="sxs-lookup"><span data-stu-id="1ed25-248">REAL</span></span> | <span data-ttu-id="1ed25-249">Single</span><span class="sxs-lookup"><span data-stu-id="1ed25-249">Single</span></span>
<span data-ttu-id="1ed25-250">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="1ed25-250">DOUBLE</span></span> | <span data-ttu-id="1ed25-251">Single</span><span class="sxs-lookup"><span data-stu-id="1ed25-251">Single</span></span>
<span data-ttu-id="1ed25-252">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="1ed25-252">DECIMAL</span></span> | <span data-ttu-id="1ed25-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="1ed25-253">Decimal</span></span>
<span data-ttu-id="1ed25-254">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="1ed25-254">BOOLEAN</span></span> | <span data-ttu-id="1ed25-255">Byte</span><span class="sxs-lookup"><span data-stu-id="1ed25-255">Byte</span></span>
<span data-ttu-id="1ed25-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="1ed25-256">VARCHAR</span></span> | <span data-ttu-id="1ed25-257">String</span><span class="sxs-lookup"><span data-stu-id="1ed25-257">String</span></span>
<span data-ttu-id="1ed25-258">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="1ed25-258">NVARCHAR</span></span> | <span data-ttu-id="1ed25-259">String</span><span class="sxs-lookup"><span data-stu-id="1ed25-259">String</span></span>
<span data-ttu-id="1ed25-260">CLOB</span><span class="sxs-lookup"><span data-stu-id="1ed25-260">CLOB</span></span> | <span data-ttu-id="1ed25-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1ed25-261">Byte[]</span></span>
<span data-ttu-id="1ed25-262">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="1ed25-262">ALPHANUM</span></span> | <span data-ttu-id="1ed25-263">String</span><span class="sxs-lookup"><span data-stu-id="1ed25-263">String</span></span>
<span data-ttu-id="1ed25-264">BLOB</span><span class="sxs-lookup"><span data-stu-id="1ed25-264">BLOB</span></span> | <span data-ttu-id="1ed25-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1ed25-265">Byte[]</span></span>
<span data-ttu-id="1ed25-266">DATE</span><span class="sxs-lookup"><span data-stu-id="1ed25-266">DATE</span></span> | <span data-ttu-id="1ed25-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="1ed25-267">DateTime</span></span>
<span data-ttu-id="1ed25-268">TIME</span><span class="sxs-lookup"><span data-stu-id="1ed25-268">TIME</span></span> | <span data-ttu-id="1ed25-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1ed25-269">TimeSpan</span></span>
<span data-ttu-id="1ed25-270">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="1ed25-270">TIMESTAMP</span></span> | <span data-ttu-id="1ed25-271">DateTime</span><span class="sxs-lookup"><span data-stu-id="1ed25-271">DateTime</span></span>
<span data-ttu-id="1ed25-272">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="1ed25-272">SECONDDATE</span></span> | <span data-ttu-id="1ed25-273">DateTime</span><span class="sxs-lookup"><span data-stu-id="1ed25-273">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="1ed25-274">Known limitations</span><span class="sxs-lookup"><span data-stu-id="1ed25-274">Known limitations</span></span>
<span data-ttu-id="1ed25-275">There are a few known limitations when copying data from SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="1ed25-275">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="1ed25-276">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span><span class="sxs-lookup"><span data-stu-id="1ed25-276">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="1ed25-277">SMALLDECIMAL is not supported</span><span class="sxs-lookup"><span data-stu-id="1ed25-277">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="1ed25-278">VARBINARY is not supported</span><span class="sxs-lookup"><span data-stu-id="1ed25-278">VARBINARY is not supported</span></span>
- <span data-ttu-id="1ed25-279">Valid Dates are between 1899/12/30 and 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="1ed25-279">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="1ed25-280">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="1ed25-280">Map source to sink columns</span></span>
<span data-ttu-id="1ed25-281">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1ed25-281">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1ed25-282">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="1ed25-282">Repeatable read from relational sources</span></span>
<span data-ttu-id="1ed25-283">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="1ed25-283">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="1ed25-284">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="1ed25-284">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1ed25-285">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="1ed25-285">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1ed25-286">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="1ed25-286">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1ed25-287">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="1ed25-287">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1ed25-288">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="1ed25-288">Performance and Tuning</span></span>
<span data-ttu-id="1ed25-289">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="1ed25-289">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
