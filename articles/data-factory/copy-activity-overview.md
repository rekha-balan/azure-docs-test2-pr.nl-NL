---
title: Copy Activity in Azure Data Factory | Microsoft Docs
description: Learn about the copy activity in Azure Data Factory that you can use to copy data from a supported source data store to a supported sink data store.
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
ms.date: 06/15/2018
ms.author: jingwang
ms.openlocfilehash: 8e34b0823b7f10455ac0b66fb0614d3946f2382e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871171"
---
# <a name="copy-activity-in-azure-data-factory"></a><span data-ttu-id="2bd6e-103">Copy Activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2bd6e-103">Copy Activity in Azure Data Factory</span></span>

## <a name="overview"></a><span data-ttu-id="2bd6e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2bd6e-104">Overview</span></span>

> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-data-movement-activities.md)
> * [Current version](copy-activity-overview.md)

<span data-ttu-id="2bd6e-107">In Azure Data Factory, you can use Copy Activity to copy data among data stores located on-premises and in the cloud.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-107">In Azure Data Factory, you can use Copy Activity to copy data among data stores located on-premises and in the cloud.</span></span> <span data-ttu-id="2bd6e-108">After the data is copied, it can be further transformed and analyzed.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-108">After the data is copied, it can be further transformed and analyzed.</span></span> <span data-ttu-id="2bd6e-109">You can also use Copy Activity to publish transformation and analysis results for business intelligence (BI) and application consumption.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-109">You can also use Copy Activity to publish transformation and analysis results for business intelligence (BI) and application consumption.</span></span>

![Role of Copy Activity](media/copy-activity-overview/copy-activity.png)

