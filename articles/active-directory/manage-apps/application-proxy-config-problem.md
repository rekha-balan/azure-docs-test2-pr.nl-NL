---
title: Problem creating an Application Proxy application | Microsoft Docs
description: How to troubleshoot issues creating Application Proxy applications in the Azure AD Admin portal
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 2344d35827cf541f0230f74917be3ae0ea39e074
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868754"
---
# <a name="problem-creating-an-application-proxy-application"></a>Problem creating an Application Proxy application 

Below are some of the common issues people face when creating a new application proxy application.

## <a name="recommended-documents"></a>Recommended documents 

To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).

If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application. Most error messages include a suggested fix. 

## <a name="specific-things-to-check"></a>Specific things to check

To avoid common errors, verify:

-   You are an administrator with permission to create an Application Proxy application

-   The internal URL is unique

-   The external URL is unique

-   The URLs start with http or https, and end with a “/”

-   The URL should be a domain name and not an IP address

The error message should display in the top right corner when you create the application. You can also select the notification icon to see the error messages.

   ![Notification prompt](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Next steps
[Enable Application Proxy in the Azure portal](application-proxy-enable.md)
