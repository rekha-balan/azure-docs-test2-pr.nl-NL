---
title: Add the Excel connector | Microsoft Docs
description: Overview of the Excel connector with REST API parameters
services: ''
documentationcenter: ''
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 03af8652-9223-4348-9490-602872a680f0
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: aa8b95bd92d6bed60ba20ffd28e53d26930d7a31
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552095"
---
# <a name="get-started-with-the-excel-connector"></a><span data-ttu-id="aa9d9-103">Get started with the Excel connector</span><span class="sxs-lookup"><span data-stu-id="aa9d9-103">Get started with the Excel connector</span></span>
<span data-ttu-id="aa9d9-104">Currently, there is no Excel connector in Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="aa9d9-104">Currently, there is no Excel connector in Logic Apps.</span></span> 

## <a name="to-use-excel-data"></a><span data-ttu-id="aa9d9-105">To use Excel data</span><span class="sxs-lookup"><span data-stu-id="aa9d9-105">To use Excel data</span></span>
<span data-ttu-id="aa9d9-106">You can store Excel data as a comma-separated value (CSV) file in a storage folder, such as [OneDrive](connectors-create-api-onedrive.md).</span><span class="sxs-lookup"><span data-stu-id="aa9d9-106">You can store Excel data as a comma-separated value (CSV) file in a storage folder, such as [OneDrive](connectors-create-api-onedrive.md).</span></span> <span data-ttu-id="aa9d9-107">You can also use this CSV file with the [flat-file connector](../logic-apps/logic-apps-enterprise-integration-flatfile.md).</span><span class="sxs-lookup"><span data-stu-id="aa9d9-107">You can also use this CSV file with the [flat-file connector](../logic-apps/logic-apps-enterprise-integration-flatfile.md).</span></span>

<!---

There is no Excel connector in Logic Apps. Originally, this topic only referenced PowerApps. Removed all PowerApps references. 



Connect to Excel to insert a row, delete a row, and more. 

## Triggers and actions
Excel includes the following action. There are no triggers. 

|Trigger|Actions|
|--- | ---|
|None | <ul><li>Get rows</li><li>Insert row</li><li>Delete row</li><li>Get row</li><li>Get tables</li><li>Update row</li></ul>

All connectors support data in JSON and XML formats. 

## Swagger REST API reference
Applies to version: 1.0.

### Inserts a new row into an Excel table
```POST: /datasets/{dataset}/tables/{table}/items``` 



| Name| Data Type|Required|Located In|Default Value|Description|
| ---|---|---|---|---|---|
|dataset|string|yes|path|none|Excel file name|
|table|string|yes|path|none|Excel table name|
|item| |yes|body|none|Row to insert into the specified Excel table|


### Response

|Name|Description|
|---|---|
|200|OK|
|default|Operation Failed.|




### Retrieves a single row from an Excel table
```GET: /datasets/{dataset}/tables/{table}/items/{id}``` 



| Name| Data Type|Required|Located In|Default Value|Description|
| ---|---|---|---|---|---|
|dataset|string|yes|path|none|Excel file name|
|table|string|yes|path|none|Excel table name|
|id|string|yes|path|none|Unique identifier of row to retrieve|


### Response

|Name|Description|
|---|---|
|200|OK|
|default|Operation Failed.|




### Deletes a row from an Excel table
```DELETE: /datasets/{dataset}/tables/{table}/items/{id}``` 



| Name| Data Type|Required|Located In|Default Value|Description|
| ---|---|---|---|---|---|
|dataset|string|yes|path|none|Excel file name|
|table|string|yes|path|none|Excel table name|
|id|string|yes|path|none|Unique identifier of the row to delete|


### Response

|Name|Description|
|---|---|
|200|OK|
|default|Operation Failed.|




### Updates an existing row in an Excel table
```PATCH: /datasets/{dataset}/tables/{table}/items/{id}``` 



| Name| Data Type|Required|Located In|Default Value|Description|
| ---|---|---|---|---|---|
|dataset|string|yes|path|none|Excel file name|
|table|string|yes|path|none|Excel table name|
|id|string|yes|path|none|Unique identifier of the row to update|
|item| |yes|body|none|Row with updated values|


### Response

|Name|Description|
|---|---|
|200|OK|
|default|Operation Failed.|




## Object definitions

#### DataSetsMetadata

| Name | Data Type | Required|
|---|---|---|
|tabular|not defined|no|
|blob|not defined|no|

#### TabularDataSetsMetadata

| Name | Data Type |Required|
|---|---|---|
|source|string|no|
|displayName|string|no|
|urlEncoding|string|no|
|tableDisplayName|string|no|
|tablePluralName|string|no|

#### BlobDataSetsMetadata

| Name | Data Type |Required|
|---|---|---|
|source|string|no|
|displayName|string|no|
|urlEncoding|string|no|

#### TableMetadata

| Name | Data Type |Required|
|---|---|---|
|name|string|no|
|title|string|no|
|x-ms-permission|string|no|
|schema|not defined|no|

#### DataSetsList

| Name | Data Type |Required|
|---|---|---|
|value|array|no|

#### DataSet

| Name | Data Type |Required|
|---|---|---|
|Name|string|no|
|DisplayName|string|no|

#### Table

| Name | Data Type |Required|
|---|---|---|
|Name|string|no|
|DisplayName|string|no|

#### Item

| Name | Data Type |Required|
|---|---|---|
|ItemInternalId|string|no|

#### TablesList

| Name | Data Type |Required|
|---|---|---|
|value|array|no|

#### ItemsList

| Name | Data Type |Required|
|---|---|---|
|value|array|no|


## Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)  


-->
