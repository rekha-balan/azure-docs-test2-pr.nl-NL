---
title: Admin guide for the Azure Active Directory SSO plug-in | Microsoft Docs
description: Learn how to configure single sign-on between Azure Active Directory and Jira/Confluence.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4b663047-7f88-443b-97bd-54224b232815
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: jeedes
ms.openlocfilehash: 7cbe0d0ea3bbbd60b7cd2dc88ef249c4380083a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967428"
---
# <a name="admin-guide-for-the-azure-active-directory-sso-plug-in"></a>Admin guide for the Azure Active Directory SSO plug-in

## <a name="overview"></a>Overview

The Azure Active Directory (Azure AD) single sign-on (SSO) plug-in enables Microsoft Azure AD customers to use their work or school account for signing in to Atlassian Jira and Confluence Server-based products. It implements SAML 2.0-based SSO.

## <a name="how-it-works"></a>How it works

When users want to sign in to the Atlassian Jira or Confluence application, they see the **Login with Azure AD** button on the sign-in page. When they select it, they're required to sign in by using the Azure AD organization sign-in page (that is, their work or school account).

After the users are authenticated, they should be able to sign in to the application. If they are already authenticated with the ID and password for their work or school account, then they directly sign in to the application. 

Sign-in works across Jira and Confluence. If users are signed in to the Jira application and Confluence is opened in the same browser window, they don't have to provide the credentials for the other app. 

Users can also get to the Atlassian product through My Apps under the work or school account. They should be signed in without being asked for credentials.

> [!NOTE]
> User provisioning is not done through the plug-in.

## <a name="audience"></a>Audience

Jira and Confluence admins can use the plug-in to enable SSO by using Azure AD.

## <a name="assumptions"></a>Assumptions

* Jira and Confluence instances are HTTPS enabled.
* Users are already created in Jira or Confluence.
* Users have roles assigned in Jira or Confluence.
* Admins have access to information required to configure the plug-in.
* Jira or Confluence is available outside the company network as well.
* The plug-in works with only the on-premises version of Jira and Confluence.

## <a name="prerequisites"></a>Prerequisites

Note the following information before you install the plug-in:

* Jira and Confluence are installed on a Windows 64-bit version.
* Jira and Confluence versions are HTTPS enabled.
* Jira and Confluence are available on the internet.
* Admin credentials are in place for Jira and Confluence.
* Admin credentials are in place for Azure AD.
* WebSudo is disabled in Jira and Confluence.

## <a name="supported-versions-of-jira-and-confluence"></a>Supported versions of Jira and Confluence

The plug-in supports the following versions of Jira and Confluence:

* Jira Core and Software: 6.0 to 7.8
* Jira Service Desk: 3.0 to 3.2
* Confluence: 5.0 to 5.10

## <a name="installation"></a>Installation

To install the plug-in, follow these steps:

1. Sign in to your Jira or Confluence instance as an admin.

2. Go to the Jira/Confluence administration console and select **Add-ons**.

3. From the Atlassian Marketplace, search for **Microsoft SAML SSO Plugin**.

   The appropriate version of the plug-in appears in the search results.

4. Select the plug-in, and the Universal Plug-in Manager (UPM) installs it.

After the plug-in is installed, it appears in the **User Installed Add-ons** section of **Manage Add-ons**.

## <a name="plug-in-configuration"></a>Plug-in configuration

Before you start using the plug-in, you must configure it. Select the plug-in, select the **Configure** button, and provide the configuration details.

The following image shows the configuration screen in both Jira and Confluence:

![Plug-in configuration screen](./media/ms-confluence-jira-plugin-adminguide/jira.png)

*   **Metadata URL**: The URL to get federation metadata from Azure AD.

*   **Identifiers**: The URL that Azure AD uses to validate the source of the request. It maps to the **Identifier** element in Azure AD. The plug-in automatically derives this URL as https://*<domain:port>*/.

*   **Reply URL**: The reply URL in your identity provider (IdP) that initiates the SAML sign-in. It maps to the **Reply URL** element in Azure AD. The plug-in automatically derives this URL as https://*<domain:port>*/plugins/servlet/saml/auth.

*   **Sign On URL**: The sign-on URL in your IdP that initiates the SAML sign-in. It maps to the **Sign On** element in Azure AD. The plug-in automatically derives this URL as https://*<domain:port>*/plugins/servlet/saml/auth.

*   **IdP Entity ID**: The entity ID that your IdP uses. This box is populated when the metadata URL is resolved.

*   **Login URL**: The sign-in URL from your IdP. This box is populated from Azure AD when the metadata URL is resolved.

*   **Logout URL**: The logout URL from your IdP. This box is populated from Azure AD when the metadata URL is resolved.

*   **X.509 Certificate**: Your IdP’s X.509 certificate. This box is populated from Azure AD when the metadata URL is resolved.

*   **Login Button Name**: The name of the sign-in button that your organization wants users to see on the sign-in page.

*   **SAML User ID Locations**: The location where the Jira or Confluence user ID is expected in the SAML response. It can be in **NameID** or in a custom attribute name.

*   **Attribute Name**: The name of the attribute where the user ID is expected.

*   **Enable Home Realm Discovery**: The selection to make if the company is using Active Directory Federation Services (AD FS)-based sign-in.

*   **Domain Name**: The domain name if sign-in is AD FS based.

*   **Enable Single Signout**: The selection to make if you want to sign out from Azure AD when a user signs out from Jira or Confluence.

## <a name="troubleshooting"></a>Troubleshooting

* **You're getting multiple certificate errors**: Sign in to Azure AD and remove the multiple certificates that are available against the app. Ensure that only one certificate is present.

* **A certificate is about to expire in Azure AD**: Add-ons take care of automatic rollover of the certificate. When a certificate is about to expire, a new certificate should be marked active and unused certificates should be deleted. When a user tries to sign in to Jira in this scenario, the plug-in fetches and saves the new certificate.

* **You want to disable WebSudo (disable the secure administrator session)**:

  * For Jira, secure administrator sessions (that is, password confirmation before accessing administration functions) are enabled by default. If you want to remove this ability in your Jira instance, specify the following line in your jira-config.properties file: `ira.websudo.is.disabled = true`

  * For Confluence, follow the steps on the [Confluence support site](https://confluence.atlassian.com/doc/configuring-secure-administrator-sessions-218269595.html).

* **Fields that are supposed to be populated by the metadata URL are not getting populated**:

  * Check if the URL is correct. Check if you have mapped the correct tenant and app ID.

  * Enter the URL in a browser and see if you receive the federation metadata XML.

* **There's an internal server error**: Review the logs in the log directory of the installation. If you're getting the error when the user is trying to sign in by using Azure AD SSO, you can share the logs with the support team.

* **There's a "User ID not found" error when the user tries to sign in**: Create the user ID in Jira or Confluence.

* **There's an "App not found" error in Azure AD**: See if the appropriate URL is mapped to the app in Azure AD.

* **You need support**: Reach out to the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>). The team responds in 24-48 business hours.

  You can also raise a support ticket with Microsoft through the Azure portal channel.