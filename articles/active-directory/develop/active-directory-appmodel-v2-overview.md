---
title: Resources for the Azure AD v2.0 endpoint | Microsoft Docs
description: An introduction to building apps with both Microsoft Account and Azure Active Directory sign-in.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: d3571d3d842ac908200c7e6b437b40d3c370b38d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552294"
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="36b69-103">Sign-in Microsoft Account & Azure AD users in a single app</span><span class="sxs-lookup"><span data-stu-id="36b69-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="36b69-104">In the past, an app developer who wanted to support both Microsoft accounts and Azure Active Directory was required to integrate with two separate systems.</span><span class="sxs-lookup"><span data-stu-id="36b69-104">In the past, an app developer who wanted to support both Microsoft accounts and Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="36b69-105">We've now introduced a new authentication API version that enables you to sign in users in with both types of accounts using the Azure AD system.</span><span class="sxs-lookup"><span data-stu-id="36b69-105">We've now introduced a new authentication API version that enables you to sign in users in with both types of accounts using the Azure AD system.</span></span>  <span data-ttu-id="36b69-106">This converged authentication system is known as **the v2.0 endpoint**.</span><span class="sxs-lookup"><span data-stu-id="36b69-106">This converged authentication system is known as **the v2.0 endpoint**.</span></span>  <span data-ttu-id="36b69-107">With the v2.0 endpoint, one simple integration allows you to reach an audience that spans millions of users with both personal and work/school accounts.</span><span class="sxs-lookup"><span data-stu-id="36b69-107">With the v2.0 endpoint, one simple integration allows you to reach an audience that spans millions of users with both personal and work/school accounts.</span></span>

<span data-ttu-id="36b69-108">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) and [Office 365](https://msdn.microsoft.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) using either type of account.</span><span class="sxs-lookup"><span data-stu-id="36b69-108">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) and [Office 365](https://msdn.microsoft.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) using either type of account.</span></span>

<!-- For a quick introduction to the v2.0 endpoint, please view the [Getting Started with Microsoft Identities: Enterprise Grade Sign In For Your Apps](https://azure.microsoft.com/documentation/videos/build-2016-getting-started-with-microsoft-identities-enterprise-grade-sign-in-for-your-apps/) video. -->

## <a name="getting-started"></a><span data-ttu-id="36b69-109">Getting Started</span><span class="sxs-lookup"><span data-stu-id="36b69-109">Getting Started</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Build/2016/P530/player]


<span data-ttu-id="36b69-110">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span><span class="sxs-lookup"><span data-stu-id="36b69-110">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="36b69-111">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span><span class="sxs-lookup"><span data-stu-id="36b69-111">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<!-- TODO: Finalize this table  -->
[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="36b69-112">What's New</span><span class="sxs-lookup"><span data-stu-id="36b69-112">What's New</span></span>
<span data-ttu-id="36b69-113">The conceptual information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="36b69-113">The conceptual information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="36b69-114">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="36b69-114">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="36b69-115">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="36b69-115">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="36b69-116">We've recently added support for [admin restricted scopes](active-directory-v2-scopes.md) and the [OAuth2 client credentials grant](active-directory-v2-protocols-oauth-client-creds.md).</span><span class="sxs-lookup"><span data-stu-id="36b69-116">We've recently added support for [admin restricted scopes](active-directory-v2-scopes.md) and the [OAuth2 client credentials grant](active-directory-v2-protocols-oauth-client-creds.md).</span></span>  <span data-ttu-id="36b69-117">Try them out!</span><span class="sxs-lookup"><span data-stu-id="36b69-117">Try them out!</span></span>

## <a name="reference"></a><span data-ttu-id="36b69-118">Reference</span><span class="sxs-lookup"><span data-stu-id="36b69-118">Reference</span></span>
<span data-ttu-id="36b69-119">These links will be useful for exploring the platform in depth:</span><span class="sxs-lookup"><span data-stu-id="36b69-119">These links will be useful for exploring the platform in depth:</span></span>

* <span data-ttu-id="36b69-120">Build 2016: [Getting Started with Microsoft Identities: Enterprise Grade Sign In For Your Apps](https://azure.microsoft.com/documentation/videos/build-2016-getting-started-with-microsoft-identities-enterprise-grade-sign-in-for-your-apps/)</span><span class="sxs-lookup"><span data-stu-id="36b69-120">Build 2016: [Getting Started with Microsoft Identities: Enterprise Grade Sign In For Your Apps](https://azure.microsoft.com/documentation/videos/build-2016-getting-started-with-microsoft-identities-enterprise-grade-sign-in-for-your-apps/)</span></span>
* <span data-ttu-id="36b69-121">Get help on Stack Overflow using the [azure-active-directory](http://stackoverflow.com/questions/tagged/azure-active-directory) or [adal](http://stackoverflow.com/questions/tagged/adal) tags.</span><span class="sxs-lookup"><span data-stu-id="36b69-121">Get help on Stack Overflow using the [azure-active-directory](http://stackoverflow.com/questions/tagged/azure-active-directory) or [adal](http://stackoverflow.com/questions/tagged/adal) tags.</span></span>
* [<span data-ttu-id="36b69-122">v2.0 Protocol Reference</span><span class="sxs-lookup"><span data-stu-id="36b69-122">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="36b69-123">v2.0 Token Reference</span><span class="sxs-lookup"><span data-stu-id="36b69-123">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="36b69-124">v2.0 Library Reference</span><span class="sxs-lookup"><span data-stu-id="36b69-124">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="36b69-125">Scopes and Consent in the v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="36b69-125">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="36b69-126">The Microsoft App Registration Portal</span><span class="sxs-lookup"><span data-stu-id="36b69-126">The Microsoft App Registration Portal</span></span>](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)
* [<span data-ttu-id="36b69-127">Office 365 REST API Reference</span><span class="sxs-lookup"><span data-stu-id="36b69-127">Office 365 REST API Reference</span></span>](https://msdn.microsoft.com/office/office365/howto/authenticate-Office-365-APIs-using-v2)
* [<span data-ttu-id="36b69-128">The Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="36b69-128">The Microsoft Graph</span></span>](https://graph.microsoft.io)

