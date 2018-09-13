---
title: Use the SharePoint Online Connector in your Logic Apps | Microsoft Docs
description: Get started using the the SharePoint Online Connector  in your Logic apps
services: ''
documentationcenter: ''
author: msftman
manager: anneta
editor: ''
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 3cd8d972ddb65effe1e6608009e8063bb1cdd17a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553458"
---
# <a name="get-started-with-the-sharepoint-online-connector"></a>Get started with the SharePoint Online Connector
The SharePoint Connector provides an way to work with Lists on SharePoint.

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version.
> 
> 

To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="lets-talk-about-triggers-and-actions"></a>Let's talk about triggers and actions
The SharePoint Connector  can be used as an action; it has trigger(s). All connectors support data in JSON and XML formats. 

The SharePoint Connector  has the following action(s) and/or trigger(s) available:

### <a name="sharepoint-actions"></a>SharePoint actions
You can take these action(s):

| Action | Description |
| --- | --- |
| GetFileMetadata |Used for getting a file metadata on Document Library |
| UpdateFile |Used for updating a file on Document Library |
| DeleteFile |Used for deleting a file on Document Library |
| GetFileMetadataByPath |Used for getting a file metadata on Document Library |
| GetFileContentByPath |Used for getting a file on Document Library |
| GetFileContent |Used for getting a file on Document Library |
| CreateFile |Used for uploading a file on Document Library |
| CopyFile |Used for copying a file on Document Library |
| ExtractFolderV2 |Used for extracting a folder on Document Library |
| PostItem |Creates a new item in a SharePoint list |
| GetItem |Retrieves a single item from a SharePoint list |
| DeleteItem |Deletes an item from a SharePoint list |
| PatchItem |Updates an item in a SharePoint list |

### <a name="sharepoint-triggers"></a>SharePoint triggers
You can listen for these event(s):

| Trigger | Description |
| --- | --- |
| OnNewFile |Triggers a flow when a new file is created in a SharePoint folder |
| OnUpdatedFile |Triggers a flow when a file is modified in a SharePoint folder |
| GetOnNewItems |When a new item is created in a SharePoint list |
| GetOnUpdatedItems |When an existing item is modified in a SharePoint list |

## <a name="create-a-connection-to-sharepoint"></a>Create a connection to SharePoint
To use the SharePoint Connector , you first create a **connection** then provide the details for these properties: 

| Property | Required | Description |
| --- | --- | --- |
| Token |Yes |Provide SharePoint Credentials |

In order to connect to **SharePoint Online**, you need to provide your identity (username and password, smart card credentials, etc.) to SharePoint Online. Once you've been authenticated, you can proceed to use the SharePoint Online Connector  in your logic app. 

While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:

1. Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:   
   ![Configure SharePoint][1]  
2. Select **SharePoint Online - When a file is created**   
3. Select **Sign in to SharePoint Online**:   
   ![Configure SharePoint][2]    
4. Provide your SharePoint credentials to sign in to authenticate with SharePoint   
   ![Configure SharePoint][3]     
5. After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.          
   ![Configure SharePoint][4]  
6. You can then add other triggers and actions that you need to complete your logic app.   
7. Save your work by selecting **Save** on the menu bar above.  

