---
title: Claims-aware apps - Azure AD App Proxy | Microsoft Docs
description: How to publish on-premises ASP.NET applications that accept ADFS claims for secure remote access by your users.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: kgremban
ms.openlocfilehash: e53b07576176c58b9135fd160a2e59717d61ce29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553825"
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="d592b-103">Working with claims aware apps in Application Proxy</span><span class="sxs-lookup"><span data-stu-id="d592b-103">Working with claims aware apps in Application Proxy</span></span>
<span data-ttu-id="d592b-104">Claims aware apps perform a redirection to the Security Token Service (STS), which in turn requests credentials from the user in exchange for a token before redirecting the user to the application.</span><span class="sxs-lookup"><span data-stu-id="d592b-104">Claims aware apps perform a redirection to the Security Token Service (STS), which in turn requests credentials from the user in exchange for a token before redirecting the user to the application.</span></span> <span data-ttu-id="d592b-105">To enable Application Proxy to work with these redirects, the following steps need to be taken.</span><span class="sxs-lookup"><span data-stu-id="d592b-105">To enable Application Proxy to work with these redirects, the following steps need to be taken.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d592b-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d592b-106">Prerequisites</span></span>
<span data-ttu-id="d592b-107">Before performing this procedure, make sure that the STS the claims aware app redirects to is available outside of your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="d592b-107">Before performing this procedure, make sure that the STS the claims aware app redirects to is available outside of your on-premises network.</span></span>

## <a name="azure-classic-portal-configuration"></a><span data-ttu-id="d592b-108">Azure classic portal configuration</span><span class="sxs-lookup"><span data-stu-id="d592b-108">Azure classic portal configuration</span></span>
1. <span data-ttu-id="d592b-109">Publish your application according to the instructions described in [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d592b-109">Publish your application according to the instructions described in [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>
2. <span data-ttu-id="d592b-110">In the list of applications, select the claims aware app and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="d592b-110">In the list of applications, select the claims aware app and click **Configure**.</span></span>
3. <span data-ttu-id="d592b-111">If you chose **Passthrough** as your **Preauthentication Method**, make sure to select **HTTPS** as your **External URL** scheme.</span><span class="sxs-lookup"><span data-stu-id="d592b-111">If you chose **Passthrough** as your **Preauthentication Method**, make sure to select **HTTPS** as your **External URL** scheme.</span></span>
4. <span data-ttu-id="d592b-112">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **None** as your **Internal Authentication Method**.</span><span class="sxs-lookup"><span data-stu-id="d592b-112">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **None** as your **Internal Authentication Method**.</span></span>

## <a name="adfs-configuration"></a><span data-ttu-id="d592b-113">ADFS configuration</span><span class="sxs-lookup"><span data-stu-id="d592b-113">ADFS configuration</span></span>
1. <span data-ttu-id="d592b-114">Open ADFS Management.</span><span class="sxs-lookup"><span data-stu-id="d592b-114">Open ADFS Management.</span></span>
2. <span data-ttu-id="d592b-115">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d592b-115">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Relying Party Trusts right-click on app name - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="d592b-117">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="d592b-117">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="d592b-118">Under **Trusted URL** enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d592b-118">Under **Trusted URL** enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Add an Endpoint - set Trusted URL value - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="d592b-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="d592b-120">Next steps</span></span>
* [<span data-ttu-id="d592b-121">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="d592b-121">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="d592b-122">Troubleshoot issues you're having with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="d592b-122">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
* [<span data-ttu-id="d592b-123">Enable native client apps to interact with proxy applications</span><span class="sxs-lookup"><span data-stu-id="d592b-123">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)




