---
title: Self-service password reset in Azure Active Directory B2C | Microsoft Docs
description: Demonstrates how to set up self-service password reset for your customers in Azure Active Directory B2C
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 3612e10df12e2b18f32caae55bdd83b12a4e24a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779316"
---
# <a name="set-up-self-service-password-reset-for-your-customers"></a><span data-ttu-id="2444a-103">Set up self-service password reset for your customers</span><span class="sxs-lookup"><span data-stu-id="2444a-103">Set up self-service password reset for your customers</span></span>
<span data-ttu-id="2444a-104">With the self-service password reset feature, your customers who have signed up for local accounts can reset their passwords on their own.</span><span class="sxs-lookup"><span data-stu-id="2444a-104">With the self-service password reset feature, your customers who have signed up for local accounts can reset their passwords on their own.</span></span> <span data-ttu-id="2444a-105">This significantly reduces the burden on your support staff, especially if your application has millions of customers using it on a regular basis.</span><span class="sxs-lookup"><span data-stu-id="2444a-105">This significantly reduces the burden on your support staff, especially if your application has millions of customers using it on a regular basis.</span></span> <span data-ttu-id="2444a-106">Currently, using a verified email address is the only supported recovery method.</span><span class="sxs-lookup"><span data-stu-id="2444a-106">Currently, using a verified email address is the only supported recovery method.</span></span>

> [!NOTE]
> <span data-ttu-id="2444a-107">This article applies to self-service password reset used in the context of a sign-in policy.</span><span class="sxs-lookup"><span data-stu-id="2444a-107">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="2444a-108">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="2444a-108">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="2444a-109">By default, your directory doesn't have self-service password reset turned on.</span><span class="sxs-lookup"><span data-stu-id="2444a-109">By default, your directory doesn't have self-service password reset turned on.</span></span> <span data-ttu-id="2444a-110">Use the following steps to turn it on:</span><span class="sxs-lookup"><span data-stu-id="2444a-110">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="2444a-111">Sign in to the [Azure portal](https://portal.azure.com/) as the Subscription Administrator.</span><span class="sxs-lookup"><span data-stu-id="2444a-111">Sign in to the [Azure portal](https://portal.azure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="2444a-112">This is the same work or school account or the same Microsoft account that you used to create your directory.</span><span class="sxs-lookup"><span data-stu-id="2444a-112">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="2444a-113">Open **Azure Active Directory** (in the navigation bar on the left side).</span><span class="sxs-lookup"><span data-stu-id="2444a-113">Open **Azure Active Directory** (in the navigation bar on the left side).</span></span>
4. <span data-ttu-id="2444a-114">Set **Self service password reset enabled**  to **All**.</span><span class="sxs-lookup"><span data-stu-id="2444a-114">Set **Self service password reset enabled**  to **All**.</span></span> 
5. <span data-ttu-id="2444a-115">Click **Save** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="2444a-115">Click **Save** at the top of the page.</span></span> <span data-ttu-id="2444a-116">You're done!</span><span class="sxs-lookup"><span data-stu-id="2444a-116">You're done!</span></span>

<span data-ttu-id="2444a-117">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span><span class="sxs-lookup"><span data-stu-id="2444a-117">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="2444a-118">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the customer experience.</span><span class="sxs-lookup"><span data-stu-id="2444a-118">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the customer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="2444a-119">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/fundamentals/customize-branding.md).</span><span class="sxs-lookup"><span data-stu-id="2444a-119">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/fundamentals/customize-branding.md).</span></span>
> 
> 

