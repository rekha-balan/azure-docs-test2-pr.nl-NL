---
title: Move data from SAP Business Warehouse using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from SAP Business Warehouse using Azure Data Factory.
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
ms.openlocfilehash: cf62f0676740c82d58d5ac5644ceffb8daf1a4f2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564501"
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="eaed3-103">Move data From SAP Business Warehouse using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="eaed3-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="eaed3-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="eaed3-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="eaed3-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="eaed3-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="eaed3-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="eaed3-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="eaed3-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="eaed3-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="eaed3-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eaed3-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="eaed3-109">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="eaed3-109">Supported versions and installation</span></span>
<span data-ttu-id="eaed3-110">This connector supports SAP Business Warehouse version 7.x.</span><span class="sxs-lookup"><span data-stu-id="eaed3-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="eaed3-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span><span class="sxs-lookup"><span data-stu-id="eaed3-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="eaed3-112">To enable the connectivity to the SAP BW instance, install the following components:</span><span class="sxs-lookup"><span data-stu-id="eaed3-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="eaed3-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="eaed3-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="eaed3-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="eaed3-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="eaed3-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="eaed3-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="eaed3-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="eaed3-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="eaed3-117">**SAP NetWeaver library** on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="eaed3-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="eaed3-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="eaed3-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="eaed3-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span><span class="sxs-lookup"><span data-stu-id="eaed3-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="eaed3-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span><span class="sxs-lookup"><span data-stu-id="eaed3-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="eaed3-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span><span class="sxs-lookup"><span data-stu-id="eaed3-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="eaed3-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span><span class="sxs-lookup"><span data-stu-id="eaed3-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="eaed3-123">Getting started</span><span class="sxs-lookup"><span data-stu-id="eaed3-123">Getting started</span></span>
<span data-ttu-id="eaed3-124">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="eaed3-124">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="eaed3-125">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-125">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="eaed3-126">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="eaed3-126">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="eaed3-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="eaed3-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="eaed3-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="eaed3-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="eaed3-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="eaed3-130">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="eaed3-130">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="eaed3-131">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="eaed3-131">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="eaed3-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="eaed3-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="eaed3-133">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="eaed3-133">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="eaed3-134">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="eaed3-134">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="eaed3-135">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="eaed3-135">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="eaed3-136">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span><span class="sxs-lookup"><span data-stu-id="eaed3-136">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="eaed3-137">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="eaed3-137">Linked service properties</span></span>
<span data-ttu-id="eaed3-138">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span><span class="sxs-lookup"><span data-stu-id="eaed3-138">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="eaed3-139">Property</span><span class="sxs-lookup"><span data-stu-id="eaed3-139">Property</span></span> | <span data-ttu-id="eaed3-140">Description</span><span class="sxs-lookup"><span data-stu-id="eaed3-140">Description</span></span> | <span data-ttu-id="eaed3-141">Allowed values</span><span class="sxs-lookup"><span data-stu-id="eaed3-141">Allowed values</span></span> | <span data-ttu-id="eaed3-142">Required</span><span class="sxs-lookup"><span data-stu-id="eaed3-142">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="eaed3-143">server</span><span class="sxs-lookup"><span data-stu-id="eaed3-143">server</span></span> | <span data-ttu-id="eaed3-144">Name of the server on which the SAP BW instance resides.</span><span class="sxs-lookup"><span data-stu-id="eaed3-144">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="eaed3-145">string</span><span class="sxs-lookup"><span data-stu-id="eaed3-145">string</span></span> | <span data-ttu-id="eaed3-146">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-146">Yes</span></span>
<span data-ttu-id="eaed3-147">systemNumber</span><span class="sxs-lookup"><span data-stu-id="eaed3-147">systemNumber</span></span> | <span data-ttu-id="eaed3-148">System number of the SAP BW system.</span><span class="sxs-lookup"><span data-stu-id="eaed3-148">System number of the SAP BW system.</span></span> | <span data-ttu-id="eaed3-149">Two-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="eaed3-149">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="eaed3-150">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-150">Yes</span></span>
<span data-ttu-id="eaed3-151">clientId</span><span class="sxs-lookup"><span data-stu-id="eaed3-151">clientId</span></span> | <span data-ttu-id="eaed3-152">Client ID of the client in the SAP W system.</span><span class="sxs-lookup"><span data-stu-id="eaed3-152">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="eaed3-153">Three-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="eaed3-153">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="eaed3-154">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-154">Yes</span></span>
<span data-ttu-id="eaed3-155">username</span><span class="sxs-lookup"><span data-stu-id="eaed3-155">username</span></span> | <span data-ttu-id="eaed3-156">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="eaed3-156">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="eaed3-157">string</span><span class="sxs-lookup"><span data-stu-id="eaed3-157">string</span></span> | <span data-ttu-id="eaed3-158">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-158">Yes</span></span>
<span data-ttu-id="eaed3-159">password</span><span class="sxs-lookup"><span data-stu-id="eaed3-159">password</span></span> | <span data-ttu-id="eaed3-160">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="eaed3-160">Password for the user.</span></span> | <span data-ttu-id="eaed3-161">string</span><span class="sxs-lookup"><span data-stu-id="eaed3-161">string</span></span> | <span data-ttu-id="eaed3-162">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-162">Yes</span></span>
<span data-ttu-id="eaed3-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="eaed3-163">gatewayName</span></span> | <span data-ttu-id="eaed3-164">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="eaed3-164">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="eaed3-165">string</span><span class="sxs-lookup"><span data-stu-id="eaed3-165">string</span></span> | <span data-ttu-id="eaed3-166">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-166">Yes</span></span>
<span data-ttu-id="eaed3-167">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="eaed3-167">encryptedCredential</span></span> | <span data-ttu-id="eaed3-168">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="eaed3-168">The encrypted credential string.</span></span> | <span data-ttu-id="eaed3-169">string</span><span class="sxs-lookup"><span data-stu-id="eaed3-169">string</span></span> | <span data-ttu-id="eaed3-170">No</span><span class="sxs-lookup"><span data-stu-id="eaed3-170">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="eaed3-171">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="eaed3-171">Dataset properties</span></span>
<span data-ttu-id="eaed3-172">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="eaed3-172">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="eaed3-173">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="eaed3-173">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="eaed3-174">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="eaed3-174">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="eaed3-175">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-175">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="eaed3-176">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="eaed3-176">Copy activity properties</span></span>
<span data-ttu-id="eaed3-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="eaed3-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="eaed3-178">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="eaed3-178">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="eaed3-179">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="eaed3-179">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="eaed3-180">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="eaed3-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="eaed3-181">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="eaed3-181">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="eaed3-182">Property</span><span class="sxs-lookup"><span data-stu-id="eaed3-182">Property</span></span> | <span data-ttu-id="eaed3-183">Description</span><span class="sxs-lookup"><span data-stu-id="eaed3-183">Description</span></span> | <span data-ttu-id="eaed3-184">Allowed values</span><span class="sxs-lookup"><span data-stu-id="eaed3-184">Allowed values</span></span> | <span data-ttu-id="eaed3-185">Required</span><span class="sxs-lookup"><span data-stu-id="eaed3-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eaed3-186">query</span><span class="sxs-lookup"><span data-stu-id="eaed3-186">query</span></span> | <span data-ttu-id="eaed3-187">Specifies the MDX query to read data from the SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="eaed3-187">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="eaed3-188">MDX query.</span><span class="sxs-lookup"><span data-stu-id="eaed3-188">MDX query.</span></span> | <span data-ttu-id="eaed3-189">Yes</span><span class="sxs-lookup"><span data-stu-id="eaed3-189">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="eaed3-190">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="eaed3-190">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="eaed3-191">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="eaed3-191">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="eaed3-192">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="eaed3-192">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="eaed3-193">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="eaed3-193">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="eaed3-194">This sample provides JSON snippets.</span><span class="sxs-lookup"><span data-stu-id="eaed3-194">This sample provides JSON snippets.</span></span> <span data-ttu-id="eaed3-195">It does not include step-by-step instructions for creating the data factory.</span><span class="sxs-lookup"><span data-stu-id="eaed3-195">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="eaed3-196">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="eaed3-196">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="eaed3-197">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="eaed3-197">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="eaed3-198">A linked service of type [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="eaed3-198">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="eaed3-199">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="eaed3-199">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="eaed3-200">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="eaed3-200">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="eaed3-201">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="eaed3-201">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="eaed3-202">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="eaed3-202">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="eaed3-203">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="eaed3-203">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="eaed3-204">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="eaed3-204">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="eaed3-205">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="eaed3-205">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="eaed3-206">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="eaed3-206">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="eaed3-207">SAP Business Warehouse linked service</span><span class="sxs-lookup"><span data-stu-id="eaed3-207">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="eaed3-208">This linked service links your SAP BW instance to the data factory.</span><span class="sxs-lookup"><span data-stu-id="eaed3-208">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="eaed3-209">The type property is set to **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-209">The type property is set to **SapBw**.</span></span> <span data-ttu-id="eaed3-210">The typeProperties section provides connection information for the SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="eaed3-210">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="eaed3-211">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="eaed3-211">Azure Storage linked service</span></span>
<span data-ttu-id="eaed3-212">This linked service links your Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="eaed3-212">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="eaed3-213">The type property is set to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-213">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="eaed3-214">The typeProperties section provides connection information for the Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="eaed3-214">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="eaed3-215">SAP BW input dataset</span><span class="sxs-lookup"><span data-stu-id="eaed3-215">SAP BW input dataset</span></span>
<span data-ttu-id="eaed3-216">This dataset defines the SAP Business Warehouse dataset.</span><span class="sxs-lookup"><span data-stu-id="eaed3-216">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="eaed3-217">You set the type of the Data Factory dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-217">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="eaed3-218">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span><span class="sxs-lookup"><span data-stu-id="eaed3-218">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="eaed3-219">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="eaed3-219">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="eaed3-220">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="eaed3-220">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="eaed3-221">Frequency and interval properties defines the schedule.</span><span class="sxs-lookup"><span data-stu-id="eaed3-221">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="eaed3-222">In this case, the data is read from the SAP BW instance hourly.</span><span class="sxs-lookup"><span data-stu-id="eaed3-222">In this case, the data is read from the SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="eaed3-223">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="eaed3-223">Azure Blob output dataset</span></span>
<span data-ttu-id="eaed3-224">This dataset defines the output Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="eaed3-224">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="eaed3-225">The type property is set to AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="eaed3-225">The type property is set to AzureBlob.</span></span> <span data-ttu-id="eaed3-226">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span><span class="sxs-lookup"><span data-stu-id="eaed3-226">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="eaed3-227">The data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="eaed3-227">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="eaed3-228">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="eaed3-228">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="eaed3-229">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="eaed3-229">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="eaed3-230">Pipeline with Copy activity</span><span class="sxs-lookup"><span data-stu-id="eaed3-230">Pipeline with Copy activity</span></span>
<span data-ttu-id="eaed3-231">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="eaed3-231">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="eaed3-232">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="eaed3-232">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="eaed3-233">The query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="eaed3-233">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="eaed3-234">Type mapping for SAP BW</span><span class="sxs-lookup"><span data-stu-id="eaed3-234">Type mapping for SAP BW</span></span>
<span data-ttu-id="eaed3-235">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="eaed3-235">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="eaed3-236">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="eaed3-236">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="eaed3-237">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="eaed3-237">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="eaed3-238">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="eaed3-238">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="eaed3-239">Data type in the ABAP Dictionary</span><span class="sxs-lookup"><span data-stu-id="eaed3-239">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="eaed3-240">.Net Data Type</span><span class="sxs-lookup"><span data-stu-id="eaed3-240">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="eaed3-241">ACCP</span><span class="sxs-lookup"><span data-stu-id="eaed3-241">ACCP</span></span> |  <span data-ttu-id="eaed3-242">Int</span><span class="sxs-lookup"><span data-stu-id="eaed3-242">Int</span></span>
<span data-ttu-id="eaed3-243">CHAR</span><span class="sxs-lookup"><span data-stu-id="eaed3-243">CHAR</span></span> | <span data-ttu-id="eaed3-244">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-244">String</span></span>
<span data-ttu-id="eaed3-245">CLNT</span><span class="sxs-lookup"><span data-stu-id="eaed3-245">CLNT</span></span> | <span data-ttu-id="eaed3-246">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-246">String</span></span>
<span data-ttu-id="eaed3-247">CURR</span><span class="sxs-lookup"><span data-stu-id="eaed3-247">CURR</span></span> | <span data-ttu-id="eaed3-248">Decimal</span><span class="sxs-lookup"><span data-stu-id="eaed3-248">Decimal</span></span>
<span data-ttu-id="eaed3-249">CUKY</span><span class="sxs-lookup"><span data-stu-id="eaed3-249">CUKY</span></span> | <span data-ttu-id="eaed3-250">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-250">String</span></span>
<span data-ttu-id="eaed3-251">DEC</span><span class="sxs-lookup"><span data-stu-id="eaed3-251">DEC</span></span> | <span data-ttu-id="eaed3-252">Decimal</span><span class="sxs-lookup"><span data-stu-id="eaed3-252">Decimal</span></span>
<span data-ttu-id="eaed3-253">FLTP</span><span class="sxs-lookup"><span data-stu-id="eaed3-253">FLTP</span></span> | <span data-ttu-id="eaed3-254">Double</span><span class="sxs-lookup"><span data-stu-id="eaed3-254">Double</span></span>
<span data-ttu-id="eaed3-255">INT1</span><span class="sxs-lookup"><span data-stu-id="eaed3-255">INT1</span></span> | <span data-ttu-id="eaed3-256">Byte</span><span class="sxs-lookup"><span data-stu-id="eaed3-256">Byte</span></span>
<span data-ttu-id="eaed3-257">INT2</span><span class="sxs-lookup"><span data-stu-id="eaed3-257">INT2</span></span> | <span data-ttu-id="eaed3-258">Int16</span><span class="sxs-lookup"><span data-stu-id="eaed3-258">Int16</span></span>
<span data-ttu-id="eaed3-259">INT4</span><span class="sxs-lookup"><span data-stu-id="eaed3-259">INT4</span></span> | <span data-ttu-id="eaed3-260">Int</span><span class="sxs-lookup"><span data-stu-id="eaed3-260">Int</span></span>
<span data-ttu-id="eaed3-261">LANG</span><span class="sxs-lookup"><span data-stu-id="eaed3-261">LANG</span></span> | <span data-ttu-id="eaed3-262">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-262">String</span></span>
<span data-ttu-id="eaed3-263">LCHR</span><span class="sxs-lookup"><span data-stu-id="eaed3-263">LCHR</span></span> | <span data-ttu-id="eaed3-264">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-264">String</span></span>
<span data-ttu-id="eaed3-265">LRAW</span><span class="sxs-lookup"><span data-stu-id="eaed3-265">LRAW</span></span> | <span data-ttu-id="eaed3-266">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eaed3-266">Byte[]</span></span>
<span data-ttu-id="eaed3-267">PREC</span><span class="sxs-lookup"><span data-stu-id="eaed3-267">PREC</span></span> | <span data-ttu-id="eaed3-268">Int16</span><span class="sxs-lookup"><span data-stu-id="eaed3-268">Int16</span></span>
<span data-ttu-id="eaed3-269">QUAN</span><span class="sxs-lookup"><span data-stu-id="eaed3-269">QUAN</span></span> | <span data-ttu-id="eaed3-270">Decimal</span><span class="sxs-lookup"><span data-stu-id="eaed3-270">Decimal</span></span>
<span data-ttu-id="eaed3-271">RAW</span><span class="sxs-lookup"><span data-stu-id="eaed3-271">RAW</span></span> | <span data-ttu-id="eaed3-272">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eaed3-272">Byte[]</span></span>
<span data-ttu-id="eaed3-273">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="eaed3-273">RAWSTRING</span></span> | <span data-ttu-id="eaed3-274">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eaed3-274">Byte[]</span></span>
<span data-ttu-id="eaed3-275">STRING</span><span class="sxs-lookup"><span data-stu-id="eaed3-275">STRING</span></span> | <span data-ttu-id="eaed3-276">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-276">String</span></span>
<span data-ttu-id="eaed3-277">UNIT</span><span class="sxs-lookup"><span data-stu-id="eaed3-277">UNIT</span></span> | <span data-ttu-id="eaed3-278">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-278">String</span></span>
<span data-ttu-id="eaed3-279">DATS</span><span class="sxs-lookup"><span data-stu-id="eaed3-279">DATS</span></span> | <span data-ttu-id="eaed3-280">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-280">String</span></span>
<span data-ttu-id="eaed3-281">NUMC</span><span class="sxs-lookup"><span data-stu-id="eaed3-281">NUMC</span></span> | <span data-ttu-id="eaed3-282">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-282">String</span></span>
<span data-ttu-id="eaed3-283">TIMS</span><span class="sxs-lookup"><span data-stu-id="eaed3-283">TIMS</span></span> | <span data-ttu-id="eaed3-284">String</span><span class="sxs-lookup"><span data-stu-id="eaed3-284">String</span></span>

> [!NOTE]
> <span data-ttu-id="eaed3-285">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="eaed3-285">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="eaed3-286">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="eaed3-286">Map source to sink columns</span></span>
<span data-ttu-id="eaed3-287">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="eaed3-287">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="eaed3-288">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="eaed3-288">Repeatable read from relational sources</span></span>
<span data-ttu-id="eaed3-289">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="eaed3-289">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="eaed3-290">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="eaed3-290">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="eaed3-291">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="eaed3-291">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="eaed3-292">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="eaed3-292">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="eaed3-293">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="eaed3-293">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="eaed3-294">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="eaed3-294">Performance and Tuning</span></span>
<span data-ttu-id="eaed3-295">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="eaed3-295">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
