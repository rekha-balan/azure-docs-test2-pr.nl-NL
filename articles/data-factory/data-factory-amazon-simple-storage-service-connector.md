---
title: Move data from Amazon Simple Storage Service by using Data Factory | Microsoft Docs
description: Learn about how to move data from Amazon Simple Storage Service (S3) by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: jingwang
ms.openlocfilehash: d153bd715640a637c022c05fb86c45e1322dea14
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563274"
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Move data from Amazon Simple Storage Service by using Azure Data Factory
This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3). It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.

You can copy data from Amazon S3 to any supported sink data store. For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.

## <a name="required-permissions"></a>Required permissions
To copy data from Amazon S3, make sure you have been granted the following permissions:

* `s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.
* `s3:ListBucket` for Amazon S3 Bucket Operations. If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.

For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Getting started
You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.

The easiest way to create a pipeline is to use the **Copy Wizard**. For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).

You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**. For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:

1. Create **linked services** to link input and output data stores to your data factory.
2. Create **datasets** to represent input and output data for the copy operation.
3. Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.

When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you. When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format. For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.

> [!NOTE]
> For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.

## <a name="linked-service-properties"></a>Linked service properties
A linked service links a data store to a data factory. You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory. The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.

| Property | Description | Allowed values | Required |
| --- | --- | --- | --- |
| accessKeyID |ID of the secret access key. |string |Yes |
| secretAccessKey |The secret access key itself. |Encrypted secret string |Yes |

Here is an example:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Dataset properties
To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**. Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service. For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md). 

Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table). The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store. The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:

| Property | Description | Allowed values | Required |
| --- | --- | --- | --- |
| bucketName |The S3 bucket name. |String |Yes |
| key |The S3 object key. |String |No |
| prefix |Prefix for the S3 object key. Objects whose keys start with this prefix are selected. Applies only when key is empty. |String |No |
| version |The version of the S3 object, if S3 versioning is enabled. |String |No |
| format | The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Set the **type** property under format to one of these values. For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections. <br><br> If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions. |No | |
| compression | Specify the type and level of compression for the data. The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**. The supported levels are: **Optimal** and **Fastest**. For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No | |


> [!NOTE]
> **bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.

### <a name="sample-dataset-with-prefix"></a>Sample dataset with prefix

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Sample dataset (with version)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Dynamic paths for S3
The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

You can do the same for the **prefix** property of an Amazon S3 dataset. For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Copy activity properties
For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md). Properties such as name, description, input and output tables, and policies are available for all types of activities. Properties available in the **typeProperties** section of the activity vary with each activity type. For the copy activity, properties vary depending on the types of sources and sinks. When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:

| Property | Description | Allowed values | Required |
| --- | --- | --- | --- |
| recursive |Specifies whether to recursively list S3 objects under the directory. |true/false |No |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a>JSON example: Copy data from Amazon S3 to Azure Blob storage
This sample shows how to copy data from Amazon S3 to an Azure Blob storage. However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.

The sample provides JSON definitions for the following Data Factory entities. You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* A linked service of type [AwsAccessKey](#linked-service-properties).
* A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).
* An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

The sample copies data from Amazon S3 to an Azure blob every hour. The JSON properties used in these samples are described in sections following the samples.

### <a name="amazon-s3-linked-service"></a>Amazon S3 linked service

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure Storage linked service

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

### <a name="amazon-s3-input-dataset"></a>Amazon S3 input dataset

Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory. Set this property to true on an input dataset that is not produced by an activity in the pipeline.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Azure Blob output dataset

Data is written to a new blob every hour (frequency: hour, interval: 1). The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed. The folder path uses the year, month, day, and hours parts of the start time.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Copy activity in a pipeline with an Amazon S3 source and a blob sink

The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour. In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a>Next steps
See the following articles:

* To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).

* For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
