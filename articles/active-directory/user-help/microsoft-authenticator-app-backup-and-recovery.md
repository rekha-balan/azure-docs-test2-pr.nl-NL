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
# <a name="backup-and-recover-account-credentials-with-the-microsoft-authenticator-app"></a><span data-ttu-id="24d84-103">Backup and recover account credentials with the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="24d84-103">Backup and recover account credentials with the Microsoft Authenticator app</span></span>

<span data-ttu-id="24d84-104">**Applies to:**</span><span class="sxs-lookup"><span data-stu-id="24d84-104">**Applies to:**</span></span>

- <span data-ttu-id="24d84-105">iOS devices</span><span class="sxs-lookup"><span data-stu-id="24d84-105">iOS devices</span></span>

<span data-ttu-id="24d84-106">The Microsoft Authenticator app backs up your account credentials and related app settings, such as the order of your accounts, to the cloud.</span><span class="sxs-lookup"><span data-stu-id="24d84-106">The Microsoft Authenticator app backs up your account credentials and related app settings, such as the order of your accounts, to the cloud.</span></span> <span data-ttu-id="24d84-107">After backup, you can also use the app to recover your information on a new device, potentially avoiding getting locked out or having to recreate accounts.</span><span class="sxs-lookup"><span data-stu-id="24d84-107">After backup, you can also use the app to recover your information on a new device, potentially avoiding getting locked out or having to recreate accounts.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="24d84-108">You need one personal Microsoft account and one iCloud account for each backup storage location.</span><span class="sxs-lookup"><span data-stu-id="24d84-108">You need one personal Microsoft account and one iCloud account for each backup storage location.</span></span> <span data-ttu-id="24d84-109">But within that storage location, you can back up several accounts.</span><span class="sxs-lookup"><span data-stu-id="24d84-109">But within that storage location, you can back up several accounts.</span></span> <span data-ttu-id="24d84-110">For example, you can have a personal account, a school account, and a third-party account like Facebook, Google, and so on.</span><span class="sxs-lookup"><span data-stu-id="24d84-110">For example, you can have a personal account, a school account, and a third-party account like Facebook, Google, and so on.</span></span><br><br><span data-ttu-id="24d84-111">Only your personal and 3rd-party account credentials are stored, which includes your user name and the account verification code that’s required to prove your identity.</span><span class="sxs-lookup"><span data-stu-id="24d84-111">Only your personal and 3rd-party account credentials are stored, which includes your user name and the account verification code that’s required to prove your identity.</span></span> <span data-ttu-id="24d84-112">We don’t store any other information associated with your accounts, including emails or files.</span><span class="sxs-lookup"><span data-stu-id="24d84-112">We don’t store any other information associated with your accounts, including emails or files.</span></span> <span data-ttu-id="24d84-113">We also don’t associate or share your accounts in any way or with any other product or service.</span><span class="sxs-lookup"><span data-stu-id="24d84-113">We also don’t associate or share your accounts in any way or with any other product or service.</span></span> <span data-ttu-id="24d84-114">And finally, your IT admin won’t get any information about any of these accounts.</span><span class="sxs-lookup"><span data-stu-id="24d84-114">And finally, your IT admin won’t get any information about any of these accounts.</span></span>

## <a name="back-up-your-account-credentials"></a><span data-ttu-id="24d84-115">Back up your account credentials</span><span class="sxs-lookup"><span data-stu-id="24d84-115">Back up your account credentials</span></span>
<span data-ttu-id="24d84-116">Before you can back up your credentials, must have both:</span><span class="sxs-lookup"><span data-stu-id="24d84-116">Before you can back up your credentials, must have both:</span></span>

