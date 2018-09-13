---
title: How to determine what single-sign on method to use | Microsoft Docs
description: Understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.
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
ms.openlocfilehash: a9afb3f611a5762d329788b0aa7e1bc52e41fab3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866420"
---
# <a name="how-to-determine-what-single-sign-on-method-to-use"></a><span data-ttu-id="5b35a-103">How to determine what single-sign on method to use</span><span class="sxs-lookup"><span data-stu-id="5b35a-103">How to determine what single-sign on method to use</span></span>

<span data-ttu-id="5b35a-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span><span class="sxs-lookup"><span data-stu-id="5b35a-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="5b35a-105">Single sign-on and provisioning modes supported by specific application types</span><span class="sxs-lookup"><span data-stu-id="5b35a-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="5b35a-106">The following table describes the different single sign-on and provisioning modes supported by each of the preceding application types.</span><span class="sxs-lookup"><span data-stu-id="5b35a-106">The following table describes the different single sign-on and provisioning modes supported by each of the preceding application types.</span></span> <span data-ttu-id="5b35a-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span><span class="sxs-lookup"><span data-stu-id="5b35a-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![App types table](./media/single-sign-on-modes/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="5b35a-109">How to choose a single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="5b35a-109">How to choose a single sign-on mode</span></span>

<span data-ttu-id="5b35a-110">Following are the supported **single sign-on** modes for Azure AD applications.</span><span class="sxs-lookup"><span data-stu-id="5b35a-110">Following are the supported **single sign-on** modes for Azure AD applications.</span></span>

-   <span data-ttu-id="5b35a-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span><span class="sxs-lookup"><span data-stu-id="5b35a-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="5b35a-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="5b35a-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="5b35a-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span><span class="sxs-lookup"><span data-stu-id="5b35a-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="5b35a-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(\*\*Note:*\* this option is not available when the application proxy is configured for an application)\*</span><span class="sxs-lookup"><span data-stu-id="5b35a-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(\*\*Note:*\* this option is not available when the application proxy is configured for an application)\*</span></span>

-   <span data-ttu-id="5b35a-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header-based authentication that you wish to perform single-sign on to *(\*\*Note:*\* this option is only available when the application proxy and PingAccess are configured for an application)\*</span><span class="sxs-lookup"><span data-stu-id="5b35a-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header-based authentication that you wish to perform single-sign on to *(\*\*Note:*\* this option is only available when the application proxy and PingAccess are configured for an application)\*</span></span>

-   <span data-ttu-id="5b35a-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(\*\*Note:*\* this option is only available when the application proxy is configured for an application)\*</span><span class="sxs-lookup"><span data-stu-id="5b35a-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(\*\*Note:*\* this option is only available when the application proxy is configured for an application)\*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="5b35a-117">Single sign-on modes for custom-developed applications</span><span class="sxs-lookup"><span data-stu-id="5b35a-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="5b35a-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not previously listed, which include:</span><span class="sxs-lookup"><span data-stu-id="5b35a-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not previously listed, which include:</span></span>

-   <span data-ttu-id="5b35a-119">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span><span class="sxs-lookup"><span data-stu-id="5b35a-119">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="5b35a-120">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span><span class="sxs-lookup"><span data-stu-id="5b35a-120">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="5b35a-121">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span><span class="sxs-lookup"><span data-stu-id="5b35a-121">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="5b35a-122">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span><span class="sxs-lookup"><span data-stu-id="5b35a-122">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="5b35a-123">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span><span class="sxs-lookup"><span data-stu-id="5b35a-123">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="5b35a-124">How to set an application’s single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="5b35a-124">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="5b35a-125">To set an application’s **single sign-on** mode, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="5b35a-125">To set an application’s **single sign-on** mode, follow these instructions:</span></span>

1.  <span data-ttu-id="5b35a-126">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="5b35a-126">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5b35a-127">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b35a-127">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="5b35a-128">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b35a-128">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b35a-129">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b35a-129">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="5b35a-130">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="5b35a-130">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5b35a-131">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="5b35a-131">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5b35a-132">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b35a-132">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="5b35a-133">Once the application loads, click **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b35a-133">Once the application loads, click **Single sign-on** from the application’s left-hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b35a-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b35a-134">Next steps</span></span>
[<span data-ttu-id="5b35a-135">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="5b35a-135">Provide single sign-on to your apps with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)

