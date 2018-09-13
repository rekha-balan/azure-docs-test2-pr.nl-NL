---
title: Troubleshoot two-step verification | Microsoft Docs
description: This document will provide users information on what to do if they run into an issue with Azure Multi-Factor Authentication.
services: multi-factor-authentication
keywords: multifactor authentication client, authentication problem, correlation ID
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: dc68780d7d5f1c7f476da545e4ec14e3393c1341
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549095"
---
# <a name="having-trouble-with-two-step-verification"></a><span data-ttu-id="85a6d-104">Having trouble with two-step verification</span><span class="sxs-lookup"><span data-stu-id="85a6d-104">Having trouble with two-step verification</span></span>
<span data-ttu-id="85a6d-105">This article discusses some issues that you may experience with two-step verification.</span><span class="sxs-lookup"><span data-stu-id="85a6d-105">This article discusses some issues that you may experience with two-step verification.</span></span> <span data-ttu-id="85a6d-106">If the issue you're having is not included here, please provide detailed feedback in the comments section so that we can improve.</span><span class="sxs-lookup"><span data-stu-id="85a6d-106">If the issue you're having is not included here, please provide detailed feedback in the comments section so that we can improve.</span></span>

## <a name="i-lost-my-phone-or-it-was-stolen"></a><span data-ttu-id="85a6d-107">I lost my phone or it was stolen</span><span class="sxs-lookup"><span data-stu-id="85a6d-107">I lost my phone or it was stolen</span></span>
<span data-ttu-id="85a6d-108">There are two ways to get back in to your account.</span><span class="sxs-lookup"><span data-stu-id="85a6d-108">There are two ways to get back in to your account.</span></span> <span data-ttu-id="85a6d-109">The first is to sign in using your alternate authentication phone number, if you have set one up.</span><span class="sxs-lookup"><span data-stu-id="85a6d-109">The first is to sign in using your alternate authentication phone number, if you have set one up.</span></span> <span data-ttu-id="85a6d-110">The second is to ask your administrator to clear your settings.</span><span class="sxs-lookup"><span data-stu-id="85a6d-110">The second is to ask your administrator to clear your settings.</span></span>

<span data-ttu-id="85a6d-111">If your phone was lost or stolen, we also recommend that you have your administrator reset your app passwords and clear any remembered devices.</span><span class="sxs-lookup"><span data-stu-id="85a6d-111">If your phone was lost or stolen, we also recommend that you have your administrator reset your app passwords and clear any remembered devices.</span></span> <span data-ttu-id="85a6d-112">If your admin isn't sure how to accomplish this, point them to this article: [Manage users and devices](../multi-factor-authentication-manage-users-and-devices.md).</span><span class="sxs-lookup"><span data-stu-id="85a6d-112">If your admin isn't sure how to accomplish this, point them to this article: [Manage users and devices](../multi-factor-authentication-manage-users-and-devices.md).</span></span>

### <a name="use-an-alternate-phone-number"></a><span data-ttu-id="85a6d-113">Use an alternate phone number</span><span class="sxs-lookup"><span data-stu-id="85a6d-113">Use an alternate phone number</span></span>
<span data-ttu-id="85a6d-114">If you have set up multiple verification options, including a secondary phone number or an authenticator app on a different device, you can use one of these to sign in.</span><span class="sxs-lookup"><span data-stu-id="85a6d-114">If you have set up multiple verification options, including a secondary phone number or an authenticator app on a different device, you can use one of these to sign in.</span></span>

<span data-ttu-id="85a6d-115">To sign in using the alternate phone number, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="85a6d-115">To sign in using the alternate phone number, follow these steps:</span></span>

