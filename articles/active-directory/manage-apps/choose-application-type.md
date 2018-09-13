---
title: How to choose which application type to use when adding an application | Microsoft Docs
description: Understand the supported types of applications you can integrate with Azure AD and their related configuration options
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/09/2018
ms.author: barbkess
ms.openlocfilehash: 3a9f27a92a4bc808ff9bcf04b66523a92f1bcf03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869358"
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="81926-103">How to choose which application type to use when adding an application</span><span class="sxs-lookup"><span data-stu-id="81926-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="81926-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span><span class="sxs-lookup"><span data-stu-id="81926-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="81926-105">What is supported by each of them</span><span class="sxs-lookup"><span data-stu-id="81926-105">What is supported by each of them</span></span>
* <span data-ttu-id="81926-106">Why you might choose which application</span><span class="sxs-lookup"><span data-stu-id="81926-106">Why you might choose which application</span></span>
* <span data-ttu-id="81926-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span><span class="sxs-lookup"><span data-stu-id="81926-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="81926-108">Supported application types in Azure AD</span><span class="sxs-lookup"><span data-stu-id="81926-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="81926-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span><span class="sxs-lookup"><span data-stu-id="81926-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="81926-110">These include:</span><span class="sxs-lookup"><span data-stu-id="81926-110">These include:</span></span>

-   <span data-ttu-id="81926-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81926-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="81926-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span><span class="sxs-lookup"><span data-stu-id="81926-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="81926-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span><span class="sxs-lookup"><span data-stu-id="81926-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="81926-114">**Non-Gallery Applications** – Bring your own applications!</span><span class="sxs-lookup"><span data-stu-id="81926-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="81926-115">Any web link you want, or any application that renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM that you wish to integrate for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81926-115">Any web link you want, or any application that renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM that you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-preceding-application-types"></a><span data-ttu-id="81926-116">Features and capabilities supported by all the preceding application types</span><span class="sxs-lookup"><span data-stu-id="81926-116">Features and capabilities supported by all the preceding application types</span></span>

<span data-ttu-id="81926-117">The following features are supported by any of the preceding four application types in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="81926-117">The following features are supported by any of the preceding four application types in Azure AD:</span></span>

-   <span data-ttu-id="81926-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="81926-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="81926-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span><span class="sxs-lookup"><span data-stu-id="81926-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="81926-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span><span class="sxs-lookup"><span data-stu-id="81926-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="81926-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span><span class="sxs-lookup"><span data-stu-id="81926-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="81926-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span><span class="sxs-lookup"><span data-stu-id="81926-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="81926-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span><span class="sxs-lookup"><span data-stu-id="81926-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="81926-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span><span class="sxs-lookup"><span data-stu-id="81926-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="81926-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span><span class="sxs-lookup"><span data-stu-id="81926-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="81926-126">Single sign-on and provisioning modes supported by specific application types</span><span class="sxs-lookup"><span data-stu-id="81926-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="81926-127">The following table describes the different single sign-on and provisioning modes supported by each of the preceding application types.</span><span class="sxs-lookup"><span data-stu-id="81926-127">The following table describes the different single sign-on and provisioning modes supported by each of the preceding application types.</span></span> <span data-ttu-id="81926-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span><span class="sxs-lookup"><span data-stu-id="81926-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![App types table](./media/choose-application-type/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="81926-130">How to choose a single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="81926-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="81926-131">Following are the supported **single sign-on** modes for Azure AD applications.</span><span class="sxs-lookup"><span data-stu-id="81926-131">Following are the supported **single sign-on** modes for Azure AD applications.</span></span>

-   <span data-ttu-id="81926-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span><span class="sxs-lookup"><span data-stu-id="81926-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="81926-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="81926-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="81926-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span><span class="sxs-lookup"><span data-stu-id="81926-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="81926-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims \*</span><span class="sxs-lookup"><span data-stu-id="81926-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims \*</span></span>

   >[!NOTE]
   ><span data-ttu-id="81926-136">This option is not available when the application proxy is configured for an application.</span><span class="sxs-lookup"><span data-stu-id="81926-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="81926-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header-based authentication that you wish to perform single-sign on to</span><span class="sxs-lookup"><span data-stu-id="81926-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header-based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="81926-138">This option is only available when the application proxy and PingAccess is configured for an application.</span><span class="sxs-lookup"><span data-stu-id="81926-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="81926-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span><span class="sxs-lookup"><span data-stu-id="81926-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="81926-140">This option is only available when the application proxy is configured for an application.</span><span class="sxs-lookup"><span data-stu-id="81926-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="81926-141">Single sign-on modes for custom-developed applications</span><span class="sxs-lookup"><span data-stu-id="81926-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="81926-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not previously listed, which include:</span><span class="sxs-lookup"><span data-stu-id="81926-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not previously listed, which include:</span></span>

-   <span data-ttu-id="81926-143">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span><span class="sxs-lookup"><span data-stu-id="81926-143">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="81926-144">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span><span class="sxs-lookup"><span data-stu-id="81926-144">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="81926-145">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span><span class="sxs-lookup"><span data-stu-id="81926-145">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="81926-146">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span><span class="sxs-lookup"><span data-stu-id="81926-146">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="81926-147">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application that supports these single sign-on modes.</span><span class="sxs-lookup"><span data-stu-id="81926-147">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application that supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="81926-148">How to set an application’s single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="81926-148">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="81926-149">To set an application’s **single sign-on** mode, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="81926-149">To set an application’s **single sign-on** mode, follow these instructions:</span></span>

1.  <span data-ttu-id="81926-150">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="81926-150">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="81926-151">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="81926-151">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="81926-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="81926-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="81926-153">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="81926-153">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="81926-154">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="81926-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="81926-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="81926-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="81926-156">Select the application for which you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="81926-156">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="81926-157">Once the application loads, click **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="81926-157">Once the application loads, click **Single sign-on** from the application’s left-hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="81926-158">How to choose a provisioning mode</span><span class="sxs-lookup"><span data-stu-id="81926-158">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="81926-159">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81926-159">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="81926-160">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span><span class="sxs-lookup"><span data-stu-id="81926-160">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="81926-161">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="81926-161">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="81926-162">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span><span class="sxs-lookup"><span data-stu-id="81926-162">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="81926-163">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81926-163">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="81926-164">How to set an application’s provisioning mode</span><span class="sxs-lookup"><span data-stu-id="81926-164">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="81926-165">To set an application’s **provisioning** mode, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="81926-165">To set an application’s **provisioning** mode, follow these instructions:</span></span>

<span data-ttu-id="81926-166">To set an application’s **single sign-on** mode, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="81926-166">To set an application’s **single sign-on** mode, follow these instructions:</span></span>

1.  <span data-ttu-id="81926-167">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="81926-167">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="81926-168">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="81926-168">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="81926-169">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="81926-169">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="81926-170">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="81926-170">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="81926-171">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="81926-171">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="81926-172">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="81926-172">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="81926-173">Select the application for which you want to configure provisioning.</span><span class="sxs-lookup"><span data-stu-id="81926-173">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="81926-174">Once the application loads, click **Provisioning** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="81926-174">Once the application loads, click **Provisioning** from the application’s left-hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81926-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="81926-175">Next steps</span></span>
[<span data-ttu-id="81926-176">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81926-176">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
