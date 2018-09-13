---
title: Move data from SAP HANA using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from SAP HANA using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: jingwang
ms.openlocfilehash: 37594924f9474d225421d2b2d783a19d9295fcf8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562940"
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="6b262-103">Move data From SAP HANA using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6b262-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="6b262-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="6b262-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="6b262-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="6b262-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6b262-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="6b262-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="6b262-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="6b262-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6b262-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="6b262-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="6b262-109">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="6b262-109">Supported versions and installation</span></span>
<span data-ttu-id="6b262-110">This connector supports any version of SAP HANA database.</span><span class="sxs-lookup"><span data-stu-id="6b262-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="6b262-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span><span class="sxs-lookup"><span data-stu-id="6b262-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="6b262-112">To enable the connectivity to the SAP HANA instance, install the following components:</span><span class="sxs-lookup"><span data-stu-id="6b262-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="6b262-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="6b262-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="6b262-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="6b262-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="6b262-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="6b262-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="6b262-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="6b262-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="6b262-117">**SAP HANA ODBC driver** on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="6b262-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="6b262-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="6b262-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="6b262-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span><span class="sxs-lookup"><span data-stu-id="6b262-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6b262-120">Getting started</span><span class="sxs-lookup"><span data-stu-id="6b262-120">Getting started</span></span>
<span data-ttu-id="6b262-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="6b262-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="6b262-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="6b262-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6b262-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="6b262-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="6b262-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6b262-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6b262-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="6b262-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6b262-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="6b262-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6b262-127">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="6b262-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6b262-128">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="6b262-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6b262-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="6b262-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6b262-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="6b262-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6b262-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="6b262-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6b262-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="6b262-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6b262-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span><span class="sxs-lookup"><span data-stu-id="6b262-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6b262-134">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="6b262-134">Linked service properties</span></span>
<span data-ttu-id="6b262-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span><span class="sxs-lookup"><span data-stu-id="6b262-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="6b262-136">Property</span><span class="sxs-lookup"><span data-stu-id="6b262-136">Property</span></span> | <span data-ttu-id="6b262-137">Description</span><span class="sxs-lookup"><span data-stu-id="6b262-137">Description</span></span> | <span data-ttu-id="6b262-138">Allowed values</span><span class="sxs-lookup"><span data-stu-id="6b262-138">Allowed values</span></span> | <span data-ttu-id="6b262-139">Required</span><span class="sxs-lookup"><span data-stu-id="6b262-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="6b262-140">server</span><span class="sxs-lookup"><span data-stu-id="6b262-140">server</span></span> | <span data-ttu-id="6b262-141">Name of the server on which the SAP HANA instance resides.</span><span class="sxs-lookup"><span data-stu-id="6b262-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="6b262-142">If your server is using a customized port, specify `server:port`.</span><span class="sxs-lookup"><span data-stu-id="6b262-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="6b262-143">string</span><span class="sxs-lookup"><span data-stu-id="6b262-143">string</span></span> | <span data-ttu-id="6b262-144">Yes</span><span class="sxs-lookup"><span data-stu-id="6b262-144">Yes</span></span>
<span data-ttu-id="6b262-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6b262-145">authenticationType</span></span> | <span data-ttu-id="6b262-146">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="6b262-146">Type of authentication.</span></span> | <span data-ttu-id="6b262-147">string.</span><span class="sxs-lookup"><span data-stu-id="6b262-147">string.</span></span> <span data-ttu-id="6b262-148">"Basic" or "Windows"</span><span class="sxs-lookup"><span data-stu-id="6b262-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="6b262-149">Yes</span><span class="sxs-lookup"><span data-stu-id="6b262-149">Yes</span></span> 
<span data-ttu-id="6b262-150">username</span><span class="sxs-lookup"><span data-stu-id="6b262-150">username</span></span> | <span data-ttu-id="6b262-151">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="6b262-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="6b262-152">string</span><span class="sxs-lookup"><span data-stu-id="6b262-152">string</span></span> | <span data-ttu-id="6b262-153">Yes</span><span class="sxs-lookup"><span data-stu-id="6b262-153">Yes</span></span>
<span data-ttu-id="6b262-154">password</span><span class="sxs-lookup"><span data-stu-id="6b262-154">password</span></span> | <span data-ttu-id="6b262-155">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="6b262-155">Password for the user.</span></span> | <span data-ttu-id="6b262-156">string</span><span class="sxs-lookup"><span data-stu-id="6b262-156">string</span></span> | <span data-ttu-id="6b262-157">Yes</span><span class="sxs-lookup"><span data-stu-id="6b262-157">Yes</span></span>
<span data-ttu-id="6b262-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6b262-158">gatewayName</span></span> | <span data-ttu-id="6b262-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="6b262-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="6b262-160">string</span><span class="sxs-lookup"><span data-stu-id="6b262-160">string</span></span> | <span data-ttu-id="6b262-161">Yes</span><span class="sxs-lookup"><span data-stu-id="6b262-161">Yes</span></span>
<span data-ttu-id="6b262-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6b262-162">encryptedCredential</span></span> | <span data-ttu-id="6b262-163">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="6b262-163">The encrypted credential string.</span></span> | <span data-ttu-id="6b262-164">string</span><span class="sxs-lookup"><span data-stu-id="6b262-164">string</span></span> | <span data-ttu-id="6b262-165">No</span><span class="sxs-lookup"><span data-stu-id="6b262-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="6b262-166">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="6b262-166">Dataset properties</span></span>
<span data-ttu-id="6b262-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="6b262-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6b262-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="6b262-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6b262-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="6b262-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6b262-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="6b262-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="6b262-171">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="6b262-171">Copy activity properties</span></span>
<span data-ttu-id="6b262-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="6b262-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6b262-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="6b262-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="6b262-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="6b262-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="6b262-175">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="6b262-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6b262-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="6b262-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6b262-177">Property</span><span class="sxs-lookup"><span data-stu-id="6b262-177">Property</span></span> | <span data-ttu-id="6b262-178">Description</span><span class="sxs-lookup"><span data-stu-id="6b262-178">Description</span></span> | <span data-ttu-id="6b262-179">Allowed values</span><span class="sxs-lookup"><span data-stu-id="6b262-179">Allowed values</span></span> | <span data-ttu-id="6b262-180">Required</span><span class="sxs-lookup"><span data-stu-id="6b262-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6b262-181">query</span><span class="sxs-lookup"><span data-stu-id="6b262-181">query</span></span> | <span data-ttu-id="6b262-182">Specifies the SQL query to read data from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="6b262-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="6b262-183">SQL query.</span><span class="sxs-lookup"><span data-stu-id="6b262-183">SQL query.</span></span> | <span data-ttu-id="6b262-184">Yes</span><span class="sxs-lookup"><span data-stu-id="6b262-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="6b262-185">JSON example: Copy data from SAP HANA to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="6b262-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="6b262-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6b262-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6b262-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="6b262-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="6b262-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6b262-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="6b262-189">This sample provides JSON snippets.</span><span class="sxs-lookup"><span data-stu-id="6b262-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="6b262-190">It does not include step-by-step instructions for creating the data factory.</span><span class="sxs-lookup"><span data-stu-id="6b262-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="6b262-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="6b262-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="6b262-192">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="6b262-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="6b262-193">A linked service of type [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6b262-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="6b262-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6b262-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6b262-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6b262-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6b262-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6b262-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6b262-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6b262-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6b262-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="6b262-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="6b262-199">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="6b262-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6b262-200">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="6b262-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="6b262-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="6b262-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="6b262-202">SAP HANA linked service</span><span class="sxs-lookup"><span data-stu-id="6b262-202">SAP HANA linked service</span></span>
<span data-ttu-id="6b262-203">This linked service links your SAP HANA instance to the data factory.</span><span class="sxs-lookup"><span data-stu-id="6b262-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="6b262-204">The type property is set to **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="6b262-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="6b262-205">The typeProperties section provides connection information for the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="6b262-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="6b262-206">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="6b262-206">Azure Storage linked service</span></span>
<span data-ttu-id="6b262-207">This linked service links your Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="6b262-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="6b262-208">The type property is set to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="6b262-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="6b262-209">The typeProperties section provides connection information for the Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="6b262-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="6b262-210">SAP HANA input dataset</span><span class="sxs-lookup"><span data-stu-id="6b262-210">SAP HANA input dataset</span></span>

