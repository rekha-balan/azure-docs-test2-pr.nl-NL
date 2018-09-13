---
title: Microsoft Authenticator app for mobile phones | Microsoft Docs
description: Learn how to upgrade to the latest version of Azure Authenticator.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: curtland
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 4adc5a76a20b7f3932b921bf1180f68251f5b44a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551072"
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="cfbd0-103">Get started with the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="cfbd0-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="cfbd0-104">The Microsoft Authenticator app provides an additional level of security in your Azure account (for example, bsimon@contoso.onmicrosoft.com), your on-premises work account (for example, bsimon@contoso.com), or your Microsoft account (for example, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="cfbd0-104">The Microsoft Authenticator app provides an additional level of security in your Azure account (for example, bsimon@contoso.onmicrosoft.com), your on-premises work account (for example, bsimon@contoso.com), or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="cfbd0-105">The app works in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="cfbd0-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="cfbd0-106">**Notification**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-106">**Notification**.</span></span> <span data-ttu-id="cfbd0-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="cfbd0-108">Simply view the notification, and if it's legitimate, select **Verify**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="cfbd0-109">Otherwise, you can select **Deny**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-109">Otherwise, you can select **Deny**.</span></span> <span data-ttu-id="cfbd0-110">For information about denying notifications, see How to use the Deny and Report Fraud Feature for Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-110">For information about denying notifications, see How to use the Deny and Report Fraud Feature for Multi-Factor Authentication.</span></span>
* <span data-ttu-id="cfbd0-111">**Password with verification code**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-111">**Password with verification code**.</span></span> <span data-ttu-id="cfbd0-112">The app can be used as a software token to generate an OAuth verification code.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-112">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="cfbd0-113">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-113">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="cfbd0-114">The verification code provides a second form of authentication.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-114">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="cfbd0-115">The Microsoft Authenticator app replaces the Azure Authenticator app.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-115">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span>  <span data-ttu-id="cfbd0-116">The Azure Authenticator app will continue to work, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-116">The Azure Authenticator app will continue to work, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="install-the-app"></a><span data-ttu-id="cfbd0-117">Install the app</span><span class="sxs-lookup"><span data-stu-id="cfbd0-117">Install the app</span></span>
<span data-ttu-id="cfbd0-118">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="cfbd0-118">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="cfbd0-119">Add accounts to the app</span><span class="sxs-lookup"><span data-stu-id="cfbd0-119">Add accounts to the app</span></span>
<span data-ttu-id="cfbd0-120">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-120">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures.</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="cfbd0-121">Add a personal Microsoft account to the app</span><span class="sxs-lookup"><span data-stu-id="cfbd0-121">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="cfbd0-122">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc), all you have to do is sign in to your account in the Microsoft Authenticator app.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-122">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="cfbd0-123">Add a work or school account to the app using the QR code scanner</span><span class="sxs-lookup"><span data-stu-id="cfbd0-123">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="cfbd0-124">Go to the security verification settings screen.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-124">Go to the security verification settings screen.</span></span>  <span data-ttu-id="cfbd0-125">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="cfbd0-125">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="cfbd0-126">Check the box next to **Azure Authenticator app** then select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-126">Check the box next to **Azure Authenticator app** then select **Configure**.</span></span>

    ![The Configure button on the security verification settings screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="cfbd0-128">This brings up a screen with a QR code on it.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-128">This brings up a screen with a QR code on it.</span></span>

    ![Screen that provides the QR code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="cfbd0-130">Open the Microsoft Authenticator app.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-130">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="cfbd0-131">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-131">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="cfbd0-132">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-132">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="cfbd0-133">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="cfbd0-133">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="cfbd0-134">When the app shows your account name with a six-digit code underneath it, you're done.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-134">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Accounts screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="cfbd0-136">Add an account to the app manually</span><span class="sxs-lookup"><span data-stu-id="cfbd0-136">Add an account to the app manually</span></span>
1. <span data-ttu-id="cfbd0-137">Go to the security verification settings screen.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-137">Go to the security verification settings screen.</span></span>  <span data-ttu-id="cfbd0-138">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="cfbd0-138">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="cfbd0-139">Select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-139">Select **Configure**.</span></span>

    ![The Configure button on the security verification settings screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="cfbd0-141">This brings up a screen with a QR code on it.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-141">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="cfbd0-142">Note the code and URL.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-142">Note the code and URL.</span></span>

    ![Screen that provides the QR code and URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="cfbd0-144">Open the Microsoft Authenticator app.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-144">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="cfbd0-145">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-145">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="cfbd0-146">In the scanner, select **enter code manually**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-146">In the scanner, select **enter code manually**.</span></span>

    ![Screen for scanning a QR code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="cfbd0-148">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-148">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Screen for entering code and URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="cfbd0-150">When the app shows your account name with a six-digit code underneath it, you're done.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-150">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Accounts screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="cfbd0-152">Add an account to the app using Touch ID</span><span class="sxs-lookup"><span data-stu-id="cfbd0-152">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="cfbd0-153">The Microsoft Authenticator app on iOS supports Touch ID.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-153">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="cfbd0-154">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-154">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="cfbd0-155">With Touch ID, iOS users don’t need to enter a PIN.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-155">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="cfbd0-156">Instead, they can scan their fingerprint and select **Approve**.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-156">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="cfbd0-157">Setting up Touch ID with Microsoft Authenticator is simple.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-157">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="cfbd0-158">You complete a normal verification challenge with a PIN.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-158">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="cfbd0-159">If your device supports Touch ID, Microsoft Authenticator will set it up automatically for that account.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-159">If your device supports Touch ID, Microsoft Authenticator will set it up automatically for that account.</span></span>

![Verification of Touch ID setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="cfbd0-161">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-161">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Push notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/authenticator-app-how-to/touchid2.png)











