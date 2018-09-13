---
title: How to configure single sign-on to an Application Proxy application | Microsoft Docs
description: How you can configure single sign-on to your application proxy application quickly
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: d83dedd6d8ff141b83841b38210715a56f55bf3c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551102"
---
# <a name="how-to-configure-single-sign-on-to-an-application-proxy-application"></a>How to configure single sign-on to an Application Proxy application

Single sign-on (SSO) allows your users to access an application without authenticating multiple times. It allows the single authentication to occur in the cloud, against Azure Active Directory, and allows the service or Connector to impersonate the user to complete any additional authentication challenges from the application.

## <a name="how-to-configure-single-sign-on"></a>How to configure single-sign on
To configure SSO, first make sure that your application is configured for Pre-Authentication through Azure Active Directory. To do this, go to **Azure Active Directory** -&gt; **Enterprise Applications** -&gt; **All Applications** -&gt; Your application **-&gt; Application Proxy**. On this page, you see the “Pre Authentication” field, and make sure that is set to “Azure Active Directory. 

For more information on the Pre-Authentication methods, see step four of the [app publishing document](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Pre-authentication method in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Configuring single sign-on modes for Application Proxy Applications
Next we configure the specific type of single sign-on. The sign-on methods are classified based on what type of authentication the backend application uses. App Proxy applications supports three types of sign-on:

-   **Password-based Sign-On**: Password-based sign-on can be used for any application that uses username and password fields to sign-on. Configuration steps can be found in our [password-SSO configuration documentation](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Integrated Windows Authentication**: For applications using Integrated Windows Authentication (IWA), single sign-on is enabled through Kerberos Constrained Delegation (KCD). This gives Application Proxy Connectors permission in Active Directory to impersonate users, and to send and receive tokens on their behalf. Details on configuring KCD can be found in the [Single Sign-On with KCD documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Header-based Sign-On**: Header-based sign on is enabled through a partnership and does require some additional configuration. For details on the partnership and step-by-step instructions for configuring single sign-on to an application that uses headers for authentication, see the [PingAccess for Azure AD documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Each of these options can be found by going to your application in “Enterprise Applications”, and opening the **Single Sign-On** page on the left menu. note that if your application was created in the old portal, you may not see all these options.

On this page, you also see one additional Sign-On option: Linked Sign-On. This is also supported by Application Proxy. However, note that this option does not add single sign-on to the application. That said the application may already have single sign-on implemented using another service such as Active Directory Federation Services. 

This option allows an admin to create a link to an application that users first land on when accessing the application. For example, if there is an application that is configured to authenticate users using Active Directory Federation Services 2.0, an administrator can use the “Linked Sign-On” option to create a link to it on the access panel.

## <a name="next-steps"></a>Next steps
[Provide single sign-on to your apps with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)