- <span data-ttu-id="24d84-117">A personal [Microsoft account](https://account.microsoft.com/account) to act as your recovery account.</span><span class="sxs-lookup"><span data-stu-id="24d84-117">A personal [Microsoft account](https://account.microsoft.com/account) to act as your recovery account.</span></span>

- <span data-ttu-id="24d84-118">An [iCloud account](https://www.icloud.com/) for the actual storage location.</span><span class="sxs-lookup"><span data-stu-id="24d84-118">An [iCloud account](https://www.icloud.com/) for the actual storage location.</span></span> 

<span data-ttu-id="24d84-119">Requiring you to sign in to both accounts together provides stronger security for your backup information.</span><span class="sxs-lookup"><span data-stu-id="24d84-119">Requiring you to sign in to both accounts together provides stronger security for your backup information.</span></span>

<span data-ttu-id="24d84-120">**To turn on Cloud backup**</span><span class="sxs-lookup"><span data-stu-id="24d84-120">**To turn on Cloud backup**</span></span>
-   <span data-ttu-id="24d84-121">On your iOS device, select **Settings**, select **Backup**, and then turn on **Auto backup**.</span><span class="sxs-lookup"><span data-stu-id="24d84-121">On your iOS device, select **Settings**, select **Backup**, and then turn on **Auto backup**.</span></span>

    <span data-ttu-id="24d84-122">Your account credentials are backed up to your iCloud account.</span><span class="sxs-lookup"><span data-stu-id="24d84-122">Your account credentials are backed up to your iCloud account.</span></span>

    ![iOS settings screen, showing the location of the auto backup settings](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-turn-on.png)

## <a name="recover-your-account-credentials-on-your-new-device"></a><span data-ttu-id="24d84-124">Recover your account credentials on your new device</span><span class="sxs-lookup"><span data-stu-id="24d84-124">Recover your account credentials on your new device</span></span>
<span data-ttu-id="24d84-125">You can recover your account credentials from your iCloud account, using the same Microsoft recovery account you set up when you backed up your information.</span><span class="sxs-lookup"><span data-stu-id="24d84-125">You can recover your account credentials from your iCloud account, using the same Microsoft recovery account you set up when you backed up your information.</span></span>

### <a name="to-recover-your-information"></a><span data-ttu-id="24d84-126">To recover your information</span><span class="sxs-lookup"><span data-stu-id="24d84-126">To recover your information</span></span>
1.  <span data-ttu-id="24d84-127">On your iOS device, open the Microsoft Authenticator app, and select **Begin recovery** from the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="24d84-127">On your iOS device, open the Microsoft Authenticator app, and select **Begin recovery** from the bottom of the screen.</span></span>

    ![Microsoft Authenticator app, showing where to click Begin recovery](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-begin-recovery.png)

2.  <span data-ttu-id="24d84-129">Sign in to your recovery account, using the same personal Microsoft account you used during the backup process.</span><span class="sxs-lookup"><span data-stu-id="24d84-129">Sign in to your recovery account, using the same personal Microsoft account you used during the backup process.</span></span>

    <span data-ttu-id="24d84-130">Your account credentials are recovered to the new device.</span><span class="sxs-lookup"><span data-stu-id="24d84-130">Your account credentials are recovered to the new device.</span></span>

<span data-ttu-id="24d84-131">After you finish your recovery, you might notice that your personal Microsoft account verification codes in the Microsoft Authenticator app are different between your old and new phones.</span><span class="sxs-lookup"><span data-stu-id="24d84-131">After you finish your recovery, you might notice that your personal Microsoft account verification codes in the Microsoft Authenticator app are different between your old and new phones.</span></span> <span data-ttu-id="24d84-132">The codes are different because each device has its own unique credential, but both are valid and work while signing in using the associated phone.</span><span class="sxs-lookup"><span data-stu-id="24d84-132">The codes are different because each device has its own unique credential, but both are valid and work while signing in using the associated phone.</span></span>

## <a name="recover-additional-accounts-requiring-more-verification"></a><span data-ttu-id="24d84-133">Recover additional accounts requiring more verification</span><span class="sxs-lookup"><span data-stu-id="24d84-133">Recover additional accounts requiring more verification</span></span>
<span data-ttu-id="24d84-134">If you use push notifications with your personal, work, or school accounts, you'll get an on-screen alert that says you must provide additional verification before you can recover your information.</span><span class="sxs-lookup"><span data-stu-id="24d84-134">If you use push notifications with your personal, work, or school accounts, you'll get an on-screen alert that says you must provide additional verification before you can recover your information.</span></span> <span data-ttu-id="24d84-135">Because push notifications require using a credential that’s tied to your specific device and never sent over the network, you must prove your identity before the credential is created on your device.</span><span class="sxs-lookup"><span data-stu-id="24d84-135">Because push notifications require using a credential that’s tied to your specific device and never sent over the network, you must prove your identity before the credential is created on your device.</span></span>

<span data-ttu-id="24d84-136">For personal Microsoft accounts, you can prove your identity by entering your password along with an alternate email or phone number.</span><span class="sxs-lookup"><span data-stu-id="24d84-136">For personal Microsoft accounts, you can prove your identity by entering your password along with an alternate email or phone number.</span></span> <span data-ttu-id="24d84-137">For work or school accounts, you must scan a QR code given to you by your account provider.</span><span class="sxs-lookup"><span data-stu-id="24d84-137">For work or school accounts, you must scan a QR code given to you by your account provider.</span></span>

### <a name="to-provide-additional-verification-for-personal-accounts"></a><span data-ttu-id="24d84-138">To provide additional verification for personal accounts</span><span class="sxs-lookup"><span data-stu-id="24d84-138">To provide additional verification for personal accounts</span></span>
1.  <span data-ttu-id="24d84-139">In the **Accounts** screen of the Microsoft Authenticator app, select the drop-down arrow next to the account you want to recover.</span><span class="sxs-lookup"><span data-stu-id="24d84-139">In the **Accounts** screen of the Microsoft Authenticator app, select the drop-down arrow next to the account you want to recover.</span></span>

    ![Microsoft Authenticator app, showing the available accounts with their associated drop-down arrows](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-arrow.png)

2.  <span data-ttu-id="24d84-141">Select **Sign in to recover**, type your password, and then confirm your email address or phone number as additional verification.</span><span class="sxs-lookup"><span data-stu-id="24d84-141">Select **Sign in to recover**, type your password, and then confirm your email address or phone number as additional verification.</span></span>

    ![Microsoft Authenticator app, allowing you to enter your sign-in info](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-sign-in.png)

### <a name="to-provide-additional-verification-for-work-or-school-accounts"></a><span data-ttu-id="24d84-143">To provide additional verification for work or school accounts</span><span class="sxs-lookup"><span data-stu-id="24d84-143">To provide additional verification for work or school accounts</span></span>
1.  <span data-ttu-id="24d84-144">In the **Accounts** screen of the Microsoft Authenticator app, select the drop-down arrow next to the account you want to recover.</span><span class="sxs-lookup"><span data-stu-id="24d84-144">In the **Accounts** screen of the Microsoft Authenticator app, select the drop-down arrow next to the account you want to recover.</span></span>

    ![Microsoft Authenticator app, showing the available accounts with their associated drop-down arrows](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-additonal-accts.png)

2.  <span data-ttu-id="24d84-146">Select **Scan QR code to recover**, and then scan the QR code provided by your admin.</span><span class="sxs-lookup"><span data-stu-id="24d84-146">Select **Scan QR code to recover**, and then scan the QR code provided by your admin.</span></span>

    ![Microsoft Authenticator app, allowing you to scan your QR code](./media/microsoft-authenticator-app-backup-and-recovery/backup-and-recovery-scan-qr-code.png)

    >[!NOTE]
    ><span data-ttu-id="24d84-148">For more info about how to get a QR code, see the [How to add accounts section of the Get started with the Microsoft Authenticator app](https://docs.microsoft.com/azure/active-directory/user-help/microsoft-authenticator-app-how-to#add-accounts-to-the-app) article.</span><span class="sxs-lookup"><span data-stu-id="24d84-148">For more info about how to get a QR code, see the [How to add accounts section of the Get started with the Microsoft Authenticator app](https://docs.microsoft.com/azure/active-directory/user-help/microsoft-authenticator-app-how-to#add-accounts-to-the-app) article.</span></span>

## <a name="troubleshooting-backup-and-recovery-problems"></a><span data-ttu-id="24d84-149">Troubleshooting backup and recovery problems</span><span class="sxs-lookup"><span data-stu-id="24d84-149">Troubleshooting backup and recovery problems</span></span>
<span data-ttu-id="24d84-150">There are a few reasons why your backup might not be available:</span><span class="sxs-lookup"><span data-stu-id="24d84-150">There are a few reasons why your backup might not be available:</span></span>

-   <span data-ttu-id="24d84-151">**Changing operating systems.**</span><span class="sxs-lookup"><span data-stu-id="24d84-151">**Changing operating systems.**</span></span> <span data-ttu-id="24d84-152">Your backup is stored in the cloud storage option provided by your phone’s operating system, which means the backup is unavailable if you switch between Android and iOS.</span><span class="sxs-lookup"><span data-stu-id="24d84-152">Your backup is stored in the cloud storage option provided by your phone’s operating system, which means the backup is unavailable if you switch between Android and iOS.</span></span> <span data-ttu-id="24d84-153">In this situation, you must manually recreate your account within the app.</span><span class="sxs-lookup"><span data-stu-id="24d84-153">In this situation, you must manually recreate your account within the app.</span></span>

-   <span data-ttu-id="24d84-154">**Network or password problems.**</span><span class="sxs-lookup"><span data-stu-id="24d84-154">**Network or password problems.**</span></span> <span data-ttu-id="24d84-155">Make sure you’re connected to a network and signed into your iCloud account using the same AppleID you used on your last iPhone.</span><span class="sxs-lookup"><span data-stu-id="24d84-155">Make sure you’re connected to a network and signed into your iCloud account using the same AppleID you used on your last iPhone.</span></span>

-   <span data-ttu-id="24d84-156">**Accidental deletion.**</span><span class="sxs-lookup"><span data-stu-id="24d84-156">**Accidental deletion.**</span></span> <span data-ttu-id="24d84-157">It’s possible that you deleted your backup account from your previous device or while managing your cloud storage account.</span><span class="sxs-lookup"><span data-stu-id="24d84-157">It’s possible that you deleted your backup account from your previous device or while managing your cloud storage account.</span></span> <span data-ttu-id="24d84-158">In this situation, you must manually recreate your account within the app.</span><span class="sxs-lookup"><span data-stu-id="24d84-158">In this situation, you must manually recreate your account within the app.</span></span>

-   <span data-ttu-id="24d84-159">**Existing Microsoft Authenticator accounts.**</span><span class="sxs-lookup"><span data-stu-id="24d84-159">**Existing Microsoft Authenticator accounts.**</span></span> <span data-ttu-id="24d84-160">If you've already set up accounts in the Microsoft Authenticator app, the app won't be able to recover your backed-up accounts.</span><span class="sxs-lookup"><span data-stu-id="24d84-160">If you've already set up accounts in the Microsoft Authenticator app, the app won't be able to recover your backed-up accounts.</span></span> <span data-ttu-id="24d84-161">Preventing recovery helps ensure that your account details aren't overwritten with out-of-date information.</span><span class="sxs-lookup"><span data-stu-id="24d84-161">Preventing recovery helps ensure that your account details aren't overwritten with out-of-date information.</span></span> <span data-ttu-id="24d84-162">In this situation, you must remove any existing account information from the existing accounts set up in your Authenticator app before you can recover your backup.</span><span class="sxs-lookup"><span data-stu-id="24d84-162">In this situation, you must remove any existing account information from the existing accounts set up in your Authenticator app before you can recover your backup.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24d84-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="24d84-163">Next steps</span></span>
<span data-ttu-id="24d84-164">Now that you've backed up and recovered your account credentials to your new device, you can continue to use the Microsoft Authenticator app to verify your identity.</span><span class="sxs-lookup"><span data-stu-id="24d84-164">Now that you've backed up and recovered your account credentials to your new device, you can continue to use the Microsoft Authenticator app to verify your identity.</span></span>

## <a name="related-topics"></a><span data-ttu-id="24d84-165">Related topics</span><span class="sxs-lookup"><span data-stu-id="24d84-165">Related topics</span></span>
- [<span data-ttu-id="24d84-166">Get started with the Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="24d84-166">Get started with the Microsoft Authenticator app</span></span>](microsoft-authenticator-app-how-to.md)  

- [<span data-ttu-id="24d84-167">Microsoft Authenticator app FAQ</span><span class="sxs-lookup"><span data-stu-id="24d84-167">Microsoft Authenticator app FAQ</span></span>](microsoft-authenticator-app-faq.md)

- [<span data-ttu-id="24d84-168">Multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="24d84-168">Multi-factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/)
