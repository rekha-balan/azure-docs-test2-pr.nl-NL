---
title: 'Azure AD: Self-service password reset registration | Microsoft Docs'
description: Register authentication data for self-service password reset
services: active-directory
keywords: Active directory password management, password management, Azure AD self service password reset, SSPR
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/16/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: c21a3b1dd7c7e324997b67f371d6ae606a95019a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551970"
---
# <a name="register-for-self-service-password-reset"></a><span data-ttu-id="cb153-104">Register for self-service password reset</span><span class="sxs-lookup"><span data-stu-id="cb153-104">Register for self-service password reset</span></span>

<span data-ttu-id="cb153-105">As an end user if your administrator has enabled it, you can reset your password or unlock you account without having to speak to a person using self-service password reset (SSPR).</span><span class="sxs-lookup"><span data-stu-id="cb153-105">As an end user if your administrator has enabled it, you can reset your password or unlock you account without having to speak to a person using self-service password reset (SSPR).</span></span> <span data-ttu-id="cb153-106">Before you can use this functionality, you have to register authentication methods or confirm the predefined authentication methods your administrator has populated.</span><span class="sxs-lookup"><span data-stu-id="cb153-106">Before you can use this functionality, you have to register authentication methods or confirm the predefined authentication methods your administrator has populated.</span></span>

## <a name="register-or-confirm-authentication-data-with-sspr"></a><span data-ttu-id="cb153-107">Register or confirm authentication data with SSPR</span><span class="sxs-lookup"><span data-stu-id="cb153-107">Register or confirm authentication data with SSPR</span></span>

1. <span data-ttu-id="cb153-108">Open the web browser on your device and go to the [password reset registration page](http://aka.ms/ssprsetup)</span><span class="sxs-lookup"><span data-stu-id="cb153-108">Open the web browser on your device and go to the [password reset registration page](http://aka.ms/ssprsetup)</span></span>
2. <span data-ttu-id="cb153-109">Enter your username and password provided by your administrator</span><span class="sxs-lookup"><span data-stu-id="cb153-109">Enter your username and password provided by your administrator</span></span>
3. <span data-ttu-id="cb153-110">Depending on the options your administrator has approved, you will see one or more of the following items for you to configure or verify to be used if you need to reset your password</span><span class="sxs-lookup"><span data-stu-id="cb153-110">Depending on the options your administrator has approved, you will see one or more of the following items for you to configure or verify to be used if you need to reset your password</span></span>
    * <span data-ttu-id="cb153-111">Office phone - This option is only able to be set by your administrator</span><span class="sxs-lookup"><span data-stu-id="cb153-111">Office phone - This option is only able to be set by your administrator</span></span>
    * <span data-ttu-id="cb153-112">Authentication Phone - This option should be set to another phone number you would have access to like a cell phone that can receive a text or call (Your administrator may populate this for you with your cell phone number if they already have your permission to use that information)</span><span class="sxs-lookup"><span data-stu-id="cb153-112">Authentication Phone - This option should be set to another phone number you would have access to like a cell phone that can receive a text or call (Your administrator may populate this for you with your cell phone number if they already have your permission to use that information)</span></span>
    * <span data-ttu-id="cb153-113">Authentication Email - This option should be set to an alternative email address that you can access without the password you need to reset</span><span class="sxs-lookup"><span data-stu-id="cb153-113">Authentication Email - This option should be set to an alternative email address that you can access without the password you need to reset</span></span>
    * <span data-ttu-id="cb153-114">Security Questions - This option gives you a list of questions your administrator has approved for you to answer.</span><span class="sxs-lookup"><span data-stu-id="cb153-114">Security Questions - This option gives you a list of questions your administrator has approved for you to answer.</span></span> <span data-ttu-id="cb153-115">You may not use the same answer for more than one question.</span><span class="sxs-lookup"><span data-stu-id="cb153-115">You may not use the same answer for more than one question.</span></span>
4. <span data-ttu-id="cb153-116">Provide and verify the information required by your administrator.</span><span class="sxs-lookup"><span data-stu-id="cb153-116">Provide and verify the information required by your administrator.</span></span> <span data-ttu-id="cb153-117">If more than one option is available we suggest that you register multiple methods to provide flexibility when another method is unavailable (Example: Traveling and unable to access your office phone)</span><span class="sxs-lookup"><span data-stu-id="cb153-117">If more than one option is available we suggest that you register multiple methods to provide flexibility when another method is unavailable (Example: Traveling and unable to access your office phone)</span></span>

    <span data-ttu-id="cb153-118">![Register authentication methods and click finish][Register]</span><span class="sxs-lookup"><span data-stu-id="cb153-118">![Register authentication methods and click finish][Register]</span></span>

5. <span data-ttu-id="cb153-119">When done with step 4 choose **finish** and you will now be able to use self-service password reset when you need to in the future.</span><span class="sxs-lookup"><span data-stu-id="cb153-119">When done with step 4 choose **finish** and you will now be able to use self-service password reset when you need to in the future.</span></span>

<span data-ttu-id="cb153-120">If you enter data in the Authentication Phone or Authentication Email, it is not visible in the global directory.</span><span class="sxs-lookup"><span data-stu-id="cb153-120">If you enter data in the Authentication Phone or Authentication Email, it is not visible in the global directory.</span></span> <span data-ttu-id="cb153-121">The only people who can see this data are you and your administrators.</span><span class="sxs-lookup"><span data-stu-id="cb153-121">The only people who can see this data are you and your administrators.</span></span> <span data-ttu-id="cb153-122">Only you can see the answers to your Security Questions.</span><span class="sxs-lookup"><span data-stu-id="cb153-122">Only you can see the answers to your Security Questions.</span></span>

<span data-ttu-id="cb153-123">Administrators may require you to confirm your authentication methods after a period of time to make sure you still have the appropriate methods registered.</span><span class="sxs-lookup"><span data-stu-id="cb153-123">Administrators may require you to confirm your authentication methods after a period of time to make sure you still have the appropriate methods registered.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb153-124">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cb153-124">Next Steps</span></span>

* [<span data-ttu-id="cb153-125">How to change your password using self-service password reset</span><span class="sxs-lookup"><span data-stu-id="cb153-125">How to change your password using self-service password reset</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="cb153-126">Password reset registration page</span><span class="sxs-lookup"><span data-stu-id="cb153-126">Password reset registration page</span></span>](http://aka.ms/ssprsetup)
* [<span data-ttu-id="cb153-127">Password reset portal</span><span class="sxs-lookup"><span data-stu-id="cb153-127">Password reset portal</span></span>](https://passwordreset.microsoftonline.com/)

[Register]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-reset-register/register-2-methods.png "Password reset registration page showing registered methods and finish button"

