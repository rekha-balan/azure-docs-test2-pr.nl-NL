---
title: Add the Google Drive connector in logic apps | Microsoft Docs
description: Overview of the Google Drive connector with REST API parameters
services: ''
suite: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: b2bcebc5-02d2-435b-b0da-ef53bc51c4b6
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 8b4f1d0737b217b5474274c9db6f6405d7e77b60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564745"
---
# <a name="get-started-with-the-google-drive-connector"></a>Get started with the Google Drive connector
Connect to Google Drive to create files, get rows, and more. With Google Drive, you can: 

* Build your business flow based on the data you get from your search. 
* Use actions to search images, search the news, and more. These actions get a response, and then make the output available for other actions. For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.

To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
Google Drive includes the following actions. There are no triggers. 

| Triggers | Actions |
| --- | --- |
| None |<ul><li>Create file</li><li>Insert row</li><li>Copy file</li><li>Delete file</li><li>Delete row</li><li>Extract archive to folder</li><li>Get file content using id</li><li>Get file content using path</li><li>Get file metadata using id</li><li>Get file metadata using path</li><li>Get row</li><li>Update file</li><li>Update row</li></ul> |

All connectors support data in JSON and XML formats.

## <a name="create-the-connection-to-google-drive"></a>Create the connection to Google Drive
When you add this connector to your logic apps, you must authorize logic apps to connect to your Google Drive.

> [!INCLUDE [Steps to create a connection to googledrive](../../includes/connectors-create-api-googledrive.md)]
> 
> 

After you create the connection, you enter the Google Drive properties, like the folder path or file name. The **REST API reference** in this topic describes these properties.

> [!TIP]
> You can use this same Google Drive connection in other logic apps.
> 
> 

## <a name="swagger-rest-api-reference"></a>Swagger REST API reference
Applies to version: 1.0.

### <a name="create-file"></a>Create file
Uploads a file to Google Drive.  
```POST: /datasets/default/files```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| folderPath |string |yes |query |none |Folder path to upload the file to Google Drive |
| name |string |yes |query |none |Name of the file to create in Google Drive |
| body |string(binary) |yes |body |none |Content of the file to upload to Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="insert-row"></a>Insert row
Inserts a row into a Google Sheet.  
```POST: /datasets/{dataset}/tables/{table}/items```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |Unique identifier of the Google Sheet file |
| table |string |yes |path |none |Unique identifier of the worksheet |
| item |ItemInternalId: string |yes |body |none |Row to insert into the specified sheet |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="copy-file"></a>Copy file
Copies a file on Google Drive.  
```POST: /datasets/default/copyFile```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| source |string |yes |query |none |Url to source file |
| destination |string |yes |query |none |Destination file path in Google Drive, including target filename |
| overwrite |boolean |no |query |none |Overwrites the destination file if set to 'true' |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="delete-file"></a>Delete file
Deletes a file from Google Drive.  
```DELETE: /datasets/default/files/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |yes |path |none |Unique identifier of the file to delete from Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="delete-row"></a>Delete Row
Deletes a row from a Google Sheet.  
```DELETE: /datasets/{dataset}/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |Unique identifier of the Google Sheet file |
| table |string |yes |path |none |Unique identifier of the worksheet |
| id |string |yes |path |none |Unique identifier of the row to delete |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="extract-archive-to-folder"></a>Extract archive to folder
Extracts an archive file into a folder in Google Drive (example: .zip).  
```POST: /datasets/default/extractFolderV2```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| source |string |yes |query |none |Path to the archive file |
| destination |string |yes |query |none |Path in Google Drive to extract the archive contents |
| overwrite |boolean |no |query |none |Overwrites the destination files if set to 'true' |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-content-using-id"></a>Get file content using id
Retrieves file content from Google Drive using id.  
```GET: /datasets/default/files/{id}/content```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |yes |path |none |Unique identifier of the file to retrieve in Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-content-using-path"></a>Get file content using path
Retrieves file content from Google Drive using path.  
```GET: /datasets/default/GetFileContentByPath```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| path |string |yes |query |none |Path of the file in Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-metadata-using-id"></a>Get file metadata using id
Retrieves file metadata from Google Drive using id.  
```GET: /datasets/default/files/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |yes |path |none |Unique identifier of the file in Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-file-metadata-using-path"></a>Get file metadata using path
Retrieves file metadata from Google Drive using path.  
```GET: /datasets/default/GetFileByPath```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| path |string |yes |query |none |Path of the file in Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="get-row"></a>Get row
Retrieves a single row from a Google Sheet.  
```GET: /datasets/{dataset}/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |Unique identifier of the Google Sheet file |
| table |string |yes |path |none |Unique identifier of the worksheet |
| id |string |yes |path |none |Unique identifier of row to retrieve |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="update-file"></a>Update file
Updates a file in Google Drive.  
```PUT: /datasets/default/files/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| id |string |yes |path |none |Unique identifier of the file to update in Google Drive |
| body |string(binary) |yes |body |none |Content of the file to upload to Google Drive |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="update-row"></a>Update row
Updates a row in a Google Sheet.  
```PATCH: /datasets/{dataset}/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |Unique identifier of the Google Sheet file |
| table |string |yes |path |none |Unique identifier of the worksheet |
| id |string |yes |path |none |Unique identifier of the row to update |
| item |ItemInternalId: string |yes |body |none |Row with updated values |

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

#### <a name="tablemetadata"></a>TableMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| name |string |no |
| title |string |no |
| x-ms-permission |string |no |
| schema |not defined |no |

#### <a name="tableslist"></a>TablesList
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |no |

#### <a name="table"></a>Table
| Property Name | Data Type | Required |
| --- | --- | --- |
| Name |string |no |
| DisplayName |string |no |

#### <a name="item"></a>Item
| Property Name | Data Type | Required |
| --- | --- | --- |
| ItemInternalId |string |no |

#### <a name="itemslist"></a>ItemsList
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |no |

## <a name="next-steps"></a>Next steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

Go back to the [APIs list](apis-list.md).

<!--References-->
[5]: https://console.developers.google.com/
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/google-developers-console.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/use-google-apis.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/googledrive-api-overview.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/enable-googledrive-api.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/googledrive-api-credentials-add.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/configure-consent-screen.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-googledrive/create-client-id.png







