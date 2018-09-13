---
title: Add the Box connector to your Logic Apps | Microsoft Docs
description: Overview of the Box connector with REST API parameters
services: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: 949579cf-a81c-4790-9ef5-fe39b4fbd0c5
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: bb6bef230f4ba4f7019fd2f120c2115d97649b81
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549930"
---
# <a name="get-started-with-the-box-connector"></a>Get started with the Box connector
Connect to Box and create files, delete files, and more. 

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version.
> 
> 

With Box, you can:

* Build your business flow based on the data you get from Box. 
* Use triggers when a file is created or updated.
* Use actions that copy a file, delete a file, and more. These actions get a response, and then make the output available for other actions. For example, when a file is changed on Box, you can take that file and email it using Office 365.

To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
Box includes the following trigger and actions.

| Triggers | Actions |
| --- | --- |
| <ul><li>When a file is created</li><li>When a file is modified</li></ul> |<ul><li>Create file</li><li>When a file is created</li><li>Copy file</li><li>Delete file</li><li>Extract archive to folder</li><li>Get file content using id</li><li>Get file content using path</li><li>Get file metadata using id</li><li>Get file metadata using path</li><li>Update file</li><li>When a file is modified</li></ul> |

All connectors support data in JSON and XML formats.

## <a name="create-a-connection-to-box"></a>Create a connection to Box
When you add this connector to your logic apps, you must authorize logic apps to connect to your Box.

> [!INCLUDE [Steps to create a connection to box](../../includes/connectors-create-api-box.md)]
> 
> 

After you create the connection, you enter the Box properties. The **REST API reference** in this topic describes these properties.

> [!TIP]
> You can use this same Box connection in other logic apps.
> 
> 

## <a name="swagger-rest-api-reference"></a>Swagger REST API reference
Applies to version: 1.0.

### <a name="create-file"></a>Create file
Uploads a file to Box.  
```POST: /datasets/default/files```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| folderPath |string |Yes |query |None |Folder path to upload the file to Box |
| name |string |Yes |query |None |Name of the file to create in Box |
| body |string(binary) |Yes |body |None |Content of the file to upload to Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="when-a-file-is-created"></a>When a file is created
Triggers a flow when a new file is created in a Box folder.  
```GET: /datasets/default/triggers/onnewfile```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| folderId |string |Yes |query |None |Unique identifier of the folder in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="copy-file"></a>Copy file
Copies a file to Box.  
```POST: /datasets/default/copyFile```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| source |string |Yes |query |None |Url to source file |
| destination |string |Yes |query |None |Destination file path in Box, including target filename |
| overwrite |boolean |No |query |None |Overwrites the destination file if set to 'true' |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="delete-file"></a>Delete file
Deletes a file from Box.  
```DELETE: /datasets/default/files/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |Yes |path |None |Unique identifier of the file to delete from Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="extract-archive-to-folder"></a>Extract archive to folder
Extracts an archive file into a folder in Box (example: .zip).  
```POST: /datasets/default/extractFolderV2```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| source |string |Yes |query | |Path to the archive file |
| destination |string |Yes |query | |Path in Box to extract the archive contents |
| overwrite |boolean |No |query | |Overwrites the destination files if set to 'true' |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-content-using-id"></a>Get file content using id
Retrieves file contents from Box using id.  
```GET: /datasets/default/files/{id}/content```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |Yes |path |None |Unique identifier of the file in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-content-using-path"></a>Get file content using path
Retrieves file contents from Box using path.  
```GET: /datasets/default/GetFileContentByPath```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| path |string |Yes |query |None |Unique path to the file in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-metadata-using-id"></a>Get file metadata using id
Retrieves file metadata from Box using file id.  
```GET: /datasets/default/files/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |Yes |path |None |Unique identifier of the file in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-metadata-using-path"></a>Get file metadata using path
Retrieves file metadata from Box using path.  
```GET: /datasets/default/GetFileByPath```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| path |string |Yes |query |None |Unique path to the file in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="update-file"></a>Update file
Updates a file in Box.  
```PUT: /datasets/default/files/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |Yes |path |None |Unique identifier of the file to update in Box |
| body |string(binary) |Yes |body |None |Content of the file to update in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="when-a-file-is-modified"></a>When a file is modified
Triggers a flow when a file is modified in a Box folder.  
```GET: /datasets/default/triggers/onupdatedfile```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| folderId |string |Yes |query |None |Unique identifier of the folder in Box |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
#### <a name="datasetsmetadata"></a>DataSetsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| tabular |not defined |no |
| blob |not defined |no |

#### <a name="tabulardatasetsmetadata"></a>TabularDataSetsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| source |string |no |
| displayName |string |no |
| urlEncoding |string |no |
| tableDisplayName |string |no |
| tablePluralName |string |no |

#### <a name="blobdatasetsmetadata"></a>BlobDataSetsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| source |string |no |
| displayName |string |no |
| urlEncoding |string |no |

#### <a name="blobmetadata"></a>BlobMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| Id |string |no |
| Name |string |no |
| DisplayName |string |no |
| Path |string |no |
| LastModified |string |no |
| Size |integer |no |
| MediaType |string |no |
| IsFolder |boolean |no |
| ETag |string |no |
| FileLocator |string |no |

## <a name="next-steps"></a>Next steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

