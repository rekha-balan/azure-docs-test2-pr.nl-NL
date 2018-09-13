---
title: How to get AppSource certified for Azure Active Directory| Microsoft Docs
description: Details on how to get your application AppSource certified for Azure Active Directory.
services: active-directory
documentationcenter: ''
author: skwan
manager: mbaldwin
editor: ''
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/28/2017
ms.author: skwan;bryanla
ms.openlocfilehash: 3290a375963bc3e625cbdb05b5f9686e8cfb34f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548897"
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory-ad"></a><span data-ttu-id="f3175-103">How to get AppSource Certified for Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="f3175-103">How to get AppSource Certified for Azure Active Directory (AD)</span></span>
<span data-ttu-id="f3175-104">To receive AppSource certification for Azure AD, your application must implement the multi-tenant sign in pattern with Azure AD using the OpenID Connect or OAuth 2.0 protocols.</span><span class="sxs-lookup"><span data-stu-id="f3175-104">To receive AppSource certification for Azure AD, your application must implement the multi-tenant sign in pattern with Azure AD using the OpenID Connect or OAuth 2.0 protocols.</span></span>  

<span data-ttu-id="f3175-105">If you’re not familiar with Azure AD sign-in or multi-tenant application development:</span><span class="sxs-lookup"><span data-stu-id="f3175-105">If you’re not familiar with Azure AD sign-in or multi-tenant application development:</span></span>

1. <span data-ttu-id="f3175-106">Start by reading about the [Browser to Web App scenarios in Authentication Scenarios for Azure AD][AAD-Auth-Scenarios-Browser-To-WebApp].</span><span class="sxs-lookup"><span data-stu-id="f3175-106">Start by reading about the [Browser to Web App scenarios in Authentication Scenarios for Azure AD][AAD-Auth-Scenarios-Browser-To-WebApp].</span></span>  
2. <span data-ttu-id="f3175-107">Next, check out the Azure AD [web application quick-start guides][AAD-QuickStart-Web-Apps], which demonstrate how to implement sign-in, and include companion code samples.</span><span class="sxs-lookup"><span data-stu-id="f3175-107">Next, check out the Azure AD [web application quick-start guides][AAD-QuickStart-Web-Apps], which demonstrate how to implement sign-in, and include companion code samples.</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="f3175-108">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Web) that will help you get up and running with Azure Active Directory in just a few minutes!</span><span class="sxs-lookup"><span data-stu-id="f3175-108">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Web) that will help you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="f3175-109">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span><span class="sxs-lookup"><span data-stu-id="f3175-109">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="f3175-110">When you’re finished, you will have a simple application that can authenticate users in your tenant and a back-end that can accept tokens and perform validation.</span><span class="sxs-lookup"><span data-stu-id="f3175-110">When you’re finished, you will have a simple application that can authenticate users in your tenant and a back-end that can accept tokens and perform validation.</span></span>
   > 
   > 
3. <span data-ttu-id="f3175-111">To learn how to implement the multi-tenant sign-in pattern with Azure AD, check out [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern][AAD-Howto-Multitenant-Overview]</span><span class="sxs-lookup"><span data-stu-id="f3175-111">To learn how to implement the multi-tenant sign-in pattern with Azure AD, check out [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern][AAD-Howto-Multitenant-Overview]</span></span>

## <a name="related-content"></a><span data-ttu-id="f3175-112">Related content</span><span class="sxs-lookup"><span data-stu-id="f3175-112">Related content</span></span>
<span data-ttu-id="f3175-113">For more information on building applications that support Azure AD sign-in, or to get help and support, refer to the [Azure AD Developer's Guide][AAD-Dev-Guide].</span><span class="sxs-lookup"><span data-stu-id="f3175-113">For more information on building applications that support Azure AD sign-in, or to get help and support, refer to the [Azure AD Developer's Guide][AAD-Dev-Guide].</span></span>

<span data-ttu-id="f3175-114">Please use the Disqus comments section following this article to provide feedback and help us refine and shape our content.</span><span class="sxs-lookup"><span data-stu-id="f3175-114">Please use the Disqus comments section following this article to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#web-application-quick-start-guides


<!--Image references-->










