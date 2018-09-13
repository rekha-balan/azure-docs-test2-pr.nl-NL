---
title: Claims-aware apps - Azure AD App Proxy | Microsoft Docs
description: How to publish on-premises ASP.NET applications that accept ADFS claims for secure remote access by your users.
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
ms.date: 08/04/2017
ms.author: barbkess
ms.reviewer: harshja
ms.openlocfilehash: cf92b5b6ee3c6a529a43e7fa4cfeeb09954ad9ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869547"
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="15ff5-103">Working with claims-aware apps in Application Proxy</span><span class="sxs-lookup"><span data-stu-id="15ff5-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="15ff5-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="15ff5-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="15ff5-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span><span class="sxs-lookup"><span data-stu-id="15ff5-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="15ff5-106">There are a few ways to enable Application Proxy to work with these redirects.</span><span class="sxs-lookup"><span data-stu-id="15ff5-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="15ff5-107">Use this article to configure your deployment for claims-aware apps.</span><span class="sxs-lookup"><span data-stu-id="15ff5-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="15ff5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15ff5-108">Prerequisites</span></span>
<span data-ttu-id="15ff5-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="15ff5-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="15ff5-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span><span class="sxs-lookup"><span data-stu-id="15ff5-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="15ff5-111">Publish your application</span><span class="sxs-lookup"><span data-stu-id="15ff5-111">Publish your application</span></span>

1. <span data-ttu-id="15ff5-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15ff5-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="15ff5-113">Navigate to the application page in the portal and select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="15ff5-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="15ff5-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span><span class="sxs-lookup"><span data-stu-id="15ff5-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="15ff5-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span><span class="sxs-lookup"><span data-stu-id="15ff5-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="15ff5-116">Configure ADFS</span><span class="sxs-lookup"><span data-stu-id="15ff5-116">Configure ADFS</span></span>

<span data-ttu-id="15ff5-117">You can configure ADFS for claims-aware apps in one of two ways.</span><span class="sxs-lookup"><span data-stu-id="15ff5-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="15ff5-118">The first is by using custom domains.</span><span class="sxs-lookup"><span data-stu-id="15ff5-118">The first is by using custom domains.</span></span> <span data-ttu-id="15ff5-119">The second is with WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="15ff5-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="15ff5-120">Option 1: Custom domains</span><span class="sxs-lookup"><span data-stu-id="15ff5-120">Option 1: Custom domains</span></span>

<span data-ttu-id="15ff5-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](application-proxy-configure-custom-domain.md) for your applications.</span><span class="sxs-lookup"><span data-stu-id="15ff5-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](application-proxy-configure-custom-domain.md) for your applications.</span></span> <span data-ttu-id="15ff5-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span><span class="sxs-lookup"><span data-stu-id="15ff5-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="15ff5-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span><span class="sxs-lookup"><span data-stu-id="15ff5-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="15ff5-124">Option 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="15ff5-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="15ff5-125">Open ADFS Management.</span><span class="sxs-lookup"><span data-stu-id="15ff5-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="15ff5-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="15ff5-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Relying Party Trusts right-click on app name - screenshot](./media/application-proxy-configure-for-claims-aware-applications/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="15ff5-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="15ff5-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="15ff5-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="15ff5-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Add an Endpoint - set Trusted URL value - screenshot](./media/application-proxy-configure-for-claims-aware-applications/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="15ff5-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="15ff5-131">Next steps</span></span>
* <span data-ttu-id="15ff5-132">[Enable single-sign on](application-proxy-single-sign-on.md) for applications that aren't claims-aware</span><span class="sxs-lookup"><span data-stu-id="15ff5-132">[Enable single-sign on](application-proxy-single-sign-on.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="15ff5-133">Enable native client apps to interact with proxy applications</span><span class="sxs-lookup"><span data-stu-id="15ff5-133">Enable native client apps to interact with proxy applications</span></span>](application-proxy-configure-native-client-application.md)