## <a name="sharepoint-rest-api-reference"></a>SharePoint REST API reference
#### <a name="this-documentation-is-for-version-10"></a>This documentation is for version: 1.0
### <a name="used-for-getting-a-file-metadata-on-document-library"></a>Used for getting a file metadata on Document Library
**```GET: /datasets/{dataset}/files/{id}```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| id |string |yes |path |none |Unique identifier of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-updating-a-file-on-document-library"></a>Used for updating a file on Document Library
**```PUT: /datasets/{dataset}/files/{id}```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| id |string |yes |path |none |Unique identifier of the file |
| body | |yes |body |none |The Content of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-deleting-a-file-on-document-library"></a>Used for deleting a file on Document Library
**```DELETE: /datasets/{dataset}/files/{id}```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| id |string |yes |path |none |Unique identifier of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-getting-a-file-metadata-on-document-library"></a>Used for getting a file metadata on Document Library
**```GET: /datasets/{dataset}/GetFileByPath```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| path |string |yes |query |none |Path of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-getting-a-file-on-document-library"></a>Used for getting a file on Document Library
**```GET: /datasets/{dataset}/GetFileContentByPath```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| path |string |yes |query |none |Path of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-getting-a-file-on-document-library"></a>Used for getting a file on Document Library
**```GET: /datasets/{dataset}/files/{id}/content```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| id |string |yes |path |none |Unique identifier of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-uploading-a-file-on-document-library"></a>Used for uploading a file on Document Library
**```POST: /datasets/{dataset}/files```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| folderPath |string |yes |query |none |The path to the folder |
| name |string |yes |query |none |Name of the file |
| body | |yes |body |none |The Content of the file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-copying-a-file-on-document-library"></a>Used for copying a file on Document Library
**```POST: /datasets/{dataset}/copyFile```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| source |string |yes |query |none |Path to the source file |
| destination |string |yes |query |none |Path to the destination file |
| overwrite |boolean |no |query |false |Whether or not to overwrite an existing file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="triggers-a-flow-when-a-new-file-is-created-in-a-sharepoint-folder"></a>Triggers a flow when a new file is created in a SharePoint folder
**```GET: /datasets/{dataset}/triggers/onnewfile```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint site url |
| folderId |string |yes |query |none |Unique identifier of the folder in SharePoint |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="triggers-a-flow-when-a-file-is-modified-in-a-sharepoint-folder"></a>Triggers a flow when a file is modified in a SharePoint folder
**```GET: /datasets/{dataset}/triggers/onupdatedfile```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint site url |
| folderId |string |yes |query |none |Unique identifier of the folder in SharePoint |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="used-for-extracting-a-folder-on-document-library"></a>Used for extracting a folder on Document Library
**```POST: /datasets/{dataset}/extractFolderV2```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site URL. E.g. http://contoso.sharepoint.com/sites/mysite |
| source |string |yes |query |none |Path to the source file |
| destination |string |yes |query |none |Path to the destination folder |
| overwrite |boolean |no |query |false |Whether or not to overwrite an existing file |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="when-a-new-item-is-created-in-a-sharepoint-list"></a>When a new item is created in a SharePoint list
**```GET: /datasets/{dataset}/tables/{table}/onnewitems```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site url (example: http://contoso.sharepoint.com/sites/mysite) |
| table |string |yes |path |none |SharePoint list name |
| $skip |integer |no |query |none |Number of entries to skip (default = 0) |
| $top |integer |no |query |none |Maximum number of entries to retrieve (default = 256) |
| $filter |string |no |query |none |An ODATA filter query to restrict the number of entries |
| $orderby |string |no |query |none |An ODATA orderBy query for specifying the order of entries |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="when-an-existing-item-is-modified-in-a-sharepoint-list"></a>When an existing item is modified in a SharePoint list
**```GET: /datasets/{dataset}/tables/{table}/onupdateditems```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site url (example: http://contoso.sharepoint.com/sites/mysite) |
| table |string |yes |path |none |SharePoint list name |
| $skip |integer |no |query |none |Number of entries to skip (default = 0) |
| $top |integer |no |query |none |Maximum number of entries to retrieve (default = 256) |
| $filter |string |no |query |none |An ODATA filter query to restrict the number of entries |
| $orderby |string |no |query |none |An ODATA orderBy query for specifying the order of entries |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="creates-a-new-item-in-a-sharepoint-list"></a>Creates a new item in a SharePoint list
**```POST: /datasets/{dataset}/tables/{table}/items```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site url (example: http://contoso.sharepoint.com/sites/mysite) |
| table |string |yes |path |none |SharePoint list name |
| item | |yes |body |none |Item to create |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="retrieves-a-single-item-from-a-sharepoint-list"></a>Retrieves a single item from a SharePoint list
**```GET: /datasets/{dataset}/tables/{table}/items/{id}```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site url (example: http://contoso.sharepoint.com/sites/mysite) |
| table |string |yes |path |none |SharePoint list name |
| id |integer |yes |path |none |Unique identifier of item to be retrieved |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="deletes-an-item-from-a-sharepoint-list"></a>Deletes an item from a SharePoint list
**```DELETE: /datasets/{dataset}/tables/{table}/items/{id}```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site url (example: http://contoso.sharepoint.com/sites/mysite) |
| table |string |yes |path |none |SharePoint list name |
| id |integer |yes |path |none |Unique identifier of item to be deleted |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
### <a name="updates-an-item-in-a-sharepoint-list"></a>Updates an item in a SharePoint list
**```PATCH: /datasets/{dataset}/tables/{table}/items/{id}```** 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| dataset |string |yes |path |none |SharePoint Site url (example: http://contoso.sharepoint.com/sites/mysite) |
| table |string |yes |path |none |SharePoint list name |
| id |integer |yes |path |none |Unique identifier of item to be updated |
| item | |yes |body |none |Item with changed properties |

### <a name="here-are-the-possible-responses"></a>Here are the possible responses:
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

- - -
## <a name="object-definitions"></a>Object definition(s):
 **DataSetsMetadata**:

Required properties for DataSetsMetadata:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| tabular |not defined |
| blob |not defined |

 **TabularDataSetsMetadata**:

Required properties for TabularDataSetsMetadata:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| source |string |
| displayName |string |
| urlEncoding |string |
| tableDisplayName |string |
| tablePluralName |string |

 **BlobDataSetsMetadata**:

Required properties for BlobDataSetsMetadata:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| source |string |
| displayName |string |
| urlEncoding |string |

 **BlobMetadata**:

Required properties for BlobMetadata:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| Id |string |
| Name |string |
| DisplayName |string |
| Path |string |
| LastModified |string |
| Size |integer |
| MediaType |string |
| IsFolder |boolean |
| ETag |string |
| FileLocator |string |

 **Object**:

Required properties for Object:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
|  | |

 **TableMetadata**:

Required properties for TableMetadata:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| name |string |
| title |string |
| x-ms-permission |string |
| schema |not defined |

 **DataSetsList**:

Required properties for DataSetsList:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| value |array |

 **DataSet**:

Required properties for DataSet:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| Name |string |
| DisplayName |string |

 **Table**:

Required properties for Table:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| Name |string |
| DisplayName |string |

 **Item**:

Required properties for Item:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| ItemInternalId |string |

 **ItemsList**:

Required properties for ItemsList:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| value |array |

 **TablesList**:

Required properties for TablesList:

None of the properties are required. 

**All properties**: 

| Name | Data Type |
| --- | --- |
| value |array |

## <a name="next-steps"></a>Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)  

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png




