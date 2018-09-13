---
title: Single sign-on to apps with Azure AD Application Proxy | Microsoft Docs
description: Turn on single sign-on for your published on-premises applications with Azure AD Application Proxy in the Azure portal.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: asteen
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: kgremban
ms.openlocfilehash: 270e2cc17f46b29b6587ed1ff1cf3cef1c218513
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549790"
---
# <a name="provide-single-sign-on-with-azure-ad-application-proxy---public-preview"></a><span data-ttu-id="9de98-103">Provide single sign-on with Azure AD Application Proxy - Public Preview</span><span class="sxs-lookup"><span data-stu-id="9de98-103">Provide single sign-on with Azure AD Application Proxy - Public Preview</span></span>

<span data-ttu-id="9de98-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span><span class="sxs-lookup"><span data-stu-id="9de98-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="9de98-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span><span class="sxs-lookup"><span data-stu-id="9de98-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="9de98-106">Now, your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span><span class="sxs-lookup"><span data-stu-id="9de98-106">Now, your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="9de98-107">In this article, we'll use the example of a password-based app to show how password vaulting provides a simple SSO experience.</span><span class="sxs-lookup"><span data-stu-id="9de98-107">In this article, we'll use the example of a password-based app to show how password vaulting provides a simple SSO experience.</span></span> 

<span data-ttu-id="9de98-108">You should already have published and tested your app with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="9de98-108">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="9de98-109">If not, follow the steps in [Publish applications using Azure AD Application Proxy - Public Preview](application-proxy-publish-azure-portal.md) then come back here.</span><span class="sxs-lookup"><span data-stu-id="9de98-109">If not, follow the steps in [Publish applications using Azure AD Application Proxy - Public Preview](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

<span data-ttu-id="9de98-110">Or, if you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9de98-110">Or, if you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="9de98-111">Set up password vaulting for your application</span><span class="sxs-lookup"><span data-stu-id="9de98-111">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="9de98-112">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9de98-112">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="9de98-113">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9de98-113">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="9de98-114">From the list, select the app that you want to set up with SSO.</span><span class="sxs-lookup"><span data-stu-id="9de98-114">From the list, select the app that you want to set up with SSO.</span></span> <span data-ttu-id="9de98-115">If you have a lot of apps, you can use the search box to filter for the right one.</span><span class="sxs-lookup"><span data-stu-id="9de98-115">If you have a lot of apps, you can use the search box to filter for the right one.</span></span>  
4. <span data-ttu-id="9de98-116">Under the Manage section, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9de98-116">Under the Manage section, select **Single sign-on**.</span></span>

   ![Select Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="9de98-118">For the SSO mode, choose **Password-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9de98-118">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="9de98-119">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app.</span><span class="sxs-lookup"><span data-stu-id="9de98-119">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app.</span></span> <span data-ttu-id="9de98-120">This should be the External URL that you created when you published the app through Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="9de98-120">This should be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Choose password-based Sign-on and enter your URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="9de98-122">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="9de98-122">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="9de98-123">Test your app</span><span class="sxs-lookup"><span data-stu-id="9de98-123">Test your app</span></span>

<span data-ttu-id="9de98-124">Go to the [MyApps site](https://myapps.microsoft.com) and select the app you just configured.</span><span class="sxs-lookup"><span data-stu-id="9de98-124">Go to the [MyApps site](https://myapps.microsoft.com) and select the app you just configured.</span></span> <span data-ttu-id="9de98-125">Sign in with your credentials for that app (or the credentials for the test account you set up with access).</span><span class="sxs-lookup"><span data-stu-id="9de98-125">Sign in with your credentials for that app (or the credentials for the test account you set up with access).</span></span> <span data-ttu-id="9de98-126">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span><span class="sxs-lookup"><span data-stu-id="9de98-126">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9de98-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="9de98-127">Next steps</span></span>

<span data-ttu-id="9de98-128">Read about other ways to implement [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span><span class="sxs-lookup"><span data-stu-id="9de98-128">Read about other ways to implement [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span></span>


