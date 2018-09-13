---
title: How to choose which application type to use when adding an application | Microsoft Docs
description: Understand the supported types of applications you can integrate with Azure AD and their related configuration options
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
ms.openlocfilehash: ca736f4615c188ab5c2650642b5949dcc27013ee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672163"
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="caef2-103">How to choose which application type to use when adding an application</span><span class="sxs-lookup"><span data-stu-id="caef2-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="caef2-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span><span class="sxs-lookup"><span data-stu-id="caef2-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="caef2-105">What is supported by each of them</span><span class="sxs-lookup"><span data-stu-id="caef2-105">What is supported by each of them</span></span>
* <span data-ttu-id="caef2-106">Why you might choose which application</span><span class="sxs-lookup"><span data-stu-id="caef2-106">Why you might choose which application</span></span>
* <span data-ttu-id="caef2-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span><span class="sxs-lookup"><span data-stu-id="caef2-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="caef2-108">Supported application types in Azure AD</span><span class="sxs-lookup"><span data-stu-id="caef2-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="caef2-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span><span class="sxs-lookup"><span data-stu-id="caef2-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="caef2-110">These include:</span><span class="sxs-lookup"><span data-stu-id="caef2-110">These include:</span></span>

-   <span data-ttu-id="caef2-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caef2-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="caef2-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span><span class="sxs-lookup"><span data-stu-id="caef2-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="caef2-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span><span class="sxs-lookup"><span data-stu-id="caef2-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="caef2-114">**Non-Gallery Applications** – Bring your own applications!</span><span class="sxs-lookup"><span data-stu-id="caef2-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="caef2-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caef2-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="caef2-116">Features and capabilities supported by all the above application types</span><span class="sxs-lookup"><span data-stu-id="caef2-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="caef2-117">The following features are supported by any of the above 4 application types in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="caef2-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="caef2-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="caef2-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="caef2-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span><span class="sxs-lookup"><span data-stu-id="caef2-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="caef2-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span><span class="sxs-lookup"><span data-stu-id="caef2-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="caef2-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span><span class="sxs-lookup"><span data-stu-id="caef2-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="caef2-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span><span class="sxs-lookup"><span data-stu-id="caef2-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="caef2-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span><span class="sxs-lookup"><span data-stu-id="caef2-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="caef2-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span><span class="sxs-lookup"><span data-stu-id="caef2-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="caef2-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span><span class="sxs-lookup"><span data-stu-id="caef2-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="caef2-126">Single sign-on and provisioning modes supported by specific application types</span><span class="sxs-lookup"><span data-stu-id="caef2-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="caef2-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span><span class="sxs-lookup"><span data-stu-id="caef2-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="caef2-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span><span class="sxs-lookup"><span data-stu-id="caef2-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![App types table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="caef2-130">How to choose a single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="caef2-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="caef2-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span><span class="sxs-lookup"><span data-stu-id="caef2-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="caef2-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span><span class="sxs-lookup"><span data-stu-id="caef2-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="caef2-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="caef2-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="caef2-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span><span class="sxs-lookup"><span data-stu-id="caef2-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="caef2-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims \*</span><span class="sxs-lookup"><span data-stu-id="caef2-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims \*</span></span>

   >[!NOTE]
   ><span data-ttu-id="caef2-136">This option is not available when the application proxy is configured for an application.</span><span class="sxs-lookup"><span data-stu-id="caef2-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="caef2-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span><span class="sxs-lookup"><span data-stu-id="caef2-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="caef2-138">This option is only available when the application proxy and PingAccess is configured for an application.</span><span class="sxs-lookup"><span data-stu-id="caef2-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="caef2-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span><span class="sxs-lookup"><span data-stu-id="caef2-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="caef2-140">This option is only available when the application proxy is configured for an application.</span><span class="sxs-lookup"><span data-stu-id="caef2-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="caef2-141">Single sign-on modes for custom-developed applications</span><span class="sxs-lookup"><span data-stu-id="caef2-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="caef2-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span><span class="sxs-lookup"><span data-stu-id="caef2-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="caef2-143">These include:</span><span class="sxs-lookup"><span data-stu-id="caef2-143">These include:</span></span>

-   <span data-ttu-id="caef2-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span><span class="sxs-lookup"><span data-stu-id="caef2-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="caef2-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span><span class="sxs-lookup"><span data-stu-id="caef2-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="caef2-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span><span class="sxs-lookup"><span data-stu-id="caef2-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="caef2-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span><span class="sxs-lookup"><span data-stu-id="caef2-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="caef2-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span><span class="sxs-lookup"><span data-stu-id="caef2-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="caef2-149">How to set an application’s single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="caef2-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="caef2-150">To set an application’s **single sign-on** mode, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="caef2-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="caef2-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="caef2-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="caef2-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="caef2-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="caef2-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="caef2-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="caef2-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="caef2-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="caef2-155">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="caef2-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="caef2-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="caef2-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="caef2-157">Select the application for which you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="caef2-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="caef2-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="caef2-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="caef2-159">How to choose a provisioning mode</span><span class="sxs-lookup"><span data-stu-id="caef2-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="caef2-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caef2-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="caef2-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span><span class="sxs-lookup"><span data-stu-id="caef2-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="caef2-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="caef2-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="caef2-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span><span class="sxs-lookup"><span data-stu-id="caef2-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="caef2-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caef2-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="caef2-165">How to set an application’s provisioning mode</span><span class="sxs-lookup"><span data-stu-id="caef2-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="caef2-166">To set an application’s **provisioning** mode, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="caef2-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="caef2-167">To set an application’s **single sign-on** mode, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="caef2-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="caef2-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="caef2-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="caef2-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="caef2-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="caef2-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="caef2-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="caef2-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="caef2-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="caef2-172">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="caef2-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="caef2-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="caef2-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="caef2-174">Select the application for which you want to configure provisioning.</span><span class="sxs-lookup"><span data-stu-id="caef2-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="caef2-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="caef2-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caef2-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="caef2-176">Next steps</span></span>
[<span data-ttu-id="caef2-177">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="caef2-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

