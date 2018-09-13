---
title: 'Azure AD Connect: Troubleshoot connectivity issues | Microsoft Docs'
description: Explains how to troubleshoot connectivity issues with Azure AD Connect.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: 64ec261b3e65f0a3fb2a2a5ef6e14588248c76dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661514"
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Troubleshoot connectivity issues with Azure AD Connect
This article explains how connectivity between Azure AD Connect and Azure AD works and how to troubleshoot connectivity issues. These issues are most likely to be seen in an environment with a proxy server.

## <a name="troubleshoot-connectivity-issues-in-the-installation-wizard"></a>Troubleshoot connectivity issues in the installation wizard
Azure AD Connect is using Modern Authentication (using the ADAL library) for authentication. The installation wizard and the sync engine proper require machine.config to be properly configured since these two are .NET applications.

In this article, we show how Fabrikam connects to Azure AD through its proxy. The proxy server is named fabrikamproxy and is using port 8080.

First we need to make sure [**machine.config**](active-directory-aadconnect-prerequisites.md#connectivity) is correctly configured.  
![machineconfig](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> In some non-Microsoft blogs, it is documented that changes should be made to miiserver.exe.config instead. However, this file is overwritten on every upgrade so even if it works during initial install, the system stops working on first upgrade. For that reason, the recommendation is to update machine.config instead.
>
>

The proxy server must also have the required URLs opened. The official list is documented in [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Of these URLs, the following table is the absolute bare minimum to be able to connect to Azure AD at all. This list does not include any optional features, such as password writeback, or Azure AD Connect Health. It is documented here to help in troubleshooting for the initial configuration.

| URL | Port | Description |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Used to download CRL lists. |
| \*.verisign.com |HTTP/80 |Used to download CRL lists. |
| \*.entrust.com |HTTP/80 |Used to download CRL lists for MFA. |
| \*.windows.net |HTTPS/443 |Used to sign in to Azure AD. |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |Used for MFA. |
| \*.microsoftonline.com |HTTPS/443 |Used to configure your Azure AD directory and import/export data. |

## <a name="errors-in-the-wizard"></a>Errors in the wizard
The installation wizard is using two different security contexts. On the page **Connect to Azure AD**, it is using the currently signed in user. On the page **Configure**, it is changing to the [account running the service for the sync engine](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). If there is an issue, it appears most likely already at the **Connect to Azure AD** page in the wizard since the proxy configuration is global.

The following issues are the most common errors you encounter in the installation wizard.

### <a name="the-installation-wizard-has-not-been-correctly-configured"></a>The installation wizard has not been correctly configured
This error appears when the wizard itself cannot reach the proxy.  
![nomachineconfig](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* If you see this error, verify the [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) has been correctly configured.
* If that looks correct, follow the steps in [Verify proxy connectivity](#verify-proxy-connectivity) to see if the issue is present outside the wizard as well.

### <a name="a-microsoft-account-is-used"></a>A Microsoft account is used
If you use a **Microsoft account** rather than a **school or organization** account, you see a generic error.  
![A Microsoft Account is used](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="the-mfa-endpoint-cannot-be-reached"></a>The MFA endpoint cannot be reached
This error appears if the endpoint **https://secure.aadcdn.microsoftonline-p.com** cannot be reached and your global admin has MFA enabled.  
![nomachineconfig](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* If you see this error, verify that the endpoint **secure.aadcdn.microsoftonline-p.com** has been added to the proxy.

### <a name="the-password-cannot-be-verified"></a>The password cannot be verified
If the installation wizard is successful in connecting to Azure AD, but the password itself cannot be verified you see this error:  
![badpassword](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Is the password a temporary password and must be changed? Is it actually the correct password? Try to sign in to https://login.microsoftonline.com (on another computer than the Azure AD Connect server) and verify the account is usable.

### <a name="verify-proxy-connectivity"></a>Verify proxy connectivity
To verify if the Azure AD Connect server has actual connectivity with the Proxy and Internet, use some PowerShell to see if the proxy is allowing web requests or not. In a PowerShell prompt, run `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Technically the first call is to https://login.microsoftonline.com and this URI works as well, but the other URI is faster to respond.)

PowerShell uses the configuration in machine.config to contact the proxy. The settings in winhttp/netsh should not impact these cmdlets.

If the proxy is correctly configured, you should get a success status: ![proxy200](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

If you receive **Unable to connect to the remote server**, then PowerShell is trying to make a direct call without using the proxy or DNS is not correctly configured. Make sure the **machine.config** file is correctly configured.
![unabletoconnect](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

If the proxy is not correctly configured, you get an error: ![proxy200](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Error | Error Text | Comment |
| --- | --- | --- |
| 403 |Forbidden |The proxy has not been opened for the requested URL. Revisit the proxy configuration and make sure the [URLs](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) have been opened. |
| 407 |Proxy Authentication Required |The proxy server required a sign-in and none was provided. If your proxy server requires authentication, make sure to have this setting configured in the machine.config. Also make sure you are using domain accounts for the user running the wizard and for the service account. |

## <a name="the-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>The communication pattern between Azure AD Connect and Azure AD
If you have followed all these preceding steps and still cannot connect, you might at this point start looking at network logs. This section is documenting a normal and successful connectivity pattern. It is also listing common red herrings that can be ignored when you are reading the network logs.

* There are calls to https://dc.services.visualstudio.com. It is not required to have this URL open in the proxy for the installation to succeed and these calls can be ignored.
* You see that dns resolution lists the actual hosts to be in the DNS name space nsatc.net and other namespaces not under microsoftonline.com. However, there are not any web service requests on the actual server names and you do not have to add these URLs to the proxy.
* The endpoints adminwebservice and provisioningapi are discovery endpoints and used to find the actual endpoint to use. These endpoints are different depending on your region.

### <a name="reference-proxy-logs"></a>Reference proxy logs
Here is a dump from an actual proxy log and the installation wizard page from where it was taken (duplicate entries to the same endpoint have been removed). This section can be used as a reference for your own proxy and network logs. The actual endpoints might be different in your environment (in particular those URLs in *italic*).

**Connect to Azure AD**

| Time | URL |
| --- | --- |
| 1/11/2016 8:31 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Configure**

| Time | URL |
| --- | --- |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Initial Sync**

| Time | URL |
| --- | --- |
| 1/11/2016 8:48 |connect://login.windows.net:443 |
| 1/11/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>Authentication errors
This section covers errors that can be returned from ADAL (the authentication library used by Azure AD Connect) and PowerShell. The error explained should help you in understand your next steps.

### <a name="invalid-grant"></a>Invalid Grant
Invalid username or password. For more information, see [The password cannot be verified](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Unknown User Type
Your Azure AD directory cannot be found or resolved. Maybe you try to login with a username in an unverified domain?

### <a name="user-realm-discovery-failed"></a>User Realm Discovery Failed
Network or proxy configuration issues. The network cannot be reached. See [Troubleshoot connectivity issues in the installation wizard](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>User Password Expired
Your credentials have expired. Change your password.

### <a name="authorizationfailure"></a>AuthorizationFailure
Unknown issue.

### <a name="authentication-cancelled"></a>Authentication Cancelled
The multi-factor authentication (MFA) challenge was cancelled.

### <a name="connecttomsonline"></a>ConnectToMSOnline
Authentication was successful, but Azure AD PowerShell has an authentication problem.

### <a name="azurerolemissing"></a>AzureRoleMissing
Authentication was successful. You are not a global administrator.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
Authentication was successful. Privileged identity management has been enabled and you are currently not a global administrator. For more information, see [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
Authentication was successful. Could not retrieve company information from Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
Authentication was successful. Could not retrieve domain information from Azure AD.

### <a name="unexpected-exception"></a>Unexpected exception
Shown as Unexpected error in the installation wizard. Can happen if you try to use a **Microsoft Account** rather than a **school or organization account**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Troubleshooting steps for previous releases.
With releases starting with build number 1.1.105.0 (released February 2016), the sign-in assistant was retired. This section and the configuration should no longer be required, but is kept as reference.

For the single-sign in assistant to work, winhttp must be configured. This configuration can be done with [**netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="the-sign-in-assistant-has-not-been-correctly-configured"></a>The Sign-in assistant has not been correctly configured
This error appears when the Sign-in assistant cannot reach the proxy or the proxy is not allowing the request.
![nonetsh](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* If you see this error, look at the proxy configuration in [netsh](active-directory-aadconnect-prerequisites.md#connectivity) and verify it is correct.
  ![netshshow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* If that looks correct, follow the steps in [Verify proxy connectivity](#verify-proxy-connectivity) to see if the issue is present outside the wizard as well.

## <a name="next-steps"></a>Next steps
Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).











