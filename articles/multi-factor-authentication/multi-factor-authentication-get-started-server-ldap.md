---
title: LDAP Authentication and Azure MFA Server | Microsoft Docs
description: This is the Azure Multi-factor authentication page that will assist in deploying LDAP Authentication and Azure Multi-Factor Authentication Server.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/03/2017
ms.author: kgremban
ms.openlocfilehash: 519be8d368362c3af31c10dafa7180229f6e9a37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550433"
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>LDAP Authentication and Azure Multi-Factor Authentication Server
By default, the Azure Multi-Factor Authentication Server is configured to import or synchronize users from Active Directory. However, it can be configured to bind to different LDAP directories, such as an ADAM directory, or specific Active Directory domain controller. When connected to a directory via LDAP, the Azure Multi-Factor Authentication Server can be configured to act as an LDAP proxy to perform authentications. It also allows for the use of LDAP bind as a RADIUS target, for pre-authentication of users with IIS Authentication, or for primary authentication in the Azure MFA user portal.

To use Azure Multi-Factor Authentication as an LDAP proxy, insert the Azure Multi-Factor Authentication Server between the LDAP client (e.g. VPN appliance, application) and the LDAP directory server. The Azure Multi-Factor Authentication Server must be configured to communicate with both the client servers and the LDAP directory. In this configuration, the Azure Multi-Factor Authentication Server accepts LDAP requests from client servers and applications and forwards them to the target LDAP directory server to validate the primary credentials. If the response from the LDAP directory shows that they primary credentials are valid, Azure Multi-Factor Authentication performs a second identity verification and sends a response back to the LDAP client. The entire authentication succeeds only if both the LDAP server authentication and the second-step verification succeed.

## <a name="ldap-authentication-configuration"></a>LDAP Authentication Configuration
To configure LDAP authentication, install the Azure Multi-Factor Authentication Server on a Windows server. Use the following procedure:

### <a name="add-an-ldap-client"></a>Add an LDAP client

1. In the Azure Multi-Factor Authentication Server select the LDAP Authentication icon in the left menu.
2. Check the **Enable LDAP Authentication** checkbox.

        ![LDAP Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. On the Clients tab, change the TCP port and SSL port if the Azure Multi-Factor Authentication LDAP service should bind to non-standard ports to listen for LDAP requests.
4. If you plan to use LDAPS from the client to the Azure Multi-Factor Authentication Server, an SSL certificate must be installed on the server that the Server is running on. Click the **Browse…** button next to the SSL certificate box and select the installed certificate that will be used for the secure connection.
5. Click **Add…**
6. In the Add LDAP Client dialog box, enter the IP address of the appliance, server, or application that will authenticate to the Server and an Application name (optional). The Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.
7. Check the **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to two-step verification. If a significant number of users have not yet been imported into the Server and/or will be exempt from two-step verification, leave the box unchecked. See the help file for additional information on this feature.

Repeat these steps to add additional LDAP clients.

### <a name="configure-the-ldap-directory-connection"></a>Configure the LDAP directory connection

When the Azure Multi-Factor Authentication is configured to receive LDAP authentications, it must proxy those authentications to the LDAP directory. Therefore, the Target tab only displays a single, grayed out option to use an LDAP target.

1. To configure the LDAP directory connection, click the **Directory Integration** icon.
2. On the Settings tab, select the **Use specific LDAP configuration** radio button.
3. Select **Edit…**
4. In the Edit LDAP Configuration dialog box, populate the fields with the information required to connect to the LDAP directory. Descriptions of the fields are included in the Azure Multi-Factor Authentication Server help file.

    ![Directory Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Test the LDAP connection by clicking the **Test** button.
6. If the LDAP connection test was successful, click the **OK** button.
7. Click the **Filters** tab. The Server is pre-configured to load containers, security groups, and users from Active Directory. If binding to a different LDAP directory, you probably need to edit the filters displayed. Click the **Help** link for more information on filters.
8. Click the **Attributes** tab. The Server is pre-configured to map attributes from Active Directory.
9. If you're binding to a different LDAP directory or to change the pre-configured attribute mappings, click **Edit…**
10. In the Edit Attributes dialog box, modify the LDAP attribute mappings for your directory. Attribute names can be typed in or selected by clicking the **…** button next to each field. Click the **Help** link for more information on attributes.
11. Click the **OK** button.
12. Click the **Company Settings** icon and select the **Username Resolution** tab.
13. If you're connecting to Active Directory from a domain-joined server, leave the **Use Windows security identifiers (SIDs) for matching usernames** radio button selected. Otherwise, select the **Use LDAP unique identifier attribute for matching usernames** radio button. 

When the **Use LDAP unique identifier attribute for matching usernames** radio button is selected, the Azure Multi-Factor Authentication Server attempts to resolve each username to a unique identifier in the LDAP directory. An LDAP search is performed on the Username attributes defined in the Directory Integration -> Attributes tab. When a user authenticates, the username is resolved to the unique identifier in the LDAP directory and the unique identifier is used for matching the user in the Azure Multi-Factor Authentication data file. This allows for case-insensitive comparisons, as well as long and short username formats.

After you complete these steps, the MFA Server begins listening on the configured ports for LDAP access requests from the configured clients, and is set to proxy those requests to the LDAP directory for authentication.

## <a name="ldap-client-configuration"></a>LDAP Client Configuration
To configure the LDAP client, use the guidelines:

* Configure your appliance, server, or application to authenticate via LDAP to the Azure Multi-Factor Authentication Server as though it were your LDAP directory. Use the same settings that you would normally use to connect directly to your LDAP directory, except for the server name or IP address, which will be that of the Azure Multi-Factor Authentication Server.
* Configure the LDAP timeout to 30-60 seconds so that there is time to validate the user’s credentials with the LDAP directory, perform the second-step verification, receive their response, and then respond to the LDAP access request.
* If using LDAPS, the appliance or server making the LDAP queries must trust the SSL certificate installed on the Azure Multi-Factor Authentication Server.



