---
title: List your application in the Azure Active Directory application gallery | Microsoft Docs
description: Learn how to list an application that supports single sign-on in the Azure Active Directory app gallery
services: active-directory
documentationcenter: dev-center-name
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/31/2018
ms.author: celested
ms.reviewer: elisol, bryanla
ms.custom: aaddev
ms.openlocfilehash: d5c00e9df9c1bfee0c665cafc763c52a36f98052
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857349"
---
# <a name="list-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="77861-103">List your application in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="77861-103">List your application in the Azure Active Directory application gallery</span></span>


##  <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="77861-104">What is the Azure AD application gallery?</span><span class="sxs-lookup"><span data-stu-id="77861-104">What is the Azure AD application gallery?</span></span>

<span data-ttu-id="77861-105">Azure Active Directory (Azure AD) is a cloud-based identity service.</span><span class="sxs-lookup"><span data-stu-id="77861-105">Azure Active Directory (Azure AD) is a cloud-based identity service.</span></span> <span data-ttu-id="77861-106">The [Azure AD application gallery](https://azure.microsoft.com/marketplace/active-directory/all/) is in the Azure Marketplace app store, where all application connectors are published for single sign-on and user provisioning.</span><span class="sxs-lookup"><span data-stu-id="77861-106">The [Azure AD application gallery](https://azure.microsoft.com/marketplace/active-directory/all/) is in the Azure Marketplace app store, where all application connectors are published for single sign-on and user provisioning.</span></span> <span data-ttu-id="77861-107">Customers who use Azure AD as an identity provider find the different SaaS application connectors published here.</span><span class="sxs-lookup"><span data-stu-id="77861-107">Customers who use Azure AD as an identity provider find the different SaaS application connectors published here.</span></span> <span data-ttu-id="77861-108">IT administrators add connectors from the app gallery, and then configure and use the connectors for single sign-on and provisioning.</span><span class="sxs-lookup"><span data-stu-id="77861-108">IT administrators add connectors from the app gallery, and then configure and use the connectors for single sign-on and provisioning.</span></span> <span data-ttu-id="77861-109">Azure AD supports all major federation protocols for single sign-on, including SAML 2.0, OpenID Connect, OAuth, and WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="77861-109">Azure AD supports all major federation protocols for single sign-on, including SAML 2.0, OpenID Connect, OAuth, and WS-Fed.</span></span>

## <a name="what-are-the-benefits-of-listing-an-application-in-the-gallery"></a><span data-ttu-id="77861-110">What are the benefits of listing an application in the gallery?</span><span class="sxs-lookup"><span data-stu-id="77861-110">What are the benefits of listing an application in the gallery?</span></span>

*  <span data-ttu-id="77861-111">Customers find the best possible single sign-on experience.</span><span class="sxs-lookup"><span data-stu-id="77861-111">Customers find the best possible single sign-on experience.</span></span>

*  <span data-ttu-id="77861-112">Configuration of the application is simple and minimal.</span><span class="sxs-lookup"><span data-stu-id="77861-112">Configuration of the application is simple and minimal.</span></span>

*  <span data-ttu-id="77861-113">A quick search finds your application in the gallery.</span><span class="sxs-lookup"><span data-stu-id="77861-113">A quick search finds your application in the gallery.</span></span>

*  <span data-ttu-id="77861-114">Free, Basic, and Premium Azure AD customers can all use this integration.</span><span class="sxs-lookup"><span data-stu-id="77861-114">Free, Basic, and Premium Azure AD customers can all use this integration.</span></span>

*  <span data-ttu-id="77861-115">Mutual customers get a step-by-step configuration tutorial.</span><span class="sxs-lookup"><span data-stu-id="77861-115">Mutual customers get a step-by-step configuration tutorial.</span></span>

*  <span data-ttu-id="77861-116">Customers who use SCIM can use provisioning for the same app.</span><span class="sxs-lookup"><span data-stu-id="77861-116">Customers who use SCIM can use provisioning for the same app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77861-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77861-117">Prerequisites</span></span>

- <span data-ttu-id="77861-118">For Federated applications (Open ID and SAML/WS-Fed), the application must support the SaaS model for getting listed in Azure AD gallery.</span><span class="sxs-lookup"><span data-stu-id="77861-118">For Federated applications (Open ID and SAML/WS-Fed), the application must support the SaaS model for getting listed in Azure AD gallery.</span></span> <span data-ttu-id="77861-119">The enterprise gallery applications should support multiple customer configurations and not any specific customer.</span><span class="sxs-lookup"><span data-stu-id="77861-119">The enterprise gallery applications should support multiple customer configurations and not any specific customer.</span></span>

- <span data-ttu-id="77861-120">For Open ID Connect, the application should be multi-tenanted  and [Azure AD consent framework](quickstart-v1-integrate-apps-with-azure-ad.md#overview-of-the-consent-framework) should be properly implemented for the application.</span><span class="sxs-lookup"><span data-stu-id="77861-120">For Open ID Connect, the application should be multi-tenanted  and [Azure AD consent framework](quickstart-v1-integrate-apps-with-azure-ad.md#overview-of-the-consent-framework) should be properly implemented for the application.</span></span> <span data-ttu-id="77861-121">The user can send the login request to a common endpoint so that any customer can provide consent to the application.</span><span class="sxs-lookup"><span data-stu-id="77861-121">The user can send the login request to a common endpoint so that any customer can provide consent to the application.</span></span> <span data-ttu-id="77861-122">You can control user access based on the tenant ID and the user's UPN received in the token.</span><span class="sxs-lookup"><span data-stu-id="77861-122">You can control user access based on the tenant ID and the user's UPN received in the token.</span></span>

- <span data-ttu-id="77861-123">For SAML 2.0/WS-Fed, your application needs to have the capability to do the SAML/WS-Fed SSO integration in SP or IDP mode.</span><span class="sxs-lookup"><span data-stu-id="77861-123">For SAML 2.0/WS-Fed, your application needs to have the capability to do the SAML/WS-Fed SSO integration in SP or IDP mode.</span></span> <span data-ttu-id="77861-124">Please ensure this is working correctly before submitting the request.</span><span class="sxs-lookup"><span data-stu-id="77861-124">Please ensure this is working correctly before submitting the request.</span></span>

- <span data-ttu-id="77861-125">For Password SSO, please ensure that your application supports form authentication so that password vaulting can be done to get single sign-on work as expected.</span><span class="sxs-lookup"><span data-stu-id="77861-125">For Password SSO, please ensure that your application supports form authentication so that password vaulting can be done to get single sign-on work as expected.</span></span>

- <span data-ttu-id="77861-126">For Automatic User-Provisioning requests, application should be listed in the gallery with single sign-on feature enabled using any of the federation protocol described above.</span><span class="sxs-lookup"><span data-stu-id="77861-126">For Automatic User-Provisioning requests, application should be listed in the gallery with single sign-on feature enabled using any of the federation protocol described above.</span></span> <span data-ttu-id="77861-127">You can request for SSO and User provisioning together on the portal, if it's not already listed.</span><span class="sxs-lookup"><span data-stu-id="77861-127">You can request for SSO and User provisioning together on the portal, if it's not already listed.</span></span>

##  <a name="implementing-sso-using-federation-protocol"></a><span data-ttu-id="77861-128">Implementing SSO using federation protocol</span><span class="sxs-lookup"><span data-stu-id="77861-128">Implementing SSO using federation protocol</span></span>

<span data-ttu-id="77861-129">To list an application in the Azure AD app gallery, you first need to implement one of the following federation protocols supported by Azure AD and agree with Azure AD application Gallery terms and conditions.</span><span class="sxs-lookup"><span data-stu-id="77861-129">To list an application in the Azure AD app gallery, you first need to implement one of the following federation protocols supported by Azure AD and agree with Azure AD application Gallery terms and conditions.</span></span> <span data-ttu-id="77861-130">Read the terms and conditions of the Azure AD application gallery from [here](https://azure.microsoft.com/en-us/support/legal/active-directory-app-gallery-terms/).</span><span class="sxs-lookup"><span data-stu-id="77861-130">Read the terms and conditions of the Azure AD application gallery from [here](https://azure.microsoft.com/en-us/support/legal/active-directory-app-gallery-terms/).</span></span>

*   <span data-ttu-id="77861-131">**OpenID Connect**: To integrate your application with Azure AD using the Open ID Connect protocol, follow the [developers' instructions](authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="77861-131">**OpenID Connect**: To integrate your application with Azure AD using the Open ID Connect protocol, follow the [developers' instructions](authentication-scenarios.md).</span></span>

    ![TimeLine of listing OpenID Connect application into the gallery](./media/howto-app-gallery-listing/openid.png)

    * <span data-ttu-id="77861-133">If you want to add your application to list in the gallery using OpenID Connect, select **OpenID Connect & OAuth 2.0** as above.</span><span class="sxs-lookup"><span data-stu-id="77861-133">If you want to add your application to list in the gallery using OpenID Connect, select **OpenID Connect & OAuth 2.0** as above.</span></span>

    * <span data-ttu-id="77861-134">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span><span class="sxs-lookup"><span data-stu-id="77861-134">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span></span> 

*   <span data-ttu-id="77861-135">**SAML 2.0** or **WS-Fed**: If your app supports SAML 2.0, you can integrate it directly with an Azure AD tenant by using the [instructions to add a custom application](../manage-apps/configure-single-sign-on-non-gallery-applications.md).</span><span class="sxs-lookup"><span data-stu-id="77861-135">**SAML 2.0** or **WS-Fed**: If your app supports SAML 2.0, you can integrate it directly with an Azure AD tenant by using the [instructions to add a custom application](../manage-apps/configure-single-sign-on-non-gallery-applications.md).</span></span>

    ![TimeLine of listing SAML 2.0 or WS-Fed application into the gallery](./media/howto-app-gallery-listing/saml.png)

    * <span data-ttu-id="77861-137">If you want to add your application to list in the gallery using **SAML 2.0** or **WS-Fed**, select **SAMl 2.0/WS-Fed** as above.</span><span class="sxs-lookup"><span data-stu-id="77861-137">If you want to add your application to list in the gallery using **SAML 2.0** or **WS-Fed**, select **SAMl 2.0/WS-Fed** as above.</span></span>

    * <span data-ttu-id="77861-138">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span><span class="sxs-lookup"><span data-stu-id="77861-138">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span></span>

## <a name="implementing-sso-using-password-sso"></a><span data-ttu-id="77861-139">Implementing SSO using Password SSO</span><span class="sxs-lookup"><span data-stu-id="77861-139">Implementing SSO using Password SSO</span></span>

<span data-ttu-id="77861-140">Create a web application that has an HTML sign-in page to configure [password-based single sign-on](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="77861-140">Create a web application that has an HTML sign-in page to configure [password-based single sign-on](../manage-apps/what-is-single-sign-on.md).</span></span> <span data-ttu-id="77861-141">Password-based SSO, also referred to as password vaulting, enables you to manage user access and passwords to web applications that don't support identity federation.</span><span class="sxs-lookup"><span data-stu-id="77861-141">Password-based SSO, also referred to as password vaulting, enables you to manage user access and passwords to web applications that don't support identity federation.</span></span> <span data-ttu-id="77861-142">It is also useful for scenarios in which several users need to share a single account, such as to your organization's social media app accounts.</span><span class="sxs-lookup"><span data-stu-id="77861-142">It is also useful for scenarios in which several users need to share a single account, such as to your organization's social media app accounts.</span></span>

![TimeLine of listing Password SSO application into the gallery](./media/howto-app-gallery-listing/passwordsso.png)

* <span data-ttu-id="77861-144">If you want to add your application to list in the gallery using Password SSO, select **Password SSO** as above.</span><span class="sxs-lookup"><span data-stu-id="77861-144">If you want to add your application to list in the gallery using Password SSO, select **Password SSO** as above.</span></span>

* <span data-ttu-id="77861-145">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span><span class="sxs-lookup"><span data-stu-id="77861-145">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span></span>

##  <a name="updateremove-existing-listing"></a><span data-ttu-id="77861-146">Update/Remove existing listing</span><span class="sxs-lookup"><span data-stu-id="77861-146">Update/Remove existing listing</span></span>

<span data-ttu-id="77861-147">To update or remove an existing application in the Azure AD app gallery, you first need to submit the request in the [Application Network Portal](https://microsoft.sharepoint.com/teams/apponboarding/Apps).</span><span class="sxs-lookup"><span data-stu-id="77861-147">To update or remove an existing application in the Azure AD app gallery, you first need to submit the request in the [Application Network Portal](https://microsoft.sharepoint.com/teams/apponboarding/Apps).</span></span> <span data-ttu-id="77861-148">If you have an Office 365 account, use that to sign in to this portal.</span><span class="sxs-lookup"><span data-stu-id="77861-148">If you have an Office 365 account, use that to sign in to this portal.</span></span> <span data-ttu-id="77861-149">If not, use your Microsoft account (such as Outlook or Hotmail) to sign in.</span><span class="sxs-lookup"><span data-stu-id="77861-149">If not, use your Microsoft account (such as Outlook or Hotmail) to sign in.</span></span>

* <span data-ttu-id="77861-150">Select appropriate option from the below image</span><span class="sxs-lookup"><span data-stu-id="77861-150">Select appropriate option from the below image</span></span>

    ![TimeLine of listing saml application into the gallery](./media/howto-app-gallery-listing/updateorremove.png)

    * <span data-ttu-id="77861-152">If you want to update an existing application, select **Update existing application listing**.</span><span class="sxs-lookup"><span data-stu-id="77861-152">If you want to update an existing application, select **Update existing application listing**.</span></span>

    * <span data-ttu-id="77861-153">If you want to remove an existing application from the Azure AD gallery, select **Remove existing application listing**</span><span class="sxs-lookup"><span data-stu-id="77861-153">If you want to remove an existing application from the Azure AD gallery, select **Remove existing application listing**</span></span>

    * <span data-ttu-id="77861-154">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span><span class="sxs-lookup"><span data-stu-id="77861-154">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span></span> 

## <a name="submit-the-request-in-the-portal"></a><span data-ttu-id="77861-155">Submit the request in the portal</span><span class="sxs-lookup"><span data-stu-id="77861-155">Submit the request in the portal</span></span>

<span data-ttu-id="77861-156">After you've tested that your application integration works with Azure AD, submit your request for access on our [Application Network Portal](https://microsoft.sharepoint.com/teams/apponboarding/Apps).</span><span class="sxs-lookup"><span data-stu-id="77861-156">After you've tested that your application integration works with Azure AD, submit your request for access on our [Application Network Portal](https://microsoft.sharepoint.com/teams/apponboarding/Apps).</span></span> <span data-ttu-id="77861-157">If you have an Office 365 account, use that to sign in to this portal.</span><span class="sxs-lookup"><span data-stu-id="77861-157">If you have an Office 365 account, use that to sign in to this portal.</span></span> <span data-ttu-id="77861-158">If not, use your Microsoft account (such as Outlook or Hotmail) to sign in.</span><span class="sxs-lookup"><span data-stu-id="77861-158">If not, use your Microsoft account (such as Outlook or Hotmail) to sign in.</span></span>

<span data-ttu-id="77861-159">After you sign in, the following page appears.</span><span class="sxs-lookup"><span data-stu-id="77861-159">After you sign in, the following page appears.</span></span> <span data-ttu-id="77861-160">Provide a business justification for needing access in the text box, and then select **Request Access**.</span><span class="sxs-lookup"><span data-stu-id="77861-160">Provide a business justification for needing access in the text box, and then select **Request Access**.</span></span> <span data-ttu-id="77861-161">Our team reviews the details and gives you access accordingly.</span><span class="sxs-lookup"><span data-stu-id="77861-161">Our team reviews the details and gives you access accordingly.</span></span> <span data-ttu-id="77861-162">After that, you can sign in to the portal and submit your detailed request for the application.</span><span class="sxs-lookup"><span data-stu-id="77861-162">After that, you can sign in to the portal and submit your detailed request for the application.</span></span>

<span data-ttu-id="77861-163">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span><span class="sxs-lookup"><span data-stu-id="77861-163">If you have any issues regarding access, contact the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span></span>

![Access Request on SharePoint portal](./media/howto-app-gallery-listing/accessrequest.png)

## <a name="timelines"></a><span data-ttu-id="77861-165">Timelines</span><span class="sxs-lookup"><span data-stu-id="77861-165">Timelines</span></span>
    
<span data-ttu-id="77861-166">The timeline for the process of listing a SAML 2.0 or WS-Fed application in the gallery is 7-10 business days.</span><span class="sxs-lookup"><span data-stu-id="77861-166">The timeline for the process of listing a SAML 2.0 or WS-Fed application in the gallery is 7-10 business days.</span></span>

   ![TimeLine of listing saml application into the gallery](./media/howto-app-gallery-listing/timeline.png)

<span data-ttu-id="77861-168">The timeline for the process of listing an OpenID Connect application in the gallery is 2-5 business days.</span><span class="sxs-lookup"><span data-stu-id="77861-168">The timeline for the process of listing an OpenID Connect application in the gallery is 2-5 business days.</span></span>

   ![TimeLine of listing saml application into the gallery](./media/howto-app-gallery-listing/timeline2.png)

<span data-ttu-id="77861-170">The timeline for the process of listing the application in the gallery with user provisioning support is 40-45 business days.</span><span class="sxs-lookup"><span data-stu-id="77861-170">The timeline for the process of listing the application in the gallery with user provisioning support is 40-45 business days.</span></span>

   ![TimeLine of listing saml application into the gallery](./media/howto-app-gallery-listing/provisioningtimeline.png)

## <a name="escalations"></a><span data-ttu-id="77861-172">Escalations</span><span class="sxs-lookup"><span data-stu-id="77861-172">Escalations</span></span>

<span data-ttu-id="77861-173">For any escalations, send email to the [Azure AD SSO Integration Team](mailto:SaaSApplicationIntegrations@service.microsoft.com)  which is SaaSApplicationIntegrations@service.microsoft.com and we'll respond as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="77861-173">For any escalations, send email to the [Azure AD SSO Integration Team](mailto:SaaSApplicationIntegrations@service.microsoft.com)  which is SaaSApplicationIntegrations@service.microsoft.com and we'll respond as soon as possible.</span></span>