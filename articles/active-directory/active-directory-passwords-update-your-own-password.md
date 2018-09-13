---
title: 'Azure AD: Reset Your Password | Microsoft Docs'
description: Use self-service password reset to regain access to your account
services: active-directory
keywords: Active directory password management, password management, Azure AD self service password reset, SSPR
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 7ba69b18-317a-4a62-afa3-924c4ea8fb49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: 2b10727b5329ed697af5d0aec0ea1fe07c2ab4d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549400"
---
# <a name="help-i-forgot-my-password"></a>Help I forgot my password

Step 1... don't panic

If the following scenarios apply to you, we can help

* You are unsure how to access your account and can't remember your password
* A password was not assigned and your administrator sent you here

## <a name="unlock-my-account"></a>Unlock my account

If you are here to unlock your account, follow the steps below. When you see **Chose a new password** at step 6 below, you are able to unlock or change your password and be unlocked.

## <a name="reset-my-password"></a>Reset my password

To get back into your account, follow these steps below.
1. From any work or school sign-in page, click the **Can't access your account? link** then **Work or school account** or go directly to the [password reset page](https://passwordreset.microsoftonline.com/)

    ![Can't access your account?][Login]

2. Enter your work or school **User ID** and prove you aren't a robot by passing the CAPTCHA challenge and entering the text presented to you and click **Next**

   > [!NOTE]
   > If your administrator has not enabled this functionality, you are presented with a "contact your administrator" link at this point so that your administrator can provide assistance via email or a web portal of their own.
   >

3. Depending on how your administrator has configured things you will see one or more of the following
    * **Email my alternate email** - Sends an email with a 6-digit code to either your alternate email or your authentication email (you choose).
    * **Text my mobile phone** - Texts your phone with a 6-digit code to either your mobile phone or your authentication phone (you choose).
    * **Call my mobile phone** - Calls either your mobile phone or your authentication phone (you choose). Press the # key to verify the call.
    * **Call my office phone** - Calls your office phone. Press the # key to verify the call.
    * **Answer my security questions** - Displays your preregistered security questions for you to answer.
4. Populate the required fields with answers to the challenge information and click **Next**

    ![Verify your authentication data][Verification]

5. Your administrator may require an additional verification step and you may have to repeat step 4 again with a different option
6. On the **Choose a new password** page, enter a new password that meets your organizations requirements, confirm your password and then click **Finish**

    ![Change your password][Change]

7. When you see **Your password has been reset**, you can sign in with your new password.

    ![Your password has been reset][Complete]

After using this method to unlock or reset your password, you may receive an email confirming this process has been completed that comes from an account like "Microsoft on behalf of Your Organization Here". If you get an email like this, and did not use self-service password reset to regain access to your account contact your administrator.

## <a name="change-my-password"></a>Change my password

If you know your password already and need to change it, try the steps that follow

### <a name="change-your-password-from-the-office-365-portal"></a>Change your password from the Office 365 portal

1. Click on your profile on the upper right side click **View account**
2. **Security & privacy**
3. **Password**
4. Enter your old password and set and confirm your new password
5. **Submit**

### <a name="change-your-password-from-the-azure-access-panel"></a>Change your password from the Azure Access Panel

1. Sign in to the [Azure Access Portal](https://myapps.microsoft.com/) using your existing password
2. Click on your profile on the upper right side then click **Profile**
3. **Change password**
4. Enter your old password and set and confirm your new password
5. **Submit**

## <a name="next-steps"></a>Next Steps

* [How to register to use self-service password reset](active-directory-passwords-reset-register.md)
* [Password reset registration page](http://aka.ms/ssprsetup)
* [Password reset portal](https://passwordreset.microsoftonline.com/)

[Login]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-update-your-own-password/reset-1-login.png "Login page Can't access your account?"
[Verification]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-update-your-own-password/reset-2-verification.png "Verify your authentication data"
[Change]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-update-your-own-password/reset-3-change.png "Change your password"
[Complete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-update-your-own-password/reset-4-complete.png "Password has been reset"




