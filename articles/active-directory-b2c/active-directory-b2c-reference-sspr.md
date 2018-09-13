---
title: 'Azure Active Directory B2C: Self-service password reset | Microsoft Docs'
description: A topic demonstrating how to set up self-service password reset for your consumers in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4a9194ac2139b5937703f6ebf98c9b721e87e210
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550071"
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="27051-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span><span class="sxs-lookup"><span data-stu-id="27051-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="27051-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span><span class="sxs-lookup"><span data-stu-id="27051-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="27051-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span><span class="sxs-lookup"><span data-stu-id="27051-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="27051-106">Currently, we only support using a verified email address as a recovery method.</span><span class="sxs-lookup"><span data-stu-id="27051-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="27051-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span><span class="sxs-lookup"><span data-stu-id="27051-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="27051-108">This article applies to self-service password reset used in the context of a sign-in policy.</span><span class="sxs-lookup"><span data-stu-id="27051-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="27051-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="27051-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="27051-110">By default, your directory will not have self-service password reset turned on.</span><span class="sxs-lookup"><span data-stu-id="27051-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="27051-111">Use the following steps to turn it on:</span><span class="sxs-lookup"><span data-stu-id="27051-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="27051-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span><span class="sxs-lookup"><span data-stu-id="27051-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="27051-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span><span class="sxs-lookup"><span data-stu-id="27051-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="27051-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span><span class="sxs-lookup"><span data-stu-id="27051-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="27051-115">Find your directory under the **Directory** tab and click it.</span><span class="sxs-lookup"><span data-stu-id="27051-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="27051-116">Click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="27051-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="27051-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span><span class="sxs-lookup"><span data-stu-id="27051-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="27051-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span><span class="sxs-lookup"><span data-stu-id="27051-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Self-service password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="27051-120">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="27051-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="27051-121">You're done!</span><span class="sxs-lookup"><span data-stu-id="27051-121">You're done!</span></span>

<span data-ttu-id="27051-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span><span class="sxs-lookup"><span data-stu-id="27051-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="27051-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span><span class="sxs-lookup"><span data-stu-id="27051-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="27051-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="27051-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 


