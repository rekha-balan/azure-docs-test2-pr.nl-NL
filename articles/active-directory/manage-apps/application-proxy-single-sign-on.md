---
title: Manage SSO for Azure AD Application Proxy | Microsoft Docs
description: Learn about the basics of single sign-on with Application Proxy
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: dbdbe8b83af20f66ad2cc99d2a5665262479b4a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857071"
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="95165-103">How does Azure AD Application Proxy provide single sign-on?</span><span class="sxs-lookup"><span data-stu-id="95165-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="95165-104">Single sign-on is a key element of Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="95165-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="95165-105">It provides the best user experience because your users only have to sign in to Azure Active Directory in the cloud.</span><span class="sxs-lookup"><span data-stu-id="95165-105">It provides the best user experience because your users only have to sign in to Azure Active Directory in the cloud.</span></span> <span data-ttu-id="95165-106">Once they authenticate to Azure Active Directory, the Application Proxy connector handles the authentication to the on-premises application.</span><span class="sxs-lookup"><span data-stu-id="95165-106">Once they authenticate to Azure Active Directory, the Application Proxy connector handles the authentication to the on-premises application.</span></span> <span data-ttu-id="95165-107">The backend application can't tell the difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span><span class="sxs-lookup"><span data-stu-id="95165-107">The backend application can't tell the difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="95165-108">To use Azure Active Directory for single sign-on to your applications, you need to select **Azure Active Directory** as the pre-authentication method.</span><span class="sxs-lookup"><span data-stu-id="95165-108">To use Azure Active Directory for single sign-on to your applications, you need to select **Azure Active Directory** as the pre-authentication method.</span></span> <span data-ttu-id="95165-109">If you select **Passthrough** then your users don't authenticate to Azure Active Directory at all, but are directed straight to the application.</span><span class="sxs-lookup"><span data-stu-id="95165-109">If you select **Passthrough** then your users don't authenticate to Azure Active Directory at all, but are directed straight to the application.</span></span> <span data-ttu-id="95165-110">You can configure this setting when you first publish an application, or navigate to your application in the Azure portal and edit the Application Proxy settings.</span><span class="sxs-lookup"><span data-stu-id="95165-110">You can configure this setting when you first publish an application, or navigate to your application in the Azure portal and edit the Application Proxy settings.</span></span> 

<span data-ttu-id="95165-111">To see your single sign-on options, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="95165-111">To see your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="95165-112">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95165-112">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="95165-113">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="95165-113">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="95165-114">Select the app whose single sign-on options you want to manage.</span><span class="sxs-lookup"><span data-stu-id="95165-114">Select the app whose single sign-on options you want to manage.</span></span>
4. <span data-ttu-id="95165-115">Select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="95165-115">Select **Single sign-on**.</span></span>

   ![SSO dropdown menu](./media/application-proxy-single-sign-on/single-sign-on-mode.png)

<span data-ttu-id="95165-117">The dropdown menu shows five options for single sign-on to your application:</span><span class="sxs-lookup"><span data-stu-id="95165-117">The dropdown menu shows five options for single sign-on to your application:</span></span>

* <span data-ttu-id="95165-118">Azure AD single sign-on disabled</span><span class="sxs-lookup"><span data-stu-id="95165-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="95165-119">Password-based sign-on</span><span class="sxs-lookup"><span data-stu-id="95165-119">Password-based sign-on</span></span>
* <span data-ttu-id="95165-120">Linked sign-on</span><span class="sxs-lookup"><span data-stu-id="95165-120">Linked sign-on</span></span>
* <span data-ttu-id="95165-121">Integrated Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="95165-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="95165-122">Header-based sign-on</span><span class="sxs-lookup"><span data-stu-id="95165-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="95165-123">Azure AD single sign-on disabled</span><span class="sxs-lookup"><span data-stu-id="95165-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="95165-124">If you don't want to use Azure Active Directory integration for single sign-on to your application, choose **Azure AD single sign-on disabled**.</span><span class="sxs-lookup"><span data-stu-id="95165-124">If you don't want to use Azure Active Directory integration for single sign-on to your application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="95165-125">With this option selected, your users may authenticate twice.</span><span class="sxs-lookup"><span data-stu-id="95165-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="95165-126">First, they authenticate to Azure Active Directory and then sign in to the application itself.</span><span class="sxs-lookup"><span data-stu-id="95165-126">First, they authenticate to Azure Active Directory and then sign in to the application itself.</span></span> 

