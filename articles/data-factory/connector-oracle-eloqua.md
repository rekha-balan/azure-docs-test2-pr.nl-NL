---
title: Copy data from Oracle Eloqua using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Oracle Eloqua to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/22/2018
ms.author: jingwang
ms.openlocfilehash: 821e345933ba52ed2c71251bab3ba159e5412568
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856983"
---
# <a name="copy-data-from-oracle-eloqua-using-azure-data-factory"></a>Copy data from Oracle Eloqua using Azure Data Factory

This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Eloqua. It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.

> [!IMPORTANT]
> This connector is currently in preview. You can try it out and provide feedback. If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).

## <a name="supported-capabilities"></a>Supported capabilities

You can copy data from Oracle Eloqua to any supported sink data store. For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.

Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.

## <a name="getting-started"></a>Getting started

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Eloqua connector.

## <a name="linked-service-properties"></a>Linked service properties

The following properties are supported for Oracle Eloqua linked service:

| Property | Description | Required |
|:--- |:--- |:--- |
| type | The type property must be set to: **Eloqua** | Yes |
| endpoint | The endpoint of the Eloqua server. Eloqua supports multiple data centers, to determine your endpoint, login to https://login.eloqua.com with your credential, then copy the **base URL** portion from the redirected URL with the pattern of `xxx.xxx.eloqua.com`. | Yes |
| username | The site name and user name of your Eloqua account in the form: `SiteName\Username` e.g. `Eloqua\Alice`.  | Yes |
| password | The password corresponding to the user name. Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md). | Yes |
| useEncryptedEndpoints | Specifies whether the data source endpoints are encrypted using HTTPS. The default value is true.  | No |
| useHostVerification | Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL. The default value is true.  | No |
| usePeerVerification | Specifies whether to verify the identity of the server when connecting over SSL. The default value is true.  | No |

**Example:**

```json
{
    "name": "EloquaLinkedService",
    "properties": {
        "type": "Eloqua",
        "typeProperties": {
            "endpoint" : "<base URL e.g. xxx.xxx.eloqua.com>",
            "username" : "<site name>\\<user name e.g. Eloqua\\Alice>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a>Dataset properties

For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article. This section provides a list of properties supported by Oracle Eloqua dataset.

To copy data from Oracle Eloqua, set the type property of the dataset to **EloquaObject**. There is no additional type-specific property in this type of dataset.

**Example**

```json
{
    "name": "EloquaDataset",
    "properties": {
        "type": "EloquaObject",
        "linkedServiceName": {
            "referenceName": "<Eloqua linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Copy activity properties

For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article. This section provides a list of properties supported by Oracle Eloqua source.

### <a name="eloquasource-as-source"></a>EloquaSource as source

To copy data from Oracle Eloqua, set the source type in the copy activity to **EloquaSource**. The following properties are supported in the copy activity **source** section:

| Property | Description | Required |
|:--- |:--- |:--- |
| type | The type property of the copy activity source must be set to: **EloquaSource** | Yes |
| query | Use the custom SQL query to read data. For example: `"SELECT * FROM Accounts"`. | Yes |

**Example:**

```json
"activities":[
    {
        "name": "CopyFromEloqua",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Eloqua input dataset name>",
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
                "type": "EloquaSource",
                "query": "SELECT * FROM Accounts"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>Next steps
For a list of supported data stored by Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).
