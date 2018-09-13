---
title: Manage your two-step verification settings | Microsoft Docs
description: Manage how you use Azure Multi-Factor Authentication including changing your contact information or configuring your devices.
services: multi-factor-authentication
keywords: multifactor authentication client, authentication problem, correlation ID
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: e9b93e3cf359db0730410c27dde9ffb92ac08606
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550431"
---
# <a name="manage-your-settings-for-two-step-verification"></a>Manage your settings for two-step verification
This article answers questions about how to update settings for two-step verification or multi-factor authentication. If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.

## <a name="where-to-find-the-settings-page"></a>Where to find the settings page
Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.

If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions. Otherwise, the following instructions should work for everybody else. If you follow these steps but don't see the same options, that means that your work or school customized their own portal. Ask your admin for the link to your Azure Multi-Factor Authentication portal.

1. Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Select your account name in the top right, then select **profile**.  
3. Select **Additional security verification**.  

    ![Myapps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-manage/myapps1.png)
4. The Additional security verification page loads with your settings.

    ![Proofup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a>I want to change my phone number, or add a secondary number
It is important to configure a secondary authentication phone number.  Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.

> [!NOTE]
> If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).  

**To change your primary phone number:**  

1. On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.  
2. Select **Save**.  
3. If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.  

**To add a secondary phone number:**  

1. On the Additional security verification page, check the box next to **Alternate authentication phone.**  
2. Enter your secondary phone number in the text box.  
3. Select **Save** and your changes are finished.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Require two-step verification again on a device you've marked as trusted

Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser. If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices. 

1. On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.
2. The next time you sign in on any device, you'll be prompted to perform two-step verification. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a>How do I clean up Microsoft Authenticator from my old device and move to a new one?
When you uninstall the app from your device or reset the device, it does not remove the activation on the back end. For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Next steps
* Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)
* Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.