<span data-ttu-id="2bd6e-111">Copy Activity is executed on an [Integration Runtime](concepts-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-111">Copy Activity is executed on an [Integration Runtime](concepts-integration-runtime.md).</span></span> <span data-ttu-id="2bd6e-112">For different data copy scenario, different flavor of Integration Runtime can be leveraged:</span><span class="sxs-lookup"><span data-stu-id="2bd6e-112">For different data copy scenario, different flavor of Integration Runtime can be leveraged:</span></span>

* <span data-ttu-id="2bd6e-113">When copying data between data stores that both are publicly accessible, copy activity can be empowered by **Azure Integration Runtime**, which is secure, reliable, scalable, and [globally available](concepts-integration-runtime.md#integration-runtime-location).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-113">When copying data between data stores that both are publicly accessible, copy activity can be empowered by **Azure Integration Runtime**, which is secure, reliable, scalable, and [globally available](concepts-integration-runtime.md#integration-runtime-location).</span></span>
* <span data-ttu-id="2bd6e-114">When copying data from/to data stores located on-premises or in a network with access control (for example, Azure Virtual Network), you need to set up a **self-hosted Integrated Runtime** to empower data copy.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-114">When copying data from/to data stores located on-premises or in a network with access control (for example, Azure Virtual Network), you need to set up a **self-hosted Integrated Runtime** to empower data copy.</span></span>

<span data-ttu-id="2bd6e-115">Integration Runtime needs to be associated with each source and sink data store.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-115">Integration Runtime needs to be associated with each source and sink data store.</span></span> <span data-ttu-id="2bd6e-116">Learn details on how copy activity [determines which IR to use](concepts-integration-runtime.md#determining-which-ir-to-use).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-116">Learn details on how copy activity [determines which IR to use](concepts-integration-runtime.md#determining-which-ir-to-use).</span></span>

<span data-ttu-id="2bd6e-117">Copy Activity goes through the following stages to copy data from a source to a sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-117">Copy Activity goes through the following stages to copy data from a source to a sink.</span></span> <span data-ttu-id="2bd6e-118">The service that powers Copy Activity:</span><span class="sxs-lookup"><span data-stu-id="2bd6e-118">The service that powers Copy Activity:</span></span>

1. <span data-ttu-id="2bd6e-119">Reads data from a source data store.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-119">Reads data from a source data store.</span></span>
2. <span data-ttu-id="2bd6e-120">Performs serialization/deserialization, compression/decompression, column mapping, etc. It does these operations based on the configurations of the input dataset, output dataset, and Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-120">Performs serialization/deserialization, compression/decompression, column mapping, etc. It does these operations based on the configurations of the input dataset, output dataset, and Copy Activity.</span></span>
3. <span data-ttu-id="2bd6e-121">Writes data to the sink/destination data store.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-121">Writes data to the sink/destination data store.</span></span>

![Copy Activity Overview](media/copy-activity-overview/copy-activity-overview.png)

## <a name="supported-data-stores-and-formats"></a><span data-ttu-id="2bd6e-123">Supported data stores and formats</span><span class="sxs-lookup"><span data-stu-id="2bd6e-123">Supported data stores and formats</span></span>

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores.md)]

### <a name="supported-file-formats"></a><span data-ttu-id="2bd6e-124">Supported file formats</span><span class="sxs-lookup"><span data-stu-id="2bd6e-124">Supported file formats</span></span>

<span data-ttu-id="2bd6e-125">You can use Copy Activity to **copy files as-is** between two file-based data stores, in which case the data is copied efficiently without any serialization/deserialization.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-125">You can use Copy Activity to **copy files as-is** between two file-based data stores, in which case the data is copied efficiently without any serialization/deserialization.</span></span>

<span data-ttu-id="2bd6e-126">Copy Activity also supports reading from and writing to files in specified formats: **Text, JSON, Avro, ORC, and Parquet**, and compression codec **GZip, Deflate, BZip2, and ZipDeflate** are supported.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-126">Copy Activity also supports reading from and writing to files in specified formats: **Text, JSON, Avro, ORC, and Parquet**, and compression codec **GZip, Deflate, BZip2, and ZipDeflate** are supported.</span></span> <span data-ttu-id="2bd6e-127">See [Supported file and compression formats](supported-file-formats-and-compression-codecs.md) with details.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-127">See [Supported file and compression formats](supported-file-formats-and-compression-codecs.md) with details.</span></span>

<span data-ttu-id="2bd6e-128">For example, you can do the following copy activities:</span><span class="sxs-lookup"><span data-stu-id="2bd6e-128">For example, you can do the following copy activities:</span></span>

* <span data-ttu-id="2bd6e-129">Copy data in on-premises SQL Server and write to Azure Data Lake Store in ORC format.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-129">Copy data in on-premises SQL Server and write to Azure Data Lake Store in ORC format.</span></span>
* <span data-ttu-id="2bd6e-130">Copy files in text (CSV) format from on-premises File System and write to Azure Blob in Avro format.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-130">Copy files in text (CSV) format from on-premises File System and write to Azure Blob in Avro format.</span></span>
* <span data-ttu-id="2bd6e-131">Copy zipped files from on-premises File System and decompress then land to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-131">Copy zipped files from on-premises File System and decompress then land to Azure Data Lake Store.</span></span>
* <span data-ttu-id="2bd6e-132">Copy data in GZip compressed text (CSV) format from Azure Blob and write to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-132">Copy data in GZip compressed text (CSV) format from Azure Blob and write to Azure SQL Database.</span></span>

## <a name="supported-regions"></a><span data-ttu-id="2bd6e-133">Supported regions</span><span class="sxs-lookup"><span data-stu-id="2bd6e-133">Supported regions</span></span>

<span data-ttu-id="2bd6e-134">The service that powers Copy Activity is available globally in the regions and geographies listed in [Azure Integration Runtime locations](concepts-integration-runtime.md#integration-runtime-location).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-134">The service that powers Copy Activity is available globally in the regions and geographies listed in [Azure Integration Runtime locations](concepts-integration-runtime.md#integration-runtime-location).</span></span> <span data-ttu-id="2bd6e-135">The globally available topology ensures efficient data movement that usually avoids cross-region hops.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-135">The globally available topology ensures efficient data movement that usually avoids cross-region hops.</span></span> <span data-ttu-id="2bd6e-136">See [Services by region](https://azure.microsoft.com/regions/#services) for availability of Data Factory and Data Movement in a region.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-136">See [Services by region](https://azure.microsoft.com/regions/#services) for availability of Data Factory and Data Movement in a region.</span></span>

## <a name="configuration"></a><span data-ttu-id="2bd6e-137">Configuration</span><span class="sxs-lookup"><span data-stu-id="2bd6e-137">Configuration</span></span>

<span data-ttu-id="2bd6e-138">To use copy activity in Azure Data Factory, you need to:</span><span class="sxs-lookup"><span data-stu-id="2bd6e-138">To use copy activity in Azure Data Factory, you need to:</span></span>

1. <span data-ttu-id="2bd6e-139">**Create linked services for source data store and sink data store.**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-139">**Create linked services for source data store and sink data store.**</span></span> <span data-ttu-id="2bd6e-140">Refer to the connector article's "Linked service properties" section on how to configure and the supported properties.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-140">Refer to the connector article's "Linked service properties" section on how to configure and the supported properties.</span></span> <span data-ttu-id="2bd6e-141">You can find the supported connector list in [Supported data stores and formats](#supported-data-stores-and-formats) section.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-141">You can find the supported connector list in [Supported data stores and formats](#supported-data-stores-and-formats) section.</span></span>
2. <span data-ttu-id="2bd6e-142">**Create datasets for source and sink.**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-142">**Create datasets for source and sink.**</span></span> <span data-ttu-id="2bd6e-143">Refer to the source and sink connector articles' "Dataset properties" section on how to configure and the supported properties.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-143">Refer to the source and sink connector articles' "Dataset properties" section on how to configure and the supported properties.</span></span>
3. <span data-ttu-id="2bd6e-144">**Create a pipeline with copy activity.**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-144">**Create a pipeline with copy activity.**</span></span> <span data-ttu-id="2bd6e-145">The next section provides an example.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-145">The next section provides an example.</span></span>  

### <a name="syntax"></a><span data-ttu-id="2bd6e-146">Syntax</span><span class="sxs-lookup"><span data-stu-id="2bd6e-146">Syntax</span></span>

<span data-ttu-id="2bd6e-147">The following template of a copy activity contains an exhaustive list of supported properties.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-147">The following template of a copy activity contains an exhaustive list of supported properties.</span></span> <span data-ttu-id="2bd6e-148">Specify the ones that fit your scenario.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-148">Specify the ones that fit your scenario.</span></span>

```json
"activities":[
    {
        "name": "CopyActivityTemplate",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<source dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<sink dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>",
                <properties>
            },
            "sink": {
                "type": "<sink type>"
                <properties>
            },
            "translator":
            {
                "type": "TabularTranslator",
                "columnMappings": "<column mapping>"
            },
            "dataIntegrationUnits": <number>,
            "parallelCopies": <number>,
            "enableStaging": true/false,
            "stagingSettings": {
                <properties>
            },
            "enableSkipIncompatibleRow": true/false,
            "redirectIncompatibleRowSettings": {
                <properties>
            }
        }
    }
]
```

### <a name="syntax-details"></a><span data-ttu-id="2bd6e-149">Syntax details</span><span class="sxs-lookup"><span data-stu-id="2bd6e-149">Syntax details</span></span>

| <span data-ttu-id="2bd6e-150">Property</span><span class="sxs-lookup"><span data-stu-id="2bd6e-150">Property</span></span> | <span data-ttu-id="2bd6e-151">Description</span><span class="sxs-lookup"><span data-stu-id="2bd6e-151">Description</span></span> | <span data-ttu-id="2bd6e-152">Required</span><span class="sxs-lookup"><span data-stu-id="2bd6e-152">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2bd6e-153">type</span><span class="sxs-lookup"><span data-stu-id="2bd6e-153">type</span></span> | <span data-ttu-id="2bd6e-154">The type property of a copy activity must be set to: **Copy**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-154">The type property of a copy activity must be set to: **Copy**</span></span> | <span data-ttu-id="2bd6e-155">Yes</span><span class="sxs-lookup"><span data-stu-id="2bd6e-155">Yes</span></span> |
| <span data-ttu-id="2bd6e-156">inputs</span><span class="sxs-lookup"><span data-stu-id="2bd6e-156">inputs</span></span> | <span data-ttu-id="2bd6e-157">Specify the dataset you created which points to the source data.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-157">Specify the dataset you created which points to the source data.</span></span> <span data-ttu-id="2bd6e-158">Copy activity supports only a single input.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-158">Copy activity supports only a single input.</span></span> | <span data-ttu-id="2bd6e-159">Yes</span><span class="sxs-lookup"><span data-stu-id="2bd6e-159">Yes</span></span> |
| <span data-ttu-id="2bd6e-160">outputs</span><span class="sxs-lookup"><span data-stu-id="2bd6e-160">outputs</span></span> | <span data-ttu-id="2bd6e-161">Specify the dataset you created which points to the sink data.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-161">Specify the dataset you created which points to the sink data.</span></span> <span data-ttu-id="2bd6e-162">Copy activity supports only a single output.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-162">Copy activity supports only a single output.</span></span> | <span data-ttu-id="2bd6e-163">Yes</span><span class="sxs-lookup"><span data-stu-id="2bd6e-163">Yes</span></span> |
| <span data-ttu-id="2bd6e-164">typeProperties</span><span class="sxs-lookup"><span data-stu-id="2bd6e-164">typeProperties</span></span> | <span data-ttu-id="2bd6e-165">A group of properties to configure copy activity.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-165">A group of properties to configure copy activity.</span></span> | <span data-ttu-id="2bd6e-166">Yes</span><span class="sxs-lookup"><span data-stu-id="2bd6e-166">Yes</span></span> |
| <span data-ttu-id="2bd6e-167">source</span><span class="sxs-lookup"><span data-stu-id="2bd6e-167">source</span></span> | <span data-ttu-id="2bd6e-168">Specify the copy source type and the corresponding properties on how to retrieve data.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-168">Specify the copy source type and the corresponding properties on how to retrieve data.</span></span><br/><br/><span data-ttu-id="2bd6e-169">Learn details from the "Copy activity properties" section in connector article listed in [Supported data stores and formats](#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-169">Learn details from the "Copy activity properties" section in connector article listed in [Supported data stores and formats](#supported-data-stores-and-formats).</span></span> | <span data-ttu-id="2bd6e-170">Yes</span><span class="sxs-lookup"><span data-stu-id="2bd6e-170">Yes</span></span> |
| <span data-ttu-id="2bd6e-171">sink</span><span class="sxs-lookup"><span data-stu-id="2bd6e-171">sink</span></span> | <span data-ttu-id="2bd6e-172">Specify the copy sink type and the corresponding properties on how to write data.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-172">Specify the copy sink type and the corresponding properties on how to write data.</span></span><br/><br/><span data-ttu-id="2bd6e-173">Learn details from the "Copy activity properties" section in connector article listed in [Supported data stores and formats](#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-173">Learn details from the "Copy activity properties" section in connector article listed in [Supported data stores and formats](#supported-data-stores-and-formats).</span></span> | <span data-ttu-id="2bd6e-174">Yes</span><span class="sxs-lookup"><span data-stu-id="2bd6e-174">Yes</span></span> |
| <span data-ttu-id="2bd6e-175">translator</span><span class="sxs-lookup"><span data-stu-id="2bd6e-175">translator</span></span> | <span data-ttu-id="2bd6e-176">Specify explicit column mappings from source to sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-176">Specify explicit column mappings from source to sink.</span></span> <span data-ttu-id="2bd6e-177">Applies when the default copy behavior cannot fulfill your need.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-177">Applies when the default copy behavior cannot fulfill your need.</span></span><br/><br/><span data-ttu-id="2bd6e-178">Learn details from [Schema and data type mapping](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-178">Learn details from [Schema and data type mapping](copy-activity-schema-and-type-mapping.md).</span></span> | <span data-ttu-id="2bd6e-179">No</span><span class="sxs-lookup"><span data-stu-id="2bd6e-179">No</span></span> |
| <span data-ttu-id="2bd6e-180">dataIntegrationUnits</span><span class="sxs-lookup"><span data-stu-id="2bd6e-180">dataIntegrationUnits</span></span> | <span data-ttu-id="2bd6e-181">Specify the powerfulness of [Azure Integration Runtime](concepts-integration-runtime.md) to empower data copy.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-181">Specify the powerfulness of [Azure Integration Runtime](concepts-integration-runtime.md) to empower data copy.</span></span> <span data-ttu-id="2bd6e-182">Formerly known as cloud Data Movement Units (DMU).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-182">Formerly known as cloud Data Movement Units (DMU).</span></span> <br/><br/><span data-ttu-id="2bd6e-183">Learn details from [Data Integration Units](copy-activity-performance.md#data-integration-units).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-183">Learn details from [Data Integration Units](copy-activity-performance.md#data-integration-units).</span></span> | <span data-ttu-id="2bd6e-184">No</span><span class="sxs-lookup"><span data-stu-id="2bd6e-184">No</span></span> |
| <span data-ttu-id="2bd6e-185">parallelCopies</span><span class="sxs-lookup"><span data-stu-id="2bd6e-185">parallelCopies</span></span> | <span data-ttu-id="2bd6e-186">Specify the parallelism that you want Copy Activity to use when reading data from source and writing data to sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-186">Specify the parallelism that you want Copy Activity to use when reading data from source and writing data to sink.</span></span><br/><br/><span data-ttu-id="2bd6e-187">Learn details from [Parallel copy](copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-187">Learn details from [Parallel copy](copy-activity-performance.md#parallel-copy).</span></span> | <span data-ttu-id="2bd6e-188">No</span><span class="sxs-lookup"><span data-stu-id="2bd6e-188">No</span></span> |
| <span data-ttu-id="2bd6e-189">enableStaging</span><span class="sxs-lookup"><span data-stu-id="2bd6e-189">enableStaging</span></span><br/><span data-ttu-id="2bd6e-190">stagingSettings</span><span class="sxs-lookup"><span data-stu-id="2bd6e-190">stagingSettings</span></span> | <span data-ttu-id="2bd6e-191">Choose to stage the interim data in aa blob storage instead of directly copy data from source to sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-191">Choose to stage the interim data in aa blob storage instead of directly copy data from source to sink.</span></span><br/><br/><span data-ttu-id="2bd6e-192">Learn the useful scenarios and configuration details from [Staged copy](copy-activity-performance.md#staged-copy).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-192">Learn the useful scenarios and configuration details from [Staged copy](copy-activity-performance.md#staged-copy).</span></span> | <span data-ttu-id="2bd6e-193">No</span><span class="sxs-lookup"><span data-stu-id="2bd6e-193">No</span></span> |
| <span data-ttu-id="2bd6e-194">enableSkipIncompatibleRow</span><span class="sxs-lookup"><span data-stu-id="2bd6e-194">enableSkipIncompatibleRow</span></span><br/><span data-ttu-id="2bd6e-195">redirectIncompatibleRowSettings</span><span class="sxs-lookup"><span data-stu-id="2bd6e-195">redirectIncompatibleRowSettings</span></span>| <span data-ttu-id="2bd6e-196">Choose how to handle incompatible rows when copying data from source to sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-196">Choose how to handle incompatible rows when copying data from source to sink.</span></span><br/><br/><span data-ttu-id="2bd6e-197">Learn details from [Fault tolerance](copy-activity-fault-tolerance.md).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-197">Learn details from [Fault tolerance](copy-activity-fault-tolerance.md).</span></span> | <span data-ttu-id="2bd6e-198">No</span><span class="sxs-lookup"><span data-stu-id="2bd6e-198">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="2bd6e-199">Monitoring</span><span class="sxs-lookup"><span data-stu-id="2bd6e-199">Monitoring</span></span>

<span data-ttu-id="2bd6e-200">You can monitor the copy activity run on Azure Data Factory "Author & Monitor" UI or programmatically.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-200">You can monitor the copy activity run on Azure Data Factory "Author & Monitor" UI or programmatically.</span></span> <span data-ttu-id="2bd6e-201">You can then compare the performance and configuration of your scenario to Copy Activity's [performance reference](copy-activity-performance.md#performance-reference) from in-house testing.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-201">You can then compare the performance and configuration of your scenario to Copy Activity's [performance reference](copy-activity-performance.md#performance-reference) from in-house testing.</span></span>

### <a name="monitor-visually"></a><span data-ttu-id="2bd6e-202">Monitor visually</span><span class="sxs-lookup"><span data-stu-id="2bd6e-202">Monitor visually</span></span>

<span data-ttu-id="2bd6e-203">To visually monitor the copy activity run, go to your data factory -> **Author & Monitor** -> **Monitor tab**, you see a list of pipeline runs with a "View Activity Runs" link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-203">To visually monitor the copy activity run, go to your data factory -> **Author & Monitor** -> **Monitor tab**, you see a list of pipeline runs with a "View Activity Runs" link in the **Actions** column.</span></span> 

![Monitor pipeline runs](./media/load-data-into-azure-data-lake-store/monitor-pipeline-runs.png)

<span data-ttu-id="2bd6e-205">Click to see the list of activities in this pipeline run.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-205">Click to see the list of activities in this pipeline run.</span></span> <span data-ttu-id="2bd6e-206">In the **Actions** column, you have links to the copy activity input, output, errors (if copy activity run fails), and details.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-206">In the **Actions** column, you have links to the copy activity input, output, errors (if copy activity run fails), and details.</span></span>

![Monitor activity runs](./media/load-data-into-azure-data-lake-store/monitor-activity-runs.png)

<span data-ttu-id="2bd6e-208">Click the "**Details**" link under **Actions** to see copy activity's execution details and performance characteristics.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-208">Click the "**Details**" link under **Actions** to see copy activity's execution details and performance characteristics.</span></span> <span data-ttu-id="2bd6e-209">It shows you information including volume/rows/files of data copied from source to sink, throughput, steps it goes through with corresponding duration and used configurations for your copy scenario.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-209">It shows you information including volume/rows/files of data copied from source to sink, throughput, steps it goes through with corresponding duration and used configurations for your copy scenario.</span></span>

<span data-ttu-id="2bd6e-210">**Example: copy from Amazon S3 to Azure Data Lake Store**
![Monitor activity run details](./media/copy-activity-overview/monitor-activity-run-details-adls.png)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-210">**Example: copy from Amazon S3 to Azure Data Lake Store**
![Monitor activity run details](./media/copy-activity-overview/monitor-activity-run-details-adls.png)</span></span>

<span data-ttu-id="2bd6e-211">**Example: copy from Azure SQL Database to Azure SQL Data Warehouse using staged copy**
![Monitor activity run details](./media/copy-activity-overview/monitor-activity-run-details-sql-dw.png)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-211">**Example: copy from Azure SQL Database to Azure SQL Data Warehouse using staged copy**
![Monitor activity run details](./media/copy-activity-overview/monitor-activity-run-details-sql-dw.png)</span></span>

### <a name="monitor-programmatically"></a><span data-ttu-id="2bd6e-212">Monitor programmatically</span><span class="sxs-lookup"><span data-stu-id="2bd6e-212">Monitor programmatically</span></span>

<span data-ttu-id="2bd6e-213">Copy activity execution details and performance characteristics are also returned in Copy Activity run result -> Output section.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-213">Copy activity execution details and performance characteristics are also returned in Copy Activity run result -> Output section.</span></span> <span data-ttu-id="2bd6e-214">Below is an exhaustive list; only the applicable ones to your copy scenario will show up.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-214">Below is an exhaustive list; only the applicable ones to your copy scenario will show up.</span></span> <span data-ttu-id="2bd6e-215">Learn how to monitor activity run from [quickstart monitoring section](quickstart-create-data-factory-dot-net.md#monitor-a-pipeline-run).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-215">Learn how to monitor activity run from [quickstart monitoring section](quickstart-create-data-factory-dot-net.md#monitor-a-pipeline-run).</span></span>

| <span data-ttu-id="2bd6e-216">Property name</span><span class="sxs-lookup"><span data-stu-id="2bd6e-216">Property name</span></span>  | <span data-ttu-id="2bd6e-217">Description</span><span class="sxs-lookup"><span data-stu-id="2bd6e-217">Description</span></span> | <span data-ttu-id="2bd6e-218">Unit</span><span class="sxs-lookup"><span data-stu-id="2bd6e-218">Unit</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2bd6e-219">dataRead</span><span class="sxs-lookup"><span data-stu-id="2bd6e-219">dataRead</span></span> | <span data-ttu-id="2bd6e-220">Data size read from source</span><span class="sxs-lookup"><span data-stu-id="2bd6e-220">Data size read from source</span></span> | <span data-ttu-id="2bd6e-221">Int64 value in **bytes**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-221">Int64 value in **bytes**</span></span> |
| <span data-ttu-id="2bd6e-222">dataWritten</span><span class="sxs-lookup"><span data-stu-id="2bd6e-222">dataWritten</span></span> | <span data-ttu-id="2bd6e-223">Data size written to sink</span><span class="sxs-lookup"><span data-stu-id="2bd6e-223">Data size written to sink</span></span> | <span data-ttu-id="2bd6e-224">Int64 value in **bytes**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-224">Int64 value in **bytes**</span></span> |
| <span data-ttu-id="2bd6e-225">filesRead</span><span class="sxs-lookup"><span data-stu-id="2bd6e-225">filesRead</span></span> | <span data-ttu-id="2bd6e-226">Number of files being copied when copying data from file storage.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-226">Number of files being copied when copying data from file storage.</span></span> | <span data-ttu-id="2bd6e-227">Int64 value (no unit)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-227">Int64 value (no unit)</span></span> |
| <span data-ttu-id="2bd6e-228">filesWritten</span><span class="sxs-lookup"><span data-stu-id="2bd6e-228">filesWritten</span></span> | <span data-ttu-id="2bd6e-229">Number of files being copied when copying data to file storage.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-229">Number of files being copied when copying data to file storage.</span></span> | <span data-ttu-id="2bd6e-230">Int64 value (no unit)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-230">Int64 value (no unit)</span></span> |
| <span data-ttu-id="2bd6e-231">rowsCopied</span><span class="sxs-lookup"><span data-stu-id="2bd6e-231">rowsCopied</span></span> | <span data-ttu-id="2bd6e-232">Number of rows being copied (not applicable for binary copy).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-232">Number of rows being copied (not applicable for binary copy).</span></span> | <span data-ttu-id="2bd6e-233">Int64 value (no unit)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-233">Int64 value (no unit)</span></span> |
| <span data-ttu-id="2bd6e-234">rowsSkipped</span><span class="sxs-lookup"><span data-stu-id="2bd6e-234">rowsSkipped</span></span> | <span data-ttu-id="2bd6e-235">Number of incompatible rows being skipped.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-235">Number of incompatible rows being skipped.</span></span> <span data-ttu-id="2bd6e-236">You can turn on the feature by set "enableSkipIncompatibleRow" to true.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-236">You can turn on the feature by set "enableSkipIncompatibleRow" to true.</span></span> | <span data-ttu-id="2bd6e-237">Int64 value (no unit)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-237">Int64 value (no unit)</span></span> |
| <span data-ttu-id="2bd6e-238">throughput</span><span class="sxs-lookup"><span data-stu-id="2bd6e-238">throughput</span></span> | <span data-ttu-id="2bd6e-239">Ratio at which data are transferred</span><span class="sxs-lookup"><span data-stu-id="2bd6e-239">Ratio at which data are transferred</span></span> | <span data-ttu-id="2bd6e-240">Floating point number in **KB/s**</span><span class="sxs-lookup"><span data-stu-id="2bd6e-240">Floating point number in **KB/s**</span></span> |
| <span data-ttu-id="2bd6e-241">copyDuration</span><span class="sxs-lookup"><span data-stu-id="2bd6e-241">copyDuration</span></span> | <span data-ttu-id="2bd6e-242">The duration of the copy</span><span class="sxs-lookup"><span data-stu-id="2bd6e-242">The duration of the copy</span></span> | <span data-ttu-id="2bd6e-243">Int32 value in seconds</span><span class="sxs-lookup"><span data-stu-id="2bd6e-243">Int32 value in seconds</span></span> |
| <span data-ttu-id="2bd6e-244">sqlDwPolyBase</span><span class="sxs-lookup"><span data-stu-id="2bd6e-244">sqlDwPolyBase</span></span> | <span data-ttu-id="2bd6e-245">If PolyBase is used when copying data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-245">If PolyBase is used when copying data into SQL Data Warehouse.</span></span> | <span data-ttu-id="2bd6e-246">Boolean</span><span class="sxs-lookup"><span data-stu-id="2bd6e-246">Boolean</span></span> |
| <span data-ttu-id="2bd6e-247">redshiftUnload</span><span class="sxs-lookup"><span data-stu-id="2bd6e-247">redshiftUnload</span></span> | <span data-ttu-id="2bd6e-248">If UNLOAD is used when copying data from Redshift.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-248">If UNLOAD is used when copying data from Redshift.</span></span> | <span data-ttu-id="2bd6e-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="2bd6e-249">Boolean</span></span> |
| <span data-ttu-id="2bd6e-250">hdfsDistcp</span><span class="sxs-lookup"><span data-stu-id="2bd6e-250">hdfsDistcp</span></span> | <span data-ttu-id="2bd6e-251">If DistCp is used when copying data from HDFS.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-251">If DistCp is used when copying data from HDFS.</span></span> | <span data-ttu-id="2bd6e-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="2bd6e-252">Boolean</span></span> |
| <span data-ttu-id="2bd6e-253">effectiveIntegrationRuntime</span><span class="sxs-lookup"><span data-stu-id="2bd6e-253">effectiveIntegrationRuntime</span></span> | <span data-ttu-id="2bd6e-254">Show which Integration Runtime(s) is used to empower the activity run, in the format of `<IR name> (<region if it's Azure IR>)`.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-254">Show which Integration Runtime(s) is used to empower the activity run, in the format of `<IR name> (<region if it's Azure IR>)`.</span></span> | <span data-ttu-id="2bd6e-255">Text (string)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-255">Text (string)</span></span> |
| <span data-ttu-id="2bd6e-256">usedDataIntegrationUnits</span><span class="sxs-lookup"><span data-stu-id="2bd6e-256">usedDataIntegrationUnits</span></span> | <span data-ttu-id="2bd6e-257">The effective Data Integration Units during copy.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-257">The effective Data Integration Units during copy.</span></span> | <span data-ttu-id="2bd6e-258">Int32 value</span><span class="sxs-lookup"><span data-stu-id="2bd6e-258">Int32 value</span></span> |
| <span data-ttu-id="2bd6e-259">usedParallelCopies</span><span class="sxs-lookup"><span data-stu-id="2bd6e-259">usedParallelCopies</span></span> | <span data-ttu-id="2bd6e-260">The effective parallelCopies during copy.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-260">The effective parallelCopies during copy.</span></span> | <span data-ttu-id="2bd6e-261">Int32 value</span><span class="sxs-lookup"><span data-stu-id="2bd6e-261">Int32 value</span></span>|
| <span data-ttu-id="2bd6e-262">redirectRowPath</span><span class="sxs-lookup"><span data-stu-id="2bd6e-262">redirectRowPath</span></span> | <span data-ttu-id="2bd6e-263">Path to the log of skipped incompatible rows in the blob storage you configure under "redirectIncompatibleRowSettings".</span><span class="sxs-lookup"><span data-stu-id="2bd6e-263">Path to the log of skipped incompatible rows in the blob storage you configure under "redirectIncompatibleRowSettings".</span></span> <span data-ttu-id="2bd6e-264">See below example.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-264">See below example.</span></span> | <span data-ttu-id="2bd6e-265">Text (string)</span><span class="sxs-lookup"><span data-stu-id="2bd6e-265">Text (string)</span></span> |
| <span data-ttu-id="2bd6e-266">executionDetails</span><span class="sxs-lookup"><span data-stu-id="2bd6e-266">executionDetails</span></span> | <span data-ttu-id="2bd6e-267">More details on the stages copy activity goes through, and the corresponding steps, duration, used configurations, etc. It's not recommended to parse this section as it may change.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-267">More details on the stages copy activity goes through, and the corresponding steps, duration, used configurations, etc. It's not recommended to parse this section as it may change.</span></span> | <span data-ttu-id="2bd6e-268">Array</span><span class="sxs-lookup"><span data-stu-id="2bd6e-268">Array</span></span> |

```json
"output": {
    "dataRead": 107280845500,
    "dataWritten": 107280845500,
    "filesRead": 10,
    "filesWritten": 10,
    "copyDuration": 224,
    "throughput": 467707.344,
    "errors": [],
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US 2)",
    "usedDataIntegrationUnits": 32,
    "usedParallelCopies": 8,
    "executionDetails": [
        {
            "source": {
                "type": "AmazonS3"
            },
            "sink": {
                "type": "AzureDataLakeStore"
            },
            "status": "Succeeded",
            "start": "2018-01-17T15:13:00.3515165Z",
            "duration": 221,
            "usedDataIntegrationUnits": 32,
            "usedParallelCopies": 8,
            "detailedDurations": {
                "queuingDuration": 2,
                "transferDuration": 219
            }
        }
    ]
}
```

## <a name="schema-and-data-type-mapping"></a><span data-ttu-id="2bd6e-269">Schema and data type mapping</span><span class="sxs-lookup"><span data-stu-id="2bd6e-269">Schema and data type mapping</span></span>

<span data-ttu-id="2bd6e-270">See the [Schema and data type mapping](copy-activity-schema-and-type-mapping.md), which describes how copy activity maps your source data to sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-270">See the [Schema and data type mapping](copy-activity-schema-and-type-mapping.md), which describes how copy activity maps your source data to sink.</span></span>

## <a name="fault-tolerance"></a><span data-ttu-id="2bd6e-271">Fault tolerance</span><span class="sxs-lookup"><span data-stu-id="2bd6e-271">Fault tolerance</span></span>

<span data-ttu-id="2bd6e-272">By default, copy activity stops copying data and returns failure when it encounters incompatible data between source and sink.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-272">By default, copy activity stops copying data and returns failure when it encounters incompatible data between source and sink.</span></span> <span data-ttu-id="2bd6e-273">You can explicitly configure to skip and log the incompatible rows and only copy those compatible data to make the copy succeeded.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-273">You can explicitly configure to skip and log the incompatible rows and only copy those compatible data to make the copy succeeded.</span></span> <span data-ttu-id="2bd6e-274">See the [Copy Activity fault tolerance](copy-activity-fault-tolerance.md) on more details.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-274">See the [Copy Activity fault tolerance](copy-activity-fault-tolerance.md) on more details.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2bd6e-275">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="2bd6e-275">Performance and tuning</span></span>

<span data-ttu-id="2bd6e-276">See the [Copy Activity performance and tuning guide](copy-activity-performance.md), which describes key factors that affect the performance of data movement (Copy Activity) in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-276">See the [Copy Activity performance and tuning guide](copy-activity-performance.md), which describes key factors that affect the performance of data movement (Copy Activity) in Azure Data Factory.</span></span> <span data-ttu-id="2bd6e-277">It also lists the observed performance during internal testing and discusses various ways to optimize the performance of Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-277">It also lists the observed performance during internal testing and discusses various ways to optimize the performance of Copy Activity.</span></span>

## <a name="incremental-copy"></a><span data-ttu-id="2bd6e-278">Incremental copy</span><span class="sxs-lookup"><span data-stu-id="2bd6e-278">Incremental copy</span></span> 
<span data-ttu-id="2bd6e-279">Data Factory supports scenarios for incrementally copying delta data from a source data store to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-279">Data Factory supports scenarios for incrementally copying delta data from a source data store to a destination data store.</span></span> <span data-ttu-id="2bd6e-280">See [Tutorial: incrementally copy data](tutorial-incremental-copy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-280">See [Tutorial: incrementally copy data](tutorial-incremental-copy-overview.md).</span></span> 

## <a name="read-and-write-partitioned-data"></a><span data-ttu-id="2bd6e-281">Read and write partitioned data</span><span class="sxs-lookup"><span data-stu-id="2bd6e-281">Read and write partitioned data</span></span>
<span data-ttu-id="2bd6e-282">In version 1, Azure Data Factory supported reading or writing partitioned data by using SliceStart/SliceEnd/WindowStart/WindowEnd system variables.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-282">In version 1, Azure Data Factory supported reading or writing partitioned data by using SliceStart/SliceEnd/WindowStart/WindowEnd system variables.</span></span> <span data-ttu-id="2bd6e-283">In the current version, you can achieve this behavior by using a pipeline parameter and trigger's start time/scheduled time as a value of the parameter.</span><span class="sxs-lookup"><span data-stu-id="2bd6e-283">In the current version, you can achieve this behavior by using a pipeline parameter and trigger's start time/scheduled time as a value of the parameter.</span></span> <span data-ttu-id="2bd6e-284">For more information, see [How to read or write partitioned data](how-to-read-write-partitioned-data.md).</span><span class="sxs-lookup"><span data-stu-id="2bd6e-284">For more information, see [How to read or write partitioned data](how-to-read-write-partitioned-data.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bd6e-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="2bd6e-285">Next steps</span></span>
<span data-ttu-id="2bd6e-286">See the following quickstarts, tutorials, and samples:</span><span class="sxs-lookup"><span data-stu-id="2bd6e-286">See the following quickstarts, tutorials, and samples:</span></span>

- [<span data-ttu-id="2bd6e-287">Copy data from one location to another location in the same Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="2bd6e-287">Copy data from one location to another location in the same Azure Blob Storage</span></span>](quickstart-create-data-factory-dot-net.md)
- [<span data-ttu-id="2bd6e-288">Copy data from Azure Blob Storage to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2bd6e-288">Copy data from Azure Blob Storage to Azure SQL Database</span></span>](tutorial-copy-data-dot-net.md)
- [<span data-ttu-id="2bd6e-289">Copy data from on-premises SQL Server to Azure</span><span class="sxs-lookup"><span data-stu-id="2bd6e-289">Copy data from on-premises SQL Server to Azure</span></span>](tutorial-hybrid-copy-powershell.md)