<span data-ttu-id="6b262-211">This dataset defines the SAP HANA dataset.</span><span class="sxs-lookup"><span data-stu-id="6b262-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="6b262-212">You set the type of the Data Factory dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="6b262-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="6b262-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span><span class="sxs-lookup"><span data-stu-id="6b262-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="6b262-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="6b262-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="6b262-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="6b262-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="6b262-216">Frequency and interval properties defines the schedule.</span><span class="sxs-lookup"><span data-stu-id="6b262-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="6b262-217">In this case, the data is read from the SAP HANA instance hourly.</span><span class="sxs-lookup"><span data-stu-id="6b262-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="6b262-218">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="6b262-218">Azure Blob output dataset</span></span>
<span data-ttu-id="6b262-219">This dataset defines the output Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="6b262-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="6b262-220">The type property is set to AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="6b262-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="6b262-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span><span class="sxs-lookup"><span data-stu-id="6b262-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="6b262-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6b262-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6b262-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="6b262-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6b262-224">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="6b262-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="6b262-225">Pipeline with Copy activity</span><span class="sxs-lookup"><span data-stu-id="6b262-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="6b262-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="6b262-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6b262-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6b262-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="6b262-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="6b262-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="6b262-229">Type mapping for SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6b262-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="6b262-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="6b262-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="6b262-231">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="6b262-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6b262-232">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="6b262-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6b262-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="6b262-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="6b262-234">SAP HANA Type</span><span class="sxs-lookup"><span data-stu-id="6b262-234">SAP HANA Type</span></span> | <span data-ttu-id="6b262-235">.NET Based Type</span><span class="sxs-lookup"><span data-stu-id="6b262-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="6b262-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="6b262-236">TINYINT</span></span> | <span data-ttu-id="6b262-237">Byte</span><span class="sxs-lookup"><span data-stu-id="6b262-237">Byte</span></span>
<span data-ttu-id="6b262-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="6b262-238">SMALLINT</span></span> | <span data-ttu-id="6b262-239">Int16</span><span class="sxs-lookup"><span data-stu-id="6b262-239">Int16</span></span>
<span data-ttu-id="6b262-240">INT</span><span class="sxs-lookup"><span data-stu-id="6b262-240">INT</span></span> | <span data-ttu-id="6b262-241">Int32</span><span class="sxs-lookup"><span data-stu-id="6b262-241">Int32</span></span>
<span data-ttu-id="6b262-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="6b262-242">BIGINT</span></span> | <span data-ttu-id="6b262-243">Int64</span><span class="sxs-lookup"><span data-stu-id="6b262-243">Int64</span></span>
<span data-ttu-id="6b262-244">REAL</span><span class="sxs-lookup"><span data-stu-id="6b262-244">REAL</span></span> | <span data-ttu-id="6b262-245">Single</span><span class="sxs-lookup"><span data-stu-id="6b262-245">Single</span></span>
<span data-ttu-id="6b262-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="6b262-246">DOUBLE</span></span> | <span data-ttu-id="6b262-247">Single</span><span class="sxs-lookup"><span data-stu-id="6b262-247">Single</span></span>
<span data-ttu-id="6b262-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="6b262-248">DECIMAL</span></span> | <span data-ttu-id="6b262-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="6b262-249">Decimal</span></span>
<span data-ttu-id="6b262-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="6b262-250">BOOLEAN</span></span> | <span data-ttu-id="6b262-251">Byte</span><span class="sxs-lookup"><span data-stu-id="6b262-251">Byte</span></span>
<span data-ttu-id="6b262-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="6b262-252">VARCHAR</span></span> | <span data-ttu-id="6b262-253">String</span><span class="sxs-lookup"><span data-stu-id="6b262-253">String</span></span>
<span data-ttu-id="6b262-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="6b262-254">NVARCHAR</span></span> | <span data-ttu-id="6b262-255">String</span><span class="sxs-lookup"><span data-stu-id="6b262-255">String</span></span>
<span data-ttu-id="6b262-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="6b262-256">CLOB</span></span> | <span data-ttu-id="6b262-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6b262-257">Byte[]</span></span>
<span data-ttu-id="6b262-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="6b262-258">ALPHANUM</span></span> | <span data-ttu-id="6b262-259">String</span><span class="sxs-lookup"><span data-stu-id="6b262-259">String</span></span>
<span data-ttu-id="6b262-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="6b262-260">BLOB</span></span> | <span data-ttu-id="6b262-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6b262-261">Byte[]</span></span>
<span data-ttu-id="6b262-262">DATE</span><span class="sxs-lookup"><span data-stu-id="6b262-262">DATE</span></span> | <span data-ttu-id="6b262-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="6b262-263">DateTime</span></span>
<span data-ttu-id="6b262-264">TIME</span><span class="sxs-lookup"><span data-stu-id="6b262-264">TIME</span></span> | <span data-ttu-id="6b262-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6b262-265">TimeSpan</span></span>
<span data-ttu-id="6b262-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="6b262-266">TIMESTAMP</span></span> | <span data-ttu-id="6b262-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="6b262-267">DateTime</span></span>
<span data-ttu-id="6b262-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="6b262-268">SECONDDATE</span></span> | <span data-ttu-id="6b262-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="6b262-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="6b262-270">Known limitations</span><span class="sxs-lookup"><span data-stu-id="6b262-270">Known limitations</span></span>
<span data-ttu-id="6b262-271">There are a few known limitations when copying data from SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="6b262-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="6b262-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span><span class="sxs-lookup"><span data-stu-id="6b262-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="6b262-273">SMALLDECIMAL is not supported</span><span class="sxs-lookup"><span data-stu-id="6b262-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="6b262-274">VARBINARY is not supported</span><span class="sxs-lookup"><span data-stu-id="6b262-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="6b262-275">Valid Dates are between 1899/12/30 and 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="6b262-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6b262-276">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="6b262-276">Map source to sink columns</span></span>
<span data-ttu-id="6b262-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6b262-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6b262-278">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="6b262-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="6b262-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="6b262-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6b262-280">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="6b262-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6b262-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="6b262-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6b262-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="6b262-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6b262-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="6b262-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6b262-284">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="6b262-284">Performance and Tuning</span></span>
<span data-ttu-id="6b262-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="6b262-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
