---
title: Register an application with the Azure AD v2.0 endpoint using the portal | Microsoft Docs
description: How to register an app with Microsoft for enabling sign-in and accessing Microsoft services using the v2.0 endpoint
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 4a71d02d37e55ae08035632c323283438b3f66c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556706"
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="a54d6-103">How to register an app with the v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="a54d6-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="a54d6-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a54d6-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="a54d6-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span><span class="sxs-lookup"><span data-stu-id="a54d6-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="a54d6-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="a54d6-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a54d6-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a54d6-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="a54d6-108">Visit the Microsoft app registration portal</span><span class="sxs-lookup"><span data-stu-id="a54d6-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="a54d6-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="a54d6-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="a54d6-110">This is a new app registration portal where you can manage your Microsoft apps.</span><span class="sxs-lookup"><span data-stu-id="a54d6-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="a54d6-111">Sign in with either a personal or work or school Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="a54d6-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="a54d6-112">If you don't have either, sign up for a new personal account.</span><span class="sxs-lookup"><span data-stu-id="a54d6-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="a54d6-113">Go ahead, it won't take long - we'll wait here.</span><span class="sxs-lookup"><span data-stu-id="a54d6-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="a54d6-114">Done?</span><span class="sxs-lookup"><span data-stu-id="a54d6-114">Done?</span></span> <span data-ttu-id="a54d6-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span><span class="sxs-lookup"><span data-stu-id="a54d6-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="a54d6-116">Let's change that.</span><span class="sxs-lookup"><span data-stu-id="a54d6-116">Let's change that.</span></span>

<span data-ttu-id="a54d6-117">Click **Add an app**, and give it a name.</span><span class="sxs-lookup"><span data-stu-id="a54d6-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="a54d6-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span><span class="sxs-lookup"><span data-stu-id="a54d6-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="a54d6-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span><span class="sxs-lookup"><span data-stu-id="a54d6-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>
<!-- TODO: Link for app secrets -->

<span data-ttu-id="a54d6-120">Next, add the Platforms that your app will use.</span><span class="sxs-lookup"><span data-stu-id="a54d6-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="a54d6-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span><span class="sxs-lookup"><span data-stu-id="a54d6-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="a54d6-122">For mobile apps, copy down the default redirect uri automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="a54d6-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="a54d6-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span><span class="sxs-lookup"><span data-stu-id="a54d6-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="a54d6-124">Make sure to click **Save** before moving on.</span><span class="sxs-lookup"><span data-stu-id="a54d6-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="a54d6-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span><span class="sxs-lookup"><span data-stu-id="a54d6-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="a54d6-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="a54d6-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="a54d6-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span><span class="sxs-lookup"><span data-stu-id="a54d6-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="a54d6-128">Build a quick start app</span><span class="sxs-lookup"><span data-stu-id="a54d6-128">Build a quick start app</span></span>
<span data-ttu-id="a54d6-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span><span class="sxs-lookup"><span data-stu-id="a54d6-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="a54d6-130">Here are a few recommendations:</span><span class="sxs-lookup"><span data-stu-id="a54d6-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

