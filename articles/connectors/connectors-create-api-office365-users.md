---
title: Add the Office 365 Users connector in Logic Apps | Microsoft Docs
description: Overview of Office 365 Users connector with REST API parameters
services: ''
documentationcenter: ''
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 407aaf57cf7e174e1561a3c383e08ab25df78428
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552104"
---
# <a name="get-started-with-the-office-365-users-connector"></a>Get started with the Office 365 Users connector
Connect to Office 365 Users to get profiles, search users, and more. 

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version.
> 
> 

With Office 365 Users, you can:

* Build your business flow based on the data you get from Office 365 Users. 
* Use actions that get direct reports, get a manager's user profile, and more. These actions get a response, and then make the output available for other actions. For example, get a person's direct reports, and then take this information and update a SQL Azure database. 

To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
The Office 365 Users connector has the following actions available. There are no triggers.

| Triggers | Actions |
| --- | --- |
| None |<ul><li>Get manager</li><li>Get my profile</li><li>Get direct reports</li><li>Get user profile</li><li>Search for users</li></ul> |

All connectors support data in JSON and XML formats. 

## <a name="create-a-connection-to-office-365-users"></a>Create a connection to Office 365 Users
When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

After you create the connection, you enter the Office 365 Users properties, like the user ID. The **REST API reference** in this topic describes these properties.

> [!TIP]
> You can use this same Office 365 Users connection in other logic apps.
> 
> 

## <a name="office-365-users-rest-api-reference"></a>Office 365 Users REST API reference
Applies to version: 1.0.

### <a name="get-my-profile"></a>Get my profile
Retrieves the profile for the current user.  
```GET: /users/me``` 

There are no parameters for this call.

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="get-user-profile"></a>Get user profile
Retrieves a specific user profile.  
```GET: /users/{userId}``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| userId |string |yes |path |none |User principal name or email id |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="get-manager"></a>Get manager
Retrieves user profile for the manager of the specified user.  
```GET: /users/{userId}/manager``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| userId |string |yes |path |none |User principal name or email id |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="get-direct-reports"></a>Get direct reports
Get direct reports.  
```GET: /users/{userId}/directReports``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| userId |string |yes |path |none |User principal name or email id |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

### <a name="search-for-users"></a>Search for users
Retrieves search results of user profiles.  
```GET: /users``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| searchTerm |string |no |query |none |Search string (applies to: display name, given name, surname, mail, mail nickname and user principal name) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
#### <a name="user-user-model-class"></a>User: User model class
| Property Name | Data Type | Required |
| --- | --- | --- |
| DisplayName |string |no |
| GivenName |string |no |
| Surname |string |no |
| Mail |string |no |
| MailNickname |string |no |
| TelephoneNumber |string |no |
| AccountEnabled |boolean |no |
| Id |string |yes |
| UserPrincipalName |string |no |
| Department |string |no |
| JobTitle |string |no |
| mobilePhone |string |no |

## <a name="next-steps"></a>Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

Go back to the [APIs list](apis-list.md).

<!--References-->
[5]: https://portal.azure.com
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/aad-tenant-applications.PNG
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/aad-tenant-applications-add-appinfo.PNG
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/aad-tenant-applications-add-app-properties.PNG
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/contoso-aad-app.PNG
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/contoso-aad-app-configure.PNG





