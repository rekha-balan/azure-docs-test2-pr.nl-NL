---
title: Single sign-on with Application Proxy | Microsoft Docs
description: Covers how to provide single sign-on using Azure AD Application Proxy.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 16a2d87c7d955a6a36d70f2717a042ed7be42b37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552935"
---
# <a name="provide-single-sign-on-to-your-apps-with-application-proxy"></a>Provide single sign-on to your apps with Application Proxy
Single sign-on is a key element of Azure AD Application Proxy. It provides the best user experience with the following steps:

1. A user signs in to the cloud.  
2. All security validations happen in the cloud (preauthentication).  
3. When the request is sent to the on-prem application, the Application Proxy Connector impersonates the user. The backend application thinks this is a regular user coming from a domain-joined device.

![Access diagram from end user, through Application Proxy, to the corporate network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_diagram.png)

Azure AD Application Proxy helps you provide a single sign-on (SSO) experience for your users. Use the following instructions to publish your apps using SSO:

## <a name="sso-for-on-prem-iwa-apps-using-kcd-with-application-proxy"></a>SSO for on-prem IWA apps using KCD with Application Proxy
You can enable single sign-on to your applications using Integrated Windows Authentication (IWA) by giving Application Proxy Connectors permission in Active Directory to impersonate users, and send and receive tokens on their behalf.

### <a name="network-diagram"></a>Network diagram
This diagram explains the flow when a user attempts to access an on-prem application that uses IWA.

