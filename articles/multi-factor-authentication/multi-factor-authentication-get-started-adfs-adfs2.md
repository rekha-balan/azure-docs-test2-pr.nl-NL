---
title: Use Azure MFA Server with AD FS 2.0 | Microsoft Docs
description: This is the Azure Multi-Factor authentication page that describes how to get started with Azure MFA and AD FS 2.0.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/24/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e1172c84a151a10cd591aed552da17220175aa2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555258"
---
# <a name="configure-azure-multi-factor-authentication-server-to-work-with-ad-fs-20"></a>Configure Azure Multi-Factor Authentication Server to work with AD FS 2.0
This article is for organizations that are federated with Azure Active Directory, and want to secure resources that are on-premises or in the cloud. Protect your resources by using the Azure Multi-Factor Authentication Server and configuring it to work with AD FS so that two-step verification is triggered for high-value end points.

This documentation covers using the Azure Multi-Factor Authentication Server with AD FS 2.0. For information about AD FS, see [Securing cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Secure AD FS 2.0 with a proxy
To secure AD FS 2.0 with a proxy, install the Azure Multi-Factor Authentication Server on the AD FS proxy server.

### <a name="configure-iis-authentication"></a>Configure IIS authentication
1. In the Azure Multi-Factor Authentication Server, click the **IIS Authentication** icon in the left menu.
2. Click the **Form-Based** tab.
3. Click **Add**.

   <center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. To detect username, password, and domain variables automatically, enter the login URL (like https://sso.contoso.com/adfs/ls) within the Auto-Configure Form-Based Website dialog box and click **OK**.
5. Check the **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to two-step verification. If a significant number of users have not yet been imported into the Server and/or will be exempt from two-step verification, leave the box unchecked. 
6. If the page variables cannot be detected automatically, click the **Specify Manually…** button in the Auto-Configure Form-Based Website dialog box.
7. In the Add Form-Based Website dialog box, enter the URL to the AD FS login page in the Submit URL field (like https://sso.contoso.com/adfs/ls) and enter an Application name (optional). The Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages. 
8. Set the Request format to **POST or GET**.
9. Enter the Username variable (ctl00$ContentPlaceHolder1$UsernameTextBox) and Password variable (ctl00$ContentPlaceHolder1$PasswordTextBox). If your form-based login page displays a domain textbox, enter the Domain variable as well. To find the names of the input boxes on the login page, go to the login page in a web browser, right-click on the page and select **View Source**.
10. Check the **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to two-step verification. If a significant number of users have not yet been imported into the Server and/or will be exempt from two-step verification, leave the box unchecked.
    <center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Click **Advanced…** to review advanced settings. Settings that you can configure include:

    - Select a custom denial page file
    - Cache successful authentications to the website using cookies
    - Select how to authenticate the primary credentials

12. Since the AD FS proxy server is not likely to be joined to the domain, you can use LDAP to connect to your domain controller for user import and pre-authentication. In the Advanced Form-Based Website dialog box, click the **Primary Authentication** tab and select **LDAP Bind** for the Pre-authentication Authentication type.
13. When complete, click **OK** to return to the Add Form-Based Website dialog box. 
14. Click **OK** to close the dialog box.
15. Once the URL and page variables have been detected or entered, the website data displays in the Form-Based panel.
16. Click the **Native Module** tab and select the server, the website that the AD FS proxy is running under (like “Default Web Site”), or the AD FS proxy application (like “ls” under “adfs”) to enable the IIS plug-in at the desired level.
17. Click the **Enable IIS authentication** box at the top of the screen.

The IIS authentication is now enabled.

### <a name="configure-directory-integration"></a>Configure directory integration
You enabled IIS authentication, but to perform the pre-authentication to your Active Directory (AD) via LDAP you must configure the LDAP connection to the domain controller.

1. Click the **Directory Integration** icon.
2. On the Settings tab, select the **Use specific LDAP configuration** radio button.

   <center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Click **Edit**.
4. In the Edit LDAP Configuration dialog box, populate the fields with the information required to connect to the AD domain controller. Descriptions of the fields are included in the Azure Multi-Factor Authentication Server help file.
5. Test the LDAP connection by clicking the **Test** button.

   <center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. If the LDAP connection test was successful, click **OK**.

### <a name="configure-company-settings"></a>Configure company settings
1. Next, click the **Company Settings** icon and select the **Username Resolution** tab.
2. Select the **Use LDAP unique identifier attribute for matching usernames** radio button.
3. If users enter their username in “domain\username” format, the Server needs to be able to strip the domain off the username when it creates the LDAP query. That can be done through a registry setting.
4. Open the registry editor and go to HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive Networks/PhoneFactor on a 64-bit server. If on a 32-bit server, take the “Wow6432Node” out of the path. Create a DWORD registry key called “UsernameCxz_stripPrefixDomain” and set the value to 1. Azure Multi-Factor Authentication is now securing the AD FS proxy.

Ensure that users have been imported from Active Directory into the Server. See the [Trusted IPs section](#trusted-ips) if you would like to whitelist internal IP addresses so that two-step verification is not required when signing in to the website from those locations.

<center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 Direct without a proxy
You can secure AD FS when the AD FS proxy is not used. Install the Azure Multi-Factor Authentication Server on the AD FS server and configure the Server per the following steps:

1. Within the Azure Multi-Factor Authentication Server, click the **IIS Authentication** icon in the left menu.
2. Click the **HTTP** tab.
3. Click **Add**.
4. In the Add Base URL dialogue box, enter the URL for the AD FS website where HTTP authentication is performed (like https://sso.domain.com/adfs/ls/auth/integrated) into the Base URL field. Then, enter an Application name (optional). The Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.
5. If desired, adjust the Idle timeout and Maximum session times.
6. Check the **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to two-step verification. If a significant number of users have not yet been imported into the Server and/or will be exempt from two-step verification, leave the box unchecked. 
7. Check the cookie cache box if desired.

   <center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Click **OK**.
9. Click the **Native Module** tab and select the server, the website (like “Default Web Site”), or the AD FS application (like “ls” under “adfs”) to enable the IIS plug-in at the desired level.
10. Click the **Enable IIS authentication** box at the top of the screen. 

Azure Multi-Factor Authentication is now securing AD FS.

Ensure that users have been imported from Active Directory into the Server. See the Trusted IPs section if you would like to whitelist internal IP addresses so that two-step verification is not required when signing in to the website from those locations.

## <a name="trusted-ips"></a>Trusted IPs
Trusted IPs allow users to bypass Azure Multi-Factor Authentication for website requests originating from specific IP addresses or subnets. For example, you may want to exempt users from two-step verification when they sign in from the office. For this, you would specify the office subnet as a Trusted IPs entry.

### <a name="to-configure-trusted-ips"></a>To configure trusted IPs
1. In the IIS Authentication section, click the **Trusted IPs** tab.
2. Click the **Add…** button.
3. When the Add Trusted IPs dialog box appears, select one of the **Single IP**, **IP range**, or **Subnet** radio buttons.
4. Enter the IP address, range of IP addresses, or subnet that should be whitelisted. If entering a subnet, select the appropriate Netmask and click the **OK** button. The trusted IP has now been added.

<center>![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>







