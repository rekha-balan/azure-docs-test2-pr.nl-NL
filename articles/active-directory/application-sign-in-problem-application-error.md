---
title: Error on an application's page after signing in | Microsoft Docs
description: How to resolve issues with Azure AD sign in when the application itself emits an error
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
ms.openlocfilehash: b92c86a82205d9840168a606abc66420f0208a1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669383"
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Error on an application's page after signing in

In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow. In this scenario, the application is not accepting the response issue by Azure AD.

There are some possible reasons why the application didn’t accept the response from Azure AD. If the error in the application is not clear enough to know what is missing in the response, then:

-   If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.

-   Share the SAML response with the application vendor to know what is missing.

## <a name="missing-attributes-in-the-saml-response"></a>Missing attributes in the SAML response

To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

   * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to configure single sign-on.

7.  Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.

8.  click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.

   To add an attribute:

   * click **Add attribute**. Enter the **Name** and the select the **Value** from the dropdown.

   * Click **Save.** You see the new attribute in the table.

9.  Save the configuration.

Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a>The application expects a different User Identifier value or format

The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a>Add an attribute in the Azure AD application configuration:

To change the User Identifier value, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

   * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to configure single sign-on.

7.  Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.

8.  Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.

## <a name="change-entityid-user-identifier-format"></a>Change EntityID (User Identifier) format

If the application expects another format for the EntityID attribute. Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.

Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest. For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a>The application expects a different signature method for the SAML response

To change what parts of the SAML token are digitally signed by Azure Active Directory. Follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

  * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to configure single sign-on.

7.  Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.

8.  click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.

9.  Select the appropriate **Signing Option** expected by the application:

  * Sign SAML response

  * Sign SAML response and assertion

  * Sign SAML assertion

Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a>The application expects the signing algorithm to be SHA-1

By default, Azure AD signs the SAML token using the most security algorithm. Changing the sign algorithm to SHA-1 is not recommended unless required by the application.

To change the signing algorithm, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

   * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to configure single sign-on.

7.  Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.

8.  click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.

9.  Select SHA-1, in the **Signing Algorithm**.

Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.

## <a name="next-steps"></a>Next steps
[How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
