---
title: Claims-aware apps - Azure AD App Proxy | Microsoft Docs
description: How to publish on-premises ASP.NET applications that accept ADFS claims for secure remote access by your users.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: kgremban
ms.openlocfilehash: e53b07576176c58b9135fd160a2e59717d61ce29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553825"
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Working with claims aware apps in Application Proxy
Claims aware apps perform a redirection to the Security Token Service (STS), which in turn requests credentials from the user in exchange for a token before redirecting the user to the application. To enable Application Proxy to work with these redirects, the following steps need to be taken.

## <a name="prerequisites"></a>Prerequisites
Before performing this procedure, make sure that the STS the claims aware app redirects to is available outside of your on-premises network.

## <a name="azure-classic-portal-configuration"></a>Azure classic portal configuration
1. Publish your application according to the instructions described in [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).
2. In the list of applications, select the claims aware app and click **Configure**.
3. If you chose **Passthrough** as your **Preauthentication Method**, make sure to select **HTTPS** as your **External URL** scheme.
4. If you chose **Azure Active Directory** as your **Preauthentication Method**, select **None** as your **Internal Authentication Method**.

## <a name="adfs-configuration"></a>ADFS configuration
1. Open ADFS Management.
2. Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.  

   ![Relying Party Trusts right-click on app name - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.
4. Under **Trusted URL** enter the URL you entered in the Application Proxy under **External URL** and click **OK**.  

   ![Add an Endpoint - set Trusted URL value - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Next steps
* [Enable single-sign on](active-directory-application-proxy-sso-using-kcd.md)
* [Troubleshoot issues you're having with Application Proxy](active-directory-application-proxy-troubleshoot.md)
* [Enable native client apps to interact with proxy applications](active-directory-application-proxy-native-client.md)




