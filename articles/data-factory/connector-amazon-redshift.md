---
title: Copy data from Amazon Redshift using Azure Data Factory | Microsoft Docs
description: Learn about how to copy data from Amazon Redshift to supported sink data stores by using Azure Data Factory.
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
ms.date: 02/07/2018
ms.author: jingwang
ms.openlocfilehash: 6d36733b63645fd86580ccdc5af756739f77338c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869837"
---
# <a name="copy-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="79def-103">Copy data from Amazon Redshift using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="79def-103">Copy data from Amazon Redshift using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-amazon-redshift-connector.md)
> * [Current version](connector-amazon-redshift.md)


<span data-ttu-id="79def-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="79def-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an Amazon Redshift.</span></span> <span data-ttu-id="79def-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="79def-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="79def-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="79def-108">Supported capabilities</span></span>

<span data-ttu-id="79def-109">You can copy data from Amazon Redshift to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="79def-109">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="79def-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="79def-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="79def-111">Specifically, this Amazon Redshift connector supports retrieving data from Redshift using query or built-in Redshift UNLOAD support.</span><span class="sxs-lookup"><span data-stu-id="79def-111">Specifically, this Amazon Redshift connector supports retrieving data from Redshift using query or built-in Redshift UNLOAD support.</span></span>

> [!TIP]
> To achieve the best performance when copying large amounts of data from Redshift, consider using the built-in Redshift UNLOAD through Amazon S3. See [Use UNLOAD to copy data from Amazon Redshift](#use-unload-to-copy-data-from-amazon-redshift) section for details.

## <a name="prerequisites"></a><span data-ttu-id="79def-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="79def-114">Prerequisites</span></span>

* <span data-ttu-id="79def-115">If you are copying data to an on-premises data store using [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md), grant Integration Runtime (use IP address of the machine) the access to Amazon Redshift cluster.</span><span class="sxs-lookup"><span data-stu-id="79def-115">If you are copying data to an on-premises data store using [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md), grant Integration Runtime (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="79def-116">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span><span class="sxs-lookup"><span data-stu-id="79def-116">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="79def-117">If you are copying data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span><span class="sxs-lookup"><span data-stu-id="79def-117">If you are copying data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="79def-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="79def-118">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="79def-119">The following sections provide details about properties that are used to define Data Factory entities specific to Amazon Redshift connector.</span><span class="sxs-lookup"><span data-stu-id="79def-119">The following sections provide details about properties that are used to define Data Factory entities specific to Amazon Redshift connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="79def-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="79def-120">Linked service properties</span></span>

<span data-ttu-id="79def-121">The following properties are supported for Amazon Redshift linked service:</span><span class="sxs-lookup"><span data-stu-id="79def-121">The following properties are supported for Amazon Redshift linked service:</span></span>

| <span data-ttu-id="79def-122">Property</span><span class="sxs-lookup"><span data-stu-id="79def-122">Property</span></span> | <span data-ttu-id="79def-123">Description</span><span class="sxs-lookup"><span data-stu-id="79def-123">Description</span></span> | <span data-ttu-id="79def-124">Required</span><span class="sxs-lookup"><span data-stu-id="79def-124">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79def-125">type</span><span class="sxs-lookup"><span data-stu-id="79def-125">type</span></span> | <span data-ttu-id="79def-126">The type property must be set to: **AmazonRedshift**</span><span class="sxs-lookup"><span data-stu-id="79def-126">The type property must be set to: **AmazonRedshift**</span></span> | <span data-ttu-id="79def-127">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-127">Yes</span></span> |
| <span data-ttu-id="79def-128">server</span><span class="sxs-lookup"><span data-stu-id="79def-128">server</span></span> |<span data-ttu-id="79def-129">IP address or host name of the Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="79def-129">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="79def-130">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-130">Yes</span></span> |
| <span data-ttu-id="79def-131">port</span><span class="sxs-lookup"><span data-stu-id="79def-131">port</span></span> |<span data-ttu-id="79def-132">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="79def-132">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="79def-133">No, default is 5439</span><span class="sxs-lookup"><span data-stu-id="79def-133">No, default is 5439</span></span> |
| <span data-ttu-id="79def-134">database</span><span class="sxs-lookup"><span data-stu-id="79def-134">database</span></span> |<span data-ttu-id="79def-135">Name of the Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="79def-135">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="79def-136">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-136">Yes</span></span> |
| <span data-ttu-id="79def-137">username</span><span class="sxs-lookup"><span data-stu-id="79def-137">username</span></span> |<span data-ttu-id="79def-138">Name of user who has access to the database.</span><span class="sxs-lookup"><span data-stu-id="79def-138">Name of user who has access to the database.</span></span> |<span data-ttu-id="79def-139">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-139">Yes</span></span> |
| <span data-ttu-id="79def-140">password</span><span class="sxs-lookup"><span data-stu-id="79def-140">password</span></span> |<span data-ttu-id="79def-141">Password for the user account.</span><span class="sxs-lookup"><span data-stu-id="79def-141">Password for the user account.</span></span> <span data-ttu-id="79def-142">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="79def-142">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="79def-143">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-143">Yes</span></span> |
| <span data-ttu-id="79def-144">connectVia</span><span class="sxs-lookup"><span data-stu-id="79def-144">connectVia</span></span> | <span data-ttu-id="79def-145">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="79def-145">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="79def-146">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="79def-146">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="79def-147">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="79def-147">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="79def-148">No</span><span class="sxs-lookup"><span data-stu-id="79def-148">No</span></span> |

<span data-ttu-id="79def-149">**Example:**</span><span class="sxs-lookup"><span data-stu-id="79def-149">**Example:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "<server name>",
            "database": "<database name>",
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="79def-150">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="79def-150">Dataset properties</span></span>

<span data-ttu-id="79def-151">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="79def-151">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="79def-152">This section provides a list of properties supported by Amazon Redshift dataset.</span><span class="sxs-lookup"><span data-stu-id="79def-152">This section provides a list of properties supported by Amazon Redshift dataset.</span></span>

<span data-ttu-id="79def-153">To copy data from Amazon Redshift, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="79def-153">To copy data from Amazon Redshift, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="79def-154">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="79def-154">The following properties are supported:</span></span>

| <span data-ttu-id="79def-155">Property</span><span class="sxs-lookup"><span data-stu-id="79def-155">Property</span></span> | <span data-ttu-id="79def-156">Description</span><span class="sxs-lookup"><span data-stu-id="79def-156">Description</span></span> | <span data-ttu-id="79def-157">Required</span><span class="sxs-lookup"><span data-stu-id="79def-157">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79def-158">type</span><span class="sxs-lookup"><span data-stu-id="79def-158">type</span></span> | <span data-ttu-id="79def-159">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="79def-159">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="79def-160">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-160">Yes</span></span> |
| <span data-ttu-id="79def-161">tableName</span><span class="sxs-lookup"><span data-stu-id="79def-161">tableName</span></span> | <span data-ttu-id="79def-162">Name of the table in the Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="79def-162">Name of the table in the Amazon Redshift.</span></span> | <span data-ttu-id="79def-163">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="79def-163">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="79def-164">**Example**</span><span class="sxs-lookup"><span data-stu-id="79def-164">**Example**</span></span>

```json
{
    "name": "AmazonRedshiftDataset",
    "properties":
    {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<Amazon Redshift linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="79def-165">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="79def-165">Copy activity properties</span></span>

<span data-ttu-id="79def-166">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="79def-166">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="79def-167">This section provides a list of properties supported by Amazon Redshift source.</span><span class="sxs-lookup"><span data-stu-id="79def-167">This section provides a list of properties supported by Amazon Redshift source.</span></span>

### <a name="amazon-redshift-as-source"></a><span data-ttu-id="79def-168">Amazon Redshift as source</span><span class="sxs-lookup"><span data-stu-id="79def-168">Amazon Redshift as source</span></span>

<span data-ttu-id="79def-169">To copy data from Amazon Redshift, set the source type in the copy activity to **AmazonRedshiftSource**.</span><span class="sxs-lookup"><span data-stu-id="79def-169">To copy data from Amazon Redshift, set the source type in the copy activity to **AmazonRedshiftSource**.</span></span> <span data-ttu-id="79def-170">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="79def-170">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="79def-171">Property</span><span class="sxs-lookup"><span data-stu-id="79def-171">Property</span></span> | <span data-ttu-id="79def-172">Description</span><span class="sxs-lookup"><span data-stu-id="79def-172">Description</span></span> | <span data-ttu-id="79def-173">Required</span><span class="sxs-lookup"><span data-stu-id="79def-173">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79def-174">type</span><span class="sxs-lookup"><span data-stu-id="79def-174">type</span></span> | <span data-ttu-id="79def-175">The type property of the copy activity source must be set to: **AmazonRedshiftSource**</span><span class="sxs-lookup"><span data-stu-id="79def-175">The type property of the copy activity source must be set to: **AmazonRedshiftSource**</span></span> | <span data-ttu-id="79def-176">Yes</span><span class="sxs-lookup"><span data-stu-id="79def-176">Yes</span></span> |
| <span data-ttu-id="79def-177">query</span><span class="sxs-lookup"><span data-stu-id="79def-177">query</span></span> |<span data-ttu-id="79def-178">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="79def-178">Use the custom query to read data.</span></span> |<span data-ttu-id="79def-179">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="79def-179">SQL query string.</span></span> <span data-ttu-id="79def-180">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="79def-180">For example: select \* from MyTable.</span></span> |<span data-ttu-id="79def-181">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="79def-181">No (if "tableName" in dataset is specified)</span></span> |
| <span data-ttu-id="79def-182">redshiftUnloadSettings</span><span class="sxs-lookup"><span data-stu-id="79def-182">redshiftUnloadSettings</span></span> | <span data-ttu-id="79def-183">Property group when using Amazon Redshift UNLOAD.</span><span class="sxs-lookup"><span data-stu-id="79def-183">Property group when using Amazon Redshift UNLOAD.</span></span> | <span data-ttu-id="79def-184">No</span><span class="sxs-lookup"><span data-stu-id="79def-184">No</span></span> |
| <span data-ttu-id="79def-185">s3LinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="79def-185">s3LinkedServiceName</span></span> | <span data-ttu-id="79def-186">Refers to an Amazon S3 to-be-used as an interim store by specifying a linked service name of "AmazonS3" type.</span><span class="sxs-lookup"><span data-stu-id="79def-186">Refers to an Amazon S3 to-be-used as an interim store by specifying a linked service name of "AmazonS3" type.</span></span> | <span data-ttu-id="79def-187">Yes if using UNLOAD</span><span class="sxs-lookup"><span data-stu-id="79def-187">Yes if using UNLOAD</span></span> |
| <span data-ttu-id="79def-188">bucketName</span><span class="sxs-lookup"><span data-stu-id="79def-188">bucketName</span></span> | <span data-ttu-id="79def-189">Indicate the S3 bucket to store the interim data.</span><span class="sxs-lookup"><span data-stu-id="79def-189">Indicate the S3 bucket to store the interim data.</span></span> <span data-ttu-id="79def-190">If not provided, Data Factory service generates it automatically.</span><span class="sxs-lookup"><span data-stu-id="79def-190">If not provided, Data Factory service generates it automatically.</span></span>  | <span data-ttu-id="79def-191">Yes if using UNLOAD</span><span class="sxs-lookup"><span data-stu-id="79def-191">Yes if using UNLOAD</span></span> |

<span data-ttu-id="79def-192">**Example: Amazon Redshift source in copy activity using UNLOAD**</span><span class="sxs-lookup"><span data-stu-id="79def-192">**Example: Amazon Redshift source in copy activity using UNLOAD**</span></span>

```json
"source": {
    "type": "AmazonRedshiftSource",
    "query": "<SQL query>",
    "redshiftUnloadSettings": {
        "s3LinkedServiceName": {
            "referenceName": "<Amazon S3 linked service>",
            "type": "LinkedServiceReference"
        },
        "bucketName": "bucketForUnload"
    }
}
```

<span data-ttu-id="79def-193">Learn more on how to use UNLOAD to copy data from Amazon Redshift efficiently from next section.</span><span class="sxs-lookup"><span data-stu-id="79def-193">Learn more on how to use UNLOAD to copy data from Amazon Redshift efficiently from next section.</span></span>

## <a name="use-unload-to-copy-data-from-amazon-redshift"></a><span data-ttu-id="79def-194">Use UNLOAD to copy data from Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="79def-194">Use UNLOAD to copy data from Amazon Redshift</span></span>

<span data-ttu-id="79def-195">[UNLOAD](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html) is a mechanism provided by Amazon Redshift, which can unload the results of a query to one or more files on Amazon Simple Storage Service (Amazon S3).</span><span class="sxs-lookup"><span data-stu-id="79def-195">[UNLOAD](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html) is a mechanism provided by Amazon Redshift, which can unload the results of a query to one or more files on Amazon Simple Storage Service (Amazon S3).</span></span> <span data-ttu-id="79def-196">It is the way recommended by Amazon for copying large data set from Redshift.</span><span class="sxs-lookup"><span data-stu-id="79def-196">It is the way recommended by Amazon for copying large data set from Redshift.</span></span>

<span data-ttu-id="79def-197">**Example: copy data from Amazon Redshift to Azure SQL Data Warehouse using UNLOAD, staged copy and PolyBase**</span><span class="sxs-lookup"><span data-stu-id="79def-197">**Example: copy data from Amazon Redshift to Azure SQL Data Warehouse using UNLOAD, staged copy and PolyBase**</span></span>

<span data-ttu-id="79def-198">For this sample use case, copy activity unloads data from Amazon Redshift to Amazon S3 as configured in "redshiftUnloadSettings", and then copy data from Amazon S3 to Azure Blob as specified in "stagingSettings", lastly use PolyBase to load data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="79def-198">For this sample use case, copy activity unloads data from Amazon Redshift to Amazon S3 as configured in "redshiftUnloadSettings", and then copy data from Amazon S3 to Azure Blob as specified in "stagingSettings", lastly use PolyBase to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="79def-199">All the interim format is handled by copy activity properly.</span><span class="sxs-lookup"><span data-stu-id="79def-199">All the interim format is handled by copy activity properly.</span></span>

![Redshift to SQL DW copy workflow](media\copy-data-from-amazon-redshift\redshift-to-sql-dw-copy-workflow.png)

```json
"activities":[
    {
        "name": "CopyFromAmazonRedshiftToSQLDW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "AmazonRedshiftDataset",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "AzureSQLDWDataset",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "AmazonRedshiftSource",
                "query": "select * from MyTable",
                "redshiftUnloadSettings": {
                    "s3LinkedServiceName": {
                        "referenceName": "AmazonS3LinkedService",
                        "type": "LinkedServiceReference"
                    },
                    "bucketName": "bucketForUnload"
                }
            },
            "sink": {
                "type": "SqlDWSink",
                "allowPolyBase": true
            },
            "enableStaging": true,
            "stagingSettings": {
                "linkedServiceName": "AzureStorageLinkedService",
                "path": "adfstagingcopydata"
            },
            "dataIntegrationUnits": 32
        }
    }
]
```

## <a name="data-type-mapping-for-amazon-redshift"></a><span data-ttu-id="79def-201">Data type mapping for Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="79def-201">Data type mapping for Amazon Redshift</span></span>

<span data-ttu-id="79def-202">When copying data from Amazon Redshift, the following mappings are used from Amazon Redshift data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="79def-202">When copying data from Amazon Redshift, the following mappings are used from Amazon Redshift data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="79def-203">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="79def-203">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="79def-204">Amazon Redshift data type</span><span class="sxs-lookup"><span data-stu-id="79def-204">Amazon Redshift data type</span></span> | <span data-ttu-id="79def-205">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="79def-205">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="79def-206">BIGINT</span><span class="sxs-lookup"><span data-stu-id="79def-206">BIGINT</span></span> |<span data-ttu-id="79def-207">Int64</span><span class="sxs-lookup"><span data-stu-id="79def-207">Int64</span></span> |
| <span data-ttu-id="79def-208">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="79def-208">BOOLEAN</span></span> |<span data-ttu-id="79def-209">String</span><span class="sxs-lookup"><span data-stu-id="79def-209">String</span></span> |
| <span data-ttu-id="79def-210">CHAR</span><span class="sxs-lookup"><span data-stu-id="79def-210">CHAR</span></span> |<span data-ttu-id="79def-211">String</span><span class="sxs-lookup"><span data-stu-id="79def-211">String</span></span> |
| <span data-ttu-id="79def-212">DATE</span><span class="sxs-lookup"><span data-stu-id="79def-212">DATE</span></span> |<span data-ttu-id="79def-213">DateTime</span><span class="sxs-lookup"><span data-stu-id="79def-213">DateTime</span></span> |
| <span data-ttu-id="79def-214">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="79def-214">DECIMAL</span></span> |<span data-ttu-id="79def-215">Decimal</span><span class="sxs-lookup"><span data-stu-id="79def-215">Decimal</span></span> |
| <span data-ttu-id="79def-216">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="79def-216">DOUBLE PRECISION</span></span> |<span data-ttu-id="79def-217">Double</span><span class="sxs-lookup"><span data-stu-id="79def-217">Double</span></span> |
| <span data-ttu-id="79def-218">INTEGER</span><span class="sxs-lookup"><span data-stu-id="79def-218">INTEGER</span></span> |<span data-ttu-id="79def-219">Int32</span><span class="sxs-lookup"><span data-stu-id="79def-219">Int32</span></span> |
| <span data-ttu-id="79def-220">REAL</span><span class="sxs-lookup"><span data-stu-id="79def-220">REAL</span></span> |<span data-ttu-id="79def-221">Single</span><span class="sxs-lookup"><span data-stu-id="79def-221">Single</span></span> |
| <span data-ttu-id="79def-222">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="79def-222">SMALLINT</span></span> |<span data-ttu-id="79def-223">Int16</span><span class="sxs-lookup"><span data-stu-id="79def-223">Int16</span></span> |
| <span data-ttu-id="79def-224">TEXT</span><span class="sxs-lookup"><span data-stu-id="79def-224">TEXT</span></span> |<span data-ttu-id="79def-225">String</span><span class="sxs-lookup"><span data-stu-id="79def-225">String</span></span> |
| <span data-ttu-id="79def-226">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="79def-226">TIMESTAMP</span></span> |<span data-ttu-id="79def-227">DateTime</span><span class="sxs-lookup"><span data-stu-id="79def-227">DateTime</span></span> |
| <span data-ttu-id="79def-228">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="79def-228">VARCHAR</span></span> |<span data-ttu-id="79def-229">String</span><span class="sxs-lookup"><span data-stu-id="79def-229">String</span></span> |

## <a name="next-steps"></a><span data-ttu-id="79def-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="79def-230">Next steps</span></span>
<span data-ttu-id="79def-231">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="79def-231">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
