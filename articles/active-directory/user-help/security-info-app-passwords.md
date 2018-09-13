---
title: Set up app passwords using security info - Azure Active Directory | Microsoft Docs
description: Set up auto-generated passwords (app passwords) to use with each non-browser app, separate from a normal password, using security info.
services: active-directory
author: eross-msft
manager: mtillman
ms.reviewer: sahenry
ms.service: active-directory
ms.workload: identity
ms.component: user-help
ms.topic: conceptual
ms.date: 07/30/2018
ms.author: lizross
ms.openlocfilehash: e527a0eaec433b96b5c37c5ec22f392a7166dfe8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868677"
---
# <a name="manage-app-passwords-using-security-info-preview"></a><span data-ttu-id="cf528-103">Manage app passwords using security info (preview)</span><span class="sxs-lookup"><span data-stu-id="cf528-103">Manage app passwords using security info (preview)</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-end-user-preview-notice-security-info.md)]

<span data-ttu-id="cf528-104">Certain non-browser apps, such as Outlook 2010, doesn't support two-step verification.</span><span class="sxs-lookup"><span data-stu-id="cf528-104">Certain non-browser apps, such as Outlook 2010, doesn't support two-step verification.</span></span> <span data-ttu-id="cf528-105">This lack of support means that if you're using two-step verification, the app won't work.</span><span class="sxs-lookup"><span data-stu-id="cf528-105">This lack of support means that if you're using two-step verification, the app won't work.</span></span> <span data-ttu-id="cf528-106">To get around this problem, you can create an auto-generated password to use with each non-browser app, separate from your normal password.</span><span class="sxs-lookup"><span data-stu-id="cf528-106">To get around this problem, you can create an auto-generated password to use with each non-browser app, separate from your normal password.</span></span>

<span data-ttu-id="cf528-107">When using app passwords, it's important to remember:</span><span class="sxs-lookup"><span data-stu-id="cf528-107">When using app passwords, it's important to remember:</span></span>

- <span data-ttu-id="cf528-108">App passwords are auto-generated and only entered once per app.</span><span class="sxs-lookup"><span data-stu-id="cf528-108">App passwords are auto-generated and only entered once per app.</span></span>

- <span data-ttu-id="cf528-109">There's a limit of 40 passwords per user.</span><span class="sxs-lookup"><span data-stu-id="cf528-109">There's a limit of 40 passwords per user.</span></span> <span data-ttu-id="cf528-110">If you try to create one after that limit, you'll be prompted to delete an existing password before being allowed to create the new one.</span><span class="sxs-lookup"><span data-stu-id="cf528-110">If you try to create one after that limit, you'll be prompted to delete an existing password before being allowed to create the new one.</span></span>