![Microsoft AAD authentication flow diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. The user enters the URL to access the on-prem application through Application Proxy.
2. Application Proxy redirects the request to Azure AD authentication services to preauthenticate. At this point, Azure AD applies any applicable authentication and authorization policies, such as multifactor authentication. If the user is validated, Azure AD creates a token and sends it to the user.
3. The user passes the token to Application Proxy.
4. Application Proxy validates the token and retrieves the User Principal Name (UPN) from it, and then sends the request, the UPN, and the Service Principal Name (SPN) to the Connector through a dually authenticated secure channel.
5. The Connector performs Kerberos Constrained Delegation (KCD) negotiation with the on-prem AD, impersonating the user to get a Kerberos token to the application.
6. Active Directory sends the Kerberos token for the application to the Connector.
7. The Connector sends the original request to the application server, using the Kerberos token it received from AD.
8. The application sends the response to the Connector, which is then returned to the Application Proxy service and finally to the user.

### <a name="prerequisites"></a>Prerequisites
Before you get started with SSO for Application Proxy, make sure your environment is ready with the following settings and configurations:

* Your apps, like SharePoint Web apps, are set to use Integrated Windows Authentication. For more information, see [Enable Support for Kerberos Authentication](https://technet.microsoft.com/library/dd759186.aspx), or for SharePoint see [Plan for Kerberos authentication in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* All your apps have Service Principal Names.
* The server running the Connector and the server running the app are domain joined and part of the same domain or trusting domains. For more information on domain join, see [Join a Computer to a Domain](https://technet.microsoft.com/library/dd807102.aspx).
* The server running the Connector has access to read the TokenGroupsGlobalAndUniversal for users. This is a default setting that might have been impacted by security hardening the environment. Get more help with this setting in [KB2009157](https://support.microsoft.com/en-us/kb/2009157).

### <a name="active-directory-configuration"></a>Active Directory configuration
The Active Directory configuration varies, depending on whether your Application Proxy Connector and the published server are in the same domain or not.

#### <a name="connector-and-published-server-in-the-same-domain"></a>Connector and published server in the same domain
1. In Active Directory, go to **Tools** > **Users and Computers**.
2. Select the server running the Connector.
.3. Right-click and select **Properties** > **Delegation**.
4. Select **Trust this computer for delegation to specified services only**. Under **Services to which this account can present delegated credentials** add the value for the SPN identity of the application server.
5. This enables the Application Proxy Connector to impersonate users in AD against the applications defined in the list.

![Connector-SVR Properties window screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-published-server-in-different-domains"></a>Connector and published server in different domains
1. For a list of prerequisites for working with KCD across domains, see [Kerberos Constrained Delegation across domains](https://technet.microsoft.com/library/hh831477.aspx).
2. In Windows 2012 R2, use the `principalsallowedtodelegateto` property on the Connector server to enable the Application Proxy to delegate for the Connector server, where the published server is `sharepointserviceaccount` and the delegating server is `connectormachineaccount`.

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

> [!NOTE]
> `sharepointserviceaccount` can be the SPS machine account or a service account under which the SPS app pool is running.
>
>

### <a name="azure-classic-portal-configuration"></a>Azure classic portal configuration
1. Publish your application according to the instructions described in [Publish applications with Application Proxy](active-directory-application-proxy-publish.md). Make sure to select **Azure Active Directory** as the **Preauthentication Method**.
2. After your application appears in the list of applications, select it and click **Configure**.
3. Under **Properties**, set **Internal Authentication Method** to **Integrated Windows Authentication**.  
   ![Advanced Application Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  
4. Enter the **Internal Application SPN** of the application server. In this example, the SPN for our published application is http/lob.contoso.com.  

> [!IMPORTANT]
> If your on-premises UPN and the UPN in Azure Active Directory are not identical, you need to configure the [delegated login identity](#delegated-login-identity) in order for preauthentication to work.
>
>

|  |  |
| --- | --- |
| Internal Authentication Method |If you use Azure AD for preauthentication, you can set an internal authentication method to enable your users to benefit from single sign-on (SSO) to this application. <br><br> Select **Integrated Windows Authentication** (IWA) if your application uses IWA and you can configure Kerberos Constrained Delegation (KCD) to enable SSO for this application. Applications that use IWA must be configured using KCD, otherwise Application Proxy can't publish these applications. <br><br> Select **None** if your application does not use IWA. |
| Internal Application SPN |This is the Service-Principal-Name (SPN) of the internal application as configured in the on-prem Azure AD. The SPN is used by the Application Proxy Connector to fetch Kerberos tokens for the application using KCD. |

## <a name="sso-for-non-windows-apps"></a>SSO for non-Windows apps
The Kerberos delegation flow in Azure AD Application Proxy starts when Azure AD authenticates the user in the cloud. Once the request arrives on-premises, the Azure AD Application Proxy Connector issues a Kerberos ticket on behalf of the user by interacting with the local Active Directory. This process is referred to as Kerberos Constrained Delegation (KCD). In the next phase, a request is sent to the backend application with this Kerberos ticket. There are several protocols that define how to send such requests. Most non-Windows servers expect Negotiate/SPNego that is now supported on Azure AD Application Proxy.

![Non-Windows SSO diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_nonwindows_diagram.png)

For more information about Kerberos, see [All you want to know about Kerberos Constrained Delegation (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="delegated-login-identity"></a>Delegated login identity
Delegated login identity helps you handle two different login scenarios:

* Non-Windows applications that typically get user identity in the form of a username or SAM account name, not an email address (username@domain).
* Alternative login configurations where the UPN in Azure AD and the UPN in your on-premises Active Directory are different.

With Application Proxy, you can select which identity to use to obtain the Kerberos ticket. This setting is per application. Some of these options are suitable for systems that do not accept email address format, others are designed for alternative login.

![Delegated login identity parameter screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

If delegated login identity is used, the value might not be unique for all the domains or forests in your organization. You can avoid this issue by publishing these applications twice using two different Connector groups. Since each application has a different user audience, you can join its Connectors to a different domain.

## <a name="working-with-sso-when-on-premises-and-cloud-identities-are-not-identical"></a>Working with SSO when on-premises and cloud identities are not identical
Unless otherwise configured, Application Proxy assumes that users have exactly the same identity in the cloud and on-premises. You can configure, for each application, which identity should be used when performing single sign-on.  

This capability allows many organizations that have different on-prem and cloud identities to have SSO from the cloud to on-prem apps without requiring the users to enter different usernames and passwords. This includes organizations that:

* Have multiple domains internally (joe@us.contoso.com, joe@eu.contoso.com) and a single domain in the cloud (joe@contoso.com).
* Have non-routable domain name internally (joe@contoso.usa) and a legal one in the cloud.
* Do not use domain names internally (joe)
* Use different aliases on-prem and in the cloud. E.g. joe-johns@contoso.com vs. joej@contoso.com  

It also helps with applications that do not accept addresses in the form of email address, which is a very common scenario for non-Windows backend servers.

### <a name="setting-sso-for-different-cloud-and-on-prem-identities"></a>Setting SSO for different cloud and on-prem identities
1. Configure Azure AD Connect settings so the main identity is the email address (mail). This is done as part of the customize process, by changing the **User Principal Name** field in the sync settings. These settings also determine how users log in to Office365, Windows10 devices, and other applications that use Azure AD as their identity store.  
   ![Identifying users screenshot - User Principal Name dropdown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. In the Application Configuration settings for the application you would like to modify, select the **Delegated Login Identity** to be used:

   * User Principal Name: joe@contoso.com  
   * Alternate User Principal Name: joed@contoso.local  
   * Username part of User Principal Name: joe  
   * Username part of Alternate User Principal Name: joed  
   * On-premises SAM account name: depending on-prem domain controller configuration

   ![Delegated login identity drop-down menu screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)  

### <a name="troubleshooting-sso-for-different-identities"></a>Troubleshooting SSO for different identities
If there is an error in the SSO process, it appears in the Connector machine event log as explained in [Troubleshooting](active-directory-application-proxy-troubleshoot.md).
But, in some cases, the request is successfully sent to the backend application while this application replies in various other HTTP responses. Troubleshooting these cases should start by examining event number 24029 on the Connector machine in the Application Proxy session event log. The user identity that was used for delegation appears in the “user” field within the event details. To turn on session log, select **Show analytic and debug logs** in the event viewer view menu.

## <a name="see-also"></a>See also
* [Publish applications with Application Proxy](active-directory-application-proxy-publish.md)
* [Troubleshoot issues you're having with Application Proxy](active-directory-application-proxy-troubleshoot.md)
* [Working with claims aware applications](active-directory-application-proxy-claims-aware-apps.md)
* [Enable conditional access](active-directory-application-proxy-conditional-access.md)

For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-sso-using-kcd/Properties.jpg