1. <span data-ttu-id="85a6d-116">Sign in as you normally would.</span><span class="sxs-lookup"><span data-stu-id="85a6d-116">Sign in as you normally would.</span></span>
2. <span data-ttu-id="85a6d-117">When prompted to further verify your account, choose **Use a different verification option**.</span><span class="sxs-lookup"><span data-stu-id="85a6d-117">When prompted to further verify your account, choose **Use a different verification option**.</span></span>
   
    ![Different Verification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-manage/differentverification.png)
3. <span data-ttu-id="85a6d-119">Select the phone number that you have access to.</span><span class="sxs-lookup"><span data-stu-id="85a6d-119">Select the phone number that you have access to.</span></span>
   
    ![Alternate phone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-manage/altphone2.png)
4. <span data-ttu-id="85a6d-121">After you're back in your account, [manage your settings](multi-factor-authentication-end-user-manage-settings.md) to change your authentication phone number.</span><span class="sxs-lookup"><span data-stu-id="85a6d-121">After you're back in your account, [manage your settings](multi-factor-authentication-end-user-manage-settings.md) to change your authentication phone number.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85a6d-122">It is important to configure a secondary authentication phone number.</span><span class="sxs-lookup"><span data-stu-id="85a6d-122">It is important to configure a secondary authentication phone number.</span></span> <span data-ttu-id="85a6d-123">If your primary phone number and your mobile app are on the same phone, you need a third option if your phone is lost or stolen.</span><span class="sxs-lookup"><span data-stu-id="85a6d-123">If your primary phone number and your mobile app are on the same phone, you need a third option if your phone is lost or stolen.</span></span>   

### <a name="clear-your-settings"></a><span data-ttu-id="85a6d-124">Clear your settings</span><span class="sxs-lookup"><span data-stu-id="85a6d-124">Clear your settings</span></span>
<span data-ttu-id="85a6d-125">If you have not configured a secondary authentication phone number, then you will have to contact your administrator for help.</span><span class="sxs-lookup"><span data-stu-id="85a6d-125">If you have not configured a secondary authentication phone number, then you will have to contact your administrator for help.</span></span> <span data-ttu-id="85a6d-126">Have them clear your settings so the next time you sign in, you will be prompted to [set up your account](multi-factor-authentication-end-user-first-time.md) again.</span><span class="sxs-lookup"><span data-stu-id="85a6d-126">Have them clear your settings so the next time you sign in, you will be prompted to [set up your account](multi-factor-authentication-end-user-first-time.md) again.</span></span>

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a><span data-ttu-id="85a6d-127">I am not receiving a text or call on my phone</span><span class="sxs-lookup"><span data-stu-id="85a6d-127">I am not receiving a text or call on my phone</span></span>
<span data-ttu-id="85a6d-128">There are several reasons why you may try to sign in, but not receive the text or phone call.</span><span class="sxs-lookup"><span data-stu-id="85a6d-128">There are several reasons why you may try to sign in, but not receive the text or phone call.</span></span> <span data-ttu-id="85a6d-129">If you've successfully received texts or phone calls to your phone in the past, then this is probably an issue with the phone provider, not your account.</span><span class="sxs-lookup"><span data-stu-id="85a6d-129">If you've successfully received texts or phone calls to your phone in the past, then this is probably an issue with the phone provider, not your account.</span></span> <span data-ttu-id="85a6d-130">Make sure that you have good cell signal, and if you are trying to receive a text message make sure that your phone and service plan support text messages.</span><span class="sxs-lookup"><span data-stu-id="85a6d-130">Make sure that you have good cell signal, and if you are trying to receive a text message make sure that your phone and service plan support text messages.</span></span>

<span data-ttu-id="85a6d-131">If you've waited several minutes for a text or call, the fastest way to get into your account is to try a different option.</span><span class="sxs-lookup"><span data-stu-id="85a6d-131">If you've waited several minutes for a text or call, the fastest way to get into your account is to try a different option.</span></span>

