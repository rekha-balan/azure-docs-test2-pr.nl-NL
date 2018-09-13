---
title: RSS | Microsoft Docs
description: Create Logic apps with Azure App service. RSS connector allows the users to publish and retrieve feed items. It also allows the users to trigger operations when a new item is published to the feed.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: a10a6277-ed29-4e68-a881-ccdad6fd0ad8
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 5e13e126fecda66a453b4ced619016121af98b2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552022"
---
# <a name="get-started-with-the-rss-connector"></a>Get started with the RSS connector
RSS is a popular web syndication format used to publish frequently updated content – like blog entries and news headlines.  Many content publishers provide an RSS feed to allow users to subscribe to it.  Use the RSS connector to retrieve feed information and trigger flows when new items are published in an RSS feed.

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version. 
> 
> 

You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
The RSS connector can be used as an action; it has trigger(s). All connectors support data in JSON and XML formats. 

 The RSS connector has the following action(s) and/or trigger(s) available:

### <a name="rss-actions"></a>RSS actions
You can take these action(s):

| Action | Description |
| --- | --- |
| [ListFeedItems](connectors-create-api-rss.md#listfeeditems) |Get all RSS feed items. |

### <a name="rss-triggers"></a>RSS triggers
You can listen for these event(s):

| Trigger | Description |
| --- | --- |
| When a new feed item published |Triggers a workflow when a new feed is published |

## <a name="create-a-connection-to-rss"></a>Create a connection to RSS
> [!INCLUDE [Steps to create a connection to an RSS feed](../../includes/connectors-create-api-rss.md)]
> 
> [!TIP]
> You can use this connection in other logic apps.
> 
> 

## <a name="reference-for-rss"></a>Reference for RSS
Applies to version: 1.0

## <a name="onnewfeed"></a>OnNewFeed
When a new feed item published: Triggers a workflow when a new feed is published 

```GET: /OnNewFeed``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| feedUrl |string |yes |query |none |Feed url |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 500 |Internal Server Error. Unknown error occured |
| default |Operation Failed. |

## <a name="listfeeditems"></a>ListFeedItems
List all RSS feed items.: Get all RSS feed items. 

```GET: /ListFeedItems``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| feedUrl |string |yes |query |none |Feed url |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 500 |Internal Server Error. Unknown error occured |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
### <a name="triggerbatchresponsefeeditem"></a>TriggerBatchResponse[FeedItem]
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="feeditem"></a>FeedItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |Yes |
| title |string |Yes |
| content |string |Yes |
| links |array |No |
| updatedOn |string |No |

## <a name="next-steps"></a>Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)