- <span data-ttu-id="cf528-111">Use one app password per device, not per app.</span><span class="sxs-lookup"><span data-stu-id="cf528-111">Use one app password per device, not per app.</span></span> <span data-ttu-id="cf528-112">For example, create a single password for all the apps on your laptop, and then another single password for all the apps on your desktop.</span><span class="sxs-lookup"><span data-stu-id="cf528-112">For example, create a single password for all the apps on your laptop, and then another single password for all the apps on your desktop.</span></span>

    >[!Note]
    ><span data-ttu-id="cf528-113">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span><span class="sxs-lookup"><span data-stu-id="cf528-113">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="cf528-114">This support means that after two-step verification is turned on, you'll no longer need app passwords for Office 2013 clients.</span><span class="sxs-lookup"><span data-stu-id="cf528-114">This support means that after two-step verification is turned on, you'll no longer need app passwords for Office 2013 clients.</span></span> <span data-ttu-id="cf528-115">For more info, see the [How modern authentication works for Office 2013 and Office 2016 client apps](https://support.office.com/article/how-modern-authentication-works-for-office-2013-and-office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) article.</span><span class="sxs-lookup"><span data-stu-id="cf528-115">For more info, see the [How modern authentication works for Office 2013 and Office 2016 client apps](https://support.office.com/article/how-modern-authentication-works-for-office-2013-and-office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) article.</span></span>

## <a name="create-and-delete-app-passwords-using-security-info"></a><span data-ttu-id="cf528-116">Create and delete app passwords using security info</span><span class="sxs-lookup"><span data-stu-id="cf528-116">Create and delete app passwords using security info</span></span>

<span data-ttu-id="cf528-117">If you use two-step verification with your work or school account and your administrator has turned on the security info experience, you can create and delete your app passwords using the My Apps portal.</span><span class="sxs-lookup"><span data-stu-id="cf528-117">If you use two-step verification with your work or school account and your administrator has turned on the security info experience, you can create and delete your app passwords using the My Apps portal.</span></span>

<span data-ttu-id="cf528-118">If your administrator hasn't turned on the security info experience, you must follow the instructions and information in the [Manage app passwords for two-step verification](multi-factor-authentication-end-user-app-passwords.md) section.</span><span class="sxs-lookup"><span data-stu-id="cf528-118">If your administrator hasn't turned on the security info experience, you must follow the instructions and information in the [Manage app passwords for two-step verification](multi-factor-authentication-end-user-app-passwords.md) section.</span></span>

### <a name="to-create-app-passwords-using-the-my-apps-portal"></a><span data-ttu-id="cf528-119">To create app passwords using the My Apps portal</span><span class="sxs-lookup"><span data-stu-id="cf528-119">To create app passwords using the My Apps portal</span></span>

1. <span data-ttu-id="cf528-120">Sign in to your work or school account.</span><span class="sxs-lookup"><span data-stu-id="cf528-120">Sign in to your work or school account.</span></span>

2. <span data-ttu-id="cf528-121">Go to myapps.microsoft.com, select your name from the upper right corner of the page, and then select **Profile**.</span><span class="sxs-lookup"><span data-stu-id="cf528-121">Go to myapps.microsoft.com, select your name from the upper right corner of the page, and then select **Profile**.</span></span>

3. <span data-ttu-id="cf528-122">In the **Manage account** area, select **Edit security info**.</span><span class="sxs-lookup"><span data-stu-id="cf528-122">In the **Manage account** area, select **Edit security info**.</span></span>

    ![Profile screen with Edit security info link highlighted](media/security-info/security-info-profile.png)

4. <span data-ttu-id="cf528-124">In the **Keep your account secure** screen, select **Add security info**.</span><span class="sxs-lookup"><span data-stu-id="cf528-124">In the **Keep your account secure** screen, select **Add security info**.</span></span>

    ![Security info screen with existing, editable info](media/security-info/security-info-edit-add-info.png)

5. <span data-ttu-id="cf528-126">In the **Add security info** screen, select **App password**.</span><span class="sxs-lookup"><span data-stu-id="cf528-126">In the **Add security info** screen, select **App password**.</span></span>

6. <span data-ttu-id="cf528-127">In the **Create your app password** screen, type a name for your app password, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="cf528-127">In the **Create your app password** screen, type a name for your app password, and then select **Next**.</span></span>

    ![Screen where you name your app password](media/security-info/security-info-name-app-password.png)

7. <span data-ttu-id="cf528-129">Select **Copy** to copy the password to clipboard, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="cf528-129">Select **Copy** to copy the password to clipboard, and then select **Next**.</span></span>

    ![Screen with app password for copying](media/security-info/security-info-create-app-password.png)
    
8. <span data-ttu-id="cf528-131">Make sure the app password appears on the **Keep your account secure** screen.</span><span class="sxs-lookup"><span data-stu-id="cf528-131">Make sure the app password appears on the **Keep your account secure** screen.</span></span>

    ![Keep secure screen, with app password](media/security-info/security-info-keep-secure-app-password.png)

### <a name="to-delete-app-passwords-using-the-my-apps-portal"></a><span data-ttu-id="cf528-133">To delete app passwords using the My Apps portal</span><span class="sxs-lookup"><span data-stu-id="cf528-133">To delete app passwords using the My Apps portal</span></span>

1. <span data-ttu-id="cf528-134">On the **Keep your account secure** screen, select the **X** next to the app password to delete.</span><span class="sxs-lookup"><span data-stu-id="cf528-134">On the **Keep your account secure** screen, select the **X** next to the app password to delete.</span></span>

    ![Keep secure screen, delete app password](media/security-info/security-info-keep-secure-delete-app-password.png)

2. <span data-ttu-id="cf528-136">In the **Delete application password** screen, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="cf528-136">In the **Delete application password** screen, select **Delete**.</span></span>

    ![Delete app password screen](media/security-info/security-info-keep-secure-delete-app-password2.png)

## <a name="next-steps"></a><span data-ttu-id="cf528-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf528-138">Next steps</span></span>

- <span data-ttu-id="cf528-139">If you need to update your security info, follow the instructions in the [Manage your security info](security-info-manage-settings.md) article.</span><span class="sxs-lookup"><span data-stu-id="cf528-139">If you need to update your security info, follow the instructions in the [Manage your security info](security-info-manage-settings.md) article.</span></span>

- <span data-ttu-id="cf528-140">For more general info about security info and what you can do, see [Security info overview](user-help-security-info-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cf528-140">For more general info about security info and what you can do, see [Security info overview](user-help-security-info-overview.md)</span></span> 