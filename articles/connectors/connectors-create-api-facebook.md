---
title: Add the Facebook connector in your Logic Apps | Microsoft Docs
description: Overview of the Facebook connector with REST API parameters
services: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: f4d6f0ed-c09b-488c-be1c-8cf2b5b1d4b8
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b8a66308c4f4f1df610cdacd092ef133bd605665
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563190"
---
# <a name="get-started-with-the-facebook-connector"></a>Get started with the Facebook connector
Connect to Facebook and post to a timeline, get a page feed, and more. 

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version.
> 
> 

With Facebook, you can:

* Build your business flow based on the data you get from Facebook. 
* Use a trigger when a new post is received.
* Use actions that post to your timeline, get a page feed, and more. These actions get a response, and then make the output available for other actions. For example, when there is a new post on your timeline, you can take that post and push it to your Twitter feed. 

To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
The Facebook connector includes the following trigger and actions. 

| Triggers | Actions |
| --- | --- |
| <ul><li>When there is a new post on my timeline</li></ul> |<ul><li>Get feed from my timeline</li><li>Post to my timeline</li><li>When there is a new post on my timeline</li><li>Get page feed</li><li>Get user timeline</li><li>Post to page</li></ul> |

All connectors support data in JSON and XML formats.

## <a name="create-a-connection-to-facebook"></a>Create a connection to Facebook
When you add this connector to your logic apps, you must authorize logic apps to connect to your Facebook.

1. Sign in to your Facebook account
2. Select **Authorize**, and allow your logic apps to connect and use your Facebook. 

> [!INCLUDE [Steps to create a connection to Facebook](../../includes/connectors-create-api-facebook.md)]
> 
> [!TIP]
> You can use this same Facebook connection in other logic apps.
> 
> 

## <a name="swagger-rest-api-reference"></a>Swagger REST API reference
Applies to version: 1.0.

### <a name="get-feed-from-my-timeline"></a>Get feed from my timeline
Gets the feeds from the logged in user's timeline.  
```GET: /me/feed```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| fields |string |no |query |none |Specify the fields you want returned. Example (id,name,picture). |
| limit |integer |no |query |none |Maximum number of posts to be retrieved |
| with |string |no |query |none |Restrict the list of posts to only those with location attached. |
| filter |string |no |query |none |Retrieve only posts that match a particular stream filter. |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="post-to-my-timeline"></a>Post to my timeline
Post a status message to the logged in user's timeline.  
```POST: /me/feed```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| post |string |yes |body |none |New message to be posted |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="when-there-is-a-new-post-on-my-timeline"></a>When there is a new post on my timeline
Triggers a new flow when there is a new post on the logged in user's timeline.  
```GET: /trigger/me/feed```

There are no parameters. 

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="get-page-feed"></a>Get page feed
Get posts from the feed of a specified page.  
```GET: /{pageId}/feed```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| pageId |string |yes |path |none |Id of the page from which posts have to be retrieved. |
| limit |integer |no |query |none |Maximum number of posts to be retrieved |
| include_hidden |boolean |no |query |none |Whether or not to include any posts that were hidden by the Page |
| fields |string |no |query |none |Specify the fields you want returned. Example (id,name,picture). |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="get-user-timeline"></a>Get user timeline
Get Posts from a user's timeline.  
```GET: /{userId}/feed```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| userId |string |yes |path |none |Id of the user whose timeline have to be retrieved. |
| limit |integer |no |query |none |Maximum number of posts to be retrieved |
| with |string |no |query |none |Restrict the list of posts to only those with location attached. |
| filter |string |no |query |none |Retrieve only posts that match a particular stream filter. |
| fields |string |no |query |none |Specify the fields you want returned. Example (id,name,picture). |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="post-to-page"></a>Post to page
Post a message to a Facebook Page as the logged in user.  
```POST: /{pageId}/feed```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| pageId |string |yes |path |none |Id of the page to post. |
| post |many |yes |body |none |New message to be posted. |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
#### <a name="getfeedresponse"></a>GetFeedResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| data |array |no |

#### <a name="triggerfeedresponse"></a>TriggerFeedResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| data |array |no |

#### <a name="postitem-a-single-entry-in-a-profiles-feed"></a>PostItem: A single entry in a profile's feed
The profile could be a user, page, app, or group. 

| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |no |
| admin_creator |array |no |
| caption |string |no |
| created_time |string |no |
| description |string |no |
| feed_targeting |not defined |no |
| from |not defined |no |
| icon |string |no |
| is_hidden |boolean |no |
| is_published |boolean |no |
| link |string |no |
| message |string |no |
| name |string |no |
| object_id |string |no |
| picture |string |no |
| place |not defined |no |
| privacy |not defined |no |
| properties |array |no |
| source |string |no |
| status_type |string |no |
| story |string |no |
| targeting |not defined |no |
| to |array |no |
| type |string |no |
| updated_time |string |no |
| with_tags |not defined |no |

