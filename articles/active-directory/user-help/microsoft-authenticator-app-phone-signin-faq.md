---
title: Microsoft Authenticator phone sign-in - Azure and Microsoft accounts | Microsoft Docs
description: Use your phone to sign in to your Microsoft account instead of typing your password. This article answers FAQs about this feature.
services: active-directory
author: eross-msft
manager: mtillman
ms.service: active-directoary
ms.workload: identity
ms.component: user-help
ms.topic: conceptual
ms.date: 08/12/2017
ms.author: lizross
ms.reviewer: librown
ms.openlocfilehash: 3536c5da7833c32b583f1a510be43864c9107068
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968766"
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Sign in with your phone, not your password
The Microsoft Authenticator app helps you keep your accounts secure by performing two-step verification after you enter your password. But did you know that it can replace the password for your personal Microsoft account entirely?

This feature is available on iOS and Android devices, and works with personal Microsoft accounts.
 
## <a name="how-it-works"></a>How it works
Many of you use the Microsoft Authenticator app for two-step verification when you sign in to your Microsoft account. You type your password, then go to the app to either approve a notification or get a verification code. With phone sign-in, you skip the password and do all of your identity verification on your phone. Because phone sign-in is a type of two-step verification, you still need to provide a thing you know and a thing you have to verify your identity. The phone is still the thing you have, and your phone's PIN or biometric key is the thing you know.

## <a name="how-to-get-started"></a>How to get started
To sign in to your personal Microsoft account with your phone, follow these steps:

1. Enable phone sign-in for your account.

    - If you don't have the Microsoft Authenticator app yet, install and add your personal Microsoft account according to the steps on the [Microsoft Authenticator page](microsoft-authenticator-app-how-to.md). Newly added accounts are automatically enabled, so you're good to go.

    - If you already use Microsoft Authenticator for two-step verification, select your account from the app home page, and select **Enable phone sign-in** from the drop-down menu.

    >[!NOTE]
    >To protect your account, we require a PIN or biometric lock on your device. If you keep your phone unlocked, the app pops up a request asking you to set up a lock before enabling phone sign-in.

2. Most pages where you would normally enter your Microsoft account password have a link that says **Use an app instead**. Select this link to sign in with your phone.
 
3. Microsoft sends a notification to your phone. Approve the notification to sign in to your account.   
 
## <a name="faq"></a>FAQ

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>How is signing in with my phone more secure than typing a password?  
Today most people sign in to web sites or apps using a username and password.  Unfortunately, passwords are often lost, stolen, or guessed by hackers. When you set up the Microsoft Authenticator app to sign in, we generate a key on your phone that can unlock your account. We protect this key with the PIN or biometric that you already use on your phone.  When you sign in with your phone, this key is used to prove your identity securely with two factors – the phone itself, and your ability to unlock it.
 
The key used is similar to the keys used in Windows Hello and the FIDO Alliance UAF specifications. Your bio data is only used to protect the key locally, and is never sent to, or stored in, the cloud. 
 
### <a name="where-can-i-use-my-phone-to-replace-my-password-and-where-would-i-still-need-the-password"></a>Where can I use my phone to replace my password, and where would I still need the password?  
Today, the phone sign-in feature only works with web apps and services that are powered by personal Microsoft accounts, iOS or Android apps that use a personal Microsoft account, and apps on Windows 10 that use a personal Microsoft account. When you sign in to one of these web sites or apps, on the page where you usually enter your password there's a link that says, **Use an app instead**. 

Phone sign-in can't be used to unlock a Windows PC, XBOX, or any desktop versions of Microsoft apps such as Office apps at this time.
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>Does this replace two-step verification? Should I turn it off?   
Sometimes. We're working on expanding the scope of phone sign-in, but for now there are still places in the Microsoft ecosystem that don't support it. In those places, we're still using two-step verification for secure sign-in. For that reason, no, you shouldn't turn off two-step verification for your account.
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-to-approve-two-notifications"></a>Okay, if I keep two-step verification turned on for my account, do I have to approve two notifications?
No, you won't. Signing in to your Microsoft account with your phone counts as two-step verification. Instead of typing in your password, then approving a notification you prove your identity by knowing how to unlock your phone, and then approving a notification. We won't send you a second notification to approve.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>What if I lose my phone or don’t have it with me, how can I access my account?  
You can always click **Use a password instead** on the sign-in page to switch back to using your password. Keep in mind that if you use two-step verification, you still need a second method to verify your sign-in. That's why we strongly encourage you to make sure that you have extra, up-to-date security info on your account. You can manage your security info at https://account.live.com/proofs/manage.
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-to-entering-my-password"></a>How do I stop using this feature and go back to entering my password?
Click **Use a password instead** when you sign in. We remember your most recent choice, and offer that by default the next time you sign in. If you ever want to go back to signing in with your phone, click **Use an app instead**. 
 
### <a name="can-i-use-the-app-to-sign-in-to-all-my-accounts-with-microsoft"></a>Can I use the app to sign in to all my accounts with Microsoft?   
This functionality is only available for personal Microsoft accounts at this time. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>Can I sign into my PC with my phone?  
For your PC, we recommend signing in with Windows Hello on Windows 10 using your face, fingerprint, or a PIN.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>Can I sign in with my Windows Phone?  
At this time, we are not developing this functionality for the Microsoft Authenticator on Windows Phone. 

## <a name="next-steps"></a>Next steps
If you haven't downloaded the Microsoft Authenticator app, check it out. The app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), and phone sign-in is available on the Microsoft Authenticator app for [Android](http://go.microsoft.com/fwlink/?Linkid=825072) and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

If you have questions about the app in general, take a look at the [Microsoft Authenticator FAQs](microsoft-authenticator-app-faq.md)