1. <span data-ttu-id="85a6d-132">Select **Use a different verification option** on the page that's waiting for your verification.</span><span class="sxs-lookup"><span data-stu-id="85a6d-132">Select **Use a different verification option** on the page that's waiting for your verification.</span></span>
   
    ![Different Verification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. <span data-ttu-id="85a6d-134">Select the phone number or delivery method you want to use.</span><span class="sxs-lookup"><span data-stu-id="85a6d-134">Select the phone number or delivery method you want to use.</span></span>
   
    <span data-ttu-id="85a6d-135">If you received multiple verification codes, only the newest one works.</span><span class="sxs-lookup"><span data-stu-id="85a6d-135">If you received multiple verification codes, only the newest one works.</span></span>

<span data-ttu-id="85a6d-136">If you don’t have another method configured, contact your admin and ask them to clear your settings.</span><span class="sxs-lookup"><span data-stu-id="85a6d-136">If you don’t have another method configured, contact your admin and ask them to clear your settings.</span></span> <span data-ttu-id="85a6d-137">The next time you sign in, you will be prompted to [set up multi-factor authentication](multi-factor-authentication-end-user-first-time.md) again.</span><span class="sxs-lookup"><span data-stu-id="85a6d-137">The next time you sign in, you will be prompted to [set up multi-factor authentication](multi-factor-authentication-end-user-first-time.md) again.</span></span>

<span data-ttu-id="85a6d-138">If you often have delays due to bad cell signal, we recommend you use the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) on your smartphone.</span><span class="sxs-lookup"><span data-stu-id="85a6d-138">If you often have delays due to bad cell signal, we recommend you use the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) on your smartphone.</span></span> <span data-ttu-id="85a6d-139">The app can generate random security codes that you use to sign in, and these codes don't require any cell signal or internet connection.</span><span class="sxs-lookup"><span data-stu-id="85a6d-139">The app can generate random security codes that you use to sign in, and these codes don't require any cell signal or internet connection.</span></span>

