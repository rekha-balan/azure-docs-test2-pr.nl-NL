---
title: Manage user data in Azure Active Directory B2C | Microsoft Docs
description: Learn how to delete or export user data in Azure AD B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 05/06/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 49e9efa537ad1f2a1d7f06dd7f8a68a409c7d4e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869879"
---
# <a name="manage-user-data-in-azure-active-directory-b2c"></a>Manage user data in Azure Active Directory B2C

 This article discusses how you can manage the user data in Azure Active Directory (Azure AD) B2C by using the operations that are provided by the [Azure Active Directory Graph API](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog). Managing user data includes deleting or exporting data from audit logs.

[!INCLUDE [gdpr-intro-sentence.md](../../includes/gdpr-intro-sentence.md)]

## <a name="delete-user-data"></a>Delete user data

User data is stored in the Azure AD B2C directory and in the audit logs. All user audit data is retained for 30 days in Azure AD B2C. If you want to delete user data within that 30-day period, you can use the [Delete a user](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#DeleteUser) operation. A DELETE operation is required for each of the Azure AD B2C tenants where data might reside. 

Every user in Azure AD B2C is assigned an object ID. The object ID provides an unambiguous identifier for you to use to delete user data in Azure AD B2C. Depending on your architecture, the object ID can be a useful correlation identifier across other services, such as financial, marketing, and customer relationship management databases. 

The most accurate way to get the object ID for a user is to obtain it as part of an authentication journey with Azure AD B2C. If you receive a valid request for data from a user by using other methods, an offline process, such as a search by a customer service support agent, might be necessary to find the user and note the associated object ID. 

The following example shows a possible data-deletion flow:

1. The user signs in and selects **Delete my data**.
2. The application offers an option to delete the data within an administration section of the application.
3. The application forces an authentication to Azure AD B2C. Azure AD B2C provides a token with the object ID of the user back to the application. 
4. The token is received by the application, and the object ID is used to delete the user data through a call to the Azure AD Graph API. The Azure AD Graph API deletes the user data and returns a status code of 200 OK.
5. The application orchestrates the deletion of user data in other organizational systems as needed by using the object ID or other identifiers.
6. The application confirms the deletion of data and provides next steps to the user.

## <a name="export-customer-data"></a>Export customer data

The process of exporting customer data from Azure AD B2C is similar to the deletion process.

Azure AD B2C user data is limited to:

- **Data stored in the Azure Active Directory**: You can retrieve data in an Azure AD B2C authentication user journey by using the object ID or any sign-in name, such as an email address or username. 
- **User-specific audit events report**: You can index data by using the object ID.

In the following example of an export data flow, the steps that are described as being performed by the application can also be performed by either a backend process or a user with an administrator role in the directory:

1. The user signs in to the application. Azure AD B2C enforces authentication with Azure Multi-Factor Authentication if needed.
2. The application uses the user credentials to call an Azure AD Graph API operation to retrieve the user attributes. The Azure AD Graph API provides the attribute data in JSON format. Depending on the schema, you can set the ID token contents to include all personal data about a user.
3. The application retrieves the user audit activity. The Azure AD Graph API provides the event data to the application.
4. The application aggregates the data and makes it available to the user.

## <a name="next-steps"></a>Next steps

- To learn how to manage how users access your application, see [Manage user access](manage-user-access.md).



