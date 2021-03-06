---
title: Backup and recover with Microsoft Authenticator app - Azure Active Directory | Microsoft Docs
description: Learn how to backup and recover your account credentials, using the Microsoft Authenticator app.
services: active-directory
author: eross-msft
manager: mtillman
ms.component: user-help
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 03/28/2018
ms.author: lizross
ms.reviewer: olhaun
ms.openlocfilehash: 39ec7c979294860967deb3307f5d87112b762257
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867376"
---
# <a name="backup-and-recover-account-credentials-with-the-microsoft-authenticator-app"></a>Backup and recover account credentials with the Microsoft Authenticator app

**Applies to:**

- iOS devices

The Microsoft Authenticator app backs up your account credentials and related app settings, such as the order of your accounts, to the cloud. After backup, you can also use the app to recover your information on a new device, potentially avoiding getting locked out or having to recreate accounts.

>[!IMPORTANT]
> You need one personal Microsoft account and one iCloud account for each backup storage location. But within that storage location, you can back up several accounts. For example, you can have a personal account, a school account, and a third-party account like Facebook, Google, and so on.<br><br>Only your personal and 3rd-party account credentials are stored, which includes your user name and the account verification code that’s required to prove your identity. We don’t store any other information associated with your accounts, including emails or files. We also don’t associate or share your accounts in any way or with any other product or service. And finally, your IT admin won’t get any information about any of these accounts.

## <a name="back-up-your-account-credentials"></a>Back up your account credentials
Before you can back up your credentials, must have both:

- A personal [Microsoft account](https://account.microsoft.com/account) to act as your recovery account.

- An [iCloud account](https://www.icloud.com/) for the actual storage location. 

Requiring you to sign in to both accounts together provides stronger security for your backup information.

**To turn on Cloud backup**
-   On your iOS device, select **Settings**, select **Backup**, and then turn on **Auto backup**.

    Your account credentials are backed up to your iCloud account.

    ![iOS settings screen, showing the location of the auto backup settings](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-turn-on.png)

## <a name="recover-your-account-credentials-on-your-new-device"></a>Recover your account credentials on your new device
You can recover your account credentials from your iCloud account, using the same Microsoft recovery account you set up when you backed up your information.

### <a name="to-recover-your-information"></a>To recover your information
1.  On your iOS device, open the Microsoft Authenticator app, and select **Begin recovery** from the bottom of the screen.

    ![Microsoft Authenticator app, showing where to click Begin recovery](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-begin-recovery.png)

2.  Sign in to your recovery account, using the same personal Microsoft account you used during the backup process.

    Your account credentials are recovered to the new device.

After you finish your recovery, you might notice that your personal Microsoft account verification codes in the Microsoft Authenticator app are different between your old and new phones. The codes are different because each device has its own unique credential, but both are valid and work while signing in using the associated phone.

## <a name="recover-additional-accounts-requiring-more-verification"></a>Recover additional accounts requiring more verification
If you use push notifications with your personal, work, or school accounts, you'll get an on-screen alert that says you must provide additional verification before you can recover your information. Because push notifications require using a credential that’s tied to your specific device and never sent over the network, you must prove your identity before the credential is created on your device.

For personal Microsoft accounts, you can prove your identity by entering your password along with an alternate email or phone number. For work or school accounts, you must scan a QR code given to you by your account provider.

### <a name="to-provide-additional-verification-for-personal-accounts"></a>To provide additional verification for personal accounts
1.  In the **Accounts** screen of the Microsoft Authenticator app, select the drop-down arrow next to the account you want to recover.

    ![Microsoft Authenticator app, showing the available accounts with their associated drop-down arrows](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-arrow.png)

2.  Select **Sign in to recover**, type your password, and then confirm your email address or phone number as additional verification.

    ![Microsoft Authenticator app, allowing you to enter your sign-in info](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-sign-in.png)

### <a name="to-provide-additional-verification-for-work-or-school-accounts"></a>To provide additional verification for work or school accounts
1.  In the **Accounts** screen of the Microsoft Authenticator app, select the drop-down arrow next to the account you want to recover.

    ![Microsoft Authenticator app, showing the available accounts with their associated drop-down arrows](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-additonal-accts.png)

2.  Select **Scan QR code to recover**, and then scan the QR code provided by your admin.

    ![Microsoft Authenticator app, allowing you to scan your QR code](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-scan-qr-code.png)

    >[!NOTE]
    >For more info about how to get a QR code, see the [How to add accounts section of the Get started with the Microsoft Authenticator app](https://docs.microsoft.com/azure/active-directory/user-help/microsoft-authenticator-app-how-to#add-accounts-to-the-app) article.

## <a name="troubleshooting-backup-and-recovery-problems"></a>Troubleshooting backup and recovery problems
There are a few reasons why your backup might not be available:

-   **Changing operating systems.** Your backup is stored in the cloud storage option provided by your phone’s operating system, which means the backup is unavailable if you switch between Android and iOS. In this situation, you must manually recreate your account within the app.

-   **Network or password problems.** Make sure you’re connected to a network and signed into your iCloud account using the same AppleID you used on your last iPhone.

-   **Accidental deletion.** It’s possible that you deleted your backup account from your previous device or while managing your cloud storage account. In this situation, you must manually recreate your account within the app.

-   **Existing Microsoft Authenticator accounts.** If you've already set up accounts in the Microsoft Authenticator app, the app won't be able to recover your backed-up accounts. Preventing recovery helps ensure that your account details aren't overwritten with out-of-date information. In this situation, you must remove any existing account information from the existing accounts set up in your Authenticator app before you can recover your backup.

## <a name="next-steps"></a>Next steps
Now that you've backed up and recovered your account credentials to your new device, you can continue to use the Microsoft Authenticator app to verify your identity.

## <a name="related-topics"></a>Related topics
- [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md)  

- [Microsoft Authenticator app FAQ](microsoft-authenticator-app-faq.md)

- [Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)