#### <a name="triggeritem-a-single-entry-in-a-profiles-feed"></a>TriggerItem: A single entry in a profile's feed
The profile could be a user, page, app, or group.

| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |no |
| created_time |string |no |
| from |not defined |no |
| message |string |no |
| type |string |no |

#### <a name="adminitem"></a>AdminItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |no |
| link |string |no |

#### <a name="propertyitem"></a>PropertyItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| name |string |no |
| text |string |no |
| href |string |no |

#### <a name="userpostfeedrequest"></a>UserPostFeedRequest
| Property Name | Data Type | Required |
| --- | --- | --- |
| message |string |yes |
| link |string |no |
| picture |string |no |
| name |string |no |
| caption |string |no |
| description |string |no |
| place |string |no |
| tags |string |no |
| privacy |not defined |no |
| object_attachment |string |no |

#### <a name="pagepostfeedrequest"></a>PagePostFeedRequest
| Property Name | Data Type | Required |
| --- | --- | --- |
| message |string |yes |
| link |string |no |
| picture |string |no |
| name |string |no |
| caption |string |no |
| description |string |no |
| actions |array |no |
| place |string |no |
| tags |string |no |
| object_attachment |string |no |
| targeting |not defined |no |
| feed_targeting |not defined |no |
| published |boolean |no |
| scheduled_publish_time |string |no |
| backdated_time |string |no |
| backdated_time_granularity |string |no |
| child_attachments |array |no |
| multi_share_end_card |boolean |no |

#### <a name="postfeedresponse"></a>PostFeedResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |no |

#### <a name="profilecollection"></a>ProfileCollection
| Property Name | Data Type | Required |
| --- | --- | --- |
| data |array |no |

#### <a name="useritem"></a>UserItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |no |
| first_name |string |no |
| last_name |string |no |
| name |string |no |
| gender |string |no |
| about |string |no |

#### <a name="actionitem"></a>ActionItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| name |string |no |
| link |string |no |

#### <a name="targetitem"></a>TargetItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| countries |array |no |
| locales |array |no |
| regions |array |no |
| cities |array |no |

#### <a name="feedtargetitem-object-that-controls-news-feed-targeting-for-this-post"></a>FeedTargetItem: Object that controls news feed targeting for this post
Anyone in these groups is more likely to see this post, others are less likely. Applies to Pages only.

| Property Name | Data Type | Required |
| --- | --- | --- |
| countries |array |no |
| regions |array |no |
| cities |array |no |
| age_min |integer |no |
| age_max |integer |no |
| genders |array |no |
| relationship_statuses |array |no |
| interested_in |array |no |
| college_years |array |no |
| interests |array |no |
| relevant_until |integer |no |
| education_statuses |array |no |
| locales |array |no |

#### <a name="placeitem"></a>PlaceItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |no |
| name |string |no |
| overall_rating |number |no |
| location |not defined |no |

#### <a name="locationitem"></a>LocationItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| city |string |no |
| country |string |no |
| latitude |number |no |
| located_in |string |no |
| longitude |number |no |
| name |string |no |
| region |string |no |
| state |string |no |
| street |string |no |
| zip |string |no |

#### <a name="privacyitem"></a>PrivacyItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| description |string |no |
| value |string |yes |
| allow |string |no |
| deny |string |no |
| friends |string |no |

#### <a name="childattachmentsitem"></a>ChildAttachmentsItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| link |string |no |
| picture |string |no |
| image_hash |string |no |
| name |string |no |
| description |string |no |

#### <a name="postphotorequest"></a>PostPhotoRequest
| Property Name | Data Type | Required |
| --- | --- | --- |
| url |string |yes |
| caption |string |no |

#### <a name="postphotoresponse"></a>PostPhotoResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |yes |
| post_id |string |yes |

#### <a name="postvideorequest"></a>PostVideoRequest
| Property Name | Data Type | Required |
| --- | --- | --- |
| videoData |string |yes |
| description |string |yes |
| title |string |yes |
| uploadedVideoName |string |no |

#### <a name="getphotoresponse"></a>GetPhotoResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| data |not defined |yes |

#### <a name="getphotoresponseitem"></a>GetPhotoResponseItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| url |string |yes |
| is_silhouette |boolean |yes |
| height |string |no |
| width |string |no |

#### <a name="geteventresponse"></a>GetEventResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| data |array |yes |

#### <a name="geteventresponseitem"></a>GetEventResponseItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |yes |
| name |string |yes |
| start_time |string |no |
| end_time |string |no |
| timezone |string |no |
| location |string |no |
| description |string |no |
| ticket_uri |string |no |
| rsvp_status |string |yes |

## <a name="next-steps"></a>Next steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