<span data-ttu-id="95165-127">This option is a good choice if your on-premises application doesn't require users to authenticate, but you want to add Azure Active Directory as a layer of security for remote access.</span><span class="sxs-lookup"><span data-stu-id="95165-127">This option is a good choice if your on-premises application doesn't require users to authenticate, but you want to add Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="95165-128">Password-based sign-on</span><span class="sxs-lookup"><span data-stu-id="95165-128">Password-based sign-on</span></span>

<span data-ttu-id="95165-129">If you want to use Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span><span class="sxs-lookup"><span data-stu-id="95165-129">If you want to use Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="95165-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span><span class="sxs-lookup"><span data-stu-id="95165-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="95165-131">With password-based sign-on, your users need to sign in to the application the first time they access it.</span><span class="sxs-lookup"><span data-stu-id="95165-131">With password-based sign-on, your users need to sign in to the application the first time they access it.</span></span> <span data-ttu-id="95165-132">After that, Azure Active Directory supplies the username and password on behalf of the user.</span><span class="sxs-lookup"><span data-stu-id="95165-132">After that, Azure Active Directory supplies the username and password on behalf of the user.</span></span> 

<span data-ttu-id="95165-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-password-vaulting.md).</span><span class="sxs-lookup"><span data-stu-id="95165-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-password-vaulting.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="95165-134">Linked sign-on</span><span class="sxs-lookup"><span data-stu-id="95165-134">Linked sign-on</span></span>

<span data-ttu-id="95165-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span><span class="sxs-lookup"><span data-stu-id="95165-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="95165-136">This option enables Azure Active Directory to leverage existing SSO solutions, but still gives your users remote access to the application.</span><span class="sxs-lookup"><span data-stu-id="95165-136">This option enables Azure Active Directory to leverage existing SSO solutions, but still gives your users remote access to the application.</span></span> 

<span data-ttu-id="95165-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](what-is-single-sign-on.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="95165-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](what-is-single-sign-on.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="95165-138">Integrated Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="95165-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="95165-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want to use Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span><span class="sxs-lookup"><span data-stu-id="95165-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want to use Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="95165-140">With this option, your users only need to authenticate to Azure Active Directory, and then the Application Proxy connector impersonates the user to get a Kerberos token and sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="95165-140">With this option, your users only need to authenticate to Azure Active Directory, and then the Application Proxy connector impersonates the user to get a Kerberos token and sign in to the application.</span></span> 

<span data-ttu-id="95165-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-with-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="95165-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-with-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="95165-142">Header-based sign-on</span><span class="sxs-lookup"><span data-stu-id="95165-142">Header-based sign-on</span></span> 

<span data-ttu-id="95165-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span><span class="sxs-lookup"><span data-stu-id="95165-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="95165-144">With this option, your users only need to authentication the Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95165-144">With this option, your users only need to authentication the Azure Active Directory.</span></span> <span data-ttu-id="95165-145">Microsoft partners with a third-party authentication service called PingAccess, which translated the Azure Active Directory access token into a header format for the application.</span><span class="sxs-lookup"><span data-stu-id="95165-145">Microsoft partners with a third-party authentication service called PingAccess, which translated the Azure Active Directory access token into a header format for the application.</span></span> 

<span data-ttu-id="95165-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-with-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="95165-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-with-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95165-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="95165-147">Next steps</span></span>

- [<span data-ttu-id="95165-148">Password vaulting for single sign-on with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="95165-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-configure-single-sign-on-password-vaulting.md)
- [<span data-ttu-id="95165-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="95165-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)
- [<span data-ttu-id="95165-150">Header-based authentication for single sign-on with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="95165-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-ping-access.md) 