## <a name="app-passwords-are-not-working"></a><span data-ttu-id="85a6d-140">App passwords are not working</span><span class="sxs-lookup"><span data-stu-id="85a6d-140">App passwords are not working</span></span>
<span data-ttu-id="85a6d-141">First, make sure that you have entered the app password correctly.</span><span class="sxs-lookup"><span data-stu-id="85a6d-141">First, make sure that you have entered the app password correctly.</span></span>  <span data-ttu-id="85a6d-142">If it is still not working try signing-in and [create a new app password](multi-factor-authentication-end-user-app-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="85a6d-142">If it is still not working try signing-in and [create a new app password](multi-factor-authentication-end-user-app-passwords.md).</span></span>  <span data-ttu-id="85a6d-143">If this does not work, contact your administrator and have them [delete your existing app passwords](../multi-factor-authentication-manage-users-and-devices.md) and then you can create a new one.</span><span class="sxs-lookup"><span data-stu-id="85a6d-143">If this does not work, contact your administrator and have them [delete your existing app passwords](../multi-factor-authentication-manage-users-and-devices.md) and then you can create a new one.</span></span>

## <a name="i-didnt-find-an-answer-to-my-problem"></a><span data-ttu-id="85a6d-144">I didn't find an answer to my problem.</span><span class="sxs-lookup"><span data-stu-id="85a6d-144">I didn't find an answer to my problem.</span></span>
<span data-ttu-id="85a6d-145">If you've tried these troubleshooting steps but are still running into problems, contact your administrator or the person who set up multi-factor authentication for you.</span><span class="sxs-lookup"><span data-stu-id="85a6d-145">If you've tried these troubleshooting steps but are still running into problems, contact your administrator or the person who set up multi-factor authentication for you.</span></span> <span data-ttu-id="85a6d-146">They should be able to assist you.</span><span class="sxs-lookup"><span data-stu-id="85a6d-146">They should be able to assist you.</span></span>

<span data-ttu-id="85a6d-147">Also, you can post a question on the [Azure AD Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD) or [contact support](https://support.microsoft.com/contactus) and we'll respond to your problem as soon as we can.</span><span class="sxs-lookup"><span data-stu-id="85a6d-147">Also, you can post a question on the [Azure AD Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD) or [contact support](https://support.microsoft.com/contactus) and we'll respond to your problem as soon as we can.</span></span>

<span data-ttu-id="85a6d-148">If you contact support, include the following information:</span><span class="sxs-lookup"><span data-stu-id="85a6d-148">If you contact support, include the following information:</span></span>

* <span data-ttu-id="85a6d-149">**User ID** – What's the email address you tried to sign in with?</span><span class="sxs-lookup"><span data-stu-id="85a6d-149">**User ID** – What's the email address you tried to sign in with?</span></span>
* <span data-ttu-id="85a6d-150">**General description of the error** – what exact error message did you see?</span><span class="sxs-lookup"><span data-stu-id="85a6d-150">**General description of the error** – what exact error message did you see?</span></span>  <span data-ttu-id="85a6d-151">If there was no error message, describe the unexpected behavior you noticed, in detail.</span><span class="sxs-lookup"><span data-stu-id="85a6d-151">If there was no error message, describe the unexpected behavior you noticed, in detail.</span></span>
* <span data-ttu-id="85a6d-152">**Page** – what page were you on when you saw the error (include the URL)?</span><span class="sxs-lookup"><span data-stu-id="85a6d-152">**Page** – what page were you on when you saw the error (include the URL)?</span></span>
* <span data-ttu-id="85a6d-153">**ErrorCode** - the specific error code you are receiving.</span><span class="sxs-lookup"><span data-stu-id="85a6d-153">**ErrorCode** - the specific error code you are receiving.</span></span>
* <span data-ttu-id="85a6d-154">**SessionId** - the specific session id you are receiving.</span><span class="sxs-lookup"><span data-stu-id="85a6d-154">**SessionId** - the specific session id you are receiving.</span></span>
* <span data-ttu-id="85a6d-155">**Correlation ID** – what was the correlation id code generated when the user saw the error.</span><span class="sxs-lookup"><span data-stu-id="85a6d-155">**Correlation ID** – what was the correlation id code generated when the user saw the error.</span></span>
* <span data-ttu-id="85a6d-156">**Timestamp** – what was the precise date and time you saw the error (include the timezone)?</span><span class="sxs-lookup"><span data-stu-id="85a6d-156">**Timestamp** – what was the precise date and time you saw the error (include the timezone)?</span></span>

<span data-ttu-id="85a6d-157">Much of this information can be found on your sign-in page.</span><span class="sxs-lookup"><span data-stu-id="85a6d-157">Much of this information can be found on your sign-in page.</span></span> <span data-ttu-id="85a6d-158">When you don't verify your sign-in in time, select **View details**.</span><span class="sxs-lookup"><span data-stu-id="85a6d-158">When you don't verify your sign-in in time, select **View details**.</span></span>

![Sign in error details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-troubleshoot/view_details.png)

<span data-ttu-id="85a6d-160">Including this information helps us to solve your problem as quickly as possible.</span><span class="sxs-lookup"><span data-stu-id="85a6d-160">Including this information helps us to solve your problem as quickly as possible.</span></span>

## <a name="related-topics"></a><span data-ttu-id="85a6d-161">Related topics</span><span class="sxs-lookup"><span data-stu-id="85a6d-161">Related topics</span></span>
* [<span data-ttu-id="85a6d-162">Manage your settings for two-step verification</span><span class="sxs-lookup"><span data-stu-id="85a6d-162">Manage your settings for two-step verification</span></span>](multi-factor-authentication-end-user-manage-settings.md)  
* [<span data-ttu-id="85a6d-163">Microsoft Authenticator application FAQ</span><span class="sxs-lookup"><span data-stu-id="85a6d-163">Microsoft Authenticator application FAQ</span></span>](microsoft-authenticator-app-faq.md)





