---
title: Copy data from MariaDB using Azure Data Factory  | Microsoft Docs
description: Learn how to copy data from MariaDB to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 93d4886d5c266555a5c61a121622943f218caa48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965929"
---
# <a name="copy-data-from-mariadb-using-azure-data-factory"></a>Copy data from MariaDB using Azure Data Factory 

This article outlines how to use the Copy Activity in Azure Data Factory to copy data from MariaDB. It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.

## <a name="supported-capabilities"></a>Supported capabilities

You can copy data from MariaDB to any supported sink data store. For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.

Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.

This connector currently supports MariaDB of version less than 10.2.

## <a name="getting-started"></a>Getting started

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

The following sections provide details about properties that are used to define Data Factory entities specific to MariaDB connector.

## <a name="linked-service-properties"></a>Linked service properties

The following properties are supported for MariaDB linked service:

| Property | Description | Required |
|:--- |:--- |:--- |
| type | The type property must be set to: **MariaDB** | Yes |
| connectionString | An ODBC connection string to connect to MariaDB. Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md). | Yes |
| connectVia | The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store. You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible). If not specified, it uses the default Azure Integration Runtime. |No |

**Example:**

```json
{
    "name": "MariaDBLinkedService",
    "properties": {
        "type": "MariaDB",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<host>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
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

For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article. This section provides a list of properties supported by MariaDB dataset.

To copy data from MariaDB, set the type property of the dataset to **MariaDBTable**. There is no additional type-specific property in this type of dataset.

**Example**

```json
{
    "name": "MariaDBDataset",
    "properties": {
        "type": "MariaDBTable",
        "linkedServiceName": {
            "referenceName": "<MariaDB linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Copy activity properties

For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article. This section provides a list of properties supported by MariaDB source.

### <a name="mariadbsource-as-source"></a>MariaDBSource as source

To copy data from MariaDB, set the source type in the copy activity to **MariaDBSource**. The following properties are supported in the copy activity **source** section:

| Property | Description | Required |
|:--- |:--- |:--- |
| type | The type property of the copy activity source must be set to: **MariaDBSource** | Yes |
| query | Use the custom SQL query to read data. For example: `"SELECT * FROM MyTable"`. | Yes |

**Example:**

```json
"activities":[
    {
        "name": "CopyFromMariaDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<MariaDB input dataset name>",
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
                "type": "MariaDBSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>Next steps
For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).
