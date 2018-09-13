---
title: Move data from Amazon Redshift by using Azure Data Factory | Microsoft Docs
description: Learn how to move data from Amazon Redshift by using Azure Data Factory Copy Activity.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 7ece34809734478ddb52c12d5dbd92291231f439
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857184"
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="bfeb3-103">Move data From Amazon Redshift using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bfeb3-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-amazon-redshift-connector.md)
> * [Version 2 (current version)](../connector-amazon-redshift.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Amazon Redshift connector in V2](../connector-amazon-redshift.md).

<span data-ttu-id="bfeb3-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="bfeb3-109">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-109">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="bfeb3-110">Data Factory currently supports only moving data from Amazon Redshift to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-110">Data Factory currently supports only moving data from Amazon Redshift to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="bfeb3-111">Moving data from other data stores to Amazon Redshift is not supported.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-111">Moving data from other data stores to Amazon Redshift is not supported.</span></span>

> [!TIP]
> To achieve the best performance when copying large amounts of data from Amazon Redshift, consider using the built-in Redshift **UNLOAD** command through Amazon Simple Storage Service (Amazon S3). For details, see [Use UNLOAD to copy data from Amazon Redshift](#use-unload-to-copy-data-from-amazon-redshift).

## <a name="prerequisites"></a><span data-ttu-id="bfeb3-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bfeb3-114">Prerequisites</span></span>
* <span data-ttu-id="bfeb3-115">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-115">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="bfeb3-116">Grant access for a gateway to the Amazon Redshift cluster by using the on-premises machine IP address.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-116">Grant access for a gateway to the Amazon Redshift cluster by using the on-premises machine IP address.</span></span> <span data-ttu-id="bfeb3-117">For instructions, see [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-117">For instructions, see [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html).</span></span>
* <span data-ttu-id="bfeb3-118">To move data to an Azure data store, see the [Compute IP address and SQL ranges that are used by the Microsoft Azure Datacenters](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-118">To move data to an Azure data store, see the [Compute IP address and SQL ranges that are used by the Microsoft Azure Datacenters](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="getting-started"></a><span data-ttu-id="bfeb3-119">Getting started</span><span class="sxs-lookup"><span data-stu-id="bfeb3-119">Getting started</span></span>
<span data-ttu-id="bfeb3-120">You can create a pipeline with a copy activity to move data from an Amazon Redshift source by using different tools and APIs.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-120">You can create a pipeline with a copy activity to move data from an Amazon Redshift source by using different tools and APIs.</span></span>

<span data-ttu-id="bfeb3-121">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-121">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="bfeb3-122">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-122">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="bfeb3-123">You can also create a pipeline by using the Azure portal, Visual Studio, Azure PowerShell, or other tools.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-123">You can also create a pipeline by using the Azure portal, Visual Studio, Azure PowerShell, or other tools.</span></span> <span data-ttu-id="bfeb3-124">Azure Resource Manager templates, the .NET API, or the REST API can also be used to create the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-124">Azure Resource Manager templates, the .NET API, or the REST API can also be used to create the pipeline.</span></span> <span data-ttu-id="bfeb3-125">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-125">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="bfeb3-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="bfeb3-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="bfeb3-127">Create linked services to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-127">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="bfeb3-128">Create datasets to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-128">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="bfeb3-129">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-129">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="bfeb3-130">When you use the Copy Wizard, JSON definitions for these Data Factory entities are automatically created.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-130">When you use the Copy Wizard, JSON definitions for these Data Factory entities are automatically created.</span></span> <span data-ttu-id="bfeb3-131">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-131">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="bfeb3-132">The [JSON example: Copy data from Amazon Redshift to Azure Blob storage](#json-example-copy-data-from-amazon-redshift-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an Amazon Redshift data store.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-132">The [JSON example: Copy data from Amazon Redshift to Azure Blob storage](#json-example-copy-data-from-amazon-redshift-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an Amazon Redshift data store.</span></span>

<span data-ttu-id="bfeb3-133">The following sections describe the JSON properties that are used to define the Data Factory entities for Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-133">The following sections describe the JSON properties that are used to define the Data Factory entities for Amazon Redshift.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bfeb3-134">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="bfeb3-134">Linked service properties</span></span>

<span data-ttu-id="bfeb3-135">The following table provides descriptions for the JSON elements that are specific to an Amazon Redshift linked service.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-135">The following table provides descriptions for the JSON elements that are specific to an Amazon Redshift linked service.</span></span>

| <span data-ttu-id="bfeb3-136">Property</span><span class="sxs-lookup"><span data-stu-id="bfeb3-136">Property</span></span> | <span data-ttu-id="bfeb3-137">Description</span><span class="sxs-lookup"><span data-stu-id="bfeb3-137">Description</span></span> | <span data-ttu-id="bfeb3-138">Required</span><span class="sxs-lookup"><span data-stu-id="bfeb3-138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfeb3-139">**type**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-139">**type**</span></span> |<span data-ttu-id="bfeb3-140">This property must be set to **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-140">This property must be set to **AmazonRedshift**.</span></span> |<span data-ttu-id="bfeb3-141">Yes</span><span class="sxs-lookup"><span data-stu-id="bfeb3-141">Yes</span></span> |
| <span data-ttu-id="bfeb3-142">**server**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-142">**server**</span></span> |<span data-ttu-id="bfeb3-143">The IP address or host name of the Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-143">The IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="bfeb3-144">Yes</span><span class="sxs-lookup"><span data-stu-id="bfeb3-144">Yes</span></span> |
| <span data-ttu-id="bfeb3-145">**port**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-145">**port**</span></span> |<span data-ttu-id="bfeb3-146">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-146">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="bfeb3-147">No (default is 5439)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-147">No (default is 5439)</span></span> |
| <span data-ttu-id="bfeb3-148">**database**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-148">**database**</span></span> |<span data-ttu-id="bfeb3-149">The name of the Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-149">The name of the Amazon Redshift database.</span></span> |<span data-ttu-id="bfeb3-150">Yes</span><span class="sxs-lookup"><span data-stu-id="bfeb3-150">Yes</span></span> |
| <span data-ttu-id="bfeb3-151">**username**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-151">**username**</span></span> |<span data-ttu-id="bfeb3-152">The name of the user who has access to the database.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-152">The name of the user who has access to the database.</span></span> |<span data-ttu-id="bfeb3-153">Yes</span><span class="sxs-lookup"><span data-stu-id="bfeb3-153">Yes</span></span> |
| <span data-ttu-id="bfeb3-154">**password**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-154">**password**</span></span> |<span data-ttu-id="bfeb3-155">The password for the user account.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-155">The password for the user account.</span></span> |<span data-ttu-id="bfeb3-156">Yes</span><span class="sxs-lookup"><span data-stu-id="bfeb3-156">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="bfeb3-157">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="bfeb3-157">Dataset properties</span></span>

<span data-ttu-id="bfeb3-158">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-158">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bfeb3-159">The **structure**, **availability**, and **policy** sections are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-159">The **structure**, **availability**, and **policy** sections are similar for all dataset types.</span></span> <span data-ttu-id="bfeb3-160">Examples of dataset types include Azure SQL, Azure Blob storage, and Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-160">Examples of dataset types include Azure SQL, Azure Blob storage, and Azure Table storage.</span></span>

<span data-ttu-id="bfeb3-161">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the store.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-161">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the store.</span></span> <span data-ttu-id="bfeb3-162">**The typeProperties** section for a dataset of type **RelationalTable**, which includes the Amazon Redshift dataset, has the following properties:</span><span class="sxs-lookup"><span data-stu-id="bfeb3-162">**The typeProperties** section for a dataset of type **RelationalTable**, which includes the Amazon Redshift dataset, has the following properties:</span></span>

| <span data-ttu-id="bfeb3-163">Property</span><span class="sxs-lookup"><span data-stu-id="bfeb3-163">Property</span></span> | <span data-ttu-id="bfeb3-164">Description</span><span class="sxs-lookup"><span data-stu-id="bfeb3-164">Description</span></span> | <span data-ttu-id="bfeb3-165">Required</span><span class="sxs-lookup"><span data-stu-id="bfeb3-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfeb3-166">**tableName**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-166">**tableName**</span></span> |<span data-ttu-id="bfeb3-167">The name of the table in the Amazon Redshift database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-167">The name of the table in the Amazon Redshift database that the linked service refers to.</span></span> |<span data-ttu-id="bfeb3-168">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-168">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="bfeb3-169">Copy Activity properties</span><span class="sxs-lookup"><span data-stu-id="bfeb3-169">Copy Activity properties</span></span>

<span data-ttu-id="bfeb3-170">For a list of sections and properties that are available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-170">For a list of sections and properties that are available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bfeb3-171">The **name**, **description**, **inputs** table, **outputs** table, and **policy** properties are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-171">The **name**, **description**, **inputs** table, **outputs** table, and **policy** properties are available for all types of activities.</span></span> <span data-ttu-id="bfeb3-172">The properties that are available in the **typeProperties** section vary for each activity type.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-172">The properties that are available in the **typeProperties** section vary for each activity type.</span></span> <span data-ttu-id="bfeb3-173">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-173">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="bfeb3-174">For Copy Activity, when the source is of type **AmazonRedshiftSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="bfeb3-174">For Copy Activity, when the source is of type **AmazonRedshiftSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="bfeb3-175">Property</span><span class="sxs-lookup"><span data-stu-id="bfeb3-175">Property</span></span> | <span data-ttu-id="bfeb3-176">Description</span><span class="sxs-lookup"><span data-stu-id="bfeb3-176">Description</span></span> | <span data-ttu-id="bfeb3-177">Required</span><span class="sxs-lookup"><span data-stu-id="bfeb3-177">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfeb3-178">**query**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-178">**query**</span></span> | <span data-ttu-id="bfeb3-179">Use the custom query to read the data.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-179">Use the custom query to read the data.</span></span> |<span data-ttu-id="bfeb3-180">No (if the **tableName** property of a dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-180">No (if the **tableName** property of a dataset is specified)</span></span> |
| <span data-ttu-id="bfeb3-181">**redshiftUnloadSettings**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-181">**redshiftUnloadSettings**</span></span> | <span data-ttu-id="bfeb3-182">Contains the property group when using the Redshift **UNLOAD** command.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-182">Contains the property group when using the Redshift **UNLOAD** command.</span></span> | <span data-ttu-id="bfeb3-183">No</span><span class="sxs-lookup"><span data-stu-id="bfeb3-183">No</span></span> |
| <span data-ttu-id="bfeb3-184">**s3LinkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-184">**s3LinkedServiceName**</span></span> | <span data-ttu-id="bfeb3-185">The Amazon S3 to use as an interim store.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-185">The Amazon S3 to use as an interim store.</span></span> <span data-ttu-id="bfeb3-186">The linked service is specified by using an Azure Data Factory name of type **AwsAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-186">The linked service is specified by using an Azure Data Factory name of type **AwsAccessKey**.</span></span> | <span data-ttu-id="bfeb3-187">Required when using the **redshiftUnloadSettings** property</span><span class="sxs-lookup"><span data-stu-id="bfeb3-187">Required when using the **redshiftUnloadSettings** property</span></span> |
| <span data-ttu-id="bfeb3-188">**bucketName**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-188">**bucketName**</span></span> | <span data-ttu-id="bfeb3-189">Indicates the Amazon S3 bucket to use to store the interim data.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-189">Indicates the Amazon S3 bucket to use to store the interim data.</span></span> <span data-ttu-id="bfeb3-190">If this property is not provided, Copy Activity auto-generates a bucket.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-190">If this property is not provided, Copy Activity auto-generates a bucket.</span></span> | <span data-ttu-id="bfeb3-191">Required when using the **redshiftUnloadSettings** property</span><span class="sxs-lookup"><span data-stu-id="bfeb3-191">Required when using the **redshiftUnloadSettings** property</span></span> |

<span data-ttu-id="bfeb3-192">Alternatively, you can use the **RelationalSource** type, which includes Amazon Redshift, with the following property in the **typeProperties** section.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-192">Alternatively, you can use the **RelationalSource** type, which includes Amazon Redshift, with the following property in the **typeProperties** section.</span></span> <span data-ttu-id="bfeb3-193">Note this source type doesn't support the Redshift **UNLOAD** command.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-193">Note this source type doesn't support the Redshift **UNLOAD** command.</span></span>

| <span data-ttu-id="bfeb3-194">Property</span><span class="sxs-lookup"><span data-stu-id="bfeb3-194">Property</span></span> | <span data-ttu-id="bfeb3-195">Description</span><span class="sxs-lookup"><span data-stu-id="bfeb3-195">Description</span></span> | <span data-ttu-id="bfeb3-196">Required</span><span class="sxs-lookup"><span data-stu-id="bfeb3-196">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfeb3-197">**query**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-197">**query**</span></span> |<span data-ttu-id="bfeb3-198">Use the custom query to read the data.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-198">Use the custom query to read the data.</span></span> | <span data-ttu-id="bfeb3-199">No (if the **tableName** property of a dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-199">No (if the **tableName** property of a dataset is specified)</span></span> |

## <a name="use-unload-to-copy-data-from-amazon-redshift"></a><span data-ttu-id="bfeb3-200">Use UNLOAD to copy data from Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="bfeb3-200">Use UNLOAD to copy data from Amazon Redshift</span></span>

<span data-ttu-id="bfeb3-201">The Amazon Redshift [**UNLOAD**](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html) command unloads the results of a query to one or more files on Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-201">The Amazon Redshift [**UNLOAD**](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html) command unloads the results of a query to one or more files on Amazon S3.</span></span> <span data-ttu-id="bfeb3-202">This command is recommended by Amazon for copying large datasets from Redshift.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-202">This command is recommended by Amazon for copying large datasets from Redshift.</span></span>

<span data-ttu-id="bfeb3-203">**Example: Copy data from Amazon Redshift to Azure SQL Data Warehouse**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-203">**Example: Copy data from Amazon Redshift to Azure SQL Data Warehouse**</span></span>

<span data-ttu-id="bfeb3-204">This example copies data from Amazon Redshift to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-204">This example copies data from Amazon Redshift to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bfeb3-205">The example uses the Redshift **UNLOAD** command, staged copy data, and Microsoft PolyBase.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-205">The example uses the Redshift **UNLOAD** command, staged copy data, and Microsoft PolyBase.</span></span>

<span data-ttu-id="bfeb3-206">For this sample use case, Copy Activity first unloads the data from Amazon Redshift to Amazon S3 as configured in the  **redshiftUnloadSettings** option.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-206">For this sample use case, Copy Activity first unloads the data from Amazon Redshift to Amazon S3 as configured in the  **redshiftUnloadSettings** option.</span></span> <span data-ttu-id="bfeb3-207">Next, the data is copied from Amazon S3 to Azure Blob storage as specified in the **stagingSettings** option.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-207">Next, the data is copied from Amazon S3 to Azure Blob storage as specified in the **stagingSettings** option.</span></span> <span data-ttu-id="bfeb3-208">Finally, PolyBase loads the data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-208">Finally, PolyBase loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="bfeb3-209">All of the interim formats are handled by Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-209">All of the interim formats are handled by Copy Activity.</span></span>

![Copy workflow from Amazon Redshift to SQL Data Warehouse](media\data-factory-amazon-redshift-connector\redshift-to-sql-dw-copy-workflow.png)

```json
{
    "name": "CopyFromRedshiftToSQLDW",
    "type": "Copy",
    "typeProperties": {
        "source": {
            "type": "AmazonRedshiftSource",
            "query": "select * from MyTable",
            "redshiftUnloadSettings": {
                "s3LinkedServiceName":"MyAmazonS3StorageLinkedService",
                "bucketName": "bucketForUnload"
            }
        },
        "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyAzureStorageLinkedService",
            "path": "adfstagingcopydata"
        },
        "cloudDataMovementUnits": 32
        .....
    }
}
```

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob-storage"></a><span data-ttu-id="bfeb3-211">JSON example: Copy data from Amazon Redshift to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="bfeb3-211">JSON example: Copy data from Amazon Redshift to Azure Blob storage</span></span>
<span data-ttu-id="bfeb3-212">This sample shows how to copy data from an Amazon Redshift database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-212">This sample shows how to copy data from an Amazon Redshift database to Azure Blob Storage.</span></span> <span data-ttu-id="bfeb3-213">Data can be copied directly to any [supported sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-213">Data can be copied directly to any [supported sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity.</span></span>  

<span data-ttu-id="bfeb3-214">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="bfeb3-214">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="bfeb3-215">A linked service of type [AmazonRedshift](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-215">A linked service of type [AmazonRedshift](#linked-service-properties)</span></span>
* <span data-ttu-id="bfeb3-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="bfeb3-217">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-217">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="bfeb3-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="bfeb3-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="bfeb3-219">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties) properties</span><span class="sxs-lookup"><span data-stu-id="bfeb3-219">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties) properties</span></span>

<span data-ttu-id="bfeb3-220">The sample copies data from a query result in Amazon Redshift to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-220">The sample copies data from a query result in Amazon Redshift to an Azure blob hourly.</span></span> <span data-ttu-id="bfeb3-221">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-221">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="bfeb3-222">**Amazon Redshift linked service**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-222">**Amazon Redshift linked service**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="bfeb3-223">**Azure Blob storage linked service**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-223">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="bfeb3-224">**Amazon Redshift input dataset**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-224">**Amazon Redshift input dataset**</span></span>

<span data-ttu-id="bfeb3-225">The **external** property is set to "true" to inform the Data Factory service that the dataset is external to the data factory.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-225">The **external** property is set to "true" to inform the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="bfeb3-226">This property setting indicates that the dataset is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-226">This property setting indicates that the dataset is not produced by an activity in the data factory.</span></span> <span data-ttu-id="bfeb3-227">Set the property to true on an input dataset that is not produced by an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-227">Set the property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="bfeb3-228">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-228">**Azure Blob output dataset**</span></span>

<span data-ttu-id="bfeb3-229">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-229">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="bfeb3-230">The **folderPath** property for the blob is dynamically evaluated.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-230">The **folderPath** property for the blob is dynamically evaluated.</span></span> <span data-ttu-id="bfeb3-231">The property value is based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-231">The property value is based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bfeb3-232">The folder path uses the year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-232">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="bfeb3-233">**Copy activity in a pipeline with an Azure Redshift source (of type RelationalSource) and an Azure Blob sink**</span><span class="sxs-lookup"><span data-stu-id="bfeb3-233">**Copy activity in a pipeline with an Azure Redshift source (of type RelationalSource) and an Azure Blob sink**</span></span>

<span data-ttu-id="bfeb3-234">The pipeline contains a copy activity that is configured to use the input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-234">The pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="bfeb3-235">The pipeline is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-235">The pipeline is scheduled to run every hour.</span></span> <span data-ttu-id="bfeb3-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="bfeb3-237">The SQL query specified for the **query** property selects the data to copy from the past hour.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-237">The SQL query specified for the **query** property selects the data to copy from the past hour.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "AmazonRedshiftSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)",
                        "redshiftUnloadSettings": {
                            "s3LinkedServiceName":"myS3Storage",
                            "bucketName": "bucketForUnload"
                        }
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    },
                    "cloudDataMovementUnits": 32
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="bfeb3-238">Type mapping for Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="bfeb3-238">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="bfeb3-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type.</span></span> <span data-ttu-id="bfeb3-240">The types are converted by using a two-step approach:</span><span class="sxs-lookup"><span data-stu-id="bfeb3-240">The types are converted by using a two-step approach:</span></span>

1. <span data-ttu-id="bfeb3-241">Convert from a native source type to a .NET type</span><span class="sxs-lookup"><span data-stu-id="bfeb3-241">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="bfeb3-242">Convert from a .NET type to a native sink type</span><span class="sxs-lookup"><span data-stu-id="bfeb3-242">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="bfeb3-243">The following mappings are used when Copy Activity converts the data from an Amazon Redshift type to a .NET type:</span><span class="sxs-lookup"><span data-stu-id="bfeb3-243">The following mappings are used when Copy Activity converts the data from an Amazon Redshift type to a .NET type:</span></span>

| <span data-ttu-id="bfeb3-244">Amazon Redshift type</span><span class="sxs-lookup"><span data-stu-id="bfeb3-244">Amazon Redshift type</span></span> | <span data-ttu-id="bfeb3-245">.NET type</span><span class="sxs-lookup"><span data-stu-id="bfeb3-245">.NET type</span></span> |
| --- | --- |
| <span data-ttu-id="bfeb3-246">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="bfeb3-246">SMALLINT</span></span> |<span data-ttu-id="bfeb3-247">Int16</span><span class="sxs-lookup"><span data-stu-id="bfeb3-247">Int16</span></span> |
| <span data-ttu-id="bfeb3-248">INTEGER</span><span class="sxs-lookup"><span data-stu-id="bfeb3-248">INTEGER</span></span> |<span data-ttu-id="bfeb3-249">Int32</span><span class="sxs-lookup"><span data-stu-id="bfeb3-249">Int32</span></span> |
| <span data-ttu-id="bfeb3-250">BIGINT</span><span class="sxs-lookup"><span data-stu-id="bfeb3-250">BIGINT</span></span> |<span data-ttu-id="bfeb3-251">Int64</span><span class="sxs-lookup"><span data-stu-id="bfeb3-251">Int64</span></span> |
| <span data-ttu-id="bfeb3-252">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="bfeb3-252">DECIMAL</span></span> |<span data-ttu-id="bfeb3-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="bfeb3-253">Decimal</span></span> |
| <span data-ttu-id="bfeb3-254">REAL</span><span class="sxs-lookup"><span data-stu-id="bfeb3-254">REAL</span></span> |<span data-ttu-id="bfeb3-255">Single</span><span class="sxs-lookup"><span data-stu-id="bfeb3-255">Single</span></span> |
| <span data-ttu-id="bfeb3-256">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="bfeb3-256">DOUBLE PRECISION</span></span> |<span data-ttu-id="bfeb3-257">Double</span><span class="sxs-lookup"><span data-stu-id="bfeb3-257">Double</span></span> |
| <span data-ttu-id="bfeb3-258">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="bfeb3-258">BOOLEAN</span></span> |<span data-ttu-id="bfeb3-259">String</span><span class="sxs-lookup"><span data-stu-id="bfeb3-259">String</span></span> |
| <span data-ttu-id="bfeb3-260">CHAR</span><span class="sxs-lookup"><span data-stu-id="bfeb3-260">CHAR</span></span> |<span data-ttu-id="bfeb3-261">String</span><span class="sxs-lookup"><span data-stu-id="bfeb3-261">String</span></span> |
| <span data-ttu-id="bfeb3-262">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="bfeb3-262">VARCHAR</span></span> |<span data-ttu-id="bfeb3-263">String</span><span class="sxs-lookup"><span data-stu-id="bfeb3-263">String</span></span> |
| <span data-ttu-id="bfeb3-264">DATE</span><span class="sxs-lookup"><span data-stu-id="bfeb3-264">DATE</span></span> |<span data-ttu-id="bfeb3-265">DateTime</span><span class="sxs-lookup"><span data-stu-id="bfeb3-265">DateTime</span></span> |
| <span data-ttu-id="bfeb3-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="bfeb3-266">TIMESTAMP</span></span> |<span data-ttu-id="bfeb3-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="bfeb3-267">DateTime</span></span> |
| <span data-ttu-id="bfeb3-268">TEXT</span><span class="sxs-lookup"><span data-stu-id="bfeb3-268">TEXT</span></span> |<span data-ttu-id="bfeb3-269">String</span><span class="sxs-lookup"><span data-stu-id="bfeb3-269">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="bfeb3-270">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="bfeb3-270">Map source to sink columns</span></span>
<span data-ttu-id="bfeb3-271">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-271">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="bfeb3-272">Repeatable reads from relational sources</span><span class="sxs-lookup"><span data-stu-id="bfeb3-272">Repeatable reads from relational sources</span></span>
<span data-ttu-id="bfeb3-273">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-273">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="bfeb3-274">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-274">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="bfeb3-275">You can also configure the retry **policy** for a dataset to rerun a slice when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-275">You can also configure the retry **policy** for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="bfeb3-276">Make sure that the same data is read, no matter how many times the slice is rerun.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-276">Make sure that the same data is read, no matter how many times the slice is rerun.</span></span> <span data-ttu-id="bfeb3-277">Also make sure that the same data is read regardless of how you rerun the slice.</span><span class="sxs-lookup"><span data-stu-id="bfeb3-277">Also make sure that the same data is read regardless of how you rerun the slice.</span></span> <span data-ttu-id="bfeb3-278">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-278">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bfeb3-279">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="bfeb3-279">Performance and tuning</span></span>
<span data-ttu-id="bfeb3-280">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-280">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bfeb3-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfeb3-281">Next steps</span></span>
<span data-ttu-id="bfeb3-282">For step-by-step instructions for creating a pipeline with Copy Activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="bfeb3-282">For step-by-step instructions for creating a pipeline with Copy Activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
