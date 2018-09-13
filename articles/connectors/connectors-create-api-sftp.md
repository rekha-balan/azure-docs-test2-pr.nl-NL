---
title: Learn how to use the SFTP connector in your logic apps | Microsoft Docs
description: Create logic apps with Azure App service. Connect to SFTP API to send and receive files. You can perform various operations such as create, update, get or delete files.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: deonhe
ms.openlocfilehash: 2977404fb408ea5301c88caa7ce6767a906ca9c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552504"
---
# <a name="get-started-with-the-sftp-connector"></a>Get started with the SFTP connector
Use the SFTP connector to access an SFTP account to send and receive files. You can perform various operations such as create, update, get or delete files.  

To use [any connector](apis-list.md), you first need to create a logic app. You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-to-sftp"></a>Connect to SFTP
Before your logic app can access any service, you first need to create a *connection* to the service. A [connection](connectors-overview.md) provides connectivity between a logic app and another service.  

### <a name="create-a-connection-to-sftp"></a>Create a connection to SFTP
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Use an SFTP trigger
A trigger is an event that can be used to start the workflow defined in a logic app. [Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

In this example, I will show you how to use the **SFTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an SFTP server. In the example, you will also learn how to add a condition that checks the contents of the new or modified file and make a decision to extract the file if its contents indicate that it  should be extracted before using the contents. Finally, you will learn how to add an action to extract the contents of a file and place the extracted contents in a folder on the SFTP server. 

In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent orders from customers.  You could then use an SFTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Add a condition
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Use an SFTP action
An action is an operation carried out by the workflow defined in a logic app. [Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="technical-details"></a>Technical Details
Here are the details about the triggers, actions and responses that this connection supports:

## <a name="sftp-triggers"></a>SFTP triggers
SFTP has the following trigger(s):  

| Trigger | Description |
| --- | --- |
| [When a file is added or modified](connectors-create-api-sftp.md#when-a-file-is-added-or-modified) |This operation triggers a flow when a file is added or modified in a folder. |

## <a name="sftp-actions"></a>SFTP actions
SFTP has the following actions:

| Action | Description |
| --- | --- |
| [Get file metadata](connectors-create-api-sftp.md#get-file-metadata) |This operation gets file metadata using the file id. |
| [Update file](connectors-create-api-sftp.md#update-file) |This operation updates the file content. |
| [Delete file](connectors-create-api-sftp.md#delete-file) |This operation deletes a file. |
| [Get file metadata using path](connectors-create-api-sftp.md#get-file-metadata-using-path) |This operation gets file metadata using the file path. |
| [Get file content using path](connectors-create-api-sftp.md#get-file-content-using-path) |This operation gets file contents using the file path. |
| [Get file content](connectors-create-api-sftp.md#get-file-content) |This operation gets file contents using the file id. |
| [Create file](connectors-create-api-sftp.md#create-file) |This operation uploads a file to an SFTP server. |
| [Copy file](connectors-create-api-sftp.md#copy-file) |This operation copies a file to an SFTP server. |
| [List files in folder](connectors-create-api-sftp.md#list-files-in-folder) |This operation gets files contained in a folder. |
| [List files in root folder](connectors-create-api-sftp.md#list-files-in-root-folder) |This operation gets the files in the root folder. |
| [Extract folder](connectors-create-api-sftp.md#extract-folder) |This operation extracts an archive file into a folder (example: .zip). |

### <a name="action-details"></a>Action details
Here are the details for the actions and triggers for this connector, along with their responses:

### <a name="get-file-metadata"></a>Get file metadata
This operation gets file metadata using the file id. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| id* |File |Specify the file |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

### <a name="update-file"></a>Update file
This operation updates the file content. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| id* |File |Specify the file |
| body* |File content |Content of the file to update |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

### <a name="delete-file"></a>Delete file
This operation deletes a file. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| id* |File |Specify the file |

An * indicates that a property is required

### <a name="get-file-metadata-using-path"></a>Get file metadata using path
This operation gets file metadata using the file path. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| path* |File path |Unique path of the file |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

### <a name="get-file-content-using-path"></a>Get file content using path
This operation gets file contents using the file path. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| path* |File path |Unique path of the file |

An * indicates that a property is required

### <a name="get-file-content"></a>Get file content
This operation gets file contents using the file id. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| id* |File |Specify the file |

An * indicates that a property is required

### <a name="create-file"></a>Create file
This operation uploads a file to an SFTP server. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| folderPath* |Folder path |Unique path of the folder |
| name* |File name |Name of the file |
| body* |File content |Content of the file to create |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

|  | Property Name | Data Type |
| --- | --- | --- |
| Id |string | |
| Name |string | |
| DisplayName |string | |
| Path |string | |
| LastModified |string | |
| Size |integer | |
| MediaType |string | |
| IsFolder |boolean | |
| ETag |string | |
| FileLocator |string | |

### <a name="copy-file"></a>Copy file
This operation copies a file to an SFTP server. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| source* |Source file path |Path to the source file |
| destination* |Destination file path |Path to the destination file, including file name |
| overwrite |Overwrite? |Overwrites the destination file if set to 'true' |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

### <a name="when-a-file-is-added-or-modified"></a>When a file is added or modified
This operation triggers a flow when a file is added or modified in a folder. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| folderId* |Folder |Specify a folder |

An * indicates that a property is required

### <a name="list-files-in-folder"></a>List files in folder
This operation gets files contained in a folder. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| id* |Folder |Specify the folder |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

### <a name="list-files-in-root-folder"></a>List files in root folder
This operation gets the files in the root folder. 

There are no parameters for this call

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

### <a name="extract-folder"></a>Extract folder
This operation extracts an archive file into a folder (example: .zip). 

| Property Name | Display Name | Description |
| --- | --- | --- |
| source* |Source archive file path |Path to the archive file |
| destination* |Destination folder path |Path to the destination folder |
| overwrite |Overwrite? |Overwrites the destination files if set to 'true' |

An * indicates that a property is required

#### <a name="output-details"></a>Output Details
BlobMetadata

| Property Name | Data Type |
| --- | --- | --- |
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

## <a name="http-responses"></a>HTTP responses
The actions and triggers above can return one or more of the following HTTP status codes: 

| Name | Description |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 500 |Internal Server Error. Unknown error occurred. |
| default |Operation Failed. |

## <a name="next-steps"></a>Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)

