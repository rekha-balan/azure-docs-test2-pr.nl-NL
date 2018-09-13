---
title: Single sign-on to apps with Azure AD Application Proxy | Microsoft Docs
description: Turn on single sign-on for your published on-premises applications with Azure AD Application Proxy in the Azure portal.
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
ms.date: 07/20/2017
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: fa12dd5e9dbe25bad947abed5ab1c732d231b25c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966581"
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="362f1-103">Password vaulting for single sign-on with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="362f1-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="362f1-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span><span class="sxs-lookup"><span data-stu-id="362f1-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="362f1-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span><span class="sxs-lookup"><span data-stu-id="362f1-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="362f1-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span><span class="sxs-lookup"><span data-stu-id="362f1-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="362f1-107">Application Proxy supports several [single sign-on modes](application-proxy-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="362f1-107">Application Proxy supports several [single sign-on modes](application-proxy-single-sign-on.md).</span></span> <span data-ttu-id="362f1-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span><span class="sxs-lookup"><span data-stu-id="362f1-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="362f1-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span><span class="sxs-lookup"><span data-stu-id="362f1-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="362f1-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span><span class="sxs-lookup"><span data-stu-id="362f1-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="362f1-111">You should already have published and tested your app with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="362f1-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="362f1-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span><span class="sxs-lookup"><span data-stu-id="362f1-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="362f1-113">Set up password vaulting for your application</span><span class="sxs-lookup"><span data-stu-id="362f1-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="362f1-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="362f1-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="362f1-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="362f1-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="362f1-116">From the list, select the app that you want to set up with SSO.</span><span class="sxs-lookup"><span data-stu-id="362f1-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="362f1-117">Select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="362f1-117">Select **Single sign-on**.</span></span>

   ![Select Single sign-on](./media/application-proxy-configure-single-sign-on-password-vaulting/select-sso.png)

5. <span data-ttu-id="362f1-119">For the SSO mode, choose **Password-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="362f1-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="362f1-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span><span class="sxs-lookup"><span data-stu-id="362f1-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="362f1-121">This may be the External URL that you created when you published the app through Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="362f1-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Choose password-based Sign-on and enter your URL](./media/application-proxy-configure-single-sign-on-password-vaulting/password-sso.png)

7. <span data-ttu-id="362f1-123">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="362f1-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="362f1-124">Test your app</span><span class="sxs-lookup"><span data-stu-id="362f1-124">Test your app</span></span>

<span data-ttu-id="362f1-125">Go to external URL that you configured for remote access to your application.</span><span class="sxs-lookup"><span data-stu-id="362f1-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="362f1-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span><span class="sxs-lookup"><span data-stu-id="362f1-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="362f1-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span><span class="sxs-lookup"><span data-stu-id="362f1-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="362f1-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="362f1-128">Next steps</span></span>

- <span data-ttu-id="362f1-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="362f1-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-single-sign-on.md)</span></span>
- <span data-ttu-id="362f1-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security.md)</span><span class="sxs-lookup"><span data-stu-id="362f1-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security.md)</span></span>