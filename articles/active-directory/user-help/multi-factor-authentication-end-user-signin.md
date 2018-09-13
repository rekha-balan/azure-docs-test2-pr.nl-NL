---
title: Azure MFA sign-in with two-step verification | Microsoft Docs
description: This page will provide you guidance on where to go to see the various sign-in methods available with Azure MFA.
keywords: user authentication, sign-in experience, sign-in with mobile phone, sign-in with office phone
services: active-directory
author: eross-msft
manager: mtillman
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.workload: identity
ms.service: active-directory
ms.component: user-help
ms.topic: conceptual
ms.date: 04/02/2017
ms.author: lizross
ms.reviewer: librown
ms.openlocfilehash: e7886d3c8aa1ef9ee1e392030aabf0d187568e24
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869060"
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="643d4-104">The sign-in experience with Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="643d4-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="643d4-105">The purpose of this article is to walk through a typical sign-in experience.</span><span class="sxs-lookup"><span data-stu-id="643d4-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="643d4-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="643d4-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="643d4-107">What will your sign-in experience be?</span><span class="sxs-lookup"><span data-stu-id="643d4-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="643d4-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span><span class="sxs-lookup"><span data-stu-id="643d4-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="643d4-109">Choose the option that best describes what you are doing:</span><span class="sxs-lookup"><span data-stu-id="643d4-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="643d4-110">How do you sign in?</span><span class="sxs-lookup"><span data-stu-id="643d4-110">How do you sign in?</span></span> |
| --- |
| [<span data-ttu-id="643d4-111">With a phone call to my mobile or office phone</span><span class="sxs-lookup"><span data-stu-id="643d4-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="643d4-112">With a text to my mobile phone</span><span class="sxs-lookup"><span data-stu-id="643d4-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="643d4-113">With notifications from the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="643d4-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="643d4-114">With verification codes from the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="643d4-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="643d4-115">With an alternate method, because I can't use my preferred method right now</span><span class="sxs-lookup"><span data-stu-id="643d4-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="643d4-116">Signing in with a phone call</span><span class="sxs-lookup"><span data-stu-id="643d4-116">Signing in with a phone call</span></span>
<span data-ttu-id="643d4-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span><span class="sxs-lookup"><span data-stu-id="643d4-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="643d4-118">Sign in to an application or service such as Office 365 using your username and password.</span><span class="sxs-lookup"><span data-stu-id="643d4-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="643d4-119">Microsoft calls you.</span><span class="sxs-lookup"><span data-stu-id="643d4-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="643d4-120">Answer the phone and hit the # key.</span><span class="sxs-lookup"><span data-stu-id="643d4-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="643d4-121">Signing in with a text message</span><span class="sxs-lookup"><span data-stu-id="643d4-121">Signing in with a text message</span></span>
<span data-ttu-id="643d4-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span><span class="sxs-lookup"><span data-stu-id="643d4-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="643d4-123">Sign in to an application or service such as Office 365 using your username and password.</span><span class="sxs-lookup"><span data-stu-id="643d4-123">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="643d4-124">Microsoft sends you a text message that contains a number code.</span><span class="sxs-lookup"><span data-stu-id="643d4-124">Microsoft sends you a text message that contains a number code.</span></span>
3. <span data-ttu-id="643d4-125">Enter the code in the box provided on the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="643d4-125">Enter the code in the box provided on the sign-in page.</span></span>

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="643d4-126">Signing in with the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="643d4-126">Signing in with the Microsoft Authenticator app</span></span>
<span data-ttu-id="643d4-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span><span class="sxs-lookup"><span data-stu-id="643d4-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="643d4-128">There are two different ways to use the app.</span><span class="sxs-lookup"><span data-stu-id="643d4-128">There are two different ways to use the app.</span></span> <span data-ttu-id="643d4-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span><span class="sxs-lookup"><span data-stu-id="643d4-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="643d4-130">To sign in with a notification from the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="643d4-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="643d4-131">Sign in to an application or service such as Office 365 using your username and password.</span><span class="sxs-lookup"><span data-stu-id="643d4-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="643d4-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span><span class="sxs-lookup"><span data-stu-id="643d4-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Microsoft sends notification](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="643d4-134">Open the notification on your phone and select the **Verify** key.</span><span class="sxs-lookup"><span data-stu-id="643d4-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="643d4-135">If your company requires a PIN, enter it here.</span><span class="sxs-lookup"><span data-stu-id="643d4-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="643d4-136">You should now be signed in.</span><span class="sxs-lookup"><span data-stu-id="643d4-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="643d4-137">To sign in using a verification code with the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="643d4-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="643d4-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span><span class="sxs-lookup"><span data-stu-id="643d4-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="643d4-139">This number changes every 30 seconds so that you don't use the same number twice.</span><span class="sxs-lookup"><span data-stu-id="643d4-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="643d4-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span><span class="sxs-lookup"><span data-stu-id="643d4-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span>

1. <span data-ttu-id="643d4-141">Sign in to an application or service such as Office 365 using your username and password.</span><span class="sxs-lookup"><span data-stu-id="643d4-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="643d4-142">Microsoft prompts you for a verification code.</span><span class="sxs-lookup"><span data-stu-id="643d4-142">Microsoft prompts you for a verification code.</span></span>

  ![Enter verification code](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="643d4-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span><span class="sxs-lookup"><span data-stu-id="643d4-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="643d4-145">Signing in with an alternate method</span><span class="sxs-lookup"><span data-stu-id="643d4-145">Signing in with an alternate method</span></span>
<span data-ttu-id="643d4-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span><span class="sxs-lookup"><span data-stu-id="643d4-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="643d4-147">This situation is why we recommend that you set up backup methods for your account.</span><span class="sxs-lookup"><span data-stu-id="643d4-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="643d4-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span><span class="sxs-lookup"><span data-stu-id="643d4-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="643d4-149">Sign in to an application or service such as Office 365 using your username and password.</span><span class="sxs-lookup"><span data-stu-id="643d4-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="643d4-150">Select **Use a different verification option**.</span><span class="sxs-lookup"><span data-stu-id="643d4-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="643d4-151">You see different verification options based on how many you have setup.</span><span class="sxs-lookup"><span data-stu-id="643d4-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="643d4-152">Choose an alternate method and sign in.</span><span class="sxs-lookup"><span data-stu-id="643d4-152">Choose an alternate method and sign in.</span></span>

  ![Use alternate method](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="643d4-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="643d4-154">Next steps</span></span>

<span data-ttu-id="643d4-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="643d4-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="643d4-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="643d4-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="643d4-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span><span class="sxs-lookup"><span data-stu-id="643d4-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span>
