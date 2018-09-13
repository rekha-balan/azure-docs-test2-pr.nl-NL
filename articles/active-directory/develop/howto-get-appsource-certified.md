---
title: How to get AppSource certified for Azure Active Directory| Microsoft Docs
description: Details on how to get your application AppSource certified for Azure Active Directory.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/21/2018
ms.author: celested
ms.reviewer: andret
ms.custom: aaddev
ms.openlocfilehash: a2876ccdfe073a3c642304a1381faf77ae4a7d90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870098"
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a>How to get AppSource Certified for Azure Active Directory

[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).

To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory (Azure AD). The sign-in process must use the [OpenID Connect](v1-protocols-openid-connect-code.md) or [OAuth 2.0](v1-protocols-oauth-code.md) protocols. SAML integration is not accepted for AppSource certification.

## <a name="guides-and-code-samples"></a>Guides and code samples

If you want to learn about how to integrate your application with Azure AD using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](azure-ad-developers-guide.md#get-started "Get Started with Azure AD for developers").

## <a name="multi-tenant-applications"></a>Multi-tenant applications

A *multi-tenant application* is an application that accepts sign-ins from users from any company or organization that have Azure AD without requiring a separate instance, configuration, or deployment. AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.

To enable multi-tenancy on your application, follow these steps:
1. Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps). By default, applications created in the Azure portal are configured as *[single-tenant](#single-tenant-applications)*.
1. Update your code to send requests to the `common` endpoint. To do this, update the endpoint from `https://login.microsoftonline.com/{yourtenant}` to `https://login.microsoftonline.com/common*`.
1. For some platforms, like ASP .NET, you need also to update your code to accept multiple issuers.

For more information about multi-tenancy, see [How to sign in any Azure Active Directory (Azure AD) user using the multi-tenant application pattern](howto-convert-app-to-be-multi-tenant.md).

### <a name="single-tenant-applications"></a>Single-tenant applications

A *single-tenant application* is an application that only accepts sign-ins from users of a defined Azure AD instance. External users (including work or school accounts from other organizations, or personal accounts) can sign in to a single-tenant application after adding each user as a guest account to the Azure AD instance that the application is registered. 

You can add users as guest accounts to Azure AD through the [Azure AD B2B collaboration](../b2b/what-is-b2b.md) and you can do this [programatically](../../active-directory-b2c/code-samples.md). When using B2B, users can create a self-service portal that does not require an invitation to sign in. For more info, see [Self-service portal for Azure AD B2B collaboration sign-up](https://docs.microsoft.com/azure/active-directory/b2b/self-service-portal).

Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/free trial experience that AppSource recommends, enable multi-tenancy on your application instead.

## <a name="appsource-trial-experiences"></a>AppSource trial experiences

### <a name="free-trial-customer-led-trial-experience"></a>Free trial (customer-led trial experience) 

The customer-led trial is the experience that AppSource recommends as it offers a single-click access to your application. Below an illustration of how this experience looks like:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>User finds your application in AppSource Web Site</li><li>Selects ‘Free trial’ option</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource redirects user to a URL in your web site</li><li>Your web site starts the <i>single-sign-on</i> process automatically (on page load)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>User is redirected to Microsoft Sign-in page</li><li>User provides credentials to sign in</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>User gives consent for your application</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Sign-in completes and user is redirected back to your web site</li><li>User starts the free trial</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Contact me (partner-led trial experience)

You can use the partner trial experience when a manual or a long-term operation needs to happen to provision the user/company--for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete. In this case, after the user selects the **Request Trial** button and fills out a form, AppSource sends you the user's contact information. When you receive this information, you then provision the environment and send the instructions to the user on how to access the trial experience:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>User finds your application in AppSource web site</li><li>Selects ‘Contact Me’ option</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Fills out a form with contact information</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>You receive user information</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Setup environment</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Contact user with trial info</td>
        </tr>
        </table><br/><br/>
        <ul><li>You receive user's information and setup trial instance</li><li>You send the hyperlink to access your application to the user</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>User accesses your application and complete the single-sign-on process</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>User gives consent for your application</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Sign-in completes and user is redirected back to your web site</li><li>User starts the free trial</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>More information

For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Next Steps

- For more information on building applications that support Azure AD sign-ins, see [Authentication scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios).
- For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Get support

For Azure AD integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource) with the community to provide support. 

We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before. Make sure that your questions or comments are tagged with [`[azure-active-directory]` and `[appsource]`](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource).

Use the following comments section to provide feedback and help us refine and shape our content.

<!--Reference style links -->
[AAD-Auth-Scenarios]:authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]:authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: azure-ad-developers-guide.md
[AAD-Howto-Multitenant-Overview]: howto-convert-app-to-be-multi-tenant.md
[AAD-QuickStart-Web-Apps]: azure-ad-developers-guide.md#get-started


<!--Image references-->