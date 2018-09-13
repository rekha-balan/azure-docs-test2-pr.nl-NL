---
title: Register an application with the Azure AD v2.0 endpoint using the portal | Microsoft Docs
description: How to register an app with Microsoft for enabling sign-in and accessing Microsoft services using the v2.0 endpoint
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2018
ms.author: celested
ms.custom: aaddev
ms.openlocfilehash: 8ab4e6b5b2813a216b6dd6f0fc108a09239ca9a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867830"
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="ec7c3-103">How to register an app with the v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="ec7c3-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="ec7c3-104">To build an app that accepts both personal Microsoft account (MSA) & work or school account (Azure AD) sign-in, you'll first need to register an app with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-104">To build an app that accepts both personal Microsoft account (MSA) & work or school account (Azure AD) sign-in, you'll first need to register an app with Microsoft.</span></span> <span data-ttu-id="ec7c3-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="ec7c3-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span> <span data-ttu-id="ec7c3-107">To determine if you should use the v2.0 endpoint, read about the [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ec7c3-107">To determine if you should use the v2.0 endpoint, read about the [v2.0 limitations](active-directory-v2-limitations.md).</span></span>


## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="ec7c3-108">Visit the Microsoft app registration portal</span><span class="sxs-lookup"><span data-stu-id="ec7c3-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="ec7c3-109">First, navigate to the Microsoft app registration portal at [https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="ec7c3-109">First, navigate to the Microsoft app registration portal at [https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span> 

<span data-ttu-id="ec7c3-110">Sign in with either a personal or work or school Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-110">Sign in with either a personal or work or school Microsoft account.</span></span> <span data-ttu-id="ec7c3-111">If you don't have either, sign up for a new personal account.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-111">If you don't have either, sign up for a new personal account.</span></span>

<span data-ttu-id="ec7c3-112">Done?</span><span class="sxs-lookup"><span data-stu-id="ec7c3-112">Done?</span></span> <span data-ttu-id="ec7c3-113">You should now be looking at your list of Microsoft apps, which is probably empty.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-113">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span> <span data-ttu-id="ec7c3-114">Let's change that.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-114">Let's change that.</span></span>

<span data-ttu-id="ec7c3-115">Click **Add an app**, and give it a name.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-115">Click **Add an app**, and give it a name.</span></span> <span data-ttu-id="ec7c3-116">The portal will assign your app a globally unique Application ID that you'll use later in your code.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-116">The portal will assign your app a globally unique Application ID that you'll use later in your code.</span></span> <span data-ttu-id="ec7c3-117">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-117">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="ec7c3-118">Next, add the **Platforms** that your app will use.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-118">Next, add the **Platforms** that your app will use.</span></span>

* <span data-ttu-id="ec7c3-119">For web-based apps, provide a **Redirect URI** where sign-in messages can be sent.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-119">For web-based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="ec7c3-120">For mobile apps, copy down the default redirect URI automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-120">For mobile apps, copy down the default redirect URI automatically created for you.</span></span>
* <span data-ttu-id="ec7c3-121">For web APIs, a default scope to access the Web API is automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-121">For web APIs, a default scope to access the Web API is automatically created for you.</span></span> <span data-ttu-id="ec7c3-122">You can choose to add additional scopes using the **Add Scope** button.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-122">You can choose to add additional scopes using the **Add Scope** button.</span></span> <span data-ttu-id="ec7c3-123">You can also add any applications that are pre-authorized to use your Web API using the **Pre-authorized applications** form.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-123">You can also add any applications that are pre-authorized to use your Web API using the **Pre-authorized applications** form.</span></span> 

<span data-ttu-id="ec7c3-124">Optionally, you can customize the look and feel of your sign-in page in the **Profile** section.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-124">Optionally, you can customize the look and feel of your sign-in page in the **Profile** section.</span></span> <span data-ttu-id="ec7c3-125">Make sure to click **Save** before moving on.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-125">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="ec7c3-126">When you create an application using [https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-126">When you create an application using [https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span> <span data-ttu-id="ec7c3-127">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-127">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span> <span data-ttu-id="ec7c3-128">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-128">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>


## <a name="build-a-quickstart-app"></a><span data-ttu-id="ec7c3-129">Build a quickstart app</span><span class="sxs-lookup"><span data-stu-id="ec7c3-129">Build a quickstart app</span></span>
<span data-ttu-id="ec7c3-130">Now that you have a Microsoft app, you can complete one of the v2.0 quickstart tutorials.</span><span class="sxs-lookup"><span data-stu-id="ec7c3-130">Now that you have a Microsoft app, you can complete one of the v2.0 quickstart tutorials.</span></span> <span data-ttu-id="ec7c3-131">Here are a few recommendations:</span><span class="sxs-lookup"><span data-stu-id="ec7c3-131">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

