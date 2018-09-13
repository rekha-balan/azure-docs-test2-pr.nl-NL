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
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="1b38f-103">How to get AppSource Certified for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b38f-103">How to get AppSource Certified for Azure Active Directory</span></span>

<span data-ttu-id="1b38f-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span><span class="sxs-lookup"><span data-stu-id="1b38f-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="1b38f-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b38f-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1b38f-106">The sign-in process must use the [OpenID Connect](v1-protocols-openid-connect-code.md) or [OAuth 2.0](v1-protocols-oauth-code.md) protocols.</span><span class="sxs-lookup"><span data-stu-id="1b38f-106">The sign-in process must use the [OpenID Connect](v1-protocols-openid-connect-code.md) or [OAuth 2.0](v1-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="1b38f-107">SAML integration is not accepted for AppSource certification.</span><span class="sxs-lookup"><span data-stu-id="1b38f-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="1b38f-108">Guides and code samples</span><span class="sxs-lookup"><span data-stu-id="1b38f-108">Guides and code samples</span></span>

<span data-ttu-id="1b38f-109">If you want to learn about how to integrate your application with Azure AD using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](azure-ad-developers-guide.md#get-started "Get Started with Azure AD for developers").</span><span class="sxs-lookup"><span data-stu-id="1b38f-109">If you want to learn about how to integrate your application with Azure AD using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](azure-ad-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="1b38f-110">Multi-tenant applications</span><span class="sxs-lookup"><span data-stu-id="1b38f-110">Multi-tenant applications</span></span>

<span data-ttu-id="1b38f-111">A *multi-tenant application* is an application that accepts sign-ins from users from any company or organization that have Azure AD without requiring a separate instance, configuration, or deployment.</span><span class="sxs-lookup"><span data-stu-id="1b38f-111">A *multi-tenant application* is an application that accepts sign-ins from users from any company or organization that have Azure AD without requiring a separate instance, configuration, or deployment.</span></span> <span data-ttu-id="1b38f-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span><span class="sxs-lookup"><span data-stu-id="1b38f-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="1b38f-113">To enable multi-tenancy on your application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1b38f-113">To enable multi-tenancy on your application, follow these steps:</span></span>
1. <span data-ttu-id="1b38f-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).</span><span class="sxs-lookup"><span data-stu-id="1b38f-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).</span></span> <span data-ttu-id="1b38f-115">By default, applications created in the Azure portal are configured as *[single-tenant](#single-tenant-applications)*.</span><span class="sxs-lookup"><span data-stu-id="1b38f-115">By default, applications created in the Azure portal are configured as *[single-tenant](#single-tenant-applications)*.</span></span>
1. <span data-ttu-id="1b38f-116">Update your code to send requests to the `common` endpoint.</span><span class="sxs-lookup"><span data-stu-id="1b38f-116">Update your code to send requests to the `common` endpoint.</span></span> <span data-ttu-id="1b38f-117">To do this, update the endpoint from `https://login.microsoftonline.com/{yourtenant}` to `https://login.microsoftonline.com/common*`.</span><span class="sxs-lookup"><span data-stu-id="1b38f-117">To do this, update the endpoint from `https://login.microsoftonline.com/{yourtenant}` to `https://login.microsoftonline.com/common*`.</span></span>
1. <span data-ttu-id="1b38f-118">For some platforms, like ASP .NET, you need also to update your code to accept multiple issuers.</span><span class="sxs-lookup"><span data-stu-id="1b38f-118">For some platforms, like ASP .NET, you need also to update your code to accept multiple issuers.</span></span>

<span data-ttu-id="1b38f-119">For more information about multi-tenancy, see [How to sign in any Azure Active Directory (Azure AD) user using the multi-tenant application pattern](howto-convert-app-to-be-multi-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1b38f-119">For more information about multi-tenancy, see [How to sign in any Azure Active Directory (Azure AD) user using the multi-tenant application pattern](howto-convert-app-to-be-multi-tenant.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="1b38f-120">Single-tenant applications</span><span class="sxs-lookup"><span data-stu-id="1b38f-120">Single-tenant applications</span></span>

<span data-ttu-id="1b38f-121">A *single-tenant application* is an application that only accepts sign-ins from users of a defined Azure AD instance.</span><span class="sxs-lookup"><span data-stu-id="1b38f-121">A *single-tenant application* is an application that only accepts sign-ins from users of a defined Azure AD instance.</span></span> <span data-ttu-id="1b38f-122">External users (including work or school accounts from other organizations, or personal accounts) can sign in to a single-tenant application after adding each user as a guest account to the Azure AD instance that the application is registered.</span><span class="sxs-lookup"><span data-stu-id="1b38f-122">External users (including work or school accounts from other organizations, or personal accounts) can sign in to a single-tenant application after adding each user as a guest account to the Azure AD instance that the application is registered.</span></span> 

<span data-ttu-id="1b38f-123">You can add users as guest accounts to Azure AD through the [Azure AD B2B collaboration](../b2b/what-is-b2b.md) and you can do this [programatically](../../active-directory-b2c/code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1b38f-123">You can add users as guest accounts to Azure AD through the [Azure AD B2B collaboration](../b2b/what-is-b2b.md) and you can do this [programatically](../../active-directory-b2c/code-samples.md).</span></span> <span data-ttu-id="1b38f-124">When using B2B, users can create a self-service portal that does not require an invitation to sign in.</span><span class="sxs-lookup"><span data-stu-id="1b38f-124">When using B2B, users can create a self-service portal that does not require an invitation to sign in.</span></span> <span data-ttu-id="1b38f-125">For more info, see [Self-service portal for Azure AD B2B collaboration sign-up](https://docs.microsoft.com/azure/active-directory/b2b/self-service-portal).</span><span class="sxs-lookup"><span data-stu-id="1b38f-125">For more info, see [Self-service portal for Azure AD B2B collaboration sign-up](https://docs.microsoft.com/azure/active-directory/b2b/self-service-portal).</span></span>

<span data-ttu-id="1b38f-126">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span><span class="sxs-lookup"><span data-stu-id="1b38f-126">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>

## <a name="appsource-trial-experiences"></a><span data-ttu-id="1b38f-127">AppSource trial experiences</span><span class="sxs-lookup"><span data-stu-id="1b38f-127">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="1b38f-128">Free trial (customer-led trial experience)</span><span class="sxs-lookup"><span data-stu-id="1b38f-128">Free trial (customer-led trial experience)</span></span> 

<span data-ttu-id="1b38f-129">The customer-led trial is the experience that AppSource recommends as it offers a single-click access to your application.</span><span class="sxs-lookup"><span data-stu-id="1b38f-129">The customer-led trial is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="1b38f-130">Below an illustration of how this experience looks like:</span><span class="sxs-lookup"><span data-stu-id="1b38f-130">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="1b38f-131">User finds your application in AppSource Web Site</span><span class="sxs-lookup"><span data-stu-id="1b38f-131">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="1b38f-132">Selects ‘Free trial’ option</span><span class="sxs-lookup"><span data-stu-id="1b38f-132">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="1b38f-133">AppSource redirects user to a URL in your web site</span><span class="sxs-lookup"><span data-stu-id="1b38f-133">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="1b38f-134">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span><span class="sxs-lookup"><span data-stu-id="1b38f-134">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="1b38f-135">User is redirected to Microsoft Sign-in page</span><span class="sxs-lookup"><span data-stu-id="1b38f-135">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="1b38f-136">User provides credentials to sign in</span><span class="sxs-lookup"><span data-stu-id="1b38f-136">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="1b38f-137">User gives consent for your application</span><span class="sxs-lookup"><span data-stu-id="1b38f-137">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="1b38f-138">Sign-in completes and user is redirected back to your web site</span><span class="sxs-lookup"><span data-stu-id="1b38f-138">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="1b38f-139">User starts the free trial</span><span class="sxs-lookup"><span data-stu-id="1b38f-139">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="1b38f-140">Contact me (partner-led trial experience)</span><span class="sxs-lookup"><span data-stu-id="1b38f-140">Contact me (partner-led trial experience)</span></span>

<span data-ttu-id="1b38f-141">You can use the partner trial experience when a manual or a long-term operation needs to happen to provision the user/company--for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span><span class="sxs-lookup"><span data-stu-id="1b38f-141">You can use the partner trial experience when a manual or a long-term operation needs to happen to provision the user/company--for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="1b38f-142">In this case, after the user selects the **Request Trial** button and fills out a form, AppSource sends you the user's contact information.</span><span class="sxs-lookup"><span data-stu-id="1b38f-142">In this case, after the user selects the **Request Trial** button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="1b38f-143">When you receive this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span><span class="sxs-lookup"><span data-stu-id="1b38f-143">When you receive this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="1b38f-144">User finds your application in AppSource web site</span><span class="sxs-lookup"><span data-stu-id="1b38f-144">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="1b38f-145">Selects ‘Contact Me’ option</span><span class="sxs-lookup"><span data-stu-id="1b38f-145">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="1b38f-146">Fills out a form with contact information</span><span class="sxs-lookup"><span data-stu-id="1b38f-146">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="1b38f-147">You receive user information</span><span class="sxs-lookup"><span data-stu-id="1b38f-147">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="1b38f-148">Setup environment</span><span class="sxs-lookup"><span data-stu-id="1b38f-148">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="1b38f-149">Contact user with trial info</span><span class="sxs-lookup"><span data-stu-id="1b38f-149">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="1b38f-150">You receive user's information and setup trial instance</span><span class="sxs-lookup"><span data-stu-id="1b38f-150">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="1b38f-151">You send the hyperlink to access your application to the user</span><span class="sxs-lookup"><span data-stu-id="1b38f-151">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="1b38f-152">User accesses your application and complete the single-sign-on process</span><span class="sxs-lookup"><span data-stu-id="1b38f-152">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="1b38f-153">User gives consent for your application</span><span class="sxs-lookup"><span data-stu-id="1b38f-153">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="1b38f-154">Sign-in completes and user is redirected back to your web site</span><span class="sxs-lookup"><span data-stu-id="1b38f-154">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="1b38f-155">User starts the free trial</span><span class="sxs-lookup"><span data-stu-id="1b38f-155">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="1b38f-156">More information</span><span class="sxs-lookup"><span data-stu-id="1b38f-156">More information</span></span>

<span data-ttu-id="1b38f-157">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="1b38f-157">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="1b38f-158">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1b38f-158">Next Steps</span></span>

- <span data-ttu-id="1b38f-159">For more information on building applications that support Azure AD sign-ins, see [Authentication scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="1b38f-159">For more information on building applications that support Azure AD sign-ins, see [Authentication scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios).</span></span>
- <span data-ttu-id="1b38f-160">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="1b38f-160">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="1b38f-161">Get support</span><span class="sxs-lookup"><span data-stu-id="1b38f-161">Get support</span></span>

<span data-ttu-id="1b38f-162">For Azure AD integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource) with the community to provide support.</span><span class="sxs-lookup"><span data-stu-id="1b38f-162">For Azure AD integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource) with the community to provide support.</span></span> 

<span data-ttu-id="1b38f-163">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span><span class="sxs-lookup"><span data-stu-id="1b38f-163">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="1b38f-164">Make sure that your questions or comments are tagged with [`[azure-active-directory]` and `[appsource]`](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource).</span><span class="sxs-lookup"><span data-stu-id="1b38f-164">Make sure that your questions or comments are tagged with [`[azure-active-directory]` and `[appsource]`](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource).</span></span>

<span data-ttu-id="1b38f-165">Use the following comments section to provide feedback and help us refine and shape our content.</span><span class="sxs-lookup"><span data-stu-id="1b38f-165">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]:authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]:authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: azure-ad-developers-guide.md
[AAD-Howto-Multitenant-Overview]: howto-convert-app-to-be-multi-tenant.md
[AAD-QuickStart-Web-Apps]: azure-ad-developers-guide.md#get-started


<!--Image references-->
