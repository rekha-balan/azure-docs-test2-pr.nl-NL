---
title: Copy data from MongoDB using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Mongo DB to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/05/2018
ms.author: jingwang
ms.openlocfilehash: debb27f49c730df4a8bef42b1f1ef9ec50f1faf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867228"
---
# <a name="copy-data-from-mongodb-using-azure-data-factory"></a>Copy data from MongoDB using Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-on-premises-mongodb-connector.md)
> * [Current version](connector-mongodb.md)

This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a MongoDB database. It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.

## <a name="supported-capabilities"></a>Supported capabilities

You can copy data from MongoDB database to any supported sink data store. For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.

Specifically, this MongoDB connector supports:

- MongoDB **versions 2.4, 2.6, 3.0, 3.2, 3.4 and 3.6**.
- Copying data using **Basic** or **Anonymous** authentication.

## <a name="prerequisites"></a>Prerequisites

To copy data from a MongoDB database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime. See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article to learn details. The Integration Runtime provides a built-in MongoDB driver, therefore you don't need to manually install any driver when copying data from MongoDB.

## <a name="getting-started"></a>Getting started

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

The following sections provide details about properties that are used to define Data Factory entities specific to MongoDB connector.

## <a name="linked-service-properties"></a>Linked service properties

The following properties are supported for MongoDB linked service:

| Property | Description | Required |
|:--- |:--- |:--- |
| type |The type property must be set to: **MongoDb** |Yes |
| server |IP address or host name of the MongoDB server. |Yes |
| port |TCP port that the MongoDB server uses to listen for client connections. |No (default is 27017) |
| databaseName |Name of the MongoDB database that you want to access. |Yes |
| authenticationType | Type of authentication used to connect to the MongoDB database.<br/>Allowed values are: **Basic**, and **Anonymous**. |Yes |
| username |User account to access MongoDB. |Yes (if basic authentication is used). |
| password |Password for the user. Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md). |Yes (if basic authentication is used). |
| authSource |Name of the MongoDB database that you want to use to check your credentials for authentication. |No. For basic authentication, default is to use the admin account and the database specified using databaseName property. |
| enableSsl | Specifies whether the connections to the server are encrypted using SSL. The default value is false.  | No |
| allowSelfSignedServerCert | Specifies whether to allow self-signed certificates from the server. The default value is false.  | No |
| connectVia | The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store. You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible). If not specified, it uses the default Azure Integration Runtime. |No |

**Example:**

```json
{
    "name": "MongoDBLinkedService",
    "properties": {
        "type": "MongoDb",
        "typeProperties": {
            "server": "<server name>",
            "databaseName": "<database name>",
            "authenticationType": "Basic",
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

## <a name="dataset-properties"></a>Dataset properties

For a full list of sections and properties available for defining datasets, see the datasets article. This section provides a list of properties supported by MongoDB dataset.

To copy data from MongoDB, set the type property of the dataset to **MongoDbCollection**. The following properties are supported:

| Property | Description | Required |
|:--- |:--- |:--- |
| type | The type property of the dataset must be set to: **MongoDbCollection** | Yes |
| collectionName |Name of the collection in MongoDB database. |Yes |

**Example:**

```json
{
     "name":  "MongoDbDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": {
            "referenceName": "<MongoDB linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "collectionName": "<Collection name>"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Copy activity properties

For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article. This section provides a list of properties supported by MongoDB source.

### <a name="mongodb-as-source"></a>MongoDB as source

To copy data from MongoDB, set the source type in the copy activity to **MongoDbSource**. The following properties are supported in the copy activity **source** section:

| Property | Description | Required |
|:--- |:--- |:--- |
| type | The type property of the copy activity source must be set to: **MongoDbSource** | Yes |
| query |Use the custom SQL-92 query to read data. For example: select * from MyTable. |No (if "collectionName" in dataset is specified) |

**Example:**

```json
"activities":[
    {
        "name": "CopyFromMongoDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<MongoDB input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "MongoDbSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

> [!TIP]
> When specify the SQL query, pay attention to the DateTime format. For example: `SELECT * FROM Account WHERE LastModifiedDate >= '2018-06-01' AND LastModifiedDate < '2018-06-02'` or to use parameter `SELECT * FROM Account WHERE LastModifiedDate >= '@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}' AND LastModifiedDate < '@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'`

## <a name="schema-by-data-factory"></a>Schema by Data Factory

Azure Data Factory service infers schema from a MongoDB collection by using the **latest 100 documents** in the collection. If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.

## <a name="data-type-mapping-for-mongodb"></a>Data type mapping for MongoDB

When copying data from MongoDB, the following mappings are used from MongoDB data types to Azure Data Factory interim data types. See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.

| MongoDB data type | Data factory interim data type |
|:--- |:--- |
| Binary |Byte[] |
| Boolean |Boolean |
| Date |DateTime |
| NumberDouble |Double |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |String |
| String |String |
| UUID |Guid |
| Object |Renormalized into flatten columns with “_" as nested separator |

> [!NOTE]
> To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section.
>
> Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined.

## <a name="support-for-complex-types-using-virtual-tables"></a>Support for complex types using virtual tables

Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database. For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables. Specifically, if a table contains such columns, the driver generates the following virtual tables:

* A **base table**, which contains the same data as the real table except for the complex type columns. The base table uses the same name as the real table that it represents.
* A **virtual table** for each complex type column, which expands the nested data. The virtual tables are named using the name of the real table, a separator “_" and the name of the array or object.

Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data. You can access the content of MongoDB arrays by querying and joining the virtual tables.

### <a name="example"></a>Example

For example, ExampleTable here is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.

| _id | Customer Name | Invoices | Service Level | Ratings |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id:"123", item:"toaster", price:"456", discount:"0.2"}, {invoice_id:"124", item:"oven", price: "1235", discount: "0.2"}] |Silver |[5,6] |
| 2222 |XYZ |[{invoice_id:"135", item:"fridge", price: "12543", discount: "0.0"}] |Gold |[1,2] |

The driver would generate multiple virtual tables to represent this single table. The first virtual table is the base table named “ExampleTable", shown in the example. The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.

| _id | Customer Name | Service Level |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

The following tables show the virtual tables that represent the original arrays in the example. These tables contain the following:

* A reference back to the original primary key column corresponding to the row of the original array (via the _id column)
* An indication of the position of the data within the original array
* The expanded data for each element within the array

**Table “ExampleTable_Invoices":**

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | item | price | Discount |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |toaster |456 |0.2 |
| 1111 |1 |124 |oven |1235 |0.2 |
| 2222 |0 |135 |fridge |12543 |0.0 |

**Table “ExampleTable_Ratings":**

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |


## <a name="next-steps"></a>Next steps
For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).